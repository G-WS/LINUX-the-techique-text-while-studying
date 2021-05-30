# linux

## 系统操作篇

### 常见目录介绍

/	根目录

/root	用户的家目录

/home/username	普通用户的家目录

/etc	配置文件目录

/bin	命令目录

/sbin	管理命令目录

/usr/bin/usr/sbin	系统预装的其他命令

init 3	打开练习环境（极简模式）

init 0	关机，正确的将练习模式关闭

### 万能的帮助命令

分别对应三种不同类型的帮助命令

Linux的基本操作方式是命令行，海量的命令不适合“死记硬背”，遇到陌生命令可以通过帮助命令进行查询

#### man	帮助

man是manual的缩写

man帮助用法演示

```shell
 man ls
```

man 【命令名称】默认为第一篇章

按q退回命令行终端

man也是一条命令，分为九章，可以使用man命令获得man命令的帮助

```shell
man 7 man
```

7是篇章号，man是命令

篇章：

1、commands	用户可以从shell运行命令//shell先理解为终端

2、System calls	系统调用

3、Library calls	库调用，函数获取帮助

4、special files	/dev)目录中的文件

5、File format and contentions	一些配置文件的格式及说明

6、Games	游戏

7、Macro packages and conventions	宏

8、System management commands	系统管理命令

9、废弃的篇章

篇章的作用是什么？

例如：passwd	进行用户密码设置的命令

​		   /etc/passwd	文件

```shell
man passwd#无法识别哪一种
man 1 passwd#对命令
man 5 passwd#对文件
```

查看命令有什么类型

```shell
man -a passwd
```

退出q	退出这个命令用ctrl+c

#### help	帮助

shell（命令解释器）自带的命令成为内部命令，看不到实体，其他的是外部命令

内部命令使用help 帮助

```sh
help cd
```

外部命令使用help 帮助

```sh
ls --help #正确
cd --help #错误，会显示无效
```

可以通过type 【命令】来区分命令是内部还是外部（还有别名功能）

```sh
type cd
```

#### info	帮助

info 帮助比help更详细，作为help的补充

但是info全是英文

```shell
info ls
```

### 一切皆文件

#### 文件查看/修改

ls	查看当前目录下的文件

通过ls命令可以查看文件的名称，权限，类型，修改时间等

ls 【选项，选项...】 参数 ...

常用参数

```sh
-l  #长格式显示文件
-a  #显示隐藏文件
-r  #逆序显示
-t	#按照时间顺序显示
-R	#递归显示
```

ls  【选项】 【文件...】//ls后可以接多个文件名

```sh
LS /root
ls /root /
```

注：命令和参数之间需要有空格，多个空格是允许的

长格式显示文件

```sh
ls -l .
ls -l
```

上面两者一样，.表示参数，代表的是当前目录，如果参数没写，则默认是当前目录。

长格式中，最左侧第一个字段的第一个字符代表的文件类型，

若为-，代表的是文件

若为d，代表的是目录（文件夹）

后面9个字符代表的是权限

第二个字段表示文件或文件夹的个数

第三个字段表示谁创建了这个文件（哪个用户）

第四个字段表示这个用户属于哪一个用户组

第五个字段表示文件的大小

第六个字段表示文件最后修改的时间

第七个字段表示文件名称

注: clear 或 ctrl+l 可以清屏

显示隐藏文件：

```sh
ls -a
```

防止普通用户误操作，故隐藏

逆序显示：

```sh
ls -r
```

经常和 -l 搭配使用

按照时间顺序显示：

```sh
ls -t
```

组合的两种写法：

```sh
ls -r -t -l
ls -rtl
```

递归显示：

```sh
ls -R
```

#### 目录文件的创建修改与删除

显示当前的目录

```shell
pwd
pwd -l #逻辑
pwd -p #物理
```

注：SYNOPSIS：n.总览

/ 与/ root是不同的目录

/ ：	根目录

/root：	是root用户的家目录

不同颜色代表不同的权限

#代表不受限

$代表普通用户，访问权限受限

通过下面命令可以在终端切换为root用户

```sh
su - root
```

注：su和sudo不是一个命令

执行上面命令后接着输入root用户的密码就可以切换到root用户

cd	更改当前操作目录

从根目录进入	绝对路径

从当前目录进入当前目录的下一级目录	相对路径

```sh
cd /path/to/...	#绝对路径
cd ./path/to/...	#相对路径
cd ../path/to/...	#相对路径
```

回到当前目录的上一级目录

```sh
cd ..
```

回到上次操作的目录

```sh
cd -
```

man 获取内置命令，获取的是命令解释器bash的帮助，内置命令应该使用help

```sh
help cd
```

当目录较长的时候可以用 tab 自动补全

由于使用ls进入目录太长，所以可以切换目录

```sh
ls /etc/sysconfig/network-scripts/
```

等价于

```sh
cd /etc/sysconfig/network-scripts/
ls
```

等价于

```sh
cd /etc
cd ./sysconfig/network-scripts/
#第二条语句也可以去掉./
cd sysconfig/network-scripts/
```

切换目录后可以使用pwd获取当前目录，查看是否成功切换目录

建立目录（新建文件夹）

mkdir 【选项】 【目录】...	//代表可以通过mkdir建立多个目录

在根目录下创建目录a

```sh
mkdir /a
```

在当前目录下创建目录a

```sh
mkdir ./a
mkdir a
```

注：绝对路径，相对路径

同时创建多个目录

```shell
mkdir b c d
```

若目录已经存在，会提示无法创建，文件已经存在

创建多级目录

```sh
mkdir /a
mkdir /a/b
mkdir /a/b/c
```

等价于

```sh
mkdir -p /a/b/c
```

可以通过ls -R /a命令来递归查看

```sh
ls -R /a/b/c
```

删除目录

rmdir	删除空目录

注：只能删除空白的目录

```shell
rmdir /a
```

执行上面语句会失败，因为虽然a目录下都是空目录，但是会被视为文件。体现了Linux系统中一切皆文件的特点。

rm -r	删除非空目录（必须带-r）

会逐级进行确认，输入y即可

若不想逐级确认（不去提示）

```sh
rm -r -f /a
```

```sh
rm -rf /a
```

错误写法：

```sh
rm -r -f / a
```

这样会不进行提示，直接删除根目录下的所有文件和目录，所以使用时需要反复进行确认。

#### 通配符

面对多个相似文件的操作

定义：shell	内建的符号

用途：操作多个相似（有简单规律）的文件

常用通配符

​	* 匹配任何字符串

​	? 匹配一个字符串

​	[xyz] 匹配xyz任意一个字符

​	[a-z] 匹配一个范围

​	[!xyz]或[ ^ xyz] 不匹配

建立测试

```sh
cd /tmp
touch filea fileb filec
mkdir dira dirb dirc -p	#有些命令支持选项写到文件后
cp -v file* /
touch fileaa fileabc
cp -v file* /
ls file*
cp file? /
ls file?
```

#### 文件操作

新建空白文件

touch命令创建空白文件

在根目录下创建空白文件filea

```sh
touch /filea
```

复制文件

cp命令复制文件和目录

复制目录

错误写法

```sh
cp /root/a /tmp
```

会报错，所以我们需要加上选项

正确写法：

```sh
cp -r /root/a /tmp
```

复制文件：

```sh
cp /filea /tmp
```

通过-v 命令可以显示复制的过程

```sh
cp -v /file /tmp
```

复制的时候，文件的属主有时候会发生变化，文件的时间一定会发生变化，如果不想让其发生变化，则使用cp -p命令

```sh
cp -p
```

-a命令等同于-dpR,相比于cp -p命令更为极端

```sh
cp -a
```

移动文件

mv：

1、重命名功能

2、文件和文件夹的移动功能

将filea改名为fileb

```sh
mv /filea /fileb
```

相当于在Linux底层进行了一次移动

将file移动到目录tmp中

```sh
mv /fileb /tmp
```

将tmp目录下的fileb移动到根目录下，并且改名为filec

```sh
mv /tmp/fileb /filec
```

对目录进行移动

```sh
mkdir /dirc
mv /dirc /tmp
```

面对相似的文件和目录时使用通配符

删除文件

```sh
rm -r	#删除目录（包括目录下的所有文件）
rm -f	#删除文件不进行提醒
```

注：rm命令可以删除多个目录，需谨慎使用

#### 文本内容查看

cat	文本内容显示到终端（文本非常长时，也会显示到终端）

cat	后面可以接多个文件

head	查看文件开头

tail	查看文件结尾

​	常见参数-f文件内容更新后，显示信息同步更新。

wc	统计文件内容信息

```shell
cat /tmp/demo   #demo为自建的样例文件
head /tmp/demo	#查看文件的开头（默认10行）
head -5 /tmp/demo	#产看文件开头（5行）
```

由于没有样例文件，也可以查看系统中的文件

```shell
cd /root
ls
cat anaconda-ks.cfg
tail /tmp/demo	#查看结尾，默认最后10行
tail -3 /tmp/demo	#产看文件最后的3行
tail -f /tmp/demo	#跟踪文件的更新
```

ctrl+c	停止

```sh
wc -l /tmp/demo	#可以查看文件有多少行
more /tmp/demo	#分行显示，可以按空格让其继续显示
less	#也是分行显示命令
```

tail  -f   主要用于日志文件//日志文件总是在刷新

### 打包与压缩

#### Linux的备份压缩（打包）

最早的Linux备份介质是磁带，使用的命令是tar

可以打包后的磁带文件进行压缩存储，压缩的命令是gzip和bzip2

经常使用的扩展名是	.tar.gz	.tar.bz2	.tgz

故在Linux中，将一个文件进行打包压缩有两步，1>打包  2>压缩

#### 打包命令

tar 打包命令

常用参数

c	打包

x	解包

f	指定操作类型为文件

压缩有两种形式	1 gzip

​							  2 bzip2

bz2和gz的区别：bz2 的执行时间慢于gz，压缩比例大于后者

可以通过ls -th命令进行比较

```sh
ls -th /tmp/etc-backup
```

互联网有时将.tar.gz写作.tgz,将/tar/bz写作.tbz2，将双扩展名扩展为单扩展名

eg：对Linux进行备份，备份etc，将etc目录打包成文件

```sh
ls /etc
tar cf /tmp/etc-backup.tar /etc #打包
ls -l /tmp/etc-backup.tar #查看文件大小
ls -th /tmp/etc-backup.tar #以相对较大的单位（例如M）为单位显示文件大小
```

如希望打包并压缩（加一个z选项）

打包成gz：

```shell
tar czf /tmp/etc-backup.tar.gz /etc
```

打包成bz2：

```sh
tar cjf /tmp/etc-backup.tar.bz2 /etc
```

将打包文件进行解包，并放在/root下	

```sh
tar xf /tmp/etc-backup.tar -C /root
```

注：c大写

解压缩：

```sh
zxf jxf
```

#### 压缩和解压缩

可以使用gzip和bzip2命令单独操作

通常和tar 命令配合操作

常用参数

```sh
tar -z gzip	#格式压缩和解压缩
tar -j bzip2	#格式邮政所和解压缩
```

### 强大的文本编辑器vi

#### 多模式文本编辑器

多模式产生的原因（多模式相较于记事本）

四种模式

​	正常模式（Normal-mode）

​	插入模式（Insert-mode）	:q退出  可以通过键盘完成一切操作，按i进行文本操作

​	命令模式（Command-mode）

​	可视模式（Visual-mode）

#### 正常模式

进入其他模式转换指令

i I a A o O 进入插入模式

​	i	：在光标当前位置进入插入模式

​	I	：（shift+i）在光标所在当前行的开头进入插入模式

​	a	：光标会回到光标所在当前位置的下一行进入插入模式

​	A	：在光标所在当前行的结尾进入插入模式

​	o	：来到光标所在的下一行进入插入模式，同时下一行会换行

​	O	：在光标所在的上一行进入插入模式，同时原本的行下移一行（回车）

v V ctrl+v	进入可视化模式

:	进入命令模式

esc	从其他模式回到正常模式

进入vim编辑器：

```sh
vim
```

或

```sh
vim 所要编辑的文件名
```

vim中移动光标使用h（左移）j（下移）k（上移）l（右移）

用键盘的上下左右会出现乱码

基本操作

​	y	复制	yy	屏幕无显示，复制整行

​					 3yy	提示复制了三行

​					 y $ 复制当前行从光标到结尾

​	d	剪切	dd	剪切一整行

​					 d $	剪切当前行从光标到结尾

​	p	粘贴

​	u	撤销（在普通模式下）可多次撤销,相当于后退

​	ctrl+r	重做（将撤销指令重做），相当于前进

​	x	删除单个字符

​	r	替换单个字符

​	G	定位到指定行

移至11行

```shell
11 G
```

g	文本第一行，G	文本最后一行

^	定位到行首（shift+6）

$	定位到行尾（shift+4）

:set nu	显示当前行

注：均在普通模式进行

#### 命令模式

基本操作：

:w	写入	:w+保存的文件名	eg：:w /root/a.txt	若是通过vim+文件名打开的文件，使用:w可以直接保存

:q	退出	也可以一起使用	:wq(保存并退出)

:!	执行shell命令	:q!(不保存并退出)

eg：	:! ipconfig

:s	替换	:s /old/new	将old替换为new（默认只针对光标所在的行）

/	查找	/x	查找字母，x，光标会闪烁到指定位置	若出现多个x,可以按n匹配下一个字符 N匹配上一个字符

若出现多个x全部替换	:%s /x/X/g

指定行时 :3,5 s /x/X

:set	设置命令 :set nu 显示符号

​						  :set nonu 不显示符号

​							只能对单词修改生效，推出后消失

vim /etc/vimrc	对这个文件修改配置

eg：由次希望执行打开就显示行号，在最后一行可插入新空行 G o 加上set nu,ESC,:wq即可修改成功

#### 可视模式

三种进入可视模式的方式（拖动光标选择）

v	字符可视模式（以字符为单位）

V	行可视模式（以行为单位）

ctrl+v	块可视模式（上下对齐的块）

​	配合d和l（大写i）命令可以进行块的便利模式

​	d	选中后，删除

​	l	来到这一块左上角，出入插入的信息

### 用户与权限管理

#### 多用户操作系统

多用户操作系统的目的是隔离

​	用户权限隔离

​	系统资源隔离

root用户与普通用户的区别

#### 用户管理常用命令

useradd	新建用户

userdel	删除用户

passwd		修改用户密码

usermod	修改用户属性

chage	修改用户属性	具体用man查看(主要是修改用户的生命周期)

root用户才有权限进行用户创建

```shell
useradd wilson
```

可以用id命令验证是否存在此用户

```shell
id root
id wilson
```

root的家目录在/root下

Wilson的家目录在/home/wilson/下

```shell
ls /home/wilson/
ls /etc/passwd
#或
tail -10 /etc/passwd
#或
tail -10 /etc/shadow
```

```sh
userdel wilson
userdel -r wilson	#-r 可以将该用户的家目录也删除
```

```sh
usermod -d /home/w/ w
```

#### 组管理命令

groupadd	新建用户组

```shell
groupadd group1#创建用户组
useradd user1#增加用户
usermod -g group1 user1#修改用户组
#或
useradd -g group1 user2
#可以通过id命令查看
```

groupdel	删除用户组

#### 用户切换

root切换普通用户无密码，如同用户切换root用户需要密码，普通用户切换普通用户也需要密码

```sh
su - user1
exit#此指令可以登出
```

su	切换用户

​	su - USERNAME	使用login shell 方式切换用户

sudo	在自己的用户下，以其他用户身份执行命令

visudo	设置需要使用sudo的用户（组）

例如：shutdown只能root使用

```sh
useradd user3
shutdown -h 30#30分钟后关闭该用户
shutdown -c #可以取消（这条命令不执行）
su - user3
visudo #此命令加上% 
wich shutdown #找到shutdown命令所在目录

```

在里卖弄加入user3 localhost=

​								ALL=/sbin/shutdown -c

​						这时sudo /sbin/shutdown -c只需要输入user3的密码

#### 用户配置文件

/etc/passwd	用户配置文件

/etc/shadow	用户密码相关配置文件

/etc/group	用户组配置文件

```shell
vim /etc/shadow
```

例如：user2:$6$...............:18049:0:99999:7:::

user2是用户名

$6代表加密过，那两个用户密码相同，显示出来也会不同

```sh
vim /etc/passwd
```

例如：root​ : x:0:0:root:/root:/bin/bash

第一个字段代表用户名称

第二个字段代表是否需要密码验证	x表示需要 空表示不需要

第三个字段代表uid

第四个字段代表gid（组）

第五个字段代表注释

第六个字段代表家目录

第七个字段代表命令解释器	第七个字段若为/sbin/nologin，则不允许登陆终端

新建用户时会对配置文件中写入一行

```sh
vim /etc/group
```

sys:x :s:

第一个字段表示组名称

第二个字段表示是否有密码

第三个字段表示gid

第四个字段表示其他组设置

查看文件权限的方法

——r w-------1   root     root   1523    sep   28  12:05   anaconda-ks.cfg

类型  权限          所属用户和组                                          文件名

-普通文件           哪个用户创建

d目录文件           创建的用户属于哪个组

b块特殊文件	块设备（类似硬盘）

c字符特殊文件	字符设备（终端）

l符号链接

f命名管道

s套接字文件

#### 文件权限的表示方法

- 字符权限表示方法

​	r	读

​	w	写

​	x	执行

- 数字权限的表示方法

  r=4

  w=2

  x=1

  一种8进制表示方法

  例如：-rw-r-x-r-- 1 username groupname mtime filename

  rw-	文件属主的权限

  r-x	文件属组的权限（组中的用户）

  r--	其他用户的权限

  - 创建新文件有默认权限，根据umask值计算，属主和属组根据当前进程的用户来设定

- x   可以进入目录

- rx   显示目录内的文件名（进入目录并且可以查看文件名）

#### 文件权限管理常用命令

##### 修改权限的命令

- chmod	修改文件，目录权限

chomd u  +

​			g  -	权	文

​			o  =   限	件

​			a				名

注：+加权限

​		-减权限

​		=设置权限

举例

```shell
chmod g-r afile
```

注;权限只限制非root用户

```sh
chmod u-wx
#或
chmod 446 #相加 
```

默认权限=446——文件掩码值

两种修改方式：1字符2数字

```sh
chmod u+x /tmp/testfile
chmod 775 /tmp/testfile
```

- chown	更改属主，属组

  ```sh
  mkdir /test #新建目录
  ls -l /
  ls -ld /test #单独查看文件
  chown user1 /test #修改属主
  ls -ld /test
  chown :group1 /test #修改属组
  ls -ld /test
  ```

- chgrp   可以单独更改属组，不常用

  ```sh
  chgrp user3 /test
  ls -ld /test
  ```

  crtl + r 可以搜索之前的命令

  测试：

  ```sh
  ls -ld /test #目录
  chmod 777 /test #将特权设置为最大
  ls -ld /test
  touch afile #创建新文件
  ls
  chown user1: group1 afile #同时修改属组和属主
  ls -l
  chmod 400 afile
  ls -l
  echo 123 > afile #输出重定向，把输出在屏幕桑的字符输入文件
  cat afile #查看
  su - user1
  id #验证
  cat /test/afile
  echo 456 > /test/afile 
  #会提示权限不够
  exit
  chmod 200 /test/afile
  ls -l /test/afile
  su - user1
  echo 456 > /test/afile
  touch /test/bfile
  ls -l /test/
  chmod 020 /test/bfile
  ls -l /test/ #中间代表组内都有权限冲突，以属主为主
  #020属主依旧没有权限，但是组内其他人有权限
  echo 456 > /test/bfile 
  #失败，因为属主user1无权限
  su - user2
  id user2
  echo 456 > /test/bfile
  exit
  chmod 400 /test
  su - user1 
  ls -l /test
  #会提示权限不够
  exit
  chmod u=x /test
  ls -ld /test
  su - user1
  cd /test
  exit
  chmod u=rx /test
  su - user1
  cd /test
  ls
  ls -l
  chmod u=wx /test
  su - user1 
  cd /test
  ls -l
  #无权限
  rm afile 
  exit
  ```

  

##### 特殊权限

- SUID	用于二进制可执行文件，执行命令时却文件属主权限

  如/user/bin/passwd	普通用户也可以用SUID改密码

  ```sh
  ls -l /usr/bin/passwd
  ```

-  SGID   用于目录，在该目录下创建新的文件和目录，权限自动更改为该目录的属组

- SBIT   用于目录，该目录下新建的文件和目录，仅root和自己可以删除

  如/tmp

## 系统管理篇

### 网络管理

#### 网络状态查看

### 网络配置

### 路由命令

### 网络故障排除

### 网络服务管理

### 常用网络配置文件