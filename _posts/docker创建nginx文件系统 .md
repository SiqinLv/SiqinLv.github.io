# step 1: 安装必要的一些系统工具
sudo yum install -y yum-utils device-mapper-persistent-data lvm2
# Step 2: 添加软件源信息
sudo yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
# Step 3: 更新并安装 Docker-CE
sudo yum makecache fast
sudo yum -y install docker-ce
# Step 4: 开启Docker服务
sudo service docker start

使用docker下载nginx
1 docker search nginx 
2 docker pull nginx
3 docker 

docker images
查看所有镜像

docker ps -a
查看运行的docker服务

运行nginx
docker run -itd  nginx

查看运行的服务
docker ps

结果
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS         PORTS     NAMES
48b8344d681c   nginx     "/docker-entrypoint.…"   4 seconds ago   Up 3 seconds   80/tcp    friendly_noether

！注意48就是下面要用到的id

创建一个文件夹并复制刚才运行的服务到当前文件夹下
docker cp 48:/etc/nginx .


修改配置
cd conf.d/
vim default.conf

配置如下
server {
    listen       80;
    server_name  localhost;

    #access_log  /var/log/nginx/host.access.log  main;

    location / {
        root   /usr/share/nginx/html;
    }

    #error_page  404              /404.html;

    # redirect server error pages to the static page /50x.html
    #
    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   /usr/share/nginx/html;
    }

    # proxy the PHP scripts to Apache listening on 127.0.0.1:80
    #
    #location ~ \.php$ {
    #    proxy_pass   http://127.0.0.1;
    #}

    # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
    #
    #location ~ \.php$ {
    #    root           html;
    #    fastcgi_pass   127.0.0.1:9000;
    #    fastcgi_index  index.php;
    #    fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
    #    include        fastcgi_params;
    #}

    # deny access to .htaccess files, if Apache's document root
    # concurs with nginx's one
    #
    #location ~ /\.ht {
    #    deny  all;
    #}
}

#相关命令
#docker rm 服务名字
#docker stop 服务名字


配置好了之后 运行
docker run -itd -p 8001:80 -v /root/fileSystem/pdfImage/finalized_img:/usr/share/nginx/html/ -v /root/yx/tmp/nginx:/etc/nginx nginx
查看运行的服务内部文件夹
docker exec -it 服务名字 bash
cd /usr/share/nginx/html/
ls

如何访问搭建好的文件系统
ip:8001/R101-0103003.png
