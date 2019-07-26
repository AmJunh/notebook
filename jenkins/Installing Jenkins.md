Jenkins Install
=

On Ubuntu
--

#### **执行如下代码：**
```
    wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -
    sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
    sudo apt-get update
    sudo apt-get install jenkins
```

#### **Jenkins的运行**

服务启动|停止|重启：`sudo service jenkins start|stop|restart`


#### **Jenkins的初次配置**

> 1. 浏览器中访问： `http://IP:8080`， 使用`cat /var/lib/jenkins/secrets/initialAdminPassword`查看初始密码并在浏览器中登录 
> 2. 安装推荐或自选插件(老手可自行配置，新手推荐默认方式)
> 3. 创建管理员
> 4. 更改8080端口：jenkins默认使用8080端口，较容易冲突，更改方式如下：
>> 4.1. 编辑 `/etc/default/jenkins `文件，将`HTTP_PORT=8080`更改为自定义端口  
>> 4.2. 编辑 `/etc/init.d/jenkins`文件，将唯一的8080更改为自定义端口
        
参看官方文档：
1. [Installing Jenkins on Ubuntu][1]

[1]:https://wiki.jenkins.io/display/JENKINS/Installing+Jenkins+on+Ubuntu
