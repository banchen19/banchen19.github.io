# desktop

## 创建.desktop文件

打开文本编辑器，创建一个新的.desktop文件，文件名可以与AppImage的名称相同，例如navicat15.desktop。
```
nano ~/.local/share/applications/navicat15.desktop
```

## 输入内容
在.desktop文件中输入以下内容：
```
[Desktop Entry]
Name=Navicat 15
Comment=Navicat 15
Exec=/home/banchen/文档/NV_Sql_tools/tmp/navicat15.AppImage   
Icon=/home/banchen/文档/NV_Sql_tools/tmp/n15p/navicat-icon.png
Terminal=false
Type=Application
Categories=Developer;
```

请注意，上述内容中的Exec字段应该是您的navicat15.AppImage的完整路径。同样，如果您希望为Navicat指定一个图标，可以在Icon字段中提供图标文件的路径。
## 保存并关闭

保存并关闭文本编辑器。然后将保存了.desktop文件的目录添加到您的$PATH环境变量中，这样系统就能够在应用程序列表中找到它。

```
export PATH=$PATH:~/.local/share/applications
```
或者，您可以将.desktop文件复制到/usr/share/applications/目录下，这样所有用户都可以访问该应用程序。
```
sudo cp ~/.local/share/applications/navicat15.desktop /usr/share/applications/
```

添加权限
```
sudo chmod +x navicat15.desktop
```
## 完成
