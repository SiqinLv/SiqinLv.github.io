+ **删除所有wps 进程**
  ```sh
    kill -9 `ps -ef|grep wps|awk '{print $2}' 
  ```
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
 1. ```select * from model_repair_handbook where content REGEXP '\\.png(?!"\\/>|\\?Expires)'```
 2. 正则分组查询
  ```mysql
	SELECT * FROM 
	(
	select CONCAT("", REPLACE(extend_synonym_name, ',', "|"), "") as a from (select CONCAT(base_synonym_name,',',GROUP_CONCAT(extend_synonym_name)) as extend_synonym_name from base_synonym as b
	LEFT JOIN extend_synonym AS e
	ON b.base_synonym_id=e.base_synonym_id
	GROUP BY b.base_synonym_id ) AS t 
	) AS t2
	WHERE '检查行车时有哒哒声' REGEXP t2.a;
  ```
+  **有空格或特殊符文件拷贝 用双引号包起来**
+  ```cp /root/广本知识图谱数据/维修案例数据集/维修案例集0827/"16M缤智RU1后尾 门无法开启.docx" /root/lsq/new_day1/flask_file/common/```
+  **删除所有gunicron进程**
  ```sh
    kill -9 `ps -ef|grep gunicorn|awk '{print $2}'
   ```
+ **删除当前目录下的所有文件**
+  ```rm ./* -rf```
+  **jupyter 安装**
+  ```pip install jupyter```
+  运行 jupyter
+  前台运行：```jupyter notebook --ip=0.0.0.0 --port=8083 --allow-root```
+  后台运行：```nohup jupyter notebook --ip=0.0.0.0 --port=9999 --allow-root &```
+  推荐使用：```nohup jupyter lab --ip='0.0.0.0' --port=8888 --notebook-dir='./' --no-browser --allow-root &```
+   浏览器不弹出启动：
+  ```jupyter notebook --no-browser```
+  **windows下**:
  ```sh
	d:
	cd D:\lvsiqin\pycharm_code\jupyter
	conda activate langchain_env
	jupyter notebook
  ```

+ **jupyterlab 安装**
+  ```(python) pip install jupyterlab```
+ 进入python代码编辑：
+ ```from jupyter_server.auth import passwd```
+ ```passwd()```
+ 退出python后jupyterlab配置文件生成：
+ ```jupyter lab --generate-config```
+ 生成的配置路径一般在：
+ ```/root/.jupyter/jupyter_lab_config.py```
+ 指定路径下运行jupyterlab `mkdir -p /home/workspace`
+ jupyterlab 前台运行
+ ```jupyter lab --allow-root```
+ jupyterlab 后台运行
+ ```nohup jupyter lab --allow-root --port 8888 &```
+ jupyterlab 后台、指定ip、端口号及运行目录 运行
+ `nohup jupyter lab --ip='*' --port=8701 --notebook-dir='/home/workspace' --no-browser --allow-root &`


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
+ 代理结果检验: ```curl --proxy http://192.168.4.224:7891  https://www.google.com.hk/```

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

+ **模型服务运行：**
+ ```nohup gunicorn -w 3 -k gevent --threads 5 --worker-connections 100 --keep-alive 5  -b 0.0.0.0:8080 app_vllm240105_3:app &```
+ ```nohup gunicorn -w 3 --threads 5 --worker-connections 100 --keep-alive 5  -b 0.0.0.0:7777 JL_embedding_neo4j:app &```
+ ```nohup gunicorn -w 3 --threads 5 --worker-connections 100 --keep-alive 5  -b 0.0.0.0:8086 GB02:app &```
+  ```gunicorn -w 1 -b 0.0.0.0:8082 fileServer2:app```
+ gevent 没有的情况下需自行安装，否则就用以下方式启动
+  ** conda 环境切换
+  ```conda activate lsq```

+ **conda 虚拟环境添加到jupyter内核环境中**
+ 为已有的环境下载kernel文件：```conda install -n 已存环境名称 ipykernel```
+ 将该环境写入jupyter的kernel中：
+ ```python -m ipykernel install --user --name 环境名称 --display-name "你想在jupyter中显示的该环境的名称"```
+ 也可指定python路径 ```sudo $(which python) -m ipykernel install --user --name paddlepaddle_env_v2 --display-name "paddlepaddle_env_v2"```

+ 例如：`sudo /opt/conda/envs/paddlepaddle_env/bin/python -m ipykernel install --name paddlepaddle_env --display-name "paddlepaddle_env"`
+ **删除conda环境**
+ ```conda remove -n your_env_name --all```


+ **pip 国内镜像** 
    >- 豆瓣：-i https://pypi.douban.com/simple
    >- 阿里：-i http://mirrors.aliyun.com/pypi/simple/ --trusted-host mirrors.aliyun.com
    >- 清华：-i https://pypi.tuna.tsinghua.edu.cn/simple/
    >- 豆瓣：-i http://pypi.douban.com/simple/ --trusted-host pypi.douban.com

+ **安装neo4j**
+ ```pip install neo4j-driver```(本人这种用的比较多) 或 ```pip install py2neo```
+ **图谱删除所有**
+ ```MATCH (n) OPTIONAL MATCH (n)- [r]- () DELETE n,r```
  - **修改neo4j 标签：**
    ```sh
	MATCH (n:OldLabel)
	WITH n
	SET n:NewLabel
	REMOVE n:OldLabel
	RETURN n;
    ```
  - **图谱标签修改**
    ```match(n:`方案ID`) remove n:`方案ID` set n:`解决方案```
  - **图谱数据修改**
    ```sh
    例1：match(n) where n.name='测量EN27B–1针脚到前舱电器盒UH-6针脚之间导线是否导通。' and n.dtc='P001500'  set n.name='aa' return n
    例2：match(n) where n.name contains '23-09-15_15-19-02.png' set n.name='aa'
    ```
    
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
  	# 或使用
        pip freeze -> requirements.txt  # 环境导出
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

  

**向量数据库**
  ```sh
	1.pinecone(使用较多);
	2、weavviate;
	3.Faiss;
	4.chroma
  ```
**远程文件传输**
  - scp -r /data/lsq/code/llama2/Llama2-Chinese-main/ appuser@10.140.143.3:/data/lsq/code/llama2/Llama2-Chinese-main # -r为文件递归上传

- **指定cuda包环境路径**
  ```sh
    export LD_LIBRARY_PATH=/opt/anaconda3/envs/llama2_chinese/lib/python3.9/site-packages/nvidia/cuda_runtime/lib:$LD_LIBRARY_PATH
    export LD_LIBRARY_PATH=/opt/anaconda3/envs/llama2_chinese/lib/python3.9/site-packages/nvidia/cublas/lib:$LD_LIBRARY_PATH
  ```


- **解决conda环境问题**
- 使用```vim ~/.condarc```查看源
  ```base
	channels:
	- https://pypi.tuna.tsinghua.edu.cn/simple
	- https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/
	- https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/pro/
	- https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/pytorch/
	- https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge/
	- https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
	- https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
	- http://mirrors.aliyun.com/pypi/simple/
	- defaults
	show_channel_urls: true
  ```
  可用：```ssl_verify: false``` 和 ```show_channel_urls: true```

- 设置mysql排序结果的方式
  ```mysql
     sql select title,content from gb_gq_table where title like '%M8夏天开空调不制冷是什么原因%' or  title like '%夏天开空调%' or  title like '%空调%' order by case when title like '%M8夏天开空调不制冷是什么原因%' then 1 else 2 end limit 2
  ```
- **模型使用vllm推理**
  ```
  CUDA_VISIBLE_DEVICES=1  nohup python -m vllm.entrypoints.openai.api_server --model /data/jupyter_workspaces/wanglina/models/llama2-Chinese-13b-Chat_0221 --host 0.0.0.0 --port 6666 --tensor-parallel-size 1 --max-parallel-loading-workers 8 --tokenizer-mode auto &
  ```

- **手机端mlc-llm安装(目前没用到)**
  先创建conda环境：```conda create -n mlc-chat-venv -c mlc-ai -c conda-forge mlc-chat-cli-nightly```
  完整版环境安装：```conda create -n mlc-chat-venv -c conda-forge -c  mlc-ai -c mlc-chat-cli-nightly "cmake>=3.24" "llvmdev>=15" rust python=3.11```
  
- **再下载源码并安装**
  ```sh
	# 项目官地址:https://llm.mlc.ai/docs/install/tvm.html
	# clone from GitHub
	git clone --recursive https://github.com/mlc-ai/mlc-llm.git && cd mlc-llm/  # 在本地计算机上运行完毕后上传到服务器上，因为里面有很多github的依赖包
	# create build directory
	mkdir -p build && cd build
	# generate build configuration
	python3 ../cmake/gen_cmake_config.py
	# build `mlc_chat_cli`
	cmake .. && cmake --build . --parallel $(nproc) && cd ..
  ```
  查看路径：```llvm-config --libdir```
  ```cmake -G "Ninja" -DLLVM_ENABLE_PROJECTS="clang;clang-tools-extra;compiler-rt;" ../llvm```
  **重点**
  ```sh
	# controls default compilation flags
	echo "set(CMAKE_BUILD_TYPE RelWithDebInfo)" >> config.cmake
	# LLVM is a must dependency
	echo "set(USE_LLVM \"llvm-config --ignore-libllvm --link-static\")" >> config.cmake
	echo "set(HIDE_PRIVATE_SYMBOLS ON)" >> config.cmake
	# GPU SDKs, turn on if needed
	echo "set(USE_CUDA   OFF)" >> config.cmake
	echo "set(USE_METAL  OFF)" >> config.cmake
	echo "set(USE_VULKAN OFF)" >> config.cmake
	echo "set(USE_OPENCL OFF)" >> config.cmake
	echo "set(USE_LIBBACKTRACE OFF)" >> config.cmake

  	echo "set(DCMAKE_VERBOSE_MAKEFILE ON)" >> config.cmake
  ```
  **报-static-libstdc++时,编译解决方案为**
  ```g++ -std=c++11```
  启动：```python -m mlc_chat.rest --model llama2 --lib-path /data/lvsiqin/jupyter/mlc_llm/dist/prebuilt/Llama-2-13b-chat-hf-q4f16_1 --device 0 --host 0.0.0.0 --port 7777```

+ **使用vllm模型启动**
  ```
  
  ```
  模型启动，--model后的参数为模型路径，可根据需求更换
  ```
  CUDA_VISIBLE_DEVICES=1  nohup python -m vllm.entrypoints.openai.api_server --model /data/jupyter_workspaces/wanglina/models/llama2-Chinese-13b-Chat_0221 --host 0.0.0.0 --port 6666 --tensor-parallel-size 1 --max-parallel-loading-workers 8 --tokenizer-mode auto &
  ```
+ **docker 容器操作**
  - 下载、运行和启动mysql容器
    ```sh
      docker run -d --restart=always -p 3306:3306 --privileged=true  -e MYSQL_ROOT_PASSWORD=cihon --name mysql mysql:latest --character-set-server=utf8 --collation-server=utf8_general_ci
    ```
  - 下载、运行、启动并指定数据存储位置的mysql容器代码
    ```sh
      docker run --name mysql -p 3306:3306 --privileged=true --restart unless-stopped -v /mydata/mysql/log:/var/log/mysql -v /mydata/mysql/data:/var/lib/mysql -v /mydata/mysql/conf:/etc/mysql/conf.d -e MYSQL_ROOT_PASSWORD=123456 -d mysql:5.7
    ```
  - 下载、运行、后台启动、指定数据存储位置且容器异常退出时自动重启的mysql容器代码
    ```sh
      docker run --name mysql -d -p 3306:3306 --privileged=true --restart unless-stopped -v /data/tools/mysql/log:/var/log/mysql -v /data/tools/mysql/data:/var/lib/mysql -v /data/tools/mysql/conf:/etc/mysql/conf.d -e MYSQL_ROOT_PASSWORD=123456 mysql:5.7
    ```
  - ***启动neo4j***
    ```bash
      docker run -d --restart=always --name neo4j -p 7474:7474 -p 7687:7687 -v /home/neo4j/data:/data -v /home/neo4j/logs:/logs -v /home/neo4j/conf:/var/lib/neo4j/conf -v /home/neo4j/import:/var/lib/neo4j/import --env NEO4J_AUTH=neo4j/cihon2023 neo4j:latest```
    ```
    ```sh
      # langchain 中添加了-e 参数
      docker run -d --restart=always --name neo4j -p 7474:7474 -p 7687:7687 -v /home/neo4j/data:/data -v /home/neo4j/logs:/logs -v /home/neo4j/conf:/var/lib/neo4j/conf -v /home/neo4j/import:/var/lib/neo4j/import --env NEO4J_AUTH=neo4j/cihon2023  -e NEO4J_PLUGINS=\[\"apoc\"\] neo4j:latest
    ```
  - **启动nginx**
    ```sh
      docker run --name nignx -itd -p 8108:80 --restart=always -v /data/lsq/nginx/html:/usr/share/nginx/html -v /data/lsq/nginx/nginx.conf:/etc/nginx/nginx.conf -v /data/lsq/nginx/conf.d:/etc/nginx/conf.d -v /data/lsq/nginx/logs:/var/log/nginx nginx
    ```
 - **启动向量库**
   ```sh
	sudo docker run -d --name milvus_cpu_2.3.9 \
	-p 19530:19530 \
	-p 19121:19121 \
	-v /home/milvus/db:/var/lib/milvus/db \
	-v /home/milvus/conf:/var/lib/milvus/conf \
	-v /home/milvus/logs:/var/lib/milvus/logs \
	-v /home/milvus/wal:/var/lib/milvus/wal \
	milvus_lsq:v2.3.9
   ```
   
  
- **panddlepaddle服务启动**
  ```sh
    CUDA_VISIBLE_DEVICES=0,1 nohup python -u  -m paddle.distributed.launch --gpus "0,1" /data/PaddleNLP-develop/llm/run_pretrain.py /data/PaddleNLP-develop/llm/llama/pretrain-flagalpha_llama2_7b-tp2sd4_stage2.json --data_cache /data/checkpoints/ &
  ```
**BML:**
  ```vim /home/bml/.condarc```
**查看linux系统信息:**
  ```cat /proc/version```
**注意**
  ```sh
    # 镜像大模型启动时，需要配置--shm-size  32g 即共享内存大小，否则会报核错误
    docker run -idt  --shm-size  32g -v /data/jupyter_workspaces/lvsiqin/GB02/docker_img:/data  ppd_nvia_lsq:v1
  ```
**模型训练**
  ```bash
    docker run -it  --shm-size  32g -v /data/jupyter_workspaces/lvsiqin/GB02/docker_img:/data  -w /data/ ppd_nvia_lsq:v1 python3.10  -u  -m paddle.distributed.launch --gpus "2,3,4,5,6,7" /data/PaddleNLP-develop/llm/run_pretrain.py /data/PaddleNLP-develop/llm/llama/pretrain-flagalpha_llama2_7b-tp2sd4_stage2.json --data_cache /data/checkpoints/
  ```
**容器模型启动**
```bash
    docker run -it  -v /data/jupyter_workspaces/lvsiqin/GB02/docker_img:/data  -w /data/ ppd_nvia_lsq:v1 python3.10 -m paddle.distributed.launch --gpus "2,3,4,5,6,7" /data/PaddleNLP-develop/llm/flask_server.py --model_name_or_path /data/FlagAlpha/Llama2-Chinese-7b-Chat --port 8010 --flask_port 8011 --dtype "float16"
```

**BML:**
  ```vim /home/bml/.condarc```

**牛洲广本账号信息**
  - ***EasyConnect***
    > 用户名：`O-NIUZHOU`
    > 密  码：`Cihon@#01`
  - ***齐治科技***
    + 用户名：`O-NIUZHOU`
    + 密  码：`Ghac@654321`
  - ***CCE***
    + 网址：```https://cce.ghac.cn/cce```
    + 用户名：`o-niuzhou`
    + 密  码：`Ghac@111`
  - ***堡垒机***
    + 用户名：`o-niuzhou`
    + 密  码：`Ch@#01020304`

**BML 平台账号密码**
  + 网址：```https://cloud.ghac.cn/logon/LogonPoint/tmindex.html ```
  + 邮箱地址：O-SONGGUOPENG@ghac.cn
  + 用户名：`O-SONGGUOPENG`
  + 密  码：`Cihon}Ghac.cn0411!`
  + 广本邮箱地址：`https://sdp.ghac.cn/UniSSOView/#/login`
  + 广本邮箱：`user/pwd:O-SONGGUOPENG/Cihon}Ghac.cn1209!`
> 平台内部
  + 网址：```[https://cloud.ghac.cn/logon/LogonPoint/tmindex.html ](http://10.110.195.212:8080/)```
  + 用户名：`SONGGUOPENG`
  + 密  码：`ghac1103@Cihon`
**移动云文件传输**
```sh
  scp -r -P 2222 root@ip:/data/jupyter_workspaces/lvsiqin/GB02/ppd_nvida_lsq_v1.tar C:\Users\jiang\Downloads
```
**docker容器操作**
+ 拉取镜像：`docker pull nvidia/cuda:11.8.0-cudnn8-devel-ubuntu22.04`
+ 启动临时镜像: `docker run --name xlName -idt 镜像名称`
+ 复制代码到容器中: `docker cp /data/jupyter_workspaces/lvsiqin/GB02 7b826a822107:/data/`

**容器ubuntu内安装python环境**
- 1.更新系统：
    ```sh
      apt update
      apt upgrade
    ```
- 2.下载pythonrun
    ```sh
      wget https://www.python.org/ftp/python/3.10.3/Python-3.10.3.tgz
    ```
    - 2.1.安装依赖
      ```sh
        apt-get install zlib1g-dev # 可能不需要安装
        apt-get install libffi-dev libssl-dev
        apt-get install libsqlite3-dev
        apt-get install libbz2-dev
        apt-get install libffi-dev
        apt-get install liblzma-dev
        apt-get install xz-utils
      ```
- 3.解压&编译
    ```sh
      tar -xf Python-3.10.3.tgz
      cd Python-3.10.3
      ./configure --enable-optimizations --with-ssl --with-zlib --with-sqlite --with-tkinter --with-bz2 --with-lzma
      make -j $(nproc)
      make altinstall
    ```
- 4.验证：
    ```sh
      pip3.10 python3.10
    ```
- 5.安装vim命令
    ```sh
      apt install vim
    ```
**ubuntu 文件乱码解决**
- 1.确定字符集命令：`locale`
- 2.添加字符集到系统文件中`vim /etc/profile` 在最后一样加上：`export LANG=C.UTF-8`
- 3.编译：`source /etc/profile`

**查看容器内空间占用情况**
du -sh  /*
**卸载pip3.7下的所有不包括setuptools、PyGObject、python-apt的包**
- jupyter-client       7.3.0
- jupyter_core         4.12.0
- jupyter_packaging    0.12.3
- jupyter-server       1.6.4
- jupyterlab           3.3.4
- jupyterlab-pygments  0.2.2
- jupyterlab-server    2.10.3
- 指定pip路径进行包卸载：\jupyter-client\|jupyter_core\|jupyter_packaging\|jupyter-server\|jupyterlab\|jupyterlab-pygments\|jupyterlab-server\pip3.7 freeze | grep -v "pip3.7\|setuptools\|PyGObject\|python-apt\|jupyterlab\|jupyter-client\|jupyter_core\|jupyter_packaging\|jupyter-server\|jupyterlab\|jupyterlab-pygments\|jupyterlab-server\|packaging" | xargs pip3.7 uninstall -y

**容器扩容 `--shm-size`**,大模型训练是必须使用该参数，否则在没有任何错误的情况加容易报核错误
`docker run --name lm_tuning_docker -idt --shm-size  32g lm_tuning:v1`

**容器打包成镜像**
  ```
    docker commit -a "lsq" -m "model_train" 03a1579bc3b7 train:v1 
    docker commit -a "lsq" -m "model_train" 8f72a48c0da8 paddlepaddle_llama2_7:v1
  ```
**容器导出**
  ```
    docker save -o /data/local/docker/gb2_img_v1.tar gb2_img:v1
    docker save -o gb2_img:v0.tar gb2_img:v0
  ```

**广本2期模型训练：**
  服务器虚拟环境启动训练：
  ```sh
    sh /data/PaddleNLP-develop/llm/llama/run_trainer_tp4pp2.sh
  ```
  或使用
  ```sh
    CUDA_VISIBLE_DEVICES=6,7 python3.9 -u  -m paddle.distributed.launch --gpus "6,7" /data/PaddleNLP-develop/llm/run_pretrain.py /data/PaddleNLP-develop/llm/llama/pretrain-flagalpha_llama2_7b-tp2sd4_stage2.json --data_cache /data/checkpoints/
  ```
  容器启动训练
  ```sh
    docker run -it  --shm-size  32g -v /data/jupyter_workspaces/lvsiqin/GB02/docker_img:/data  -w /data/ ppd_nvia_lsq:v1 python3.10  -u  -m paddle.distributed.launch --gpus "2,3,4,5,6,7" /data/PaddleNLP-develop/llm/run_pretrain.py /data/PaddleNLP-develop/llm/llama/pretrain-flagalpha_llama2_7b-tp2sd4_stage2.json --data_cache /data/checkpoints/
  ```
  在BML平台容器启动训练：
  ```sh
    docker run -it  --shm-size  32g  -v /home/bml/storage/mnt/v-r7vzv7ek3r9s2amy/org/GB02/data:/data  -w /data/  ppd_nvia_lsq:v1 python3.10  -u  -m paddle.distributed.launch --gpus "2,3,4,5,6,7" /data/PaddleNLP-develop/llm/run_pretrain.py /data/PaddleNLP-develop/llm/llama/pretrain-flagalpha_llama2_7b-tp2sd4_stage2.json --data_cache /data/checkpoints/
  ```

- **容器服务启动**
  启动环境 必装：
  - > gradio flask
  1.启动方式1：内部测试启动：
  `docker run -idt -v /data/jupyter_workspaces/lvsiqin/GB02/docker_img:/data  -w /data/ -p 18888:18888 -p 18011:18011 ppd_nvia_lsq:v4`
  2.启动方式2：容器里面运行：
  ```sh
    nohup python3.10 -m paddle.distributed.launch --gpus "0" /data/PaddleNLP-develop/llm/flask_server.py --model_name_or_path /data/llama2-Chinese-13b-Chat_0221 --port 18888 --flask_port 18011 --dtype "float16" &
  ```
  3.启动方式3：服务器外部启动：
  ```sh
  docker run -it  -v /data/jupyter_workspaces/lvsiqin/GB02/docker_img:/data  -w /data/ ppd_nvia_lsq:v1 python3.10 -m paddle.distributed.launch --gpus "0" /data/PaddleNLP-develop/llm/flask_server.py --model_name_or_path /data/FlagAlpha/Llama2-Chinese-7b-Chat --port 8010 --flask_port 8011 --dtype "float16"
  ```
  1.CUP启动： python3.10 -m paddle.distributed.launch /data/PaddleNLP-develop/llm/flask_server.py --model_name_or_path /data/FlagAlpha/Llama2-Chinese-7b-Chat --port 7788 --flask_port 18011 --dtype "float32" # 特别慢，慎用
  
**可能需要设置下cuda路径** `export LD_LIBRARY_PATH="/usr/bin:/usr/local/cuda/lib64:$LD_LIBRARY_PATH"`  

**容器打包**
  ```sh
    docker commit -a "lsq" -m "model_train" 8f72a48c0da8 paddlepaddle_llama2_7:v1
  ```
**容器启动**
  ```sh
    docker run -w /data/ -v /data/jupyter_workspaces/lvsiqin/GB02/docker_panddle_llama2_7/run_trainer_tp4pp2.sh:/data/run_trainer_tp4pp2.sh_/paddlepaddle_llama2_7_docker/  --shm-size  32g paddlepaddle_llama2_7:v1 sh /data/run_trainer_tp4pp2_lsq.sh --gpus "2,3,4,5,6,7"
  ```
  在容器内部，可通过`python3.10 PaddleNLP-develop/llm/predictor.py --model_name /data/FlagAlpha/Llama2-Chinese-7b-Chat --inference_model --dtype float16`测试环境是否符合模型运行条件，否则对环境进行适配
**环境bug解决**
- cp /data/Paddle-develop/python/paddle/base/framework.py /usr/local/lib/python3.10/site-packages/paddle/base/framework.py # 来自官方源码
- cp /data/jupyter_workspaces/lvsiqin/GB02/Paddle-develop/python/paddle/base/framework.py /data/tools/anaconda3/envs/paddlepaddle_env/lib/python3.9/site-packages/paddle/base/framework.py -y 

**vll推理工具** `--env "HUGGING_FACE_HUB_TOKEN=<secret>"`
` docker 下载启动：
  ```sh
    docker run --runtime nvidia --gpus all     -v /data/jupyter_workspaces/lvsiqin/GB02/docker_img:/data    -p 8000:8000     --ipc=host --shm-size 5g  vllm/vllm-openai:latest  --model /data/FlagAlpha/Llama2-Chinese-7b-Chat
  ```
**已有容器上新建镜像容器2：** 进行容器叠加：
  - docker export <container-id> > container.tar
  - cat container.tar | docker import - <new-image-name>

**错误解决：**
  - libcublas.so.11: undefined symbol: cublasLtGetStatusString, versio…
  - 安装pytorch之后，import torch报错
  - libcublas.so.11: undefined symbol: cublasLtGetStatusString, version libcublasLt.so.11
  - 解决方法：
    >`pip uninstall nvidia_cublas_cu11`

**文件内容查找**
```sh
  grep -r "in_cinn_mode" /path/to/directory
```

**bml平台notebook部署** 不记得了，没权限没用过，pass掉
  - bmlmodel config -a 7cce4b232e624f47a834ab5d0ef8030f -s e77a1f1f0d384e338497b9e485281e4b
  - bmlmodel publish -n  gb02_text2text -v 1.0.0.0 -p version -l pymodel

**运行广本项目**
  ```sh
    cd /home/bml/mnt/data && gunicorn -w 1 -b 0.0.0.0:18086 GB02_bak:app
  ```
  添包且切换目录运行`pip install gunicorn && cd /home/bml/mnt/data && gunicorn -w 1 -b 0.0.0.0:18086 GB02_bak:app`
**本机虚拟机**
  - 账号：`root`
  - 密码：`123`
  > 登录cce:`cce  login https://cce.ghac.cn`
  - 用户名：o-niuzhou
  - 密码：Ch@#01020304
  > 齐治科技：
  - 用户名：O-SONGGUOPENG
  - 用户名：Cihon}Ghac.cn1209!
**向量库启动命令**
  - 容器启动：`docker run -d --name milvus_cpu_2.3.9 -p 19530:19530 -p 19121:19121 -v /home/milvus_mapping:/var/lib/milvus  milvus_lsq:v2.3.9`
  - 容器日志：`docker logs -f milvus_cpu_2.3.9`
**bug解决**
  - 原因：`Error while finding module specification for 'paddle.distributed.launch' (ModuleNotFoundError: No module named 'paddle')`
  - 结果：`pip install paddlepaddle-gpu -i https://mirror.baidu.com/pypi/simple`
**不用conda activate 环境名切换时，可用**
  - pip which 路径被改，环境切换方式：
  ```sh
    export PATH=/data/tools/anaconda3/envs/paddlepaddle_env/bin:$PATH
    export LD_LIBRARY_PATH="/data/tools/anaconda3/envs/paddlepaddle_env/lib:$LD_LIBRARY_PATH"
  ```
**paddlepaddle 判断GPU是否可用**
  ```python
    import paddle
    paddle.is_compiled_with_cuda()
  ```
**查看pip路径**
 - ```pip show pip``` 或 ```which pip```

**修改gunicron的python路径**
 - ```python
       vim /home/bml/storage/mnt/v-r7vzv7ek3r9s2amy/org/app/paddlepaddle_env_v2/bin/gunicorn
   ```
 - 强制重新安装 gunicorn： ```pip install --force-reinstall gunicorn```
 - 确认 gunicorn 的路径：```head -n 1 /home/bml/storage/mnt/v-r7vzv7ek3r9s2amy/org/app/paddlepaddle_env_v2/bin/gunicorn```
 - 检查 gunicorn 是否正常工作：```gunicorn --version```
 - 确定这三个在同一路径下：
   ```base
	which python
	which pip
	which gunicorn
   ```
 - 获得调试信息: ```gunicorn -w 1 -b 0.0.0.0:18086 run_v1:app --log-level debug```
