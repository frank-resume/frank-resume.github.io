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
memcached -d -m 1024 -u root -l 127.0.0.1 -p 11211 -c 1024 -P /tmp/memcached.pid
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
<summary>Docker</summary>

```
1.安装依赖包
apt-get install software-properties-common

2.添加GPG密钥
curl -fsSL https://mirrors.ustc.edu.cn/docker-ce/linux/ubuntu/gpg | apt-key add -

3.添加软件源
add-apt-repository "deb [arch=amd64] https://mirrors.ustc.edu.cn/docker-ce/linux/ubuntu $(lsb_release -cs) stable"

4.安装docker和docker-compose
apt-get install docker-ce
apt-get install docker-compose

5.添加服务和启动docker
systemctl enable docker
systemctl start docker

6.添加组和加入组
groupadd docker
usermod -aG docker $USER
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
