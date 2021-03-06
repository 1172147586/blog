## CentOS下安装PHP拓展Swoole

[Swoole官网](https://www.swoole.com/)

## 系统版本

* CentOS Linux release 7.5.1804 (Core)
* PHP 7.1.18

## 使用源码安装

### 安装系统依赖

```
sudo yum install -y gcc glibc-headers gcc-c++
```

### 安装PHP71

这里简单使用yum方式安装。

```
sudo yum install -y epel-release && sudo rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm
sudo yum install -y php71w php71w-gd php71w-curl php71w-common php71w-cli php71w-mysql php71w-mbstring php71w-fpm php71w-xml php71w-pdo php71w-zip php71w-devel
```

### 下载Swoole源码并安装

查看最新的[Swoole源码](https://github.com/swoole/swoole-src/releases)，这里选择`v4.0.0-rc1`版本安装。

```
cd /usr/local/src/ && wget https://github.com/swoole/swoole-src/archive/v4.0.0-rc1.tar.gz -O swoole.v4.0.0-rc1.tar.gz
tar xf swoole.v4.0.0-rc1.tar.gz
phpize
./configure
make
sudo make install
```
> 默认将生成的`swoole.so`文件放置在`/usr/lib64/php/modules/`下。

### 配置php.ini

通过命令`php --ini`查到`php.ini`文件所在路径，这里是`/etc/php.ini`，编辑它，在合适的位置新增下面行。

```
extension=swoole.so
```

### 验证

执行下面的命令检查是否成功引入Swoole拓展。

```
php -m |grep swoole
```
