## this
this 是自身的一个对象，代表对象本身，可以理解为：**指向对象本身的一个指针**。
this 的用法在 Java 中大体可以分为3种：

**1.普通的直接引用**
这种就不用讲了，this 相当于是指向当前对象本身。

**2.形参与成员名字重名，用 this 来区分：**
举个例子：
```java
class Person {
    private int age = 10;
    public Person(){
    System.out.println("初始化年龄："+age);
}
    public int GetAge(int age){
        this.age = age;
        return this.age;
    }
}
 
public class test1 {
    public static void main(String[] args) {
        Person Harry = new Person();
        System.out.println("Harry's age is "+Harry.GetAge(12));
    }
}
```
可以看到，这里 `age` 是 `GetAge` 成员方法的形参，`this.age` 是 `Person` 类的成员变量。

**3.引用构造函数**
这个和 super 放在一起讲，见下面。

## super
super 可以理解为是指向自己超（父）类对象的一个指针，而这个超类指的是离自己最近的一个父类。
super 也有三种用法：

**1.普通的直接引用**

与 `this` 类似，`super` 相当于是指向当前对象的父类，这样就可以用 `super.xxx` 来引用父类的成员。

**2.子类中的成员变量或方法与父类中的成员变量或方法同名**
举个例子：
```java
class Country {
    String name;
    void value() {
       name = "China";
    }
}
  
class City extends Country {
    String name;
    void value() {
    name = "Shanghai";
    super.value();      //调用父类的方法
    System.out.println(name);
    System.out.println(super.name);
    }
  
    public static void main(String[] args) {
       City c=new City();
       c.value();
       }
}
```
可以看到，这里既调用了父类的方法，也调用了父类的变量。若不调用父类方法 `value()`，只调用父类变量 `name` 的话，则父类 `name` 值为默认值 `null`。

**3.引用构造函数**
- **super(参数)**：调用父类中的某一个构造函数（应该为构造函数中的第一条语句）。
- **this(参数)**：调用本类中另一种形式的构造函数（应该为构造函数中的第一条语句）。
在这里补充一下构造函数和构造方法的知识：
+ 构造函数
	**1. 方法名必须与类名完全相同**
```java
	class Light {
    public Light() { }          // 构造函数，名称为 Light
}
```
	*2.*
	（连 `void` 都不能写）  
    普通方法可以有返回值，但构造函数不能有任何返回类型声明。