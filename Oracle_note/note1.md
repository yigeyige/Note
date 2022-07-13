#**Oracle**  
**author: YIGe**  
**date: 2020/7/10 15:28**  

1. 查询锁表语句  
    + 简洁锁表查询  
        ```sql
        select *
          from v$locked_object aa,
               all_objects     oo
         where aa.object_id = oo.object_id;
        ```
    + 查询锁，生成解锁语句  
        ```sql
        select lo.*,
               lo.locked_mode,
               lo.session_id,
               vss.serial#,
               vps.spid,
               vss.action action,
               vss.osuser osuser,
               vss.process ap_pid,
               vps.spid db_pid,
               'alter system kill session ' || '''' || lo.session_id || ',' ||
               vss.serial# || ''';' kill_command
          from v$locked_object lo, 
               all_objects     aa,
               v$session       vss,
               v$process       vps
         where lo.session_id = vss.sid
           and aa.object_id = lo.object_id
           and vss.paddr = vps.addr
         order by 2,
                  3;
        --简易版sql
        select 'alter system kill session ' || '''' || tt.session_id || ',' ||
               t.serial# || ''';' kill_command,
               tt.os_user_name,
               t.serial#,
        	   t.SQL_EXEC_START,
               oo.object_name,
               t.*
          from sys.v_$session       t,
               sys.v_$locked_object tt,
               sys.v_$process       pp,
               user_objects         oo
         where t.sid = tt.session_id
           and oo.object_id = tt.object_id
           and t.paddr = pp.addr;
        ```
      
2. with as 用法  
    如果在package中使用 可能会存在问题，因为其相当于是产生一个临时表  
    
3. delete问题  
    delete和insert中断都有回滚事务的。
    TRUNCATE TABLE TableName 
    1、删除表全部内容，但保留表结构 
    2、速度快，但不可回滚，要三思 
    3、触发器中没有TRUNCATE，即这个语句无法触发任何操作 
    4、行标识的序号重置（或者可以说：新行标识所用的计数值重置为该列的种子） 
    5、DELETE语句每删除一条记录都是一个事务，会产生若干"日志"。但TRUNCATE是释放整个数据页（一个页8K），所以解释了上述的第二点。
    
4. 重命名表
    ```sql
    alter table old_table_name rename to new_table_name;
    ```
    
5. 修改用户密码  
    ```sql
    alter user 用户名 identified by newpassword replace oldpassword;
    ```
   
6. 索引  
    + 6.1 删除索引  
        ```sql
        drop index index_name;
   
        alter table table_name drop constraint pk_name cascade;
        ```
    + 6.2 创建索引  
        online和非online方式创建索引，效果相同;  
        online方式创建索引，由于使用了一张临时表，以ROW SHARE锁表，不会阻塞原表DML的语句，  
        非online方式创建索引，则会以SHARE NOWAIT锁表，阻塞原表DML语句;
        online方式创建索引，Oracle执行工作复杂，因此比非online方式创建索引用时要久.
        ```sql
        create index reimburse.IDX_CLAIMBASE_PROCESS_STATE on reimburse.T_CLAIM_BASE (PROCESS_STATE) online;
        ```
    
7. 索引问题  
    + 7.1 常量索引  
        对于这种列上空较少的（占全表1/20）的列，常见的索引是无效的，因为索引默认不存空。   
        如果要创建，建议 这么写 create index  index_name on  T (col1, 1) 。  后边加个常量。
    + 7.2 联合索引  
        常规不推荐建立联合索引。如非要建立联合索引，满足最左匹配原则。
        select count(distinct account_no) a1,count(distinct claimno) a2 from t_account_processlog
        如上sql, 比较a1和a2数量大小，以数量最大的列为索引前面列。
        
        
8. 特殊sql  
    + 8.1 查询短时内表的修改记录（需要开启快照）  
        ```sql
        select *
          from reimburse.t_claim_base AS OF TIMESTAMP TO_TIMESTAMP('2021-06-29 16:15:40', 'yyyy-mm-dd hh24:mi:ss')
         where claim_id = 48133811
        ```  
    + 8.2 特殊like查询  
        ```sql
        select * from dual where 'a%b%' like '%/%%' escape '/'
        ```
    + 8.3  查询segment  
        ```sql
        select owner,
               segment_name,
               segment_type,
               bytes / 1024 / 1024 as mb
          from dba_segments
         where segment_name in ('T_INTEGRATED_MESSAGE',
                                'T_INTEGRATED_MESSAGE_IDX1',
                                'T_INTEGRATED_MESSAGE_IDX2',
                                'T_INTEGRATED_MESSAGE_N1');
        ```  
    + 8.4 kill会话  
        ```sql
        ALTER SYSTEM DISCONNECT SESSION IMMEDIATE;
        ```
    + 8.5 特殊执行   
        ```sql
        prompt Importing...
        set feedback off
        set define off
                
        prompt Done.
        ```  
    + 8.6 分析索引  
        ```sql 
        analyze table test_table compute statistics for all indexes for all columns;
        ```
      
9. 授权操作  
    + 8.1 授权  
        ```sql
        grant execute on query_account_backinfo to dbquery;
        ```