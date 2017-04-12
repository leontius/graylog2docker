# graylog2docker

### 安装
docker 安装  
环境：centos 7.0 64位  
Graylog 官方提供了 docker 镜像：  
docker pull mongo:3  
docker pull elasticsearch:2  
docker pull graylog2/server:2.1.2-1  
docker-compose 拉起服务：    
```
version: '2'
services:
  mongo:
    image: "mongo:3"
    volumes:
        - /data/mongo:/data/db
  elasticsearch:
    image: "elasticsearch:2"
    volumes:
        - /data/elasticsearch:/usr/share/elasticsearch/data
    command: "elasticsearch -Des.cluster.name='graylog'"
  graylog:
    image: graylog2/server:2.1.2-1
    environment:
      GRAYLOG_WEB_ENDPOINT_URI: http://x.x.x.x:9000/api
    depends_on:
      - mongo
      - elasticsearch
    ports:
      - "9000:9000"
      - "514:514"
      - "515:515"
```
