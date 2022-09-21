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
@ https://blog.csdn.net/qq_32101863/article/details/120344080#:~:text=%E4%BA%8C%E3%80%81%E6%93%8D%E4%BD%9C%E6%AD%A5%E9%AA%A4%201%201.%E6%8B%89%E5%8F%96%E9%95%9C%E5%83%8F%202%202.%E7%94%A8continuumio%2Fanaconda3%E9%95%9C%E5%83%8F%E5%88%9B%E5%BB%BA%E4%B8%80%E4%B8%AA%E5%90%8D%E4%B8%BAtest%E7%9A%84%E5%AE%B9%E5%99%A8%203%203.%E8%BF%9B%E5%85%A5test%E5%AE%B9%E5%99%A8%EF%BC%8C%E6%9F%A5%E7%9C%8Bconda%E4%BD%8D%E7%BD%AE,4%204.%E5%9C%A8%E6%9C%AC%E5%9C%B0%E7%8E%AF%E5%A2%83%E4%B8%AD%E5%B0%86%E6%9C%AC%E5%9C%B0%E7%8E%AF%E5%A2%83%E5%A4%8D%E5%88%B6%E5%88%B0docker%E4%B8%AD%205%205.%E5%9C%A8%E6%9C%AC%E5%9C%B0%E7%8E%AF%E5%A2%83%E4%B8%AD%E5%B0%86%E6%9C%AC%E5%9C%B0%E4%BB%A3%E7%A0%81%E5%A4%8D%E5%88%B6%E5%88%B0docker%E4%B8%AD%206%206.%E5%B0%86%E5%AE%B9%E5%99%A8%E4%BF%9D%E5%AD%98%E4%B8%BA%E9%95%9C%E5%83%8F%207%207.%E5%B0%86%E9%95%9C%E5%83%8F%E5%AD%98%E4%B8%BA%E5%8E%8B%E7%BC%A9%E5%8C%85
