### 如何将文件夹打包成镜像,并上传到docker hub

##### 首先,**docker build** 命令用于使用 Dockerfile 创建容器。

Code(代码): docker build  -t ImageName:TagName dir

example(例子): docker build -t zeepelin-lab:zeepelin /home/wangyan/project/bigdata-zerotohero/docker-environment/zeppelin-lab

##### 然后,使用 docker ps 命令来检查是否成功生成容器并在环境中运行

code(代码): docker ps

##### 下一步需要使用自己的docker hub账号(没有账号的同学,建议自己去注册一个),

去docker hub的官网登陆并在账号中注册一个公有pubic或私有仓库private,最好以自己要上传的镜像名命名仓库名

##### 回到我们的docker环境,继续写代码:

##### 登陆docker账户仓库

code(代码):

```
docker login
// 输入账号和密码
```

##### 将容器变为镜像

code(代码):

```
// 找到运行中的容器 
docker ps
// 选择一个容器,进行打包为镜像
docker commit 容器id 设置打包为镜像的名字
// 找到打包的镜像
docker images
```

example(例子):

docker commit 53c0(注意一般情况下,不需要打全id名,docker就可以帮我们找到的) zeeplin-lab

docker images

##### 接下来选择将镜像上传到那个仓库中去,需要docker tag 设置仓库

```
docker tag zeeplin-lab ywan328/zeeplin-lab

// 这个命令的意思是 将镜像zeeplin-lab 设置上传的仓库名字 仓库名字是docker上注册的         用户名/仓库名        
// 如果没有仓库 按照我上面的创建一个

docker images
```

其中 容器打包的镜像id和刚刚tag的 用户名/仓库名id 一样  可以不要理会

如果需要进行版本控制 只需要在tag 仓库名后面加上  :版本号   可以得到设置版本镜像

默认的版本号是:latest

##### 上传镜像

code(代码):

```
docker push 被tag的镜像名
```

```
docker push 被tag的镜像名:版本号
```

example(例子):

docker push ywan328/zeepelin-lab:latest

##### 从docker hub拉取已上传的镜像

docker pull ywan328/zeepelin-lab:latest



