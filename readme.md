# 一， 创建alpine 3.18 基础离线镜像包

### 从dockerhub 拉取 alpine 3.18 镜像
docker pull alpine:3.18

### 启动 alpine 3.18 镜像 为容器，然后导出
docker run -dit --name alpine3.18 alpine:3.18 /bin/sh

docker exec -it 518 sh

docker export -o alpine-3.18.tar alpine3.18

### 验证导出的tar转为镜像是否能正常启动
docker import alpine-3.18.tar alpine-test:3.18
docker run -dit --name alpinetest3.18 alpine-test:3.18 /bin/sh
docker ps
docker exec -it alpinetest3.18 sh

验证ok！

## 二，创建 alpine 3.18 + gcc 12 + python 3.11.4镜像

docker run -dit --name alpine3.18-py alpine:3.18 /bin/sh
docker exec -it alpine3.18-py sh

echo -e 'https://mirrors.aliyun.com/alpine/v3.18/main/\nhttps://mirrors.aliyun.com/alpine/v3.18/community/' > /etc/apk/repositories
https://mirrors.aliyun.com/alpine/v3.18/main/
https://mirrors.aliyun.com/alpine/v3.18/community/

cat /etc/apk/repositories
echo > /etc/apk/repositories
#https://mirrors.aliyun.com/alpine/v3.18/main/
#https://mirrors.aliyun.com/alpine/v3.18/community/
https://repo.huaweicloud.com/alpine/v3.18/main/

apk update

只有华为镜像源有 python 3.11.4 镜像
apk add python3=3.11.4-r0
apk add gcc=12.2.1_git20220924-r10

### 导出容器为镜像tar
docker export -o alpine-3.18-py.tar alpine3.18-py

### 验证新镜像是否能运行起来
docker import alpine-3.18-py.tar alpine-test-py:3.18
docker run -dit --name alpinetestpy3.18 alpine-test-py:3.18 /bin/sh
docker ps
docker exec -it alpinetestpy3.18 sh

验证ok！
