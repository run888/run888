# PHP

## 变量

四种变量   全局数组   $开头   不声明为空

echo

## 数据类型

String（字符串）, Integer（整型）, Float（浮点型）, Boolean（布尔型）, Array（数组）, Object（对象）, NULL（空值）。

var_dump



- 松散比较：使用两个等号 **==** 比较，只比较值，不比较类型。
- 严格比较：用三个等号 **===** 比较，除了比较值，也比较类型。

![image-20210507114928776](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210507114928776.png)

### 常量

``` PHP
define("GREETING", "欢迎访问 Runoob.com");
echo GREETING;    // 输出 "欢迎访问 Runoob.com"   不需要加$
echo '<br>';
echo greeting;   // 输出 "greeting"  第三个参数
```



### 字符串

并置运算符 (.)    strlen()    strpos() 



### 运算符

xor 异或

![image-20210507124202268](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210507124202268.png)



### 数组

``` php
$cars=array("Volvo","BMW","Toyota");
//可以自己分配键值
count($cars);
```

### 关联数组

关联数组是使用您分配给数组的指定的键的数组。

``` php
$age=array("Peter"=>"35","Ben"=>"37","Joe"=>"43");
$age['Peter']="35";
$age['Ben']="37";
$age['Joe']="43";

$age=array("Peter"=>"35","Ben"=>"37","Joe"=>"43");
 
foreach($age as $x=>$x_value)
{
    echo "Key=" . $x . ", Value=" . $x_value;
    echo "<br>";
}
```



### 排序

- sort() - 对数组进行升序排列
- rsort() - 对数组进行降序排列
- asort() - 根据关联数组的值，对数组进行升序排列
- ksort() - 根据关联数组的键，对数组进行升序排列
- arsort() - 根据关联数组的值，对数组进行降序排列
- krsort() - 根据关联数组的键，对数组进行降序排列



## 超级全局变量

- $GLOBALS
- $_SERVER
- $_REQUEST
- $_POST
- $_GET
- $_FILES
- $_ENV
- $_COOKIE
- $_SESSION



## 运算符

错误抑制符 @   （waring   notice级别）

合并运算$a ?? B

连接运算  .

优先级





## 循环

- **foreach** - 根据数组中每个元素来循环代码块

![image-20210507131359695](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210507131359695.png)

``` php
<?php

$info = array('name' => '鸣人', 'kill'=> '螺旋丸');
foreach($info as $key => $value) {
    echo $key .':'. $value;
} 

<?php

$info = array('name' => '鸣人', 'kill'=> '螺旋丸');
foreach($info as $value) {
   echo $value;
} 
```







## 魔术常量

trait

## 命名空间

![image-20210507140717119](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210507140717119.png)

![image-20210507141319208](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210507141319208.png)



。。。。



## 面向对象



### 构造析构

``` php
class MyDestructableClass {
   function __construct() {
       print "构造函数\n";
       $this->name = "MyDestructableClass";
   }

   function __destruct() {
       print "销毁 " . $this->name . "\n";
   }
}
```

### 继承

不支持多继承

``` php
class Child extends Parent {
   // 代码部分
}
```



### 访问控制

类属性必须定义为公有，受保护，私有之一。如果用 var 定义，则被视为公有。

类中的方法可以被定义为公有，私有或受保护。如果没有设置这些关键字，则该方法默认为公有。





### 接口

``` php
// 声明一个'iTemplate'接口
interface iTemplate
{
    public function setVariable($name, $var);
    public function getHtml($template);
}


// 实现接口
class Template implements iTemplate
{
    private $vars = array();
  
    public function setVariable($name, $var)
    {
        $this->vars[$name] = $var;
    }
  
    public function getHtml($template)
    {
        foreach($this->vars as $name => $value) {
            $template = str_replace('{' . $name . '}', $value, $template);
        }
 
        return $template;
    }
}
```



### 抽象类

``` php
abstract class AbstractClass
{
 // 强制要求子类定义这些方法
    abstract protected function getValue();
    abstract protected function prefixValue($prefix);

    // 普通方法（非抽象方法）
    public function printOut() {
        print $this->getValue() . PHP_EOL;
    }
}

class ConcreteClass1 extends AbstractClass
{
    protected function getValue() {
        return "ConcreteClass1";
    }

    public function prefixValue($prefix) {
        return "{$prefix}ConcreteClass1";
    }
}
```



### static  

静态属性不能通过一个类已实例化的对象来访问（但静态方法可以）。

由于静态方法不需要通过对象即可调用，所以伪变量 $this 在静态方法中不可用。

静态属性不可以由对象通过 -> 操作符来访问。

``` php
<?php
class Foo {
  public static $my_static = 'foo';
  
  public function staticValue() {
     return self::$my_static;
  }
}

print Foo::$my_static . PHP_EOL;
$foo = new Foo();

print $foo->staticValue() . PHP_EOL;
?>   
```



### final

``` php
class BaseClass {
   public function test() {
       echo "BaseClass::test() called" . PHP_EOL;
   }
   
   final public function moreTesting() {
       echo "BaseClass::moreTesting() called"  . PHP_EOL;
   }
}
```



### 调用父类构造方法

PHP 不会在子类的构造方法中自动的调用父类的构造方法。要执行父类的构造方法，需要在子类的构造方法中调用 **parent::__construct()** 。





## 文件

### 文件包含

直接放到对应位置PHP代码就会解析

执行的时候才会去编译

``` php
include ;
require ; //没有找到会报错   如果有函数就会报错重名
include_once ; 
require_once ; //包含一次会检测有没有包含    有开销
```



