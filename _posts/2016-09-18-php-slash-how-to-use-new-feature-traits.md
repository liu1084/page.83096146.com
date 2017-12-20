---
layout: post
title: "php/How to use new feature: traits"
date: 2016-09-18 11:35:41 +0800
comments: true
categories: 
---


## 什么是trait

PHP 5.4中的traits，是新引入的特性，中文还真不知道如何准确翻译好。其实际的目的，是为了有的场合想用多继承，但PHP又没多继承，于是就发明了这样的一个东西。
Traits可以理解为一组能被不同的类都能调用到的方法集合，但Traits不是类！不能被实例化。先来例子看下语法：

```php
<?php
trait myTrait{
    function traitMethod1(){}
    function traitMethod2(){}

}

//然后是调用这个traits,语法为：
class myClass{
    use myTrait;
}

//这样就可以通过use myTraits，调用Traits中的方法了，比如：
$obj = new myClass();
$obj-> traitMethod1 ();
$obj-> traitMethod2 (); 
>

```

接下来，我们探究下为什么要用traits，举个例子，比如有两个类，分别为business（商务者）和Individual(个人），它们都有地址的属性，传统的做法是，再抽象出一个这两个类都共同有特性的父类，比如client，在client类中设置访问属性address,business和individual分别继承之，如下代码：

```php
// Class Client  
class Client  {  
    private $address;  
    public getAddress() {  
        return $this->address;  
    }       
    public setAddress($address) {  
        $this->address = $address;    
    }  
}  
      
class Business extends Client{  
    //这里可以使用address属性  
}  

// Class Individual  
class Individual extends Client{  
//这里可以使用address属性  
}  
```

但假如又有一个叫order类的，需要访问同样的地址属性，那怎么办呢？order类是没办法继承client类的，因为这个不符合OOP的原则。这个时候traits就派上用场了，可以定义一个traits，用来定义这些公共属性。

```php

// Trait Address
trait Address{
    private $address;
    public getAddress() {
        eturn $this->address;
    }
    public setAddress($address) {
        $this->address = $address;
    }
}
// Class Business
class Business{
    use Address;
    // 这里可以使用address属性
}
// Class Individual
class Individual{
    use Address;
    //这里可以使用address属性
}
// Class Order
class Order{
    use Address;
    //这里可以使用address属性
}  

```

## 优先级
从基类继承的成员会被 trait 插入的成员所覆盖。优先顺序是来自当前类的成员覆盖了 trait 的方法，而 trait 则覆盖了被继承的方法。