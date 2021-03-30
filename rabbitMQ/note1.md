#**rabbitMQ**  
**author: YIGe**  
**date: 2021/3/10 16:01** 

1. rabbitMQ搭建  
    + 创建用户  
        ```shell script
        cd rabbitmq/sbin
        sudo ./rabbitmqctl add_user admin admin
        sudo ./rabbitmqctl set_user_tags admin administrator
        sudo ./rabbitmqctl set_permissions admin ".*"  ".*"  ".*"
        ```
