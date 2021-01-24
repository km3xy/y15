04.24 14:32
termux主题配色
sh -c "$(curl -fsSL https://html.sqlsec.com/termux-install.sh)"  


定制常用按键
在 Termux v0.66 的版本之后我们可以通过 ~/.termux/termux.properties 文件来定制我们的常用功能按键，默认是不存在这个文件的，我们得自己配置创建一下这个文件。

下面做尝试简单配置一下这个文件:

Bash
# 新建并编辑配置文件
vim ~/.termux/termux.properties
内容为：

Bash
extra-keys = [ \
 ['ESC','|','/','HOME','UP','END','PGUP','DEL'], \
 ['TAB','CTRL','ALT','LEFT','DOWN','RIGHT','PGDN','BKSP'] \
]
如果无法创建这个文件，那么得首先新建一下这个目录 mkdir ~/.termux

修改完成保存文件后，重启 Termux app生效配置：


vim ~/.termux/termux.properties


zsh 主题配色
编辑家目录下的.zshrc配置文件

Bash
$ vim .zshrc


robbyrussell
主题比较多，国光这里就不列举了，感兴趣大家可以一个个尝试去看看。 当然如果你是个变态的话，可以尝试random 主题,每打开一个会话配色主题都是随机的.

Bash
ZSH_THEME="random"
zsh 插件推荐
zsh 之所以受欢迎除了好看的配色以为，另一个原因就是强大的插件了。下面国光列举一款比较实用的插件的安装方法，更多强大的插件等待大家自己去探索。

autosuggestions
根据用户的平时使用习惯，终端会自动提示接下来可能要输入的命令，这个实际使用效率还是比较高的：

Bash
# 拷贝到 plugins 目录下
git clone git://github.com/zsh-users/zsh-autosuggestions $ZSH_CUSTOM/plugins/zsh-autosuggestions
在 ~/.zshrc 中配置：

Ini
plugins=(其他的插件 zsh-autosuggestions)

输入zsh命令生效配置:


效果图
可以看到国光我只敲了一个v后面的命令就自动提示补全了，这时候只要按右方向键，在 Termux 里面的快捷键是 音量加 + D，就可以直接补全命令了。

修改启动问候语
默认的启动问候语如下:


这个启动问候语在前期对于初学者有一定的帮助，但是随着你们 Termux 的熟悉，这个默认的问候语就会显得比较臃肿。编辑问候语文件可以直接修改启动显示的问候语:

Bash
vim $PREFIX/etc/motd
修改完的效果如下:


本文版本归国光所有 转载注明出处哦
这样启动新的会话的时候看上去就会简洁很多。什么你也想要这个效果？ 呐 下面是国光自己生成的，可以直接复制粘贴:

Ini
  _____                              
 |_   _|__ _ __ _ __ ___  _   ___  __
   | |/ _ \ '__| '_ ` _ \| | | \ \/ /
   | |  __/ |  | | | | | | |_| |>  < 
   |_|\___|_|  |_| |_| |_|\__,_/_/\_\
超级管理员身份
实际上 Termux 不需要 root 权限也可以折腾各种各样的操作的，大家不必对 root 抱有啥幻想，本文的操作基本上没有涉及到手机要用到 root 的地步。

手机没有root
利用proot可以为手机没有root的用户来模拟一个root的环境，这里主要是经典的 Linux 文件系统布局上的模拟。

Bash
pkg install proot -y
然后终端下面输入:

Bash
termux-chroot
即可模拟root环境，该环境模仿 Termux 中的常规Linux文件系统，但是不是真正的 root。


输入exit可回到普通用户的文件系统。

手机已经root
安装tsu，这是一个su的 Termux 版本，是一个真正的root权限，用来在termux上替代su，操作不慎可能对手机有安全风险。因为官方封装了，所以安装也很简单：

Bash
pkg install tsu -y
然后终端下面输入:

Bash
tsu
即可切换root用户，这个时候会弹出root授权提示，给予其root权限，效果图如下:


18年的老图了 将就着看吧

在管理员身份下，输入exit可回到普通用户身份。不过本文没有设计到 root 权限的操作，一些底层的工具可能才会需要，考虑到 root 的不安全性 和 那些工具的冷门性，国光这里就没有继续拓展。

开发环境
Termux 支持的开发环境很强，可以完美的运行 C、Python、Java、PHP、Ruby等开发环境，建议读者朋友们选择自己需要的开发环境折腾。

编辑器
写代码前总得折腾一下编辑器，毕竟磨刀不误砍柴工嘛。Termux 支持多种编辑器，完全可以满足日常使用需求。

Emacs
据说Emacs是神的编辑器，国光我这种小菜鸡还不会使用哎，但是 Termux 官方已经封装好了 Emacs了，我们安装起来就会简单很多:

Bash
pkg install emacs  
nano
nano 是一个小而美的编辑器。具有如下：打开多个文件，每行滚动，撤消/重做，语法着色，行编号等功能

同样安装起来也很简单：

Bash
pkg install nano
Vim
Vim 被称为编辑器之神，基本上 Linux 发行版都会自带 Vim，这个在前文基本工具已经安装了，如果你没有安装的话，可以使用如下命令安装：

Bash
pkg install vim
并且官方也已经封装了vim-python，对Python相关的优化。

Bash
pkg install vim-python
解决汉字乱码
如果你的Vim打开汉字出现乱码的话，那么在家目录(~)下,新建.vimrc文件

Bash
vim .vimrc
添加内容如下:

Ini
set fileencodings=utf-8,gb2312,gb18030,gbk,ucs-bom,cp936,latin1
set enc=utf8
set fencs=utf8,gbk,gb2312,gb18030
然后source下变量:

Bash
source .vimrc
效果图


Vim 配色
Termux Vim 自带了如下的配色：

Bash
ls /data/data/com.termux/files/usr/share/vim/vim82/colors

desert.vim    morning.vim    shine.vim    blue.vim      elflord.vim   murphy.vim     slate.vim    darkblue.vim  evening.vim   pablo.vim      industry.vim  peachpuff.vim  torte.vim    delek.vim     koehler.vim   ron.vim        zellner.vim   
配色可以自己一个个尝试一下，还是向上面的汉字乱码那样，编辑家目录下的.vimrc文件：

Bash
vim ~/.vimrc
新增如下内容：

Ini
set nu                " 显示行号
colorscheme desert    " 颜色主题
syntax on             " 打开语法高亮


下面是国光随便找的几个颜色主题效果，感兴趣的朋友可以自己一个个尝试：


slate

murphy

peachpuff
Apache
Apache是一个开源网页服务器软件，由于其跨平台和安全性，被广泛使用，是最流行的Web服务器软件之一。

安装 Apache
Bash
pkg install apache2
启动 Apache
Bash
apachectl start
然后浏览器访问: http://127.0.0.1:8080 访问是否成功启动：


Termux 自带的 Apache 的网站默认路径为：

$PREFIX/share/apache2/default-site/htdocs/index.html

停止 Apache
Bash
apachectl stop
重启 Apache
Bash
apachectl restart
Apache 解析 PHP
既然Apache、PHP、MySQL都成功安装的话，那么现在只要配置好 Apache 解析 PHP 之后就可以打造一个 Android 平台上的 LAMPP平台了。

安装 php-apache
默认的 Apache 是无法解析 PHP的，我们需要安装相应的包：

Bash
pkg install php-apache
配置 Apache
Termux 上的 Apache 默认配置文件的路径为:

$PREFIX/etc/apache2/httpd.conf

直接编辑配置文件:

Bash
vim /data/data/com.termux/files/usr/etc/apache2/httpd.conf
配置文件里面搜索 PHP 没有相关的模块，所以需要我们手动添加 PHP7 的模块:

Bash
LoadModule php7_module /data/data/com.termux/files/usr/libexec/apache2/libphp7.so 
并在刚刚这个语句下方添加解析器，内容如下:

Properties
<FilesMatch \.php$>
  SetHandler application/x-httpd-php
</FilesMatch> 
接着继续往下找配置文件里面配置默认首页的地方，我们添加 index.php 到默认首页的规则里面:

Properties
<IfModule dir_module>
  DirectoryIndex index.php index.html
</IfModule>
这表示网站目录的默认首页是 index.php，如果没有 index.php 系统会自动寻找 index.html做为默认首页了。

修改完 Apache 的配置文件后，记得使用 apachectl restart 重启 Apache 服务，然后这个时候回发现我们重启居然报错了：

Verilog
Apache is running a threaded MPM, but your PHP Module is not compiled to be threadsafe.  You need to recompile PHP.
AH00013: Pre-configuration failed
不要慌问题不大，下面来解决这个问题

解决 Apache PHP 报错
先找到如下行

Properties
LoadModule mpm_worker_module libexec/apache2/mod_mpm_worker.so
给他注释掉为:

Properties
#LoadModule mpm_worker_module libexec/apache2/mod_mpm_worker.so
然后找到如下行:

Properties
#LoadModule mpm_prefork_module libexec/apache2/mod_mpm_prefork.so
取消注释为:

Properties
LoadModule mpm_prefork_module libexec/apache2/mod_mpm_prefork.so
最终的示例图如下:



解析 PHP 测试
在 Apache 的网站根目录下，创建一个 index.php ，测试一下 phpinfo() 函数能否正常运行:

Bash
echo '<?php phpinfo(); ?>' > $PREFIX/share/apache2/default-site/htdocs/index.php
然后浏览访问: http://127.0.0.1:8080 查看效果:


OK
C
Termux 官方封装了 Clang，他是一个C、C++、Objective-C和Objective-C++编程语言的编译器前端。

安装 clang
Bash
pkg install clang
编译测试
clang 在编译这一块很强大，感兴趣的朋友可以去网上查看详细的教程，国光这里只演示基本的 Hello World使用。写一个Hello World的C程序，如下 hello.c:

C
#include <stdio.h>

int main(){
  printf("Hello World")
  return 0;
}
编辑完成后，使用 clang 来编译生成 hello 的可执行文件：

Bash
clang hello.c -o hello
￼
效果图
Java
Termux 原生编译JAVA只能使用 ecj (Eclipse Compiler for Java) 和 dx 了，然后使用 Android 自带的 dalvikvm 运行。如果想要完整体验JAVA环境的话，另一个方法就是 Termux 里面安装一个完整的 Linux 系统，然后在 Linux里面运行Java，安装系统部分下面文章会详细介绍，这一节国光只介绍最基本的操作。

安装编译工具
Bash
pkg install ecj dx -y
国光这里只演示基本的 Hello World 使用。写一个Hello World的 JAVA 程序，如下 HelloWorld.java:

Java
public class HelloWorld {
    public static void main(String[] args){
        System.out.println("Hello Termux");
    }
}
编译生成 class 文件
Bash
ecj HelloWorld.java
编译生成 dex 文件
Bash
dx --dex --output=hello.dex HelloWorld.class
使用 dalvikvm 运行
格式规范如下：dalvikvm -cp dex文件名 类名

Bash
dalvikvm -cp hello.dex HelloWorld
￼
效果图
MariaDB(MySQL)
MariaDB 是 MySQL 关系数据库管理系统的一个复刻，由社区开发，有商业支持，旨在继续保持在GNU GPL下开源。开发这个分支的原因之一是：甲骨文公司收购了 MySQL 后，有将 MySQL 闭源的潜在风险，因此社区采用分支的方式来避开这个风险。

安装 MariaDB
Termux 官方也封装了MariaDB，所以安装起来很方便：

Bash
pkg install mariadb

这里基本上会安装很顺利，但是早期用户可能出现安装失败的情况，如果安装失败的话，这个时候手动在配置目录下创建my.cnf.d文件夹即可：

Bash
$ cd /data/data/com.termux/files/usr/etc/
$ mkdir my.cnf.d
初始化数据库
早期的 Termux 安装完 MySQL是需要初始化数据库的，新版本在安装时候就已经初始化了数据库

Bash
mysql_install_db
2020年4月19日：国光今天安装的 MySQL 发现已经存在 mysql.user 表了，无需初始化：


启动 MySQL 服务
因为正常启动完成后，MySQL 这个会话就一直存活，类似与 Debug 调试一样，此时使用Ctrl + C -> 中止当前进程也无济于事，体验式就一点都不优雅，所以这里国光使用Linux自带的nohup命令将其放到后台启动。

Bash
nohup mysqld &

图片上这个17115此时就是mysqld的进程PID号，我们使用如下命令验证一下是否正确：

Bash
ps aux|grep mysql
可以看到果然是进程的 PID 号：


至于 nohup 运行的提示

Ini
nohup: ignoring input and appending output to `nohup.out'
这个是正常现象，无伤大雅，Termux 下就这样将就着用吧。

停止 MySQL 服务
Termux 下没有好的办法退出 MySQL 服务，只能强制杀掉进程了，使用如下命令格式可以轻松杀掉进程：

Bash
kill -9 PID

成功kill掉
当然每次查看进程的PID号，再杀掉进程有点繁琐了，实际上这一步可以直接这样操作：

Bash
kill -9 `pgrep mysql`
Awesome ! 优雅!

默认的两个用户
用户登录的前提是 MySQL 服务在后台运行，如果你按照上一小节操作把 MySQL kill 掉的话，请重新启动一下MySQL 服务

新版本的 Termux 安装初始化数据库的时候包含两个高权限用户，一个是无法访问的 root 用户


提示拒绝root登录
另一个用户就是 Termux 的用户名，默认密码为空，我们来登录看看：

Bash
mysql -u $(whoami)

可以成功登录 并执行SQL语句
那么这个无法登录的 root 用户该怎么办呢 ？不要着急 继续往下看

修改 root 密码
老版本的 Termux 的直接使用mysql_secure_installation可以设置密码，但是新版本的安全策略变更了 我们在设置密码的时候回提示当前密码不正确，所以这条路行不通了。

这里我们只能使用 MySQL 的另一个用户名，即 Termux 用户名登录，然后来修改 root 的密码，使用如下命令修改 root 密码:

Bash
# 登录 Termux 用户
mysql -u $(whoami)

# 修改 root 密码的 SQL语句
use mysql;
set password for 'root'@'localhost' = password('你设置的密码');

# 刷新权限 并退出
flush privileges;
quit; 


OK！ 如何和图片上差不的效果，那么修改 root 密码就成功了。

root 用户登录
修改完密码之后我们就可以美滋滋地使用 root 用户来登录了：

Bash
mysql -u root -p
Enter password: xxxxx（这里输入你的密码)

远程登录 MySQL
使用 ip a 后查看 IP 地址后，尝试电脑端远程访问 Termux 的数据库:


发现默认是无法成功连接的，这个时候我们需要到数据库手动开启 root 用户的远程访问权限:

这里的 P@ssw0rd 是我的 root 密码

Sql
grant all on *.* to root@'%' identified by 'P@ssw0rd' with grant option;
flush privileges;


执行完成后 尝试 PC 端远程过去看看:


Nginx
Nginx 是一个高性能的 Web 和反向代理服务器，Nginx 用的熟悉的话，下面搭建各种网站也就轻而易举了。

安装 Nginx
Termux 安装 Nginx 也很简单，一条命令即可：

Bash
pkg install nginx
安装完成后，国光的习惯是查看一下版本信息：


1.17.10 版本

测试 Nginx
测试检查 Nginx 的配置文件是否正常:

Bash
nginx -t


现在测试肯定是OK的，这个多用于我们修改完 Nginx 的配置文件后的检查。

启动 Nginx
早期版本的 Termux 需要在termux-chroot 环境下才可以成功启动 Nginx ，新版本的 Termux 可以直接启动，很是方便：

Bash
nginx
Termux 在 Nginx 上默认运行的端口号是 8080， 使用pgrep命令也可以查看 Nginx 进程相关的PID号。

然后手机本地直接访问http://127.0.0.1:8080 查看 Nginx 是否正常启动：


重启 Nginx
一般当修改完 Nginx 相关的配置文件时，我们需要重启 Nginx，使用如下命令即可重启:

Bash
nginx -s reload
停止 Nginx
方法一 原生停止
Bash
nginx -s stop
或者

Bash
nginx -s quit
quit 是一个优雅的关闭方式，Nginx在退出前完成已经接受的连接请求。Stop 是快速关闭，不管有没有正在处理的请求。

方法二 杀掉进程
只需三番钟，里造会干我一样，爱象节款游戏 扯远了，只需要1条命令，即可优雅的终止掉 Nginx 服务:

Bash
kill -9 `pgrep nginx`
貌似手机党 并不好敲 这个 ` 符号 =，= ，如果实在敲不出来，那就分两步走吧：

Bash
# 查询 nginx 进程相关的 PID 号
pgrep nginx

# 杀掉 查询出的 PID号进程
kill -9 PID
Nginx 解析 PHP
Termux 下的 Nginx 解析 PHP 这里单独拿出一级标题来叙述，成功解析的话,下面安装 wordpress等 PHP网站就会轻松很多。

安装 php-fpm
Nginx 本身不能处理 PHP，它只是个 Web 服务器，当接收到 PHP 请求后发给 PHP 解释器处理。Nginx 一般是把请求转发给 fastcgi 管理进程处理，PHP-FPM 是一个PHP FastCGI管理器，所以这里得先安装它：

Bash
pkg install php-fpm
安装完成顺便检查一下版本信息吧：


配置 php-fpm
编辑 php-fpm 的配置文件 www.conf:

Bash
vim $PREFIX/etc/php-fpm.d/www.conf
定位搜索 listen = 找到

Ini
listen = /data/data/com.termux/files/usr/var/run/php-fpm.sock
将其改为：

Ini
listen = 127.0.0.1:9000
？？？啥 你不会使用 vim 搜索 ㄟ(▔,▔)ㄏ 那就老老实实一个个翻页吧。

配置 Nginx
编辑 Nginx 的配置文件 nginx.conf:

Bash
vim $PREFIX/etc/nginx/nginx.conf
下面国光贴出配置好的完整配置文件，大家可以参考下面这些图，只需要2大步骤：

添加 index.php 到默认首页的规则里面

取消 location ~ \.php$ 这些注释，按照图片上的 提示修改：

Termux 里面的 Nginx 默认网站的根目为：

/data/data/com.termux/files/usr/share/nginx/html
如果想要修改默认路径的话 只需要在配置文件中 替换2处出现的这个路径即可

下面贴一份完整的配置文件：

Nginx

worker_processes  1;
events {
    worker_connections  1024;
}

http {
    include       mime.types;
    default_type  application/octet-stream;
    sendfile        on;
    keepalive_timeout  65;

    server {
        listen       8080;
        server_name  localhost;
        location / {
            root   /data/data/com.termux/files/usr/share/nginx/html;
            index  index.html index.htm index.php;
        }

        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   /data/data/com.termux/files/usr/share/nginx/html;
        }

        location ~ \.php$ {
            root           html;
            fastcgi_pass   127.0.0.1:9000;
            fastcgi_index  index.php;
            fastcgi_param  SCRIPT_FILENAME  /data/data/com.termux/files/usr/share/nginx/html$fastcgi_script_name;
            include        fastcgi_params;
        }
    }
}
测试 PHP 解析
Nginx 默认网站的根目录为：

Bash
/data/data/com.termux/files/usr/share/nginx/html
在这个网站根目录下新建 info.php 内容为：<?php phpinfo(); ?>

Bash
echo '<?php phpinfo(); ?>' > $PREFIX/share/nginx/html/info.php
启动服务
先启动 php-fpm 服务：

Bash
php-fpm
然后再启动 Nginx 服务

Bash
nginx
如果你的 Nginx 已经启动了的话，使用 nginx -s reload 重启 Nginx

访问测试
浏览器访问http://127.0.0.1:8080/info.php 来看看刚刚新建的测试文件是否解析了：


哇哦~ awesome
Nodejs
Node.js 是能够在服务器端运行 JavaScript 的开放源代码、跨平台 JavaScript 运行环境。

安装 Nodejs
nodejs-lts 是长期支持版本，如果执行 pkg install nodejs 版本后，发现 npm 报如下错误:

Bah
segmentation fault
那么这个时候可以尝试卸载当前版本 pkg uninstall nodejs 然后执行下面命令安装长期稳定版本:

Bash
pkg install nodejs-lts
安装完成后使用如下命令查看版本信息：

Bash
node -V
npm -V
Hello World
新建一个 hello.js 脚本，内容如下:

Javascript
console.log('Hello Termux');
然后尝试运行:

Bash
$ node hello.js
Hello Termux
http-server
http-server 是一个基于 Node.js 的简单零配置命令行 HTTP 服务器。

Bash
# 安装 http-server
npm install -g http-server

# 运行 http-server
http-server

尝试电脑端浏览器直接访问看看:


OK
安装报错
早期版本的 Termux 的 npm 安装一些包的时候会报如

盘上按Ctrl + L的效果一样，达到清屏的效果。

C

Vim
Vim 被称为编辑器之神









 

