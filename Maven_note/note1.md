#**Maven**  
**author: YIGe**  
**date: 2020/7/10 15:28**  

1. 错误  
    + 1.1 本地存在依赖却依旧报无法找到错误   
        [maven 本地依赖存在但还是报依赖无法找到的错误](https://blog.csdn.net/tiny_ding/article/details/84836302)  
        1.正确的解决方式：增加命令行参数 --legacy-local-repository 避免maven查询远程仓库的依赖  
        2.删除错误jar依赖仓库中所在文件夹的 _remote.repositories 的文件  
        
    + 1.2 function are not supported at language level '5'错误  
        第一步查询：File -> Project Structure -> Project Language Level，  
        如第一步无问题，则指定maven的jdk版本，在pom文件中指定即可。  
        ```text
        <build>
            <plugins>
                <plugin>
                    <groupId>org.apache.maven.plugins</groupId>
                    <artifactId>maven-compiler-plugin</artifactId>
                    <configuration>
                        <source>8</source>
                        <target>8</target>
                    </configuration>
                </plugin>
            </plugins>
        </build>
        ```