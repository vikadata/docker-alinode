# alinode Docker

Dockerfiles for building runtime image for [Node.js Performance Platform runtime](https://help.aliyun.com/product/60298.html).

The built containter image list can be found [here](https://help.aliyun.com/document_detail/65376.html).

The version map can be found [here](https://help.aliyun.com/document_detail/60811.html).

The built images can be pulled from:

```shell
public:: docker pull registry.cn-hangzhou.aliyuncs.com/aliyun-node/alinode:[image-tag]
internal: docker pull registry-internal.cn-hangzhou.aliyuncs.com/aliyun-node/alinode:[image-tag]
VPC: docker pull registry-vpc.cn-hangzhou.aliyuncs.com/aliyun-node/alinode:[image-tag]
```

# Usage

## build images

```shell
./build.sh 2/3/4 jessie/slim/stretch
```

e.g:

```shell
# build image for the latest version alinode-v4.x (node-v10.x)
./build 4 jessie

# build image for the latest version alinode-v4.x (node-v10.x)
./build 4 slim

```

Image with tag alinode-2/3/4-jessie/slim/stretch will be created.


## verify the image

### provide **APP_ID** and **APP_SECRET** via environment variables

```shell
cd test
docker build -t alinodetest .
docker run -d -p 3333:3333 -e "APP_ID=_YOUR_APP_ID" -e "APP_SECRET=_YOUR_APP_SECRET" alinodetest
```

### provide **APP_ID** and **APP_SECRET** via config file

```shell

cd test
# provide APP_ID and APP_SECRET via app-config.json
docker build -t alinodetest .
docker run -d -p 3333:3333 alinodetest
```

Then check from [here](https://node.console.aliyun.com).

## Contribute

You're welcome to make pull requests!

# Reference
## Dockerfile FROM buildpack-deps 使用
```
表明该镜像基于Debian Linux镜像。无后缀一般表示镜像基于buildpack-deps构建。有后缀的，可以根据后缀确定Debian版本，当你需要在此镜像上安装其他包时，后缀可以作为确定Debian版本的依据。

官方建议，当你的系统中包含许多不同镜像时，推荐使用无后缀tags。此类镜像基于buildpack-deps构建，该镜像包含了大量常用debian包，这会减少基于该镜像构建的其他镜像需要额外安装的包，从而减小系统中镜像的总大小。
```
| 版本 | 代号 |
| :----: | :----: |
| Debian 11 | bullseye |
| Debian 10 | buster |
| Debian 9 | stretch |
| Debian 8 | jessie |