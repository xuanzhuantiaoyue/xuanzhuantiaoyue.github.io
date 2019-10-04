# LINUX安装node.js socket.io express PM2



##### 安装node.js

第一步: 下载node地址：https://nodejs.org/en/download/

```
wget https://nodejs.org/dist/v10.16.3/node-v10.16.3-linux-x64.tar.xz
```

下载后,是一个[node-v10.16.0-linux-x64.tar.xz ] 文件夹，进行解压：

```
xz -d XX.xz        #.xz解压命令
tar -xvf  XX.tar   #.tar解压命令
ls node-v10.16.3-linux-x64  node-v10.16.3-linux-x64.tar
```

配置环境变量

1、切换到root账户

2、vi /etc/profile ，进入文件后，在最后面追加两条路径，如下：

```
export NODEJS_HOME=/nodejs的路径
export PATH=$PATH:$NODEJS_HOME/bin
```

3、source /etc/profile ，文件生效！

或

配置环境变量

vim .bash_profile(我这里配置局部变量,vim /etc/profile 全局变量)

```
export NODE_HOME=/nodejs路径
```

```
export PATH=$PATH:$NODE_HOME/bin
```

```
export NODE_PATH=$NODE_HOME/lib/node_modules
```

保存

```
:wq
```

提交

```
source .bash_profile 
```

```
进行提交 **切记,否则配置了环境变量无效果,配置jdk同理**
```

4、验证结果：

```
node -v
```

```
v10.16.0
```

2安装socket io模块，

cd切换到你工作（网站目录下）

```
cd /www/wwwroot/nodejs
```

运行

```
npm install socket.io
```

可以看到 nodejs下有个 node_modules目录

4.编写package.json文件

```
{
```

```
    "name": "node_test",
```

```
    "version": "0.0.1",
```

```
    "description": "my first socket.io app",
```

```
    "dependencies": {
```

```
        "express": "^4.15.2",
```

```
        "socket.io": "^2.0.4"
```

```
    }
```

```
}
```

安装express

express 是一个基于node的web框架

```
npm install express
```

二、建立socket服务 

5.编写server.js基础文件

```
// 'use strict'
```

```
var app = require('express')();
```

```
var http = require('http').Server(app);
```

```
var io = require('socket.io')(http);
```

```
http.listen(3000, function () {
```

```
    console.log('listening on *:3000');
```

```
});
```

将文件上传到你想要的路径

7.node自带npm ,用npm安装node所需的模块 node install

8.让node能够在后台一直运行，下载pm2管理工具 npm install pm2 -g

9.利用pm2启动server.js文件 mp2 start server.js

```
pm2 start server.js
```

![img](https://note.youdao.com/yws/public/resource/4b33824c7b441917f0e671d1ba1ea454/xmlnote/A03E44486A2A4EA5887D80D4C585B226/17744)

PM2 常用命令

```
$ pm2 start app.js # 启动app.js应用程序
```

```
$ pm2 start app.js -i 4        # cluster mode 模式启动4个app.js的应用实例
```

```
# 4个应用程序会自动进行负载均衡
```

```
$ pm2 start app.js --name="api" # 启动应用程序并命名为 "api"
```

```
$ pm2 start app.js --watch      # 当文件变化时自动重启应用
```

```
$ pm2 start script.sh          # 启动 bash 脚本
```

```
$ pm2 list                      # 列表 PM2 启动的所有的应用程序
```

```
$ pm2 monit                    # 显示每个应用程序的CPU和内存占用情况
```

```
$ pm2 show [app-name]          # 显示应用程序的所有信息
```

```
$ pm2 logs                      # 显示所有应用程序的日志
```

```
$ pm2 logs [app-name]          # 显示指定应用程序的日志
```

```
$ pm2 flush                       # 清空所有日志文件
```

```
$ pm2 stop all                  # 停止所有的应用程序
```

```
$ pm2 stop 0                    # 停止 id为 0的指定应用程序
```

```
$ pm2 restart all              # 重启所有应用
```

```
$ pm2 reload all                # 重启 cluster mode下的所有应用
```

```
$ pm2 gracefulReload all        # Graceful reload all apps in cluster mode
```

```
$ pm2 delete all                # 关闭并删除所有应用
```

```
$ pm2 delete 0                  # 删除指定应用 id 0
```

```
$ pm2 scale api 10              # 把名字叫api的应用扩展到10个实例
```

```
$ pm2 reset [app-name]          # 重置重启数量
```

```
$ pm2 startup                  # 创建开机自启动命令
```

```
$ pm2 save                      # 保存当前应用列表
```

```
$ pm2 resurrect                # 重新加载保存的应用列表
```

```
$ pm2 update                    # Save processes, kill PM2 and restore processes
```

```
$ pm2 generate                  # Generate a sample json configuration file
pm2文档地址：http://pm2.keymetrics.io/docs/usage/quick-start/
```