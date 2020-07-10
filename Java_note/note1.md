#**Java 笔记**

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
2.     
  