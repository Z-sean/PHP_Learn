# 变量
PHP是弱类型语言，变量类型在运行时会
PHP的变量声明与初始化是一次性完成的，不支持分开操作
使用变量的优点是：方便引用，一次声明，多次引用，且变量可在运行时修改
```php
$greeting = "hello,php".PHP_EOL;
```
PHP_EOL是PHP内置的换行符，printf是PHP内置的输出函数，.是PHP中的连接符
# 变量命名规则
- 以 $ 开头（坊间戏言，PHP 程序员是有多穷，才要求变量名以货币符号开头?）；
- $ 之后具体的变量名只支持字母（支持中文字符，不过我们尽量使用 ASCII 字符，以免出现意想不到的问题）、数字、下划线，并且不能以数字开头；
- 由于是以$开头的，所以也支持关键字与保留字作为变量名
- PHP大小写敏感
```php
$greet
$_greet
$基础
$greet2
```
# 变量名引用
PHP变量可通过在变量名之前加$达到对变量名的引用效果
```php
$greet = "hellophp";
$hellophp = "hello";
echo $$greet;

===========
#输出：
hello
```
# 常量
常量一经定义就无法再修改，目的是设置运行时的只读变量
## 定义方式一
define函数
```php
define("NAME","php");

```
该函数接收两个参数，分别是常量名与常量值，与变量不同，不需要$来表示，直接使用常量名，且常量名一般全大写，命名规则与变量大致相同
通过define（）定义的常量是全局有效，所以通常在项目初始化期间通过这种方式定义全局常量。
## 定义方式二：
使用const关键字，该方式通常用于设置类常量
```php
<?php

define("LANGUAGE", "PHP");
define("AUTHOR", "学院君");

const FRAMEWORK = "Laravel";
echo LANGUAGE. '-' . FRAMEWORK . '-' . AUTHOR . PHP_EOL;
```
# 数据类型与转换
通过is_type()/var_dump()可以查看变量的类型
## 字符串形式
字符串使用''或者""来表示，区别是，双引号可以解析在包含在其中的变量/转义字符，单引号同样可以，但编写复杂，可读性差
## 整形
整形的长度是固定的，通过内置的常量可以查看范围值（PHP_INT_MIN和 PHP_INT_MAX），也就是 8 个字节长度
## 浮点型
float、double,后者的范围更大，同样性能就更差
浮点数采用近似计算，所以对于确定的十进制数字来说，尽管表面上的浮点数相等，但实际上二者不同，不能直接对浮点数进行相等比较
## 布尔型
true、false
## 类型转换
PHP支持基本数据类型之间的转换，只需要在变量名前通过添加 (目标转化类型) 强制转化即可
同时根据上下文，PHP会自动（当值需要解释为某种类型时，值**本身不会改变类型**）对变量值进行类型转换
### 数字上下文
如果任一运算对象是 float（或者不能解释为 int），则两个运算对象都将解释为 float，结果也将是 float。否则，运算对象将解释为 int，结果也将是 int。自 PHP 8.0.0 起，如果无法解释其中一个运算对象，则会抛出 TypeError。
### 字符串上下文
使用echo、print、字符串插值或者字符串连接运算符时的上下文。
这种情况下，值将会解释为 string。如果值无法解释，那么会抛出 TypeError。在 PHP 7.4.0 之前，会引发 E_RECOVERABLE_ERROR。
### 逻辑上下文
使用条件语句、三元运算符或逻辑运算符时的上下文。
在这种情况下，值将会解释为 bool。

.....
---
# 运算符
算数运算符
```php
// 基本运算
$a + $b    // 加法
$a - $b    // 减法
$a * $b    // 乘法
$a / $b    // 除法
$a % $b    // 求余
$a ** $b   // 指数运算(PHP 5.6+)

// 简写形式
$a += $b;  // 等价于 $a = $a + $b
$a -= $b;  // 等价于 $a = $a - $b
$a *= $b;  // 等价于 $a = $a * $b
$a /= $b;  // 等价于 $a = $a / $b
$a %= $b;  // 等价于 $a = $a % $b
```
自增/自减运算符
```php
// 前置和后置的区别
$a++;   // 后置自增,返回原值,然后增加
++$a;   // 前置自增,增加后返回新值
$a--;   // 后置自减
--$a;   // 前置自减
```
比较运算符
```php
// 值比较
$a == $b   // 等于
$a != $b   // 不等于
$a > $b    // 大于
$a >= $b   // 大于等于
$a < $b    // 小于
$a <= $b   // 小于等于

// 严格比较(同时比较值和类型)
$a === $b  // 完全等于
$a !== $b  // 完全不等于
```
逻辑运算符
```php
$a && $b   // 与运算(and)
$a || $b   // 或运算(or)
!$a        // 非运算(not)
$a xor $b  // 异或运算

// 逻辑运算结合比较运算
if ($a > $b && $a < $c) {
    // 条件成立
}
```
类型转换规则
```php
// 转为 false 的情况:
false      // 布尔值false
0,-0,0.0   // 零值
"",'',     // 空字符串
"0",'0'    // 字符串零
[]         // 空数组
null       // NULL值

// 其他情况都转为 true
```
# 流程控制
选择结构
```php
// 单分支
if ($score >= 80) {
    echo "优秀";
}

// 双分支
if ($score >= 80) {
    echo "优秀";
} else {
    echo "继续努力";
}

// 多分支
if ($score >= 90) {
    echo "A";
} else if ($score >= 80) {
    echo "B"; 
} else if ($score >= 60) {
    echo "C";
} else {
    echo "D";
}

// switch结构
switch ($score) {
    case $score >= 90:
        $level = "A";
        break;
    case $score >= 80:
        $level = "B";
        break;
    default:
        $level = "C";
        break;
}
```
循环结构
```php
// while循环
$i = 1;
while ($i <= 10) {
    echo $i++;
}

// do...while循环
do {
    echo $i++;
} while ($i <= 10);

// for循环
for ($i = 1; $i <= 10; $i++) {
    echo $i;
}

// foreach循环(数组专用)
foreach ($array as $key => $value) {
    echo "$key => $value";
}
```
循环控制
```php
// break - 跳出整个循环
foreach ($array as $value) {
    if ($value == 5) {
        break;
    }
}

// continue - 跳过本次循环
foreach ($array as $value) {
    if ($value == 5) {
        continue;
    }
    echo $value;
}
```
选择结构：
- 条件简单时使用if-else
- 多条件判断时优先使用switch
- switch语句记得加break防止穿透
循环结构：
- 数组遍历优先使用foreach
- 需要精确控制循环次数时使用for
- while适用于不确定循环次数的场景

# 数组
## 数组创建
索引数组指的是数组的键为隐式数字，并且会自动维护
```php
<?php

$nums = [2, 4, 8, 16, 32];
$lans = ['PHP', 'Golang', 'JavaScript'];
```
除了指定值来初始化创建数组外，还可以初始化一个空数组，在 PHP 中，初始化空数组时不必指定数组大小，也不必指定数据类型
```php
$fruits = [];
``` 

## 数组操作（增删改查）
- 向数组中添加元素
```php
$fruits[] = 'Apple';
$fruits[] = 'Orange';
$fruits[] = 'Pear';
```
通过count()函数获取数组长度
- 删除某个元素
```php
unset($fruits[1]);
```
- 修改某个元素值
```php
$fruits[2] = 'Banana';
```
- 查看某个索引的元素-通过键来查看
```php
$fruit = $fruits[0];
```
对于一般的数组修改，数组不会自动重排索引，而是留出了一个「空洞」
如果想获取重新索引的新数组，可以通过函数array_values 来实现
要删除整个数组，可以用 unset($fruits) 实现，删除之后，$fruits 值变为 NULL并且不可用 
PHP数组支持各种类型，这也是与其他语言数组不同的地方
```php
$book = [
    'Laravel精品课',
    '学院君',
    2020,
    99.0,
    false
];
```
再打印布尔类型时，false 会被转化为空字符串，true 会被转化为 1，另外浮点型数字也会被转化为对应的字符串格式数据。

另外，PHP 数组底层是哈希表驱动，所以支持无限扩容。
