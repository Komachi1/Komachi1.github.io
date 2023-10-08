# Linux

<img src="img/logo/linux_logo.png" alt="linux_logo" style="zoom: 10%;" />

## 快捷键

`Ctrl + u` 剪切光标到行首的所有内容

`Ctrl + k` 剪切光标到行尾的所有内容

`Ctrl + y` 粘贴

`Ctrl + c` 终止当前运行的进程

`Ctrl + z` 挂起当前进程，可使用 `fg` 命令恢复

`↑、↓` 查找执行过的命令

`!!` 执行上一条命令

`Tab` 命令和文件名自动补全

`Ctrl + l` & 输入`clear` 清屏，实质上只是让终端显示页向后翻了一页

## 常用命令

### 文件操作

#### cd

```shell	
# 更改当前工作目录
cd {dir}
# 跳转到根目录
cd /
# 跳转到当前用户目录
cd ~
# 跳转到上一级目录
cd ..
```

#### pwd

```shell
# 显示当前工作目录的路径
pwd
```

#### ls

```shell
# 以详细列表的形式显示当前工作目录下的所有可见文件
ls -l
# 显示当前工作目录下的所有文件，包括隐藏文件
ls -a
# 上述两种显示方式的结合
ls -la
```

#### tree

```shell
# 以树形结构显示指定目录下的文件结构
tree {dir}
```

#### cat

```shell
# 在标准输出（屏幕）上查看指定文件的内容
cat {file}
# 添加行号
cat -n {file}
```

#### head/tail

```shell
# 在标准输出（屏幕）上查看指定文件的开头N行内容（默认为10行）
head -n {N} {file}
# 在标准输出（屏幕）上查看指定文件的最后N行内容（默认为10行）
tail -n {N} {file}
```

#### more/less

```shell
# 在标准输出（屏幕）上分页显示文件内容
more {file}
# 按页或按窗口打印文件内容
less {file}
```

在 `more/less` 环境中也可使用一些基本命令：

* `<space> / <Enter>` 翻页

* `b` 返回上一页

* `q` 退出

#### mkdir

```shell	
# 创建一个新目录
mkdir {dir}
# 创建多级目录
mkdir -p {dir1/dir2/dir3 ...} 
```

#### touch

```shell
# 修改文件的访问时间和修改时间，若当前目录下没有同名文本，则创建一个新文本
touch {file}
```

#### grep

```shell
# 在指定文件file中搜寻指定字符串string
grep "{string}" {file}
# 忽略大小写
grep -i "{string}" {file}
# 在指定目录下的所有文件中递归搜寻指定的字符串
grep -r "{string}" {dir}
```

#### cp

```shell
# 复制source文件并将副本重命名为destination文件
cp {source_file} {destination_file}
# 复制文件夹
cp -r {source-folder} {destination-folder}
```

#### mv

```shell
# 将指定source文件或文件夹移至destination处，也可用于将source文件（夹）重命名为destination
mv {source} {destination}
```

#### rm/rmdir

```shell
# 删除指定的文件
rm {file}
# 递归删除指定目录下的所有子目录和文件
rm -r {dir}
# 强制删除
rm -f {file}
# 删除指定目录
rmdir {dir}
```

#### echo

```shell
# 在标准输出（屏幕）上打印content
echo {content}
# 以覆盖文本的方式写入文件
echo {content} > {file}
# 以在文本末尾追加的方式写入
echo {content} >> {file}
```

#### history

```shell
# 显示之前执行过的命令
history
```

#### tar

```shell
# 将指定的files添加进.tar压缩包
tar -cvf {archive-file.tar} {files}
# 提取指定压缩文件的内容到当前工作目录
tar -xvf {archive-file.tar}
# 查看指定压缩包内的内容
tar -tvf {archive-file.tar}
```

#### find

在指定目录下查找文件。

```shell
find {paths} {expression} {actions}
```

`expression` ：搜索条件

* `-name` 根据文件名称进行检索（区分大小写），如需忽略文件名的大小写可使用`-iname` 选项。
  `-name` 和 `-iname` 两个选项都支持通配符：
  *  `?` 表示任意一个单一的符号
  * `*` 表示任意数量（包括0）的未知符号

```shell
#查找 /usr 目录下所有文件名以 .txt 结尾的文件或目录
find /usr -name '*.txt' 
#查找 /usr 目录下所有文件名刚好为 4 个字符的文件或目录
find /usr -name '????' 
```

* `-path` 在搜索时匹配某个文件或目录的完整路径。

```shell
#查找 /usr 下所有文件名以 .txt 结尾的文件或目录，且该文件的父目录为 src
find /usr -path '*/src/*.txt' 
```

* `-type` 指定搜索的文件类型。
  * `f` 文件
  * `d` 目录
  * `l` 符号链接

```shell
#检索 /usr 下所有文件名以 java 开头的目录
find /usr -type d -name 'java*' 
```

* `-empty` 搜索空文件或空目录。

```shell
#检索用户主目录下所有的空目录
find ~ -type d -empty 
```

* `-user` 检索归属于特定用户的文件或目录。

```shell
#检索根目录下所有属主为 xiao 的文件
find / -type f -user xiao 
```

类似于 `-user`选项，`-group` 选项则可以根据文件或目录的**属组**进行检索。

`find` 命令支持对当前匹配条件进行反义。

```shell
#检索 /usr 下所有文件名不以 `.txt` 为后缀的文件
find /usr -type f ! -name '*.txt'
```

`actions`：对搜索结果执行命令

* `-delete` 删除搜索到的文件和目录

### 用户及权限管理

```shell
# 切换当前用户
su {user}
# 临时获取root用户权限，执行命令
sudo {command}
# 查询当前用户的用户名
whoami
# 更改当前用户的密码
passwd

```

#### chmod

更改用户对文件的权限。

> 文本权限
>
> * 读权限 (r) 对文本而言，具有读取文本内容的权限；对目录来说，具有浏览目录的权限。
> * 写权限 (w) 对文本而言，具有新增、修改文本内容的权限；对目录来说，具有删除、移动目录内文本的权限。
> * 可执行权限 (x) 对文本而言，具有执行文本的权限；对目录了来说该用户具有进入目录的权限。

```shell
chmod {mode} {file}
```

`mode` ：权限设定字串，格式为`[ugoa][[+-=][rwx]]`

* `u` 表示该文件的拥有者，`g` 表示与该文件的拥有者属于同一个用户组(group)，`o` 表示其他以外的人，`a` 表示三者皆是。
* `+` 表示增加权限，`-` 表示取消权限，`=` 表示唯一设定权限。
* `r` 表示可读取，`w` 表示可写入，`x` 表示可执行。

#### 进程管理

```shell
# 显示当前系统中运行进程的信息
ps
# 过滤出指定PID的进程
ps -ef | grep {PID}
# 实时显示进程状态
top
# 终止指定PID的进程
kill {PID}
# 强制终止
kill -9 {PID}
```

## vim

> vim 分为三种模式，分别是命令模式(Commend mode)，输入模式(Insert mode)和底线命令模式(Last line mode)。

### 命令模式

启动 vim 时会直接进入命令模式，此时键盘输入会被 vim 识别为命令，而非输入字符。

`i,I`：切换到输入模式，`i` 为从目前光标所在处输入，I 为在目前所在行的第一个非空格符处开始输入

`a,A`：切换到输入模式，`a` 为从目前光标所在的下一个字符处开始输入，`A` 为从光标所在行的最后一个字符处开始输入

`o,O`：切换到输入模式，`o` 为在目前光标所在的下一行处输入新的一行，`O` 为在目前光标所在的上一行处输入新的一行

`r,R`：切换到取代模式(Replace mode)，`r` 只会取代光标所在的那个字符一次，`R` 会一直取代光标所在的文字，直到按下 `ESC` 退出

`:` 切换到底线命令模式

#### 移动光标

`h,j,k,l` 光标向左，下，上，右移动一个字符，如果想要进行多次移动的话，如向下移动 30 行，可以使用 `30j` 或 `30↓` 的组合按键

`Ctrl + f` 屏幕向下移动一页，相当于 `Page Down`

`Ctrl + b` 屏幕向上移动一页，相当于 `Page Up`

`+/-` 光标移动到非空格的下一行/上一行

`n + space` `n` 表示数字，输入数字再按下空格光标会向右移动 `n` 个字符

`0` 光标移动到这一行的首字符处，相当于 `Home`

`$` 光标移动到这一行的末字符处，相当于 `End`

`G` 移动到这个文本的最后一行

`nG` 移动到这个文本的第 `n` 行

`gg` 移动到这个文本的第一行

`n + Enter` 光标向下移动 `n` 行

#### 搜索替换

`/word` 向光标下寻找一个名称为 `word` 的字符串

`?word` 向光标上寻找一个名称为 `word` 的字符串

`n` 重复前一个搜索动作，如 `/word` 后，按下 `n` 会继续向下寻找一个名称为 `word` 的字符串

`N` 与 `n` 相反，反向进行前一个搜索动作，如 `/word` 后，按下 `N` 会向上寻找一个名称为 `word` 的字符串

#### 删除、复制与粘贴

`x,X` 向后，前删除一个字符，相当于 `Del，Backspace`

`nx` `n` 为数字，连续向后删除 `n` 个字符

`dd` 删除光标所在的那一整行

`ndd` 删除光标所在的向下 `n` 行

`ncj` `n` 为数字，向下删除 `n` 行

`yy` 复制光标所在的那一行

`nyy` `n` 为数字，复制光标所在向下 `n` 行

`p, P` `p` 为将复制的数据粘贴在光标下一行，`P` 则为粘贴在光标上一行

`J` 将光标所在行与下一行合为一行

`u` 撤销

`Ctrl + r` 恢复撤销

`.` 重复前一个动作

### 底线命令模式

`q` 退出程序

`q!` 不保存对文件的修改强制退出程序

`w` 写入文件

`w!` 若文件属性为只读，强制写入文件

`wq` 写入文件后退出，`wq!` 为强制写入后退出

`ZZ` 相当于 `wq`

`ZQ` 相当于 `q!`

`w {file}` 将编辑的数据储存为名为 `file` 的文件

`n1,n2 w {filename}` 将第 `n1` 行到第 `n2` 行的内容储存为名为 `filename` 的文件

`r {filename}` 将 `filename` 文件的内容追加到光标所在行后面

`!{command}` 暂时离开 vim 到指令行模式下执行 `command` 命令的显示结果

`set nu` 显示行号

`set nonu` 与 `set nu` 相反，取消行号

# **Ubuntu**

<img src="img/logo/ubuntu_logo.png" alt="ubuntu_logo" style="zoom: 67%;" />

## 命令

### 软件安装

```shell
# 更新软件包索引
apt update
# 安装一个新软件包
apt install {package}
# 卸载一个已安装的软件包（保留配置文档）
apt remove {package}
# 卸载一个已安装的软件包（删除配置文档）
apt remove --purge {package}
# 删除包及其依赖的软件包
apt autoremove {package}
# 删除包及其依赖的软件包，及其依赖的软件包的配置文件
apt autoremove --purge {package}
```

### 系统管理

#### 防火墙

```shell
# 查看防火墙状态
ufw status
# 开启防火墙
ufw enable
# 制定规则，允许指定端口或服务访问
ufw allow 22/ssh
# 删除某条规则
ufw delete allow 22
# 关闭防火墙
ufw disable
```

## 设置

### root用户设置

Ubuntu 默认 root 用户是不能登录的，密码也是空的。

如果要使用 `su` 命令登录 root 用户，必须先使用 `sudo passwd root` 命令为 root 用户设置密码 。

### 静态 IP 设置

1. 设置虚拟机网络连接方式为 NAT 模式；
2. 编辑 `/etc/netplan/**.yaml` 文件；

3. 在 `**.yaml` 文件中添加以下内容，保存退出；

```yaml
network:
  version: 2
  renderer: NetworkManager
  ethernets:
    # 网卡名
    ens33:
      # 设置静态ip地址
      addresses: [192.168.xxx.xxx/24]
      # 设置网关地址
      gateway4: 192.168.xxx.2
      routes:
        - to: default
          via: 192.168.xxx.2
      # 设置DNS服务器地址
      nameservers:
        addresses: [192.168.xxx.2]
```

4. 使用 `netplan apply` 命令应用修改。

### 远程连接

```shell
# 安装 SSH
apt install ssh
```

## 软件安装

### JDK8

```shell
apt install openjdk-8-jdk
```

### MySQL

**1、从Ubuntu源仓库安装MySQL**

```shell
apt install mysql-server
```

安装完成后，MySQL 服务将会自动启动，验证 MySQL 服务器正在运行：

```shell
systemctl status mysql
```

**2、配置MySQL**

MySQL 安装文件附带了一个名为 `mysql_secure_installation` 的脚本，能够提高数据库服务器的安全性。

不带参数运行这个脚本：

```shell
sudo mysql_secure_installation
```

以下为配置项：

(1) 安装验证密码插件（用于测试 MySQL 用户密码的强度）

```shell
VALIDATE PASSWORD PLUGIN can be used to test passwords
and improve security. It checks the strength of password
and allows the users to set only those passwords which are
secure enough. Would you like to setup VALIDATE PASSWORD plugin?
Press y|Y for Yes, any other key for No: N
```

(2) 设置 MySQL root 用户密码

```shell
Please set the password for root here...
New password: 
Re-enter new password: 
```

(3) 删除匿名用户

```shell
By default, a MySQL installation has an anonymous user,
allowing anyone to log into MySQL without having to have
a user account created for them...
Remove anonymous users? (Press y|Y for Yes, any other key for No) : Y
```

(4) 禁止 root 从远程登录

```shell
Normally, root should only be allowed to connect from
'localhost'. This ensures that someone cannot guess at
the root password from the network...
Disallow root login remotely? (Press y|Y for Yes, any other key for No) : Y
```

(5) 删除 `test` 数据库并取消对它的访问权限

```shell
By default, MySQL comes with a database named 'test' that
anyone can access...
Remove test database and access to it? (Press y|Y for Yes, any other key for No) : Y
```

(6) 刷新授权表，让初始化后的设定立即生效

```shell
Reloading the privilege tables will ensure that all changes
made so far will take effect immediately.
Reload privilege tables now? (Press y|Y for Yes, any other key for No) : Y
```

**3、创建新用户并授权远程访问**

MySQL8.0 安装完成后 root 用户只支持 localhost 访问，若要远程访问需要添加一个新用户。

```shell
ufw allow 3306 # 关闭防火墙对 3306 端口的监听
vim /etc/mysql/mysql.conf.d/mysqld.cnf # 注释掉 `bind-address` 行
/etc/init.d/mysql restart # 重启 MySQL 服务
mysql -u root -p
mysql> create user 'peng'@'%'identified by '220824'; # 创建一个用户
mysql> grant all privileges on *.* to 'peng'@'%' with grant option; # 授权远程访问
mysql> flush privileges; # 刷新权限
```

### Redis

在线安装

```shell
apt install redis-server
```

安装完成后，Redis 服务器会自动启动，查看 Redis 服务器状态：

```shell
netstat -nlt | grep 6379
```

安装 Redis 服务器后，会自动地一起安装 Redis 命令行客户端程序。

```shell
# 启动 redis 客户端
redis-cli
# 停止 redis
/etc/init.d/redis-server stop
# 启动 redis
/etc/init.d/redis-server start
# 重启 redis
/etc/init.d/redis-server restart
```

设置允许远程访问：

```shell
# 关闭防火墙对 6379 端口的监听
ufw allow 6379
# 修改 Redis 配置文件 redis.conf：
# 1、注释掉 bind 127.0.0.1 ::1 配置项
# 2、将 protected-mode 配置项改为 no
sudo vim /etc/redis/redis.conf
# 重启 redis 服务
sudo /etc/init.d/redis-server restart
```

### Nginx

在线安装

```shell
sudo apt install nginx
```

安装完成后，Nginx 服务器会自动启动，验证 Nginx 服务已启动：

```shell
sudo systemctl status nginx
```

配置防火墙：

```shell
sudo ufw allow 'Nginx Full'
```

访问 `http://localhost`，显示默认 Nginx 加载页面，说明安装成功。

### RabbitMQ

RabbitMQ 需要 Erlang 环境，安装 Erlang：

```shell
sudo apt install erlang
```

在线安装 RabbitMQ：

```shell
sudo apt install rabbitmq-server
```

安装完成后，查看 RabbitMQ 运行状态：

```shell
sudo rabbitmqctl status
```

开启 RabbitMQ 的管理面板：

```shell
sudo rabbitmq-plugins enable rabbitmq_management
```

创建一个新用户：

```shell
sudo rabbitmqctl add_user {username} {password}
```

将管理员权限给予新创建用户：

```shell
sudo rabbitmqctl set_user_tags {username} administrator
```

### 解压

一、迷你小火车

```shell
apt install sl
sl
```

二、黑客帝国数据字节流

```shell
sudo apt install cmatrix
cmatrix -C yellow
```

## Tips

### 程序前后台切换

在 `Linux` 终端运行命令的时候，在命令末尾加上 `&` 符号，就可以让程序在后台运行。

```shell
./{程序名} &
```

如果程序正在前台运行，可以使用 `Ctrl+z` 选项把程序暂停：

```shell
# 查看所有运行的程序
jobs –l
# 将编号为number的程序放在后台运行
bg %[{number}]
# 将编号为number的程序放在前台运行
fg %[number]
# 终止运行编号为number的程序
kill %[number]
```

### 阿里云ECS服务器延长SSH连接时间

通过 SSH 连接阿里云 ECS 服务器，如果一段时间不操作，就会因为超时而断开连接，很不方便。可以通过设置 SSH 服务，延长超时时间：

修改 `/etc/ssh/sshd_config` 文件：

```
# ClientAliveInterval 0
# ClientAliveCountMax 3
// 去掉注释，修改为
// ssh server 每隔120秒发送一条信息给 c
ClientAliveInterval 120 
// 如果 client 没有响应，则判断一次超时，这个参数设置允许超时的次数
ClientAliveCountMax 3
```

保存后重启 SSH 服务：

```shell
sudo systemctl restart sshd.service
```

# VMware

<img src="img/logo/vmware_logo.jpg" alt="vmware_logo" style="zoom: 33%;" />

## VMware虚拟机三种网络模式

VMware 提供了三种网络工作模式，它们分别是：**Bridged（桥接模式）**、**NAT（网络地址转换模式）**、**Host-Only（仅主机模式）**。
打开 VMware 虚拟机，可以在选项栏的 `编辑` 下的 `虚拟网络编辑器` 中看到 `VMnet0（桥接模式）`、`VMnet1（仅主机模式）`、`VMnet8（NAT模式）`，`VMnet0` 表示的是用于桥接模式下的虚拟交换机；`VMnet1` 表示的是用于仅主机模式下的虚拟交换机；`VMnet8` 表示的是用于 NAT 模式下的虚拟交换机。
同时，在主机上对应的有 `VMware Network Adapter VMnet1` 和 `VMware Network Adapter VMnet8` 两块虚拟网卡，它们分别作用于仅主机模式与 NAT 模式下。在 `网络连接` 中我们可以看到这两块虚拟网卡，如果将这两块卸载了，可以在 VMware 的 `编辑` 下的 `虚拟网络编辑器` 中点击 `还原默认设置`，可重新将虚拟网卡还原。

### 一、Bridged（桥接模式）

<img src="https://note1145141919810.oss-cn-hangzhou.aliyuncs.com/VMware%E6%A1%A5%E6%8E%A5%E6%A8%A1%E5%BC%8F.png" style="zoom: 50%;" />

VMware 桥接模式，也就是将虚拟机的虚拟网络适配器与主机的物理网络适配器进行交接，虚拟机中的虚拟网络适配器可通过主机中的物理网络适配器**直接访问到外部网络**。**简而言之，这就好像在局域网中添加了一台新的、独立的计算机一样。因此，虚拟机也会占用局域网中的一个 IP 地址，并且可以和其他终端进行相互访问。**

如果想把虚拟机当做一台完全独立的计算机看待，并且允许它和其他终端一样的进行网络通信，那么桥接模式通常是虚拟机访问网络的最简单途径。

> 桥接模式下无需虚拟网卡，因为虚拟机直接使用物理机上的物理网卡 IP 作为网关；但虚拟机的网段必须和物理机保持一致。

### 二、NAT（地址转换模式）

<img src="https://note1145141919810.oss-cn-hangzhou.aliyuncs.com/VMwareNAT%E6%A8%A1%E5%BC%8F.png" style="zoom: 50%;" />

NAT(*Network Address Translation*) 意即网络地址转换。NAT 模式也是 VMware 创建虚拟机的默认网络连接模式。使用 NAT 模式网络连接时，**VMware 会在主机上建立单独的专用网络（私网），用以在主机和虚拟机之间相互通信**。虚拟机向**外网**发送的请求分组，都会交由 NAT 网络适配器加上特殊标记并**以主机的名义转发出去**，外网返回的响应分组，也是先由主机接收，然后交由 NAT 网络适配器根据特殊标记进行识别并转发给**内网**中对应的虚拟机，因此，虚拟机在外网中不必具有自己的 IP 地址。**从外部网络来看，虚拟机和主机在共享一个 IP 地址，默认情况下，外部网络终端也无法访问到虚拟机。**

> 在一台主机上只允许有一个 NAT 模式的虚拟网络。因此，同一台主机上的多个采用 NAT 模式网络连接的虚拟机也是可以相互访问的。

### 三、Host-Only（仅主机模式）

**仅主机模式，是一种比 NAT 模式更加封闭的的网络连接模式，它将创建完全包含在主机中的专用网络**。仅主机模式的虚拟网络适配器仅对主机可见，并在虚拟机和主机系统之间提供网络连接。相对于 NAT 模式而言，仅主机模式不具备 NAT 功能，**因此在默认情况下，使用仅主机模式网络连接的虚拟机无法连接到 Internet**（在主机上安装合适的路由或代理软件，或者在 Windows 系统的主机上使用 Internet 连接共享功能，仍然可以让虚拟机连接到 Internet 或其他网络）。

在同一台主机上可以创建多个仅主机模式的虚拟网络，**如果多个虚拟机处于同一个仅主机模式网络中，那么它们之间是可以相互通信的**；如果它们处于不同的仅主机模式网络，则默认情况下无法进行相互通信（可通过在它们之间设置路由器来实现相互通信）。



