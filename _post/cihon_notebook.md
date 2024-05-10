+ **删除所有wps 进程**
+ ```kill -9 `ps -ef|grep wps|awk '{print $2}'```
+ **拷贝某个项目文件到某个目录下**
+ ```cp /root/lsq/code/维修案例集0827/??? /root/lsq/code/new_day1/flask_file/common/```
+ **拷贝所有项目文件到工程目录中**
+ ```cp /root/lsq/code/维修案例集0827/* /root/lsq/code/new_day1/upload/ -rf```
+ **查看cpu核数**
+ ```cat /proc/cpuinfo| grep "processor"| wc -l```
+ **查看文件个数**
+  ls -l |grep "^-"|wc -l
+  **查看文件夹个数**
+  ls -l | grep "^d" | wc -l

+ **pip 国内镜像**
+ https://pypi.douban.com/simple
+ 
