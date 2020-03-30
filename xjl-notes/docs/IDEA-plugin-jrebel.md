# 1.环境配置

使用 idea IDE 进行项目热部署，首先需要安装 Jrebel 插件

## 1.1.安装JUnit插件步骤

File-->settings-->Plguins-->Browse repositories-->输入 JUnit-->选择 JUnit Generator V2.0 安装

<div align="center"> <img src="../xjl-notes/docs/pics/jrebel/0.png" width="1000px"/> </div><br>

## 1.2.由于这是款收费软件，破解方法就百度吧

# 2.运行项目

运行 Java 项目

1.选中运行类

2.点 Jrebel 插件提供的 Debug 按钮

3.一般都自动设置好自动编译触发的时机和时间，项目运行后，修改项目代码，代码界面失去焦距，Jrebel 自动编译

运行项目
<div align="center"> <img src="../xjl-notes/docs/pics/jrebel/1.png" width="1000px"/> </div><br>

Jrebel 成功启动
<div align="center"> <img src="../xjl-notes/docs/pics/jrebel/2.png" width="1000px"/> </div><br>

修改代码后，切换页面焦距，等几秒钟，Jrebel 自动编辑成功并提示修改代码的文件
<div align="center"> <img src="../xjl-notes/docs/pics/jrebel/3.png" width="1000px"/> </div><br>

> 运行 Tomcat 或者 Spring-boot 项目可能需要一些配置触发自动编译的条件