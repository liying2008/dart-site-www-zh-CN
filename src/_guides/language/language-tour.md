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
:   类型。一些其他的 [内置类型](#内置类型)
    如 `String`, `List`, and `bool`。

`42`
:   数字字面量。 数字字面量是一种编译时常量。

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
    [The main() function](#main-函数)。

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
    例如，一个 [条件表达式](#条件表达式)
    `condition ? expr1 : expr2` 具有值 `expr1` 或 `expr2`。
    相比之下 [if-else 语句](#if-和-else) 没有值。
    一条语句通常包含一个或多个表达式，
    但是一个表达式不能只包含一条语句。

-   Dart 工具可以报告两种类型的问题： _警告_ 和 _错误_ 。
    警告仅表示您的代码可能无法工作，但并不会阻止程序运行。
    错误分为 编译期错误 和 运行期错误。编译期错误会直接导致程序无法执行，
    运行期错误会在代码执行时抛出[异常](#异常)。


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

[abstract]: #抽象类
[as]: #类型判断运算符
[assert]: #断言
[async]: #asynchrony-support
[await]: #asynchrony-support
[break]: #break-和-continue
[case]: #switch-和-case
[catch]: #捕获异常
[class]: #实例变量
[const]: #final-和-const
{% comment %}
  [TODO: Make sure that points to a place that talks about const constructors,
  as well as const literals and variables.]
{% endcomment %}
[continue]: #break-和-continue
[covariant]: /guides/language/sound-problems#the-covariant-keyword
[default]: #switch-和-case
[deferred]: #lazily-loading-a-library
[do]: #while-和-do-while
[dynamic]: #重要概念
[else]: #if-和-else
[enum]: #enumerated-types
[export]: /guides/libraries/create-library-packages
[extends]: #extending-a-class
[external]: https://stackoverflow.com/questions/24929659/what-does-external-mean-in-dart
[factory]: #factory-constructors
[false]: #booleans
[final]: #final-和-const
[finally]: #finally
[for]: #for-循环
[Function]: #函数
[get]: #getters-and-setters
[hide]: #importing-only-part-of-a-library
[if]: #if-和-else
[implements]: #隐式接口
[import]: #using-libraries
[in]: #for-循环
[interface]: https://stackoverflow.com/questions/28595501/was-the-interface-keyword-removed-from-dart
[is]: #类型判断运算符
[library]: #libraries-and-visibility
[mixin]: #adding-features-to-a-class-mixins
[new]: #使用构造器
[null]: #默认值
[on]: #捕获异常
[operator]: #overridable-operators
[part]: /guides/libraries/create-library-packages#organizing-a-library-package
[rethrow]: #捕获异常
[return]: #函数
[set]: #getters-and-setters
[show]: #importing-only-part-of-a-library
[static]: #class-variables-and-methods
[super]: #extending-a-class
[switch]: #switch-和-case
[sync]: #generators
[this]: #构造器
[throw]: #抛出异常
[true]: #booleans
[try]: #捕获异常
[typedef]: #typedefs
[var]: #变量
[void]: https://medium.com/dartlang/dart-2-legacy-of-the-void-e7afb5f44df0
{% comment %}
  TODO: Add coverage of void to the language tour.
{% endcomment %}
[with]: #adding-features-to-a-class-mixins
[while]: #while-和-do-while
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
  更多信息，请参考 [断言](#断言)。
{{site.alert.end}}

### Final 和 Const

如果您不打算更改一个变量，可以使用 `final` 或 `const` 来修饰它，
这两个关键字可以代替 `var` 或者加在一个具体的类型前。
一个 final 变量只可以被赋值一次； 一个 const 变量是一个编译时常量。
（const 变量同时也是 final 的。）顶层的 final 变量或者类的 final 变量在其第一次使用的时候被初始化。

{{site.alert.note}}
  实例变量可以是 `final` 的但不能是 `const` 的。
  final 实例变量必须在构造器主体开始之前初始化，
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

使用 `const` 修饰的变量为 **编译时常量**。
如果使用 const 修饰类中的变量，则必须加上 `static` 关键字，即 `static const`。
声明 const 变量，须将其值设置为编译期常数，例如数字或字符串字面量、const 变量或对常数进行算术运算的结果：

<?code-excerpt "misc/lib/language_tour/variables.dart (const)"?>
```dart
const bar = 1000000; // Unit of pressure (dynes/cm2)
const double atm = 1.01325 * bar; // Standard atmosphere
```

`const` 关键字不止可以用来声明常量，
还可以用来创建常量 _值_ 。
你也可以将构造器声明为 const 的，
这种类型的构造器 _创建_ 的对象是不可改变的。

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
[类型检查和强制类型转换](#类型判断运算符) (`is` and `as`)，
[collection if](#collection-operators)
以及 [展开操作符](#spread-operator) (`...` and `...?`)：

<?code-excerpt "misc/lib/language_tour/variables.dart (const-dart-25)"?>
```dart
// 从 Dart 2.5 开始，以下都是合法的编译时常量
const Object i = 3; // Where i is a const Object with an int value...
const list = [i as int]; // Use a typecast.
const map = {if (i is int) i: "int"}; // Use is and collection if.
const set = {if (list is List<int>) ...list}; // ...and a spread.
```
更多关于使用 `const` 创建常量值的信息，请参考
[Lists](#lists)、[Maps](#maps) 和 [Classes](#类)。


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

数字字面量是编译时常量。
很多算术表达式只要其操作数是常量，则表达式结果也是编译时常量。

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

字符串字面量是一个编译时常量，
只要是编译时常量都可以作为字符串字面量的插值表达式。

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
布尔类型只有两个对象 `true` 和 `false`，两者都是编译时常量。

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

如果要创建一个编译时常量的 list，只需要在 list 字面量前加上 `const` 关键字：

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
Dart 支持 set 字面量和 [Set][Set class] 类型。

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

如果想创建一个编译时常量的 set，
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
  详细信息，请参考 [构造器的使用](#使用构造器) 。
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

如果想创建一个编译时常量的 map，
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

symbol 字面量是编译时常量。


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
  例如，您不能在其中放置 [if 语句](#if-和-else)，
  但是可以使用 [条件表达式](#条件表达式)。
{{site.alert.end}}

函数可以有两种类型的参数： _必要参数_ and _可选参数_。
必要参数定义在参数列表前面，可选参数则定义在必要参数后面。
可选参数可以是 _命名参数_ 或 _位置参数_。

{{site.alert.note}}
  一些API（尤其是 [Flutter][] widget 构造器）仅使用命名参数，
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
默认值必须是编译时常量。
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
  上面代码中的 `..` 语法称为 [级联调用](#级联符号-) 。
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

### 函数作为一等对象

您可以将函数作为参数传递给另一个函数，例如：

<?code-excerpt "misc/lib/language_tour/functions.dart (function-as-param)"?>
```dart
void printElement(int element) {
  print(element);
}

var list = [1, 2, 3];

// Pass printElement as a parameter.
list.forEach(printElement);
```

您也可以将一个函数赋值给一个变量，例如：

<?code-excerpt "misc/test/language_tour/functions_test.dart (function-as-var)"?>
```dart
var loudify = (msg) => '!!! ${msg.toUpperCase()} !!!';
assert(loudify('hello') == '!!! HELLO !!!');
```

该示例中使用了匿名函数。
下一节会有更多与其相关的介绍。

### 匿名函数

大多数函数都是有名字的，比如 `main()` 或者 `printElement()` 。
您也可以创建一个没有名字的函数，称为 _匿名函数_ ，
有时候也叫 _lambda表达式_ 或 _闭包_ 。
您可以将一个匿名函数赋值给一个变量然后使用它，
比如将该变量添加到集合中或从集合中删除。

匿名函数看起来和命名函数很相似&mdash;
在括号之间可以有0个或多个参数，
参数之间用逗号分隔，参数的类型可写可不写。

然后后面紧接着的代码块就是函数体：

<code>
([[<em>类型</em>] <em>参数1</em>[, …]]) { <br>
&nbsp;&nbsp;<em>代码块</em>; <br>
}; <br>
</code>

下面的例子定义了一个匿名函数，其只有一个没有类型的参数 `item` 。
list 中的每个元素都会调用这个函数（作为参数），
打印一个包含元素索引和其值的字符串。

<?code-excerpt "misc/test/language_tour/functions_test.dart (anonymous-function)"?>
```dart
var list = ['apples', 'bananas', 'oranges'];
list.forEach((item) {
  print('${list.indexOf(item)}: $item');
});
```

点击 **Run** 执行代码。

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

如果函数只包含一条语句，您可以使用箭头语法简写。
将下面的代码粘贴到 DartPad 然后点击 **Run** 验证函数的功能是否相同。

<?code-excerpt "misc/test/language_tour/functions_test.dart (anon-func)"?>
```dart
list.forEach(
    (item) => print('${list.indexOf(item)}: $item'));
```


### 词法作用域

Dart是一种按词法确定作用域的语言，
这意味着变量的作用域是由代码的布局静态地确定的。
您可以 “跟随花括号向外” 查看变量是否在作用域内。

下面是一个嵌套函数的例子，在每个作用域级别上都有变量：

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

注意 `nestedFunction()` 函数可以访问包括顶层变量在内的所有级别的变量。


### 词法闭包

*闭包* 是一个函数对象，它可以访问词法作用域内的变量，
即使该函数在其原始作用域之外使用时也是如此。

函数可以封闭定义到它作用域内的变量。
在下面的示例中，函数 `makeAdder()` 捕获了变量 `addBy` 。
无论函数在什么时候返回，它都可以使用捕获的 `addBy` 变量。

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


### 测试函数是否相等

下面是测试顶层函数、静态方法和实例方法是否相等的示例：

<?code-excerpt "misc/lib/language_tour/function_equality.dart"?>
```dart
void foo() {} // 顶层函数

class A {
  static void bar() {} // 静态方法
  void baz() {} // 实例方法
}

void main() {
  var x;

  // 比较顶层函数是否相等
  x = foo;
  assert(foo == x);

  // 比较静态方法是否相等
  x = A.bar;
  assert(A.bar == x);

  // 比较实例方法是否相等
  var v = A(); // Instance #1 of A
  var w = A(); // Instance #2 of A
  var y = w;
  x = w.baz;

  // 这两个闭包引用了相同的实例 (#2)，
  // 因此它们相等
  assert(y.baz == x);

  // 这两个闭包引用了不同的实例，
  // 因此它们不相等
  assert(v.baz != w.baz);
}
```


### 返回值

所有函数都有返回值。
如果函数没有指定返回值，那么 `return null;` 语句会隐式默认加到函数体中。

<?code-excerpt "misc/test/language_tour/functions_test.dart (implicit-return-null)"?>
```dart
foo() {}

assert(foo() == null);
```


## 运算符

下面表格中是 Dart 中定义的运算符。
您可以重写表格中大多数运算符，如
[重写运算符](#overridable-operators) 所述。

|--------------------------+------------------------------------------------|
|描述               | 运算符                                       |
|--------------------------|------------------------------------------------|
| 一元后缀            | <code><em>expr</em>++</code>    <code><em>expr</em>--</code>    `()`    `[]`    `.`    `?.` |
| 一元前缀           | <code>-<em>expr</em></code>    <code>!<em>expr</em></code>    <code>~<em>expr</em></code>    <code>++<em>expr</em></code>    <code>--<em>expr</em></code>      <code>await <em>expr</em></code>    |
| 乘除           | `*`    `/`    `%`    `~/`                      |
| 加减                 | `+`    `-`                                     |
| 移位                    | `<<`    `>>`    `>>>`                          |
| 按位与             | `&`                                            |
| 按位异或              | `^`                                            |
| 按位或               | `|`                                            |
| 关系&nbsp;和&nbsp;类型&nbsp;判断 | `>=`    `>`    `<=`    `<`    `as`    `is`    `is!` |
| 相等判断                 | `==`    `!=`                                   |
| 逻辑与              | `&&`                                           |
| 逻辑或               | `||`                                           |
| 空判断 (if null)                  | `??`                                           |
| 条件表达式              | <code><em>expr1</em> ? <em>expr2</em> : <em>expr3</em></code> |
| 级联                  | `..`                                           |
| 赋值               | `=`    `*=`    `/=`    `+=`    `-=`    `&=`    `^=`    <em>etc.</em> |
{:.table .table-striped}

{{site.alert.warning}}
  运算符优先级是对 Dart 解析器行为的近似。
  更准确的描述，请查阅
  [Dart 语言规范][Dart language specification] 中的语法。
{{site.alert.end}}

一旦您使用了运算符，就创建了表达式。
下面是一些运算符表达式的示例：

<?code-excerpt "misc/test/language_tour/operators_test.dart (expressions)" replace="/,//g"?>
```dart
a++
a + b
a = b
a == b
c ? a : b
a is T
```

在 [运算符表](#运算符) 中，
运算符的优先级按先后排列，即第一行优先级最高，最后一行优先级最低。
例如，`%` 运算符的优先级高于 `==` ，而 `==` 优先级高于 `&&` 。
这就意味着下面两行代码以相同的方式执行：

<?code-excerpt "misc/test/language_tour/operators_test.dart (precedence)"?>
```dart
// Parentheses improve readability.
if ((n % i == 0) && (d % i == 0)) ...

// Harder to read, but equivalent.
if (n % i == 0 && d % i == 0) ...
```

{{site.alert.warning}}
  对于有两个操作数的运算符来讲，是左边的操作数决定了运算符的功能。
  例如，有一个 Vector 对象和一个 Point 对象，
  `aVector + aPoint` 使用的是 Vector 中定义的 + 。
{{site.alert.end}}


### 算术运算符

Dart 支持常用的算数运算符，如下表所示：

|-----------------------------+-------------------------------------------|
| 运算符                    | 含义                                   |
|-----------------------------+-------------------------------------------|
| `+`                         | 加
| `–`                         | 减
| <code>-<em>表达式</em></code> | 取反
| `*`                         | 乘
| `/`                         | 除
| `~/`                        | 除，返回整数结果
| `%`                         | 取余（模）
{:.table .table-striped}

例子：

<?code-excerpt "misc/test/language_tour/operators_test.dart (arithmetic)"?>
```dart
assert(2 + 3 == 5);
assert(2 - 3 == -1);
assert(2 * 3 == 6);
assert(5 / 2 == 2.5); // 结果是 double
assert(5 ~/ 2 == 2); // 结果是 int
assert(5 % 2 == 1); // 取余

assert('5/2 = ${5 ~/ 2} r ${5 % 2}' == '5/2 = 2 r 1');
```

Dart 还支持前缀和后缀自增自减运算符。

|-----------------------------+-------------------------------------------|
| 运算符                    | 含义                                   |
|-----------------------------+-------------------------------------------|
| <code>++<em>var</em></code> | <code><em>var</em> = <em>var</em> + 1</code> (表达式值为 <code><em>var</em> + 1</code>)
| <code><em>var</em>++</code> | <code><em>var</em> = <em>var</em> + 1</code> (表达式值为 <code><em>var</em></code>)
| <code>--<em>var</em></code> | <code><em>var</em> = <em>var</em> – 1</code> (表达式值为 <code><em>var</em> – 1</code>)
| <code><em>var</em>--</code> | <code><em>var</em> = <em>var</em> – 1</code> (表达式值为 <code><em>var</em></code>)
{:.table .table-striped}

例子：

<?code-excerpt "misc/test/language_tour/operators_test.dart (increment-decrement)"?>
```dart
var a, b;

a = 0;
b = ++a; // 给 b 赋值前将 a 加 1 。
assert(a == b); // 1 == 1

a = 0;
b = a++; // 给 b 赋值后将 a 加 1 。
assert(a != b); // 1 != 0

a = 0;
b = --a; // 给 b 赋值前将 a 减 1 。
assert(a == b); // -1 == -1

a = 0;
b = a--; // 给 b 赋值后将 a 减 1 。
assert(a != b); // -1 != 0
```


### 关系运算符

下面表格列出了关系运算符及含义。

|-----------+-------------------------------------------|
| 运算符  | 含义                                   |
|-----------+-------------------------------------------|
| `==`      |       相等
| `!=`      |       不等
| `>`       |       大于
| `<`       |       小于
| `>=`      |       大于等于
| `<=`      |       小于等于
{:.table .table-striped}

要判断两个对象 x 和 y 是否相等（即 x 和 y 表示同一事物），使用 `==` 运算符即可。
（在极少数情况下，需要使用 [identical()][] 函数来判断两个对象是否是同一个对象（即完全相同）。）
`==` 运算符的工作方式如下：

1.  如果 *x* 或 *y* 为 null，如果两者都为 null 则返回 true ，否则返回 false 。

2.  调用
    <code><em>x</em>.==(<em>y</em>)</code> 将会返回一个值。
    （运算符，比如 `==` 其实是第一个操作数的一个方法，您可以重写很多运算符，包括 `==`，
    详情请参考 [重写运算符](#overridable-operators)。）

下面是使用关系运算符的例子：

<?code-excerpt "misc/test/language_tour/operators_test.dart (relational)"?>
```dart
assert(2 == 2);
assert(2 != 3);
assert(3 > 2);
assert(2 < 3);
assert(3 >= 3);
assert(2 <= 3);
```


### 类型判断运算符

`as`、 `is` 和 `is!` 是在运行时判断对象类型的运算符。

|-----------+-------------------------------------------|
| 运算符  | 含义                                   |
|-----------+-------------------------------------------|
| `as`      | 类型强制转换 （也用于指定 [库前缀](#specifying-a-library-prefix)）
| `is`      | 如果对象是指定类型则返回 true
| `is!`     | 如果对象是指定类型则返回 false
{:.table .table-striped}

如果 `obj` 实现了 `T` 的接口，则 `obj is T` 返回 true。
例如，`obj is Object` 总是返回 true（因为任何类都是 Object 的子类）。

仅当您确定一个对象是某一类型时您才可以使用 `as` 去强转该对象为这一类型。例如：

<?code-excerpt "misc/lib/language_tour/classes/employee.dart (emp as Person)"?>
```dart
(emp as Person).firstName = 'Bob';
```

如果您不确定这个对象是不是 `T` 类型，请在使用前先用 `is T` 检查一下。

<?code-excerpt "misc/lib/language_tour/classes/employee.dart (emp is Person)"?>
```dart
if (emp is Person) {
  // Type check
  emp.firstName = 'Bob';
}
```

{{site.alert.note}}
  上面两种方式是有区别的。如果 `emp` 是 null 或者不是 `Person` 类型，
  第一个例子将会抛出一个异常；而第二个例子将什么都不会做。
{{site.alert.end}}

### 赋值运算符

您可以使用 `=` 来赋值。
同时您也可以使用 `??=` 来为值为 null 的变量赋值。

<?code-excerpt "misc/test/language_tour/operators_test.dart (assignment)"?>
```dart
// 给 a 赋值
a = value;
// 只有当 b 为 null 时，才会被赋值
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

复合赋值运算符，例如 `+=`，
将算数运算符和赋值运算符结合了起来。

| `=`  | `–=` | `/=`  | `%=`  | `>>=` | `^=`
| `+=` | `*=` | `~/=` | `<<=` | `&=`  | `|=`
{:.table}

复合赋值运算符的工作原理如下：

|-----------+----------------------+-----------------------|
|           | 复合赋值  | 等效表达式 |
|-----------+----------------------+-----------------------|
|**对于一个运算符 <em>op</em>:** | <code>a <em>op</em>= b</code> | <code>a = a <em>op</em> b</code>
|**例子：**                     |`a += b`                       | `a = a + b`
{:.table}

下面的例子使用了赋值和复合赋值运算符：

<?code-excerpt "misc/test/language_tour/operators_test.dart (op-assign)"?>
```dart
var a = 2; // Assign using =
a *= 3; // Assign and multiply: a = a * 3
assert(a == 6);
```


### 逻辑运算符

您可以使用逻辑运算符取反或组合布尔表达式。

|-----------------------------+-------------------------------------------|
| 运算符                    | 含义                                   |
|-----------------------------+-------------------------------------------|
| <code>!<em>表达式</em></code> | 对表达式结果取反（即将 true 变为 false，false 变为 true）
| `||`                        | 逻辑或
| `&&`                        | 逻辑与
{:.table .table-striped}

下面是一个使用逻辑运算符的例子：

<?code-excerpt "misc/lib/language_tour/operators.dart (op-logical)"?>
```dart
if (!done && (col == 0 || col == 3)) {
  // ...Do something...
}
```


### 按位和移位运算符

您可以在 Dart 中操纵数字的各个位。
通常，您需要将这些按位和移位运算符与整数一起使用。

|-----------------------------+-------------------------------------------|
| 运算符                    | 含义                                   |
|-----------------------------+-------------------------------------------|
| `&`                         | 按位与
| `|`                         | 按位或
| `^`                         | 按位异或
| <code>~<em>表达式</em></code> | 按位取反（即将 0 变为 1，1 变为 0）
| `<<`                        | 左移
| `>>`                        | 右移
{:.table .table-striped}

下面是一个使用按位和移位运算符的例子：

<?code-excerpt "misc/test/language_tour/operators_test.dart (op-bitwise)"?>
```dart
final value = 0x22;
final bitmask = 0x0f;

assert((value & bitmask) == 0x02); // 按位与（AND）
assert((value & ~bitmask) == 0x20); // 按位取反后按位与（AND NOT）
assert((value | bitmask) == 0x2f); // 按位或（OR）
assert((value ^ bitmask) == 0x2d); // 按位异或（XOR）
assert((value << 4) == 0x220); // 左移（Shift left）
assert((value >> 4) == 0x02); // 右移（Shift right）
```


### 条件表达式

Dart 有两个特殊的运算符可以用来替代 [if-else](#if-和-else) 语句：

<code><em>条件</em> ? <em>表达式1</em> : <em>表达式2</em></code>
: 如果 _条件_ 为 true，执行 _表达式1_ 并返回其结果，否则，执行 _表达式2_ 并返回其结果。

<code><em>表达式1</em> ?? <em>表达式2</em></code>
: 如果 _表达式1_ 非 null，则返回其值；否则，执行并返回 _表达式2_ 的值。

当您需要根据布尔表达式的结果赋值时，可以考虑使用 `?:` 。

<?code-excerpt "misc/lib/language_tour/operators.dart (if-then-else-operator)"?>
```dart
var visibility = isPublic ? 'public' : 'private';
```

如果赋值是根据表达式是否为 null 则考虑使用 `??` 。

<?code-excerpt "misc/test/language_tour/operators_test.dart (if-null)"?>
```dart
String playerName(String name) => name ?? 'Guest';
```

上述示例还可以写成至少下面两种不同的形式，只是不够简洁：

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
### 级联符号 (..)

级联 (`..`) 允许您对同一对象执行一系列操作。
除了函数调用，您还可以访问同一对象上的字段。
这通常可以节省创建临时变量的步骤，并有助于您编写更多流畅的代码。

例如下面的代码：

<?code-excerpt "misc/test/language_tour/browser_test.dart (cascade-operator)"?>
```dart
querySelector('#confirm') // Get an object.
  ..text = 'Confirm' // Use its members.
  ..classes.add('important')
  ..onClick.listen((e) => window.alert('Confirmed!'));
```

第一个方法 `querySelector()` 返回了一个 selector 对象。
后面的级联符号都是调用这个 selector 对象的成员
并忽略每个操作的返回值。

上面的代码等效于：

<?code-excerpt "misc/test/language_tour/browser_test.dart (cascade-operator-example-expanded)"?>
```dart
var button = querySelector('#confirm');
button.text = 'Confirm';
button.classes.add('important');
button.onClick.listen((e) => window.alert('Confirmed!'));
```

您也可以嵌套级联，例如：

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

在返回对象的函数中要谨慎使用级联。
例如，下面的代码是错误的：

<?code-excerpt "misc/lib/language_tour/operators.dart (cannot-cascade-on-void)" plaster="none"?>
```dart
var sb = StringBuffer();
sb.write('foo')
  ..write('bar'); // Error: method 'write' isn't defined for 'void'.
```

上述代码中 `sb.write()` 返回 void ，
您无法在 `void` 上构造一个级联。

{{site.alert.note}}
  严格来说，`..` 级联符号并不是一个运算符。
  它只是 Dart 语法的一部分。
{{site.alert.end}}

### 其他运算符

您已经在其他示例中看到过下面大多数运算符了：

|----------+-------------------------------------------|
| 运算符 | 名称                 |          含义   |
|-----------+------------------------------------------|
| `()`     | 函数应用 | 表示函数调用
| `[]`     | List 访问         | 引用列表中指定索引处的值
| `.`      | 成员访问       | 引用表达式的属性；示例：`foo.bar` 从表达式 `foo` 中选择属性 `bar`
| `?.`     | 有条件的成员访问 | 类似于 `.` ，但是最左边的操作数可以为 null ；示例：`foo?.bar` 表示从表达式 `foo` 中选择属性 `bar`，除非 `foo` 为 null（在这种情况下 `foo?.bar` 的值为 null）
{:.table .table-striped}

更多有关 `.`、 `?.` 和 `..` 运算符的信息，请参考
[类](#类)。


## 流程控制语句

你可以使用下面的语句来控制 Dart 代码的执行流程：

-   `if` 和 `else`
-   `for` 循环
-   `while` 和 `do`-`while` 循环
-   `break` 和 `continue`
-   `switch` 和 `case`
-   `assert`

使用 `try-catch` 和 `throw` 也能影响控制流，
可以查看 [异常](#异常) 获取更多解释。


### If 和 Else

Dart 支持 `if-else` 语句，其中 `else` 语句是可选的，例如下面的例子。
您也可以参考 [条件表达式](#条件表达式) 。

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

与 JavaScript 不同的是，Dart 中的条件必须是一个布尔值，不能是其它类型。
详情请查阅 [Booleans](#booleans)。


### For 循环

您可以使用标准的 `for` 循环进行迭代。例如：

<?code-excerpt "misc/test/language_tour/control_flow_test.dart (for)"?>
```dart
var message = StringBuffer('Dart is fun');
for (var i = 0; i < 5; i++) {
  message.write('!');
}
```

在 Dart 语言中，`for` 循环中的闭包会自动捕获循环的 _索引值_ 
以避免 JavaScript 中一些常见的陷阱。例如有如下代码：

<?code-excerpt "misc/test/language_tour/control_flow_test.dart (for-and-closures)"?>
```dart
var callbacks = [];
for (var i = 0; i < 2; i++) {
  callbacks.add(() => print(i));
}
callbacks.forEach((c) => c());
```

正如所预期的一样，上述代码将会输出 `0` 和 `1` 。
但是在 JavaScript 中，同样的代码则会输出 `2` 和 `2` 。

如果要遍历的对象是一个 Iterable 对象，
那么可以使用 [forEach()][] 方法。
如果您不需要知道当前迭代计数器，那么使用 `forEach()` 是一个不错的选择：

<?code-excerpt "misc/lib/language_tour/control_flow.dart (forEach)"?>
```dart
candidates.forEach((candidate) => candidate.interview());
```

像 List 和 Set 等可迭代的类也支持 `for-in` 形式的
[迭代](/guides/libraries/library-tour#iteration)：

<?code-excerpt "misc/test/language_tour/control_flow_test.dart (collection)"?>
```dart
var collection = [0, 1, 2];
for (var x in collection) {
  print(x); // 0 1 2
}
```


### While 和 Do-While

`while` 循环会在循环之前判断条件：

<?code-excerpt "misc/lib/language_tour/control_flow.dart (while)"?>
```dart
while (!isDone()) {
  doSomething();
}
```

`do`-`while` 循环会先执行一遍循环，*再* 判断条件：

<?code-excerpt "misc/lib/language_tour/control_flow.dart (do-while)"?>
```dart
do {
  printLine();
} while (!atEndOfPage());
```


### Break 和 Continue

使用 `break` 可以终止循环：

<?code-excerpt "misc/lib/language_tour/control_flow.dart (while-break)"?>
```dart
while (true) {
  if (shutDownRequested()) break;
  processIncomingRequests();
}
```

使用 `continue` 可以跳过本次循环，直接进入下一次循环：

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

如果您使用的是像 list 或 set 这样的 [Iterable][] 对象的话，
上面的例子可以写成下面这种形式：

<?code-excerpt "misc/lib/language_tour/control_flow.dart (where)"?>
```dart
candidates
    .where((c) => c.yearsExperience >= 5)
    .forEach((c) => c.interview());
```


### Switch 和 Case

Dart 中的 switch 语句使用 `==` 来比较整数、字符串或编译时常量。
被比较的对象必须是同一个类的实例（还不能是其子类型），
并且这个类没有重写 `==` 运算符。 
[枚举类型](#enumerated-types) 非常适合在 `switch` 语句中使用。

{{site.alert.note}}
  Dart 中的 switch 语句仅在有限的情况下使用，
  例如用在解释器或扫描器中。
{{site.alert.end}}

通常，每一个非空的 `case` 子句都以 `break` 语句结尾。
`continue` 、`throw` 或 `return` 语句也可以结束非空的 `case` 子句。

当没有 `case` 子句匹配时，可以使用 `default` 子句来匹配这种情况：

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

下面的例子省略了 `case` 子句中的 `break` 语句，
所以会产生错误：

<?code-excerpt "misc/lib/language_tour/control_flow.dart (switch-break-omitted)" plaster="none"?>
```dart
var command = 'OPEN';
switch (command) {
  case 'OPEN':
    executeOpen();
    // 错误: 缺失 break

  case 'CLOSED':
    executeClosed();
    break;
}
```

但是，Dart 支持空的 `case` 子句，
允许其以 fall-through 的形式执行：

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

如果您确实需要 fall-through，可以使用 `continue` 语句和 label：

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

`case` 子句可以有局部变量，
这些局部变量仅在该子句范围内可见。


### 断言

在开发过程中，可以使用断言语句
— <code>assert(<em>条件</em>, <em>可选信息</em>)</code>; —
来中断当条件为 false 时程序的执行。
您可以在本文中找到大量使用 assert 语句的例子。下面是一些示例：

<?code-excerpt "misc/test/language_tour/control_flow_test.dart (assert)"?>
```dart
// 确保变量不为 null
assert(text != null);

// 确保值小于 100
assert(number < 100);

// 确保字符串以 https 开头
assert(urlString.startsWith('https'));
```

如果要给断言附加一个信息，
请添加字符串作为 `assert` 的第二个参数。

<?code-excerpt "misc/test/language_tour/control_flow_test.dart (assert-with-message)"?>
```dart
assert(urlString.startsWith('https'),
    'URL ($urlString) should start with "https".');
```

`assert` 的第一个参数可以是值为布尔值的任何表达式。
如果表达式的值为 true，则断言成功，程序继续执行。
如果表达式的值为 false，则断言失败，程序抛出 [AssertionError][] 异常。

断言什么时候起作用？
这取决于您使用的工具和框架：

* Flutter 在 [调试模式][Flutter debug mode] 下启用断言。
* 一些仅用于开发的工具，例如 [dartdevc][]，默认启用断言。
* 其他一些工具，例如 [dart][] 和 [dart2js][dart2js]，通过添加命令行参数 `--enable-asserts` 启用断言。

在生产环境代码中，断言将被忽略，
传入 `assert` 中的条件表达式也不会执行。


## 异常

Dart 代码可以抛出和捕获异常。
异常是表示发生了意外的错误。
如果异常没有被捕获，抛出异常的 [隔离区](#isolates) 将被挂起，
隔离区及其程序将被终止。

与 Java 不同的是，Dart 的所有异常都是非必检异常。
方法不会声明它可能抛出哪些异常，
您也不需要捕获所有异常。

Dart 提供了 [Exception][] 和 [Error][] 类型，以及许多预定义的子类型。
当然，您也可以定义自己的异常。
但是，Dart 程序可以将任何非 null 对象（不仅仅是 Exception 和 Error 对象）作为异常抛出。

### 抛出异常

下面是一个抛出或者 *引发* 异常的例子：

<?code-excerpt "misc/lib/language_tour/exceptions.dart (throw-FormatException)"?>
```dart
throw FormatException('Expected at least 1 section');
```

您也可以抛出任意对象：

<?code-excerpt "misc/lib/language_tour/exceptions.dart (out-of-llamas)"?>
```dart
throw 'Out of llamas!';
```

{{site.alert.note}}
  达到生产质量要求的代码（优秀的代码）通常会抛出 [Error][] 或
  [Exception][] 类型的异常。
{{site.alert.end}}

因为抛出异常是一个表达式，
所以可以在 =\> 语句中抛出异常，
也可以在其他使用表达式的地方抛出异常：

<?code-excerpt "misc/lib/language_tour/exceptions.dart (throw-is-an-expression)"?>
```dart
void distanceTo(Point other) => throw UnimplementedError();
```


### 捕获异常

捕获异常可以避免异常继续传递（除非重新抛出异常）。
捕获异常使您有机会处理它：

<?code-excerpt "misc/lib/language_tour/exceptions.dart (try)"?>
```dart
try {
  breedMoreLlamas();
} on OutOfLlamasException {
  buyMoreLlamas();
}
```

要处理可以抛出多种异常类型的代码，
可以指定多个 catch 子句。
第一个匹配上抛出的异常的类型的 catch 子句负责处理这个类型的异常。
如果 catch 子句没有指定异常类型，那么它可以处理任何类型的异常：

<?code-excerpt "misc/lib/language_tour/exceptions.dart (try-catch)"?>
```dart
try {
  breedMoreLlamas();
} on OutOfLlamasException {
  // 捕获指定类型的异常
  buyMoreLlamas();
} on Exception catch (e) {
  // 捕获 Exception 其他类型的异常
  print('Unknown exception: $e');
} catch (e) {
  // 不指定类型，任何类型的异常都可以捕获
  print('Something really unknown: $e');
}
```

正如上述代码所示，您可以使用 `on` 或 `catch` 来捕获异常，
使用 `on` 来指定异常类型，使用 `catch` 来获取异常对象，
两者可同时使用。

您可以为 `catch()` 方法指定一个或两个参数。
第一个参数为抛出的异常对象，
第二个参数为栈跟踪信息（一个 [StackTrace][] 对象）。

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

如果想将捕获的异常再次抛出，
请使用 `rethrow` 关键字。

<?code-excerpt "misc/test/language_tour/exceptions_test.dart (rethrow)" replace="/rethrow;/[!$&!]/g"?>
{% prettify dart tag=pre+code %}
void misbehave() {
  try {
    dynamic foo = true;
    print(foo++); // 运行时错误
  } catch (e) {
    print('misbehave() partially handled ${e.runtimeType}.');
    [!rethrow;!] // 允许调用者看到异常
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

为了确保不管是否有异常抛出都会执行某些代码，可以将这些代码放在 `finally` 子句中。
如果没有 `catch` 子句捕获异常，异常会在执行完 `finally` 子句后抛出：

<?code-excerpt "misc/lib/language_tour/exceptions.dart (finally)"?>
```dart
try {
  breedMoreLlamas();
} finally {
  // Always clean up, even if an exception is thrown.
  cleanLlamaStalls();
}
```

如果有 `catch` 子句捕获了异常，`finally` 子句将在捕获异常的 `catch` 子句之后执行：

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

阅读库概览中的
[异常](/guides/libraries/library-tour#exceptions)
章节获取更多信息。

## 类

Dart 是一种面向对象的语言，具有类和基于 mixin 的继承。
每个对象都是一个类的实例，所有的类都是从 [Object][Object] 类派生出来的。
*基于 mixin 的继承* 意味着，尽管每个类（Object 除外）只有一个父类，
但一个类主体可以在多个类层次中重用。
[扩展方法](#extension-methods) 是一种向类添加功能而不改变类或创建子类的方法。


### 使用类成员

对象的 *成员* 由函数和数据（分别是 *方法* 和 *实例变量*）组成。
方法的 *调用* 需要通过对象来完成：该方法可以访问该对象的函数和数据。

使用点 (`.`) 来访问实例变量或方法：

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

使用 `?.` 代替 `.` 可以避免因为左边表达式为 null 而导致的异常：

{% comment %}
{{site.dartpad}}/0cb25997742ed5382e4a
https://gist.github.com/0cb25997742ed5382e4a
{% endcomment %}

<?code-excerpt "misc/test/language_tour/classes_test.dart (safe-member-access)"?>
```dart
// 如果 p 非空则将其属性 y 的值设为 4
p?.y = 4;
```


### 使用构造器

您可以使用 *构造器* 来创建一个对象。
构造器的名字可以是 <code><em>类名</em></code>，也可以是 <code><em>类名</em>.<em>标识符</em></code>。
例如，下面的代码使用 `Point()` 和 `Point.fromJson()` 两个构造器来创建 `Point` 对象：

<?code-excerpt "misc/test/language_tour/classes_test.dart (object-creation)" replace="/ as .*?;/;/g"?>
```dart
var p1 = Point(2, 2);
var p2 = Point.fromJson({'x': 1, 'y': 2});
```

下面的代码具有相同的效果，
但是在构造器名称前使用了可选的关键字 `new`：

<?code-excerpt "misc/test/language_tour/classes_test.dart (object-creation-new)" replace="/ as .*?;/;/g"?>
```dart
var p1 = new Point(2, 2);
var p2 = new Point.fromJson({'x': 1, 'y': 2});
```

{{site.alert.version-note}}
  从 Dart 2 开始，`new` 关键字是可选的。
{{site.alert.end}}

一些类提供了 [常量构造器](#constant-constructors)。
若要使用常量构造器创建编译时常量，
请将 `const` 关键字放在构造器名称之前：

<?code-excerpt "misc/test/language_tour/classes_test.dart (const)"?>
```dart
var p = const ImmutablePoint(2, 2);
```

两个使用相同构造器相同参数值构造的编译时常量是同一个对象：

<?code-excerpt "misc/test/language_tour/classes_test.dart (identical)"?>
```dart
var a = const ImmutablePoint(1, 1);
var b = const ImmutablePoint(1, 1);

assert(identical(a, b)); // 它们是同一个实例
```

在 _常量上下文_ 中，您可以省略构造器或字面量前面的 `const` 关键字。
例如下面这段代码，创建了一个常量 map：

<?code-excerpt "misc/test/language_tour/classes_test.dart (const-context-withconst)" replace="/pointAndLine1/pointAndLine/g"?>
```dart
// 这里有太多的 const 关键字
const pointAndLine = const {
  'point': const [const ImmutablePoint(0, 0)],
  'line': const [const ImmutablePoint(1, 10), const ImmutablePoint(-2, 11)],
};
```

根据上下文，您可以只保留第一个 `const` 关键字，其余的全部省略：

<?code-excerpt "misc/test/language_tour/classes_test.dart (const-context-noconst)" replace="/pointAndLine2/pointAndLine/g"?>
```dart
// 只有一个 const，它建立了常量上下文
const pointAndLine = {
  'point': [ImmutablePoint(0, 0)],
  'line': [ImmutablePoint(1, 10), ImmutablePoint(-2, 11)],
};
```

如果常量构造器位于常量上下文之外，
并且在不使用 `const` 的情况下被调用，那么它将创建一个 **非常量对象** ：

<?code-excerpt "misc/test/language_tour/classes_test.dart (nonconst-const-constructor)"?>
```dart
var a = const ImmutablePoint(1, 1); // 创建一个常量
var b = ImmutablePoint(1, 1); // 不会创建一个常量

assert(!identical(a, b)); // 它们不是同一个实例
```

{{site.alert.version-note}}
  只有从 Dart 2 开始，才可以根据常量上下文判断省略 `const` 关键字。
{{site.alert.end}}


### 获取对象的类型

要在运行时获取对象的类型，
可以使用对象的 `runtimeType` 属性，
该属性返回一个 [Type][] 对象。

<?code-excerpt "misc/test/language_tour/classes_test.dart (runtimeType)"?>
```dart
print('The type of a is ${a.runtimeType}');
```

至此，您已经了解了如何 _使用_ 类。
本节的剩余部分将展示如何 _实现_ 类。


### 实例变量

声明实例变量的方法如下：

<?code-excerpt "misc/lib/language_tour/classes/point_with_main.dart (class)"?>
```dart
class Point {
  num x; // 声明实例变量 x，初始值为 null
  num y; // 声明实例变量 y，初始值为 null
  num z = 0; // 声明实例变量 z，初始值为 0
}
```

所有未初始化的实例变量的值都为 `null` 。

所有实例变量都会生成一个隐式的 *getter* 方法。
非 final 实例变量还会生成一个隐式的 *setter* 方法。
有关详细信息，请参见 [Getters 和 Setters](#getters-and-setters)。

<?code-excerpt "misc/lib/language_tour/classes/point_with_main.dart (class+main)" replace="/(num .*?;).*/$1/g" plaster="none"?>
```dart
class Point {
  num x;
  num y;
}

void main() {
  var point = Point();
  point.x = 4; // 使用 x 的 setter 方法
  assert(point.x == 4); // 使用 x 的 getter 方法
  assert(point.y == null); // 默认值为 null
}
```

如果您在声明一个实例变量的时候就将其初始化（而不是在构造器或其它方法中），
那么该实例变量的值就会在对象实例创建的时候被设置，
该过程会在构造器以及它的初始化列表执行前执行。


### 构造器

通过创建与其类同名的函数来声明构造器
（对于 [命名构造器](#named-constructors) 还可以添加额外的标识符）。
最常见的构造器形式是生成式构造器，它创建一个类的新实例：

<?code-excerpt "misc/lib/language_tour/classes/point_alt.dart (constructor-long-way)" plaster="none"?>
```dart
class Point {
  num x, y;

  Point(num x, num y) {
    // 还会有更好的方式来实现此逻辑，敬请期待。
    this.x = x;
    this.y = y;
  }
}
```

使用 `this` 关键字引用当前实例。

{{site.alert.note}}
  当且仅当命名冲突时使用 `this` 关键字才有意义。否则 Dart 会忽略 `this` 关键字。
{{site.alert.end}}

将构造器参数分配给实例变量是一个非常常见的操作，
所以 Dart 提供了一个语法糖来简化它：

<?code-excerpt "misc/lib/language_tour/classes/point.dart (constructor-initializer)" plaster="none"?>
```dart
class Point {
  num x, y;

  // 设置 x 和 y 的语法糖
  // 在构造器函数体执行前执行
  Point(this.x, this.y);
}
```

#### 默认构造器

如果您没有声明构造器，Dart 会提供一个默认构造器。
默认构造器没有参数，并且会调用父类的无参构造器。

#### 构造器不能被继承

子类不会继承父类的构造器。
如果子类没有声明构造器，那么只会有一个默认无参的构造器。

#### 命名构造器

可以为一个类声明多个命名构造器来表达更明确的意图：

<?code-excerpt "misc/lib/language_tour/classes/point.dart (named-constructor)" replace="/Point\.\S*/[!$&!]/g" plaster="none"?>
{% prettify dart tag=pre+code %}
class Point {
  num x, y;

  Point(this.x, this.y);

  // 命名构造器
  [!Point.origin()!] {
    x = 0;
    y = 0;
  }
}
{% endprettify %}

请记住构造器是不能被继承的，
这将意味着子类不能继承父类的命名构造器，
如果您想在子类中提供一个与父类命名构造器名字一样的构造器，
则必须在子类中显式地声明。

#### 调用父类非默认构造器

默认情况下，子类的构造器会调用父类的匿名无参的构造器，
并且该调用会发生在子类构造器的函数体代码执行前，
如果子类构造器还有一个 [初始化列表](#initializer-list)，
那么该初始化列表会在调用父类的构造器之前被执行，
总的来说，这三者的调用顺序如下：

1. 初始化列表
1. 父类的无参构造器
1. 当前类的无参构造器

如果父类没有匿名无参数构造器，
那么子类必须手动调用父类的其中一个构造器，
可以在冒号 (`:`) 之后，构造器函数体之前（如果有的话）指定要调用的父类的构造器。

下面的例子中，Employee 类调用了它的父类 Person 的命名构造器。
点击 **Run** 执行代码。

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

因为参数会在子类构造器被执行前传递给父类构造器，
因此该参数也可以是一个表达式，例如一个函数：

<?code-excerpt "misc/lib/language_tour/classes/employee.dart (method-then-constructor)"?>
```dart
class Employee extends Person {
  Employee() : super.fromJson(defaultData);
  // ···
}
```

{{site.alert.warning}}
  传递给父类构造器的参数不能使用 `this` 关键字。
  因为在参数传递这一步骤，子类构造器尚未执行，子类的实例对象也就还未初始化，
  因此所有的实例成员都不能被访问，但是类成员可以。
{{site.alert.end}}

#### 初始化列表

除了调用父类构造器外，
您还可以在构造器函数体运行之前初始化实例变量。
每个初始化器之间用逗号分隔。

<?code-excerpt "misc/lib/language_tour/classes/point_alt.dart (initializer-list)"?>
```dart
// 初始化列表是在构造器函数体执行之前
// 设置实例变量
Point.fromJson(Map<String, num> json)
    : x = json['x'],
      y = json['y'] {
  print('In Point.fromJson(): ($x, $y)');
}
```

{{site.alert.warning}}
  初始化列表 表达式右侧的语句不能使用 `this` 关键字。
{{site.alert.end}}

在开发期间，您可以在初始化列表中使用 `assert` 来验证输入数据。

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

初始化列表用来设置 final 字段是非常好用的，
下面的例子使用初始化列表初始化了三个 final 字段。
点击 **Run** 来执行代码。

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


#### 重定向构造器

有时候一个构造器的唯一目的是重定向到同一个类中的另一个构造器，
重定向构造器没有函数体，
只需在函数签名后使用冒号 (:) 指定需要重定向到的构造器即可。

<?code-excerpt "misc/lib/language_tour/classes/point_redirecting.dart"?>
```dart
class Point {
  num x, y;

  // 该类的主构造器
  Point(this.x, this.y);

  // 委托给主构造器
  Point.alongXAxis(num x) : this(x, 0);
}
```

#### 常量构造器

如果您的类生成的对象都是不会变的，
那么可以在生成这些对象时就将其变为编译时常量。
您可以在类的构造器前加上 `const` 关键字并确保所有实例变量均为 `final` 来实现该功能。

<?code-excerpt "misc/lib/language_tour/classes/immutable_point.dart"?>
```dart
class ImmutablePoint {
  static final ImmutablePoint origin =
      const ImmutablePoint(0, 0);

  final num x, y;

  const ImmutablePoint(this.x, this.y);
}
```

常量构造器创建的实例并不总是常量，
具体可以参考 [使用构造器](#使用构造器) 章节。


#### 工厂构造器

使用 `factory` 关键字标识类的构造器为工厂构造器，
这将意味着使用该构造器构造类的实例时并非总是返回新的实例对象。
例如，工厂构造器可能会从缓存中返回一个实例，或者返回一个子类型的实例。

以下示例演示了一个从缓存中返回对象的工厂构造器：

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
  在工厂构造器中无法访问 `this`。
{{site.alert.end}}

工厂构造器的调用方式与其他构造器一样：

<?code-excerpt "misc/lib/language_tour/classes/logger.dart (logger)"?>
```dart
var logger = Logger('UI');
logger.log('Button clicked');
```


### 方法

方法是为对象提供行为的函数。

#### 实例方法

对象的实例方法可以访问实例变量和 `this`。
下面的 `distanceTo()` 方法就是一个实例方法的例子：

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

#### Getter 和 Setter

Getter 和 Setter 是一对用来读写对象属性的特殊方法，
上面说过实例对象的每一个属性都有一个隐式的 Getter 方法，
如果为非 final 属性的话还会有一个 Setter 方法，
您可以通过使用 `get` 和 `set` 关键字实现 Getter 和 Setter 来创建其他属性：

<?code-excerpt "misc/lib/language_tour/classes/rectangle.dart"?>
```dart
class Rectangle {
  num left, top, width, height;

  Rectangle(this.left, this.top, this.width, this.height);

  // 定义两个计算产生的属性： right 和 bottom
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

使用 Getter 和 Setter 的好处是，您可以先使用实例变量，
之后再将它们封装成方法且不需要改动任何客户端代码，
即先定义后更改且不影响原有逻辑。

{{site.alert.note}}
  无论 Getter 是否显式定义，诸如自增 (++) 这样的操作符都以预期的方式工作。
  为了避免任何意外的副作用，操作符只调用 Getter 一次，
  然后将其值保存在一个临时变量中。
{{site.alert.end}}

#### 抽象方法

实例方法、Getter 方法以及 Setter 方法都可以是抽象的，
可以用于定义接口方法，但将其实现留给其他类。
抽象方法只能存在于 [抽象类](#抽象类) 中。

直接使用分号 (;) 替代方法体即可声明一个抽象方法：

<?code-excerpt "misc/lib/language_tour/classes/doer.dart"?>
```dart
abstract class Doer {
  // 定义实例变量和方法等

  void doSomething(); // 定义抽象方法
}

class EffectiveDoer extends Doer {
  void doSomething() {
    // 提供一个实现，因此此处方法不再是抽象的
  }
}
```


### 抽象类

使用 `abstract` 修饰符可以定义一个 *抽象类*（不能被实例化的类）。
抽象类对于定义接口方法是非常有用的。
如果您想让您的抽象类看起来可以被实例化，
请定义一个 [工厂构造器](#factory-constructors)。

抽象类常常会包含 [抽象方法](#abstract-methods)。
下面是一个含有一个抽象方法的抽象类的例子：

<?code-excerpt "misc/lib/language_tour/classes/misc.dart (abstract)"?>
```dart
// This class is declared abstract and thus
// can't be instantiated.
abstract class AbstractContainer {
  // Define constructors, fields, methods...

  void updateChildren(); // Abstract method.
}
```


### 隐式接口

每一个类都隐式地定义了一个接口，
这个接口包含所有这个类的实例成员以及这个类所实现的其它接口。
如果想要创建一个 A 类支持调用 B 类的 API 且不想继承 B 类，
则可以实现 B 类的接口。

类通过在 `implements` 子句中声明一个或多个接口，
然后提供接口所需的 API 来实现一个或多个接口。例如：

<?code-excerpt "misc/lib/language_tour/classes/impostor.dart"?>
```dart
// Person 类提供的隐式接口包含 greet() 方法
class Person {
  // 在接口中，但是只在库内可见
  final _name;

  // 不在接口中，因为它是一个构造器
  Person(this._name);

  // 在接口中
  String greet(String who) => 'Hello, $who. I am $_name.';
}

// Person 接口的一个实现
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

下面是一个类实现多个接口的示例：

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

You can use enums in [switch statements](#switch-和-case), and
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
[Set class]: {{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}/dart-core/Set-class.html
[StackTrace]: {{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}/dart-core/StackTrace-class.html
[Stream]: {{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}/dart-async/Stream-class.html
[String]: {{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}/dart-core/String-class.html
[Symbol]: {{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}/dart-core/Symbol-class.html
[synchronous-async-start]: https://github.com/dart-lang/sdk/blob/master/docs/newsletter/20170915.md#synchronous-async-start
[Type]: {{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}/dart-core/Type-class.html
