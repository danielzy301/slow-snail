# Linux下MySQL定时自动完整备份（mysqldump+crontab）

[ken.io](https://cloud.tencent.com/developer/user/1381082)[Ken的杂谈](https://cloud.tencent.com/developer/column/5248)订阅

https://cloud.tencent.com/act/pro/mysql?from=11045

## 在这篇文章中：

- 一、前言
  - [1、本文主要内容](javascript:;)
  - [2、环境信息](javascript:;)
- 二、备份准备&备份测试
  - [1、备份目录准备](javascript:;)
  - [2、备份脚本准备](javascript:;)
  - [3、备份测试&验证](javascript:;)
- 三、定时任务
  - [1、定时执行MySQL完整备份](javascript:;)
  - [2、定时清理7天以前的备份](javascript:;)
- 四、备注
  - [1、crontab命令示例](javascript:;)
- [2、附录](javascript:;)

## 一、前言

### 1、本文主要内容

- 实现数据库全量备份
- 实现定时执行备份
- 实现定时清理7天之前的备份

### 2、环境信息

| 环境/工具 | 说明                            |
| :-------- | :------------------------------ |
| MySQL     | v5.7.x                          |
| mysqldump | MySQL自带的数据导出工具         |
| crontab   | 功能相当于Windows的任务计划工具 |

## 二、备份准备&备份测试

### 1、备份目录准备

```javascript
#mysql专用目录
mkdir /mysql
#mysql备份目录
mkdir /mysql/backup
#mysql备份脚本
mkdir /mysql/backup/scripts
#mysql备份文件
mkdir /mysql/backup/files
#mysql备份日志
mkdir /mysql/backup/logs
```

### 2、备份脚本准备

- 新建完整备份脚本

```javascript
vi /mysql/backup/scripts/backup_full.sh
```

- 脚本内容

```javascript
#!/bin/bash

#备份目录
BACKUP_ROOT=/mysql/backup
BACKUP_FILEDIR=$BACKUP_ROOT/files
BACKUP_LOGDIR=$BACKUP_ROOT/logs

#当前日期
DATE=$(date +%Y%m%d)

######备份######

#查询所有数据库
#-uroot -p123456表示使用root账号执行命令，且root账号的密码为:123456
DATABASES=$(mysql -uroot -p123456 -e "show databases" | grep -Ev "Database|sys|information_schema")
#DATABASES=$(mysql -uroot -p123456 -e "SELECT SCHEMA_NAME FROM information_schema.SCHEMATA WHERE SCHEMA_NAME NOT IN ('sys','mysql','information_schema','performance_schema');" | grep -v "SCHEMA_NAME","ken.io") 
echo $DATABASES
#循环数据库进行备份
for db in $DATABASES
do
echo
echo ----------$BACKUP_FILEDIR/${db}_$DATE.sql.gz BEGIN----------
mysqldump -uroot -pRoot@1024 --default-character-set=utf8 -q --lock-all-tables --flush-logs -E -R --triggers -B ${db} | gzip > $BACKUP_FILEDIR/${db}_$DATE.sql.gz
echo ----------$BACKUP_FILEDIR/${db}_$DATE.sql.gz COMPLETE----------
echo
done

echo "done"
```

### 3、备份测试&验证

```javascript
#执行备份脚本
sh /mysql/backup/scripts/backup_full.sh

#查看备份文件
ll /mysql/backup/files -h

#解压指定文件({file}自己替换成备份的文件)
gunzip /mysql/backup/files/{file}
```

## 三、定时任务

- 安装crontab

```javascript
yum install -y crontab
```

### 1、定时执行[MySQL](https://cloud.tencent.com/product/cdb?from=10680)完整备份

- 创建定时备份任务

```javascript
#添加定时任务
crontab -e

#每天凌晨3点执行
00 3 * * * sh /mysql/backup/scripts/backup_full.sh

#查看定时任务
crontab -l
```

### 2、定时清理7天以前的备份

- 创建文件清理脚本

```javascript
#创建脚本文件
vi /mysql/backup/scripts/backup_full_clean.sh

#写入以下内容
#!/bin/bash
find /mysql/backup/files -mtime +7 -name "*.gz" -exec rm -rf {} \;
```

- 创建定时清理任务

```javascript
#添加定时任务
crontab -e

#每天凌晨1点执行
00 1 * * * sh /mysql/backup/scripts/backup_full_clean.sh

#查看定时任务
crontab -l
```

## 四、备注

### 1、crontab命令示例

| 命令                          | 说明                                       |
| :---------------------------- | :----------------------------------------- |
| * * * * * command             | 每1分钟执行一次command                     |
| 30 * * * * command            | 每30分钟执行一次command                    |
| 3,59 * * * * myCommand        | 每小时的第3和第59分钟执行                  |
| 3,59 9-18 * * * myCommand     | 在上午9点到18点的第3和第59分钟执行         |
| 3,59 9-18 */2  *  * myCommand | 每隔两天的上午9点到18点的第3和第59分钟执行 |
| 3,59 9-18 * * 1 myCommand     | 每周一上午9点到18点的第3和第59分钟执行     |

## 2、附录

- https://blog.csdn.net/zmcyu/article/details/75353245
- http://linuxtools-rst.readthedocs.io/zh_CN/latest/tool/crontab.html