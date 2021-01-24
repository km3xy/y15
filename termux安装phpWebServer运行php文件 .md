04.25 17:07
termux安装phpWebServer运行php文件


第一步安装php

安装PHP

Termux 官方封装了 PHP，所以我们安装起来就很方便：


pkg install php


安装完成后查看下版本信息：

php --version



自 PHP5.4 之后 PHP内置了一个 Web 服务器。在 Termux 下可以很方便地测试 PHP 文件

安装php后无需绑定任何组件，

直接创建目录创建文件，启动 WebServer后直接访问即可，http://127.0.0.1:8888




首先在家(~)目录下建一个www 文件夹，然后在www文件夹下新建一个index.php文件，内容为：<?php phpinfo();?>


完整的步骤如下:


# 新建 www 文件夹


mkdir ~/www

# 创建 index.php 文件

echo '<?php phpinfo();?>' > ~/www/index.php
编写完成index.php文件后，尝试使用 PHP 内置的 WebServer 直接启动:


# 进入家目录
cd ~

# 启动 WebServer
php -S 0.0.0.0:8888 -t www/
自己制定端口后，浏览器访问http://127.0.0.1:8888


如果打不开网页

重启  php -S 0.0.0.0:8888 -t www/

即可

https://www.sqlsec.com/2018/05/termux.html

用vim来打开修改PHP文件

vim  www/index.php

也可以用vim来创件新文件

vim  www/1.txt

用ls命令查看目录结构

ls   查看所有文件夹目录

ls  www  查看www下边的所有文件


vim  常用命令  i  进入输入模式

esc  退出输入模式，后，是命令行模式

命令行模式输入冒号  :x
:x  保存修改并返回

相当于:wq  返回  和   exit 命令




————分割线——————




用mkdir命令来创建文件夹


# 新建 www2 文件夹


mkdir ~/www2



可以用vim来创建新文件

vim  www2/1.txt



注意文件内容不能是空文件


如果保存的文件是空文件


ls  www2   就查不到


查看www2下面的文件


ls www2




















