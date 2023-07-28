# ubuntu22.04安装激活Navicat15详细教程

自己找合适的位置创建一个临时的文件夹 :

```
mkdir tmp && cd tmp
git clone https://gitee.com/hub-mirrors/keystone.git
git clone https://gitee.com/hub-mirrors/navicat-keygen-tools.git
```

安装所需环境

```
sudo apt install libcapstone-dev cmake build-essential rapidjson-dev libssl-dev
```

安装keystone,依次执行以下命令
```
cd keystone
mkdir build
cd build
../make-share.sh
sudo make install
sudo ldconfig
```

### 难点一 进入到文件夹 navicat-keygen-tools 修改 common 目录下的 RSACipher.hpp 文件
```
cd ../../  返回目录：navicat-keygen-tools
```
路径： common/RSACipher.hpp

原文：
```
复制109行和110行 将 == 后边的 0x10100000  改为 0x30000000（ubuntu22.04将openssl升级到了3.0.x），如果不改会报 Unexpected openssl version! 错误，这里用的gedit也可以用其他编辑工具修改

```
复制这个代码：
```
#elif (OPENSSL_VERSION_NUMBER & 0xffff0000) == 0x30000000     // openssl 3.0.x
            return RSA_bits(Get());
```
添加到原来的这个代码后面。

```
#elif (OPENSSL_VERSION_NUMBER & 0xffff0000) == 0x10100000     // openssl 1.1.x
            return RSA_bits(Get());
```
---
执行编译
```
make all
```
### 难点一回执：继续这个指令
```
ls bin
```
### 以检查navicat-keygen 和 navicat-patcher 都是否存在，如果不存在，那就是编译失败，你需回到 [难点一](#难点一-进入到文件夹-navicat-keygen-tools-修改-common-目录下的-rsacipherhpp-文件)


## 现在把你下载到的压缩包的东西解压到你命令所在的这个路径：【 tmp 】也就是我们一开始创建的临时目录

输入指令
```
ls 
```
执行后回执(检查当前文件夹是否有这些东西)
```
keystone  n15  navicat15-premium-cs.AppImage  navicat-keygen-tools libgio-2.0.so.0.5000.3 appimagetool-x86_64.AppImage
```
继续输入指令：
```
cd ..
mkdir n15
cd n15
```

---
挂载AppImage文件，并把所有的文件拷出来
```
sudo mount -o loop navicat15-premium-cs.AppImage ./n15
#mount: /home/shaun/Downloads/tmp/tmp/tmp/n15: WARNING: source write-protected, mounted read-only.
#只读的意思，不用管
cp -r n15 n15p
#卸载n15并删除
sudo umount n15 && rm -r n15
```
把 libgio-2.0.so.0.5000.3 复制到 n15p/usr/lib/ 并创建软链接
```
cp ./libgio-2.0.so.0.5000.3 ./n15p/usr/lib/
cd ./n15p/usr/lib/
ln -s libgio-2.0.so.0.5000.3 libgio-2.0.so.0
cd ../../../
```
开始破解

用navicat-keygen-tools/bin 内之前编译出来的的navicat-patcher文件，给刚刚解包好的n15p 目录打补丁

```
./navicat-keygen-tools/bin/navicat-patcher ./n15p
```
## 回车,你会看到一堆密钥以及私钥保存路径: [ /home/banchen/下载/baidu_dw/tmp/tmp/RegPrivateKey.pem ]，那么恭喜你，成功了一半！
```
#先给打包工具附执行权限
sudo chmod +x appimagetool-x86_64.AppImage
#打包
./appimagetool-x86_64.AppImage ./n15p navicat15.AppImage
```

可能遇到的问题： 缺少FUSE（Filesystem in Userspace）没遇到就不用管
---
解决办法：
```
sudo apt-get install libfuse2
```
继续运行指令
```
./appimagetool-x86_64.AppImage ./n15p navicat15.AppImage
ls
```
执行回执
```
appimagetool-x86_64.AppImage  libgio-2.0.so.0.5000.3  navicat15.AppImage             navicat-keygen-tools
keystone                      n15p                    navicat15-premium-cs.AppImage  RegPrivateKey.pem

```
双击运行n avicat15.AppImage
---

# 注意！注意！注意！断网！断网！断网！

继续执行指令
```
./navicat-keygen-tools/bin/navicat-keygen --text RegPrivateKey.pem
```
输入： 1 

输入： 1 

输入： 15

[*] Your name: aaa

[*] Your organization: bbb

复制你的密钥，我的是[ NAVA-MHDP-UT2B-**** ] 这种格式的
```
banchen@banchen-ubuntu22:~/下载/baidu_dw/tmp/tmp$ ls
appimagetool-x86_64.AppImage  libgio-2.0.so.0.5000.3  navicat15.AppImage             navicat-keygen-tools
keystone                      n15p                    navicat15-premium-cs.AppImage  RegPrivateKey.pem
banchen@banchen-ubuntu22:~/下载/baidu_dw/tmp/tmp$ ./navicat-keygen-tools/bin/navicat-keygen --text RegPrivateKey.pem
**********************************************************
*       Navicat Keygen (Linux) by @DoubleLabyrinth       *
*                   Version: 1.0                         *
**********************************************************

[*] Select Navicat product:
 0. DataModeler
 1. Premium
 2. MySQL
 3. PostgreSQL
 4. Oracle
 5. SQLServer
 6. SQLite
 7. MariaDB
 8. MongoDB
 9. ReportViewer

(Input index)> 1

[*] Select product language:
 0. English
 1. Simplified Chinese
 2. Traditional Chinese
 3. Japanese
 4. Polish
 5. Spanish
 6. French
 7. German
 8. Korean
 9. Russian
 10. Portuguese

(Input index)> 1

[*] Input major version number:
(range: 0 ~ 15, default: 12)> 15

[*] Serial number:
NAVA-MHDP-UT2B-**** # 别想着抄我的，每个人的生成的都不一样

[*] Your name: aaa    
[*] Your organization: bbb

[*] Input request code in Base64: (Double press ENTER to end)


```
复制秘钥回到软件界面注册，粘贴秘钥之后选手动激活

复制请求码

回到命令行，粘贴请求码 按两次回车
```
[*] Input request code in Base64: (Double press ENTER to end)
ZJalDQxbU8Xbb20t635eYEgNOWL+4yQq9y2lyy4Bc0HUvbl6e0pvzwIBUxVqONtmpFXayw9VlRkINZsy2p2DVGtAoiV/1SUX/gtqe0LmCiKvckWQy5JGx+bE9mfjSZBJwmJBOiYoMfAlpb4gYQlkOBHpimEETNJ2jcWiSZlegAVOe05pucPXXY0OXCUbtEs7RVppGJFC9c30Cmh9Gf/AEdqMUqZpOVlaqNEqx3wA这段加密了，别想着复制uJ3j0nCXQ7cpCuZg07foLv4KSxjrmJlmvJGJm5GneKhclTE0BeSZ6/A+tPm+S3+ajIIcOaibSREeBmy5L2G34RQCOiQg==

[*] Request Info:
{"K":"别想着复制", "DI":"别想着复制", "P":"linux"}

[*] Response Info:
{"K":"别想着复制","DI":"别想着复制","N":"aaa","O":"bbb","T":别想着复制}

[*] Activation Code:
GFqkx4lLD6I3iQJ+xu+pgPE1rMRB2cjvJWs+eZ720AxlRnNHpFSlxn2bYSMiUwFCVUckj9ziT+f54FzKvTGjrtHEceSiA/别想着复制/IAJ097bPKE9LGNL+sZ+l4vds5G4vWhqWuWbrULEqAOEP6i7XfTCjgdWxllLg73CHAGZdFN8u3ddh7bGMDt3pGlZnx+7LYWj40ufaSlNrX4nHQKY0E99SzbQ9ZrnYkz+kbdVr+mUhD1kIih0PuOdmw==

```
生成激活码之后复制 Activation Code 给的密钥

切换回软件 将激活码粘贴到框内点击ok，提示激活成功

可参考其他教程将AppImage添加到程序列表

---

资料来源：https://www.bilibili.com/read/cv18230089/

资料来源：https://www.bilibili.com/read/cv6547509?from=search&;spm_id_from=333.337.0.0

资料来源：https://chat.openai.com/