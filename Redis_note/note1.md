#**Redis 笔记**

1. Linux  
    + 1.1 停止  
        * 停止客户端   
            ```shell
            sudo ./redis-cli shutdown
            ```
        * 停止服务端  
            ```shell  
            ps -ef|grep redis
            kill -9 PID
            ```
    
    + 1.2 启动  
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
    + 1.3 卸载  
        
      
2. Windows  
    + 2.1 启动服务端   
        切换到redis主目录  
        ```cmd
        redis-server.exe redis.windows.conf
        ``` 
      
        编制bat脚本,切换到redis主目录,创建bat文件  
        ```cmd
        redis-server.exe  --service-stop
        
        redis-server.exe redis.windows.conf
        ```
    + 2.2 启动客户端  
        切换到redis主目录
        ```cmd
        redis-cli.exe
      
        127.0.0.1:6379> auth redis_password
        ```
      
    + 2.3 卸载  
       