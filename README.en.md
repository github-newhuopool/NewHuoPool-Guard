# Huobipool-Guard

> It is recommended to use Docker to manage and run it. If you have problems running Docker on Windows, you can download a separate Windows version of the executable to run from the [Release](https://github.com/github-huobipool/Huobipool-Guard/releases) page.

## Instructions for use

### I. Installing Docker

Reference: https://docs.docker.com/engine/install/

Execute the following command in the terminal:

```
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
```

### II. Starting Guard

Execute the following command in the terminal to start Guard:

```
sudo docker run -it -d \
--name huobipool-guard \
--volume /etc/machine-id:/etc/machine-id \
registry.cn-hongkong.aliyuncs.com/huobipool-public/scanner-guard:prd
```

### III. View Guard ID

Execute the following command in the terminal to view the logs:

```
sudo docker logs huobipool-guard
```

Find the message "Guard ID: xxxxxxxxxxxxxxxxxxxxxxxxxxxxx", send the message back, get the confirmation, go to https://guard.hpt.com/ to register the account, and use the ID to bind the mine.

### IV. Configure the scanning IP segment

After the mine is bound on https://guard.hpt.com/ , go to `Settings Center` - `IP Segment Management` to add the scanning IP range, Guard will automatically update the scanning configuration to scan the set IP segment.

### V. Other

#### 1. Update of Guard

##### 1.1 Manual update

Execute the following command to get the latest Guard, and stop the currently running Guard:

``` 
sudo docker pull registry.cn-hongkong.aliyuncs.com/huobipool-public/scanner-guard:prd
sudo docker rm -f huobipool-guard
```

Then use the command from step 2 to start the Guard.

##### 1.2 Configuring Automatic Updates

Execute the following command to start automatic updates:

```
sudo docker run --detach \
--name watchtower \
--volume /var/run/docker.sock:/var/run/docker.sock \
containrrr/watchtower --interval 300
```

After that Guard will always run with the latest version.
