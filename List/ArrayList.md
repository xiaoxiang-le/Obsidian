
`ArrayList` 类是一个可以动态修改的数组，与普通数组的区别就是它是没有固定大小的限制，我们可以添加或删除元素。
`ArrayList `继承了 `AbstractList `，并实现了 List 接口。
![[IMG-20260329213158738.png]]
`ArrayList `类位于 java.util 包中，使用前需要引入它，语法格式如下：
```java
import java.util.ArrayList; // 引入 ArrayList 类
ArrayList<E> objectName =new ArrayList<>();　 // 初始化
```
+  **E**: 泛型数据类型，用于设置 **`objectName`的数据类型，**只能为引用数据类型**。
+ **`objectName`**: 对象名。
##  添加元素

`ArrayList `类提供了很多有用的方法，添加元素到` ArrayList` 可以使用 `add() `方法:
```java
import java.util.ArrayList;

public class RunoobTest {
    public static void main(String[] args) {
        ArrayList<String> sites = new ArrayList<String>();
        sites.add("Google");
        sites.add("Runoob");
        sites.add("Taobao");
        sites.add("Weibo");
        System.out.println(sites);
    }
}
```
以上实例，执行输出结果为：
```
[Google, Runoob, Taobao, Weibo]
```
##  访问元素

访问` ArrayList` 中的元素可以使用 `get() `方法：
```java
import java.util.ArrayList;

public class RunoobTest {
    public static void main(String[] args) {
        ArrayList<String> sites = new ArrayList<String>();
        sites.add("Google");
        sites.add("Runoob");
        sites.add("Taobao");
        sites.add("Weibo");
        System.out.println(sites.get(1));  // 访问第二个元素
    }
}
```
**注意**：数组的索引值从 0 开始。
以上实例，执行输出结果为：
```
Runoob
```
## 修改元素

如果要修改 `ArrayList `中的元素可以使用 `set() `方法， `set(int index, E element) `方法的第一个参数是索引`（index）`，表示要替换的元素的位置，第二个参数是新元素`（element）`，表示要设置的新值：
```java
import java.util.ArrayList;

public class RunoobTest {
    public static void main(String[] args) {
        ArrayList<String> sites = new ArrayList<String>();
        sites.add("Google");
        sites.add("Runoob");
        sites.add("Taobao");
        sites.add("Weibo");
        sites.set(2, "Wiki"); // 第一个参数为索引位置，第二个为要修改的值
        System.out.println(sites);
    }
}
```
以上实例，执行输出结果为：
```
[Google, Runoob, Wiki, Weibo]
```
## 删除元素

如果要删除 `ArrayList`中的元素可以使用` remove() `方法：

```java
import java.util.ArrayList;

public class RunoobTest {
    public static void main(String[] args) {
        ArrayList<String> sites = new ArrayList<String>();
        sites.add("Google");
        sites.add("Runoob");
        sites.add("Taobao");
        sites.add("Weibo");
        sites.remove(3); // 删除第四个元素
        System.out.println(sites);
    }
}
```
以上实例，执行输出结果为：
```
[Google, Runoob, Taobao]
```
## 计算大小

如果要计算 `ArrayList `中的元素数量可以使用` size() `方法：
```java
import java.util.ArrayList;

public class RunoobTest {
    public static void main(String[] args) {
        ArrayList<String> sites = new ArrayList<String>();
        sites.add("Google");
        sites.add("Runoob");
        sites.add("Taobao");
        sites.add("Weibo");
        System.out.println(sites.size());
    }
}
```
以上实例，执行输出结果为：
```
4
```
