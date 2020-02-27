---
title: 扩展方法
description: Learn how to add to existing APIs.
---
在 Dart 2.7 中引入的扩展方法是一种向现有库添加功能的方法。
您可能在不知道的情况下使用扩展方法。
例如，当您在 IDE 中使用代码补全时，
它会建议使用扩展方法和常规方法。

<iframe width="560" height="315"
  src="https://www.youtube.com/embed/D3j0OSfT9ZI"
  frameborder="0"
  allow="accelerometer; encrypted-media; gyroscope; picture-in-picture"
  allowfullscreen>
</iframe>
<em>如果您喜欢通过看视频来学习，
这里有一个扩展方法的概览。</em>


## 概览

当您使用别人的 API 或实现一个广泛使用的库时，
更改 API 通常是不切实际或不可能的。
但是您可能仍然想向一个已有库中添加新功能。

例如，下面是一个将字符串解析为整数的代码：

```dart
int.parse('42')
```

如果将这一功能加在 `String` 上可能会更好
（代码更短，更易于使用）：

```dart
'42'.parseInt()
```

如果想让上面的代码生效，
需要导入一个包含 `String` 类扩展的库：

<?code-excerpt "extension_methods/lib/string_extensions/usage_simple_extension.dart (basic)" replace="/  print/print/g"?>
```dart
import 'string_apis.dart';
// ···
print('42'.parseInt()); // 使用扩展方法。
```

扩展不仅可以定义方法，还可以定义其他成员，
例如 Getter、Setter 和 运算符。
另外，扩展有名字，如果出现 API 冲突，这将很有帮助。
您可以通过使用 对字符串进行操作 的扩展（名为 `NumberParsing` ）
来实现扩展方法 `parseInt()` ：

<?code-excerpt "extension_methods/lib/string_extensions/string_apis.dart (parseInt)"?>
```dart
extension NumberParsing on String {
  int parseInt() {
    return int.parse(this);
  }
  // ···
}
```
<div class="prettify-filename">lib/string_apis.dart</div>

下一节将介绍如何 _使用_ 扩展方法。
再之后是介绍如何 _实现_ 扩展方法。


## 使用扩展方法

与所有 Dart 代码一样，扩展方法也在库中。
您已经了解了如何使用扩展方法，
只需导入它所在的库，并像使用普通方法一样使用它：

<?code-excerpt "extension_methods/lib/string_extensions/usage_simple_extension.dart (import-and-use)" replace="/  print/print/g"?>
```dart
// 导入一个包含 String 扩展的库。
import 'string_apis.dart';
// ···
print('42'.padLeft(5)); // 使用 String 普通方法。
print('42'.parseInt()); // 使用 String 扩展方法。
```

这就是使用扩展方法通常需要知道的全部内容。
在编写代码时，
您可能还需要了解扩展方法是如何依赖于静态类型（而不是 `dynamic`）
以及如何解决 [API 冲突](#API-冲突)。

### 静态类型和 dynamic

您不能用 `dynamic` 类型的变量调用扩展方法。
例如，下面的代码会导致运行时异常：

<?code-excerpt "extension_methods/lib/string_extensions/usage_simple_extension.dart (dynamic)" plaster="none" replace="/  \/\/ print/print/g"?>
```dart
dynamic d = '2';
print(d.parseInt()); // Runtime exception: NoSuchMethodError
```

扩展方法可以与 Dart 的类型推断配合使用。
以下代码可以运行，因为变量 `v` 被推断为 `String` 类型：

<?code-excerpt "extension_methods/lib/string_extensions/usage_simple_extension.dart (var)"?>
```dart
var v = '2';
print(v.parseInt()); // Output: 2
```

`dynamic` 无法使用扩展方法的原因是
扩展方法是根据接收方的静态类型解析的。
因为扩展方法是静态解析的，
所以它们与调用静态函数一样快。

有关静态类型和 `dynamic` 的更多信息，请参考
[Dart 类型系统](/guides/language/sound-dart) 。

### API 冲突

如果一个扩展成员 与 一个接口或另一个扩展成员冲突，
那么您有几个选择。

一种选择是改变导入冲突扩展的方式，
使用 `show` 或 `hide` 来限制暴露的 API：

<?code-excerpt "extension_methods/lib/string_extensions/usage_import.dart" replace="/  //g"?>
```dart
// Defines the String extension method parseInt().
import 'string_apis.dart';

// Also defines parseInt(), but hiding NumberParsing2
// hides that extension method.
import 'string_apis_2.dart' hide NumberParsing2;

// ···
// Uses the parseInt() defined in 'string_apis.dart'.
print('42'.parseInt());
```

另一种选择是显式地应用扩展，
这会导致代码看起来像是一个包装类:

<?code-excerpt "extension_methods/lib/string_extensions/usage_explicit.dart" replace="/  //g"?>
```dart
// Both libraries define extensions on String that contain parseInt(),
// and the extensions have different names.
import 'string_apis.dart'; // Contains NumberParsing extension.
import 'string_apis_2.dart'; // Contains NumberParsing2 extension.

// ···
// print('42'.parseInt()); // Doesn't work.
print(NumberParsing('42').parseInt());
print(NumberParsing2('42').parseInt());
```

如果两个扩展同名，
则可能需要使用前缀导入：

<?code-excerpt "extension_methods/lib/string_extensions/usage_prefix.dart" replace="/  //g"?>
```dart
// Both libraries define extensions named NumberParsing
// that contain the extension method parseInt(). One NumberParsing
// extension (in 'string_apis_3.dart') also defines parseNum().
import 'string_apis.dart';
import 'string_apis_3.dart' as rad;

// ···
// print('42'.parseInt()); // Doesn't work.

// Use the ParseNumbers extension from string_apis.dart.
print(NumberParsing('42').parseInt());

// Use the ParseNumbers extension from string_apis_3.dart.
print(rad.NumberParsing('42').parseInt());

// Only string_apis_3.dart has parseNum().
print('42'.parseNum());
```

如示例所示，
即使使用前缀导入，也可以隐式调用扩展方法。
只有在显式地调用扩展且出现名称冲突时才需要使用前缀。


## 实现扩展方法

使用下面的语法创建扩展：

```
extension <extension name> on <type> {
  (<member definition>)*
}
```

例如，您可以通过以下方式在 `String` 类上实现一个扩展：

<?code-excerpt "extension_methods/lib/string_extensions/string_apis.dart"?>
```dart
extension NumberParsing on String {
  int parseInt() {
    return int.parse(this);
  }

  double parseDouble() {
    return double.parse(this);
  }
}
```
<div class="prettify-filename">lib/string_apis.dart</div>

要创建一个只在自己库中可见的本地扩展，
可以省略扩展名称
或给它一个以下划线 (`_`) 开头的名称。

扩展的成员可以是方法、Getter、Setter、运算符。
扩展也可以有静态字段和静态助手方法。

## 实现泛型扩展

扩展可以具有泛型类型参数。
例如，下面的代码使用 Getter、运算符和方法
扩展了内置的 `List<T>` 类型：

<?code-excerpt "extension_methods/lib/fancylist.dart"?>
```dart
extension MyFancyList<T> on List<T> {
  int get doubleLength => length * 2;
  List<T> operator -() => reversed.toList();
  List<List<T>> split(int at) => <List<T>>[sublist(0, at), sublist(at)];
}
```

类型 `T` 是基于调用方法的 list 的静态类型来绑定的。
{% comment %}
TODO (https://github.com/dart-lang/site-www/issues/2171):
Add more info about generic extensions. 
For example, in the following code, `T` is `PENDING` because PENDING:

[PENDING: example]

[PENDING: Explain why it matters in normal usage.]
{% endcomment %}

## 资源

有关扩展方法的更多信息，请参见以下内容：

* [Article: Dart Extension Methods Fundamentals][article]
* [Feature specification][specification]

{% comment %}
* Video
* 2.7 blog post?
* Release notes?
* Examples?
{% endcomment %}

[specification]: https://github.com/dart-lang/language/blob/master/accepted/2.6/static-extension-members/feature-specification.md#dart-static-extension-methods-design

[article]: https://medium.com/dartlang/extension-methods-2d466cd8b308
