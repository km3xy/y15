04.27 12:40
termux访问本地文件目录创建本地文件夹
不能越级访问文件目录

不能越级访问文件

访问本地文件

开启本地访问权限

termux-setup-storage

cd  //进入sd本地目录

ls  //访问目录命令查看目录文件夹


 ls   storage  //访问本地家目录下的storage
目录

cd  //进入sd本地目录



mkdir ~/storage/downloads/www

//在本地/storage/downloads/目录下创建www文件夹

mkdir ~/storage/downloads/www2

//在本地/storage/downloads/目录下创建www2文件夹



storage//本地家里下的文件夹




cat   xx.txt    //执行输出txt文件

python   xx.py//  执行输出py文件



cat  storage/downloads/www2/aa.txt



~ $ cd
~ $ ls
app     index.php        static
config  kodbox.1.19.zip  storage
data    plugins          www

~ $ ls storage/
dcim       movies   pictures
downloads  music   shared

~ $ ls storage/downloads                         QQMail   aa   aa.txt  'i Theme'   www   www2

——————————————————
~ $ ls storage/downloads/www2/

//查看storage/downloads/www2/下的文件
//aa.txt

——————————————————

~ $ cat  storage/downloads/www2/aa.txt

//执行输出aa.txt文件内容

