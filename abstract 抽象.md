在面向对象的概念中，所有的对象都是通过类来描绘的，但是反过来，并不是所有的类都是用来描绘对象的，如果一个类中没有包含足够的信息来描绘一个具体的对象，这样的类就是抽象类。
抽象类除了不能实例化对象之外，类的其它功能依然存在，成员变量、成员方法和构造方法的访问方式和普通类一样。
由于抽象类不能实例化对象，所以抽象类必须被继承，才能被使用。也是因为这个原因，通常在设计阶段决定要不要设计抽象类。
父类包含了子类集合的常见的方法，但是由于父类本身是抽象的，所以不能使用这些方法。
在 Java 中抽象类表示的是一种继承关系，一个类只能继承一个抽象类，而一个类却可以实现多个接口。
## 桥接模式
桥接模式是一种**结构型设计模式**，它的核心目的是**将抽象部分与它的实现部分分离，使它们都可以独立地变化**。
### 为什么要使用桥接模式？

假设我们要开发一个绘图系统，支持**形状**（矩形、圆形）和**绘图方式**（DP1库、DP2库）。
如果使用继承，通常会这样设计：
```
Shape (抽象)
├── RectangleDP1
├── RectangleDP2
├── CircleDP1
└── CircleDP2
```
- 形状种类：2 种
- 绘图方式：2 种  
    最终需要 **2 × 2 = 4** 个类。
如果增加三角形（3 种形状）和 DP3（3 种绘图方式） → **3 × 3 = 9** 个类。  
这就是**类爆炸**。每次增加新形状或新绘图方式，都要同时创建多个子类，代码重复严重，难以维护。
**桥接模式正是为了解决这个问题**：将“形状”和“绘图方式”分成两个独立的层次，通过组合（桥接）连接。
下面举个代码的例子

|    角色     |              作用               | 对应到代码 |
| :-------: | :---------------------------: | :---: |
|  **抽象化**  | 定义抽象类的接口，维护一个指向**实现部分**的引用（桥） |       |
| **扩展抽象化** |      对抽象化进行扩展，实现具体的业务逻辑       |       |
| **实现化接口** |      定义实现部分的接口，通常只提供基本操作      |       |
| **具体实现化** |  真正提供具体实现，实现 Implementor 接口   |       |
```java
// (1) 定义接口 Drawing
interface Drawing {
    // (2) 画线方法
    void drawLine(double x1, double y1, double x2, double y2);
    // (3) 画圆方法
    void drawCircle(double x, double y, double r);
}

class DP1 {
    static public void draw_a_line(double x1, double y1, double x2, double y2) { /* 代码省略 */ }
    static public void draw_a_circle(double x, double y, double r) { /* 代码省略 */ }
}

class DP2 {
    static public void drawline(double x1, double x2, double y1, double y2) { /* 代码省略 */ }
    static public void drawcircle(double x, double y, double r) { /* 代码省略 */ }
}

// 适配 DP1 的绘图实现
class V1Drawing implements Drawing {
    public void drawLine(double x1, double y1, double x2, double y2) { 
        /* 代码省略（可调用 DP1.draw_a_line）*/ 
    }
    public void drawCircle(double x, double y, double r) { 
        // (4) 调用 DP1 的静态方法画圆
        DP1.draw_a_circle(x, y, r);
    }
}

// 适配 DP2 的绘图实现
class V2Drawing implements Drawing {
    public void drawLine(double x1, double y1, double x2, double y2) { 
        /* 代码省略（可调用 DP2.drawline）*/ 
    }
    public void drawCircle(double x, double y, double r) { 
        // (5) 调用 DP2 的静态方法画圆
        DP2.drawcircle(x, y, r);
    }
}

// 抽象形状类（桥接模式中的 Abstraction）
abstract class Shape {
    private Drawing _dp;   // 持有 Drawing 接口的引用

    // 构造函数（原图片中遗漏了大括号，现补全）
    public Shape(Drawing dp) {
        _dp = dp;
    }

    // 委托给 _dp 画线
    public void drawLine(double x1, double y1, double x2, double y2) {
        _dp.drawLine(x1, y1, x2, y2);
    }

    // 委托给 _dp 画圆
    public void drawCircle(double x, double y, double r) {
        _dp.drawCircle(x, y, r);
    }

    // 抽象方法：每个形状自己实现绘制逻辑
    public abstract void draw();
}

// 矩形类
class Rectangle extends Shape {
    private double _x1, _x2, _y1, _y2;

    public Rectangle(Drawing dp, double x1, double y1, double x2, double y2) {
        super(dp);               // 调用父类构造函数，传入绘图实现
        _x1 = x1; _y1 = y1;
        _x2 = x2; _y2 = y2;
    }

    public void draw() {
        // 画四条边
        drawLine(_x1, _y1, _x2, _y1);
        drawLine(_x2, _y1, _x2, _y2);
        drawLine(_x2, _y2, _x1, _y2);
        drawLine(_x1, _y2, _x1, _y1);
    }
}

// 圆形类
class Circle extends Shape {
    private double _x, _y, _r;

    public Circle(Drawing dp, double x, double y, double r) {
        super(dp);
        _x = x; _y = y; _r = r;
    }

    public void draw() {
        drawCircle(_x, _y, _r);   // 直接调用父类的画圆方法
    }
}
```
