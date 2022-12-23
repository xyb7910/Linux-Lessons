

# Tmux

## 会话与进程

命令行的典型使用方式是，打开一个终端窗口（terminal window，以下简称"窗口"），在里面输入命令。**用户与计算机的这种临时的交互，称为一次"会话"（session）** 。

会话的一个重要特点是，窗口与其中启动的进程是连在一起的。打开窗口，会话开始；关闭窗口，会话结束，会话内部的进程也会随之终止，不管有没有运行完。

一个典型的例子就是，SSH 登录远程计算机，打开一个远程窗口执行命令。这时，网络突然断线，再次登录的时候，是找不回上一次执行的命令的。因为上一次 SSH 会话已经终止了，里面的进程也随之消失了。

为了解决这个问题，会话与窗口可以"解绑"：窗口关闭时，会话并不终止，而是继续运行，等到以后需要的时候，再让会话"绑定"其他窗口。



## 作用

   **Tmux 就是会话与窗口的"解绑"工具，将它们彻底分离。**

> （1）它允许在单个窗口中，同时访问多个会话。这对于同时运行多个命令行程序很有用。
>
> （2） 它可以让新窗口"接入"已经存在的会话。
>
> （3）它允许每个会话有多个连接窗口，因此可以多人实时共享会话。
>
> （4）它还支持窗口任意的垂直和水平拆分。



## 安装

Tmux 一般需要自己安装。

> ```bash
> # Ubuntu 或 Debian
> $ sudo apt-get install tmux
> 
> # CentOS 或 Fedora
> $ sudo yum install tmux
> 
> # Mac
> $ brew install tmux
> ```



### 启动与退出

安装完成后，键入`tmux`命令，就进入了 Tmux 窗口。

> ```bash
> $ tmux
> ```

上面命令会启动 Tmux 窗口，底部有一个状态栏。状态栏的左侧是窗口信息（编号和名称），右侧是系统信息。

![img](https://www.wangbase.com/blogimg/asset/201910/bg2019102006.png)

按下`Ctrl+d`或者显式输入`exit`命令，就可以退出 Tmux 窗口。

> ```bash
> $ exit
> ```



## 前缀键

Tmux 窗口有大量的快捷键。所有快捷键都要通过前缀键唤起。默认的前缀键是`Ctrl+b`，即先按下`Ctrl+b`，快捷键才会生效。

举例来说，帮助命令的快捷键是`Ctrl+b ?`。它的用法是，在 Tmux 窗口中，先按下`Ctrl+b`，再按下`?`，就会显示帮助信息。

然后，按下 ESC 键或`q`键，就可以退出帮助。



## 结构

​    一个tmux可以包含多个`session`，一个`session`可以包含多个`window`，一个`window`可以包含多个`pane`。



## 实例

```c
        tmux:
            session 0:
                window 0:
                    pane 0
                    pane 1
                    pane 2
                    ...
                window 1
                window 2
                ...
            session 1
            session 2
            ...
```


## 操作

1. tmux：新建一个session，其中包含一个window，window中包含一个pane，pane里打开了一个shell对话框。
2. 按下`Ctrl + b`后手指松开，然后按%：将当前pane左右平分成两个pane。
3. 按下`Ctrl + b`后手指松开，然后按"（注意是双引号"）：将当前pane上下平分成两个pane。
4. `Ctrl + d`：关闭当前pane；如果当前window的所有pane均已关闭，则自动关闭window；如果当前session的所有window均已关闭，则自动关闭session。
5. 按下`ctrl + b`后手指松开，然后按方向键：选择相邻的pane。
6. 鼠标拖动pane之间的分割线，可以调整分割线的位置。
7. 按住`ctrl + b`的同时按方向键，可以调整pane之间分割线的位置。
8. 按下`ctrl + b`后手指松开，然后按`z`将当前pane全屏/取消全屏。
9. 按下`ctrl + b`后手指松开，然后按`d`挂起当前session。
10. `tmux a`：打开之前挂起的session。
11. 按下`ctrl + a`后手指松开，然后按s：选择其它session。
    -   方向键 —— 上：选择上一项 session/window/pane
    -   方向键 —— 下：选择下一项 session/window/pane
    -   方向键 —— 右：展开当前项 session/window
    -   方向键 —— 左：闭合当前项 session/window
12. 按下`Ctrl + b`后手指松开，然后按`c`在当前session中创建一个新的window。
13. 按下`Ctrl + b`后手指松开，然后按w：选择其他window，操作方法与(12)完全相同。
14. 按下`Ctrl + b`后手指松开，然后按PageUp：翻阅当前pane内的内容。
15. 鼠标滚轮：翻阅当前pane内的内容。
16. 在tmux中选中文本时，需要按住shift键。（仅支持Windows和Linux，不支持Mac，不过该操作并不是必须的，因此影响不大）
17. tmux中复制/粘贴文本的通用方式：
    - 按下`Ctrl + b`后松开手指，然后按`[`
    - 用鼠标选中文本，被选中的文本会被自动复制到tmux的剪贴板
    - 按下`Ctrl + b`后松开手指，然后按`]`，会将剪贴板中的内容粘贴到光标处



