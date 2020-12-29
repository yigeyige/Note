#**Java 笔记**  
**author: YIGe**  
**date: 2020/7/10 15:28**  

1. SSH
    * Hibernate   
        + 1.1 Hibernate查询结果集有同名字段的结果问题  
            ```sql
            select a.name, b.name 
              from table_a a,table_b b
             where a.id = b.id;
            ``` 
            上述结果集的name在hibernate框架下可能会出现前一列覆盖后一列的情况，可使用as rename进行解决。  
            修改后sql如下：
            ```sql
            select a.name as name1, b.name as name2
              from table_a a,table_b b
             where a.id = b.id;
            ```
          
        + 1.2 延迟加载   
            [Hibernate延迟加载](https://www.cnblogs.com/chenmingjun/p/9747681.html)   
            [解决延迟加载异常](https://blog.csdn.net/chenssy/article/details/8792666)   
            [使用OpenSessionInViewFilter方案解决Hibernate懒加载异常的问题](https://www.jianshu.com/p/1a8343292c4a)  
            1. OpenSessionInViewFilter需要放在StrutsPrepareAndExecuteFilter过滤器前面  
            思考原因：如果是先进入StrutsPrepareAndExecuteFilter，再进入OpenSessionInViewFilter，
            OpenSessionInViewFilter就管理不了Struts的一些操作了。  
            
            
    * Struts2  
    
    * Spring  
2.  Java 参数 null传递  
    基本类型  
    基本类型的包装类  
    Java的数据类型分为两种：
    1、基本类型：byte(8),short(16),int(32),long(64),float(32),double(64),char(16),boolean(1)
    2、对象类型：Byte,Short,Integer,Long,Float,Double,Character,Boolean    
    [Java 参数传递 空对象 null](https://blog.csdn.net/mantoureganmian/article/details/49685309)  
    当参数为基本类型时，值传递一个null时，参数强制转换类型就会报空指针异常。  
    [参数传递](./image/参数传递.png)  

3. StringBuffer&StringBuilder  


4. redis缓存  
    如果使用[缓存切面](./image/redis缓存.png)，调试的时候走的是redis缓存，不会进入类文件中
    
5. JVM加载配置文件  
    Linux下加载配置文件是随机的。
    
6. 导出分析文件
    ```shell script
    /app/soft/jdk1.8.0_211/bin/jstack -l 15429  | tee -a /tmp/15429_jstack.log
    /app/soft/jdk1.8.0_211/bin/jmap -dump:live,format=b,file=/tmp/15429.hprof 15429
    ```