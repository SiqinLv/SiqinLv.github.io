## CENTEROS
> 1.安装 docker
>- `安装必要的一些系统工具 sudo yum install -y yum-utils device-mapper-persistent-data lvm2`
>- `添加软件源信息 sudo yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo`
>- `更新yum索引列表并安装Docker引擎 sudo yum makecache fast`
>- `yum索引列表没有更新可以直接使用 yum makecache` `sudo yum install docker-ce`
> 2.启动 Docker
>- `开启Docker服务 sudo service docker start`
> 2.测试 Docker
>- `测试是否安装成功 docker version`
