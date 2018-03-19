# dYSM定位bug日志

1、打开终端输入以下路径

cd /Applications/Xcode.app/Contents/SharedFrameworks/DTDeviceKitBase.framework/Versions/A/Resources/

回车执行

2、打开以上路径文件夹，输入命令

open ./

可以看到下图文件夹。将symbolicatecrash文件拷出。这个文件是Xcode自带分析crash的程序文件


3、将刚刚找到的symbolicatecrash文件与xxx.app.dSYM文件以及xxx.crash文件放入同一个文件夹内。将打包出来的xxx.ipa文件后缀名直接改为zip解压。获取一个Payload文件夹将里面的app文件放入刚刚的文件夹内。同时也可以在获取dSYM文件的同级文件夹内找到Products文件夹，Products->Applictions->路径下的获取这个app文件。为方便下面描述，这里将含有这4个文件的文件夹称为“目标文件夹”


4、输入以下命令：

cd  “目标文件夹”的路径，比如：cd /Users/LayneWang/Desktop/未命名文件夹

5、输入命令：

ls

显示目标文件夹内所有内容

6、此步至关重要。以此输入以下命令

./symbolicatecrash  xxx.crash的文件路径  xxx.app.dYSM的路径  >  (已解析的崩溃日志).crash

这样输出的 (已解析的崩溃日志).crash即为解析后的日志，可以看到具体哪一行代码发生崩溃。

7、第6步终端可能会发生Error: "DEVELOPER_DIR" is not defined at ./symbolicatecrash line 60.的错误。

为了解决这一问题，需要再次输入以下命令

export DEVELOPER_DIR="/Applications/XCode.app/Contents/Developer"

这样就可以获得解析的日志了。
