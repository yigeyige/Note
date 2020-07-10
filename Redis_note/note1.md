#**Redis 笔记**

1. 学习推荐  
    

2. Linux  
    + 2.1 停止  
        * 停止客户端   
            ```shell
            sudo ./redis-cli shutdown
            ```
        * 停止服务端  
            ```shell  
            ps -ef|grep redis
            kill -9 PID
            ```
    
    + 2.2 启动  
        + 启动服务端  
            加上`&`号使redis以后台程序方式运行  
            ```shell
            sudo ./redis-server &
            sudo ./redis-server ../redis.conf &  
            ```
        + 启动客户端 用于本机测试   
            ```shell
            ./redis-cli -h 127.0.0.1 -p 6379 -a EmsCache2020
            127.0.0.1:6379> config get requirepass
            ```
    + 2.3 卸载  
        
      
3. Windows  
    + 3.1 启动服务端   
        切换到redis主目录  
        ```cmd
        redis-server.exe redis.windows.conf
        ``` 
      
        编制bat脚本,切换到redis主目录,创建bat文件  
        ```cmd
        redis-server.exe  --service-stop
        
        redis-server.exe redis.windows.conf
        ```
    + 3.2 启动客户端  
        切换到redis主目录
        ```cmd
        redis-cli.exe
      
        127.0.0.1:6379> auth redis_password
        ```
      
    + 3.3 卸载  
    
4. redis命令   
    + 4.1 删除所有数据库的所有key  
        ```shell script
        127.0.0.1:6379> flushall
        ```

    + 4.2 删除当前数据库的所有key  
        ```shell script
        127.0.0.1:6379> flushadb
        ```        
       