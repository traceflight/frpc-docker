# frpc-docker
[frp](https://github.com/fatedier/frp)客户端容器镜像

# 使用方法

首先创建配置`frpc.ini`文件，修改其中的server_addr等字段，然后将其挂载到容器的`/etc/frp`文件夹中。

## docker

```
$ mkdir ./config
$ tee ./config/frps.ini <<-'EOF'
[common]
server_addr = xxx.xxx.xxx.xxx
server_port = 7000
log_file = /var/log/frpc.log

[ssh]
type = tcp
local_ip = 127.0.0.1
local_port = 22
remote_port = 6000
EOF
$ docker run -d \
       --network host \
       --name frpc \
       -v `pwd`/config:/etc/frp \
       -v `pwd`/log:/var/log \
       traceflight/frpc
```

## docker-compose

```
$ git clone https://github.com/traceflight/frpc-docker.git
$ cd frpc-docker
$ docker-compose up -d
```

# 配置

参考[官方说明](https://github.com/fatedier/frp/blob/master/README_zh.md)
