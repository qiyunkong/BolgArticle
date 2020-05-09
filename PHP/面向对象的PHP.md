# 面向对象的PHP

​	所有事物都可以抽象为对象，我们将对象的属性和行为（方法统一到一个“类”中；然后实例化类，即规定对象特定的属性和方法；这样具体的对象就能完成一系列不同的行为。这就是面向对象编程”

## PHP类和对象

类是面向对象程序设计的基本概念，通俗的理解类就是对现实中某一个种类的东西的抽象， 比如汽车可以抽象为一个类，汽车拥有名字、轮胎、速度、重量等属性，可以有换挡、前进、后退等操作方法。

通常定义一个汽车类的方法为：

```php
class Car{
    $name = '汽车';
    function getName(){
        return $this->name;
    }
}
```

类是一类东西的结构描述，而对象则是一类东西的一个具体实例，例如汽车这个名词可以理解为汽车的总类，但这辆汽车则是一个具体的汽车对象。

对象通过new关键字进行实例化：

```php
$car = new Car();
echo $car->getName();
```

类与对象看起来比较相似，但实际上有本质的区别，类是抽象的概念，对象是具体的实例。类可以使程序具有可重用性。

## PHP类和对象之创建一个对象

​	上一节，我们使用汽车举例来认识了类与对象，本节我们来了解一下类的定义方法，类通过关键字class开头，然后是类名与花括号，在花括号中定义类的属性与方法。类名必须是字母或下划线开头，后面紧跟若干个字母、数字或下划线，类名最好能够表意，可以采用名词或者英文单词

```php
//定义一个类
class Car {
    //定义属性
    public $name = '汽车';

    //定义方法
    public function getName() {
        //方法内部可以使用$this伪变量调用对象的属性或者方法
        return $this->name;
    }
}
```

要创建一个类的实例，可以使用new关键字创建一个对象。

```php
$car = new Car();
//也可以采用变量来创建
$className = 'Car';
$car = new $className();
```

## PHP类和对象之类的属性

在类中定义的变量称之为属性，通常属性跟数据库中的字段有一定的关联，因此也可以称作“字段”。属性声明是由关键字 public，protected 或者 private 开头，后面跟一个普通的变量声明来组成。属性的变量可以设置初始化的默认值，默认值必须是常量。

访问控制的关键字代表的意义为：

public：公开的
protected：受保护的
private：私有的

```php
class Car{
    //定义公共属性
    public $name = '汽车';
    //定义保护的属性
    protected $corlor = '白色';
    
    //定义私用属性
    private $price = '1000000';
    
}
```

默认都为public，外部可以访问。一般通过->对象操作符来访问对象的属性或者方法，对于静态属性则使用::双冒号进行访问。当在类成员方法内部调用的时候，可以使用$this伪变量调用当前对象的属性。

```php
$car = new Car();
echo $car->name;//调用对象的属性
echo $car->color; //错误 受保护的属性不允许外
echo $car->price; //错误 私有属性不允许外部调用
```

受保护的属性与私有属性不允许外部调用，在类的成员方法内部是可以调用的。

```php
class Car{
    private $price = '1000';
    public function getPrice(){
        return $this->price; //内部访问私有属性
        
    }
    
}
```

## PHP类和对象之定义类的方法

方法就是在类中的function，很多时候我们分不清方法与函数有什么差别，在面向过程的程序设计中function叫做函数，在面向对象中function则被称之为方法。

同属性一样，类的方法也具有public，protected 以及 private 的访问控制。

访问控制的关键字代表的意义为：
public：公开的
protected：受保护的
private：私有的

我们可以这样定义方法：

```php
class  Car{
	public function getName(){
        return '汽车';
        
    }
}
$car = new Car();
echo $car->getName();
```

使用关键字static修饰的，称之为静态方法，静态方法不需要实例化对象，可以通过类名直接调用，操作符为双冒号::。

```php
class Car{
	public static function getName(){
        return '汽车';
        
    }
}
echo Car::getName(); //结果为汽车
```

## PHP类和对象之构造函数和析构函数

PHP5可以在类中使用**__construct()**定义一个构造函数，具有构造函数的类，会在每次对象创建的时候调用该函数，因此常用来在对象创建的时候进行一些初始化工作。

```php
class Car{
    function __construct(){
        print "构造函数被调用\n";
        
    }
}
$car = new Car(); //实例化的时候 会自动调用构造函数 __construct,这里会输出一个字符串构造函数__construct,
```

在子类中如果定义了__construct则不会调用父类的__construct，如果需要同时调用父类的构造函数，需要使用parent::__construct()显式的调用。

```php
class Car{
   function __construct(){
       print "父类构造函数被调用\n";
   }
}
class Truck extends Car{
    function __construct(){
        print "子类构造函数被调用\n";
        parent::__construct();
    }
}
$car = new Truck();
```

同样，PHP5支持析构函数，使用**__destruct()**进行定义，析构函数指的是当某个对象的所有引用被删除，或者对象被显式的销毁时会执行的函数。

```php
class Car{
    function __construct(){
        print "构造函数被调用\n";
    }
    function __destruct(){
        print "解析构造函数被调用\n";
    }
}
$car = new Car();
echo '使用后，准备销毁car对象\n';
unset($car); //销毁时会调用解析函数
```

当PHP代码执行完毕以后，会自动回收与销毁对象，因此一般情况下不需要显式的去销毁对象。

## PHP类和对象之Static静态关键字

静态属性与方法可以在不实例化类的情况下调用，直接使用`类名::方法名`的方式进行调用。静态属性**不允许**对象使用->操作符调用。

```php
class Car{
    private static $speed = 10;
    
    public static function getSpeed(){
        return self::$speed;
    }
}
echo Car::getSpeed(); //调用静态方法
```

静态方法也可以通过变量进行动态调用

```php
$func = 'getSpeed';
$className = 'Car';
echo $className::$func(); //动态调用静态方法
```

静态方法中，$this伪变量不允许使用。可以使用self，parent，static在内部调用静态方法与属性。

```php
class Car{
	private static $speed = 10;
    public static function getSpeed(){
        return self::$speed;
    }
    public static function speedUp(){
        return self::$speed+=10;
    }
}
class BigCar extends Car{
    public static function start(){
        parent::speedUp(); //parent调用父类的方法
    }
}
BigCar::start();
echo BigCar::getSpeed();
```

## PHP类和对象之访问控制

前面的小节，我们已经接触过访问控制了，访问控制通过关键字public，protected和private来实现。被定义为公有的类成员可以在任何地方被访问。被定义为受保护的类成员则可以被其自身以及其子类和父类访问。被定义为私有的类成员则只能被其定义所在的类访问。

类属性必须定义为**公有**、**受保护**、**私有**之一。为兼容PHP5以前的版本，如果采用 var 定义，则被视为公有。

```php
class car{
	$speed = 10; //错误 属性必须定义访问控制
	public $name; //定义共有属性

}
```

类中的方法可以被定义为**公有**、**私有**或**受保护**。如果没有设置这些关键字，则该方法默认为**公有**。

```php
class Car {
   //默认为共有方法
    function turnLeft() {
    }
}
```

如果构造函数定义成了私有方法，则不允许直接实例化对象了，这时候一般通过静态方法进行实例化，在设计模式中会经常使用这样的方法来控制对象的创建，比如单例模式只允许有一个全局唯一的对象。

```php
class Car{
    private function __construct(){
        echo 'object create';
    }
    private static $_object = null;
    public static function getInstance(){
        if(empty(self::$_object)){
            self::$_object= new Car(); //内部方法可以可以调用私用方法，因此这里可以创建对象
        }
        return self::$_object;
    }
}
//$car = new Car(); //这里不允许直接实例化对象
$car = Car::getInstance() //通过静态方法来获得一个实例
```

## PHP类和对象之对象继承

继承是面向对象程序设计中常用的一个特性，汽车是一个比较大的类，我们也可以称之为基类，除此之外，汽车还分为卡车、轿车、东风、宝马等，因为这些子类具有很多相同的属性和方法，可以采用继承汽车类来共享这些属性与方法，实现代码的复用

```php
class Car {
    public $speed = 0; //汽车的起始速度是0
    
    public function speedUp() {
        $this->speed += 10;
        return $this->speed;
    }
}
//定义继承于Car的Truck类
class Truck extends Car{
    public function speedUp(){
        $this->speed= parent::speedUp()+50;
        return $this->speed;
    }
}

$car = new Truck();
$car->speedUp();
echo $car->speed;
```

## PHP类和对象之重载

PHP中的重载指的是动态的创建属性与方法，是通过魔术方法来实现的。属性的重载通过__set，__get，__isset，__unset来分别实现对不存在属性的赋值、读取、判断属性是否设置、销毁属性。

```php
class Car{
    private $ary = array();
    public function __set($key,$val){
        $this->ary[$key] = $val;
    }
    public function __get($key){
        if(isset($this->ary[$key])){
            return $this->ary[$key];
        }
        return null;
    }
    public function __isset($key){
        if(isset($this->ary[$key])){
            return true;
        }
        return false;
    }
    public function __unset($key){
        unset($this->ary[$key]);
    }
}
$car = new Car();
$car->name = '汽车'; //name 属性动态创建并赋值
echo $car->name;
```

方法的重载通过__call来实现，当调用不存在的方法的时候，将会转为参数调用__call方法，当调用不存在的静态方法时会使用__callStatic重载

```php
class  Car{
	public $speed = 0;
    public function __call($name,$args){
        if($name === 'speedUp'){
            $this->speed +=10;
        }
    }
}
$car = new Car();
$car->speedUp(); //调用不存在的方法会使用承载
echo $car->speed;
```

## PHP类和对象之对象的高级特性

对象比较，当同一个类的两个实例的所有属性都相等时，可以使用比较运算符==进行判断，当需要判断两个变量是否为同一个对象的引用时，可以使用全等运算符===进行判断。

```php
class Car{}
$a = new Car();
$b = new Car();
if($a == $b) echo "==" //true
if($a === $b) echo "===" //false
```

对象复制，在一些特殊情况下，可以通过关键字clone来复制一个对象，这时__clone方法会被调用，通过这个魔术方法来设置属性的值。

```php
class Car {
    public $name = 'car';
    
    public function __clone() {
        $obj = new Car();
        $obj->name = $this->name;
    }
}
$a = new Car();
$a->name = 'new car';
$b = clone $a;
var_dump($b);
```

对象序列化，可以通过serialize方法将对象序列化为字符串，用于存储或者传递数据，然后在需要的时候通过unserialize将字符串反序列化成对象进行使用。

```php
class Car {
    public $name = 'car';
}
$a = new Car();
$str = serialize($a); //对象序列化成字符串
echo $str.'<br>';
$b = unserialize($str); //反序列化为对象
var_dump($b);
```

