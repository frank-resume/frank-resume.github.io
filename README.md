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
<summary># extension</summary>

```
wget https://pecl.php.net/get/swoole-4.4.8.tgz
wget https://pecl.php.net/get/redis-5.1.0.tgz
wget https://pecl.php.net/get/memcached-3.1.4.tgz
wget https://pecl.php.net/get/mongodb-1.6.0.tgz
wget https://pecl.php.net/get/yaconf-1.1.0.tgz
wget https://pecl.php.net/get/mcrypt-1.0.3.tgz
wget https://pecl.php.net/get/xdebug-2.9.0.tgz

tar -zxvf abc-x.y.z.tgz
cd abc-x.y.z

apt install autoconf
# ./lib/php/build/

/usr/local/php/bin/phpize
./configure --with-php-config=`which php-config`
make -j
make install



# gd
apt install libpng-dev libfreetype6-dev
./configure --with-php-config=`which php-config` --with-freetype

# mysqli
./configure --with-php-config=`which php-config` --with-mysqli=/usr/local/mysql/bin/mysql_config

# pdo_mysql
./configure --with-php-config=`which php-config` --with-pdo-mysql=/usr/local/mysql

# pdo_odbc
apt install unixodbc-dev
./configure --with-php-config=`which php-config` --with-pdo-odbc=unixODBC,/usr

# zlib
cp config0.m4 config.m4

# mbstring
apt install libonig-dev

# curl
apt install libcurl3-dev

# mcrypt
apt install libmcrypt-dev

# memcached
apt install libmemcached-dev
```

</details>

```
wget https://www.php.net/distributions/php-7.4.3.tar.gz
tar -zxvf php-7.4.3.tar.gz
cd php-7.4.3

apt install libxml2-dev libsqlite3-dev

./configure --prefix=/usr/local/php7.4.3 --enable-fpm
make -j
make install

# cp -a ./php.ini-development /usr/local/php/lib/php.ini
# cp -a ./sapi/fpm/init.d.php-fpm.in /etc/init.d/php-fpm
```

</details>

<details>
<summary>Python</summary>

```
wget https://www.python.org/ftp/python/2.7.17/Python-2.7.17.tgz
tar -zxvf Python-2.7.17.tgz
cd Python-2.7.17

apt install libffi-dev

./configure --prefix=/usr/local/python2.7.17
make -j
make install
```

</details>

<details>
<summary>Java</summary>

```
wget https://download.oracle.com/otn/java/jdk/8u231-b11/5b13a193868b4bf28bcb45c792fce896/jdk-8u231-linux-x64.tar.gz?AuthParam=1587322313_4b0e09d5b9c524ef820aae003afe09ea
tar -zxvf jdk-8u231-linux-x64.tar.gz
mv jdk1.8.0_231 /usr/local/java

# /etc/profile.d/jdk.sh
export JAVA_HOME=/usr/local/java
export JRE_HOME=$JAVA_HOME/jre
export CLASSPATH=.:$JAVA_HOME/lib:$JRE_HOME/lib
export PATH=$JAVA_HOME/bin:$PATH

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

./configure --prefix=/usr/local/node12.16.1
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
make PREFIX=/usr/local/redis5.0.7 install

# cp -a ./*.conf /usr/local/redis/conf/
# ./src/redis-server ./redis.conf --daemonize yes
```

</details>

<details>
<summary>MySQL</summary>

```
wget https://dev.mysql.com/get/Downloads/MySQL-8.0/mysql-boost-8.0.18.tar.gz
wget https://dev.mysql.com/get/Downloads/MySQL-5.7/mysql-boost-5.7.28.tar.gz
tar -zxvf mysql-boost-5.7.28.tar.gz
cd mysql-5.7.28

apt install cmake libncurses5-dev libssl-dev
cmake . -DCMAKE_INSTALL_PREFIX=/usr/local/mysql5.7.28 -DWITH_BOOST=boost
make -j
make install

groupadd mysql
useradd -g mysql -s /bin/false mysql
mkdir -p /usr/local/mysql/data
chown -R mysql /usr/local/mysql/data

bin/mysqld --initialize-insecure --user=mysql --basedir=/usr/local/mysql --datadir=/usr/local/mysql/data
bin/mysql_ssl_rsa_setup --user=mysql --basedir=/usr/local/mysql --datadir=/usr/local/mysql/data

bin/mysqld --user=mysql --daemonize --log-error=/var/log/mysql/error.log

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
memcached -d -u root -m 1024 -l 127.0.0.1 -p 11211 -c 1024 -P /usr/local/var/run/memcached.pid
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
mkdir -p /usr/local/mongodb/data
mongod --dbpath=/usr/local/mongodb/data --fork --logpath=/usr/local/mysql/mysql.log
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
# cors
http.cors.enabled: true
http.cors.allow-origin: "*"
# memory
bootstrap.memory_lock: false
bootstrap.system_call_filter: false
# machine learning
xpack.ml.enabled: false

# cluster
cluster.name: es_cluster
node.name: es_cluster_master
node.master: true
node.data: false
http.enable: true
# discovery
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
<summary>Filebeats</summary>

```
wget https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.6.1-linux-x86_64.tar.gz
tar -zxvf filebeat-7.6.1-linux-x86_64.tar.gz
cd filebeat-7.6.1
./bin/filebeat
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
apt install libpcre3-dev libssl-dev zlib1g-dev

./configure --prefix=/usr/local/nginx1.16.1 --with-http_ssl_module
make -j
make install
```

</details>

<details>
<summary>Apache</summary>

```
wget https://downloads.apache.org/httpd/httpd-2.4.43.tar.gz
tar -zxvf httpd-2.4.43.tar.gz
cd httpd-2.4.43

# wget https://downloads.apache.org/apr/apr-1.7.0.tar.gz
apt install libexpat1-dev
# wget https://downloads.apache.org/apr/apr-util-1.6.1.tar.gz
apt install zlib1g-dev libssl-dev libpcre3-dev

./configure --prefix=/usr/local/httpd2.4.43
make -j
make install
```

</details>

<details>
<summary>Lua</summary>

```
wget http://www.lua.org/ftp/lua-5.3.5.tar.gz
wget http://luajit.org/download/LuaJIT-2.0.5.tar.gz
tar -zxvf lua-5.3.5.tar.gz
cd lua-5.3.5

apt install libreadline-dev

make linux
make install
```

</details>

<details>
<summary>Jenkins</summary>

```
wget http://ftp-nyc.osuosl.org/pub/jenkins/war-stable/2.222.1/jenkins.war
wget https://mirrors.tuna.tsinghua.edu.cn/apache/tomcat/tomcat-9/v9.0.33/bin/apache-tomcat-9.0.33.tar.gz
wget https://mirror.bit.edu.cn/apache/maven/maven-3/3.6.3/binaries/apache-maven-3.6.3-bin.tar.gz

# java8, java11
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
wget https://github.com/rabbitmq/rabbitmq-server/archive/v3.8.2.tar.gz
wget https://github.com/rabbitmq/rabbitmq-server/releases/download/v3.8.2/rabbitmq-server-generic-unix-3.8.2.tar.xz
tar -zxvf rabbitmq-server-generic-unix-3.8.2.tar.xz
cd rabbitmq-server-3.8.2
```

</details>
