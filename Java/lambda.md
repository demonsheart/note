## lambda

### 函数式接口

只有一个抽象方法的接口叫做函数式接口

```java
interface Name{
    void theOnlyMethod();
}
```

### 函数式接口可用lambda实现

```java
(parameters) -> expression
或
(parameters) ->{ statements;}
// 调用
Name object = () -> System.out.println("dddd");
object.theOnlyMethod();
```

### 变量作用域

lambda 表达式**只能引用标记了 final 的外层局部变量**，这就是说不能在 lambda 内部修改定义在域外的局部变量，否则会编译错误。

```java
public class Java8Tester {
 
   final static String salutation = "Hello! ";
   
   public static void main(String args[]){
      GreetingService greetService1 = message -> 
      System.out.println(salutation + message);
      greetService1.sayMessage("Runoob");
   }
    
   interface GreetingService {
      void sayMessage(String message);
   }
}
```

执行以上脚本，输出结果为：

```
$ javac Java8Tester.java 
$ java Java8Tester
Hello! Runoob
```

我们也可以**直接在 lambda 表达式中访问外层的局部变量**：

```java
public class Java8Tester {
    public static void main(String args[]) {
        final int num = 1;
        Converter<Integer, String> s = (param) -> System.out.println(String.valueOf(param + num));
        s.convert(2);  // 输出结果为 3
    }
 
    public interface Converter<T1, T2> {
        void convert(int i);
    }
}
```



lambda 表达式的局部变量可以不用声明为 final，但是**必须不可被后面的代码修改**（即隐性的具有 final 的语义）

```java
int num = 1;  
Converter<Integer, String> s = (param) -> System.out.println(String.valueOf(param + num));
s.convert(2);
num = 5;  
//报错信息：Local variable num defined in an enclosing scope must be final or effectively final
```

在 Lambda 表达式当中不允许声明一个与局部变量同名的参数或者局部变量。

```java
String first = "";  
Comparator<String> comparator = (first, second) -> Integer.compare(first.length(), second.length());  //编译会出错 
```