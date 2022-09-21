## CENTEROS
> 1.安装 docker
>- `安装必要的一些系统工具 sudo yum install -y yum-utils device-mapper-persistent-data lvm2`
>- `添加软件源信息 sudo yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo`
>- `更新yum索引列表并安装Docker引擎 sudo yum makecache fast`
>- `yum索引列表没有更新可以直接使用 yum makecache` `sudo yum install docker-ce`

> 2.启动 Docker
>- `开启Docker服务 sudo service docker start`

> 3.测试 Docker
>- `测试是否安装成功 docker version`

> 4.镜像加速 Docker
>- 阿里云官网->控制台->产品与服务->搜索容器->选择容器镜像服务->镜像工具->选择对应系统进行操作 注意：这里注意registry-mirrors的地址每个人都是不一样的，要查看页面上显示的地址
>- 例：
```
>>- sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://gsi4aj17.mirror.aliyuncs.com"]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
```
* @参考文献：https://blog.csdn.net/m0_51338272/article/details/122801639 

> 1.镜像安装conda
>- 
