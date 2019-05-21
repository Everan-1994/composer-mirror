ZComposer 镜像诞生于2017年3月份，至今已运行了2年多。当前是第二次重构过的代码，基本是0故障，期间发现的一些停更问题，大多也是第三方接口调用策略/频率限制调整导致的误伤，沟通后也能很快解决。

## 镜像的安装部署

如果你想独立安装及部署镜像站点，详见[INSTALL.md]

## 镜像的使用方法

> 请尽可能用比较新的 Composer 版本。

使用 Composer 镜像加速有两种选项：

- 选项一：全局配置，这样所有项目都能惠及（推荐）；
- 选项二：单独项目配置；

选项一、全局配置（推荐）

```shell
$ composer config -g repo.packagist composer https://packagist.laravel-china.org
```

选项二、单独使用

如果仅限当前工程使用镜像，去掉 -g 即可，如下：    

```shell  
$ composer config repo.packagist composer https://packagist.laravel-china.org
```

## 遇到问题？

`composer` 命令后面加上 -vvv （是3个v）可以打印出调错信息，命令如下：

```shell
$ composer -vvv create-project laravel/laravel blog
$ composer -vvv require psr/log
```
   
如果自己解决不了，或发现 BUG，可以在 [@扣丁禅师](https://laravel-china.org/users/12063) 的 GitHub 上 [创建 Issue](https://github.com/zencodex/composer/issues/new)。

注意提问时请带上 -vvv 的输出，并且要求叙述清晰，第一次提问的同学请阅读 [关于提问的智慧](https://laravel-china.org/topics/2396/wisdom-of-asking-questions-chinese-version)。

## 常见问题

1. 已存在 composer.lock 文件，先删除，再运行 `composer install` 重新生成。
> 原因：composer.lock 缓存了之前的配置信息，从而导致新的镜像配置无效。

2. 使用 `laravel new` 命令创建工程， 这个命令会从 [这里](http://cabinet.laravel.com/latest.zip) 下一个zip包，里面自带了 composer.lock，和上面原因一样，也无法使用镜像加速，解决方法：

- 方法一（推荐）：
不使用 `laravel new`，直接用 `composer create-project laravel/laravel xxx` 新建工程。

- 方法二：
运行 `laravel new xxx`，当看见屏幕出现 - Installing doctrine/inflector 时，`Ctrl + C` 终止命令，cd xxx 进入，删除 composer.lock，再运行 `composer install`。

3. 缓存多久更新一次？

- 0时 - 早上7时，这个时间段考虑使用人数不会太频繁，间隔为15分钟
- 其余时间，间隔为5分钟

> 正常更新速度可在1分内完成 ，但更新太快，会降低CDN命中率，如果总有新文件让CDN去缓存，反而拖慢了速度，所以故意加了些延迟。我们每次采集中还会删减掉数千个僵尸包，以加快传输速度。

## 安装 Composer

### Linux/Mac：

    wget https://dl.laravel-china.org/composer.phar -O /usr/local/bin/composer
	chmod a+x /usr/local/bin/composer
 
 如遇权限不足，可添加 `sudo`。
 
###  Windows：

1. 直接下载 composer.phar，地址：https://dl.laravel-china.org/composer.phar
2. 把下载的 composer.phar 放到 PHP 安装目录
3. 新建 composer.bat, 添加如下内容，并保存：  

<pre>@php "%~dp0composer.phar" %*</pre>

### 查看当前版本

```shell
$ composer -V
```

### 升级版本

```shell
$ composer selfupdate
```

> 注意 `selfupdate` 升级命令会连接官方服务器，速度很慢。建议直接下载我们的 `composer.phar` 镜像，每天都会更新到最新。
