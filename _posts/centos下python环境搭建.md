![image-20221015112741657](C:\Users\jiang\AppData\Roaming\Typora\typora-user-images\image-20221015112741657.png)

1.广本图谱环境搭建：

wps:wget https://wdl1.cache.wps.cn/wps/download/ep/Linux2019/9615/wps-office-11.1.0.9615-1.x86_64.rpm

sudo rpm -Uvh wps-office-11.1.0.9615-1.x86_64.rpm 

若依赖检测失败：

wget http://mirror.centos.org/centos/8/AppStream/x86_64/os/Packages/mesa-libGLU-9.0.0-15.el8.x86_64.rpm

sudo rpm -Uvh mesa-libGLU-9.0.0-15.el8.x86_64.rpm

sudo yum install libX*

解决后安装wps：sudo rpm -Uvh wps-office-11.1.0.9615-1.x86_64.rpm 

若运行代码时出现：ImprotError:libXrender.so,1:cannot open ...

解决方案：yum whatprovides xxx 

```
man yum whatprovides # 用于确定哪个软件包提供某些功能或文件。只需使用特定名称或文件glob语法通配符来列出提供该功能或文件的可用或安装的软件包。
```

使用`yum whatprovides libXrender.so.1` `根据信息，使用 yum 进行依赖库的安装，**注意：如果是 Centos 的话，去掉 `.i686` 再进行安装，如果系统时 `x64` 位系统需要把 `.i686`改成 `.x86_64`**`

缺少GLIBC_2.18，参数如下内容得到解决：

curl -O http://ftp.gnu.org/gnu/glibc/glibc-2.18.tar.gz
tar zxf glibc-2.18.tar.gz 
cd glibc-2.18/
mkdir build
cd build/
../configure --prefix=/usr
make -j2
make install
