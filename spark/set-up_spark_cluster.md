# Spark集群搭建
系统：Ubuntu 16.04

role | IP | user
-- | -- | --
master | 10.0.0.6 | ubuntu
slave01 | 10.0.0.2 | lxx
slave02 | 10.0.0.4 | jermaine

## 免密登录
需要master免密登录slaves  
正常SSH：`ssh lxx@10.0.0.2`，然后输入密码。
* 设置公钥登录，不用输入密码；
* 设置`.ssh/config`，可将`lxx@10.0.0.2`替换为指定字符串；
* 设置`/etc/hosts`，将ip地址替换为指定字符串；

最终效果：  
免密SSH：`ssh slave01`，OK了。

首先slaves要安装`openssh-server`，才能被远程登录。（Ubuntu缺省已经安装了`ssh client`）  
`sudo apt-get install openssh-server`

### 公钥登录
1. master生成密钥  
`ssh-keygen -t rsa -P ""`
2. 将master的`~/.ssh/id_rsa.pub`拷贝到每个slave的`~/.ssh/authorized_keys`  
`ssh-copy-id -i ~/.ssh/id_rsa.pub user@host`  
等价于  
`ssh user@host 'mkdir -p .ssh && cat >> .ssh/authorized_keys' < ~/.ssh/id_rsa.pub`

### ssh config
向`.ssh/config`写入如下配置，这样只要`ssh slave01`就相当于`ssh lxx@10.0.0.2`
```
Host slave01
  Hostname 10.0.0.2
  User lxx
```
注：经实测，不写`User`那行也可以，只要配置好`hosts`

### hosts
修改`/etc/hosts`。建议修改，免去输入IP地址。
```
10.0.0.6        master
10.0.0.2        slave01
10.0.0.4        slave02
```


## 安装JDK
安装openjdk-8-jdk：
`sudo apt-get install openjdk-8-jdk`



## Spark配置
从 [http://spark.apache.org/downloads.html](http://spark.apache.org/downloads.html)
下载Spark  
需要将其解压到所有的结点的相同位置上，且不需要额外权限。例如，如果所有结点的用户名相同，则可将其放在`~`下。如果不相同，则选择一个统一的路径，可以放在`/usr/local/`下，由于此目录为root所有，所以需要修改Spark目录的所有者。
以后者为例，且假设在slave01上：
```
sudo tar -zxf ~/Download/spark-2.3.0-bin-hadoop2.7.tgz -C /usr/local/
cd /usr/local
sudo chown -R slave01：slave01 ./spark-2.3.0-bin-hadoop2.7
```

配置Spark
```
cd /usr/local/spark-2.3.0-bin-hadoop2.7
cp ./conf/slaves.template ./conf/slaves
echo master >> conf/slaves
echo slave01 >> conf/slaves
echo slave02 >> conf/slaves
echo "export SPARK_MASTER_HOST=10.0.0.6" >> spark-env.sh
```

启动Spark  
`./sbin/start-all.sh`

在浏览器上查看独立集群管理器Spark集群信息  
`http://master:8080`
