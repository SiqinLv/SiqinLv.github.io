+ **删除所有wps 进程**
+ ```kill -9 `ps -ef|grep wps|awk '{print $2}'```
+ **拷贝某个项目文件到某个目录下**
+ ```cp /root/lsq/code/维修案例集0827/??? /root/lsq/code/new_day1/flask_file/common/```
+ **拷贝所有项目文件到工程目录中**
+ ```cp /root/lsq/code/维修案例集0827/* /root/lsq/code/new_day1/upload/ -rf```
+ **查看cpu核数**
+ ```cat /proc/cpuinfo| grep "processor"| wc -l```
+ **查看文件个数**
+  ```ls -l |grep "^-"|wc -l```
+  **查看文件夹个数**
+  ```ls -l | grep "^d" | wc -l```
+  **mysql 正则查询**
+  ```select * from model_repair_handbook where content REGEXP '\\.png(?!"\\/>|\\?Expires)'```
+  **服务运行命令**
+  ```gunicorn -w 1 -b 0.0.0.0:8082 fileServer2:app```
+  **有空格或特殊符文件拷贝**
+  ```cp /root/广本知识图谱数据/维修案例数据集/维修案例集0827/"16M缤智RU1后尾 门无法开启.docx" /root/lsq/new_day1/flask_file/common/```
+  **删除所有gunicron进程**
+  ```kill -9 `ps -ef|grep gunicorn|awk '{print $2}'````
+ **删除当前目录下的所有文件**
+  ```rm ./* -rf```
+  **jupyter 安装**
+  ```pip install jupyter```
+  ```jupyter notebook --ip=0.0.0.0 --port=8083 --allow-root```
+  浏览器不弹出启动：
+  ```jupyter notebook --no-browser```
+ jupyterlab 安装
+  ```pip install jupyterlab```
+  python代码：```
    from jupyter_server.auth import passwd
    passwd()
    # Enter password:
    # Verify password:
     ```(python)

+ **pip 国内镜像**
+ https://pypi.douban.com/simple
+ 
