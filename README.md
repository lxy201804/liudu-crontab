# 接口化秒级定时任务

## 概述

基于 **Workerman** + **MySQL** 的接口化秒级定时任务管理，兼容 Windows 和 Linux 系统。



## 定时器格式说明

```
0   1   2   3   4   5
|   |   |   |   |   |
|   |   |   |   |   +------ day of week (0 - 6) (Sunday=0)
|   |   |   |   +------ month (1 - 12)
|   |   |   +-------- day of month (1 - 31)
|   |   +---------- hour (0 - 23)
|   +------------ min (0 - 59)
+-------------- sec (0-59)[可省略，如果没有0位,则最小时间粒度是分钟]
```



## 简单使用

- **新建 run.php**

```php
<?php

require_once "./vendor/autoload.php";

use Liudu\HttpCrontab;

date_default_timezone_set('PRC');

//数据库配置
//启动脚本后会自行创建所需的数据表
//定时器任务执行日志按月自动分表
$dbConfig = [
    'hostname' => '127.0.0.1',
    'hostport' => '3306',
    'username' => 'root',
    'password' => 'root',
    'database' => 'test',
    'charset' => 'utf8mb4'
];

//启动后默认监听 http://127.0.0.1:2345 
//可在new的时候传递第一个参数改变监听地址
(new HttpCrontab())->setDebug(true)
    ->setName('System Crontab')
    ->setDbConfig($dbConfig)
    ->run();
```

- **启动服务**

![](https://i.loli.net/2021/09/23/dTGRMSjkQZyWIbH.png)

