# Java基础



## 编译运行

1. 编写Hello.java

   ```java
   public class Hello {
       public static void main(String[] args) {
           System.out.print("Hello,World!");
       }
   }
   ```

   注意类名和文件名保持一致并且首字母大写

2. 编译.java文件

   ```bash
   javac Hello.java
   ```

   得到一个Hello.class文件

3. 运行

   ```bash
   java Hello
   ```

   [如果出现错误，参考](https://www.zhihu.com/question/36537093)



## 注释

```java
//JavaDoc:文档注释
/**
 * @Descciption HelloWorld
 * @Author demonsheart
 */
```



## 数据类型



```java
long num1 = 3L; //long 类型要在后面加个L
float num2 = 3.1F; //float 类型要在后面加个F
```

