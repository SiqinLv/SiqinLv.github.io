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
+  **查看文件夹大小**
+  ```du -h --max-depth=1```
+  **查看指定文件夹大小**
+  ```du -h --max-depth=1  /home```
+  **mysql 正则查询**
+  ```select * from model_repair_handbook where content REGEXP '\\.png(?!"\\/>|\\?Expires)'```

+  **有空格或特殊符文件拷贝 用双引号包起来**
+  ```cp /root/广本知识图谱数据/维修案例数据集/维修案例集0827/"16M缤智RU1后尾 门无法开启.docx" /root/lsq/new_day1/flask_file/common/```
+  **删除所有gunicron进程**
+  ```kill -9 `ps -ef|grep gunicorn|awk '{print $2}'````
+ **删除当前目录下的所有文件**
+  ```rm ./* -rf```
+  **jupyter 安装**
+  ```pip install jupyter```
+  运行 jupyter
+  前台运行：```jupyter notebook --ip=0.0.0.0 --port=8083 --allow-root```
+  后台运行：```nohup jupyter notebook --ip=0.0.0.0 --port=9999 --allow-root &```
+   浏览器不弹出启动：
+  ```jupyter notebook --no-browser```
+ jupyterlab 安装
+  ```(python) pip install jupyterlab```
+ 进入python代码编辑：
+ ```from jupyter_server.auth import passwd```
+ ```passwd()```
+ 退出python后jupyterlab配置文件生成：
+ ```jupyter lab --generate-config```
+ 生成的配置路径一般在：
+ ```/root/.jupyter/jupyter_lab_config.py```
+ jupyterlab 前台运行
+ ```jupyter lab --allow-root```
+ jupyterlab 后台运行
+ ```nohup jupyter lab --allow-root --port 8888 &```

+ 访问方式：```http://192.168.4.225:8891```
+ **文件压缩 linux unzip 中文解压缩**
+  指定解压编码：-O:```unzip -O gbk *.zip```
+  指定解压路径 -d：```unzip -O GBK 影酷_A58_20230116.zip -d ../../unzip文件/酷影/```
+  **文件压缩**
+  -r(文件递归)，-f(不显示提示信息)：```zip -rf zipunzip.zip GM6 GM8 GS8 影豹 影酷```
+  **删除乱码的文件**
+  查看当前目录下的文件```ls -i```
+ 删除乱码文件 ```find -inum 乱码目录前的数字编号 -delete```
+ 删除乱码文件夹 ```find -inum 乱码目录前的数字编号 -exec rm -rf {} \```

+ **安装pyaudio时正确流程**
+ ```sh
	sudo yum install portaudio-devel
	pip install pyaudio
  ```

+ **服务器安装声卡 目前服务器上都无声卡驱动，大概率无法实现**
+ - 查看音屏文件
  - ```dmesg | grep -i audio``` ```lsmod | grep snd```
  - 安装依赖包
  - ```yum install portaudio-devel```
  - ```pip install pyaudio```
  - 查看音频信息
  - lspci
  -  安装pavucontrol，使其命令可用
  -  ```yum install pavucontrol```
  -  安装yum install jackd时报错，解决方法：
  -  ```sh
		yum groupinstall "Development Tools"   
		yum install libtool libtool-ltdl-devel libsndfile-devel
		wget https://github.com/jackaudio/jack2/archive/v1.9.22.tar.gz
		tar -xf jackd-v1.9.22.tar.gz
		cd jack2-1.9.22/
		./waf configure
		./waf
      ```


+ **安装wechat-on-chatpgt时注意**
+ python==3.8.*
+ urllib3需要改为：```pip install urllib3==1.25.11``` 否则1.26.0版本的urllib3添加了HTTPS支持，但代理服务器不支持HTTPS，所以报错（pip走代理报错也差不多类似原因，具体请参考上文，有详细解读）


+ **服务器安装代理后访问方式：
+ ```curl --proxy http://127.0.0.1:7890  https://www.google.com.hk/```

+ **若误操作~/.bashrc，并~/.bashrc source了，可通过python代码修改并source**
+ ```py
	import os
	with open('/root/.bashrc') as f:
	    rc = r.read()
	#  修改rc文件
	with open('/root/.bashrc','w') as f:
	    rc = f.write(rc)
	import subprocess
	subprocess.run(['/bin/bash', '-c', 'source ~/.bashrc'])或subprocess.run(['/bin/bash', '-c', 'source ~/.bashrc'], shell=True)
  ```
+ 但在已开启的页面无效，另启一个新页面，即可正常使用
  
+ **MySQL 错误代码:1055 解决方案（推荐！！)**
+ 在mysql查询控制台：```SET sql_mode = 'STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION'```

+ **虚拟环境备份：**
+ ```conda pack -n env_name -o env_name.tar.gz```
+ 启动docker容器，将压缩包拷贝进去
+ ```cp llama2_lora_train_env.tar.gz 085a5c497b7a:/opt/conda/envs/```

+ **目前用的gunicron较多的版本：**
+ ```gunicorn==20.0.4```
+ 注意在使用gunicorn前，需要将flask代码中的app.run部分的代码注释掉

+ **模型运行：**
+ ```nohup gunicorn -w 3 -k gevent --threads 5 --worker-connections 100 --keep-alive 5  -b 0.0.0.0:8080 app_vllm240105_3:app &```
+ gevent 没有的情况下需自行安装，否则就用以下方式启动
+ **服务运行命令**
+  ```gunicorn -w 1 -b 0.0.0.0:8082 fileServer2:app```
+  ** conda 环境切换
+  ```conda activate lsq```

+ **conda 虚拟环境添加到jupyter内核环境中**
+ 为已有的环境下载kernel文件：```conda install -n 已存环境名称 ipykernel```
+ 将该环境写入jupyter的kernel中：
+ ```python -m ipykernel install --user --name 环境名称 --display-name "你想在jupyter中显示的该环境的名称"```

+ **pip 国内镜像** 
    >- 豆瓣：-i https://pypi.douban.com/simple
    >- 阿里：-i http://mirrors.aliyun.com/pypi/simple/ --trusted-host mirrors.aliyun.com
    >- 清华：-i https://pypi.tuna.tsinghua.edu.cn/simple/
    >- 豆瓣：-i pip install py2neo -i http://pypi.douban.com/simple/ --trusted-host pypi.douban.com

+ **安装neo4j**
+ ```pip install neo4j-driver```
+ **清空GPU显存**
+ 查看显存看空间：```nvidia-smi```
  >- 查看显存占用情况：```fuser -v /dev/nvidia*```
	>- 清空所有占用显存的进程：```sudo fuser -v /dev/nvidia* |awk '{for(i=1;i<=NF;i++)print "kill -9 " $i;}' | sudo sh```
	>- 要实时显示GPU占用情况，你可以使用以下命令运行```nvidia-smi```或```watch -n 1 nvidia-smi  或 nvitop --colorful```
  	>- fuser命令需要使用```yum install -y psmisc```安装,其中还包括killall、pgrep包，-y为自动确定

+ **对源码的安装**
+ - 对源码中```setup.py```文件安装
  - 1.先下载你要安装的包，并解压到磁盘下；
  - 2.<b style="color: deepskyblue">在linux中进入到该文件的setup.py 目录下</b> 或 <b style="color: deepskyblue">在window上打开cmd，并切换到该目录下；</b>
  - 3.执行：```python setup.py build```
  - 4.执行：``` python setup.py install```
+ **Linux设置用户登录超时(闲置时间): ```vim /etc/profile```,具体操作可自行百度**
+ **要将Conda虚拟环境打包并在其他电脑上使用，您可以执行以下步骤：**
+ ```sh
	conda activate your_environment_name
	conda list --export > environment.yml
	# 安装yum环境的包
	conda env create -f environment.yml
	conda env update -f environment.yml
  ```
+ **使用conda 指定环境去安装包**
+ conda install conda-pack
+ conda-pack -n llama2_lora_train -o llama2_lora_train.tar.gz
+ **解压缩**
  ```sh
  mkdir -p my_env # -p 是递归创建文件夹
  tar -xzf my_env.tar.gz -C my_env # 解压tar.gz包，-C为指定路径
  ```
+ **或打包conda环境的文件夹**
+ ```conda pack -p /explicit/path/to/my_env```
+ ** 文件操作
  - 压缩：```tar -czvf archive.tar.gz /path/to/folder```
  - 解压：```tar -xzvf archive.tar.gz```
  - 解压：```tar -xzvf archive.tar.gz -C /path/to/destination```
+ **容器操作**
+ - 容器提交为镜像：```docker commit my_container my_image:tag```
+ - 镜像打包为tar包：```docker save -o my_image.tar my_image:tag```
+ - 加载打包的镜像：```docker load -i my_image.tar```
+ - 容器运行：```docker run -d --name my_new_container my_image:tag```

+ **显示可用的conda 源**```conda config --show channels```
+ **查看核修改conda 包安装的超时时间**```conda config --show-sources```
+ 
