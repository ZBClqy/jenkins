## 部署

jenkins是用java语言开发的 所以首先在服务器安装一个jdk11

yum -y list java

然后我们找到jdk11安装

yum install -y jdk版本

### jenkins

对呀jenkins我们可以直接去官网下载war包，然后再将其拖入我们的服务器目录中即可

最后执行 java -jar jenkins.war 就开启我们的服务了

注意看命令会给我们提供默认密码首次进入jenkins要使用

然后安装我们的默认插件

进去后记得设置我们的账户密码

### 前端

部署前端项目

首先我们去jenkins的manage jenkins（管理）里面的plugins去安装我们的node.js插件 ，安装完后到tools里面去找到我们的node.js进行配置

设置名称 选择node版本 即可

然后还是到plugins安装我们的git parameter插件

最后安装我们的publish over ssh插件，安装完后到我们的system系统中去找到其进行配置。

这里配置名称

服务器公网ip

用户名

路径选择根路径

然后到高级设置里面勾选使用密码验证，输入我们的服务器密码即可

#### 新建项目

输入名称后选择 freestyle project 点击确定进行配置

这里首先输入说明，然后勾选this project is parameterized使用我们的git parameter插件进行分支配置 

输入姓名 说明 类型选择branch（分支）然后默认分支输入origin/master

随后配置我们的git

输入我们clone  git的url

资质证书 点击添加 用账号密码进行验证然后选择生成secret

然后新建我们的分支有几个建立几个

随后往下滑到我们的构建环境，因为刚才配置了node插件这里我们可以根据刚才赋予的node名称选择node进行配置

最后我们新建构建步骤，在第一个步骤里选择执行shell命令

npm install

npm run build

然后在第二个构建步骤里选择ssh发送文件或执行命令

首先也是选择我们刚才创建的ssh配置名称

然后源文件配置下面路径

dist/*/**

然后删除我们的源文件路径前面的dist文件夹

dist

远程目录选择我们服务器中项目的public即可

最后保存即可

### 后端

这里后端采用的是thinkphp

#### 新建项目

这里与前端的变化在于少了配置node

在第一个构建中我们使用的是composer不是npm

composer install