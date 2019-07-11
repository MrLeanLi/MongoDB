# MongoDB
MongoDB安装 window7 64位操作系统
在windows下安装mongo文件有两种方法。第一种是下载.zip文件，进行解压安装；第二种方法是下载.msi文件进行安装。首先采用了第一种解压的方式安装，安装过程中提示电脑缺失libeay32.dll，废了半天劲也没弄好。于是采用了第二种方法。
第一步：首先下载安装文件，下载地址如下：
https://www.mongodb.com/download-center/community
第二步：安装，傻瓜式安装，没什么可说的，要自定义安装路径，安装过程选择custom，安装不要有中文。
第三步：手动建立mongodb的数据库文件以及日志文件的存放路径。注意，此处要建在磁盘根目录下：我再C盘根目录下建立一个MongoDB文件夹，在MongoDB文件夹中建立一个log文件夹，一个db文件夹。再log文件夹下建立一个文件，命名随意。我的文件是log.log。
第四步：配置环境变量，右击我的电脑--属性--高级系统设置--环境变量。在系统变量的path下，编辑，在最后边追加如下内容（C:\Program Files\MongoDB\Server\4.0\bin;），此处配置成自己的安装路径。
此处配置文成以后，最好测试一下，进入命令行，输入mongo,会有版本信息提示，说明配置成功。
第五步：打开命令行，输入(路径根据自己安装目录而定)
mongod --dbpath C:\MongoDB\db   
如果执行成功，会打印如下信息
2019-07-11T15:54:09.212+0800 I CONTROL  Hotfix KB2731284 or later update is not
installed, will zero-out data files
2019-07-11T15:54:09.229+0800 I JOURNAL  [initandlisten] journal dir=c:\data\db\j
ournal
2019-07-11T15:54:09.237+0800 I JOURNAL  [initandlisten] recover : no journal fil
es present, no recovery needed
2019-07-11T15:54:09.290+0800 I JOURNAL  [durability] Durability thread started
2019-07-11T15:54:09.294+0800 I CONTROL  [initandlisten] MongoDB starting : pid=2
488 port=27017 dbpath=c:\data\db 64-bit host=WIN-1VONBJOCE88
2019-07-11T15:54:09.296+0800 I CONTROL  [initandlisten] targetMinOS: Windows 7/W
indows Server 2008 R2
2019-07-11T15:54:09.298+0800 I CONTROL  [initandlisten] db version v3.0.6
……

第六步：测试，在浏览器链接处输入，http://127.0.0.1:27017
如果页面提示：
It looks like you are trying to access MongoDB over HTTP on the native driver port.
说明服务器已经启动


后续：如果想像mysql那样，把mongodb的服务添加到windows服务中，需要进一步的配置。
管理员身份运行 cmd.exe（命令行） 输入：mongod.exe --bind_ip 127.0.0.1 --logpath(和下边有一个空格)
"C:\MongoDB\log\log.log" --logappend --dbpath "C:\MongoDB\db" --port 27017 --serviceName "mongodb"（和下边有一个空格）
 --serviceDisplayName "mongodb" --install
进行上述步骤以后，以管理员方式运行cmd.exe,输入net start mongodb 回车，启动mongodb服务，net stop mongodb回车，
关闭mongodb服务。
