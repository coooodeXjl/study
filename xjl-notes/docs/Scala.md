# 1.GETTING STARTED WITH SCALA IN INTELLIJ

详细内容可访问 <a href="https://www.scala-lang.org/download/" target="_blank">Scala 官网</a>

The most popular way to get Scala is either using Scala through sbt, the Scala build tool, or to use Scala through an IDE.

我选择了 use Scala through an IDE

## 1.1.First, make sure you have the Java 8 JDK installed.

To check, open the terminal and type:

```
Java -version
```
(Make sure you have version 1.8.)

(If you don't have it installed, <a href="https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html" target="_blank">download Java here</a>.)

## 1.2.Then, install Scala:

...either by installing an IDE such as IntelliJ, or sbt, Scala's build tool.

我选择在 idea 中安装插件并在 idea 中下载 Scala 2.12.8

File-->settings-->Plguins-->Browse repositories-->输入 Scala-->选择 Scala 安装

<div align="center"> <img src="../xjl-notes/docs/pics/scala/0.png" width="1000px"/> </div><br>

## 1.3.Creating the Project

1. Open up IntelliJ and click **File** => **New** => **Project**

2. On the left panel, select Scala. On the right panel, select IDEA.

3. Name the project **HelloWorld**

4. Assuming this is your first time creating a Scala project with IntelliJ, you’ll need to install a Scala SDK. To the right of the Scala SDK field, click the **Create** button.

5. Select the highest version number (e.g. 2.12.8) and click **Download**. This might take a few minutes but subsequent projects can use the same SDK.

6. Once the SDK is created and you’re back to the “New Project” window click **Finish**.

<div align="center"> <img src="../xjl-notes/docs/pics/scala/1.png" width="1000px"/> </div><br>

## 1.4.Writing code

1. On the **Project** pane on the left, right-click src and select **New** => **Scala class**.

2. Name the class Hello and change the **Kind** to object.

3. Change the code in the class to the following:

```
object Hello extends App {
  println("Hello, World!")
}
```

Right click on Hello in your code and select Run ‘Hello’.

<div align="center"> <img src="../xjl-notes/docs/pics/scala/2.png" width="1000px"/> </div><br>


# 2.Scala 语法 （对比于 Java 语法不同处）






