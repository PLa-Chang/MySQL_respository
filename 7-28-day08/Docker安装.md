在ubuntu中使用docker

# 安装docker

## 卸载旧版本

如需要，先卸载旧版本

```sh
sudo apt-get remove docker docker-engine docker.io containerd runc
```



## 获取软件最新源

```sh
sudo apt-get update
```



## 安装 apt 依赖包

用于通过HTTPS来获取仓库

```sh
sudo apt-get -y install apt-transport-https ca-certificates curl software-properties-common
```



## 安装GPG证书

```sh
curl -fsSL https://mirrors.aliyun.com/docker-ce/linux/ubuntu/gpg | sudo apt-key add -
```



## 验证

```sh
sudo apt-key fingerprint 0EBFCD88
```



## 设置稳定版仓库

```sh
sudo add-apt-repository "deb [arch=amd64] https://mirrors.aliyun.com/docker-ce/linux/ubuntu $(lsb_release -cs) stable"
```



# 安装 Docker Engine-Community

## 更新 apt 包索引

```sh
sudo apt-get update
```



## 安装最新版本

```sh
sudo apt-get install docker-ce docker-ce-cli containerd.io
```



## 测试

```sh
sudo docker run hello-world
```

显示以下结果，表示安装成功

![1690276577287](assets/1690276577287.png)



# 管理docker

显示docker状态

```sh
systemctl status docker
```



启动docker

```sh
systemctl start docker
```



停止docker

```sh
systemctl stop docker
```



重启docker

```sh
systemctl restart docker
```



开机启动

```sh
sudo systemctl enable docker
```





