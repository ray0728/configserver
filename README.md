![travis_ci](https://www.travis-ci.org/ray0728/resourceserver.svg?branch=master)
# configserver
## 说明
基于Spring Cloud的配置服务器，提供基于GITHUB的配置文件管理服务。

## 运行方式：  
application.properties中并**不包含**完整配置信息，所以**不支持**直接运行  
* java 方式

```java
java
-Djava.security.egd=file:/dev/./urandom                         \  
-Dserver.port=$CONFIGSERVER_PORT                                \  
-Deureka.client.serviceUrl.defaultZone=$EUREKASERVER_URI        \  
-Dspring.cloud.config.server.git.uri=$GIT_URI                   \  
-Dspring.cloud.config.server.git.search-paths=$GIT_SEARCH_PATH  \  
-Dspring.cloud.config.server.git.username=$GIT_USERNAME         \  
-Dspring.cloud.config.server.git.password=$GIT_PASSWD           \  
-Dlocal.save.dir=$SAVE_DIR                                      \  
-jar target.jar
```
* docker 方式  
建议用docker-compose方式运行  
```docker
configserver:
    image: ray0728//configserv:1.0
    ports:
      - "10002:10002"
    environment:
      ENCRYPT_KEY: 如果需要加密则设置该字段
      EUREKASERVER_URI: EUREKA地址
      CONFIGSERVER_PORT: 服务运行端口
      GIT_URI: GITHUB上库地址
      GIT_SEARCH_PATH: 搜寻目录
      GIT_USERNAME: GITHUB账号
      GIT_PASSWD: GITHUB密码
      SAVE_DIR: "/mnt/config"
    volumes:
      - /home/core/config/:/mnt/config
```  
关于Docker  
编译完成的Docker位于[Dockerhub][1]请结合Release中的[Tag标签][2]获取对应的Docker

[1]:https://hub.docker.com/r/ray0728/configserv/tags
[2]:https://github.com/ray0728/configserver/tags
