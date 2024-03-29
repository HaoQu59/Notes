# Scala 语言入门

Scala是一门以Java虚拟机（JVM）为运行环境并将**面向对象**和**函数式编程**的特性结合在一起的**静态类型编程语言**（静态语言需要提前编译如：Java、C、C++等，动态语言如：js）

特点：
- Scala是一门多范式的编程语言，Scala支持**面向对象**和**函数式编程**（多范式，就是多种编程方式。有面向过程、面向对象、泛型、函数式四种程序设计方法）
- Scala源代码（.scala）会被编译成Java字节码（.class），然后运行于JVM，**并可以调用现有的Java类库，实现两种语言的无缝对接**
- Scala**简洁高效**
- Scala源于Java，将**函数式编程思想**融入Java

和Java关系：
```
        javac               java
.java --------> .class ----------> run on JVM
.scala -------> .class ----------> run on JVM
        scalac              scala
```

# 环境配置

Windows中下载安装配置环境变量：
- 类似于java配置`SCALA_HOME`为安装目录
- 添加`%SCALA_HOME%\bin`到path环境变量

配置完成后在CMD下输入scala检测是否配置成功

CMD下输入scala进入交互式平台，可以在其中编写代码
```
scala>

val a = 10
val b = 20
a + b

println("Hello, world!")
```

新建`HelloScala.scala`文件

```scala
object HelloScala { // HelloScala is a object, not a class, will create a 
    def main(args : Array[String]) : Unit = {
        println("hello,world!");
    }
}
```

CMD输入

```
scalac HelloScala.scala
scala HelloScala
```

和Java编译如出一辙，Java编译后生成一个.class文件，而Scala编译后生成两个.scala文件分别为`HelloScala$.class`和`HelloScala.class`。

**这两个文件不能通过java进行运行**
Java没有引入Scala类库，添加classpath就可以通过java来执行scala编译的字节码文件

```
java -cp %SCALA_HOME%/lib/scala-library.jar; HelloScala
```

`HelloScala.class`为伴生对象的伴生类，`HelloScala$.class`为伴生对象的所属类

# IDEA环境配置

使用IntelliJ IDEA：

- 创建Maven项目
- idea可以管理安装scala
- Maven项目默认用Java写，在`main`目录下新建目录`scala`，然后将该目录标记(Mark Directory as)Source Root
- 对项目Add Framework support添加Scala SDK

```scala
object HelloWorld {
  def main(args: Array[String]): Unit = {
    println("hello world")
  }
}
```

- Ctrl + Shift + F10运行
- 可以直接调用Java的类库，例如System.out.println("Hello")
- 特殊需要引入的Java类库需要import

```scala
/*
  object: 关键字，声明一个单例对象(伴生对象)
 */
object HelloWorld {
    /*
      main 方法：从外部可以字节调用执行的方法
      def 方法名称(参数名称: 参数类型): 返回值类型 = { 方法体 }
      [] 表示泛型
     */
  def main(args: Array[String]): Unit = {
    println("hello world")
    System.out.println("hello scala")
  }
}
```

定义一个等价类区分Scala和Java
- 名称必须一样且在同一个文件中
```scala

class Student(name: String, age: Int) {
  def printInfo(): Unit = {
    println(name + " " + age + " " + Student.school)
  }
}

// 伴生对象
object Student{
  val school: String = "Uni"

  def main(args: Array[String]): Unit = {
    val alice = new Student("alice", 20)
    val bob = new Student("Bob", 23)
    alice.printInfo()
    bob.printInfo()
  }
}
```

```java
public class Student {
    private String name;
    private Integer age;
    private static String school = "Uni";

    public Student(String name, Integer age) {
        this.name = name;
        this.age = age;
    }

    public void printInfo() {
        System.out.println(this.name + " " + this.age + " " + Student.school);
    }

    public static void main(String[] args) {
        Student alice = new Student("alice", 20);
        Student bob = new Student("bob", 23);
        alice.printInfo();
        bob.printInfo();
    }
}
```
Scala库源码与API文档：
- ctrl+点击scala代码
- https://www.scala-lang.org/
- 下载Scala安装包离线查看

# 变量和数据类型
注释：（使用方法和Java完全一样）
- 单行注释: `//`
- 多行注释： `/**/`
- 文档注释： `/** */`

```scala
/*
  多行注释
 */

object Comment {
  /**
   * 文档注释
   * @param args 外部传入参数
   */
  def main(args: Array[String]): Unit = {
    // 单行注释
    println("hello")
  }
}
```

代码规范
- 使用`Tab`操作，实现整体向右缩进，用`shift+Tab`实现整体向左移动
- 使用`ctrl+shift+L`实现代码格式化
- 运算符两侧各加一个空格
- 一行最长不超过80个字符，超过使用换行

变量和常量
Java变量和常量语法
```java
变量类型 变量名称 = 初始值         int a = 10
final 常量类型 常量名称 = 初始值   final int b = 10  
```
Scala变量和常量
```scala
var 变量名 [:变量类型] = 初始值    var i:Int = 10
val 常量名 [:常量类型] = 初始值    val j:Int = 20
// 能用常量的地方不用变量
```

案例：
```scala
package chapter01

class Student(var name: String, var age: Int) {
  def printInfo(): Unit = {
    println(name + " " + age + " " + Student.school)
  }
}

// 伴生对象
object Student{
  val school: String = "Uni"
}
```

```scala
package chapter02

import chapter01.Student

object Test02_Variable {
  def main(args: Array[String]): Unit = {
    // 声明一个变量通用语法
    var a: Int = 10
    // 声明变量时，类型可以省略，编译器自动推导
    var a1 = 10
    val b1 = 20
    // 类型确定后，就不能修改，说明Scala是强数据类型语言
    var a2 = 15 // a2类型为Int
    // a2 = "ABC"
    // 变量声明时，必须要有初始值
    // var a3: Int
    // 声明/定义一个变量时，可以使用var或者val来修饰，var为变量，val为常量
    a1 = 12
    // b1 = 23 不合法

    var alice = new Student("alice", 20)
    alice = new Student("alice", 20)
    alice = null
    // 集合数据类型里可以修改
    val bob = new Student("bob", 23)
    bob.age = 24
    bob.printInfo()
  }
}
```
