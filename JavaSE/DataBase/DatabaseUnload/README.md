# 数据库的卸载
MySQL安装后，如果没有卸载干净，后面下载会很麻烦，可能一直无法正确安装
## 卸载步骤：
首先，先在服务（开始——>控制面板——>管理工具——>服务）里停掉MySQL的服务。打开控制面板-添加删除程序，找到MySQL，卸载。或者用360安全卫士来卸载也行。也可以用mysql的那个安装程序删除

把安装好的MYSQL卸载了，但这对于卸载MySQL来说这只是一半，还有重要的另一半是要清理注册表。我们要进入注册表在开始-运行里面输入regedit，打开注册表

找到关于MYSQL的项把他们都删除，要一个项一个项的查找把他们都删除，这样在安装的时候就可以了。其实注册表里MySQL的项就是这三项：

HKEY_LOCAL_MACHINE/SYSTEM/ControlSet001/Services/Eventlog/Application/MySQL

HKEY_LOCAL_MACHINE/SYSTEM/ControlSet002/Services/Eventlog/Application/MySQL

HKEY_LOCAL_MACHINE/SYSTEM/CurrentControlSet/Services/Eventlog/Application/MySQL（没有这个也没关系）

还有就是C:ProgramData文件夹下面的MySQL删除（ProgramData可能是隐藏文件夹，提前设置隐藏显示）

这样，把上面的四项删除了之后，MySQL就基本卸载完全了。

如果你还不放心的话，可以在C盘查找mysql，把相关的项都删除。


或者

1.在MySQL的安装目录中找到my.ini配置文件

2.如果没有修改过，那么在这个文件中找到 datadir="C/ProgramData/MySQL/MySQL Server 5.5/Data/" ，然后复制下来

3.控制面板--->程序卸载--->MySQL--->右键卸载

//现在还没有删除成功，现在用到我们刚刚复制的东西，那个是数据目录，在那个路径下存放着MySQL的数据文件，如果这个文件没有删除，再次安装也不会成功

4.在C/ProgramData路径下删除MySQL，这个文件夹是隐藏的，可以搜索或者显示影藏文件来找到
