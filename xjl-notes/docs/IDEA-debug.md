# 1.设置断点

在需要进行调试的代码块处设置断点，在行号的区域后面单击鼠标左键即可

<div align="center"> <img src="../xjl-notes/docs/pics/debug/debug-0.png" width="1000px"/> </div><br>

# 2.开启调试会话

点击红色箭头指向的 debug 按钮，IDEA 自带 debug 或者 jrebel 插件的 debug 都可以，进入调试会话

<div align="center"> <img src="../xjl-notes/docs/pics/debug/debug-1.png" width="1000px"/> </div><br>

程序运行到所打断点处，下方弹出 IDEA debug 视图

1.调试程序停留的代码行

2.当前上下文变量及其值

<div align="center"> <img src="../xjl-notes/docs/pics/debug/debug-2.png" width="1000px"/> </div><br>

# 3.单步调试

## 3.1 Step Over

点击红色箭头指向的按钮 Step Over(F8) ，程序向下执行一行，如果当前行有方法调用，这个方法将被执行完毕返回，然后到下一行

<div align="center"> <img src="../xjl-notes/docs/pics/debug/debug-3.png" width="1000px"/> </div><br>

## 3.2 Step Into

点击红色箭头指向的按钮 Step Into(F7)，程序向下执行一行，如果该行有自定义方法，则运行进入自定义方法（不会进入官方类库的方法）

<div align="center"> <img src="../xjl-notes/docs/pics/debug/debug-4.png" width="1000px"/> </div><br>

## 3.3 Force Step Into 

点击红色箭头指向的按钮 Force Step Into(Alt+Shift+F7)，程序向下执行一行，该按钮能进入任何方法

<div align="center"> <img src="../xjl-notes/docs/pics/debug/debug-5.png" width="1000px"/> </div><br>

## 3.4 Step Out

点击红色箭头指向的按钮 Step Out(Shift+F8)，程序向下执行完该方法，返回到该方法被调用处的下一行语句，值得注意的是，该方法已执行完毕

<div align="center"> <img src="../xjl-notes/docs/pics/debug/debug-6.png" width="1000px"/> </div><br>

## 3.5 Drop frame

点击红色箭头指向的按钮 Drop frame，你将返回到当前方法的调用处，并且所有上下文变量的值也回到调用当前方法之前。

<div align="center"> <img src="../xjl-notes/docs/pics/debug/debug-7.png" width="1000px"/> </div><br>

> 暂时使用的功能就这些，还有更多的使用方法待续


# 参考资料

<a href="https://www.cnblogs.com/Bowu/p/4026117.html" target="_blank">Intellij IDEA调试功能使用总结</a>



