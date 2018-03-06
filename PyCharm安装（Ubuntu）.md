- 官网下载PyCharm，官网提供付费版和免费版：
https://www.jetbrains.com/pycharm/
- 下载好的是tr.gz压缩包，自行解压到软件安装目录中（随便一个目录）
    - 解压方法：
        - 1、右键菜单解压压缩文件安装包
        - 2、在压缩文件安装包文件夹下打开终端输入
    **sudo tar -zxvf 压缩文件名.tar.gz /目标文件夹**
- 进入解压后的文件夹/bin   在bin文件夹中打开终端输入  **sh ./pycharm.sh**
（这种方式打开PyCharm时若关闭终端则会杀掉Pycharm进程）
- 此后若想运行PyCharm则执行上一步即可。若想一劳永逸请看下一步
- **制作PyCharm启动快捷方式**
    - 使用以下命令创建快捷方式
```
1、在终端输入 sudo gedit /usr/share/applications/Pycharm.desktop 
2、 然后在创建好的Pycharm.desktop中输入：
    [Desktop Entry]  
    Type=Application  
    Name=Pycharm  
    GenericName=Pycharm3  
    Comment=Pycharm3:The Python IDE  
    Exec="解压后的文件夹/bin/pycharm.sh" %f(或者Exec=sh /解压后的文件夹/bin/pycharm.sh)  
    Icon=解压后的文件夹/bin/pycharm.png  
    Terminal=pycharm  
    Categories=Pycharm; 
```
- 在启动器中搜索Pycharm，启动即可。若搜索不到在/usr/share/applications文件夹中找到Pycharm.desktop 复制到桌面

