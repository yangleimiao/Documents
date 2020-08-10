> 参考：https://www.cnblogs.com/chiangchou/p/idea-debug.html#_label0













![debug](.\debug.png)







![debug2](.\debug2.png)

Show Execution Point (Alt + F10)：如果你的光标在其它行或其它页面，点击这个按钮可跳转到当前代码执行的行

Step Over（F8）：步过，一行一行往下走，不进入方法

Step Into（F7）：步入，如果当前行有方法，进入方法内部，一般用于进入自定义方法

Force Step Into（Alt + Shift + F7）：强制步入，能进入任何方法，查看底层源码的时候可以用于进入官方类库的方法

Step Out（Shift + F8）：步出，从步入的方法内退出到方法调用处，此时方法已执行完毕，只是还没完成赋值

Run to Cursor（Alt + F9）：运行到光标处，可以将光标定位到你需要查看的那行，使用这个功能，代码会运行到光标处，不需要打断点











***



`ctrl + 左键 ` 跳入方法内部

`ctrl + alt + 左键 ` 跳转至实现类

` ctrl + H ` 可以打开类的继承层级面板

选中接口名称，按 ` ctrl + alt + 左键(B) ` 也可以展示继承类关系



右键，选择 ` Diagrams > Show Diagram... ` 可以打开类的继承图



查看类结构：` view -> Tool Windows -> Structure` ，也可以使用 ` Alt + 7 ` 调出这个面板







