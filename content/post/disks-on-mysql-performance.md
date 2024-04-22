---
title: "在不同的硬盘下,MySql表现如何"
description: Disks on Mysql Performance
slug: disks-on-mysql-performance
date: 2024-04-22T07:01:11+08:00
image:
categories:
    - databases
tags:
    - mysql
    - disk
    - performance
weight: 1
---

# 磁盘性能对于的数据库战斗力的影响

数据库中的数据最终皆是需要储存在硬盘之中的,硬盘的性能对于数据库性能有着决定性的影响.一直一来都听说更高的IOPS会显著增强数据库的战斗力,因此在这里拿出我的几块硬盘出来测试一下

> 事先声明以下数据仅供参考.请根据自己的实际情况做出选择

## 测试环境

- 系统: Ubuntu 23.10
- CPU: Intel(R) Xeon(R) CPU E5-2683 v3 @ 2.00GHz
- 内存: 192GB REG ECC ddr4 2133MHz
- Docker version 26.0.1, build d260a54
- MySql 8 latest official image

> 据我所知,在docker中测试磁盘性能大概会有10%左右的损失,但是至少结果是公平的.可以体现出不同参赛选手的实际水平

## 参赛选手 `4K iops`

- SAS 希捷单盘 `625 IOPS`
- LSI3008 希捷 sata x4 raid0 `924 IOPS`
- zfs 西数 sata x5 raid0 `1 184 IOPS`
- sata 杂牌固态 `27 000 IOPS`
- nvme 傲腾内存 `222 000 IOPS`

## 测试方法

同一个数据库分别拷贝到不同的硬盘上,然后进行相同的测试
 
## 比赛结果

## 赛后点评
