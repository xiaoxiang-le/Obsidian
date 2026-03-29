
在Java中，`List`接口是一个有序的集合，它允许我们按顺序存储和访问元素。它扩展了集合接口。
**List**接口定义如下：
```java
public interface List<E> extends Collection<E>
```
其中`<E>`就是类型参数（通常称为“泛型类型”）。在实例化时，我们可以将`E`替换为具体的类，例如：
+ `List<company>`——只能存放`Company`或其·子类的对象
+ `List<String>`——只能存放字符串
+ ❌`List<int>`——编译错误
从上面可以看出`<>`里只能填写**引用类型**，**不能填写基本数据类型**,所以严格来说，它只能填写**类、接口、枚举、数组等引用类型**，不能填写像 `int` 这样的“数据类型”。
由于List是接口，因此无法从中创建对象。
为了使用List接口的功能，我们可以使用以下类：
+ [数组列表（`ArrayList`类）](ArrayList.md)
+ [[LinkList]]
+ 向量（`vector`类）
+ 堆栈（`Stack`类）
![图片说明](IMG-20260329213158741.png)
这些类在Collections框架中定义并实现List接口。
### 如何使用List？

在Java中，必须导入 java.util.List 包才能使用List。
```java
//List 的ArrayList 实现
List<String> list1 = new ArrayList<>();

// List 的LinkedList 实现
List<String> list2 = new LinkedList<>();
```
在这里，我们已经创建`ArrayList`和`LinkedList`类的对象`list1`和`list2`。现在这些对象可以使用List接口的功能。

### List方法
List接口包括Collection接口的所有方法。 这是因为Collection是List的超级接口。
Collection接口中还提供了一些常用的List接口方法：
- `add()` - 将元素添加到列表
    
- `addAll()` - 将一个列表的所有元素添加到另一个
    
- `get()` - 有助于从列表中随机访问元素
    
- `iterator()` - 返回迭代器对象，该对象可用于顺序访问列表的元素
    
- `set()` - 更改列表的元素
    
- `remove()` - 从列表中删除一个元素
    
- `removeAll()` - 从列表中删除所有元素
    
- `clear()` - 从列表中删除所有元素（比removeAll()效率更高）
    
- `size()` - 返回列表的长度
    
- `toArray()` - 将列表转换为数组
    
- `contains()` -  如果列表包含指定的元素，则返回true

#### 举个软考真题的例子
```java
(1) abstract class Company {
    protected String name;
    public Company(String name) { (2) this.name = name; }
    public abstract void Add(Company c);
    public abstract void Delete(Company c);
}

class ConcreteCompany extends Company {
    private List<(3) Company> children = new ArrayList<(4) Company>();
    public ConcreteCompany(String name) { super(name); }
    public void Add(Company c) { (5) children.add(c); }
    public void Delete(Company c) { (6) children.remove(c); }
}

// 省略 HRDepartment 和 FinanceDepartment 类

public class Test {
    public static void main(String[] args) {
        ConcreteCompany root = new ConcreteCompany("北京总公司");
        root.Add(new HRDepartment("总公司人力资源部"));
        root.Add(new FinanceDepartment("总公司财务部"));

        ConcreteCompany comp = new ConcreteCompany("上海分公司");
        comp.Add(new HRDepartment("上海分公司人力资源部"));
        comp.Add(new FinanceDepartment("上海分公司财务部"));
        (7) root.Add(comp);

        ConcreteCompany comp1 = new ConcreteCompany("南京办事处");
        comp1.Add(new HRDepartment("南京办事处人力资源部"));
        comp1.Add(new FinanceDepartment("南京办事处财务部"));
        (8) comp.Add(comp1);
    }
}
```
这里（3）（4）就是填我们列表的类型参数，由于`children`存储的是子公司、办事处或部门，都是Company的类型，所以这里填写的类型参数是Cimpany
