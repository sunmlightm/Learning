# # Linux-PLAY
- dpkg -i **.deb
- sudo apt-get -f install
- Root权限运行文件管理sudo nautilus
- tar -zxvf +文件名 解压
#### 命令
- 打开终端：ctrl+alt+t
    - 关闭：ctrl+d/exit
    - 共用窗口打开：ctrl+shift+t
- 基本操作
    - 查看当前目录：pwd
    - 列出当前下的目录或文件：ls(也是一个程序 在/bin)
    - 跳转到根目录：cd /
    - 查看命令在哪个位置:which **
    - 切换到home目录:cd或者cd ~
    - Ctrl+c停止运行
    - 清屏:Ctrl+l或clear(假清屏) 彻底清屏:reset
    - history:查看之前的命令,使用!+命令编号执行目标命令
    - tab:补全
    - Ctrl+shift+ + 调大控制台文字 /减小:Ctrl+ -
    - alt+1,alt+2切换控制台
    - 回到上级目录:cd ..
#### 文件操作
    - 创建文件夹:mkdir +name
    - 创建文件:touch +name+后缀
    - ls:列出所有文件
        - ls -a列出所有文件(包含隐藏文件)
        - ls -l以列表方式列出
        - ls -l -h列表列出并且显示大小
        - 简写:ls -alh
    - 创建递归目录: mkdir a/b/c -p
    - 递归删除空文件夹 rmdir a/b -p
    - 删除文件夹下所有文件:sudo rm * -r

- 用户,组
    - 切换到root账户:sudo -s
    - cd -	可进入上次所在的目录
    - cd .	切换到当前目录
- 输出重定向:
    - ">"覆盖写入  ls bin > texe.txt
    - ">>"追加写入
- 管道命令 | :cat text.txt | more
- more :分屏显示,f下一屏,b上一屏,q退出 more text.txt
- cat 把文件在终端上全部显示:cat text.txt
    - 可以一次性打开多个 cat 1.txt 2.txt 3.txt
    - tac内容倒置
- head -n 文件 读取n行
- 多条命令使用";"链接
- 绝对路径,相对路径:
    - 绝对路径以/根目录开始
    - 相对路径cd..切换到上级目录
- **grep**文本中搜索---grep -参数 "要搜索的字符" 目标文件
    - -n	显示匹配行及行号
    - -v	显示不包含匹配文本的所有行（相当于求反）
    - -i	忽略大小写
- **拷贝文件**:
    - -r	若给出的源文件是目录文件，则cp将递归复制该目录下的所有子目录和文件，目标文件必须为一个目录名。
    - -v	显示拷贝进度
    - -i	交互式复制，在覆盖目标文件之前将给出提示要求用户确认
    - -a	该选项通常在复制目录时使用，它保留链接、文件属性，并递归地复制目录，简单而言，保持文件原有属性。
    - -f	已经存在的目标文件而不提示
    - **cp -r 01/ ./02**把当前目录下01拷贝进02
- **mv** 移动文件和目录
    - mv 01/02:如果02目录不存在,会把01改为02.  如果02是文件,会报错, 如果02是目录,则移动成功
    - -f	禁止交互式操作，如有覆盖也不会给出提示
    - -i	确认交互方式操作，如果mv操作将导致对已存在的目标文件的覆盖，系统会询问是否重写，要求用户回答以避免误覆盖文件
    - -v	显示移动进度
- **find** 查找文件
    - find ./ -name test.sh	查找当前目录下所有名为test.sh的文件
    - find ./ -name '*.sh'	查找当前目录下所有后缀为.sh的文件
    - find ./ -name "[A-Z]*"	查找当前目录下所有以大写字母开头的文件
    - find /tmp -size 2M	查找在/tmp 目录下等于2M的文件
    - find ./ -size +4k -size -5M	查找当前目录下大于4k，小于5M的文件
    - find ./ -perm 0777	查找当前目录下权限为 777 的文件或目录（说明：777权限指的是当前用户可以对相应的文件进行读取、写入和执行的操作）



<!--20180413-->


- 创建链接：
    - 创建软链接：ln -s 源文件 链接名
    - 创建硬链接：ln 源文件 链接名

#### 归档管理
   - tar使用格式: tar [参数] 打包文件名 文件
        - c	生成档案文件，创建打包文件
        - v	列出归档解档的详细过程，显示进度
        - f	指定档案文件名称，f后面一定是.tar文件，所以必须放选项最后
        - t	列出档案中包含的文件
        - x	解开档案文件

    - **打包文件**成.tar后缀：tar -cvf test.tar *
    - 解压.tar文件：tar -xvf test.tar 
    - **解压到指定目录**：：tar -xvf test.tar -C 目标文件夹
    - 把后缀是.txt文件压缩成xxx.tar.gz命令：tar -zcvf xxx.tar.gz *.txt
    - 把xxx.tar.gz文件解压命令：tar -zxvf xxx.tar.gz 
    - 把后缀.txt所有文件打包压缩成 test.tar.bz2命令：tar -jcvf test.tar.bz2 *.txt
    - 
    - gzip  [选项]  被压缩文件
        - d	解压
        - r	压缩所有子目录 >>tar.gz
    - zip、unzip文件压缩解压
        - 压缩文件：zip [-r] 目标文件(没有扩展名) 源文件
        - 解压文件：unzip -d 解压后目录文件 压缩文件
        
#### 系统管理：
- 进程管理：ps默认是当前终端开的进程数量
    - a	显示终端上的所有进程，包括其他用户的进程
    - u	显示进程的详细状态
    - x	显示没有控制终端的进程
    - w	显示加宽，以便显示更多的信息
    - r	只显示正在运行的进程
    - 一般使用ps -aux
- top动态显示进程
    - shift+M	根据内存使用量来排序
    - P	根据CPU占有率来排序
    - T	根据进程运行时间的长短来排序
    - K	可以根据后面输入的PID来杀死进程。
    - q	退出
    - 两秒更新一次top -d 2 
- kill终止进程：kill [-signal] pid
    - Kill -9 9133 强制杀死进程号为9133的进程
    - 强制删除 -9 普通删除不加数字
- reboot		重新启动操作系统
- shutdown –r now		重新启动操作系统，shutdown会给别的用户提示
- shutdown -h now		立刻关机，其中now相当于时间为0的状态
- shutdown -h 20:25		系统在今天的20:25 会关机
- shutdown -h +10		系统再过十分钟后自动关机
- df检测磁盘空间：
    - -a	显示所有文件系统的磁盘使用情况
    - -m	以1024字节为单位显示
    - -t	显示各指定文件系统的磁盘空间使用情况
    - -T	显示文件系统
- du检测目录所占磁盘空间：
    - -a	递归显示指定目录中各文件和子目录中文件占用的数据块
    - -s	显示指定文件或目录占用的数据块
    - -b	以字节为单位显示磁盘占用情况
    - -l	计算所有文件大小，对硬链接文件计算多次
    - -h转换单位
- 查看ip：linux：ifconfig---windows：ipconfig

- 查看时间日期：
    - cal
    - 显示某年： cal -y 2018
    - date ： date '+%y,%m,%d,%H,%M,%S'

- 用户管理：
    - 查看用户 whoami
    - who
    - cat /etc/passwd查看系统用户信息
    - useradd添加用户账号：useradd username -m（-m：自动创建home目录）
    - sudo useradd -d /home/test test -g lisi -m:创建test用户，home位于/home/test,隶属于lisi组
    - 修改密码：sudo passwd + username
    - userdel 删除用户
        - userdel abc(用户名)	删除abc用户，但不会自动删除用户的主目录
        - userdel -r abc(用户名)	删除用户，同时删除用户的家目录
    - 删除一个登录过的用户：
        - sudo vim /etc/passwd   --->找到要删除的账号，删除这一行配置信息
        - 删除家目录：sudo rm 要删除的账号
    - 切换用户： su 用户--->提示输入密码
    - id 用户名：查看用户是否存在
- 用户组管理：
    - 查看用户组：1.cat /etc/group  2.groups+tab两次    3.groupmod+tab两次
    - 添加删除组:
        - 添加一个组:sudo groupadd name
        - 删除组:sudo groupdel name
    - 查看某用户在哪个组:groups username
    - 修改账号的用户组:(sudo) usermod -g 用户组 用户名
    - 将普通用户添加到sudo组: sudo usermod -a -G sudo username
    - 将用户从某个组移除: sudo gpasswd 组名 -d username


#### 文件管理

- chgrp 修改文件所属组: sudo charp 组名 文件名
- chown 修改文件所有者: sudo chown 所有者 文件名
- chmod(重点):chmod u/g/o/a +/-/= rwx 文件名(sudo chmod u+x test.txt)
    - u	user 表示该文件的所有者
    - g	group 表示与该文件的所有者属于同一组( group )者，即用户组
    - o	other 表示其他以外的人
    - a	all 表示这三者皆是
    - 
    - +增加权限/ -撤销权限/=设定权限
    - 
    - r可读/w可写/x可执行
    - 数字法: r--4/w--2/ x--1 -->6:rw/5:rx/7:rwx---sudo chmod 777 1.txt(777:ugo)













#### 实例:
   
    6.用户管理
    1.查看当前用户： whoami
    2.查看系统有哪些用户：cat /etc/passwd
    3.查看有哪些组三种方式： cat /etc/group 和groups + tab（两次）,groupmod
    --------------------------------------
    4.useradd添加用户账号
    创建zhansan用户自动创建家目录： sudo useradd zhangsan -m
    切换到zhangsan这个用户： su zhangsan
    使用passwd设置和修改用户zhangsan密码: sudo passwd zhangsan
    --------------------------------------------
    5.userdel删除用户
    删除lisi这个用户并且删除家目录： sudo /etc/passwd 删除用户那一行,sudo rm /home/lisi -r
    6. su切换用户
    切换到test用户： su test
    退出使用： exit
     ---------------------------------------
    7.用户组管理
    2.groupadd、groupdel添加、删除组
    添加一个haha组： 
    删除hahha组： 
    sudo groupadd 123
    sudo groupdel 123
    查看某个账号atguigu在那个组： groups atguigu
    usermod修改用户所在组
    把账号test从test组修成abc组: sudo usermod -g abc test 
    把test账号从abc组修改成test组： sudo usermod -g test test
    普通用户test添加到sudo组命令： sudo usermod -a -G sudo test
    gpasswd把账号test从某组sudo移除: sudo gpasswd sudo -d test
    ------------------------------------
    8 .文件管理
     chgrp修改文件所属组
     例如把1.txt修改成属于test组： sudo chgrp test 1.txt
     chown 修改文件所有者
     例如把1.txt拥有者atguigu修改成test这个账号： sudo chown test 1.txt
    使用字母法和数字法把1.txt修改成拥有者和组可读可写可执行，但是其他用户一点权限也没有
    字母法命令：sudo chown u=rwx,g=rwx,o-rwx 1.txt
    数字法命令：sudo chmod 770 1.txt
    
    
#### 操作
    
    2.进程管理-（10分）
     2.1列出所有的进程ps -aux
     
     2.2杀死进程: Kill -9 9133
    3.ifconfig查看或配置网卡信息 -（10分）
    3.1检查两台电脑是否可以通信，是否连接
       
     
    4.用户管理-（10分）
    4.1查看有哪些用户cat /etc/passwd
     
    4.2判断用户是否存groups sunml
     
    4.3添加test的用户，并且自动创建家目录（这个家目录和账号一样）: sudo useradd test -m
    4.4切换进入到test账号 先使用sudo passwd test创建密码然后su test
     
    4.5如何使用普通账号test切换到root账号sudo -s
     
    4.6删除登录过的用户test用户或者abc账号（含家目录）
    sudo vim /etc/passwd删除账号然后sudo rm /home/test删除账号家目录 
    5.用户组管理-（10分）
    5.1添加和删除用户组sudo groupadd 123/sudo groupdel 123
    5.2把	用户添加到atguigu这个组
    sudo usermod -g atguigu test
     
    6. 用户和权限管理应用-（10分）
    
    1.	创建一个文件 test.txt，修改其权限为 拥有者有者可读可写，其他人没有任何权限。请使用字母法和数字法两种方式。
     字母法命令：sudo chown u=rwx,g=rwx,o-rwx 1.txt
    数字法命令：sudo chmod 770 1.txt
     
    2.创建一个叫xiaohua的用户，然后创建一个新的用户组叫meinv，并将xiaohua用户添加到meinv这个用户组中，然后创
    建一个新的文件，名字叫123.py，并修它的用户组为meinv。
    sudo useradd xiaohua
    sudo groupadd meinv
    sudo usermod -g meinv xiaohua
    sudo chgrp meinv 123.py
     
     
    3.创建一个文件a.txt，里面随便写点内容，修改文件权限为拥有者和用户组和其他用户都可读可写可执行，请用数字法
    sudo chmod 777 a.txt
     
    7. sublime编辑器-（10分）
     代码向右移动，tab 再向左移动shift+tab
     创建html_root_dir变量，快捷键变成大写:shift+ku
     html_ROOt_diR变量,快捷键变成小写shift+kl
     把文件中的某个内容全部替换ctrl+h
     
     整行删除快捷键
    ctrl+shift+k
    8. 假如当前目录下有一个叫test.py文件-（10分）
    1.打开文件命令：vi test.py -->命令模式-->插入模式（i）
    
     命令模式--->插入(编辑)模式：esc
     从当前光标的前一个字母插入i
     从当前光标所在行首插入I
     从当前光标后的一个字母插入a
     从当前光标所在行的行末插入A
     从当前光标所在行的下方开辟新的一行插入o
     从当前光标所在行的上方开辟新的一行插入O
    
     命令模式-->末行模式(Shift+;)：
     存盘退出的两种方式wq/x
     不存盘，强制退出q!
     放弃所有修改，从上次保存文件开始再编辑 e!
    
    2.从英文输入法转换中文输入法shift
    3.复制和粘贴多行和单行yy / n yy---粘贴:p
    3.剪切和粘贴多行个单行n dd p/ dd p
    5.往右缩进和往左缩进 shift+<< shift+>>
    6.撤销 u 
    7.删除一行 dd
    8.反撤销 ctrl + r
    9.光标移动到屏幕最后一行行首 L
    10.移动到指定行n shift+g
    11.光标移动文件开头 gg
    12.直接到文件最后一行行首shift+g

