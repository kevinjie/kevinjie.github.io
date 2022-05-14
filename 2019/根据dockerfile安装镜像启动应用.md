# 根据dockerfile安装镜像启动应用

#docker #dockerfile

以koa demo为例

Dockerfile配置

```yaml
# baisc image
FROM node:10.7.0

# create app directory
WORKDIR /usr/src/app

# Install app dependencies
# A wildcard is used to ensure both package.json AND package-lock.json are copied where available (npm@5+)
COPY package*.json ./
# Only copy package.json for good cached Docker layers
# http://bitjudo.com/blog/2014/03/13/building-efficient-dockerfiles-node-dot-js/

ENV YARN_VERSION 1.9.2

RUN curl -fSLO --compressed "https://yarnpkg.com/downloads/$YARN_VERSION/yarn-v$YARN_VERSION.tar.gz" \
&& tar -xzf yarn-v$YARN_VERSION.tar.gz -C /opt/ \
&& ln -snf /opt/yarn-v$YARN_VERSION/bin/yarn /usr/local/bin/yarn \
&& ln -snf /opt/yarn-v$YARN_VERSION/bin/yarnpkg /usr/local/bin/yarnpkg \
&& rm yarn-v$YARN_VERSION.tar.gz

# If you are building your code for production
# RUN npm install --only=production
RUN yarn

# Bundle app source
COPY . .

# mapped by the docker daemon
EXPOSE 8800

# launch runtime you define
CMD [ "yarn", "start" ]

# further reading
# https://github.com/nodejs/docker-node
```

构建镜像image
```
docker build -t docker-koa-demo:v1 .
```
Docker 在运行时分为 Docker 引擎（也就是服务端守护进程）和客户端工具。Docker 的引擎提供了一组 REST API，被称为 Docker Remote API，而如 docker 命令这样的客户端工具，则是通过这组 API 与 Docker 引擎交互，从而完成各种功能。因此，虽然表面上我们好像是在本机执行各种 docker 功能，但实际上，一切都是使用的远程调用形式在服务端（Docker 引擎）完成。

查看镜像
```
docker image ls
```
删除镜像
```
docker image rm <image id> <image id>
```
构建一个容器并启动
```
docker run -d -p 7788:8800 docker-koa-demo:v1
```
启动已终止的容器
```
docker container start <container id>
```
终止容器
```
docker container stop <container id>
```
重启容器
```
docker container restart <container id>
```
查看所有激活的容器
```
docker ps
```
查看所有容器
```
docker ps -a
```
进入容器
```
docker exec -it <container id> /bin/bash
```
导出容器
```
docker export <container id> > path/container.tar
```
导入容器

Docker import 快照文件或URL或某个目录

删除容器
```
docker container rm <container id> [other container id]
```
