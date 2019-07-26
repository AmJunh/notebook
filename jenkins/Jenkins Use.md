Simple Use
=

Plugin Install
--

安装插件，1、2插件使用Tag进行版本发布与回滚，3插件将代码部署到远端
> 1. Git Parameter Plug-In
> 2. Stash Branch Parameter Plug-In
> 3. Git Tag Message Plugin
> 4. Publish Over SSH


这里以Web工程为例，安装了相关插件，如下：
> NodeJS Plugin

        
#### 新建任务
选择简单配置，可参考文档使用其他类型任务

![任务选择][1]
        
#####1.General配置
勾选`参数化构建过程`， 添加参数选择 `Git Parameter`，填写参数名相关配置。

![Tag设置][2]


#####2.源码管理
勾选`Git`，填写相关配置
![Git设置][3]

填写入代码库地址，推荐使用已ssh地址，**`凭证`** 为获取远程库代码的权限校验，若没有对应选项，点击`添加`新建一个凭证即可。

###### 添加凭证
类型这里使用`SSH Username with private key`,只需在`private Key`中添加对应远程库的 **_公钥对应的私钥_** 即可，请注意，这里需要填写`对应的私钥`

![全局凭证新建][4]


#####3.构建环境
对于不同的工程，选择对应的构建环境，这里以Web工程为例，所以勾选`Provide Node & npm bin/ folder to PATH`了，默认即可。
        
注：若无NodeJs选择可选，保存现有配置，跳转到`Jenkins` -> `全局工具配置`，新增一个NodeJs即可，对于node版本选择项目对应的版本即可。

#####3.构建
**该步骤为当代码Ready后，如何进行构建**        
勾选`执行shell`了，在命令中输入对应构建命令即可  
Web工程构建为例：

```bash
npm install
npm run build
// 打包构建文件
zip -qr dist.zip dist/
```

#####4.构建后操作
**该步骤关注点为如何进行部署：构建完成后，通过SSH传递到目标服务器，并在目标服务器上执行部署脚本，完成部署**        

首先需要解决的是通过ssh能无密码登录到目标服务器  

进入`系统管理` -> `系统设置`
> 1. 在`Publish over SSH`类目中点击`新增`
> 2. 在`key`中填入对应私钥（注：该秘钥对应的公钥此时在目标服务器的授权认证目录下）
> 3. 在`SSH Server`中输入对应配置即可， `Name Username Hostname`
> 4. 点击`Test Configuration`，出现`Success`表示可Jenkins可无密码访问


回到Test任务的配置页面，继续之前配置，如下图        

![构建后操作][5]
在`Name`中选择对应SSH Server选项  

Transfer 中根据实际情况填写对应目录与文件  
Exec command中可写入对应bash命令，命令在目标服务器上执行

```bash
unzip -qo dist.zip
```

[1]:./imgs/CT1.png
[2]:./imgs/CT2.png
[3]:./imgs/CT3.png
[4]:./imgs/CT4.png
[5]:./imgs/CT5.png
