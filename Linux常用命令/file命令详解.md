####file 命令详解

|  选项      |   解读      |
|------------|-------------|
| **语法**       | file [options] file-list|
| **用途**       | 把 file-list 中的文件类型分类 |
| **输出**       | “file-list”指定文件类型依次列出|
| **-f File**    | 从文件File中读取要检测的文件 |

Demo

    file /*
    /bin:        directory 
    /boot:       directory 
    /cxassoc:    directory 
    /deepinhost: directory 
    /dev:        directory 
    /etc:        directory 
    /home:       directory 
    /initrd.img: symbolic link to `boot/initrd.img-3.13.0-43-generic' 
    /lib:        directory 
    /lost+found: directory 
    /media:      directory 
    /mnt:        directory 
    /opt:        directory 
    /proc:       directory 
    /root:       directory 
    /run:        directory 
    /sbin:       directory 
    /srv:        directory 
    /sys:        directory 
    /tmp:        sticky, directory 
    /usr:        directory 
    /var:        directory 
    /vmlinuz:    symbolic link to `boot/vmlinuz-3.13.0-43-generic' 
