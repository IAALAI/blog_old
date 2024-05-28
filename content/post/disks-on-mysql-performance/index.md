---
title: "在不同的硬盘下,MySql表现如何"
description: Disks on Mysql Performance
slug: disks-on-mysql-performance
date: 2024-05-28
image:
categories:
    - databases
tags:
    - mysql
    - disk
    - performance
    - todo
weight: 1
---

# 磁盘性能对于的数据库战斗力的影响

数据库中的数据最终皆是需要储存在硬盘之中的,硬盘的性能对于数据库性能有着决定性的影响.一直一来都听说更高的IOPS会显著增强数据库的战斗力,因此在这里拿出我的几块硬盘出来测试一下

> 事先声明以下数据仅供参考.请根据自己的实际情况做出选择

## 测试环境

- 系统: Ubuntu 24.04 noble
- CPU: Intel(R) Xeon(R) CPU E5-2683 v3 @ 2.00GHz
- 内存: 192GB REG ECC DDR4 2133MHz
- Docker version 26.0.1, build d260a54
- MySql 8 latest official image

> 据我所知,在docker中测试磁盘性能大概会有10%左右的损失,但是至少结果是公平的.可以体现出不同参赛选手的实际水平

## 参赛选手 `4K iops`

- SAS 希捷单盘 `0.6K IOPS`
- LSI3008 希捷 sata x4 raid0 `0.9K IOPS`
- zfs 西数 sata x5 raid0 `1.2 IOPS`
- sata 杂牌固态 `27K IOPS`
- nvme 傲腾内存 `222K IOPS`

## 测试方法

同一个数据库分别拷贝到不同的硬盘上,然后进行相同的测试

数据库结构如下

```sql
SET NAMES utf8mb4;
SET FOREIGN_KEY_CHECKS = 0;

-- ----------------------------
-- Table structure for logs
-- ----------------------------
DROP TABLE IF EXISTS `logs`;
CREATE TABLE `logs`  (
  `id` int NOT NULL AUTO_INCREMENT,
  `ip` int UNSIGNED NOT NULL COMMENT ' ',
  `user_agent` text CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NULL,
  `user` varchar(40) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NULL DEFAULT NULL,
  `time` bigint NOT NULL,
  `method` enum('GET','POST','PUT','DELETE','PATCH','OPTIONS','HEAD') CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `uri` text CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NULL,
  `version` enum('HTTP/1.0','HTTP/1.1','HTTP/2.0','HTTP/3.0') CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `status_code` smallint UNSIGNED NOT NULL,
  `length` int UNSIGNED NOT NULL,
  `referer` text CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NULL,
  PRIMARY KEY (`id`) USING BTREE
) ENGINE = InnoDB AUTO_INCREMENT = 5 CHARACTER SET = utf8mb4 COLLATE = utf8mb4_bin ROW_FORMAT = DYNAMIC;

SET FOREIGN_KEY_CHECKS = 1;

```
 
使用 navicat 数据生成器生成了 1000w 条数据,然后进行了以下测试,生成过程参考[此文档](https://navicat.com/en/company/aboutus/blog/1821-generating-test-data-in-navicat-16)

测试

## 比赛结果


## 赛后点评

## 加急任务

todo