# 创建和配置 GNOME Boxes 虚拟机

具体方法参照以下帖子：

- [GNOME-BOXES虚拟机创建安装_gnome boxes-CSDN博客](https://blog.csdn.net/jxq1994/article/details/125823063)
- [Linux之地表最强虚拟机gnome-boxes](https://unbroken.blog.csdn.net/article/details/127274218?spm=1001.2101.3001.6650.1&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1-127274218-blog-92078057.235%5Ev32%5Epc_relevant_default_base3&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1-127274218-blog-92078057.235%5Ev32%5Epc_relevant_default_base3&utm_relevant_index=2)

## 在 Ubuntu 中安装 GNOME Boxes 虚拟机

在终端中执行以下命令来安装 GNOME Boxes：


```
sudo apt install gnome-boxes
```


## 下载 Windows 操作系统映像文件

从 [MSDN、工具站或者微软官方网站下载 Windows 操作系统的映像文件（.iso）](https://msdn.itellyou.cn/)。

## 安装 Windows 虚拟机

1. 打开 GNOME Boxes，并点击左上角的加号，选择创建虚拟机。
2. 选择下载的 Windows 操作系统映像文件（.iso）并开始安装过程。

## 安装增强工具

安装 Windows 系统后，需要安装一些增强工具以增加日常操作的便捷性。

### Linux 和 Windows 共享剪切板

下载 `spice-guest-tools` 和 `virtio-win-gt-x64.msi` 工具，并导入到 Windows 虚拟机中。然后在 Windows 系统下安装这两个软件。

- [spice-guest-tools-latest.exe 下载链接](https://www.spice-space.org/download/windows/spice-guest-tools/spice-guest-tools-latest.exe)
- [virtio-win-gt-x64.msi 下载链接](https://fedorapeople.org/groups/virt/virtio-win/direct-downloads/archive-virtio/virtio-win-0.1.217-2/virtio-win-gt-x64.msi)

### Linux 和 Windows 共享文件

在非虚拟机中下载 `spice-webdavd` 软件：

- [spice-webdavd-x64-latest.msi 下载链接](https://www.spice-space.org/download/windows/spice-webdavd/spice-webdavd-x64-latest.msi)

下载后导入到 Windows 虚拟机中，并进行安装。安装完成后重启虚拟机中的 Windows 系统。

重启后，在虚拟机的 Windows 系统中，点击右上方的三个点，选择“属性”，进入共享文件夹的设置。

点击加号，添加共享文件夹。添加完成后，在 Windows 的资源管理器“此电脑”中即可看到共享文件夹。


# 实践操作

### 打开软件之后选择下载好的iso文件 再配置一下给的内存和存储。

帖子来源：[https://zhuanlan.zhihu.com/p/625253859](https://zhuanlan.zhihu.com/p/625253859)
