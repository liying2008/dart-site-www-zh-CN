---
title: Dart 语言概览
description: A tour of all of the major Dart language features.
short-title: Language tour
---
<?code-excerpt replace="/ *\/\/\s+ignore_for_file:[^\n]+\n//g; / *\/\/\s+ignore:[^\n]+//g; /([A-Z]\w*)\d\b/$1/g"?>

在假定您已经知道如何使用另一种语言进行编程的情况下，
此页面将向您展示如何使用 Dart 的各个主要功能，从变量、运算符到类、库。 有关该语言的简要介绍，请参见
[语言示例页面](/samples)。

要了解更多关于 Dart 核心库的信息，请参阅
[库概览](/guides/libraries/library-tour)。
如果您需要获取关于语言特性更详细的内容，请查阅 
[Dart language specification][]。

{{site.alert.note}}
  您可以使用 DartPad 来体验大部分 Dart 语言的特性
  ([learn more](/tools/dartpad))。
  **<a href="{{ site.dartpad }}" target="_blank">Open DartPad</a>**

  此页面使用嵌入式 DartPads 显示一些示例。
  {% include dartpads-embedded-troubleshooting.md %}
{{site.alert.end}}


## 一个基础的 Dart 程序

下面的代码用到了很多 Dart 语言的基础特性:

<?code-excerpt "misc/test/language_tour/basic_test.dart"?>
```dart
// 定义一个函数.
printInteger(int aNumber) {
  print('The number is $aNumber.'); // 打印到控制台.
}

// 应用执行入口.
main() {
  var number = 42; // 声明并初始化一个变量.
  printInteger(number); // 调用函数.
}
```
此程序使用到的语言特性也适用于所有（或大多数）Dart 应用程序：

<code>// <em>这是一个注释。</em> </code>
:   单行注释。
    Dart 也支持多行注释和文档注释。
    详细内容请参考 [Comments](#comments)。

`int`
:   类型。一些其他的 [内置类型](#built-in-types)
    如 `String`, `List`, and `bool`。

`42`
:   数字字面量。 数字字面量是一种编译期常量。

`print()`
:   显示输出的一种便捷方法。

`'...'` (或者 `"..."`)
:   字符串字面量。

<code>$<em>变量名</em></code> (or <code>${<em>表达式</em>}</code>)
:   字符串插值：即在字符串字面量中包含变量或表达式。更多信息，请参考
    [Strings](#strings)。

`main()`
:   一个特殊的、 *必需的*、 顶层函数。它是应用程序执行的入口。
    更多信息，请参考
    [The main() function](#the-main-function)。

`var`
:   一种用于声明变量且无需指定变量类型的方法。

{{site.alert.note}}
  该网站的代码遵循
  [Dart 风格指南](/guides/language/effective-dart/style)
  中的约定。
{{site.alert.end}}


## 重要概念

在学习 Dart 语言时，请牢记以下事实和概念：

-   所有变量引用的都是 *对象* ，每个对象都是一个 *类* 的实例。 
    数字、函数和 null 都是对象。
    所有类都从 [Object][] 类继承。

-   尽管 Dart 是强类型语言，但是声明变量时可以不指定类型，因为 Dart 可以推断类型。 
    在上面的代码中，变量 `number` 的类型被推断为 `int`。
    如果想显式地声明一个不确定的类型，请
    [使用特殊类型 `dynamic`][ObjectVsDynamic]。

-   Dart 支持泛型， 例如 `List<int>` （由 int 类型对象组成的 list）
    或者 `List<dynamic>` （由任何类型的对象组成的 list）。

-   Dart 支持顶层函数 （例如 `main()`），也支持定义依附于类或对象的函数
    （*静态方法* 和 *实例方法*）。你也可以在一个函数中定义一个函数
    （*嵌套函数* 或 *局部函数*）。

-   类似地，Dart 支持顶层 *变量*， 也支持依附于类或对象的变量
    （静态变量 和 实例变量）。
    实例变量有时也被称为字段或属性。

-   与 Java 不同， Dart 没有 `public`、`protected` 和 `private` 这些访问修饰符。
    如果一个标识符以下划线 (\_) 开头，那它在库内就是私有的。
    更多信息，请参考
    [库和可见性](#libraries-and-visibility)。

-   *标识符* 可以以字母或下划线 (\_) 开头，后跟字母、下划线和数字的任意组合。

-   Dart 既有 *表达式* （具有运行时值） 也有 *语句* （没有运行时值）。
    例如，一个 [条件表达式](#conditional-expressions)
    `condition ? expr1 : expr2` 具有值 `expr1` 或 `expr2`。
    相比之下 [if-else 语句](#if-and-else) 没有值。
    一条语句通常包含一个或多个表达式，
    但是一个表达式不能只包含一条语句。

-   Dart 工具可以报告两种类型的问题： _警告_ 和 _错误_ 。
    警告仅表示您的代码可能无法工作，但并不会阻止程序运行。
    错误分为 编译期错误 和 运行期错误。编译期错误会直接导致程序无法执行，
    运行期错误会在代码执行时抛出[异常](#exceptions)。


## 关键字

下面表格列出了 Dart 语言中的关键字。

{% assign ckw = '&nbsp;<sup title="contextual keyword" alt="contextual keyword">1</sup>' %}
{% assign bii = '&nbsp;<sup title="built-in-identifier" alt="built-in-identifier">2</sup>' %}
{% assign lrw = '&nbsp;<sup title="limited reserved word" alt="limited reserved word">3</sup>' %}
| [abstract][]{{bii}}   | [dynamic][]{{bii}}    | [implements][]{{bii}} | [show][]{{ckw}}   |
| [as][]{{bii}}         | [else][]              | [import][]{{bii}}     | [static][]{{bii}} |
| [assert][]            | [enum][]              | [in][]                | [super][]         |
| [async][]{{ckw}}      | [export][]{{bii}}     | [interface][]{{bii}}  | [switch][]        |
| [await][]{{lrw}}      | [extends][]           | [is][]                | [sync][]{{ckw}}   |
| [break][]             | [external][]{{bii}}   | [library][]{{bii}}    | [this][]          |
| [case][]              | [factory][]{{bii}}    | [mixin][]{{bii}}      | [throw][]         |
| [catch][]             | [false][]             | [new][]               | [true][]          |
| [class][]             | [final][]             | [null][]              | [try][]           |
| [const][]             | [finally][]           | [on][]{{ckw}}         | [typedef][]{{bii}}|
| [continue][]          | [for][]               | [operator][]{{bii}}   | [var][]           |
| [covariant][]{{bii}}  | [Function][]{{bii}}   | [part][]{{bii}}       | [void][]          |
| [default][]           | [get][]{{bii}}        | [rethrow][]           | [while][]         |
| [deferred][]{{bii}}   | [hide][]{{ckw}}       | [return][]            | [with][]          |
| [do][]                | [if][]                | [set][]{{bii}}        | [yield][]{{lrw}}  |
{:.table .table-striped .nowrap}

[abstract]: #abstract-classes
[as]: #type-test-operators
[assert]: #assert
[async]: #asynchrony-support
[await]: #asynchrony-support
[break]: #break-and-continue
[case]: #switch-and-case
[catch]: #catch
[class]: #instance-variables
[const]: #final-and-const
{% comment %}
  [TODO: Make sure that points to a place that talks about const constructors,
  as well as const literals and variables.]
{% endcomment %}
[continue]: #break-and-continue
[covariant]: /guides/language/sound-problems#the-covariant-keyword
[default]: #switch-and-case
[deferred]: #lazily-loading-a-library
[do]: #while-and-do-while
[dynamic]: #important-concepts
[else]: #if-and-else
[enum]: #enumerated-types
[export]: /guides/libraries/create-library-packages
[extends]: #extending-a-class
[external]: https://stackoverflow.com/questions/24929659/what-does-external-mean-in-dart
[factory]: #factory-constructors
[false]: #booleans
[final]: #final-and-const
[finally]: #finally
[for]: #for-loops
[Function]: #functions
[get]: #getters-and-setters
[hide]: #importing-only-part-of-a-library
[if]: #if-and-else
[implements]: #implicit-interfaces
[import]: #using-libraries
[in]: #for-loops
[interface]: https://stackoverflow.com/questions/28595501/was-the-interface-keyword-removed-from-dart
[is]: #type-test-operators
[library]: #libraries-and-visibility
[mixin]: #adding-features-to-a-class-mixins
[new]: #using-constructors
[null]: #default-value
[on]: #catch
[operator]: #overridable-operators
[part]: /guides/libraries/create-library-packages#organizing-a-library-package
[rethrow]: #catch
[return]: #functions
[set]: #getters-and-setters
[show]: #importing-only-part-of-a-library
[static]: #class-variables-and-methods
[super]: #extending-a-class
[switch]: #switch-and-case
[sync]: #generators
[this]: #constructors
[throw]: #throw
[true]: #booleans
[try]: #catch
[typedef]: #typedefs
[var]: #variables
[void]: https://medium.com/dartlang/dart-2-legacy-of-the-void-e7afb5f44df0
{% comment %}
  TODO: Add coverage of void to the language tour.
{% endcomment %}
[with]: #adding-features-to-a-class-mixins
[while]: #while-and-do-while
[yield]: #generators

应避免将这些关键字用作标识符。
但是，如有必要，标有上标的关键字某些情况下可以用作标识符：

* 标有上标 **1** 的关键字是 **上下文关键字**，
  只有在特定的地方才有意义。
  它们在任何地方都是有效的标识符。

* 带有上标 **2** 的单词是 **内置标识符**。 
  为了简化将 JavaScript 代码移植到 Dart 中的工作，
  这些关键字在大多数地方都是有效的标识符，
  但它们不能用作类或类型名，也不能用作导入前缀。

* 带有上标 **3** 的单词是较新的、有限的保留单词，
  它们与 Dart 1.0 版本之后添加的 [异步支持](#asynchrony-support)有关。
  您不能在任何标有 `async`、 `async*` 或 `sync*` 的函数体中使用 `await` 或 `yield` 作为标识符。

表格中的所有其他单词均为 **保留字**，不能用作标识符。


## 变量

下面是一个创建变量并初始化的例子：

<?code-excerpt "misc/lib/language_tour/variables.dart (var-decl)"?>
```dart
var name = 'Bob';
```

变量仅存储对象的引用。
这里名为 `name` 的变量存储了一个 `String` 对象的引用，而对象的值为 “Bob”。

`name` 变量的类型被推断为 `String`，
但是您可以通过指定类型来更改它。
如果一个对象不局限于单一的类型，
则可以根据[设计指南][ObjectVsDynamic]指定其为 `Object` 或 `dynamic` 类型。

{% comment %}
**[PENDING: check on Object vs. dynamic guidance.]**
{% endcomment %}

<?code-excerpt "misc/lib/language_tour/variables.dart (type-decl)"?>
```dart
dynamic name = 'Bob';
```

除此之外您也可以指定类型：

<?code-excerpt "misc/lib/language_tour/variables.dart (static-types)"?>
```dart
String name = 'Bob';
```

{{site.alert.note}}
  本文遵循
  [风格建议指南](/guides/language/effective-dart/design#types)
  中的建议，
  使用 `var` 声明局部变量，而非使用指定的类型。
{{site.alert.end}}


### 默认值

未初始化的变量都会有一个初始值：`null`。
即使是数字类型也是如此，因为在 Dart 中一切皆为对象，数字也不例外。

<?code-excerpt "misc/test/language_tour/variables_test.dart (var-null-init)"?>
```dart
int lineCount;
assert(lineCount == null);
```

{{site.alert.note}}
  生产环境代码将忽略 `assert()` 调用。
  在开发环境中，如果 _condition_ 为 false，则 <code>assert(<em>condition</em>)</code> 将会抛出一个异常。
  更多信息，请参考 [断言](#assert)。
{{site.alert.end}}

### Final 和 const

如果您不打算更改一个变量，可以使用 `final` 或 `const` 来修饰它，
这两个关键字可以代替 `var` 或者加在一个具体的类型前。
一个 final 变量只可以被赋值一次； 一个 const 变量是一个编译期常量。
（const 变量同时也是 final 的。）顶层的 final 变量或者类的 final 变量在其第一次使用的时候被初始化。

{{site.alert.note}}
  实例变量可以是 `final` 的但不能是 `const` 的。
  final 实例变量必须在构造函数主体开始之前初始化，
  比如在声明实例变量时初始化，或者作为构造器参数，或者将其置于构造器的 
  [初始化列表](#initializer-list) 中。
{{site.alert.end}}

下面是一个创建并初始化 final 变量的例子：

<?code-excerpt "misc/lib/language_tour/variables.dart (final)"?>
```dart
final name = 'Bob'; // 没有类型标注
final String nickname = 'Bobby';
```

您不能修改一个 final 变量的值：

{:.fails-sa}
<?code-excerpt "misc/lib/language_tour/variables.dart (cant-assign-to-final)"?>
```dart
name = 'Alice'; // 错误：final 变量只能被赋值一次
```

使用 `const` 修饰的变量为 **编译期常量**。
如果使用 const 修饰类中的变量，则必须加上 `static` 关键字，即 `static const`。
声明 const 变量，须将其值设置为编译期常数，例如数字或字符串字面量、const 变量或对常数进行算术运算的结果：

<?code-excerpt "misc/lib/language_tour/variables.dart (const)"?>
```dart
const bar = 1000000; // Unit of pressure (dynes/cm2)
const double atm = 1.01325 * bar; // Standard atmosphere
```

`const` 关键字不止可以用来声明常量，
还可以用来创建常量 _值_ 。
你也可以将构造函数声明为 const 的，
这种类型的构造函数 _创建_ 的对象是不可改变的。

<?code-excerpt "misc/lib/language_tour/variables.dart (const-vs-final)"?>
```dart
var foo = const [];
final bar = const [];
const baz = []; // 等价于 `const []`
```

如果使用初始化表达式为常量赋值可以省略掉 `const` 关键字，
比如上面的 `baz` 常量的赋值就省略了 `const`。
更多信息，请参考 [DON’T use const redundantly][]。

没有使用 final 和 const 修饰的变量的值是可以被更改的，即使这些变量之前引用过 const 的值：

<?code-excerpt "misc/lib/language_tour/variables.dart (reassign-to-non-final)"?>
```dart
foo = [1, 2, 3]; // foo 的值之前为 const []
```

常量的值不可以被修改：

{:.fails-sa}
<?code-excerpt "misc/lib/language_tour/variables.dart (cant-assign-to-const)"?>
```dart
baz = [42]; // 错误: 常量不能被赋值
```

从 Dart 2.5 开始，您可以在常量中使用
[类型检查和强制类型转换](#type-test-operators) (`is` and `as`)，
[collection if](#collection-operators)
以及 [展开操作符](#spread-operator) (`...` and `...?`)：

<?code-excerpt "misc/lib/language_tour/variables.dart (const-dart-25)"?>
```dart
// 从 Dart 2.5 开始，以下都是合法的编译期常量
const Object i = 3; // Where i is a const Object with an int value...
const list = [i as int]; // Use a typecast.
const map = {if (i is int) i: "int"}; // Use is and collection if.
const set = {if (list is List<int>) ...list}; // ...and a spread.
```
更多关于使用 `const` 创建常量值的信息，请参考
[Lists](#lists)、[Maps](#maps) 和 [Classes](#classes)。


## 内置类型

Dart 语言对以下类型提供特殊支持：

- numbers
- strings
- booleans
- lists (也称为 *arrays*)
- sets
- maps
- runes (用于在字符串中表示 Unicode 字符)
- symbols

您可以直接使用字面量来初始化上述类型。
例如，`'this is a string'` 是一个 string 字面量，
`true` 是一个 boolean 字面量。

{% comment %}
PENDING: add info about support for Iterable, Future, Stream?
Those can't be initialized using literals, but they do have special support.
{% endcomment %}

由于 Dart 中每个变量都引用一个对象（一个 *类* 的实例），
您通常也可以使用 *构造器* 来初始化变量。
一些内置的类型有它们自己的构造器。
例如你可以使用 `Map()` 来创建一个 map 对象。


### Numbers

Dart 支持两种 Number 类型：

[int][]

:   整数值，长度不超过64位，取决于平台（即：取值范围与平台有关）。
    在 Dart VM 中，其取值范围为
    -2<sup>63</sup> 到 2<sup>63</sup> - 1 。
    编译成 Javascript 将会使用
    [JavaScript numbers,][js numbers]
    允许的取值范围为：-2<sup>53</sup> to 2<sup>53</sup> - 1 。

{% comment %}
[PENDING: What about values on Android & iOS?
The informal spec is at
https://github.com/dart-lang/sdk/blob/master/docs/language/informal/int64.md.
{% endcomment %}

[double][]

:   64位（双精度）浮点数，由 IEEE 754 标准指定。

`int` 和 `double` 都是 [`num`][num] 的子类。
num 类中定义了一些基本的操作符，如 +、 -、 / 、 \* 等，
以及一些诸如 `abs()`、` ceil()`、
、 `floor()` 的方法.
（位运算符，如 \>\>，在 `int` 类中定义。）
如果 num 和其子类 不能满足您的要求，您还可以查看
[dart:math][] 库中的API。

整数是不含小数点的数字，下面是一些定义整数字面量的例子：

<?code-excerpt "misc/lib/language_tour/built_in_types.dart (integer-literals)"?>
```dart
var x = 1;
var hex = 0xDEADBEEF;
```

如果一个数字包含小数，那它就是 double 类型的。
下面是一些定义 double 字面量的例子：

<?code-excerpt "misc/lib/language_tour/built_in_types.dart (double-literals)"?>
```dart
var y = 1.1;
var exponents = 1.42e5;
```

从 Dart 2.1 开始，int 字面量将会在必要的时候自动转换成 double 字面量：

<?code-excerpt "misc/lib/language_tour/built_in_types.dart (int-to-double)"?>
```dart
double z = 1; // 等效于 double z = 1.0.
```

{{site.alert.version-note}}
  在 Dart 2.1 之前，在 double 上下文中使用 int 字面量是错误的。
{{site.alert.end}}

下面是字符串和数字之间转换的方式：

<?code-excerpt "misc/test/language_tour/built_in_types_test.dart (number-conversion)"?>
```dart
// String -> int
var one = int.parse('1');
assert(one == 1);

// String -> double
var onePointOne = double.parse('1.1');
assert(onePointOne == 1.1);

// int -> String
String oneAsString = 1.toString();
assert(oneAsString == '1');

// double -> String
String piAsString = 3.14159.toStringAsFixed(2);
assert(piAsString == '3.14');
```

int 类型支持传统的位移操作：(\<\<, \>\>)、 AND(&)、 OR (|)。例如:

<?code-excerpt "misc/test/language_tour/built_in_types_test.dart (bit-shifting)"?>
```dart
assert((3 << 1) == 6); // 0011 << 1 == 0110
assert((3 >> 1) == 1); // 0011 >> 1 == 0001
assert((3 | 4) == 7); // 0011 | 0100 == 0111
```

数字字面量是编译期常量。
很多算术表达式只要其操作数是常量，则表达式结果也是编译期常量。

<?code-excerpt "misc/lib/language_tour/built_in_types.dart (const-num)"?>
```dart
const msPerSecond = 1000;
const secondsUntilRetry = 5;
const msUntilRetry = secondsUntilRetry * msPerSecond;
```


### Strings

Dart 字符串是 UTF-16 编码的字符序列。
可以使用单引号或双引号来创建字符串：

<?code-excerpt "misc/lib/language_tour/built_in_types.dart (quoting)"?>
```dart
var s1 = 'Single quotes work well for string literals.';
var s2 = "Double quotes work just as well.";
var s3 = 'It\'s easy to escape the string delimiter.';
var s4 = "It's even easier to use the other delimiter.";
```

可以在字符串中以 `${`*`表达式`*`}` 的形式使用表达式。
如果表达式是一个标识符，可以省略掉 {}。
如果表达式的结果是一个对象，则 Dart 会调用该对象的 `toString()` 方法来获取一个字符串。

<?code-excerpt "misc/test/language_tour/built_in_types_test.dart (string-interpolation)"?>
```dart
var s = 'string interpolation';

assert('Dart has $s, which is very handy.' ==
    'Dart has string interpolation, ' +
        'which is very handy.');
assert('That deserves all caps. ' +
        '${s.toUpperCase()} is very handy!' ==
    'That deserves all caps. ' +
        'STRING INTERPOLATION is very handy!');
```

{{site.alert.note}}
  `==` 运算符判断两个对象的内容是否相等，如果两个字符串包含一样的字符编码序列，则表示相等。
{{site.alert.end}}

可以使用 `+` 运算符将两个字符串连接为一个，也可以将多个字符串挨着放一起变为一个：

<?code-excerpt "misc/test/language_tour/built_in_types_test.dart (adjacent-string-literals)"?>
```dart
var s1 = 'String '
    'concatenation'
    " works even over line breaks.";
assert(s1 ==
    'String concatenation works even over '
        'line breaks.');

var s2 = 'The + operator ' + 'works, as well.';
assert(s2 == 'The + operator works, as well.');
```

可以使用三个单引号或者三个双引号创建多行字符串：

<?code-excerpt "misc/lib/language_tour/built_in_types.dart (triple-quotes)"?>
```dart
var s1 = '''
You can create
multi-line strings like this one.
''';

var s2 = """This is also a
multi-line string.""";
```

在字符串前加上 `r` 作为前缀创建 “raw” 字符串（即不会被做任何处理（比如转义）的字符串）：

<?code-excerpt "misc/lib/language_tour/built_in_types.dart (raw-strings)"?>
```dart
var s = r'In a raw string, not even \n gets special treatment.';
```

查看 [Runes and grapheme clusters](#characters) 可以获取更多有关如何在字符串中表示 Unicode 字符的信息。

字符串字面量是一个编译期常量，
只要是编译期常量都可以作为字符串字面量的插值表达式。

<?code-excerpt "misc/lib/language_tour/built_in_types.dart (string-literals)"?>
```dart
// These work in a const string.
const aConstNum = 0;
const aConstBool = true;
const aConstString = 'a constant string';

// These do NOT work in a const string.
var aNum = 0;
var aBool = true;
var aString = 'a string';
const aConstList = [1, 2, 3];

const validConstString = '$aConstNum $aConstBool $aConstString';
// const invalidConstString = '$aNum $aBool $aString $aConstList';
```

关于使用字符串的更多信息，请查阅
[字符串和正则表达式](/guides/libraries/library-tour#strings-and-regular-expressions)。


### Booleans

Dart 使用 `bool` 关键字表示布尔类型，
布尔类型只有两个对象 `true` 和 `false`，两者都是编译期常量。

Dart 的类型安全性意味着您不可以使用类似
<code>if (<em>nonbooleanValue</em>)</code> 或
<code>assert (<em>nonbooleanValue</em>)</code> 这样的代码检查布尔值。
您应该总是显式地检查布尔值，就像下面的代码：

<?code-excerpt "misc/test/language_tour/built_in_types_test.dart (no-truthy)"?>
```dart
// Check for an empty string.
var fullName = '';
assert(fullName.isEmpty);

// Check for zero.
var hitPoints = 0;
assert(hitPoints <= 0);

// Check for null.
var unicorn;
assert(unicorn == null);

// Check for NaN.
var iMeantToDoThis = 0 / 0;
assert(iMeantToDoThis.isNaN);
```


### Lists

数组 *Array* 是几乎所有编程语言中最常见的集合类型，
在 Dart 中数组由 [List][] 对象表示。通常称之为 *List*。

Dart List 字面量看起来就像是 JavaScript 数组字面量。
下面是一个简单的 Dart List ：

<?code-excerpt "misc/lib/language_tour/built_in_types.dart (list-literal)"?>
```dart
var list = [1, 2, 3];
```

{{site.alert.note}}
  这里 Dart 推断出 `list` 的类型为 `List<int>`。如果您往该 list 中添加一个非int对象，
  则 Dart 分析器或 Dart 运行时将会报错。更多信息，请参考
  [类型推断](/guides/language/sound-dart#type-inference)。
{{site.alert.end}}

List 的索引从 0 开始，0 是第一个元素的索引，
`list.length - 1` 是最后一个元素的索引。
您可以像 JavaScript 中的用法那样获取 Dart 中 List 的长度以及元素：

<?code-excerpt "misc/test/language_tour/built_in_types_test.dart (list-indexing)"?>
```dart
var list = [1, 2, 3];
assert(list.length == 3);
assert(list[1] == 2);

list[1] = 1;
assert(list[1] == 1);
```

如果要创建一个编译期常量的 list，只需要在 list 字面量前加上 `const` 关键字：

<?code-excerpt "misc/lib/language_tour/built_in_types.dart (const-list)"?>
```dart
var constantList = const [1, 2, 3];
// constantList[1] = 1; // Uncommenting this causes an error.
```

<a id="spread-operator"> </a>
Dart 2.3 引入了 **展开操作符** (`...`) 和 the
**null-aware 展开操作符** (`...?`)，
它们提供了一种将多个元素插入集合的简洁方法。

例如，您可以使用 展开操作符 (`...`) 将一个 list 中的元素插入到另一个 list 中：

<?code-excerpt "misc/test/language_tour/built_in_types_test.dart (list-spread)"?>
```dart
var list = [1, 2, 3];
var list2 = [0, ...list];
assert(list2.length == 4);
```

如果展开操作符右边的表达式可能为 null，
您可以使用 null-aware 展开操作符(`...?`) 来避免产生异常：

<?code-excerpt "misc/test/language_tour/built_in_types_test.dart (list-null-spread)"?>
```dart
var list;
var list2 = [0, ...?list];
assert(list2.length == 1);
```

关于使用展开操作符的更新信息和例子，请参考
[spread operator proposal.][spread proposal]

<a id="collection-operators"> </a>
Dart 2.3 还引入了 **collection if** 和 **collection for**，
在构建集合时可以使用条件判断 (`if`) 和循环 (`for`)。

下面是一个使用 **collection if** 来创建 list 的例子，
它可能包含 3 或 4 个元素：

<?code-excerpt "misc/test/language_tour/built_in_types_test.dart (list-if)"?>
```dart
var nav = [
  'Home',
  'Furniture',
  'Plants',
  if (promoActive) 'Outlet'
];
```

下面是一个使用 **collection for**
将一个 list 中的元素修改后添加到另一个 list 中的示例：

<?code-excerpt "misc/test/language_tour/built_in_types_test.dart (list-for)"?>
```dart
var listOfInts = [1, 2, 3];
var listOfStrings = [
  '#0',
  for (var i in listOfInts) '#$i'
];
assert(listOfStrings[1] == '#1');
```

获取更多关于使用 `collection if` 和 `collection for` 的信息和例子，请查看
[集合中使用控制流的建议][collections proposal] 。

[collections proposal]: https://github.com/dart-lang/language/blob/master/accepted/2.3/control-flow-collections/feature-specification.md

[spread proposal]: https://github.com/dart-lang/language/blob/master/accepted/2.3/spread-collections/feature-specification.md

List 类中有许多用于操作 List 的便捷方法，请查阅
[Generics](#generics) 和
[Collections](/guides/libraries/library-tour#collections) 获取更多信息。


### Sets

Dart 中的 Set 是唯一元素（即集合中的元素不可重复）的无序集合。
Dart 支持 set 字面量和 [Set][] 类型。

{{site.alert.version-note}}
  尽管 Set _类型_ 一直是 Dart 中的核心部分，
  但 set _字面量_ 直到 Dart 2.2 开始才被引入。
{{site.alert.end}}

下面是一个使用 set 字面量创建 set 的例子：

<?code-excerpt "misc/lib/language_tour/built_in_types.dart (set-literal)"?>
```dart
var halogens = {'fluorine', 'chlorine', 'bromine', 'iodine', 'astatine'};
```

{{site.alert.note}}
  Dart 推断 `halogens` 变量的类型是 `Set<String>`。
  如果您向该集合中添加一个错误类型的值，Dart 分析器或 Dart 运行时将会报错。
  更多信息，请参考
  [类型推断](/guides/language/sound-dart#type-inference) 。
{{site.alert.end}}

如果想创建一个空 set，请在类型参数之前使用 `{}`，
或将 `{}` 赋值给一个 `Set` 类型的变量：

<?code-excerpt "misc/lib/language_tour/built_in_types.dart (set-vs-map)"?>
```dart
var names = <String>{};
// Set<String> names = {}; // This works, too.
// var names = {}; // Creates a map, not a set. 此处 names 是一个 map，而不是 set
```

{{site.alert.info}}
  **Set 还是 map?** map 字面量的语法和 set 字面量的语法很相似。
  由于 map 字面量先出现，所以 `{}` 默认是 `Map` 类型。
  如果您忘记给 `{}` 指定类型或者将 `{}` 赋值给一个未指定类型的变量上，
  那么 Dart 将会创建一个类型为 `Map<dynamic, dynamic>` 的对象。
{{site.alert.end}}

使用 `add()` 或 `addAll()` 方法可以向已有 set 中添加元素：

<?code-excerpt "misc/lib/language_tour/built_in_types.dart (set-add-items)"?>
```dart
var elements = <String>{};
elements.add('fluorine');
elements.addAll(halogens);
```

使用 `.length` 可以获取 set 中元素的数量：

<?code-excerpt "misc/test/language_tour/built_in_types_test.dart (set-length)"?>
```dart
var elements = <String>{};
elements.add('fluorine');
elements.addAll(halogens);
assert(elements.length == 5);
```

如果想创建一个编译期常量的 set，
可以在 set 字面量前添加 `const` 关键字：

<?code-excerpt "misc/lib/language_tour/built_in_types.dart (const-set)"?>
```dart
final constantSet = const {
  'fluorine',
  'chlorine',
  'bromine',
  'iodine',
  'astatine',
};
// constantSet.add('helium'); // Uncommenting this causes an error.
```

从 Dart 2.3 开始，set 可以像 list 一样支持 展开操作符 (`...` and `...?`)
和 `collection if` & `collection for`。
更多信息，请参考
[list 展开操作符](#spread-operator) 和
[list 集合操作符](#collection-operators) 。

查看
[Generics](#generics) 和
[Sets](/guides/libraries/library-tour#sets) 获取更多关于 set 的信息。

### Maps

通常，map 是一个用来关联 key 和 value 的对象。
key 和 value 可以是任何对象类型。
在一个 map 中，*key* 不允许重复，*value* 可以重复。
Dart 支持 map 字面量和 [Map][] 类型。

下面是两个使用 map 字面量创建 map 的例子：

<?code-excerpt "misc/lib/language_tour/built_in_types.dart (map-literal)"?>
```dart
var gifts = {
  // Key:    Value
  'first': 'partridge',
  'second': 'turtledoves',
  'fifth': 'golden rings'
};

var nobleGases = {
  2: 'helium',
  10: 'neon',
  18: 'argon',
};
```

{{site.alert.note}}
  Dart 推断 `gifts` 变量的类型是 `Map<String, String>`，`nobleGases` 变量的类型是 `Map<int, String>`。
  如果您向这两个 map 中添加一个错误类型的值，Dart 分析器或 Dart 运行时将会报错。
  更多信息，请参考
  [类型推断](/guides/language/sound-dart#type-inference) 。
{{site.alert.end}}

您也可以使用 map 的构造器创建 map 对象：

<?code-excerpt "misc/lib/language_tour/built_in_types.dart (map-constructor)"?>
```dart
var gifts = Map();
gifts['first'] = 'partridge';
gifts['second'] = 'turtledoves';
gifts['fifth'] = 'golden rings';

var nobleGases = Map();
nobleGases[2] = 'helium';
nobleGases[10] = 'neon';
nobleGases[18] = 'argon';
```

{{site.alert.note}}
  这里之所以使用 `Map()` 而不是 `new Map()` 来构造 map 对象，
  是因为从 Dart 2 开始，`new` 关键字是可选的。
  详细信息，请参考 [构造器的使用](#using-constructors) 。
{{site.alert.end}}

向已有的 map 中添加键值对的操作和 JavaScript 的类似：

<?code-excerpt "misc/lib/language_tour/built_in_types.dart (map-add-item)"?>
```dart
var gifts = {'first': 'partridge'};
gifts['fourth'] = 'calling birds'; // Add a key-value pair
```

从一个 map 中获取某值的操作也与 JavaScript 的类似：

<?code-excerpt "misc/test/language_tour/built_in_types_test.dart (map-retrieve-item)"?>
```dart
var gifts = {'first': 'partridge'};
assert(gifts['first'] == 'partridge');
```

如果检索的 key 不存在于 map 中则会返回一个 null：

<?code-excerpt "misc/test/language_tour/built_in_types_test.dart (map-missing-key)"?>
```dart
var gifts = {'first': 'partridge'};
assert(gifts['fifth'] == null);
```

使用 `.length` 可以获取 map 中键值对的数量：

<?code-excerpt "misc/test/language_tour/built_in_types_test.dart (map-length)"?>
```dart
var gifts = {'first': 'partridge'};
gifts['fourth'] = 'calling birds';
assert(gifts.length == 2);
```

如果想创建一个编译期常量的 map，
只需要在 map 字面量前添加 `const` 关键字：

<?code-excerpt "misc/lib/language_tour/built_in_types.dart (const-map)"?>
```dart
final constantMap = const {
  2: 'helium',
  10: 'neon',
  18: 'argon',
};

// constantMap[2] = 'Helium'; // Uncommenting this causes an error.
```

从 Dart 2.3 开始，map 也同 list 一样支持 展开操作符 (`...` and `...?`)、
`collection if` 和 `collection for`。
更多详细信息和示例，请参考
[spread operator proposal][spread proposal] 和
[control flow collections proposal][collections proposal] 。

查阅
[Generics](#generics) 和
[Maps](/guides/libraries/library-tour#maps) 获取有关 map 的更多信息。

<a id="characters"></a>
### Runes 和 grapheme clusters

在 Dart 中，[runes][] 公开了字符串的 Unicode 码位。
从 Dart 2.6 开始，使用 [characters 包][characters package]
来访问或者操作用户感知的字符，
也被称为
[Unicode (extended) grapheme clusters][grapheme clusters]。

Unicode 编码为每一个字母、数字和符号都定义了一个唯一的数值。
因为 Dart 中的字符串是一个 UTF-16 的字符序列，
所以如果想要表示 32 位的 Unicode 数值则需要一种特殊的语法。
通常使用 `\uXXXX` 来表示 Unicode 字符，
XXXX 是一个 4 位的 16 进制数字。
例如，心形字符 (♥) 是 `\u2665`。
对于不是4位数的 16 进制数字，则需要使用大括号将其括起来。
例如，大笑的 emoji (😆) 是 `\u{1f600}`。

如果您需要读写单个 Unicode 字符，
可以使用 characters 包中定义的 `characters` getter。
它返回的 [`Characters`][] 对象是 grapheme clusters 的一系列的字符串。
下面是一个使用 characters API 的例子：

{% comment %}
TODO: add test code
{% endcomment %}

```dart
import 'package:characters/characters.dart';
...
var hi = 'Hi 🇩🇰';
print(hi);
print('The end of the string: ${hi.substring(hi.length - 1)}');
print('The last character: ${hi.characters.last}\n');
```

输出的内容取决于你的环境，看上去会像这样：

```terminal
$ dart bin/main.dart
Hi 🇩🇰
The end of the string: ???
The last character: 🇩🇰
```

有关使用 characters 包操作字符串的详细示例，请参考
[example][characters example] 和 [API reference][characters API]。


### Symbols

[Symbol][] 表示在 Dart 中声明的操作符或标识符。
您可能永远也不会使用到 symbol，
但是如果需要按名称引用它们的 API 时就非常有用，
因为代码压缩后会改变这些标识符名称但不会改变标识符 symbol。

获取一个标识符的 symbol，可以在标识符前面加上一个 `#`：

```nocode
#radix
#bar
```

{% comment %}
The code from the following excerpt isn't actually what is being shown in the page

<?code-excerpt "misc/lib/language_tour/built_in_types.dart (symbols)"?>
```dart
// MOVE TO library tour?

void main() {
  print(Function.apply(int.parse, ['11']));
  print(Function.apply(int.parse, ['11'], {#radix: 16}));
  print(Function.apply(int.parse, ['11a'], {#onError: handleError}));
  print(Function.apply(
      int.parse, ['11a'], {#radix: 16, #onError: handleError}));
}

int handleError(String source) {
  return 0;
}
```
{% endcomment %}

symbol 字面量是编译期常量。


## 函数

Dart 是真正的面向对象的语言，因此函数也是对象，
并且具有类型 [Function.][Function API reference]
这意味着函数可以赋值给变量，或者作为参数传递给其他函数。
你也可以像调用函数一样调用 Dart 类的实例。
详情请参阅 [可调用的类](#callable-classes)。

下面是一个实现函数的例子：

<?code-excerpt "misc/lib/language_tour/functions.dart (function)"?>
```dart
bool isNoble(int atomicNumber) {
  return _nobleGases[atomicNumber] != null;
}
```

虽然 高效Dart指南 建议
[公开API上标明返回类型](/guides/language/effective-dart/design#prefer-type-annotating-public-fields-and-top-level-variables-if-the-type-isnt-obvious)，
不过即便不写返回类型，该函数依然可以工作：

<?code-excerpt "misc/lib/language_tour/functions.dart (function-omitting-types)"?>
```dart
isNoble(atomicNumber) {
  return _nobleGases[atomicNumber] != null;
}
```

如果函数体只包含一个表达式，您可以使用一个简写的语法：

<?code-excerpt "misc/lib/language_tour/functions.dart (function-shorthand)"?>
```dart
bool isNoble(int atomicNumber) => _nobleGases[atomicNumber] != null;
```

<code>=> <em>表达式</em></code> 语法是
<code>{ return <em>表达式</em>; }</code> 的简写。
`=>` 语法有时也被称为 _箭头_ 语法。

{{site.alert.note}}
  箭头 (=\>) 和分号 (;) 之间只能出现一个 *表达式*，而不是一条 *语句*。
  例如，您不能在其中放置 [if 语句](#if-and-else)，
  但是可以使用 [条件表达式](#conditional-expressions)。
{{site.alert.end}}

函数可以有两种类型的参数： _必要参数_ and _可选参数_。
必要参数定义在参数列表前面，可选参数则定义在必要参数后面。
可选参数可以是 _命名参数_ 或 _位置参数_。

{{site.alert.note}}
  一些API（尤其是 [Flutter][] widget 构造函数）仅使用命名参数，
  即使对于强制性参数也是如此。有关详细信息，请参见下一部分。
{{site.alert.end}}

### 可选参数

可选参数分为命名参数和位置参数，可在参数列表中任选其一使用，但两者不能同时出现在参数列表中。

#### 命名参数

当您调用函数时，您可以通过
<code><em>参数名</em>: <em>参数值</em></code> 的形式指定命名参数。例如：

<?code-excerpt "misc/lib/language_tour/functions.dart (use-named-parameters)"?>
```dart
enableFlags(bold: true, hidden: false);
```

定义函数时。可以使用
<code>{<em>参数1</em>, <em>参数2</em>, …}</code>
的形式指定命名参数：

<?code-excerpt "misc/lib/language_tour/functions.dart (specify-named-parameters)"?>
```dart
/// Sets the [bold] and [hidden] flags ...
void enableFlags({bool bold, bool hidden}) {...}
```

虽然命名参数是可选参数的一种，
但是您可以使用 [@required][] 注解来标注一个参数是必须的，
调用者必须为该参数提供一个值。例如：

<?code-excerpt "misc/lib/language_tour/functions.dart (required-named-parameters)" replace="/@required/[!$&!]/g"?>
{% prettify dart tag=pre+code %}
const Scrollbar({Key key, [!@required!] Widget child})
{% endprettify %}

如果调用者想创建一个 `Scrollbar` 对象而不提供 `child` 参数，
Dart 分析器将会报告一个问题。

[@required][] 注解依赖 [meta][] 包，
要使用的话，需要导入 `package:meta/meta.dart`。

#### 位置参数

使用 `[]` 将一系列函数参数包裹起来作为位置参数：

<?code-excerpt "misc/test/language_tour/functions_test.dart (optional-positional-parameters)"?>
```dart
String say(String from, String msg, [String device]) {
  var result = '$from says $msg';
  if (device != null) {
    result = '$result with a $device';
  }
  return result;
}
```

下面是一个不传可选参数调用上述函数的示例：

<?code-excerpt "misc/test/language_tour/functions_test.dart (call-without-optional-param)"?>
```dart
assert(say('Bob', 'Howdy') == 'Bob says Howdy');
```

下面是传入可选参数（第三个参数）调用上述函数的示例：

<?code-excerpt "misc/test/language_tour/functions_test.dart (call-with-optional-param)"?>
```dart
assert(say('Bob', 'Howdy', 'smoke signal') ==
    'Bob says Howdy with a smoke signal');
```

<a id="default-parameters"></a>
#### 默认参数值

可以使用 `=` 为函数的可选参数（命名参数、位置参数）设置默认值。
默认值必须是编译期常量。
如果不设置默认值，那么默认值就是 `null` 。

下面是一个为命名参数设置默认值的例子：

<?code-excerpt "misc/lib/language_tour/functions.dart (named-parameter-default-values)"?>
```dart
/// Sets the [bold] and [hidden] flags ...
void enableFlags({bool bold = false, bool hidden = false}) {...}

// bold will be true; hidden will be false.
enableFlags(bold: true);
```

{{site.alert.info}}
  **弃用提醒：** 一些老的代码里可能会使用冒号 (`:`) 而不是 `=` 设置命名参数的默认值。
  原因是，命名参数最初只支持 `:`。
  但该支持可能会被弃用，因此我们建议您
  **[使用 `=` 设置默认值][use =]** 。

  [use =]: /guides/language/effective-dart/usage#do-use--to-separate-a-named-parameter-from-its-default-value
{{site.alert.end}}

{% comment %}
PENDING: I don't see evidence that we've dropped support for `:`.
Update if/when we do. Issue #?
See `defaultNamedParameter` in the language spec.
{% endcomment %}

下面的示例展示了如何设置位置参数的默认值：

<?code-excerpt "misc/test/language_tour/functions_test.dart (optional-positional-param-default)"?>
```dart
String say(String from, String msg,
    [String device = 'carrier pigeon', String mood]) {
  var result = '$from says $msg';
  if (device != null) {
    result = '$result with a $device';
  }
  if (mood != null) {
    result = '$result (in a $mood mood)';
  }
  return result;
}

assert(say('Bob', 'Howdy') ==
    'Bob says Howdy with a carrier pigeon');
```

您也可以传入 list 或 map 作为默认值。
下面的示例定义了一个 `doStuff()` 函数，
然后给 `list` 参数指定了一个 list 默认值，
给 `gifts` 参数指定了一个 map 默认值。
{% comment %}
The function is called three times with different values. Click **Run** to see
list and map default values in action.
{% endcomment %}

<?code-excerpt "misc/lib/language_tour/functions.dart (list-map-default-function-param)"?>
```dart
void doStuff(
    {List<int> list = const [1, 2, 3],
    Map<String, String> gifts = const {
      'first': 'paper',
      'second': 'cotton',
      'third': 'leather'
    }}) {
  print('list:  $list');
  print('gifts: $gifts');
}
```

{% comment %}
https://gist.github.com/d988cfce0a54c6853799
{{site.dartpad}}/d988cfce0a54c6853799
(The gist needs updating: see https://github.com/dart-lang/site-www/issues/189)
<iframe
src="{{site.dartpad-embed-inline}}?id=d988cfce0a54c6853799"
    width="100%"
    height="450px"
    style="border: 1px solid #ccc;">
</iframe>
{% endcomment %}


### main() 函数

每个 Dart 应用程序都必须有一个顶层的 `main()` 函数，它是程序的入口。
`main()` 函数的返回值为 `void` 并且有一个类型为 `List<String>` 的可选参数。

下面是一个 web 应用的 `main()` 函数的示例：

<?code-excerpt "misc/test/language_tour/browser_test.dart (simple-web-main-function)"?>
```dart
void main() {
  querySelector('#sample_text_id')
    ..text = 'Click me!'
    ..onClick.listen(reverseText);
}
```

{{site.alert.note}}
  上面代码中的 `..` 语法称为 [级联调用](#cascade-notation-) 。
  使用级联访问可以在一个对象上执行多个操作。
{{site.alert.end}}

下面是一个命令行程序，具有带参数的 `main()` 函数：

<?code-excerpt "misc/test/language_tour/functions_test.dart (main-args)"?>
```dart
// Run the app like this: dart args.dart 1 test
void main(List<String> arguments) {
  print(arguments);

  assert(arguments.length == 2);
  assert(int.parse(arguments[0]) == 1);
  assert(arguments[1] == 'test');
}
```

您可以使用 [args 库]({{site.pub}}/packages/args)
去定义或解析命令行参数。

### Functions as first-class objects

You can pass a function as a parameter to another function. For example:

<?code-excerpt "misc/lib/language_tour/functions.dart (function-as-param)"?>
```dart
void printElement(int element) {
  print(element);
}

var list = [1, 2, 3];

// Pass printElement as a parameter.
list.forEach(printElement);
```

You can also assign a function to a variable, such as:

<?code-excerpt "misc/test/language_tour/functions_test.dart (function-as-var)"?>
```dart
var loudify = (msg) => '!!! ${msg.toUpperCase()} !!!';
assert(loudify('hello') == '!!! HELLO !!!');
```

This example uses an anonymous function.
More about those in the next section.

### Anonymous functions

Most functions are named, such as `main()` or `printElement()`.
You can also create a nameless function
called an _anonymous function_, or sometimes a _lambda_ or _closure_.
You might assign an anonymous function to a variable so that,
for example, you can add or remove it from a collection.

An anonymous function looks similar to a named function&mdash;
zero or more parameters, separated by commas
and optional type annotations, between parentheses.

The code block that follows contains the function's body:

<code>
([[<em>Type</em>] <em>param1</em>[, …]]) { <br>
&nbsp;&nbsp;<em>codeBlock</em>; <br>
}; <br>
</code>

The following example defines an anonymous function with an untyped parameter, `item`.
The function, invoked for each item in the list,
prints a string that includes the value at the specified index.

<?code-excerpt "misc/test/language_tour/functions_test.dart (anonymous-function)"?>
```dart
var list = ['apples', 'bananas', 'oranges'];
list.forEach((item) {
  print('${list.indexOf(item)}: $item');
});
```

Click **Run** to execute the code.

{% comment %}
https://gist.github.com/chalin/5d70bc1889d055c7a18d35d77874af88
{{site.dartpad}}/5d70bc1889d055c7a18d35d77874af88
{% endcomment %}

<iframe
src="{{site.dartpad-embed-inline}}?id=5d70bc1889d055c7a18d35d77874af88&split=60"
    width="100%"
    height="400px"
    style="border: 1px solid #ccc;">
</iframe>

If the function contains only one statement, you can shorten it using arrow
notation. Paste the following line into DartPad and click **Run** to verify that
it is functionally equivalent.

<?code-excerpt "misc/test/language_tour/functions_test.dart (anon-func)"?>
```dart
list.forEach(
    (item) => print('${list.indexOf(item)}: $item'));
```


### Lexical scope

Dart is a lexically scoped language, which means that the scope of
variables is determined statically, simply by the layout of the code.
You can “follow the curly braces outwards” to see if a variable is in
scope.

Here is an example of nested functions with variables at each scope
level:

<?code-excerpt "misc/test/language_tour/functions_test.dart (nested-functions)"?>
```dart
bool topLevel = true;

void main() {
  var insideMain = true;

  void myFunction() {
    var insideFunction = true;

    void nestedFunction() {
      var insideNestedFunction = true;

      assert(topLevel);
      assert(insideMain);
      assert(insideFunction);
      assert(insideNestedFunction);
    }
  }
}
```

Notice how `nestedFunction()` can use variables from every level, all
the way up to the top level.


### Lexical closures

A *closure* is a function object that has access to variables in its
lexical scope, even when the function is used outside of its original
scope.

Functions can close over variables defined in surrounding scopes. In the
following example, `makeAdder()` captures the variable `addBy`. Wherever the
returned function goes, it remembers `addBy`.

<?code-excerpt "misc/test/language_tour/functions_test.dart (function-closure)"?>
```dart
/// Returns a function that adds [addBy] to the
/// function's argument.
Function makeAdder(num addBy) {
  return (num i) => addBy + i;
}

void main() {
  // Create a function that adds 2.
  var add2 = makeAdder(2);

  // Create a function that adds 4.
  var add4 = makeAdder(4);

  assert(add2(3) == 5);
  assert(add4(3) == 7);
}
```


### Testing functions for equality

Here's an example of testing top-level functions, static methods, and
instance methods for equality:

<?code-excerpt "misc/lib/language_tour/function_equality.dart"?>
```dart
void foo() {} // A top-level function

class A {
  static void bar() {} // A static method
  void baz() {} // An instance method
}

void main() {
  var x;

  // Comparing top-level functions.
  x = foo;
  assert(foo == x);

  // Comparing static methods.
  x = A.bar;
  assert(A.bar == x);

  // Comparing instance methods.
  var v = A(); // Instance #1 of A
  var w = A(); // Instance #2 of A
  var y = w;
  x = w.baz;

  // These closures refer to the same instance (#2),
  // so they're equal.
  assert(y.baz == x);

  // These closures refer to different instances,
  // so they're unequal.
  assert(v.baz != w.baz);
}
```


### Return values

All functions return a value. If no return value is specified, the
statement `return null;` is implicitly appended to the function body.

<?code-excerpt "misc/test/language_tour/functions_test.dart (implicit-return-null)"?>
```dart
foo() {}

assert(foo() == null);
```


## Operators

Dart defines the operators shown in the following table.
You can override many of these operators, as described in
[Overridable operators](#overridable-operators).

|--------------------------+------------------------------------------------|
|Description               | Operator                                       |
|--------------------------|------------------------------------------------|
| unary postfix            | <code><em>expr</em>++</code>    <code><em>expr</em>--</code>    `()`    `[]`    `.`    `?.` |
| unary prefix             | <code>-<em>expr</em></code>    <code>!<em>expr</em></code>    <code>~<em>expr</em></code>    <code>++<em>expr</em></code>    <code>--<em>expr</em></code>      <code>await <em>expr</em></code>    |
| multiplicative           | `*`    `/`    `%`    `~/`                      |
| additive                 | `+`    `-`                                     |
| shift                    | `<<`    `>>`    `>>>`                          |
| bitwise AND              | `&`                                            |
| bitwise XOR              | `^`                                            |
| bitwise OR               | `|`                                            |
| relational&nbsp;and&nbsp;type&nbsp;test | `>=`    `>`    `<=`    `<`    `as`    `is`    `is!` |
| equality                 | `==`    `!=`                                   |
| logical AND              | `&&`                                           |
| logical OR               | `||`                                           |
| if null                  | `??`                                           |
| conditional              | <code><em>expr1</em> ? <em>expr2</em> : <em>expr3</em></code> |
| cascade                  | `..`                                           |
| assignment               | `=`    `*=`    `/=`    `+=`    `-=`    `&=`    `^=`    <em>etc.</em> |
{:.table .table-striped}

{{site.alert.warning}}
  Operator precedence is an approximation of the behavior of a Dart parser.
  For definitive answers, consult the grammar in the
  [Dart language specification][].
{{site.alert.end}}

When you use operators, you create expressions. Here are some examples
of operator expressions:

<?code-excerpt "misc/test/language_tour/operators_test.dart (expressions)" replace="/,//g"?>
```dart
a++
a + b
a = b
a == b
c ? a : b
a is T
```

In the [operator table](#operators),
each operator has higher precedence than the operators in the rows
that follow it. For example, the multiplicative operator `%` has higher
precedence than (and thus executes before) the equality operator `==`,
which has higher precedence than the logical AND operator `&&`. That
precedence means that the following two lines of code execute the same
way:

<?code-excerpt "misc/test/language_tour/operators_test.dart (precedence)"?>
```dart
// Parentheses improve readability.
if ((n % i == 0) && (d % i == 0)) ...

// Harder to read, but equivalent.
if (n % i == 0 && d % i == 0) ...
```

{{site.alert.warning}}
  For operators that work on two operands, the leftmost operand determines which
  version of the operator is used. For example, if you have a Vector object and
  a Point object, `aVector + aPoint` uses the Vector version of +.
{{site.alert.end}}


### Arithmetic operators

Dart supports the usual arithmetic operators, as shown in the following table.

|-----------------------------+-------------------------------------------|
| Operator                    | Meaning                                   |
|-----------------------------+-------------------------------------------|
| `+`                         | Add
| `–`                         | Subtract
| <code>-<em>expr</em></code> | Unary minus, also known as negation (reverse the sign of the expression)
| `*`                         | Multiply
| `/`                         | Divide
| `~/`                        | Divide, returning an integer result
| `%`                         | Get the remainder of an integer division (modulo)
{:.table .table-striped}

Example:

<?code-excerpt "misc/test/language_tour/operators_test.dart (arithmetic)"?>
```dart
assert(2 + 3 == 5);
assert(2 - 3 == -1);
assert(2 * 3 == 6);
assert(5 / 2 == 2.5); // Result is a double
assert(5 ~/ 2 == 2); // Result is an int
assert(5 % 2 == 1); // Remainder

assert('5/2 = ${5 ~/ 2} r ${5 % 2}' == '5/2 = 2 r 1');
```

Dart also supports both prefix and postfix increment and decrement
operators.

|-----------------------------+-------------------------------------------|
| Operator                    | Meaning                                   |
|-----------------------------+-------------------------------------------|
| <code>++<em>var</em></code> | <code><em>var</em> = <em>var</em> + 1</code> (expression value is <code><em>var</em> + 1</code>)
| <code><em>var</em>++</code> | <code><em>var</em> = <em>var</em> + 1</code> (expression value is <code><em>var</em></code>)
| <code>--<em>var</em></code> | <code><em>var</em> = <em>var</em> – 1</code> (expression value is <code><em>var</em> – 1</code>)
| <code><em>var</em>--</code> | <code><em>var</em> = <em>var</em> – 1</code> (expression value is <code><em>var</em></code>)
{:.table .table-striped}

Example:

<?code-excerpt "misc/test/language_tour/operators_test.dart (increment-decrement)"?>
```dart
var a, b;

a = 0;
b = ++a; // Increment a before b gets its value.
assert(a == b); // 1 == 1

a = 0;
b = a++; // Increment a AFTER b gets its value.
assert(a != b); // 1 != 0

a = 0;
b = --a; // Decrement a before b gets its value.
assert(a == b); // -1 == -1

a = 0;
b = a--; // Decrement a AFTER b gets its value.
assert(a != b); // -1 != 0
```


### Equality and relational operators

The following table lists the meanings of equality and relational operators.

|-----------+-------------------------------------------|
| Operator  | Meaning                                   |
|-----------+-------------------------------------------|
| `==`      |       Equal; see discussion below
| `!=`      |       Not equal
| `>`       |       Greater than
| `<`       |       Less than
| `>=`      |       Greater than or equal to
| `<=`      |       Less than or equal to
{:.table .table-striped}

To test whether two objects x and y represent the same thing, use the
`==` operator. (In the rare case where you need to know whether two
objects are the exact same object, use the [identical()][]
function instead.) Here’s how the `==` operator works:

1.  If *x* or *y* is null, return true if both are null, and false if only
    one is null.

2.  Return the result of the method invocation
    <code><em>x</em>.==(<em>y</em>)</code>. (That’s right,
    operators such as `==` are methods that are invoked on their first
    operand. You can even override many operators, including `==`, as
    you’ll see in
    [Overridable operators](#overridable-operators).)

Here’s an example of using each of the equality and relational
operators:

<?code-excerpt "misc/test/language_tour/operators_test.dart (relational)"?>
```dart
assert(2 == 2);
assert(2 != 3);
assert(3 > 2);
assert(2 < 3);
assert(3 >= 3);
assert(2 <= 3);
```


### Type test operators

The `as`, `is`, and `is!` operators are handy for checking types at
runtime.

|-----------+-------------------------------------------|
| Operator  | Meaning                                   |
|-----------+-------------------------------------------|
| `as`      | Typecast (also used to specify [library prefixes](#specifying-a-library-prefix))
| `is`      | True if the object has the specified type
| `is!`     | False if the object has the specified type
{:.table .table-striped}

The result of `obj is T` is true if `obj` implements the interface
specified by `T`. For example, `obj is Object` is always true.

Use the `as` operator to cast an object to a particular type if and only if
you are sure that the object is of that type. Example:

<?code-excerpt "misc/lib/language_tour/classes/employee.dart (emp as Person)"?>
```dart
(emp as Person).firstName = 'Bob';
```

If you aren't sure that the object is of type `T`, then use `is T` to check the 
type before using the object.
<?code-excerpt "misc/lib/language_tour/classes/employee.dart (emp is Person)"?>
```dart
if (emp is Person) {
  // Type check
  emp.firstName = 'Bob';
}
```

{{site.alert.note}}
  The code isn’t equivalent. If `emp` is null or not a `Person`, the
  first example throws an exception; the second does nothing.
{{site.alert.end}}

### Assignment operators

As you’ve already seen, you can assign values using the `=` operator.
To assign only if the assigned-to variable is null,
use the `??=` operator.

<?code-excerpt "misc/test/language_tour/operators_test.dart (assignment)"?>
```dart
// Assign value to a
a = value;
// Assign value to b if b is null; otherwise, b stays the same
b ??= value;
```

{% comment %}
<!-- embed a dartpad when we can hide code -->
https://gist.github.com/9de887c4daf76d39e524
{{site.dartpad}}/9de887c4daf76d39e524

<?code-excerpt "misc/test/language_tour/operators_test.dart (assignment-gist-main-body)" plaster="none"?>
```dart
void assignValues(int a, int b, int value) {
  print('Initially: a == $a, b == $b');
  // Assign value to a
  a = value;
  // Assign value to b if b is null; otherwise, b stays the same
  b ??= value;
  print('After: a == $a, b == $b');
}

main() {
  assignValues(0, 0, 1);
  assignValues(null, null, 1);
}
```
{% endcomment %}

Compound assignment operators such as `+=` combine
an operation with an assignment.

| `=`  | `–=` | `/=`  | `%=`  | `>>=` | `^=`
| `+=` | `*=` | `~/=` | `<<=` | `&=`  | `|=`
{:.table}

Here’s how compound assignment operators work:

|-----------+----------------------+-----------------------|
|           | Compound assignment  | Equivalent expression |
|-----------+----------------------+-----------------------|
|**For an operator <em>op</em>:** | <code>a <em>op</em>= b</code> | <code>a = a <em>op</em> b</code>
|**Example:**                     |`a += b`                       | `a = a + b`
{:.table}

The following example uses assignment and compound assignment
operators:

<?code-excerpt "misc/test/language_tour/operators_test.dart (op-assign)"?>
```dart
var a = 2; // Assign using =
a *= 3; // Assign and multiply: a = a * 3
assert(a == 6);
```


### Logical operators

You can invert or combine boolean expressions using the logical
operators.

|-----------------------------+-------------------------------------------|
| Operator                    | Meaning                                   |
|-----------------------------+-------------------------------------------|
| <code>!<em>expr</em></code> | inverts the following expression (changes false to true, and vice versa)
| `||`                        | logical OR
| `&&`                        | logical AND
{:.table .table-striped}

Here’s an example of using the logical operators:

<?code-excerpt "misc/lib/language_tour/operators.dart (op-logical)"?>
```dart
if (!done && (col == 0 || col == 3)) {
  // ...Do something...
}
```


### Bitwise and shift operators

You can manipulate the individual bits of numbers in Dart. Usually,
you’d use these bitwise and shift operators with integers.

|-----------------------------+-------------------------------------------|
| Operator                    | Meaning                                   |
|-----------------------------+-------------------------------------------|
| `&`                         | AND
| `|`                         | OR
| `^`                         | XOR
| <code>~<em>expr</em></code> | Unary bitwise complement (0s become 1s; 1s become 0s)
| `<<`                        | Shift left
| `>>`                        | Shift right
{:.table .table-striped}

Here’s an example of using bitwise and shift operators:

<?code-excerpt "misc/test/language_tour/operators_test.dart (op-bitwise)"?>
```dart
final value = 0x22;
final bitmask = 0x0f;

assert((value & bitmask) == 0x02); // AND
assert((value & ~bitmask) == 0x20); // AND NOT
assert((value | bitmask) == 0x2f); // OR
assert((value ^ bitmask) == 0x2d); // XOR
assert((value << 4) == 0x220); // Shift left
assert((value >> 4) == 0x02); // Shift right
```


### Conditional expressions

Dart has two operators that let you concisely evaluate expressions
that might otherwise require [if-else](#if-and-else) statements:

<code><em>condition</em> ? <em>expr1</em> : <em>expr2</em></code>
: If _condition_ is true, evaluates _expr1_ (and returns its value);
  otherwise, evaluates and returns the value of _expr2_.

<code><em>expr1</em> ?? <em>expr2</em></code>
: If _expr1_ is non-null, returns its value;
  otherwise, evaluates and returns the value of _expr2_.

When you need to assign a value
based on a boolean expression,
consider using `?:`.

<?code-excerpt "misc/lib/language_tour/operators.dart (if-then-else-operator)"?>
```dart
var visibility = isPublic ? 'public' : 'private';
```

If the boolean expression tests for null,
consider using `??`.

<?code-excerpt "misc/test/language_tour/operators_test.dart (if-null)"?>
```dart
String playerName(String name) => name ?? 'Guest';
```

The previous example could have been written at least two other ways,
but not as succinctly:

<?code-excerpt "misc/test/language_tour/operators_test.dart (if-null-alt)"?>
```dart
// Slightly longer version uses ?: operator.
String playerName(String name) => name != null ? name : 'Guest';

// Very long version uses if-else statement.
String playerName(String name) {
  if (name != null) {
    return name;
  } else {
    return 'Guest';
  }
}
```

<a id="cascade"></a>
### Cascade notation (..)

Cascades (`..`) allow you to make a sequence of operations
on the same object. In addition to function calls,
you can also access fields on that same object.
This often saves you the step of creating a temporary variable and
allows you to write more fluid code.

Consider the following code:

<?code-excerpt "misc/test/language_tour/browser_test.dart (cascade-operator)"?>
```dart
querySelector('#confirm') // Get an object.
  ..text = 'Confirm' // Use its members.
  ..classes.add('important')
  ..onClick.listen((e) => window.alert('Confirmed!'));
```

The first method call, `querySelector()`, returns a selector object.
The code that follows the cascade notation operates
on this selector object, ignoring any subsequent values that
might be returned.

The previous example is equivalent to:

<?code-excerpt "misc/test/language_tour/browser_test.dart (cascade-operator-example-expanded)"?>
```dart
var button = querySelector('#confirm');
button.text = 'Confirm';
button.classes.add('important');
button.onClick.listen((e) => window.alert('Confirmed!'));
```

You can also nest your cascades. For example:

<?code-excerpt "misc/lib/language_tour/operators.dart (nested-cascades)"?>
```dart
final addressBook = (AddressBookBuilder()
      ..name = 'jenny'
      ..email = 'jenny@example.com'
      ..phone = (PhoneNumberBuilder()
            ..number = '415-555-0100'
            ..label = 'home')
          .build())
    .build();
```

Be careful to construct your cascade on a function that returns
an actual object. For example, the following code fails:

<?code-excerpt "misc/lib/language_tour/operators.dart (cannot-cascade-on-void)" plaster="none"?>
```dart
var sb = StringBuffer();
sb.write('foo')
  ..write('bar'); // Error: method 'write' isn't defined for 'void'.
```

The `sb.write()` call returns void,
and you can't construct a cascade on `void`.

{{site.alert.note}}
  Strictly speaking, the "double dot" notation for cascades is not an operator.
  It's just part of the Dart syntax.
{{site.alert.end}}

### Other operators

You've seen most of the remaining operators in other examples:

|----------+-------------------------------------------|
| Operator | Name                 |          Meaning   |
|-----------+------------------------------------------|
| `()`     | Function application | Represents a function call
| `[]`     | List access          | Refers to the value at the specified index in the list
| `.`      | Member access        | Refers to a property of an expression; example: `foo.bar` selects property `bar` from expression `foo`
| `?.`     | Conditional member access | Like `.`, but the leftmost operand can be null; example: `foo?.bar` selects property `bar` from expression `foo` unless `foo` is null (in which case the value of `foo?.bar` is null)
{:.table .table-striped}

For more information about the `.`, `?.`, and `..` operators, see
[Classes](#classes).


## Control flow statements

You can control the flow of your Dart code using any of the following:

-   `if` and `else`
-   `for` loops
-   `while` and `do`-`while` loops
-   `break` and `continue`
-   `switch` and `case`
-   `assert`

You can also affect the control flow using `try-catch` and `throw`, as
explained in [Exceptions](#exceptions).


### If and else

Dart supports `if` statements with optional `else` statements, as the
next sample shows. Also see [conditional expressions](#conditional-expressions).

<?code-excerpt "misc/lib/language_tour/control_flow.dart (if-else)"?>
```dart
if (isRaining()) {
  you.bringRainCoat();
} else if (isSnowing()) {
  you.wearJacket();
} else {
  car.putTopDown();
}
```

Unlike JavaScript, conditions must use boolean values, nothing else. See
[Booleans](#booleans) for more information.


### For loops

You can iterate with the standard `for` loop. For example:

<?code-excerpt "misc/test/language_tour/control_flow_test.dart (for)"?>
```dart
var message = StringBuffer('Dart is fun');
for (var i = 0; i < 5; i++) {
  message.write('!');
}
```

Closures inside of Dart’s `for` loops capture the _value_ of the index,
avoiding a common pitfall found in JavaScript. For example, consider:

<?code-excerpt "misc/test/language_tour/control_flow_test.dart (for-and-closures)"?>
```dart
var callbacks = [];
for (var i = 0; i < 2; i++) {
  callbacks.add(() => print(i));
}
callbacks.forEach((c) => c());
```

The output is `0` and then `1`, as expected. In contrast, the example
would print `2` and then `2` in JavaScript.

If the object that you are iterating over is an Iterable, you can use the
[forEach()][] method. Using `forEach()` is a good option if you don’t need to
know the current iteration counter:

<?code-excerpt "misc/lib/language_tour/control_flow.dart (forEach)"?>
```dart
candidates.forEach((candidate) => candidate.interview());
```

Iterable classes such as List and Set also support the `for-in` form of
[iteration](/guides/libraries/library-tour#iteration):

<?code-excerpt "misc/test/language_tour/control_flow_test.dart (collection)"?>
```dart
var collection = [0, 1, 2];
for (var x in collection) {
  print(x); // 0 1 2
}
```


### While and do-while

A `while` loop evaluates the condition before the loop:

<?code-excerpt "misc/lib/language_tour/control_flow.dart (while)"?>
```dart
while (!isDone()) {
  doSomething();
}
```

A `do`-`while` loop evaluates the condition *after* the loop:

<?code-excerpt "misc/lib/language_tour/control_flow.dart (do-while)"?>
```dart
do {
  printLine();
} while (!atEndOfPage());
```


### Break and continue

Use `break` to stop looping:

<?code-excerpt "misc/lib/language_tour/control_flow.dart (while-break)"?>
```dart
while (true) {
  if (shutDownRequested()) break;
  processIncomingRequests();
}
```

Use `continue` to skip to the next loop iteration:

<?code-excerpt "misc/lib/language_tour/control_flow.dart (for-continue)"?>
```dart
for (int i = 0; i < candidates.length; i++) {
  var candidate = candidates[i];
  if (candidate.yearsExperience < 5) {
    continue;
  }
  candidate.interview();
}
```

You might write that example differently if you’re using an
[Iterable][] such as a list or set:

<?code-excerpt "misc/lib/language_tour/control_flow.dart (where)"?>
```dart
candidates
    .where((c) => c.yearsExperience >= 5)
    .forEach((c) => c.interview());
```


### Switch and case

Switch statements in Dart compare integer, string, or compile-time
constants using `==`. The compared objects must all be instances of the
same class (and not of any of its subtypes), and the class must not
override `==`.
[Enumerated types](#enumerated-types) work well in `switch` statements.

{{site.alert.note}}
  Switch statements in Dart are intended for limited circumstances,
  such as in interpreters or scanners.
{{site.alert.end}}

Each non-empty `case` clause ends with a `break` statement, as a rule.
Other valid ways to end a non-empty `case` clause are a `continue`,
`throw`, or `return` statement.

Use a `default` clause to execute code when no `case` clause matches:

<?code-excerpt "misc/lib/language_tour/control_flow.dart (switch)"?>
```dart
var command = 'OPEN';
switch (command) {
  case 'CLOSED':
    executeClosed();
    break;
  case 'PENDING':
    executePending();
    break;
  case 'APPROVED':
    executeApproved();
    break;
  case 'DENIED':
    executeDenied();
    break;
  case 'OPEN':
    executeOpen();
    break;
  default:
    executeUnknown();
}
```

The following example omits the `break` statement in a `case` clause,
thus generating an error:

<?code-excerpt "misc/lib/language_tour/control_flow.dart (switch-break-omitted)" plaster="none"?>
```dart
var command = 'OPEN';
switch (command) {
  case 'OPEN':
    executeOpen();
    // ERROR: Missing break

  case 'CLOSED':
    executeClosed();
    break;
}
```

However, Dart does support empty `case` clauses, allowing a form of
fall-through:

<?code-excerpt "misc/lib/language_tour/control_flow.dart (switch-empty-case)"?>
```dart
var command = 'CLOSED';
switch (command) {
  case 'CLOSED': // Empty case falls through.
  case 'NOW_CLOSED':
    // Runs for both CLOSED and NOW_CLOSED.
    executeNowClosed();
    break;
}
```

If you really want fall-through, you can use a `continue` statement and
a label:

<?code-excerpt "misc/lib/language_tour/control_flow.dart (switch-continue)"?>
```dart
var command = 'CLOSED';
switch (command) {
  case 'CLOSED':
    executeClosed();
    continue nowClosed;
  // Continues executing at the nowClosed label.

  nowClosed:
  case 'NOW_CLOSED':
    // Runs for both CLOSED and NOW_CLOSED.
    executeNowClosed();
    break;
}
```

A `case` clause can have local variables, which are visible only inside
the scope of that clause.


### Assert

During development, use an assert statement
— <code>assert(<em>condition</em>, <em>optionalMessage</em>)</code>; —
to disrupt normal execution if a boolean
condition is false. You can find examples of assert statements
throughout this tour. Here are some more:

<?code-excerpt "misc/test/language_tour/control_flow_test.dart (assert)"?>
```dart
// Make sure the variable has a non-null value.
assert(text != null);

// Make sure the value is less than 100.
assert(number < 100);

// Make sure this is an https URL.
assert(urlString.startsWith('https'));
```

To attach a message to an assertion,
add a string as the second argument to `assert`.

<?code-excerpt "misc/test/language_tour/control_flow_test.dart (assert-with-message)"?>
```dart
assert(urlString.startsWith('https'),
    'URL ($urlString) should start with "https".');
```

The first argument to `assert` can be any expression that
resolves to a boolean value. If the expression’s value
is true, the assertion succeeds and execution
continues. If it's false, the assertion fails and an exception (an
[AssertionError][]) is thrown.

When exactly do assertions work?
That depends on the tools and framework you're using:

* Flutter enables assertions in [debug mode.][Flutter debug mode]
* Development-only tools such as [dartdevc][]
  typically enable assertions by default.
* Some tools, such as [dart][] and [dart2js,][dart2js]
  support assertions through a command-line flag: `--enable-asserts`.

In production code, assertions are ignored, and
the arguments to `assert` aren't evaluated.


## Exceptions

Your Dart code can throw and catch exceptions. Exceptions are errors
indicating that something unexpected happened. If the exception isn’t
caught, the [isolate](#isolates) that raised the exception is suspended, and
typically the isolate and its program are terminated.

In contrast to Java, all of Dart’s exceptions are unchecked exceptions.
Methods do not declare which exceptions they might throw, and you are
not required to catch any exceptions.

Dart provides [Exception][] and [Error][]
types, as well as numerous predefined subtypes. You can, of course,
define your own exceptions. However, Dart programs can throw any
non-null object—not just Exception and Error objects—as an exception.

### Throw

Here’s an example of throwing, or *raising*, an exception:

<?code-excerpt "misc/lib/language_tour/exceptions.dart (throw-FormatException)"?>
```dart
throw FormatException('Expected at least 1 section');
```

You can also throw arbitrary objects:

<?code-excerpt "misc/lib/language_tour/exceptions.dart (out-of-llamas)"?>
```dart
throw 'Out of llamas!';
```

{{site.alert.note}}
  Production-quality code usually throws types that implement [Error][] or
  [Exception][].
{{site.alert.end}}

Because throwing an exception is an expression, you can throw exceptions
in =\> statements, as well as anywhere else that allows expressions:

<?code-excerpt "misc/lib/language_tour/exceptions.dart (throw-is-an-expression)"?>
```dart
void distanceTo(Point other) => throw UnimplementedError();
```


### Catch

Catching, or capturing, an exception stops the exception from
propagating (unless you rethrow the exception).
Catching an exception gives you a chance to handle it:

<?code-excerpt "misc/lib/language_tour/exceptions.dart (try)"?>
```dart
try {
  breedMoreLlamas();
} on OutOfLlamasException {
  buyMoreLlamas();
}
```

To handle code that can throw more than one type of exception, you can
specify multiple catch clauses. The first catch clause that matches the
thrown object’s type handles the exception. If the catch clause does not
specify a type, that clause can handle any type of thrown object:

<?code-excerpt "misc/lib/language_tour/exceptions.dart (try-catch)"?>
```dart
try {
  breedMoreLlamas();
} on OutOfLlamasException {
  // A specific exception
  buyMoreLlamas();
} on Exception catch (e) {
  // Anything else that is an exception
  print('Unknown exception: $e');
} catch (e) {
  // No specified type, handles all
  print('Something really unknown: $e');
}
```

As the preceding code shows, you can use either `on` or `catch` or both.
Use `on` when you need to specify the exception type. Use `catch` when
your exception handler needs the exception object.

You can specify one or two parameters to `catch()`.
The first is the exception that was thrown,
and the second is the stack trace (a [StackTrace][] object).

<?code-excerpt "misc/lib/language_tour/exceptions.dart (try-catch-2)" replace="/\(e.*?\)/[!$&!]/g"?>
{% prettify dart tag=pre+code %}
try {
  // ···
} on Exception catch [!(e)!] {
  print('Exception details:\n $e');
} catch [!(e, s)!] {
  print('Exception details:\n $e');
  print('Stack trace:\n $s');
}
{% endprettify %}

To partially handle an exception,
while allowing it to propagate,
use the `rethrow` keyword.

<?code-excerpt "misc/test/language_tour/exceptions_test.dart (rethrow)" replace="/rethrow;/[!$&!]/g"?>
{% prettify dart tag=pre+code %}
void misbehave() {
  try {
    dynamic foo = true;
    print(foo++); // Runtime error
  } catch (e) {
    print('misbehave() partially handled ${e.runtimeType}.');
    [!rethrow;!] // Allow callers to see the exception.
  }
}

void main() {
  try {
    misbehave();
  } catch (e) {
    print('main() finished handling ${e.runtimeType}.');
  }
}
{% endprettify %}


### Finally

To ensure that some code runs whether or not an exception is thrown, use
a `finally` clause. If no `catch` clause matches the exception, the
exception is propagated after the `finally` clause runs:

<?code-excerpt "misc/lib/language_tour/exceptions.dart (finally)"?>
```dart
try {
  breedMoreLlamas();
} finally {
  // Always clean up, even if an exception is thrown.
  cleanLlamaStalls();
}
```

The `finally` clause runs after any matching `catch` clauses:

<?code-excerpt "misc/lib/language_tour/exceptions.dart (try-catch-finally)"?>
```dart
try {
  breedMoreLlamas();
} catch (e) {
  print('Error: $e'); // Handle the exception first.
} finally {
  cleanLlamaStalls(); // Then clean up.
}
```

Learn more by reading the
[Exceptions](/guides/libraries/library-tour#exceptions)
section of the library tour.

## Classes

Dart is an object-oriented language with classes and mixin-based
inheritance. Every object is an instance of a class, and all classes
descend from [Object.][Object]
*Mixin-based inheritance* means that although every class (except for
Object) has exactly one superclass, a class body can be reused in
multiple class hierarchies.
[Extension methods](#extension-methods) are a way to
add functionality to a class without changing the class or creating a subclass.


### Using class members

Objects have *members* consisting of functions and data (*methods* and
*instance variables*, respectively). When you call a method, you *invoke*
it on an object: the method has access to that object’s functions and
data.

Use a dot (`.`) to refer to an instance variable or method:

<?code-excerpt "misc/test/language_tour/classes_test.dart (object-members)"?>
```dart
var p = Point(2, 2);

// Set the value of the instance variable y.
p.y = 3;

// Get the value of y.
assert(p.y == 3);

// Invoke distanceTo() on p.
num distance = p.distanceTo(Point(4, 4));
```

Use `?.` instead of `.` to avoid an exception
when the leftmost operand is null:

{% comment %}
{{site.dartpad}}/0cb25997742ed5382e4a
https://gist.github.com/0cb25997742ed5382e4a
{% endcomment %}

<?code-excerpt "misc/test/language_tour/classes_test.dart (safe-member-access)"?>
```dart
// If p is non-null, set its y value to 4.
p?.y = 4;
```


### Using constructors

You can create an object using a *constructor*.
Constructor names can be either <code><em>ClassName</em></code> or
<code><em>ClassName</em>.<em>identifier</em></code>. For example,
the following code creates `Point` objects using the
`Point()` and `Point.fromJson()` constructors:

<?code-excerpt "misc/test/language_tour/classes_test.dart (object-creation)" replace="/ as .*?;/;/g"?>
```dart
var p1 = Point(2, 2);
var p2 = Point.fromJson({'x': 1, 'y': 2});
```

The following code has the same effect, but
uses the optional `new` keyword before the constructor name:

<?code-excerpt "misc/test/language_tour/classes_test.dart (object-creation-new)" replace="/ as .*?;/;/g"?>
```dart
var p1 = new Point(2, 2);
var p2 = new Point.fromJson({'x': 1, 'y': 2});
```

{{site.alert.version-note}}
  The `new` keyword became optional in Dart 2.
{{site.alert.end}}

Some classes provide [constant constructors](#constant-constructors).
To create a compile-time constant using a constant constructor,
put the `const` keyword before the constructor name:

<?code-excerpt "misc/test/language_tour/classes_test.dart (const)"?>
```dart
var p = const ImmutablePoint(2, 2);
```

Constructing two identical compile-time constants results in a single,
canonical instance:

<?code-excerpt "misc/test/language_tour/classes_test.dart (identical)"?>
```dart
var a = const ImmutablePoint(1, 1);
var b = const ImmutablePoint(1, 1);

assert(identical(a, b)); // They are the same instance!
```

Within a _constant context_, you can omit the `const` before a constructor
or literal. For example, look at this code, which creates a const map:

<?code-excerpt "misc/test/language_tour/classes_test.dart (const-context-withconst)" replace="/pointAndLine1/pointAndLine/g"?>
```dart
// Lots of const keywords here.
const pointAndLine = const {
  'point': const [const ImmutablePoint(0, 0)],
  'line': const [const ImmutablePoint(1, 10), const ImmutablePoint(-2, 11)],
};
```

You can omit all but the first use of the `const` keyword:

<?code-excerpt "misc/test/language_tour/classes_test.dart (const-context-noconst)" replace="/pointAndLine2/pointAndLine/g"?>
```dart
// Only one const, which establishes the constant context.
const pointAndLine = {
  'point': [ImmutablePoint(0, 0)],
  'line': [ImmutablePoint(1, 10), ImmutablePoint(-2, 11)],
};
```

If a constant constructor is outside of a constant context
and is invoked without `const`,
it creates a **non-constant object**:

<?code-excerpt "misc/test/language_tour/classes_test.dart (nonconst-const-constructor)"?>
```dart
var a = const ImmutablePoint(1, 1); // Creates a constant
var b = ImmutablePoint(1, 1); // Does NOT create a constant

assert(!identical(a, b)); // NOT the same instance!
```

{{site.alert.version-note}}
  The `const` keyword became optional within a constant context in Dart 2.
{{site.alert.end}}


### Getting an object's type

To get an object's type at runtime,
you can use Object's `runtimeType` property,
which returns a [Type][] object.

<?code-excerpt "misc/test/language_tour/classes_test.dart (runtimeType)"?>
```dart
print('The type of a is ${a.runtimeType}');
```

Up to here, you've seen how to _use_ classes.
The rest of this section shows how to _implement_ classes.


### Instance variables

Here’s how you declare instance variables:

<?code-excerpt "misc/lib/language_tour/classes/point_with_main.dart (class)"?>
```dart
class Point {
  num x; // Declare instance variable x, initially null.
  num y; // Declare y, initially null.
  num z = 0; // Declare z, initially 0.
}
```

All uninitialized instance variables have the value `null`.

All instance variables generate an implicit *getter* method. Non-final
instance variables also generate an implicit *setter* method. For details,
see [Getters and setters](#getters-and-setters).

<?code-excerpt "misc/lib/language_tour/classes/point_with_main.dart (class+main)" replace="/(num .*?;).*/$1/g" plaster="none"?>
```dart
class Point {
  num x;
  num y;
}

void main() {
  var point = Point();
  point.x = 4; // Use the setter method for x.
  assert(point.x == 4); // Use the getter method for x.
  assert(point.y == null); // Values default to null.
}
```

If you initialize an instance variable where it is declared (instead of
in a constructor or method), the value is set when the instance is
created, which is before the constructor and its initializer list
execute.


### Constructors

Declare a constructor by creating a function with the same name as its
class (plus, optionally, an additional identifier as described in
[Named constructors](#named-constructors)).
The most common form of constructor, the generative constructor, creates
a new instance of a class:

<?code-excerpt "misc/lib/language_tour/classes/point_alt.dart (constructor-long-way)" plaster="none"?>
```dart
class Point {
  num x, y;

  Point(num x, num y) {
    // There's a better way to do this, stay tuned.
    this.x = x;
    this.y = y;
  }
}
```

The `this` keyword refers to the current instance.

{{site.alert.note}}
  Use `this` only when there is a name conflict. Otherwise, Dart style
  omits the `this`.
{{site.alert.end}}

The pattern of assigning a constructor argument to an instance variable
is so common, Dart has syntactic sugar to make it easy:

<?code-excerpt "misc/lib/language_tour/classes/point.dart (constructor-initializer)" plaster="none"?>
```dart
class Point {
  num x, y;

  // Syntactic sugar for setting x and y
  // before the constructor body runs.
  Point(this.x, this.y);
}
```

#### Default constructors

If you don’t declare a constructor, a default constructor is provided
for you. The default constructor has no arguments and invokes the
no-argument constructor in the superclass.

#### Constructors aren’t inherited

Subclasses don’t inherit constructors from their superclass. A subclass
that declares no constructors has only the default (no argument, no
name) constructor.

#### Named constructors

Use a named constructor to implement multiple constructors for a class
or to provide extra clarity:

<?code-excerpt "misc/lib/language_tour/classes/point.dart (named-constructor)" replace="/Point\.\S*/[!$&!]/g" plaster="none"?>
{% prettify dart tag=pre+code %}
class Point {
  num x, y;

  Point(this.x, this.y);

  // Named constructor
  [!Point.origin()!] {
    x = 0;
    y = 0;
  }
}
{% endprettify %}

Remember that constructors are not inherited, which means that a
superclass’s named constructor is not inherited by a subclass. If you
want a subclass to be created with a named constructor defined in the
superclass, you must implement that constructor in the subclass.

#### Invoking a non-default superclass constructor

By default, a constructor in a subclass calls the superclass’s unnamed,
no-argument constructor.
The superclass's constructor is called at the beginning of the
constructor body. If an [initializer list](#initializer-list)
is also being used, it executes before the superclass is called.
In summary, the order of execution is as follows:

1. initializer list
1. superclass's no-arg constructor
1. main class's no-arg constructor

If the superclass doesn’t have an unnamed, no-argument constructor,
then you must manually call one of the constructors in the
superclass. Specify the superclass constructor after a colon (`:`), just
before the constructor body (if any).

In the following example, the constructor for the Employee class calls the named
constructor for its superclass, Person. Click **Run** to execute the code.

{% comment %}
https://gist.github.com/Sfshaza/e57aa06401e6618d4eb8
{{site.dartpad}}/e57aa06401e6618d4eb8

<?code-excerpt "misc/lib/language_tour/classes/employee.dart" plaster="none"?>
```dart
class Person {
  String firstName;

  Person.fromJson(Map data) {
    print('in Person');
  }
}

class Employee extends Person {
  // Person does not have a default constructor;
  // you must call super.fromJson(data).
  Employee.fromJson(Map data) : super.fromJson(data) {
    print('in Employee');
  }
}

void main() {
  var emp = Employee.fromJson({});
  // Prints:
  // in Person
  // in Employee

  if (emp is Person) {
    // Type check
    emp.firstName = 'Bob';
  }
  (emp as Person).firstName = 'Bob';
}
```
{% endcomment %}

<iframe
src="{{site.dartpad-embed-inline}}?id=e57aa06401e6618d4eb8&split=90"
    width="100%"
    height="500px"
    style="border: 1px solid #ccc;">
</iframe>

Because the arguments to the superclass constructor are evaluated before
invoking the constructor, an argument can be an expression such as a
function call:

<?code-excerpt "misc/lib/language_tour/classes/employee.dart (method-then-constructor)"?>
```dart
class Employee extends Person {
  Employee() : super.fromJson(defaultData);
  // ···
}
```

{{site.alert.warning}}
  Arguments to the superclass constructor do not have access to `this`. For
  example, arguments can call static methods but not instance methods.
{{site.alert.end}}

#### Initializer list

Besides invoking a superclass constructor, you can also initialize
instance variables before the constructor body runs. Separate
initializers with commas.

<?code-excerpt "misc/lib/language_tour/classes/point_alt.dart (initializer-list)"?>
```dart
// Initializer list sets instance variables before
// the constructor body runs.
Point.fromJson(Map<String, num> json)
    : x = json['x'],
      y = json['y'] {
  print('In Point.fromJson(): ($x, $y)');
}
```

{{site.alert.warning}}
  The right-hand side of an initializer does not have access to `this`.
{{site.alert.end}}

During development, you can validate inputs by using `assert` in the
initializer list.

<?code-excerpt "misc/lib/language_tour/classes/point_alt.dart (initializer-list-with-assert)" replace="/assert\(.*?\)/[!$&!]/g"?>
{% prettify dart tag=pre+code %}
Point.withAssert(this.x, this.y) : [!assert(x >= 0)!] {
  print('In Point.withAssert(): ($x, $y)');
}
{% endprettify %}

{% comment %}
[PENDING: the example could be better.
Note that DartPad doesn't support this yet?

https://github.com/dart-lang/sdk/issues/30968
https://github.com/dart-lang/sdk/blob/master/docs/language/informal/assert-in-initializer-list.md]
{% endcomment %}

Initializer lists are handy when setting up final fields. The following example
initializes three final fields in an initializer list. Click **Run** to execute
the code.

{% comment %}
https://gist.github.com/Sfshaza/7a9764702c0608711e08
{{site.dartpad}}/a9764702c0608711e08

<?code-excerpt "misc/lib/language_tour/classes/point_with_distance_field.dart"?>
```dart
import 'dart:math';

class Point {
  final num x;
  final num y;
  final num distanceFromOrigin;

  Point(num x, num y)
      : x = x,
        y = y,
        distanceFromOrigin = sqrt(x * x + y * y);
}

void main() {
  var p = Point(2, 3);
  print(p.distanceFromOrigin);
}
```
{% endcomment %}

<iframe
src="{{site.dartpad-embed-inline}}?id=7a9764702c0608711e08&split=90"
    width="100%"
    height="420px"
    style="border: 1px solid #ccc;">
</iframe>


#### Redirecting constructors

Sometimes a constructor’s only purpose is to redirect to another
constructor in the same class. A redirecting constructor’s body is
empty, with the constructor call appearing after a colon (:).

<?code-excerpt "misc/lib/language_tour/classes/point_redirecting.dart"?>
```dart
class Point {
  num x, y;

  // The main constructor for this class.
  Point(this.x, this.y);

  // Delegates to the main constructor.
  Point.alongXAxis(num x) : this(x, 0);
}
```

#### Constant constructors

If your class produces objects that never change, you can make these
objects compile-time constants. To do this, define a `const` constructor
and make sure that all instance variables are `final`.

<?code-excerpt "misc/lib/language_tour/classes/immutable_point.dart"?>
```dart
class ImmutablePoint {
  static final ImmutablePoint origin =
      const ImmutablePoint(0, 0);

  final num x, y;

  const ImmutablePoint(this.x, this.y);
}
```

Constant constructors don't always create constants.
For details, see the section on
[using constructors](#using-constructors).


#### Factory constructors

Use the `factory` keyword when implementing a constructor that doesn’t
always create a new instance of its class. For example, a factory
constructor might return an instance from a cache, or it might return an
instance of a subtype.

The following example demonstrates a factory constructor returning
objects from a cache:

<?code-excerpt "misc/lib/language_tour/classes/logger.dart"?>
```dart
class Logger {
  final String name;
  bool mute = false;

  // _cache is library-private, thanks to
  // the _ in front of its name.
  static final Map<String, Logger> _cache =
      <String, Logger>{};

  factory Logger(String name) {
    return _cache.putIfAbsent(
        name, () => Logger._internal(name));
  }

  Logger._internal(this.name);

  void log(String msg) {
    if (!mute) print(msg);
  }
}
```

{{site.alert.note}}
  Factory constructors have no access to `this`.
{{site.alert.end}}

Invoke a factory constructor just like you would any other constructor:

<?code-excerpt "misc/lib/language_tour/classes/logger.dart (logger)"?>
```dart
var logger = Logger('UI');
logger.log('Button clicked');
```


### Methods

Methods are functions that provide behavior for an object.

#### Instance methods

Instance methods on objects can access instance variables and `this`.
The `distanceTo()` method in the following sample is an example of an
instance method:

<?code-excerpt "misc/lib/language_tour/classes/point.dart (class-with-distanceTo)" plaster="none"?>
```dart
import 'dart:math';

class Point {
  num x, y;

  Point(this.x, this.y);

  num distanceTo(Point other) {
    var dx = x - other.x;
    var dy = y - other.y;
    return sqrt(dx * dx + dy * dy);
  }
}
```

#### Getters and setters

Getters and setters are special methods that provide read and write
access to an object’s properties. Recall that each instance variable has
an implicit getter, plus a setter if appropriate. You can create
additional properties by implementing getters and setters, using the
`get` and `set` keywords:

<?code-excerpt "misc/lib/language_tour/classes/rectangle.dart"?>
```dart
class Rectangle {
  num left, top, width, height;

  Rectangle(this.left, this.top, this.width, this.height);

  // Define two calculated properties: right and bottom.
  num get right => left + width;
  set right(num value) => left = value - width;
  num get bottom => top + height;
  set bottom(num value) => top = value - height;
}

void main() {
  var rect = Rectangle(3, 4, 20, 15);
  assert(rect.left == 3);
  rect.right = 12;
  assert(rect.left == -8);
}
```

With getters and setters, you can start with instance variables, later
wrapping them with methods, all without changing client code.

{{site.alert.note}}
  Operators such as increment (++) work in the expected way, whether or
  not a getter is explicitly defined. To avoid any unexpected side
  effects, the operator calls the getter exactly once, saving its value
  in a temporary variable.
{{site.alert.end}}

#### Abstract methods

Instance, getter, and setter methods can be abstract, defining an
interface but leaving its implementation up to other classes.
Abstract methods can only exist in [abstract classes](#abstract-classes).

To make a method abstract, use a semicolon (;) instead of a method body:

<?code-excerpt "misc/lib/language_tour/classes/doer.dart"?>
```dart
abstract class Doer {
  // Define instance variables and methods...

  void doSomething(); // Define an abstract method.
}

class EffectiveDoer extends Doer {
  void doSomething() {
    // Provide an implementation, so the method is not abstract here...
  }
}
```


### Abstract classes

Use the `abstract` modifier to define an *abstract class*—a class that
can’t be instantiated. Abstract classes are useful for defining
interfaces, often with some implementation. If you want your abstract
class to appear to be instantiable, define a [factory
constructor](#factory-constructors).

Abstract classes often have [abstract methods](#abstract-methods).
Here’s an example of declaring an abstract class that has an abstract
method:

<?code-excerpt "misc/lib/language_tour/classes/misc.dart (abstract)"?>
```dart
// This class is declared abstract and thus
// can't be instantiated.
abstract class AbstractContainer {
  // Define constructors, fields, methods...

  void updateChildren(); // Abstract method.
}
```


### Implicit interfaces

Every class implicitly defines an interface containing all the instance
members of the class and of any interfaces it implements. If you want to
create a class A that supports class B’s API without inheriting B’s
implementation, class A should implement the B interface.

A class implements one or more interfaces by declaring them in an
`implements` clause and then providing the APIs required by the
interfaces. For example:

<?code-excerpt "misc/lib/language_tour/classes/impostor.dart"?>
```dart
// A person. The implicit interface contains greet().
class Person {
  // In the interface, but visible only in this library.
  final _name;

  // Not in the interface, since this is a constructor.
  Person(this._name);

  // In the interface.
  String greet(String who) => 'Hello, $who. I am $_name.';
}

// An implementation of the Person interface.
class Impostor implements Person {
  get _name => '';

  String greet(String who) => 'Hi $who. Do you know who I am?';
}

String greetBob(Person person) => person.greet('Bob');

void main() {
  print(greetBob(Person('Kathy')));
  print(greetBob(Impostor()));
}
```

Here’s an example of specifying that a class implements multiple
interfaces:

<?code-excerpt "misc/lib/language_tour/classes/misc.dart (point_interfaces)"?>
```dart
class Point implements Comparable, Location {...}
```


### Extending a class

Use `extends` to create a subclass, and `super` to refer to the
superclass:

<?code-excerpt "misc/lib/language_tour/classes/extends.dart" replace="/extends|super/[!$&!]/g"?>
{% prettify dart tag=pre+code %}
class Television {
  void turnOn() {
    _illuminateDisplay();
    _activateIrSensor();
  }
  // ···
}

class SmartTelevision [!extends!] Television {
  void turnOn() {
    [!super!].turnOn();
    _bootNetworkInterface();
    _initializeMemory();
    _upgradeApps();
  }
  // ···
}
{% endprettify %}




#### Overriding members

Subclasses can override instance methods, getters, and setters.
You can use the `@override` annotation to indicate that you are
intentionally overriding a member:

<?code-excerpt "misc/lib/language_tour/metadata/television.dart (override)" replace="/@override/[!$&!]/g"?>
{% prettify dart tag=pre+code %}
class SmartTelevision extends Television {
  [!@override!]
  void turnOn() {...}
  // ···
}
{% endprettify %}

To narrow the type of a method parameter or instance variable in code that is
[type safe](/guides/language/sound-dart),
you can use the [`covariant` keyword](/guides/language/sound-problems#the-covariant-keyword).


#### Overridable operators

You can override the operators shown in the following table.
For example, if you define a
Vector class, you might define a `+` method to add two vectors.

`<`  | `+`  | `|`  | `[]`
`>`  | `/`  | `^`  | `[]=`
`<=` | `~/` | `&`  | `~`
`>=` | `*`  | `<<` | `==`
`–`  | `%`  | `>>`
{:.table}

{{site.alert.note}}
  You may have noticed that `!=` is not an overridable operator. The expression
  `e1 != e2` is just syntactic sugar for `!(e1 == e2)`.
{{site.alert.end}}

Here’s an example of a class that overrides the `+` and `-` operators:

<?code-excerpt "misc/lib/language_tour/classes/vector.dart"?>
```dart
class Vector {
  final int x, y;

  Vector(this.x, this.y);

  Vector operator +(Vector v) => Vector(x + v.x, y + v.y);
  Vector operator -(Vector v) => Vector(x - v.x, y - v.y);

  // Operator == and hashCode not shown. For details, see note below.
  // ···
}

void main() {
  final v = Vector(2, 3);
  final w = Vector(2, 2);

  assert(v + w == Vector(4, 5));
  assert(v - w == Vector(0, 1));
}
```

If you override `==`, you should also override Object's `hashCode` getter.
For an example of overriding `==` and `hashCode`, see
[Implementing map keys](/guides/libraries/library-tour#implementing-map-keys).

For more information on overriding, in general, see
[Extending a class](#extending-a-class).


#### noSuchMethod()

To detect or react whenever code attempts to use a non-existent method or
instance variable, you can override `noSuchMethod()`:

<?code-excerpt "misc/lib/language_tour/classes/no_such_method.dart" replace="/noSuchMethod(?!,)/[!$&!]/g"?>
{% prettify dart tag=pre+code %}
class A {
  // Unless you override noSuchMethod, using a
  // non-existent member results in a NoSuchMethodError.
  @override
  void [!noSuchMethod!](Invocation invocation) {
    print('You tried to use a non-existent member: ' +
        '${invocation.memberName}');
  }
}
{% endprettify %}

You **can't invoke** an unimplemented method unless
**one** of the following is true:

* The receiver has the static type `dynamic`.

* The receiver has a static type that
defines the unimplemented method (abstract is OK),
and the dynamic type of the receiver has an implemention of `noSuchMethod()`
that's different from the one in class `Object`.

For more information, see the informal
[noSuchMethod forwarding specification.](https://github.com/dart-lang/sdk/blob/master/docs/language/informal/nosuchmethod-forwarding.md)


### Extension methods

Extension methods, introduced in Dart 2.7,
are a way to add functionality to existing libraries.
You might use extension methods without even knowing it.
For example, when you use code completion in an IDE,
it suggests extension methods alongside regular methods.

Here's an example of using an extension method on `String`
named `parseInt()` that's defined in `string_apis.dart`:

```dart
import 'string_apis.dart';
...
print('42'.padLeft(5)); // Use a String method.
print('42'.parseInt()); // Use an extension method.
```

For details of using and implementing extension methods, see the
[extension methods page][].

<a id="enums"></a>
### Enumerated types

Enumerated types, often called _enumerations_ or _enums_,
are a special kind of class used to represent
a fixed number of constant values.


#### Using enums

Declare an enumerated type using the `enum` keyword:

<?code-excerpt "misc/lib/language_tour/classes/enum.dart (enum)"?>
```dart
enum Color { red, green, blue }
```

Each value in an enum has an `index` getter,
which returns the zero-based position of the value in the enum declaration.
For example, the first value has index 0,
and the second value has index 1.

<?code-excerpt "misc/lib/language_tour/classes/enum.dart (index)"?>
```dart
assert(Color.red.index == 0);
assert(Color.green.index == 1);
assert(Color.blue.index == 2);
```

To get a list of all of the values in the enum,
use the enum's `values` constant.

<?code-excerpt "misc/lib/language_tour/classes/enum.dart (values)"?>
```dart
List<Color> colors = Color.values;
assert(colors[2] == Color.blue);
```

You can use enums in [switch statements](#switch-and-case), and
you'll get a warning if you don't handle all of the enum's values:

<?code-excerpt "misc/lib/language_tour/classes/enum.dart (switch)"?>
```dart
var aColor = Color.blue;

switch (aColor) {
  case Color.red:
    print('Red as roses!');
    break;
  case Color.green:
    print('Green as grass!');
    break;
  default: // Without this, you see a WARNING.
    print(aColor); // 'Color.blue'
}
```

Enumerated types have the following limits:

* You can't subclass, mix in, or implement an enum.
* You can't explicitly instantiate an enum.

For more information, see the [Dart language specification][].


### Adding features to a class: mixins

Mixins are a way of reusing a class's code in multiple class
hierarchies.

To _use_ a mixin, use the `with` keyword followed by one or more mixin
names. The following example shows two classes that use mixins:

<?code-excerpt "misc/lib/language_tour/classes/orchestra.dart (Musician and Maestro)" replace="/(with.*) \{/[!$1!] {/g"?>
{% prettify dart tag=pre+code %}
class Musician extends Performer [!with Musical!] {
  // ···
}

class Maestro extends Person
    [!with Musical, Aggressive, Demented!] {
  Maestro(String maestroName) {
    name = maestroName;
    canConduct = true;
  }
}
{% endprettify %}

To _implement_ a mixin, create a class that extends Object and
declares no constructors.
Unless you want your mixin to be usable as a regular class,
use the `mixin` keyword instead of `class`.
For example:

<?code-excerpt "misc/lib/language_tour/classes/orchestra.dart (Musical)"?>
```dart
mixin Musical {
  bool canPlayPiano = false;
  bool canCompose = false;
  bool canConduct = false;

  void entertainMe() {
    if (canPlayPiano) {
      print('Playing piano');
    } else if (canConduct) {
      print('Waving hands');
    } else {
      print('Humming to self');
    }
  }
}
```

To specify that only certain types can use the mixin — for example,
so your mixin can invoke a method that it doesn't define —
use `on` to specify the required superclass:

<?code-excerpt "misc/lib/language_tour/classes/orchestra.dart (mixin-on)"?>
```dart
mixin MusicalPerformer on Musician {
  // ···
}
```

{{site.alert.version-note}}
  Support for the `mixin` keyword was introduced in Dart 2.1. Code in earlier
  releases usually used `abstract class` instead. For more information on 2.1
  mixin changes, see the [Dart SDK changelog][] and [2.1 mixin specification.][]
{{site.alert.end}}

[Dart SDK changelog]: https://github.com/dart-lang/sdk/blob/master/CHANGELOG.md
[2.1 mixin specification.]: https://github.com/dart-lang/language/blob/master/accepted/2.1/super-mixins/feature-specification.md#dart-2-mixin-declarations


### Class variables and methods

Use the `static` keyword to implement class-wide variables and methods.

#### Static variables

Static variables (class variables) are useful for class-wide state and
constants:

<?code-excerpt "misc/lib/language_tour/classes/misc.dart (static-field)"?>
```dart
class Queue {
  static const initialCapacity = 16;
  // ···
}

void main() {
  assert(Queue.initialCapacity == 16);
}
```

Static variables aren’t initialized until they’re used.

{{site.alert.note}}
  This page follows the [style guide
  recommendation](/guides/language/effective-dart/style#identifiers)
  of preferring `lowerCamelCase` for constant names.
{{site.alert.end}}

#### Static methods

Static methods (class methods) do not operate on an instance, and thus
do not have access to `this`. For example:

<?code-excerpt "misc/lib/language_tour/classes/point_with_distance_method.dart"?>
```dart
import 'dart:math';

class Point {
  num x, y;
  Point(this.x, this.y);

  static num distanceBetween(Point a, Point b) {
    var dx = a.x - b.x;
    var dy = a.y - b.y;
    return sqrt(dx * dx + dy * dy);
  }
}

void main() {
  var a = Point(2, 2);
  var b = Point(4, 4);
  var distance = Point.distanceBetween(a, b);
  assert(2.8 < distance && distance < 2.9);
  print(distance);
}
```

{{site.alert.note}}
  Consider using top-level functions, instead of static methods, for
  common or widely used utilities and functionality.
{{site.alert.end}}

You can use static methods as compile-time constants. For example, you
can pass a static method as a parameter to a constant constructor.


## Generics

If you look at the API documentation for the basic array type,
[List,][List] you’ll see that the
type is actually `List<E>`. The \<...\> notation marks List as a
*generic* (or *parameterized*) type—a type that has formal type
parameters. [By convention][], most type variables have single-letter names,
such as E, T, S, K, and V.

[By convention]: /guides/language/effective-dart/design#do-follow-existing-mnemonic-conventions-when-naming-type-parameters


### Why use generics?

Generics are often required for type safety, but they have more benefits
than just allowing your code to run:

* Properly specifying generic types results in better generated code.
* You can use generics to reduce code duplication.

If you intend for a list to contain only strings, you can
declare it as `List<String>` (read that as “list of string”). That way
you, your fellow programmers, and your tools can detect that assigning a non-string to
the list is probably a mistake. Here’s an example:

{:.fails-sa}
<?code-excerpt "misc/lib/language_tour/generics/misc.dart (why-generics)"?>
```dart
var names = List<String>();
names.addAll(['Seth', 'Kathy', 'Lars']);
names.add(42); // Error
```

Another reason for using generics is to reduce code duplication.
Generics let you share a single interface and implementation between
many types, while still taking advantage of static
analysis. For example, say you create an interface for
caching an object:

<?code-excerpt "misc/lib/language_tour/generics/cache.dart (ObjectCache)"?>
```dart
abstract class ObjectCache {
  Object getByKey(String key);
  void setByKey(String key, Object value);
}
```

You discover that you want a string-specific version of this interface,
so you create another interface:

<?code-excerpt "misc/lib/language_tour/generics/cache.dart (StringCache)"?>
```dart
abstract class StringCache {
  String getByKey(String key);
  void setByKey(String key, String value);
}
```

Later, you decide you want a number-specific version of this
interface... You get the idea.

Generic types can save you the trouble of creating all these interfaces.
Instead, you can create a single interface that takes a type parameter:

<?code-excerpt "misc/lib/language_tour/generics/cache.dart (Cache)"?>
```dart
abstract class Cache<T> {
  T getByKey(String key);
  void setByKey(String key, T value);
}
```

In this code, T is the stand-in type. It’s a placeholder that you can
think of as a type that a developer will define later.


### Using collection literals

List, set, and map literals can be parameterized. Parameterized literals are
just like the literals you’ve already seen, except that you add
<code>&lt;<em>type</em>></code> (for lists and sets) or
<code>&lt;<em>keyType</em>, <em>valueType</em>></code> (for maps)
before the opening bracket. Here is an example of using typed literals:

<?code-excerpt "misc/lib/language_tour/generics/misc.dart (collection-literals)"?>
```dart
var names = <String>['Seth', 'Kathy', 'Lars'];
var uniqueNames = <String>{'Seth', 'Kathy', 'Lars'};
var pages = <String, String>{
  'index.html': 'Homepage',
  'robots.txt': 'Hints for web robots',
  'humans.txt': 'We are people, not machines'
};
```


### Using parameterized types with constructors

To specify one or more types when using a constructor, put the types in
angle brackets (`<...>`) just after the class name. For example:

<?code-excerpt "misc/test/language_tour/generics_test.dart (constructor-1)"?>
```dart
var nameSet = Set<String>.from(names);
```

{% comment %}[PENDING: update this sample; it ]{% endcomment %}

The following code creates a map that has integer keys and values of
type View:

<?code-excerpt "misc/test/language_tour/generics_test.dart (constructor-2)"?>
```dart
var views = Map<int, View>();
```


### Generic collections and the types they contain

Dart generic types are *reified*, which means that they carry their type
information around at runtime. For example, you can test the type of a
collection:

<?code-excerpt "misc/test/language_tour/generics_test.dart (generic-collections)"?>
```dart
var names = List<String>();
names.addAll(['Seth', 'Kathy', 'Lars']);
print(names is List<String>); // true
```

{{site.alert.note}}
  In contrast, generics in Java use *erasure*, which means that generic
  type parameters are removed at runtime. In Java, you can test whether
  an object is a List, but you can’t test whether it’s a `List<String>`.
{{site.alert.end}}


### Restricting the parameterized type

When implementing a generic type,
you might want to limit the types of its parameters.
You can do this using `extends`.

<?code-excerpt "misc/lib/language_tour/generics/base_class.dart" replace="/extends SomeBaseClass(?=. \{)/[!$&!]/g"?>
{% prettify dart tag=pre+code %}
class Foo<T [!extends SomeBaseClass!]> {
  // Implementation goes here...
  String toString() => "Instance of 'Foo<$T>'";
}

class Extender extends SomeBaseClass {...}
{% endprettify %}

It's OK to use `SomeBaseClass` or any of its subclasses as generic argument:

<?code-excerpt "misc/test/language_tour/generics_test.dart (SomeBaseClass-ok)" replace="/Foo.\w+./[!$&!]/g"?>
{% prettify dart tag=pre+code %}
var someBaseClassFoo = [!Foo<SomeBaseClass>!]();
var extenderFoo = [!Foo<Extender>!]();
{% endprettify %}

It's also OK to specify no generic argument:

<?code-excerpt "misc/test/language_tour/generics_test.dart (no-generic-arg-ok)" replace="/expect\((.*?).toString\(\), .(.*?).\);/print($1); \/\/ $2/g"?>
```dart
var foo = Foo();
print(foo); // Instance of 'Foo<SomeBaseClass>'
```

Specifying any non-`SomeBaseClass` type results in an error:

{:.fails-sa}
<?code-excerpt "misc/lib/language_tour/generics/misc.dart (Foo-Object-error)" replace="/Foo.\w+./[!$&!]/g"?>
{% prettify dart tag=pre+code %}
var foo = [!Foo<Object>!]();
{% endprettify %}


### Using generic methods

Initially, Dart's generic support was limited to classes.
A newer syntax, called _generic methods_, allows type arguments on methods and functions:

<!-- {{site.dartpad}}/a02c53b001977efa4d803109900f21bb -->
<!-- https://gist.github.com/a02c53b001977efa4d803109900f21bb -->
<?code-excerpt "misc/test/language_tour/generics_test.dart (method)" replace="/<T.(?=\()|T/[!$&!]/g"?>
{% prettify dart tag=pre+code %}
[!T!] first[!<T>!](List<[!T!]> ts) {
  // Do some initial work or error checking, then...
  [!T!] tmp = ts[0];
  // Do some additional checking or processing...
  return tmp;
}
{% endprettify %}

Here the generic type parameter on `first` (`<T>`)
allows you to use the type argument `T` in several places:

* In the function's return type (`T`).
* In the type of an argument (`List<T>`).
* In the type of a local variable (`T tmp`).

For more information about generics, see
[Using Generic Methods.](https://github.com/dart-lang/sdk/blob/master/pkg/dev_compiler/doc/GENERIC_METHODS.md)


## Libraries and visibility

The `import` and `library` directives can help you create a
modular and shareable code base. Libraries not only provide APIs, but
are a unit of privacy: identifiers that start with an underscore (\_)
are visible only inside the library. *Every Dart app is a library*, even
if it doesn’t use a `library` directive.

Libraries can be distributed using [packages](/guides/packages).


### Using libraries

Use `import` to specify how a namespace from one library is used in the
scope of another library.

For example, Dart web apps generally use the [dart:html][]
library, which they can import like this:

<?code-excerpt "misc/test/language_tour/browser_test.dart (dart-html-import)"?>
```dart
import 'dart:html';
```

The only required argument to `import` is a URI specifying the
library.
For built-in libraries, the URI has the special `dart:` scheme.
For other libraries, you can use a file system path or the `package:`
scheme. The `package:` scheme specifies libraries provided by a package
manager such as the pub tool. For example:

<?code-excerpt "misc/test/language_tour/browser_test.dart (package-import)"?>
```dart
import 'package:test/test.dart';
```

{{site.alert.note}}
  *URI* stands for uniform resource identifier.
  *URLs* (uniform resource locators) are a common kind of URI.
{{site.alert.end}}


#### Specifying a library prefix

If you import two libraries that have conflicting identifiers, then you
can specify a prefix for one or both libraries. For example, if library1
and library2 both have an Element class, then you might have code like
this:

<?code-excerpt "misc/lib/language_tour/libraries/import_as.dart" replace="/(lib\d)\.dart/package:$1\/$&/g"?>
```dart
import 'package:lib1/lib1.dart';
import 'package:lib2/lib2.dart' as lib2;

// Uses Element from lib1.
Element element1 = Element();

// Uses Element from lib2.
lib2.Element element2 = lib2.Element();
```

#### Importing only part of a library

If you want to use only part of a library, you can selectively import
the library. For example:

<?code-excerpt "misc/lib/language_tour/libraries/show_hide.dart" replace="/(lib\d)\.dart/package:$1\/$&/g"?>
```dart
// Import only foo.
import 'package:lib1/lib1.dart' show foo;

// Import all names EXCEPT foo.
import 'package:lib2/lib2.dart' hide foo;
```

<a id="deferred-loading"></a>
#### Lazily loading a library

_Deferred loading_ (also called _lazy loading_)
allows a web app to load a library on demand,
if and when the library is needed.
Here are some cases when you might use deferred loading:

* To reduce a web app's initial startup time.
* To perform A/B testing—trying out
  alternative implementations of an algorithm, for example.
* To load rarely used functionality, such as optional screens and dialogs.

{{site.alert.warn}}
  **Only dart2js supports deferred loading.**
  Flutter, the Dart VM, and dartdevc don't support deferred loading.
  For more information, see
  [issue #33118](https://github.com/dart-lang/sdk/issues/33118) and
  [issue #27776.](https://github.com/dart-lang/sdk/issues/27776)
{{site.alert.end}}

To lazily load a library, you must first
import it using `deferred as`.

<?code-excerpt "misc/lib/language_tour/libraries/greeter.dart (import)" replace="/hello\.dart/package:greetings\/$&/g"?>
```dart
import 'package:greetings/hello.dart' deferred as hello;
```

When you need the library, invoke
`loadLibrary()` using the library's identifier.

<?code-excerpt "misc/lib/language_tour/libraries/greeter.dart (loadLibrary)"?>
```dart
Future greet() async {
  await hello.loadLibrary();
  hello.printGreeting();
}
```

In the preceding code,
the `await` keyword pauses execution until the library is loaded.
For more information about `async` and `await`,
see [asynchrony support](#asynchrony-support).

You can invoke `loadLibrary()` multiple times on a library without problems.
The library is loaded only once.

Keep in mind the following when you use deferred loading:

* A deferred library's constants aren't constants in the importing file.
  Remember, these constants don't exist until the deferred library is loaded.
* You can't use types from a deferred library in the importing file.
  Instead, consider moving interface types to a library imported by
  both the deferred library and the importing file.
* Dart implicitly inserts `loadLibrary()` into the namespace that you define
  using <code>deferred as <em>namespace</em></code>.
  The `loadLibrary()` function returns a [Future](/guides/libraries/library-tour#future).


### Implementing libraries

See
[Create Library Packages](/guides/libraries/create-library-packages)
for advice on how to implement a library package, including:

* How to organize library source code.
* How to use the `export` directive.
* When to use the `part` directive.
* When to use the `library` directive.
* How to use conditional imports and exports to implement
  a library that supports multiple platforms.


<a id="asynchrony"></a>
## Asynchrony support

Dart libraries are full of functions that
return [Future][] or [Stream][] objects.
These functions are _asynchronous_:
they return after setting up
a possibly time-consuming operation
(such as I/O),
without waiting for that operation to complete.

The `async` and `await` keywords support asynchronous programming,
letting you write asynchronous code that
looks similar to synchronous code.


<a id="await"></a>
### Handling Futures

When you need the result of a completed Future,
you have two options:

* Use `async` and `await`.
* Use the Future API, as described
  [in the library tour](/guides/libraries/library-tour#future).

Code that uses `async` and `await` is asynchronous,
but it looks a lot like synchronous code.
For example, here's some code that uses `await`
to wait for the result of an asynchronous function:

<?code-excerpt "misc/lib/language_tour/async.dart (await-lookUpVersion)"?>
```dart
await lookUpVersion();
```

To use `await`, code must be in an `async` function—a
function marked as `async`:

<?code-excerpt "misc/lib/language_tour/async.dart (checkVersion)" replace="/async|await/[!$&!]/g"?>
{% prettify dart tag=pre+code %}
Future checkVersion() [!async!] {
  var version = [!await!] lookUpVersion();
  // Do something with version
}
{% endprettify %}

{{site.alert.note}}
  Although an `async` function might perform time-consuming operations, it
  doesn't wait for those operations. Instead, the `async` function executes only
  until it encounters its first `await` expression
  ([details][synchronous-async-start]). Then it returns a Future object,
  resuming execution only after the `await` expression completes.
{{site.alert.end}}

Use `try`, `catch`, and `finally` to handle errors and cleanup in code that uses
`await`:

<?code-excerpt "misc/lib/language_tour/async.dart (try-catch)"?>
```dart
try {
  version = await lookUpVersion();
} catch (e) {
  // React to inability to look up the version
}
```

You can use `await` multiple times in an `async` function.
For example, the following code waits three times
for the results of functions:

<?code-excerpt "misc/lib/language_tour/async.dart (repeated-await)"?>
```dart
var entrypoint = await findEntrypoint();
var exitCode = await runExecutable(entrypoint, args);
await flushThenExit(exitCode);
```

In <code>await <em>expression</em></code>,
the value of <code><em>expression</em></code> is usually a Future;
if it isn't, then the value is automatically wrapped in a Future.
This Future object indicates a promise to return an object.
The value of <code>await <em>expression</em></code> is that returned object.
The await expression makes execution pause until that object is available.

**If you get a compile-time error when using `await`,
make sure `await` is in an `async` function.**
For example, to use `await` in your app's `main()` function,
the body of `main()` must be marked as `async`:

<?code-excerpt "misc/lib/language_tour/async.dart (main)" replace="/async|await/[!$&!]/g"?>
{% prettify dart tag=pre+code %}
Future main() [!async!] {
  checkVersion();
  print('In main: version is ${[!await!] lookUpVersion()}');
}
{% endprettify %}


<a id="async"></a>
### Declaring async functions

An `async` function is a function whose body is marked with
the `async` modifier.

Adding the `async` keyword to a function makes it return a Future.
For example, consider this synchronous function,
which returns a String:

<?code-excerpt "misc/lib/language_tour/async.dart (sync-lookUpVersion)"?>
```dart
String lookUpVersion() => '1.0.0';
```

If you change it to be an `async` function—for example,
because a future implementation will be time consuming—the
returned value is a Future:

<?code-excerpt "misc/lib/language_tour/async.dart (async-lookUpVersion)"?>
```dart
Future<String> lookUpVersion() async => '1.0.0';
```

Note that the function's body doesn't need to use the Future API.
Dart creates the Future object if necessary.
If your function doesn't return a useful value,
make its return type `Future<void>`.

For an interactive introduction to using futures, `async`, and `await`,
see the [asynchronous programming codelab](/codelabs/async-await).

{% comment %}
TODO: Where else should we cover generalized void?
{% endcomment %}


<a id="await-for"></a>
### Handling Streams

When you need to get values from a Stream,
you have two options:

* Use `async` and an _asynchronous for loop_ (`await for`).
* Use the Stream API, as described
  [in the library tour](/guides/libraries/library-tour#stream).

{{site.alert.note}}
  Before using `await for`, be sure that it makes the code clearer and that you
  really do want to wait for all of the stream's results. For example, you
  usually should **not** use `await for` for UI event listeners, because UI
  frameworks send endless streams of events.
{{site.alert.end}}

An asynchronous for loop has the following form:

<?code-excerpt "misc/lib/language_tour/async.dart (await-for)"?>
```dart
await for (varOrType identifier in expression) {
  // Executes each time the stream emits a value.
}
```

The value of <code><em>expression</em></code> must have type Stream.
Execution proceeds as follows:

1. Wait until the stream emits a value.
2. Execute the body of the for loop,
   with the variable set to that emitted value.
3. Repeat 1 and 2 until the stream is closed.

To stop listening to the stream,
you can use a `break` or `return` statement,
which breaks out of the for loop
and unsubscribes from the stream.

**If you get a compile-time error when implementing an asynchronous for loop,
make sure the `await for` is in an `async` function.**
For example, to use an asynchronous for loop in your app's `main()` function,
the body of `main()` must be marked as `async`:

<?code-excerpt "misc/lib/language_tour/async.dart (number_thinker)" replace="/async|await for/[!$&!]/g"?>
{% prettify dart tag=pre+code %}
Future main() [!async!] {
  // ...
  [!await for!] (var request in requestServer) {
    handleRequest(request);
  }
  // ...
}
{% endprettify %}

For more information about asynchronous programming, in general, see the
[dart:async](/guides/libraries/library-tour#dartasync---asynchronous-programming)
section of the library tour.


<a id="generator"></a>
## Generators

When you need to lazily produce a sequence of values,
consider using a _generator function_.
Dart has built-in support for two kinds of generator functions:

* **Synchronous** generator: Returns an **[Iterable]** object.
* **Asynchronous** generator: Returns a **[Stream]** object.

To implement a **synchronous** generator function,
mark the function body as `sync*`,
and use `yield` statements to deliver values:

<?code-excerpt "misc/test/language_tour/async_test.dart (sync-generator)"?>
```dart
Iterable<int> naturalsTo(int n) sync* {
  int k = 0;
  while (k < n) yield k++;
}
```

To implement an **asynchronous** generator function,
mark the function body as `async*`,
and use `yield` statements to deliver values:

<?code-excerpt "misc/test/language_tour/async_test.dart (async-generator)"?>
```dart
Stream<int> asynchronousNaturalsTo(int n) async* {
  int k = 0;
  while (k < n) yield k++;
}
```

If your generator is recursive,
you can improve its performance by using `yield*`:

<?code-excerpt "misc/test/language_tour/async_test.dart (recursive-generator)"?>
```dart
Iterable<int> naturalsDownFrom(int n) sync* {
  if (n > 0) {
    yield n;
    yield* naturalsDownFrom(n - 1);
  }
}
```


## Callable classes

To allow an instance of your Dart class to be called like a function,
implement the `call()` method.

In the following example, the `WannabeFunction` class defines a call() function
that takes three strings and concatenates them, separating each with a space,
and appending an exclamation. Click **Run** to execute the code.

{% comment %}
https://gist.github.com/405379bacf30335f3aed
{{site.dartpad}}/405379bacf30335f3aed

<?code-excerpt "misc/lib/language_tour/callable_classes.dart"?>
```dart
class WannabeFunction {
  String call(String a, String b, String c) => '$a $b $c!';
}

var wf = WannabeFunction();
var out = wf('Hi', 'there,', 'gang');

main() => print(out);
```
{% endcomment %}

<iframe
src="{{site.dartpad-embed-inline}}?id=405379bacf30335f3aed"
    width="100%"
    height="350px"
    style="border: 1px solid #ccc;">
</iframe>


## Isolates

Most computers, even on mobile platforms, have multi-core CPUs.
To take advantage of all those cores, developers traditionally use
shared-memory threads running concurrently. However, shared-state
concurrency is error prone and can lead to complicated code.

Instead of threads, all Dart code runs inside of *isolates*. Each
isolate has its own memory heap, ensuring that no isolate’s state is
accessible from any other isolate.

For more information, see the following:
* [Dart asynchronous programming: Isolates and event loops][isolates article]
* [dart:isolate API reference,][dart:isolate]
  including [Isolate.spawn()][] and
  [TransferableTypedData][]
* [Background parsing][background json] cookbook on the Flutter site
* [Isolate sample app][]

[isolates article]: https://medium.com/dartlang/dart-asynchronous-programming-isolates-and-event-loops-bffc3e296a6a
[Isolate.spawn()]: {{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}/dart-isolate/Isolate/spawn.html
[TransferableTypedData]: {{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}/dart-isolate/TransferableTypedData-class.html
[background json]: {{site.flutter}}/docs/cookbook/networking/background-parsing
[Isolate sample app]: https://github.com/flutter/samples/tree/master/isolate_example


## Typedefs

In Dart, functions are objects, just like strings and numbers are
objects. A *typedef*, or *function-type alias*, gives a function type a
name that you can use when declaring fields and return types. A typedef
retains type information when a function type is assigned to a variable.

Consider the following code, which doesn't use a typedef:

<?code-excerpt "misc/lib/language_tour/typedefs/sorted_collection_1.dart"?>
```dart
class SortedCollection {
  Function compare;

  SortedCollection(int f(Object a, Object b)) {
    compare = f;
  }
}

// Initial, broken implementation.
int sort(Object a, Object b) => 0;

void main() {
  SortedCollection coll = SortedCollection(sort);

  // All we know is that compare is a function,
  // but what type of function?
  assert(coll.compare is Function);
}
```

Type information is lost when assigning `f` to `compare`. The type of
`f` is `(Object, ``Object)` → `int` (where → means returns), yet the
type of `compare` is Function. If we change the code to use explicit
names and retain type information, both developers and tools can use
that information.

<?code-excerpt "misc/lib/language_tour/typedefs/sorted_collection_2.dart"?>
```dart
typedef Compare = int Function(Object a, Object b);

class SortedCollection {
  Compare compare;

  SortedCollection(this.compare);
}

// Initial, broken implementation.
int sort(Object a, Object b) => 0;

void main() {
  SortedCollection coll = SortedCollection(sort);
  assert(coll.compare is Function);
  assert(coll.compare is Compare);
}
```

{{site.alert.note}}
  Currently, typedefs are restricted to function types. We expect this to
  change.
{{site.alert.end}}

Because typedefs are simply aliases, they offer a way to check the type
of any function. For example:

<?code-excerpt "misc/lib/language_tour/typedefs/misc.dart (compare)"?>
```dart
typedef Compare<T> = int Function(T a, T b);

int sort(int a, int b) => a - b;

void main() {
  assert(sort is Compare<int>); // True!
}
```

## Metadata

Use metadata to give additional information about your code. A metadata
annotation begins with the character `@`, followed by either a reference
to a compile-time constant (such as `deprecated`) or a call to a
constant constructor.

Two annotations are available to all Dart code: `@deprecated` and
`@override`. For examples of using `@override`,
see [Extending a class](#extending-a-class).
Here’s an example of using the `@deprecated`
annotation:

<?code-excerpt "misc/lib/language_tour/metadata/television.dart (deprecated)" replace="/@deprecated/[!$&!]/g"?>
{% prettify dart tag=pre+code %}
class Television {
  /// _Deprecated: Use [turnOn] instead._
  [!@deprecated!]
  void activate() {
    turnOn();
  }

  /// Turns the TV's power on.
  void turnOn() {...}
}
{% endprettify %}

You can define your own metadata annotations. Here’s an example of
defining a @todo annotation that takes two arguments:

<?code-excerpt "misc/lib/language_tour/metadata/todo.dart"?>
```dart
library todo;

class Todo {
  final String who;
  final String what;

  const Todo(this.who, this.what);
}
```

And here’s an example of using that @todo annotation:

<?code-excerpt "misc/lib/language_tour/metadata/misc.dart"?>
```dart
import 'todo.dart';

@Todo('seth', 'make this do something')
void doSomething() {
  print('do something');
}
```

Metadata can appear before a library, class, typedef, type parameter,
constructor, factory, function, field, parameter, or variable
declaration and before an import or export directive. You can
retrieve metadata at runtime using reflection.


## Comments

Dart supports single-line comments, multi-line comments, and
documentation comments.


### Single-line comments

A single-line comment begins with `//`. Everything between `//` and the
end of line is ignored by the Dart compiler.

<?code-excerpt "misc/lib/language_tour/comments.dart (single-line-comments)"?>
```dart
void main() {
  // TODO: refactor into an AbstractLlamaGreetingFactory?
  print('Welcome to my Llama farm!');
}
```


### Multi-line comments

A multi-line comment begins with `/*` and ends with `*/`. Everything
between `/*` and `*/` is ignored by the Dart compiler (unless the
comment is a documentation comment; see the next section). Multi-line
comments can nest.

<?code-excerpt "misc/lib/language_tour/comments.dart (multi-line-comments)"?>
```dart
void main() {
  /*
   * This is a lot of work. Consider raising chickens.

  Llama larry = Llama();
  larry.feed();
  larry.exercise();
  larry.clean();
   */
}
```


### Documentation comments

Documentation comments are multi-line or single-line comments that begin
with `///` or `/**`. Using `///` on consecutive lines has the same
effect as a multi-line doc comment.

Inside a documentation comment, the Dart compiler ignores all text
unless it is enclosed in brackets. Using brackets, you can refer to
classes, methods, fields, top-level variables, functions, and
parameters. The names in brackets are resolved in the lexical scope of
the documented program element.

Here is an example of documentation comments with references to other
classes and arguments:

<?code-excerpt "misc/lib/language_tour/comments.dart (doc-comments)"?>
```dart
/// A domesticated South American camelid (Lama glama).
///
/// Andean cultures have used llamas as meat and pack
/// animals since pre-Hispanic times.
class Llama {
  String name;

  /// Feeds your llama [Food].
  ///
  /// The typical llama eats one bale of hay per week.
  void feed(Food food) {
    // ...
  }

  /// Exercises your llama with an [activity] for
  /// [timeLimit] minutes.
  void exercise(Activity activity, int timeLimit) {
    // ...
  }
}
```

In the generated documentation, `[Food]` becomes a link to the API docs
for the Food class.

To parse Dart code and generate HTML documentation, you can use the SDK’s
[documentation generation tool.](https://github.com/dart-lang/dartdoc#dartdoc)
For an example of generated documentation, see the [Dart API
documentation.]({{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}) For advice on how to structure
your comments, see
[Guidelines for Dart Doc Comments.](/guides/language/effective-dart/documentation)


## Summary

This page summarized the commonly used features in the Dart language.
More features are being implemented, but we expect that they won’t break
existing code. For more information, see the [Dart language specification][] and
[Effective Dart](/guides/language/effective-dart).

To learn more about Dart's core libraries, see
[A Tour of the Dart Libraries](/guides/libraries/library-tour).

[AssertionError]: {{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}/dart-core/AssertionError-class.html
[`Characters`]: {{site.pub-api}}/characters/latest/characters/Characters-class.html
[characters API]: {{site.pub-api}}/characters
[characters example]: {{site.pub-pkg}}/characters#-example-tab-
[characters package]: {{site.pub-pkg}}/characters
[dart2js]: /tools/dart2js
[dart:html]: {{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}/dart-html
[dart:isolate]: {{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}/dart-isolate
[dart:math]: {{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}/dart-math
[dart]: /server/tools/dart-vm
[Dart language specification]: /guides/language/spec
[dartdevc]: /tools/dartdevc
[DON’T use const redundantly]: /guides/language/effective-dart/usage#dont-use-const-redundantly
[double]: {{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}/dart-core/double-class.html
[Error]: {{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}/dart-core/Error-class.html
[Exception]: {{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}/dart-core/Exception-class.html
[extension methods page]: /guides/language/extension-methods
[Flutter]: {{site.flutter}}
[Flutter debug mode]: {{site.flutter}}/docs/testing/debugging#debug-mode-assertions
[forEach()]: {{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}/dart-core/Iterable/forEach.html
[Function API reference]: {{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}/dart-core/Function-class.html
[Future]: {{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}/dart-async/Future-class.html
[grapheme clusters]: https://unicode.org/reports/tr29/#Grapheme_Cluster_Boundaries
[identical()]: {{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}/dart-core/identical.html
[int]: {{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}/dart-core/int-class.html
[Iterable]: {{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}/dart-core/Iterable-class.html
[js numbers]: https://stackoverflow.com/questions/2802957/number-of-bits-in-javascript-numbers/2803010#2803010
[List]: {{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}/dart-core/List-class.html
[Map]: {{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}/dart-core/Map-class.html
[meta]: {{site.pub-pkg}}/meta
[num]: {{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}/dart-core/num-class.html
[@required]: {{site.pub-api}}/meta/latest/meta/required-constant.html
[Object]: {{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}/dart-core/Object-class.html
[ObjectVsDynamic]: /guides/language/effective-dart/design#do-annotate-with-object-instead-of-dynamic-to-indicate-any-object-is-allowed
[runes]: {{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}/dart-core/Runes-class.html
[Set]: {{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}/dart-core/Set-class.html
[StackTrace]: {{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}/dart-core/StackTrace-class.html
[Stream]: {{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}/dart-async/Stream-class.html
[String]: {{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}/dart-core/String-class.html
[Symbol]: {{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}/dart-core/Symbol-class.html
[synchronous-async-start]: https://github.com/dart-lang/sdk/blob/master/docs/newsletter/20170915.md#synchronous-async-start
[Type]: {{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}/dart-core/Type-class.html
