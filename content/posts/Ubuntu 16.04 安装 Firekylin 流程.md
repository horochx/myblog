+++
title = "Ubuntu 16.04 安装 Firekylin 流程"
date = "2017-12-01T15:22:30+08:00"
author = "horochx" 
cover = ""
tags = ["Linux"]
description = "Firekylin 是一个基于 Node.js 实现的简单、快速的博客平台。"
showFullContent = false
+++

Firekylin 是一个基于 Node.js 实现的简单、快速的博客平台。

## 运行环境

> Firekylin 需要 Node.js 4.0+ 和 MySQL 环境的支持。

在安装博客之前，我们要确保服务器上安装了相关环境。

- ### 安装 Node.js

  Node.js 的安装采用包管理的方式：

  ```bash
  curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
  sudo apt-get install -y nodejs
  sudo apt-get install -y build-essential
  ```

  安装完成后，如果执行 `node -v` 输出了正确的版本号，说明 node 已经成功安装。

- ### 安装 MySQL

  MySQL 的安装采用包管理的方式：

  ```bash
  sudo apt-get update
  sudo apt-get install mysql-server
  ```

  安装过程中，依据提示创建 MySQL 的 root 密码。安装完成后，执行如下命令初始化 MySQL：

  ```bash
  mysql_secure_installation
  ```

  初始化过程中，依据提示输入刚刚创建的 root 密码。除了询问是否要更改 root 密码外，其它设置可以按`Y`和`回车键`保持默认设置。初始化完成后，使用如下命令登录至 MySQL：

  ```bash
  mysql -u root -p
  ```

  按照提示输入 MySQL 的 root 密码。现在，我们可以执行如下命令为 Firekylin 创建数据库：

  ```sql
  CREATE DATABASE firekylin;
  ```

  _firekylin_ 是数据库名，可以替换成其它你喜欢的名字。接下来，我们需要为 Firekylin 创建一个访问数据库的用户：

  ```sql
  CREATE USER firekylinAdmin@localhost IDENTIFIED BY 'password';
  ```

  其中，_firekylinAdmin_ 是用户名，_password_ 是登录密码。请将 _password_ 更换为一个安全的强密码。最后，我们将 Firekylin 的数据库权限赋予这个用户：

  ```sql
  GRANT ALL PRIVILEGES ON firekylin.* TO firekylinAdmin@localhost;
  ```

  注意，请将代码中的 _firekylin_ 与 _firekylinAdmin_ 替换为你自己创建的数据库名与用户名。最后，更新我们所做的权限修改：

  ```sql
  FLUSH PRIVILEGES;
  ```

  至此，MySQL 的所有配置均已完成，执行如下命令退出 MySQL：

  ```sql
  exit;
  ```

## 安装 Firekylin

Firekylin 的安装采用安装包安装，仓库克隆安装参见<a href="https://github.com/firekylin/firekylin/wiki/仓库版安装" target="_blank">官方教程</a>。

1. 下载最新版本 Firekylin：

   ```bash
   wget https://firekylin.org/release/latest.tar.gz
   ```

1. 解压缩安装包：

   ```bash
   tar xvf latest.tar.gz
   ```

1. 安装依赖：

   ```bash
   cd firekylin
   # 国内用户请先添加 npm 淘宝源
   # npm install --registry=https://registry.npm.taobao.org
   npm install
   ```

1. 配置 PM2：

   修改程序目录下 `pm2_default.json` 文件中的 `cwd` 配置项的值，将其改成当前路径，然后启动 Firekylin：

   ```bash
   sudo npm install -g pm2
   mv pm2_default.json pm2.json
   pm2 startOrReload pm2.json
   ```

## 配置 Nginx

1. 配置虚拟主机：

   修改程序目录下 `nginx_default.conf` 文件中的 `server_name`、`root` 配置项的值，将其改为你的域名与程序目录下 `www` 文件夹的路径。然后复制至 Nginx 配置文件目录：

   ```bash
   mv nginx_default.conf /etc/nginx/sites-enabled/firekylin
   ```

1. 配置 HTTPS：

   我们使用 <a href="https://letsencrypt.org/" target="_blank">Let's Encrypt</a> 的免费服务来配置 HTTPS 访问。

   1. 安装 certbot：

      ```bash
      sudo apt-get update
      sudo apt-get install software-properties-common
      sudo add-apt-repository ppa:certbot/certbot
      sudo apt-get update
      sudo apt-get install python-certbot-nginx
      ```

   1. 安装证书：

      ```bash
      sudo certbot --nginx
      ```

      安装过程中，依据提示输入邮箱、想要使用 HTTPS 访问的域名。Let's Encrypt 的免费证书只有三个月有效期，到期之后执行如下命令更新证书：

      ```bash
      certbot renew
      ```

1. 重启 Nginx 服务：

   ```bash
   service nginx restart
   ```

## 访问博客地址完成配置

使用浏览器访问博客地址即可看到 Firekylin 的安装程序，将先前配置的 MySQL 用户名、密码、数据库名填入相应位置，主机填写`localhost`，端口、表前缀保持不变。

## 完成安装

安装完成后会重新进入博客首页，依照博客首页自动生成的文章完成对博客的后续配置。
