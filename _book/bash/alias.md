# 设置bash自定义命令

由于工作需要，会频繁的用到命令行，有时候在用命令行创建一个文件之后，想打开这个文件进行编辑。通常的做法是：打开文件管理器，找到这个文件，然后双击打开。但是这种方式效率太低了。于是就想着是否在创建完文件之后，在命令行中就直接打开文件，于是找到了如下资料：

[资料原始地址](http://jasinyip.com/Linux/alias.html)

## alias 命令

alias 命令简单来说，就是将一些复杂繁琐的命令，简化成自定义的命令。语法如下：

- 查看当前的自定义命令列表
- 添加一条自定义命令：`alias {自定义指令名}='{具体指令}'`
- 删除一条自定义命令：`unalias {自定义指令名}`

举个例子：
在 Bash 中清屏的命令是 `clear`，如果我想用 `clr` 去代替，那么我就写 `alias clr='clear'`。
这时用 `alias` 可以看到刚才添加的自定义命令 `clr='clear'`。
执行 `clr`，成功清屏了，意味着命令执行成功。

## 输入参数

如果光光是去代替固定的命令，那就没什么意思啦，不过我们可以引入参数：

- `$@` 表示一个参数，命令中可以添加多个 `$@`，使用时按顺序输入。

## 实现 subl、chrome 命令

我使用的是 Windows 系统，Sublime Text 的路径是 `G:\Program Files\Sublime Text 2\sublime_text.exe`

输入命令：`alias sulb='"\G\Program Files\Sublime Text 2\sublime_text.exe" $@'`

现在，我们可以使用 `sulb .` 来打开当前目录了！

当然，chrome 命令同理。

## 实现 web 命令，用以 localhost 打开指定文件(或目录)

由于使用 php 较多，所以经常会使用到 `http://localhost/`来打开 php 文件。这个时候上面的 `chrome`就不能愉快地使用了。

由于 php 文件夹是固定的，我将所有项目都存放在这个 php 的目录中，路径是 `E:\www\`，所以如果我要执行 `E:\www\hello\index.php` 的话，访问地址应该为 `http://localhost/hello/index.php`。
访问地址与实际目录的区别就是 `hello` 前面那一个字符串，将之替换就好。

不过我使用的是另外的一个更简单方法，那就是先获取当前目录名，然后在前面添加 `http://localhost`就好。

我们会用到 `$PWD` 来获取当前路径，以及用 Shell 的字符串截取指令（相关资料：[Linux shell脚本的字符串截取](http://www.cnblogs.com/wangbin/archive/2011/10/11/2207179.html)）来获得最后一个 `/` 之后的字符串。

于是我们得到这样的一个东西：`${PWD##*www/}`

最后，使用 `alias` 命令：

`alias web='"F:\Program Files\Chrome\Application\chrome.exe" "http://localhost/${PWD##*/}/$@"'`

现在来使用 `web` 命令，就可以打开当前的目录所对应的访问地址了，如果后面添加参数的话，就可以打开指定的文件了~

## 重启后继续使用的方法

实际上，直接在命令行里使用 `alias`，仅仅可以应用于当前的会话，为了下次启动时不需要重新再写，我们应该把它写到 `~/.bashrc` 里。

1. 使用 vim 打开 .bashrc


1. 直接在里面添加你需要的 `alias` 命令，比如 `alias hi='echo hi'`
2. 保存，完成~

新技能 get 吧？哈哈

## 备份下自己的配置

```bash
alias sublime='"/d/SoftWare/SublimeText 3/sublime_text.exe" $@'
alias typora='"/d/SoftWare/Typora/bin/typora" $@'
alias web='"/c/Program Files (x86)/Google/Chrome/Application/chrome.exe" "http://localhost:4000/"'
```

