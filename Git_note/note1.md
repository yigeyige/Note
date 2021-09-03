#**Git 笔记**  
**author: YIGe**  
**date: 2020/7/10 15:28**  

1. 切换分支  
    + 切换分支(不创建新分支)    
        ```git命令
        git checkout origin/branch1
        ```
    + 创建并切换分支  
        ```git命令
        git checkout -b origin/branch2
        ```
        
2. 版本回退  
    + 回退到上一个版本  
        ```git命令
        git reset --hard HEAD^
        ```
    + 回退到前两个版本
        ```git命令
        git reset --hard HEAD^^
        ```
    + 回退到前两个版本
        ```git命令
        git reset --hard HEAD~100
        ```
    + 回退到某个版本号
        ```git命令
        git reset --hard 1f05713
        ```

3. 仓库关联
    + 将本地仓库与github仓库关联  
        ```git命令
        git remote add origin https://github.com/yigeyige/Git_repository.git
        ```
        
4. 分支合并  
    + 合并分支
        ```git命令
        git merge origin/branch3
        ```
    + idea解决冲突  
        使用idea -> project -> resolve conflicts手动合并冲突代码
        
5. git配置  
    + 全局配置  
        ```git命令
        git config --global user.name  "yige"  
        git config --global user.email  "635337727@qq.com"
        ```
    + 局部配置(在仓库下执行)  
        ```git命令
        git config  user.name  "zhangyi"  
        git config  user.email  "yi.zhang07@hand-china.com"
        ```
        
6. git镜像
    + 镜像加速地址
        ```git命令
        git clone https://github.com.cnpmjs.org/yigeyige/project.git
        ```
        
7. 提交规范  
    + 提交信息规范  
        ```信息
        feat：新功能（feature）
        
        fix：修补bug
        
        docs：文档（documentation）
        
        style： 格式（不影响代码运行的变动）
        
        refactor：重构（即不是新增功能，也不是修改bug的代码变动）
        
        test：增加测试
        
        chore：构建过程或辅助工具的变动
        ```
      
8. 版本撤销 
    + 撤销指定的提交   
        ```shell script
        git revert commit_id
        :wq
        ```
      
9. 合并某一个提交到指定的分支  
    ```shell script
    git checkout 指定的分支
   
    git cherry-pick commit-id //把某个commit-id的提交合并到当前分支
    ```
   
10. 更换远程地址  
    ```shell script
    git remote set-url origin https://www.github.com/yige.git
    ```
    
11. 退回到某次提交  
    重置git到指定commit  
    ```shell script
     git reset --hard HEAD^         #回退到上个版本
     git reset --hard HEAD~3        #回退到前3次提交之前，以此类推，回退到n次提交之前
     git reset --hard commit_id     #退到/进到 指定commit的sha码
     
     git push origin HEAD --force   #强推到远程
    ```
    
12. 将本地强制覆盖
    ```shell script
    git fetch --all && git reset --hard origin/40.2108.91 && git pull
    ```
    
13. 远程不小心删除分支后，以本地重新创建并推送  
    找到删除分支最后一次commit_id
    ```shell script
    git branch recover_branch commit_id
    git push origin/recover_branch
    ```