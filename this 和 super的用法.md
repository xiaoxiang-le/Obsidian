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

