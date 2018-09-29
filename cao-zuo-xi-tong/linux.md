# _linux_

Linux之父：**林纳斯·本纳第克特·托瓦兹（**Linus Benedict Torvalds, 1969年~ ），著名的电脑程序员。Linux内核的发明人及该计划的合作者。托瓦兹利用个人时间及器材创造出了这套当今全球最流行的操作系统（作业系统）内核之一。现受聘于开放源代码开发实验室（OSDL：Open Source Development Labs, Inc），全力开发Linux内核。![](/assets/importzifu.png)

**Linux根据原生程度，分为两种：**

1. **内核版本：**
   Linux不是一个操作系统，严格来讲，Linux只是一个操作系统中的内核。内核是什么？内核建立了计算机软件与硬件之间通讯的平台，内核提供系统服务，比如文件管理、虚拟内存、设备I/O等；
2. **发行版本：**
   一些组织或公司在内核版基础上进行二次开发而重新发行的版本。Linux发行版本有很多种（ubuntu和CentOS用的都很多，初学建议选择CentOS）

## linux目录

在Linux操作系统中，所有被操作系统管理的资源，例如网络接口卡、磁盘驱动器、打印机、输入输出设备、普通文件或是目录都被看作是一个文件。把一切资源都看作是文件，包括硬件设备

![](/assets/importlinuxmulu.png)

```
/ 根目录
/bin 该目录中存放Linux的常用命令 比如ls,mkdir指令等。
/dev 该目录包含了Linux系统中使用的所有外部设备 系统设备目录，硬盘丶光驱都是在此目录下/dev/cdrom。
/cdrom 该目录在刚安装系统时是空的，你可以将光驱文件系统挂在这个目录下
/etc 该目录存放了系统管理时要用到的各种配置文件和子目录
/sbin 该目录用来存放系统管理员的系统管理程序
/home 普通用户家目录，创建一个“11”用，/home下就会对应的生成一个“11”目录，该目录是“11”用户的家目录
/lib 该目录用来存放系统动态连接共享库
/lost+found 该目录在大多数情况下都是空的。但当突然停电、或者非正常关机后，有些文件就临时存放在这里
/mnt 临时文件挂载点
/root 超级用户root的家目录
/tmp 用来存放不同程序执行时产生的临时文件
/usr 用户的很多应用程序和文件都存放在该目录下
/opt:第三方程序目录，qq,wps等软件通常放置于此目录下。
/boot:系统引导目录，启动文件丶引导文件。（通常情况下不能动，否则系统将会出现无法启动等问题）。
```

## 文件挂载

linux采用的是树型结构。最上层是根目录，其他的所有目录都是从根目录出发而生成的。微软的DOS和windows也是采用树型结构，但是在DOS 和windows中这样的树型结构的根是磁盘分区的盘符，有几个分区就有几个树型结构，他们之间的关系是并列的。但是在linux中，无论操作系统管理几个磁盘分区，这样的目录树只有一个。从结构上讲，各个磁盘分区上的树型目录不一定是并列的。

### mount挂载

**挂载的概念                      
**

当要使用某个设备时，例如要读取硬盘中的一个格式化好的分区、光盘或软件等设备时，必须先把这些设备对应到某个目录（这个目录可以不为空，但挂载后这个目录下以前的内容将不可用），而这个目录就称为“挂载点（mount point）”，这样才可以读取这些设备，而这些对应的动作就是“挂载”。

需要理解的是：

linux操作系统将所有的设备都看作文件，

它将整个计算机的资源都整合成一个大的文件目录。

我们要访问存储设备中的文件，必须将文件所在的分区挂载到一个已存在的目录上，

然后通过访问这个目录来访问存储设备。

> Mount命令可以实现挂载：
>
> mount \[-fnrsvw\] \[-t vfstype\] \[-o options\] device dir

问：所有的磁盘分区都必须被挂载上才能使用，那么我们机器上的硬盘分区是如何被挂载的？

主要是利用了/etc/fstab文件。每次内核加载时知道从这里开始mount文件系统。linux系统启动时根据该文件定义自动挂载。若没有被自动挂载，分区将不能使用。

**磁盘分区和目录的关系**

任何一个分区都必须挂载到某个目录上。

目录是逻辑上的区分。分区是物理上的区分。

磁盘Linux分区都必须挂载到目录树中的某个具体的目录上才能进行读写操作。

根目录是所有Linux的文件和目录所在的地方，需要挂载上一个磁盘分区。

## 磁盘分区

要掌握Linux磁盘分区，先了解一下[硬盘](/cao-zuo-xi-tong/ying-pan.md)的物理结构。

硬盘的分区主要分为**主分区**和**扩展分区**两种。主分区和扩展分区的数目之和不能大于四个，且基本分区可以马上别使用，但不能再分区。扩展分区必须再进行分区后才能使用，也就是它必须还要进行二次分区。那么有扩展分区再分下去的是什么呢？它就是逻辑分区，而且逻辑分区没有数量上的限制。

![](/assets/importlinufenx.png)

#### hda1 、sda1 命名格式介绍

hd表示硬盘   a表示第一块盘   1表示第一分区

hda1表示第一块盘的第一分区

分类说明：

hd\(n\)是IDE接口的。

sd\(n\)是SCSI接口的，和usb接口。

具体表示：

![](/assets/importhda1.png)

## Linux基本命令

下面只是给出了一些比较常用的命令。推荐一个Linux命令快查网站，非常不错，大家如果遗忘某些命令或者对某些命令不理解都可以在这里得到解决。

Linux命令大全：[http://man.linuxde.net/](http://man.linuxde.net/)

### 目录切换命令

* `cd usr`**：** 切换到该目录下usr目录
* `cd ..（或cd../）`**：**切换到上一层目录
* `cd /`**：**切换到系统根目录
* `cd ~`**：**切换到用户主目录
* `cd -`**：**切换到上一个所在目录

### 目录的操作命令（增删改查）

1. `mkdir 目录名称`**：**增加目录

2. `ls或者ll`（ll是ls -l的缩写，ll命令以看到该目录下的所有目录和文件的详细信息）：查看目录信息

3. `find 目录 参数`**：**寻找目录（查）

   示例：

   * 列出当前目录及子目录下所有文件和文件夹:`find .`
   * 在`/home`目录下查找以.txt结尾的文件名:`find /home -name "*.txt"`
   * 同上，但忽略大小写:`find /home -iname "*.txt"`
   * 当前目录及子目录下查找所有以.txt和.pdf结尾的文件:`find . \( -name "*.txt" -o -name "*.pdf" \)`
     或`find . -name "*.txt" -o -name "*.pdf"`

4. `mv 目录名称 新目录名称`**：**修改目录的名称（改）

   注意：mv的语法不仅可以对目录进行重命名而且也可以对各种文件，压缩包等进行 重命名的操作。mv命令用来对文件或目录重新命名，或者将文件从一个目录移到另一个目录中。后面会介绍到mv命令的另一个用法。

5. `mv 目录名称 目录的新位置`**：**移动目录的位置---剪切（改）

   注意：mv语法不仅可以对目录进行剪切操作，对文件和压缩包等都可执行剪切操作。另外mv与cp的结果不同，mv好像文件“搬家”，文件个数并未增加。而cp对文件进行复制，文件个数增加了。

6. `cp -r 目录名称 目录拷贝的目标位置`**：**拷贝目录（改），-r代表递归拷贝

   注意：cp命令不仅可以拷贝目录还可以拷贝文件，压缩包等，拷贝文件和压缩包时不 用写-r递归

7. `rm [-rf] 目录`**:**删除目录（删）

   注意：rm不仅可以删除目录，也可以删除其他文件或压缩包，为了增强大家的记忆， 无论删除任何目录或文件，都直接使用`rm -rf`目录/文件/压缩包

### 文件的操作命令（增删改查）

1. `touch 文件名称`**:**文件的创建（增）

2. `cat/more/less/tail 文件名称`文件的查看（查）

   * `cat`**：**只能显示最后一屏内容
   * `more`**：**可以显示百分比，回车可以向下一行， 空格可以向下一页，q可以退出查看
   * `less`**：**可以使用键盘上的PgUp和PgDn向上 和向下翻页，q结束查看
   * `tail-10`**：**查看文件的后10行，Ctrl+C结束

   注意：命令 tail -f 文件 可以对某个文件进行动态监控，例如tomcat的日志文件， 会随着程序的运行，日志会变化，可以使用tail -f catalina-2016-11-11.log 监控 文 件的变化

3. `vim 文件`**：**修改文件的内容（改）

   vim编辑器是Linux中的强大组件，是vi编辑器的加强版，vim编辑器的命令和快捷方式有很多，但此处不一一阐述，大家也无需研究的很透彻，使用vim编辑修改文件的方式基本会使用就可以了。

   **在实际开发中，使用vim编辑器主要作用就是修改配置文件，下面是一般步骤：**

   vim 文件------&gt;进入文件-----&gt;命令模式------&gt;按i进入编辑模式-----&gt;编辑文件 -------&gt;按Esc进入底行模式-----&gt;输入:wq/q! （输入wq代表写入内容并退出，即保存；输入q!代表强制退出不保存。）

4. `rm -rf 文件`**：**删除文件（删）

   同目录删除：熟记`rm -rf`文件 即可

### 压缩文件的操作命令

**1）打包并压缩文件：**

Linux中的打包文件一般是以.tar结尾的，压缩的命令一般是以.gz结尾的。

而一般情况下打包和压缩是一起进行的，打包并压缩后的文件的后缀名一般.tar.gz。 命令：`tar -zcvf 打包压缩后的文件名 要打包压缩的文件`其中：

z：调用gzip压缩命令进行压缩

c：打包文件

v：显示运行过程

f：指定文件名

比如：加入test目录下有三个文件分别是 :aaa.txt bbb.txt ccc.txt,如果我们要打包test目录并指定压缩后的压缩包名称为test.tar.gz可以使用命令：`tar -zcvf test.tar.gz aaa.txt bbb.txt ccc.txt`**或：**`tar -zcvf test.tar.gz /test/`

**2）解压压缩包：**

命令：tar \[-xvf\] 压缩文件

其中：x：代表解压

示例：

1 将/test下的test.tar.gz解压到当前目录下可以使用命令：`tar -xvf test.tar.gz`

2 将/test下的test.tar.gz解压到根目录/usr下:`tar -xvf xxx.tar.gz -C /usr`（- C代表指定解压的位置）

### Linux的权限命令

操作系统中每个文件都拥有特定的权限、所属用户和所属组。权限是操作系统用来限制资源访问的机制，在Linux中权限一般分为读\(readable\)、写\(writable\)和执行\(excutable\)，分为三组。分别对应文件的属主\(owner\)，属组\(group\)和其他用户\(other\)，通过这样的机制来限制哪些用户、哪些组可以对特定的文件进行什么样的操作。通过`ls -l`命令我们可以 查看某个目录下的文件或目录的权限

示例：在随意某个目录下`ls -l`

[![](https://camo.githubusercontent.com/615d1a5f71d5d9e3370c67fb04f6afbc4374fd5f/68747470733a2f2f757365722d676f6c642d63646e2e786974752e696f2f323031382f372f352f313634363935356265373831646161613f773d35383926683d32323826663d706e6726733d3136333630)](https://camo.githubusercontent.com/615d1a5f71d5d9e3370c67fb04f6afbc4374fd5f/68747470733a2f2f757365722d676f6c642d63646e2e786974752e696f2f323031382f372f352f313634363935356265373831646161613f773d35383926683d32323826663d706e6726733d3136333630)

第一列的内容的信息解释如下：

[![](https://camo.githubusercontent.com/109f4a737bb3573238ab75d94ebce4dd9a79f0c1/68747470733a2f2f757365722d676f6c642d63646e2e786974752e696f2f323031382f372f352f313634363935363562363935313739313f773d34383926683d32303926663d706e6726733d3339373931)](https://camo.githubusercontent.com/109f4a737bb3573238ab75d94ebce4dd9a79f0c1/68747470733a2f2f757365722d676f6c642d63646e2e786974752e696f2f323031382f372f352f313634363935363562363935313739313f773d34383926683d32303926663d706e6726733d3339373931)

> 下面将详细讲解文件的类型、Linux中权限以及文件有所有者、所在组、其它组具体是什么？

**文件的类型：**

* d： 代表目录
* -： 代表文件
* l： 代表链接（可以认为是window中的快捷方式）

**Linux中权限分为以下几种：**

* r：代表权限是可读，r也可以用数字4表示
* w：代表权限是可写，w也可以用数字2表示
* x：代表权限是可执行，x也可以用数字1表示

**文件和目录权限的区别：**

对文件和目录而言，读写执行表示不同的意义。

对于文件：

| 权限名称 | 可执行操作 |
| :--- | :--- |
| r | 可以使用cat查看文件的内容 |
| w | 可以修改文件的内容 |
| x | 可以将其运行为二进制文件 |

对于目录：

| 权限名称 | 可执行操作 |
| :--- | :--- |
| r | 可以查看目录下列表 |
| w | 可以创建和删除目录下文件 |
| x | 可以使用cd进入目录 |

**在linux中的每个用户必须属于一个组，不能独立于组外。在linux中每个文件有所有者、所在组、其它组的概念。**

* **所有者**

  一般为文件的创建者，谁创建了该文件，就天然的成为该文件的所有者，用ls ‐ahl命令可以看到文件的所有者 也可以使用chown 用户名 文件名来修改文件的所有者 。

* **文件所在组**

  当某个用户创建了一个文件后，这个文件的所在组就是该用户所在的组 用ls ‐ahl命令可以看到文件的所有组 也可以使用chgrp 组名 文件名来修改文件所在的组。

* **其它组**

  除开文件的所有者和所在组的用户外，系统的其它用户都是文件的其它组

> 我们再来看看如何修改文件/目录的权限。

**修改文件/目录的权限的命令：**`chmod`

示例：修改/test下的aaa.txt的权限为属主有全部权限，属主所在的组有读写权限， 其他用户只有读的权限

`chmod u=rwx,g=rw,o=r aaa.txt`

[![](https://camo.githubusercontent.com/f4bf8b308d8c97418bb28745f0adcc0f2cf62f97/68747470733a2f2f757365722d676f6c642d63646e2e786974752e696f2f323031382f372f352f313634363937343437646336656361633f773d35323526683d32343626663d706e6726733d3132333632)](https://camo.githubusercontent.com/f4bf8b308d8c97418bb28745f0adcc0f2cf62f97/68747470733a2f2f757365722d676f6c642d63646e2e786974752e696f2f323031382f372f352f313634363937343437646336656361633f773d35323526683d32343626663d706e6726733d3132333632)

上述示例还可以使用数字表示：

chmod 764 aaa.txt

**补充一个比较常用的东西:**

假如我们装了一个zookeeper，我们每次开机到要求其自动启动该怎么办？

1. 新建一个脚本zookeeper
2. 为新建的脚本zookeeper添加可执行权限，命令是:
   `chmod +x zookeeper`
3. 把zookeeper这个脚本添加到开机启动项里面，命令是：
   `chkconfig --add zookeeper`
4. 如果想看看是否添加成功，命令是：
   `chkconfig --list`

###  Linux 用户管理

Linux系统是一个多用户多任务的分时操作系统，任何一个要使用系统资源的用户，都必须首先向系统管理员申请一个账号，然后以这个账号的身份进入系统。

用户的账号一方面可以帮助系统管理员对使用系统的用户进行跟踪，并控制他们对系统资源的访问；另一方面也可以帮助用户组织文件，并为用户提供安全性保护。

**Linux用户管理相关命令:**

* `useradd 选项 用户名`
  :添加用户账号
* `userdel 选项 用户名`
  :删除用户帐号
* `usermod 选项 用户名`
  :修改帐号
* `passwd 用户名`
  :更改或创建用户的密码
* `passwd -S 用户名`
  :显示用户账号密码信息
* `passwd -d 用户名`
  : 清除用户密码

useradd命令用于Linux中创建的新的系统用户。useradd可用来建立用户帐号。帐号建好之后，再用passwd设定帐号的密码．而可用userdel删除帐号。使用useradd指令所建立的帐号，实际上是保存在/etc/passwd文本文件中。

passwd命令用于设置用户的认证信息，包括用户密码、密码过期时间等。系统管理者则能用它管理系统用户的密码。只有管理者可以指定用户名称，一般用户只能变更自己的密码。

### Linux系统用户组的管理

每个用户都有一个用户组，系统可以对一个用户组中的所有用户进行集中管理。不同Linux 系统对用户组的规定有所不同，如Linux下的用户属于与它同名的用户组，这个用户组在创建用户时同时创建。

用户组的管理涉及用户组的添加、删除和修改。组的增加、删除和修改实际上就是对/etc/group文件的更新。

**Linux系统用户组的管理相关命令:**

* `groupadd 选项 用户组`
  :增加一个新的用户组
* `groupdel 用户组`
  :要删除一个已有的用户组
* `groupmod 选项 用户组`
  : 修改用户组的属性

### 在线安装软件

### 其他常用命令

* `pwd`**：**显示当前所在位置

* `grep 要搜索的字符串 要搜索的文件 --color`**：**搜索命令，--color代表高亮显示

* `ps -ef`**/**`ps aux`**：**这两个命令都是查看当前系统正在运行进程，两者的区别是展示格式不同。如果想要查看特定的进程可以使用这样的格式：`ps aux|grep redis`（查看包括redis字符串的进程）

  注意：如果直接用ps（（Process Status））命令，会显示所有进程的状态，通常结合grep命令查看某进程的状态。

* `kill -9 进程的pid`**：**杀死进程（-9 表示强制终止。）

  先用ps查找进程，然后用kill杀掉

* **网络通信命令：**

  * 查看当前系统的网卡信息：ifconfig
  * 查看与某台机器的连接情况：ping
  * 查看当前系统的端口使用：netstat -an

* `shutdown`**：**`shutdown -h now`： 指定现在立即关机；`shutdown +5 "System will shutdown after 5 minutes"`:指定5分钟后关机，同时送出警告信息给登入用户。

* `reboot`**：**`reboot`**：**重开机。`reboot -w`**：**做个重开机的模拟（只有纪录并不会真的重开机）。


