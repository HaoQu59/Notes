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
- Maven项目默认用Java写，在`main`目录下新建目录`scala`，然后将该目录标记为Source Root
