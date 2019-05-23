

1. 安装Docker Registry
    
    sudo docker run -d -v /data/registry:/var/lib/registry -p 5000:5000 --restart=always --privileged=true --name registry registry:latest

说明：
    
    -v /data/registry:/var/lib/registry 默认情况下，会将仓库存放于容器内的/var/lib/registry目录下，指定本地目录挂载到容器。

    -p 5000:5000 端口映射

    --restart=always1 在容器退出时总是重启容器,主要应用在生产环境

    --privileged=true 在CentOS7中的安全模块selinux把权限禁掉了，参数给容器加特权，不加上传镜像会报权限错误OSError: [Errno 13] Permission denied: ‘/tmp/registry/repositories/liibrary’)或者（Received unexpected HTTP status: 500 Internal Server Error）错误

    --name registry 指定容器的名称

2.  Docker Registry 的使用

推送rabbitmq:3.5-management到Registry仓库

    #使用tag命令修改标签：
    sudo docker tag tomcat localhost:5000/rabbitmq:3.5-management

推送到仓库：

    sudo docker push localhost:5000/rabbitmq:3.5-management

从仓库pull：
    
    sudo docker pull localhost:5000/rabbitmq:3.5-management