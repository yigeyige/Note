#**Java 笔记**  
**author: YIGe**  
**date: 2020/7/10 15:28**  

1. SSH
    * Hibernate   
        + Hibernate查询结果集有同名字段的结果问题  
            ```sql
            select a.name, b.name 
              from table_a a,table_b b
             where a.id = b.id;
            ``` 
            <br/>上述结果集的name在hibernate框架下可能会出现前一列覆盖后一列的情况，可使用as rename进行解决。
            <br/>修改后sql如下：
            ```sql
            select a.name as name1, b.name as name2
              from table_a a,table_b b
             where a.id = b.id;
            ```
          
        + 延迟加载  
            [Hibernate延迟加载](https://www.cnblogs.com/chenmingjun/p/9747681.html)
            
            
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
    
  