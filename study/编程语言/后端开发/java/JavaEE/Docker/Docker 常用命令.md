    下面总结一些常见的命令：

    ```
    1. 查看 docker 信息
        version
        info
    2. 操作 images
        search
        pull
        images
        rmi
        history
    3. 启动容器
    4. 查看容器
    5. 保存对容器的修改
    6. 操作容器
        rm
        stop
        start
        kill
        logs
        diff
        top
        cp
        restart
        attach
    7. 保存和加载镜像
        save
        load
    8. 登录
        login
    9. 发布
        push
    ```

    #### 查看 docker 信息

    ```
    # 查看 docker 版本
    docker version

    # 显示 docker 系统的信息
    docker info
    ```

    #### 操作 images

    ```
    # 检索 image
    docker search image_name

    # 下载 image
    docker pull image_name

    # 列出镜像列表
    docker images

    # 删除一个或者多个镜像
    docker rmi image_name

    # 显示一个镜像的历史
    docker history image_name
    ```

    #### 启动容器

    ```
    # 在容器中运行"echo"命令，输出"hello word"  
    docker run image_name echo "hello word"  

    # 交互式进入容器中  
    docker run -i -t image_name /bin/bash 

    # 在容器中安装新的程序  
    docker run image_name apt-get install -y app_name  
    ```

    #### 查看容器

    ```
    # 列出当前所有正在运行的container  
    docker ps  

    # 列出所有的container  
    docker ps -a  

    # 列出最近一次启动的container  
    docker ps -l  
    ```

    #### 保存对容器的修改

    ```
    docker commit ID new_image_name  
    ```

    当你对某一个容器做了修改之后（通过在容器中运行某一个命令），可以把对容器的修改保存下来，这样下次可以从保存后的最新状态运行该容器。

    注： image相当于类，container相当于实例，不过可以动态给实例安装新软件，然后把这个container用commit命令固化成一个image。

    #### 操作容器

    ```
    # 删除所有容器  
    docker rm `docker ps -a -q`  

    # 删除单个容器;  
    docker rm Name/ID  

    # 停止、启动、杀死一个容器  
    docker stop Name/ID  
    docker start Name/ID  
    docker kill Name/ID  

    # 从一个容器中取日志; 
    docker logs Name/ID  

    # 列出一个容器里面被改变的文件或者目录
        list列表会显示出三种事件
            A 增加的
            D 删除的
            C 被改变的  
    docker diff Name/ID  

    # 显示一个运行的容器里面的进程信息  
    docker top Name/ID  

    # 从容器里面拷贝文件/目录到本地一个路径  
    docker cp Name:/container_path to_path  
    docker cp ID:/container_path to_path  

    # 重启一个正在运行的容器
    docker restart Name/ID  

    # 附加到一个运行的容器上面
    docker attach ID  
    ```

    #### 保存和加载镜像

    ```
    # 保存镜像到一个tar包; -o, --output="" Write to an file  
    docker save image_name -o file_path  

    # 加载一个tar包格式的镜像; -i, --input="" Read from a tar archive file  
    docker load -i file_path  

    # 机器a  
    docker save image_name > /home/save.tar 

    # 使用scp将save.tar拷到机器b上，然后：  
    docker load < /home/save.tar  
    ```

    #### 登录

    ```
    # 登陆registry server
    docker login 
    ```

    #### 发布

    ````
    docker push new_image_name
    ````

