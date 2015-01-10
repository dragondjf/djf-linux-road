Linux下文件安全之权限管理
=========
####1. 基于访问权限的文件保护机制
建立防止未授权的用户访问其他用户文件的访问机制，作为文件的所有者可以设置特定的访问权限来限制哪些用户可以对该文件进行何种操作。这种策略是建立在Linux系统用户的分类、访问权限的分类和访问操作的分类的基础之上的。

####2.用户分类
Linux系统中的每个用户都必须属于某一个组，这在系统管理员创建账号的时候必须确定。
一个用户可以属于多个组，但是通常情况下，一个用户只属于某一个组。
> 系统中所有用户组的信息以及该组的用户记录都存在`/etc/group`文件下，在这个文件中，每个组占一行，每行后面列出的是该组中的用户名。



>所有的Linux系统中都有一个特殊用户，可以访问系统中的所有文件，而不论这个文件的访问权限是什么。这个用户通常被称为超级用户，是计算机的管理者。这个超级用户的用户名是root, 用户ID是0.

####3. 文件操作/访问权限的分类

在Linux系统中文件拥有3种访问权限：读（r）,写（w）和 执行（x）
> 
+ 读：允许用户读取这个文件
+ 写：允许用户修改或删除这个文件
+ 执行：允许用户运行这个文件

但是在Linux下目录也是文件，对目录而言：
>  
+ 读：读取特权意味着可以读出这个目录的内容，即可以使用 **`ls`** 命令来列出这个目录下的所有内容
+ 写：写特权意味着可以在这个目录下新建或者删除一个目录项
+ 执行： 执行特权意味着可以搜索这个目录

Linux的用户类型为：User(u), Group(g), Others(o), 对每个文件，每类用户都可以设置其rwx访问权限。也可以使用八进制数值000-777来表示

例如 
            
            rwxrwxrwx  111111111 表示用户权限数值为 777
            rwxrwx---  111111000 表示用户权限数值为 770
            rwx------  111000000 表示用户权限数值为 700
            
            其中 '-' 表示 数字'0' 

####4. 读取和更改文件的访问权限
可以使用ls -l 或 -ld 来显示文件或目录的访问权限

+ ls -l [文件列表]  在屏幕上显示当前目录下的文件和目录列表，如果参数[文件列表]中包含目录则列出目录下的文件
+ ls -ld [目录列表] 显示参数[目录列表]中指定目录下的所有目录列表


        ➜  ~  ls -l -F  PFramer
        总用量 76
        drwxrwxr-x 2 djf djf 4096  1月  4 21:32 config/
        drwxrwxr-x 2 djf djf 4096  1月  4 21:34 database/
        drwxrwxr-x 8 djf djf 4096  1月  4 22:14 gui/
        drwxrwxr-x 2 djf djf 4096  1月  4 21:34 log/
        -rw-rw-r-- 1 djf djf  792  1月  4 21:58 main.py
        -rw-rw-r-- 1 djf djf  405  1月  4 21:32 Makefile
        -rw-rw-r-- 1 djf djf  464  1月  4 21:32 makemac.sh
        drwxrwxr-x 2 djf djf 4096  1月  4 21:32 objbrowser/
        drwxrwxr-x 6 djf djf 4096  1月  4 22:30 qframer/
        -rw-rw-r-- 1 djf djf  368  1月  4 21:32 README.md
        drwxrwxr-x 4 djf djf 4096  1月  4 21:32 rpcplugins/
        -rw-rw-r-- 1 djf djf 1978  1月  4 21:32 settings.py
        -rw-rw-r-- 1 djf djf  522  1月  4 21:34 settings.pyc
        -rw-rw-r-- 1 djf djf 2804  1月  4 21:32 setupmac.py
        -rw-rw-r-- 1 djf djf 9358  1月  4 21:32 setupwin.py
        drwxrwxr-x 4 djf djf 4096  1月  4 22:05 test/
        drwxrwxr-x 2 djf djf 4096  1月  4 21:32 util/

其中第一字母为 `d` 的为目录，为 `-` 的为文件

####5. 改变文件访问权限
可以使用 `chmod` 命令来改变文件的访问权限，基本用法：

+ chmod [options] octal-mode file-list
+ chmod [options] symbolic-mode file-list

其中file-list代表需要改变的文件或目录，octal-mode表示八进制模式 symbolic-mode表示符号模式

常用参数：
+ -R 递归修改或设置文件，目录或子目录的访问权限
+ -f 强制改变文件访问特权, 如果是文件的拥有者，则得不到任何的错误信息

例如：

    ➜  test  chmod a=rwx foo
    ➜  test  ls -l foo
    -rwxrwxrwx 1 djf djf 0  1月 10 21:16 foo
    ➜  test  chmod a=rx foo 
    ➜  test  ls -l foo     
    -r-xr-xr-x 1 djf djf 0  1月 10 21:16 foo

    ➜  test  chmod 000 foo
    ➜  test  ls -l foo
    ---------- 1 djf djf 0  1月 10 21:16 foo
    ➜  test  chmod 777 foo
    ➜  test  ls -l foo    
    -rwxrwxrwx 1 djf djf 0  1月 10 21:16 foo

####6. 默认的文件访问特权

当创建一个文件或者目录时候，Linux会根据 umask 命令的参数来设定新文件或者目录的访问特权
命令umask的参数表示文件权限的掩码, 用八进制表示，掩码为1的位表示该文件特权被关闭。

> 
文件的默认访问权限 = 默认的访问权限 - 掩码

直接输入umask 可以查看当前系统设定的掩码，也就知道新建文件或者目录的访问权限

默认访问权限：
+ 目录，可执行文件，符号连接的默认访问权限为 777
+ 普通文件的默认访问 666    


        ➜  test  umask 
        002   
        ➜  test  touch foo   
        ➜  test  ls -l foo    
        -rw-rw-r-- 1 djf djf 0  1月 10 22:36 foo   
        ➜  test  mkdir dfoo    
        ➜  test  ls -ld dfoo     
        drwxrwxr-x 2 djf djf 4096  1月 10 22:36 dfoo

对foo文件而言 权限为 666 - 002 = 664 对应的符号表示-rw-rw-r--
对dfoo目录，权限为 777 - 002 = 755   对应的符号标识rwxrwxr-x


> 
umask 命令通常存放在系统启动文件 ~/.profile 或 ~/.login 或 ~/etc/profile 中。

