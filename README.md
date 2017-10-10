# server-dockerfile
dockerfile for server

## dev mode

请首先修改本地 docker-compose.yml 中的 volumes 中的路径，调整成此项目中对应的路径。并将后端服务的路径也匹配正确。

> 如果你在 Windows 中开发，请务必首先执行 `docker volume create --name pgdata -d local`

开发环境请启动 docker 以后，在当前目录下执行 `docker-compose up revel`，等待服务启动，服务将会启动在 `0.0.0.0:9000` 上

> 如果你在 Windows 中开发，需要在其他机器上访问此后端服务，请务必在防火墙中开放 9000 端口

## production mode

在本地打包好后端服务之后，上传到服务器，服务器也需要 clone 本项目。移动到此目录下的 production 目录中，然后解压缩既可。

返回本目录，执行 `docker-compose -f docker-compose-pro.yml up -d revel`

命令大概如下：

```shell
git clone git@github.com:AnnatarHe-Athena/server-dockerfile.git
cd server-dockerfile/production
mv ~/server.tar.gz .
tar -zxvf server.tar.gz
cd ..
docker-compose -f docker-compose-pro.yml up -d revel
```

服务会运行在 localhost:9000，之后可以使用 Nginx 的反向代理提供一个友好的域名和 TLS 服务。

强烈建议部署在 https 环境下，可以使用 [letsencrypt](https://letsencrypt.org/) 生成证书.
