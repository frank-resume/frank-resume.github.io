# PL
<details>
<summary>C</summary>

```
apt install gcc
gcc --version
```

</details>

<details>
<summary>PHP</summary>

<details>
<summary># Swoole Redis Memcached MongoDB Yaconf</summary>

```
wget https://pecl.php.net/get/swoole-4.4.8.tgz
wget https://pecl.php.net/get/redis-5.1.0.tgz
wget https://pecl.php.net/get/memcached-3.1.4.tgz
wget https://pecl.php.net/get/mongodb-1.6.0.tgz
wget https://pecl.php.net/get/yaconf-1.1.0.tgz
wget https://pecl.php.net/get/PDO_MYSQL-1.0.2.tgz

tar -zxvf xxx-x.x.x.tgz
cd xxx-x.x.x

/usr/local/php/bin/phpize
./configure --with-php-config=`which php-config`
make -j
make install
```

</details>

<details>
<summary># Xdebug</summary>

```
wget https://pecl.php.net/get/xdebug-2.9.0.tgz
tar -zxvf xdebug-2.9.0.tgz
cd xdebug-2.9.0

/usr/local/php/bin/phpize
./configure --with-php-config=`which php-config` --enable-xdebug
make -j
make install

[Xdebug]
zend_extension = xdebug
xdebug.auto_trace = on
xdebug.default_enable = on
xdebug.auto_profile = on
xdebug.collect_params = on
xdebug.collect_return = on
xdebug.profiler_enable = on
xdebug.remote_enable = 1
xdebug.remote_autostart = 1
xdebug.remote_host = "127.0.0.1"
xdebug.remote_port = 9000
xdebug.remote_handler = dbgp
xdebug.trace_output_dir = "/usr/local/php/xdebug/"
xdebug.profiler_output_dir = "/usr/local/php/xdebug/"
```

</details>

```
wget https://www.php.net/distributions/php-7.4.3.tar.gz
tar -zxvf php-7.4.3.tar.gz
cd php-7.4.3

apt install libxml2-dev

./configure --prefix=/usr/local/php/ --enable-fpm
make -j
make install
```

</details>

<details>
<summary>Python</summary>

```
wget https://www.python.org/ftp/python/3.8.1/Python-3.8.1.tar.xz
tar -zxvf Python-3.8.1.tar.xz
cd Python-3.8.1

apt install libffi-dev

./configure --prefix=/usr/local/python
make -j
make install
```

</details>

<details>
<summary>Java</summary>

```
wget https://download.oracle.com/otn-pub/java/jdk/14+36/076bab302c7b4508975440c56f6cc26a/jdk-14_linux-x64_bin.tar.gz?AuthParam=1584792536_3cc6bb36ee0fe7b7de91d1229f31625f
tar -zxvf jdk-14_linux-x64_bin.tar.gz
mv jdk-14 /usr/local/java

# /etc/profile.d/jdk.sh
export JAVA_HOME=/usr/local/java
export JRE_HOME=${JAVA_HOME}/jre
export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
export PATH=${JAVA_HOME}/bin:$PATH

# java -version
```

</details>

<details>
<summary>Golang</summary>

```
wget https://dl.google.com/go/go1.14.1.linux-amd64.tar.gz
tar -zxvf wget go1.14.1.src.tar.gz -C /usr/local/

export GOROOT=/usr/local/go
export GOBIN=$GOROOT/bin
export PATH=$GOBIN:$PATH
```

</details>

<details>
<summary>Node.js</summary>

```
wget https://nodejs.org/dist/v12.16.1/node-v12.16.1.tar.gz
tar -zxvf node-v12.16.1.tar.gz
cd node-v12.16.1

./configure
make -j
make install
```

</details>

# Storage
<details>
<summary>Redis</summary>

```
wget http://download.redis.io/releases/redis-5.0.7.tar.gz
tar -zxvf redis-5.0.7.tar.gz
cd redis-5.0.7

make -j
# ./src/redis-server ./redis.conf --daemonize yes
```

</details>

<details>
<summary>MySQL</summary>

```
wget http://downloads.sourceforge.net/project/boost/boost/1.59.0/boost_1_59_0.tar.gz
wget https://dev.mysql.com/get/Downloads/MySQL-5.7/mysql-boost-5.7.29.tar.gz
tar mysql-boost-5.7.29.tar.gz
cd mysql-boost-5.7.29

apt install cmake libncurses5-dev
cmake
make -j
make install

groupadd mysql
useradd -g mysql -s /bin/false mysql
mkdir -p /usr/local/mysql/data/
chown -R mysql /usr/local/mysql/data/

bin/mysqld --initialize-insecure --user=mysql --basedir=/usr/local/mysql --datadir=/usr/local/mysql/data
bin/mysql_ssl_rsa_setup  --user=mysql --basedir=/usr/local/mysql --datadir=/usr/local/mysql/data

cp support-files/my-default.cnf /etc/my.cnf
cp support-files/mysql.server /etc/init.d/mysqld
```

</details>

<details>
<summary>Memcached</summary>

```
wget http://www.memcached.org/files/memcached-1.5.20.tar.gz
tar -zxvf memcached-1.5.20.tar.gz
cd memcached-1.5.20

apt install libevent-dev

./configure --prefix=/usr/local/memcached
make -j
make install

export PATH=/usr/local/memcached/bin:$PATH
memcached -d -m 1024 -u root -l 127.0.0.1 -p 11211 -c 1024 -P /var/run/memcached.pid
telnet 127.0.0.1 11211
```

</details>

<details>
<summary>MongoDB</summary>

```
wget https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-ubuntu1804-4.2.3.tgz
tar -zxvf mongodb-linux-x86_64-ubuntu1804-4.2.3.tgz
mv mongodb-linux-x86_64-4.2.3/ /usr/local/mongodb

export PATH=/usr/local/mongodb/bin:$PATH
mkdir -p /data/db
mongod --dbpath=/data/db
```

</details>

# ElasticStack
<details>
<summary>ElasticSearch</summary>

```
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.6.1-linux-x86_64.tar.gz
tar -zxvf elasticsearch-7.6.1-linux-x86_64.tar.gz
cd elasticsearch-7.6.1
./bin/elasticsearch

# ./config/elasticsearch.yml
# access
network.host: 0.0.0.0
http.port: 9200
# machine learning
xpack.ml.enabled: false
# cors
http.cors.enabled: true
http.cors.allow-origin: "*"
# memory
bootstrap.memory_lock: false
bootstrap.system_call_filter: false
# cluster
cluster.name: es_cluster
node.name: es_cluster_master
node.master: true
discovery.zen.ping.unicast.hosts: ["127.0.0.1"]
cluster.initial_master_nodes: ["node-1"]

# /etc/security/limits.conf --- reboot
* soft nofile 65536
* hard nofile 65536
# /etc/sysctl.conf
# fs.file-max=655350
vm.max_map_count=655360
```

</details>

<details>
<summary>ES-head</summary>

```
git clone https://github.com/mobz/elasticsearch-head.git
cd elasticsearch-head
npm install

# npm run start
```

</details>

<details>
<summary>Kibana</summary>

```
wget https://artifacts.elastic.co/downloads/kibana/kibana-7.6.1-linux-x86_64.tar.gz
tar -zxvf kibana-7.6.1-linux-x86_64.tar.gz
cd kibana-7.6.1
./bin/kibana
```

</details>

<details>
<summary>Logstash</summary>

```
wget https://artifacts.elastic.co/downloads/logstash/logstash-7.6.1.tar.gz
tar -zxvf logstash-7.6.1.tar.gz
cd logstash-7.6.1
./bin/logstash
```

</details>

<details>
<summary>Beats</summary>

```

```

</details>

# Server
<details>
<summary>Nginx</summary>

```
wget http://nginx.org/download/nginx-1.16.1.tar.gz
tar -zxvf nginx-1.16.1.tar.gz
cd nginx-1.16.1

# http://zlib.net/zlib-1.2.11.tar.gz
# https://ftp.pcre.org/pub/pcre/pcre-8.43.tar.gz
# https://www.openssl.org/source/old/1.1.1/openssl-1.1.1d.tar.gz
apt install zlib1g-dev libssl-dev libpcre3-dev

./configure --with-http_ssl_module
make -j
make install
```

</details>

<details>
<summary>Jenkins</summary>

```
wget http://ftp-nyc.osuosl.org/pub/jenkins/war-stable/2.222.1/jenkins.war
wget https://mirrors.tuna.tsinghua.edu.cn/apache/tomcat/tomcat-9/v9.0.33/bin/apache-tomcat-9.0.33.tar.gz
wget https://mirror.bit.edu.cn/apache/maven/maven-3/3.6.3/binaries/apache-maven-3.6.3-bin.tar.gz

java8，java11
cloudbees-folder.hpi

java -jar jenkins.war
./tomcat/bin/startup.sh
```

</details>

<details>
<summary>Docker</summary>

```
wget https://download.docker.com/linux/static/stable/x86_64/docker-19.03.5.tgz
tar -zxvf docker-19.03.5.tgz
mv docker/* /usr/local/bin
groupadd docker
usermod -aG docker $USER

curl -L https://github.com/docker/compose/releases/download/1.25.4/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
```

</details>

<details>
<summary>Kubernetes</summary>

```
apt install apt-transport-https
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
cat <<EOF > /etc/apt/sources.list.d/kubernetes.list
deb https://mirrors.aliyun.com/kubernetes/apt kubernetes-xenial main
EOF
apt update && apt install kubectl kubeadm kubelet

swapoff -a && modprobe br_netfilter && sysctl -w net.ipv4.ip_forward=1
cat <<EOF > /etc/docker/daemon.json
{
  "exec-opts": ["native.cgroupdriver=systemd"]
}
EOF
kubeadm init --pod-network-cidr=10.244.0.0/16 --image-repository registry.aliyuncs.com/google_containers

mkdir -p $HOME/.kube
cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
chown $(id-u):$(id -g) $HOME/.kube/config
```

</details>

<details>
<summary>RabbitMQ</summary>

<details>
<summary>Erlang</summary>

```
export ERL_TOP=`pwd`

wget http://erlang.org/download/otp_src_22.2.tar.gz
tar -zxvf otp_src_22.2.tar.gz
cd otp_src_22.2

./configure --prefix=/usr/local/erlang
make -j
make install

export ERL_HOME=/path/to/install/erlang
export PATH=$PATH:$ERL_HOME/bin
```

</details>

```
wget http://erlang.org/download/otp_src_22.2.tar.gz
wget https://github.com/rabbitmq/rabbitmq-server/archive/v3.8.2.tar.gz
https://www.rabbitmq.com/releases/rabbitmq-server/v2.7.0/rabbitmq-server-generic-unix-2.7.0.tar.gz
tar -zxvf v3.8.2.tar.gz
cd rabbitmq-server-3.8.2
```

</details>

# Other
<details>
<summary>aliyun.ecs</summary>

```
远程连接密码:776286、修改实例密码

添加普通用户
adduser frank && usermod -aG sudo frank
用户 登录主机=(可切换用户:可执行命令) 无密码命令 --- NOPASSWD: ALL(不需要密码) --- ALL(需要密码)

安装环境->安全组->外网访问
```

</details>

<details>
<summary>cmd-alias</summary>

```
### C:\win-alias.bat
@echo off
doskey ls=dir $*
doskey php=wsl php $*

### regedit
计算机\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Command Processor
新建->字符串值 --- AutoRun: D:\wsl-tools\cmd-alias.bat
```

</details>

<details>
<summary>error-exception</summary>

```
PHP错误和异常

认识：
Error(错误)、Warning(警示)、Notice(提醒)
遇到错误程序终止，其他情况则继续执行

原因：
Parse error：少了分号，语句不完整
Fatal error：调用不存在的类、方法、函数和少给参数，require不存在的文件
Warning：除以0，缺少$符号，include不存在的文件
Notice：不存在的变量

问题：
Parse error、Fatal error、Warning、Notice，都会打印错误
Parse error、Fatal error，被Error捕获才不显示
Warning、Notice，由set_error_handler处理才不显示

处理：
错误类：Error，可以捕获用户抛出的Error异常、Parse error和Fatal error。但当前页面的Parse error捕获不了
异常类：Exception，可以捕获用户抛出的Exception异常。当然，用户可以自定义异常，但最好以Exception为基类
异常类：ErrorException，

预防：
set_error_handler：Warning、Notice和用户通过trigger_error触发error|warning|notice时，会交由该函数处理，用户未定义则使用系统的函数处理
register_shutdown_function：程序执行结束时都会调用该函数。如果是错误导致程序终止的，可以获取最后的错误信息

include 运行时加载，可能多次。程序继续执行(Warning)
require 开始就加载，只有一次。程序终止(Fatal error)
```

</details>

<details>
<summary>startup</summary>

```
### startup.vbs
Set ws = WScript.CreateObject("WScript.Shell")
ws.run "wsl sudo /etc/init.wsl", vbhide

### /etc/sudoers
%sudo   ALL=NOPASSWD: /etc/init.wsl

### /etc/init.wsl --- :set ff=unix
#! /bin/bash
/etc/init.d/ssh restart
/usr/local/nginx/sbin/nginx
/usr/local/php/sbin/php-fpm
redis-server /etc/redis/6379.conf --daemonize yes
/usr/local/mysql/bin/mysqld --user=mysql --log-error=/var/log/mysql/error.log --daemonize
/usr/local/memcached/bin/memcached -d
/usr/local/mongodb/bin/mongod --dbpath=/usr/local/mongodb/data
```

</details>

<details>
<summary>vscode</summary>

```
设置中文Ctrl + Shift + P

配置PHP可执行文件 win访问wsl

### PHP Intelephense
格式化快捷键Shift + Alt + F
输入提示、自动use、去掉未使用的use
跳转定义 类、方法

安装并默认wsl bash

Debug
```

</details>
