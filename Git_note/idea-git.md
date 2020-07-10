#**Idea-git**
**author: YIGe**  
**date: 2020/7/10 15:28**  

1. idea上传git  
    + 1.1 新建远程仓库  
    
    + 1.2 本地项目添加到Git仓库  
        VCS > import into version control > Create Git Repository [图片备注](./Image/create_repo.png)<br/>
        
    + 1.3 Add文件  
        项目 > Git > Add [图片备注](./Image/Add.png)<br/>
        
    + 1.4 配置远程仓库  
        项目 > Git > Repository > Remotes [图片备注](./Image/Remotes.png)<br/>
        
    + 1.5 拉去仓库信息  
        项目 > Git > Repository > Pull [图片备注](./Image/Pull.png)<br/>
        Pull > Pull Changes [图片备注](./Image/Pull-changes.png)<br/>
        若出现pull failed，使用拉去命令完成：[图片备注](./Image/Pull--rebase.png)
        ```shell script
        git pull --rebase origin master
        ```
     
    + 1.6 commit  