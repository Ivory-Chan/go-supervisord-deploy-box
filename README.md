#### Supervisord 部署模版


### 1、supervisord安装
```shell
#### 1.1 下载golang版本的supervisord二进制文件，并放在项目根目录下，二进制文件统一命名为 supervisord
#### 下载地址 https://github.com/ochinchina/supervisord/releases
```

### 2、配置项目
```markdown
### 需要安装的项目统一放在services目录下，按服务目录分类
### 在根目录下supervisord.d文件夹内添加对应的conf文件，可参考service.conf.example配置模版 
### 需要env文件的，按照项目名称命名放在env目录下，方便在conf文件中引入
```

### 3、常用supervisord命令
```shell
### 启动命令
./supervisord -c ./supervisord.conf -d

### 查看服务状态
./supervisord ctl status

### 服务 start|stop|restart
./supervisord ctl start|stop|restart

### 关闭supervisord守护进程(同时会关闭所有负载的项目进程)
./supervisord ctl shutdown

### group显示，默认不按照group显示，配置了group不起效，想要起效，需要设置环境变量：
export SUPERVISOR_GROUP_DISPLAY=true

### 其他
### 更详细的操作参见官方文档：https://github.com/ochinchina/supervisord/blob/master/README.md

```

### 4、Web GUI使用以及密码机制
```shell
### 配置中默认开启了管理界面并默认配置了密码
[inet_http_server]
port = :9001
username=xxx
password=xxxxxxx

[unix_http_server]
file=/tmp/supervisord.sock
username=xxx
password=xxxxxxx

### 访问http://xxx.xxx.xxx.xxx:9001

### 加上密码之后 ./supervisord ctl status 等操作会不起效，需要加上验证参数，如下：
./supervisord ctl -u[xxxx] -P[xxxxxxx] status
```