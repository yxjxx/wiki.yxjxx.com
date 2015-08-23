---
title: "cron"
date: 2015-08-23 14:41
---

cron的作用是定时执行命令。每分钟，每小时，每天，或者每周的某一天，也可以是每年的某一天。

anacron是cron命令的补充，cron命令适合24x7不停机的服务器，anacron适合经常会关机的个人电脑。在每次开机时检测关机期间没能执行的命令并执行。

*********************

cron相关的文件(ubuntu，其它发行版本有差异)

1. `/etc/crontab` 系统的cron命令，里面指定了每小时，每天，每月要执行的脚本所在的文件夹
2. `crontab -e`命令，修改用户的cron命令列表，格式为`m h dom mon dow command`(即分 小时 日期 月 星期 命令)，比如每三十分钟重启dropbox的cron命令是这样的`*/30 * * * * rsdropbox`(`/`表示除)
3. `crontab -l`命令列出用户定义的cron命令
4. `run-parts` 可以自定义定时执行指定文件夹下所有的脚本
5. cron命令执行的log在`/var/log/syslog`中，使用`grep CRON /var/log/syslog`单独查看cron的log

******

[cron more details reference](http://www.thegeekstuff.com/2009/06/15-practical-crontab-examples/)

[anacron more details reference](http://www.thegeekstuff.com/2011/05/anacron-examples/)
