---
layout: post
title: 记一次crontab不生效的排查过程
slug: 简单、快速
date: 2020-11-25 15:18:15
status: publish
author: <greezen>
categories: 
  - work
    - linux  
tags: 
  - linux
excerpt: 
---

#### 问题描述
> 创建了一个每天1点执行的定时任务，第二天发现脚本没有正常执行
#### 问题分析
1. 手动执行脚本，并检查权限
   > 正常执行
2. 修改成1分钟执行一次
   > 正常执行
3. 查看定时任务日志
   ```bash
   vi /var/log/cron
   ```
   > 日志中无明显错误，但日志记录的时间`不是北京时间`
4. 查看当前时间
   > 当前时间是北京时间无误
5. 重启crond服务和syslog服务
   ```bash
    systemctl restart rsyslog
    systemctl restart crond.service

   ```
6. 第二天观察执行情况
   > 正常执行，问题解决
#### 总结
> linux服务器，原来非北京时间，后来有修改成北京时间，但是相关的定时任务服务和日志服务，未重启导致