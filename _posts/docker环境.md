启动docker ： sudo systemctl start docker

卸载docker： yum remove docker-ce

查看docker状态：systemctl start docker

启动docker：systemctl start docker

查看docker版本：docker version

使用elasticsearch时，若无法启动es，可能是服务器重启后max_map_count值太小
查看max_map_count：cat /proc/sys/vm/max_map_count
设置max_map_count：sysctl -w vm.max_map_count=262144

若本地可访问，外网不可访问，可能是未设置跨域的问题：
docker exec -it elasticsearch /bin/bash （进不去使用容器id进入）

vi config/elasticsearch.yml

http.cors.enabled: true 
http.cors.allow-origin: "*"

安装:elasticsearch-head
#拉取镜像
docker pull mobz/elasticsearch-head:5

#创建容器
docker create --name elasticsearch-head -p 9100:9100 mobz/elasticsearch-head:5

#启动容器
docker start elasticsearch-head
or
docker start 容器id （docker ps -a 查看容器id ）

docker commit -m es创建及配置 -a lsq elasticsearch es_2:v2 # docker容器封装

index → db
type → table
document → row

docker run -d --name neo4j -p 7474:7474 -p 7687:7687 -v /home/neo4j/data:/data -v /home/neo4j/logs:/logs -v /home/neo4j/conf:/var/lib/neo4j/conf -v /home/neo4j/import:/var/lib/neo4j/import --env NEO4J_AUTH=none neo4j

docker run -d --name neo4j -p 7474:7474 -p 7687:7687 -v /home/neo4j/data:/data -v /home/neo4j/logs:/logs -v /home/neo4j/conf:/var/lib/neo4j/conf -v /home/neo4j/import:/var/lib/neo4j/import --env NEO4J_AUTH=none neo4j

docker run -d --restart=always --name neo4j -p 7474:7474 -p 7687:7687 -v /home/neo4j/data:/data -v /home/neo4j/logs:/logs -v /home/neo4j/conf:/var/lib/neo4j/conf -v /home/neo4j/import:/var/lib/neo4j/import --env NEO4J_AUTH=neo4j/cihon neo4j
