# Java基础

[Java菜鸟教程链接](https://www.runoob.com/java/java-basic-datatypes.html)

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

```java
//JDK7新特性
int money = 10_0000_0000;
System.out.println(money);
```

## 变量

### 命名规范

* 见名知意
* 类成员变量：首字母小写 驼峰 lastName
* 局部变量： 首字母小写 驼峰 lastName
* 常量： 大写字母和下划线  MAX_LENTH
* 类名： 首字母大写 驼峰 GoodMan
* 方法名：首字母小写 驼峰 runALL()