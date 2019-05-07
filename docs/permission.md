# Linux Permission
```linux```操作系统权限模块

## 系统管理-用户和工作组管理-分组

### 新增分组 ```groupadd```
```groupadd```命令用于创建一个新的工作组，新工作组的信息将被添加到系统文件中

#### 语法
>groupadd(选项)(参数)

#### 选项
```bash
-g：指定新建工作组的id
-r：创建系统工作组，系统工作组的组ID小于500
-K：覆盖配置文件“/ect/login.defs”
-o：允许添加组ID号不唯一的工作组
```

#### 参数
组名：指定新建工作组的组名

#### 实例
建立一个新分组：
>groupadd group

此时在```/etc/passwd```文件中将产生一个名为```group```的分组

### 删除分组 ```groupdel```
```groupdel```命令用于删除指定的工作组，本命令要修改的系统文件包括```/ect/group```和```/ect/gshadow```，若该群组中仍包括某些用户，则必须先删除这些用户后，方能删除群组

#### 语法
>groupdel(参数)

#### 参数
组名：指定要删除的工作的组名

#### 实例
>groupdel group // 删除这个工作组

### 编辑分组 ```groupmod```
```groupmod```命令更改群组识别码或名称，需要更改群组的识别码或名称时，可用```groupmod```指令来完成这项工作

#### 语法
>groupmod(选项)(参数)

#### 选项
```bash
-g<群组识别码>：设置欲使用的群组识别码
-o：重复使用群组识别码
-n<新群组名称>：设置欲使用的群组名称
```

#### 参数
组名：指定要修改的工作的组名

***

## 系统管理-用户和工作组管理-用户

### 新增用户 ```useradd```
```useradd```命令用于```Linux```中创建的新的系统用户，```useradd```可用来建立用户帐号，帐号建好之后，再用```passwd```设定帐号的密码，而可用```userdel```删除帐号，使用```useradd```指令所建立的帐号，实际上是保存在```/etc/passwd```文本文件中

在```Slackware```中，```adduser```指令是个```script```程序，利用交谈的方式取得输入的用户帐号资料，然后再交由真正建立帐号的```useradd```命令建立新用户，如此可方便管理员建立用户帐号，在```Red Hat Linux```中，```adduser```命令则是```useradd```命令的符号连接，两者实际上是同一个指令

#### 语法
>useradd(选项)(参数)

#### 选项
```
-c<备注>：加上备注文字，备注文字会保存在passwd的备注栏位中
-d<登入目录>：指定用户登入时的启始目录
-D：变更预设值
-e<有效期限>：指定帐号的有效期限
-f<缓冲天数>：指定在密码过期后多少天即关闭该帐号
-g<群组>：指定用户所属的群组
-G<群组>：指定用户所属的附加群组
-m：自动建立用户的登入目录
-M：不要自动建立用户的登入目录
-n：取消建立以用户名称为名的群组
-r：建立系统帐号
-s<shell>：指定用户登入后所使用的shell
-u<uid>：指定用户id
```

#### 参数
用户名：要创建的用户名

#### 实例
新建用户加入组：
```bash
useradd –g sales jack –G company, employees # -g：加入主要组、-G：加入次要组
```

建立一个新用户账户，并设置```ID```：
```bash
useradd maker -u 555 # 需要说明的是，设定ID值时尽量要大于500，以免冲突，因为Linux安装后会建立一些特殊用户，一般0到499之间的值留给bin、mail这样的系统账号
```

### 删除用户 ```userdel```
```userdel```命令用于删除给定的用户，以及与用户相关的文件。若不加选项，则仅删除用户帐号，而不删除相关文件。

#### 语法
>userdel(选项)(参数)

#### 选项
```
-f：强制删除用户，即使用户当前已登录；
-r：删除用户的同时，删除与用户相关的所有文件。
```

#### 参数
用户名：要删除的用户名。

#### 实例
```bash
userdel maker # 删除用户maker，但不删除其家目录及文件
userdel -r maker # 删除用户maker，其家目录及文件一并删除
```
请不要轻易用```-r```选项；他会删除用户的同时删除用户所有的文件和目录，切记如果用户目录下有重要的文件，在删除前请备份。

其实也有最简单的办法，但这种办法有点不安全，也就是直接在```/etc/passwd```中删除您想要删除用户的记录；但最好不要这样做，```/etc/passwd```是极为重要的文件，可能您一不小心会操作失误。

### 编辑用户 ```usermod```
```usermod```命令用于修改用户的基本信息。```usermod```命令不允许你改变正在线上的使用者帐号名称。当```usermod```命令用来改变```user id```，必须确认这名```user```没在电脑上执行任何程序。你需手动更改使用者的```crontab```档。也需手动更改使用者的```at```工作档。采用```NIS server```须在```server```上更动相关的```NIS```设定。

#### 语法
>usermod(选项)(参数)

#### 选项
```
-c<备注>：修改用户帐号的备注文字；
-d<登入目录>：修改用户登入时的目录；
-e<有效期限>：修改帐号的有效期限；
-f<缓冲天数>：修改在密码过期后多少天即关闭该帐号；
-g<群组>：修改用户所属的群组；
-G<群组>；修改用户所属的附加群组；
-l<帐号名称>：修改用户帐号名称；
-L：锁定用户密码，使密码无效；
-s<shell>：修改用户登入后所使用的shell；
-u<uid>：修改用户ID；
-U：解除密码锁定。
```

#### 参数
登录名：指定要修改信息的用户登录名。

#### 实例
```bash
usermod -G staff newuser2 # 将newuser2添加到组staff中
usermod -l newuser1 newuser # 修改newuser的用户名为newuser1
usermod -L newuser1 # 锁定账号newuser1
usermod -U newuser1 # 解除对newuser1的锁定
```

### 配置用户认证信息 ```passwd```
```passwd```命令用于设置用户的认证信息，包括用户密码、密码过期时间等。系统管理者则能用它管理系统用户的密码。只有管理者可以指定用户名称，一般用户只能变更自己的密码。

#### 语法
>passwd(选项)(参数)

#### 选项
```
-d：删除密码，仅有系统管理者才能使用；
-f：强制执行；
-k：设置只有在密码过期失效后，方能更新；
-l：锁住密码；
-s：列出密码的相关信息，仅有系统管理者才能使用；
-u：解开已上锁的帐号。
```

#### 参数
用户名：需要设置密码的用户名。

#### 知识扩展
与用户、分组相关的文件

存放用户信息：
>/etc/passwd<br>
>/etc/shadow

存放组信息：
>/etc/group<br>
>/etc/gshadow

用户信息文件分析（每项用```:```隔开）
```bash
例如：jack:X:503:504:::/home/jack/:/bin/bash
jack # 用户名
X # 口令、密码
503 # 用户id（0代表root、普通新建用户从500开始）
504 # 所在组
: # 描述
/home/jack/ # 用户主目录
/bin/bash # 用户缺省Shell
```

组信息文件分析
```bash
例如：jack:$!$:???:13801:0:99999:7:*:*:
jack # 组名
$!$ # 被加密的口令
13801 # 创建日期与今天相隔的天数
0 # 口令最短位数
99999 # 用户口令
7 # 到7天时提醒
* # 禁用天数
* # 过期天数
```

#### 实例
如果是普通用户执行```passwd```只能修改自己的密码。如果新建用户后，要为新用户创建密码，则用```passwd```用户名，注意要以```root```用户的权限来创建。

```bash
[root@localhost ~]$ passwd linuxde # 更改或创建linuxde用户的密码；
Changing password for user linuxde.
New UNIX password: # 请输入新密码；
Retype new UNIX password: # 再输入一次；
passwd: all authentication tokens updated successfully. # 成功；
```

普通用户如果想更改自己的密码，直接运行```passwd```即可，比如当前操作的用户是```linuxde```。

```bash
[linuxde@localhost ~]$ passwd
Changing password for user linuxde.# 更改linuxde用户的密码；
(current) UNIX password: # 请输入当前密码；
New UNIX password: # 请输入新密码；
Retype new UNIX password: # 确认新密码；
passwd: all authentication tokens updated successfully. # 更改成功；
```

比如我们让某个用户不能修改密码，可以用```-l```选项来锁定：

```bash
[root@localhost ~]$ passwd -l linuxde # 锁定用户linuxde不能更改密码；
Locking password for user linuxde.
passwd: Success # 锁定成功；

[linuxde@localhost ~]$ su linuxde # 通过su切换到linuxde用户；
[linuxde@localhost ~]$ passwd # linuxde来更改密码；
Changing password for user linuxde.
Changing password for linuxde
(current) UNIX password: # 输入linuxde的当前密码；
passwd: Authentication token manipulation error # 失败，不能更改密码；
```

再来一例：

```bash
[root@localhost ~]$ passwd -d linuxde # 清除linuxde用户密码；
Removing password for user linuxde.
passwd: Success # 清除成功；

[root@localhost ~]$ passwd -S linuxde # 查询linuxde用户密码状态；
Empty password. # 空密码，也就是没有密码；
```

注意：当我们清除一个用户的密码时，登录时就无需密码，这一点要加以注意。

### Linux工作组文件管理工具 ```gpasswd```
```gpasswd```命令是文件```/etc/group```和```/etc/gshadow```的管理工具。

#### 语法
>gpasswd(选项)(参数)

#### 选项
```
-a：添加用户到组；
-d：从组删除用户；
-A：指定管理员；
-M：指定组成员和-A的用途差不多；
-r：删除密码；
-R：限制用户登入组，只有组中的成员才可以用newgrp加入该组。
```

#### 参数
组：指定要管理的工作组。

#### 实例
如系统有个```pete```r账户，该账户本身不是```groupname```群组的成员，使用```newgrp```需要输入密码即可。
>gpasswd groupname

让使用者暂时加入成为该组成员，之后```peter```建立的文件```group```也会是```groupname```。所以该方式可以暂时让```peter```建立文件时使用其他的组，而不是```peter```本身所在的组。所以使用```gpasswd groupname```设定密码，就是让知道该群组密码的人可以暂时切换具备```groupname```群组功能的。
>gpasswd -A peter users

这样```peter```就是```users```群组的管理员，就可以执行下面的操作：
>gpasswd -a mary users
>gpasswd -a allen users

注意：添加用户到某一个组 可以使用```usermod -G group_name user_name```这个命令可以添加一个用户到指定的组，但是以前添加的组就会清空掉。所以想要添加一个用户到一个组，同时保留以前添加的组时，请使用```gpasswd```这个命令来添加操作用户：
>gpasswd -a user_name group_name

***

## 文件目录管理-文件权限属性设置

### 查看文件权限
输入```ls -l```命令后显示的内容如下：
>-rwxrw-r‐-1 root root 1213 Feb 2 09:39 abc
```
10个字符确定文件权限信息
第一个字符含义：文件（-）、目录（d）、链接（l）
其余字符每3个一组（rwx），读（r）、写（w）、执行（x）
第一组rwx：文件所有者的权限是读、写和执行
第二组rw-：与文件所有者同一组的用户的权限是读、写但不能执行
第三组r--：不与文件所有者同组的其他用户的权限是读不能写和执行
也可用数字表示为：r=4，w=2，x=1 即1-x，2-w，3-wx，4-r，5-rx，6-rw，7-rwx
1 表示该目录下的文件数
root 表示用户
root 表示用户所在的组
1213 表示文件大小（字节）
Feb 2 09:39 表示最后修改日期
abc 表示文件名
```

### 变更文件或目录的权限 ```chmod```
文件或目录权限的控制分别以读取、写入、执行3种一般权限来区分，另有3种特殊权限可供运用。用户可以使用```chmod```指令去变更文件与目录的权限，设置方式采用文字或数字代号皆可。符号连接的权限无法变更，如果用户对符号连接修改权限，其改变会作用在被连接的原始文件

#### 权限范围的表示法如下：
```
u User，即文件或目录的拥有者；
g Group，即文件或目录的所属群组；
o Other，除了文件或目录拥有者或所属群组之外，其他用户皆属于这个范围；
a All，即全部的用户，包含拥有者，所属群组以及其他用户；
r 读取权限，数字代号为“4”;
w 写入权限，数字代号为“2”；
x 执行或切换权限，数字代号为“1”；
- 不具任何权限，数字代号为“0”；
s 特殊功能说明：变更文件或目录的权限
```

#### 语法
>chmod(选项)(参数)

#### 选项
```
-c或——changes：效果类似“-v”参数，但仅回报更改的部分；
-f或--quiet或——silent：不显示错误信息；
-R或——recursive：递归处理，将指令目录下的所有文件及子目录一并处理；
-v或——verbose：显示指令执行过程；
--reference=<参考文件或目录>：把指定文件或目录的所属群组全部设成和参考文件或目录的所属群组相同；
<权限范围>+<权限设置>：开启权限范围的文件或目录的该选项权限设置；
<权限范围>-<权限设置>：关闭权限范围的文件或目录的该选项权限设置；
<权限范围>=<权限设置>：指定权限范围的文件或目录的该选项权限设置；
```

#### 参数
权限模式：指定文件的权限模式

文件：要改变权限的文件。

#### 实例
```bash
chmod 755 abc # 赋予abc权限rwxr-xr-x
chmod u=rwx,g=rx,o=rx abc # 同上u=用户权限，g=组权限，o=不同组其他用户权限
chmod u-x,g+w abc # 给abc去除用户执行的权限，增加组写的权限
chmod a+r abc # 给所有用户添加读的权限
chmod u+x,g+w f01 # 为文件f01设置自己可以执行，组员可以写入的权限
chmod a+x f01 # 对文件f01的u，g，o都设置可执行属性
```

### 改变某个文件或目录的所有者和所属的组 ```chown```
该命令可以向某个用户授权，使该用户变成指定文件的所有者或者改变文件所属的组。用户可以是用户名称或者是用户```id```，用户组可以是组名或组```id```。文件名可以使由空格分开的文件列表，在文件名中可以包含通配符

只有文件主和超级用户才可以便用该命令

#### 语法
>chown(选项)(参数)

#### 选项
```
-c或——changes：效果类似“-v”参数，但仅回报更改的部分；
-f或--quite或——silent：不显示错误信息；
-h或--no-dereference：只对符号连接的文件作修改，而不更改其他任何相关文件；
-R或——recursive：递归处理，将指定目录下的所有文件及子目录一并处理；
-v或——version：显示指令执行过程；
--dereference：效果和“-h”参数相同；
--help：在线帮助；
--reference=<参考文件或目录>：把指定文件或目录的拥有者与所属群组全部设成和参考文件或目录的拥有者与所属群组相同；
--version：显示版本信息。
```

#### 参数
用户：组：指定所有者和所属工作组。当省略“：组”，仅改变文件所有者；
文件：指定要改变所有者和工作组的文件列表。支持多个文件和目标，支持```shell```通配符。

#### 实例
```bash
chown xiaoming abc # 改变abc的所有者为xiaoming
chown root ./abc # 改变abc这个目录的所有者是root
chown ‐R root ./abc # 改变abc这个目录及其下面所有的文件和目录的所有者是root
```

### 改变文件或目录所属的用户组 ```chgrp```
该命令用来改变指定文件所属的用户组。其中，组名可以是用户组的```id```，也可以是用户组的组名。文件名可以 是由空格分开的要改变属组的文件列表，也可以是由通配符描述的文件集合。如果用户不是该文件的文件主或超级用户(```root```)，则不能改变该文件的组。

在```UNIX```系统家族里，文件或目录权限的掌控以拥有者及所属群组来管理。您可以使用```chgrp```指令去变更文件与目录的所属群组，设置方式采用群组名称或群组识别码皆可。

#### 语法
>chgrp(选项)(参数)

#### 选项
```
-c或——changes：效果类似“-v”参数，但仅回报更改的部分；
-f或--quiet或——silent：不显示错误信息；
-h或--no-dereference：只对符号连接的文件作修改，而不是该其他任何相关文件；
-R或——recursive：递归处理，将指令目录下的所有文件及子目录一并处理；
-v或——verbose：显示指令执行过程；
--reference=<参考文件或目录>：把指定文件或目录的所属群组全部设成和参考文件或目录的所属群组相同；
```

#### 参数
组：指定新工作名称；

文件：指定要改变所属组的文件列表。多个文件或者目录之间使用空格隔开。

#### 实例
```bash
chgrp root abc # 改变abc所属的组为root
chgrp -R mengxin /usr/meng # 将/usr/meng及其子目录下的所有文件的用户组改为mengxin
```
