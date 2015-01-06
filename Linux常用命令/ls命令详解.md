ls命令详解

|  选项      |   解读      |
|------------|-------------|
| **语法**       | ls [options] [pathname-list]|
| **用途**       | 显示目录内的文件名 和 “pathname-list”中指定的文件名|
| **输出**       | “pathname-list”指定目录下的文件和目录名，如果"pathname-list"中指定了文件名，则只输出该文件名|
| **-F**         | 在显示的目录名称后面加** / **，在可执行二进制文件名后面加上符号** * **, 在符号连接名后面加上 ** @ **|
| **-a**         | 显示所有的文件名，包括隐藏文件、.、..等等|
| **-i**         | 显示inode号|
| **-l**         | 显示详细信息，包括访问权限、连接数、所有者、组、文件大小（以字节计）和修改时间



Demo:

    ➜  bin  find . -name "deepin-*"|xargs ls -l -F -i
    786671 lrwxrwxrwx 1 root root      44  1月  3 14:27 ./deepin-boot-maker -> /opt/deepin-boot-maker/bin/deepin-boot-maker*
    786672 -rwxr-xr-x 1 root root   11906  1月  3 14:27 ./deepin-bug-reporter*
    786673 -rwxr-xr-x 1 root root   22204  1月  3 14:27 ./deepin-dialog*
    786677 lrwxrwxrwx 1 root root      29  1月  3 14:27 ./deepin-movie -> ../share/deepin-movie/main.py*
    786678 lrwxrwxrwx 1 root root      33  1月  3 14:27 ./deepin-music-player -> ../share/deepin-music/src/main.py*
    786679 -rwxr-xr-x 1 root root 1444436  1月  3 14:27 ./deepin-nautilus-properties*
    786680 lrwxrwxrwx 1 root root      44  1月  3 14:27 ./deepin-screenshot -> ../share/deepin-screenshot/src/screenshot.py*
    786681 lrwxrwxrwx 1 root root      42  1月  3 14:27 ./deepin-software-center -> ../share/deepin-software-center/ui/main.py*
    786682 lrwxrwxrwx 1 root root      55  1月  3 14:27 ./deepin-software-center-backend.py -> ../share/deepin-software-center/pkg_manager/apt/main.py*
    786683 lrwxrwxrwx 1 root root      36  1月  3 14:27 ./deepin-terminal -> ../share/deepin-terminal/src/main.py*
    786684 lrwxrwxrwx 1 root root      38  1月  3 14:27 ./deepin-translator -> ../share/deepin-translator/src/main.py*
