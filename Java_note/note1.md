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
2.  Java 参数 
    + null传递    
        基本类型  
        基本类型的包装类  
        Java的数据类型分为两种：
        1、基本类型：byte(8),short(16),int(32),long(64),float(32),double(64),char(16),boolean(1)
        2、对象类型：Byte,Short,Integer,Long,Float,Double,Character,Boolean    
        [Java 参数传递 空对象 null](https://blog.csdn.net/mantoureganmian/article/details/49685309)  
        当参数为基本类型时，值传递一个null时，参数强制转换类型就会报空指针异常。  
        [参数传递](./image/参数传递.png)  
    + 参数  
        1）.当使用基本数据类型作为方法的形参时，在方法体中对形参的修改不会影响到实参的数值
        2）.当使用引用数据类型作为方法的形参时，若在方法体中修改形参指向的数据内容，则会
        * 对实参变量的数值产生影响，因为形参变量和实参变量共享同一块堆区；*
        3）.当使用引用数据类型作为方法的形参时，若在方法体中修改形参变量的指向，此时不会
        * 对实参变量的数值产生影响，因此形参变量和实参变量分别指向不同的堆区；*
    
3. StringBuffer&StringBuilder  

4. redis缓存  
    如果使用[缓存切面](./image/redis缓存.png)，调试的时候走的是redis缓存，不会进入类文件中
    
5. JVM  
    + 5.1 文件加载  
        Linux下加载配置文件是随机的。  
    + 5.2 JVM配置  
        * 新生代：常规理解为存放新对象。
        * 老年代：常规理解为多次GC后仍然存活的对象放入此处。
        * 永久代(7)/元数据(8)：主要存放元数据，例如Class、Method的元信息。对GC影响比较小。
        通常配置大小计算如下：堆大小 = 新生代大小 + 老年代大小
        活跃数据的大小是指，应用程序稳定运行时长期存活对象在堆中占用的空间大小，也就是FullGC后堆中老年代占用空间的大小。
        新生代 = 1-1.5 * 活跃数据大小
        堆 = 3-4 * 活跃数据大小
    + 5.3 查看栈大小
        ```shell script
        java -XX:+PrintFlagsFinal -version | grep -i 'stack'
        ```
    
6. 导出分析文件 
    + jstack/jmap    
        ```shell script
        /app/soft/jdk1.8.0_211/bin/jmap -dump:live,format=b,file=/tmp/15429.hprof 15429
        ```
   
    + CPU过高分析    
        ```shell script
        top
        /app/soft/jdk1.8.0_211/bin/jstack -l 26614 | tee -a /tmp/26614_jstack.log
        ps -mp 26614 -o THREAD,tid,time
        printf "%x\n" 27423
        /app/soft/jdk1.8.0_211/bin/jstack 27423|grep 6b1f
        ```  
    + 查看tomcat具有多少线程   
        ```shell script
        ps -ef|grep tomcat
        ps -Lf 29295|wc -l
        ```
   
7. 单例 多例  
    + 在单例中注入多例  
        解决办法：
        1. 是给bean注入一个BeanFactory，这样我们就可以在每次需要使用多例bean时都从BeanFactory中获取一个新的beanB。  
        ```java
            public class UserService implements BeanFactoryAware {
              //多例service
              private StudentService studentService;
              private BeanFactory beanFactory;
              public void service(){
                  this.studentService = (StudentService) factory.getBean("studentService");
                  System.out.println(studentService.toString());
                  studentService.study();
              }
              public StudentService getStudentService(){
                  return studentService;
              }
              public void setBeanFactory(BeanFactory bf) throws BeansException {
                  this.beanFactory = bf;
              }
            }
        ```
        2. 