+++
date = "2015-12-19T13:21:10+08:00"
draft = true
title = "常用linux命令备忘"

+++
#### 什么是shell命令？

linux命令可以是四种：

- 是一个可执行程序，就像我们所看到的位于目录/usr/bin 中的文件一样。 属于这一类的程序，可以编译成二进制文件，诸如用 C 和 C++语言写成的程序, 也可以是由脚本语言写成的程序，比如说 shell，perl，python，ruby，等等。
- 是一个内建于 shell 自身的命令。bash 支持若干命令，内部叫做 shell 内部命令 (builtins)。例如，cd 命令，就是一个 shell 内部命令。
- 是一个 shell 函数。这些是小规模的 shell 脚本，它们混合到环境变量中。 在后续的章节里，我们将讨论配置环境变量以及书写 shell 函数。但是现在， 仅仅意识到它们的存在就可以了。
- 是一个命令别名。我们可以定义自己的命令，建立在其它命令之上。

#### 常用命令

type cmdname 查看cmdname的类型
which 查看可执行程序的路径（对其他的类型无效）：

        # which ls
        output: /usr/bin/ls

查看当前用户所在用户组
	`$groups`
第一个是有效用户组，如果要切换有效用户组：
修改/etc/passwd 中的gid：
	`angus:x:1000:4:angus:/home/angus:/bin/bash`
上面的第四个字段4 就是修改后的用户组（4是admin用户组的gid）；
useradd命令(在debian中建议使用adduser代替):
`# useradd [-u UID] [-g 初始群组] [-G 次要群组] [-mM] [-c 说明栏][-d 家目录绝对路径] [-s 使用哪个shell] 使用者账号名`

选项参数：

    -u ：后面接的是 UID ，是一组数字。直接挃定一个特定的 UID 给这个账号；
    -g ：该群组 GID 会被放置刡 /etc/passwd 第四个字段内。
    -G ：后面接的组名则是这个账号还可以加入的群组。选项不修改 /etc/group 内的相关资料
    -M ：强制不要建立家目录
    -m ：强制建立家目录，一般帐号默认是m，系统帐号默认是M
    -c ：这个就是 /etc/passwd 的第五栏的说明内容啦～可以随便我们添加的comments～
    -d ：指定家目录，务必使用绝对对路径！
    -r ：建立一个系统的账号，这个账号的 UID 会有限制 (参考 /etc/login.defs)
    -s ：指定一个shell，默认是bash。

最后，
`#passwd username`，给username用户添加一个密码，注意，root用户给其他用户增加、修改密码不是这个命令，而是
root ~# useradd -D查看useradd的默认的缺省值，example：
```
    mint ~ # useradd -D
    GROUP=100
    HOME=/home
    INACTIVE=-1
    EXPIRE=
    SHELL=/bin/sh
    SKEL=/etc/skel #这是基准目录，新建用户家目录的参数是从这里复制过去的，修改这个目录下文件后再新建用户的家目录都会复制过去。
    CREATE_MAIL_SPOOL=no
```
删除一个用户：`#userdel -r username `-r 表示连同家目录一起删除
用户参数修改 usermod ,其参数基本和useradd命令是一样。
命令chage是更改用户密码的过期信息
finger查询用户相关信息，很多bash默认没有安装
id 【username】用户的id信息
打包和解压功能：

##### 常用的三个功能(牢记)：
压缩： `tar -cjvf filename.tar.bz2 `要被压缩的文件名
查询： `tar -tjvf filename.tar.bz2`
解压： `tar -xjvf filename.tar.bz2 -C `指定解压到目录
```
    tar：c,t,x只能出现一个，j，z也只能出现一个
    -x：extract，解压
    -c：create a archive ，打包
    -t：查询一个压缩内容
    -f：要被处理的文档名，-f和其他参数分开，因为后面紧接文件名
    -v：verbose，list the content processed，
    -j：通过 bzip2 的支持进行压缩/解压缩，也有常用-z ，即gzip命令格式,此时后缀最好用tar.gz
```
rm：
```
    -f：force，不进行任何提示，慎重使用
    -r：remove recursive ，递归删除，文件夹里面有内容时必须使用这个参数
    -d：删除空目录
```
#### man
man命令的一些参数：man cmd后出现的man page第一行命令的旁边有一个（数字），这个数字是表示该命令的分类，如：
SHUTDOWN(8) Linux System Administrator’s Manual SHUTDOWN(8)
```
    代号 表示内容
    1 用户在 shell 环境中可以操作的指令或可执行文件
    2 系统核心可调用的函数或工具等
    3 一些常用的凼数(function)或凼式库(library)，大部分C的库(libc)
    4 装置档案的说明，通常在/dev 下的档案
    5 配置文件或者是某些档案的格式，/etc
    6 游戏(games)
    7 惯例与协议等，例如 Linux 文件系统、网络协议、 ASCII code 等等的说明
    8 系统管理员可用的管理指令，如shutdown
    9 跟 kernel 有关的文件
```
如果要搜索man page，利用 /string或?string 即可搜索，一个是向下搜索，一个是向上搜索。按n是下一个匹配的字符串，是不是和vim一样的呀！！！

terminal的快捷键：
`Ctrl + C`：这个是用来终止当前命令的快捷键，
`Tab`： 这个键是最有用的键了，也是笔者敲击概率最高的一个键。因为当你打一个命令打一半时，它会帮你补全的。不光是命令，当你打一个目录时，同样可以补全，不信你试试。
`Ctrl + D`： 退出当前终端，同样你也可以输入exit。
`Ctrl + Z`： 暂停当前进程，比如你正运行一个命令，突然觉得有点问题想暂停一下，就可以 使用这个快捷键。暂停后，可以使用fg 恢复它。
`Ctrl + L`： 清屏，使光标移动到第一行。
环境变量通常被放在~/.bashrc java maven 环境变量都配置在这里最好。
关于环境变量的重要文献：设置环境变量,英文

#### 关于gedit的警告问题：
有时使用gedit 编辑系统配置文件会出现警告，这是因为使用terminal启动graphical 程序是很不好的行为，应该使用gksudo，（需要先安装gksu程序），这样就不会有警告了。

常识：GNOME（使用Gtk+编写，gedit也是是用gtk+）是为了取代KDE（使用Qt图形工具库，Qt没有开源）桌面的一个项目。

sudo 临时切换到其他用户（默认root），以其他用户身份（如root）执行命令后退回当前用户身份，前提是在/etc/sudoers授权；sudo的配置文件是/etc/sudoers，用专用编辑工具visudo编辑，好处是新规则不符合规范时退出时会提醒。你可以通过sudo -l查看当前用户的sudo权限，
现在给一个普通用户xarch添加sudo授权：

    #visudo
    然后将光标移到最后一行 按a（append行末添加），回车，在最后一行加上 
    xarch ALL=(ALL) ALL

按Esc退出append模式，输入：wq保存退出。
退回到xarch用户，输入 sudo -l

