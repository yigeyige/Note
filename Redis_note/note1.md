#**Redis 笔记**

1. 停止redis  
    + 停止客户端   
        ```shell
        sudo ./redis-cli shutdown
        ```
    + 停止服务端  
        ```shell  
        ps -ef|grep redis
        kill -9 PID
        ```
    
2. 启动redis
    + 启动服务端  
        * 加上`&`号使redis以后台程序方式运行  
            ```shell
            sudo ./redis-server &
            sudo ./redis-server ../redis.conf &  
            ```
    + 启动客户端 用于本机测试   
        ```shell
        redis-cli -h 127.0.0.1 -p 6379 -a EmsCache2020
        127.0.0.1:6379> config get requirepass
        ```
3. 使用redis客户端检测连接是否正常  
    ```shell
    keys *
    ```
        