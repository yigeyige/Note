#**Docker**
**author: YIGe**  
**date: 2020/7/10 15:28**  

1. 添加加速镜像地址  
    ```shell script
    vi /etc/docker/daemon.json
    {"registry-mirrors": ["http://hub-mirror.c.163.com"]}
    sudo service docker restart
    ```
   
2. 移除容器服务  
    docker rm -f #container_id
    
3. 列出容器服务  
    docker ps  
    docker container ls  
    
4. 列出容器  
    docker images  
    
5. 进入mysql命令行  
    + 进入数据库命令行  
    docker exec -it #container_id  bash
    + 进入数据库sqlplus    
    mysql -u root -p