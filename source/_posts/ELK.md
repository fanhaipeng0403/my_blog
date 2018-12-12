---
title: ELK stack 
date: 2018-12-17 15:14:50
tags: ELK
---

# Docker-compose 配置

* [项目地址](https://github.com/fanhaipeng0403/docker-elk-filebeat)


```

version: '2'

services:

  elasticsearch:
    build: elasticsearch/
    volumes:
      - ./elasticsearch/config/elasticsearch.yml:/usr/share/elasticsearch/config/elasticsearch.yml
      - /mnt/data/elasticsearch/data:/usr/share/elasticsearch/data
    ports:
      - "9200:9200"
      - "9300:9300"
    environment:
      ES_JAVA_OPTS: "-Xmx2g -Xms2g"
    networks:
      - elk

  logstash:
    build: logstash/
    volumes:
      - ./logstash/config/logstash.yml:/usr/share/logstash/config/logstash.yml
      - ./logstash/pipeline:/usr/share/logstash/pipeline
    ports:
      - "5044:5044"
    environment:

      LS_JAVA_OPTS: "-Xmx2g -Xms2g"

    networks:
      - elk
    depends_on:
      - elasticsearch

  kibana:
    build: kibana/
    volumes:
      - ./kibana/config/:/usr/share/kibana/config
    ports:
      - "5601:5601"
    networks:
      - elk
    depends_on:
      - elasticsearch


  nginx:
    image: nginx
    restart: always
    ports:
      - 80:80
    volumes:
      - ./nginx/conf.d:/etc/nginx/conf.d
      - ./nginx/passwd:/etc/nginx/passwd
      - /var/log/nginx:/var/log/nginx
networks:


  elk:
    driver: bridge


```


##  Nginx的配置
```
server {

        listen     80;

        auth_basic "Kibana Auth";
        auth_basic_user_file /etc/nginx/passwd/kibana.passwd;


        location / {
            auth_basic "Protect Kibana";
            auth_basic_user_file /etc/nginx/passwd/kibana.passwd;
            
            
            proxy_pass http://127.0.0.1:5601; # 不可以，因为这么写是监听容器里的地址
            proxy_pass http://0.0.0.0:5601;   # 不可以，0.0.0.0不能指定某个位置，一般是监听某个局域网的所有不确定的访问者
            
            proxy_pass http://kibana:5601;    # 推荐
            proxy_pass http://10.10.1.74:5601; # 可以， 宿主ip
        }
  }

```
