# Huobipool-Guard

## 使用说明

### 一、 安装 Docker

参考资料: https://docs.docker.com/engine/install/ubuntu/

在终端中执行以下命令:

```
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
```

### 二、 启动 Guard

在终端中执行以下命令启动 Guard:

```
sudo docker run -it -d \
--name huobipool-guard \
--volume /etc/machine-id:/etc/machine-id \
registry.cn-hongkong.aliyuncs.com/huobipool-public/scanner-guard:prd
```

### 三、 查看 Guard ID

在终端中执行以下命令查看日志:

```
sudo docker logs huobipool-guard
```

找到 "Guard ID: xxxxxxxxxxxxxxxxxxxxxxxxx" 信息, 将该信息进行反馈, 得到确认后前往 https://guard.hpt.com/ 注册账号, 并用该 ID 添加绑定矿场.

### 四、 配置扫描 IP 段

在 https://guard.hpt.com/ 绑定完成后, 前往 设置中心-IP段管理 添加扫描IP范围, Guard 将自动更新扫描配置, 对设置的 IP 段进行扫描.

### 五、 其它

#### 1. Guard 的更新

##### 1.1 手动更新

执行以下命令来获取最新的 Guard, 并停止当前运行的 Guard:

``` 
sudo docker pull registry.cn-hongkong.aliyuncs.com/huobipool-public/scanner-guard:prd
sudo docker rm -f huobipool-guard
```

然后使用 步骤2 的命令来启动 Guard.

##### 1.2 配置自动更新

执行以下命令来启动自动更新:

```
sudo docker run --detach \
--name watchtower \
--volume /var/run/docker.sock:/var/run/docker.sock \
containrrr/watchtower --interval 300
```

此后 Guard 将一直保持最新版本运行.
