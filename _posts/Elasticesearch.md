- Elasticesearch集群（cluster）：
- 原生就实现了集群，融合了复制集和分片。对每个分片来说，都可以作为他的副本，做他从的机器，从而达到备份和高可用的作用。
- curl
  - curl -x http请求方式 请求的路径url
  - 带请求头：curl -X http请求方式 请求的路径url -H 请求头字段 -d 请求体数据
    - 例:curl -X http请求方式 请求的路径url -H 'Content-Type:application/json' -d 请求体数据
    - curl -X GET 127.0.0.1:9200/_cluster/health 或 curl -X GET 127.0.0.1:9200/_cluster/health （get的话可以去掉get字段，因为默认为它）
    - curl -X PUT 127.0.0.1:9200/articles -H 'Content-Type:application/json' -d '
    {
    }
    '
    - 查询服务器状态：curl 127.0.0.1:9200/_cluster/health或curl 127.0.0.1:9200/_cluster/health?pretty（格式化显示）
