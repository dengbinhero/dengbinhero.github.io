---
layout: post
title: 微博客户端发版机制
date: 2017-07-13 10:36:37.000000000 +09:00
tags: iOS
---

### 概要
目前微博团队使用的是<strong>隔周</strong>发版机制，即：<strong>每两周发一个版本</strong>，保证每月至少保证迭代两个版本。每个迭代会经历alpa1、alpha2、release三个阶段来保证代码质量。
角色扮演：
PM：负责推动整个需求进程，把控各个关键时间节点，build阶段质量验收，推动提测进程，监督需求完成质量，直到上线，具有一定project manager的
RD：需求开发、bugfix，听PM的，听测试的。
QA：保证build阶段、alpha1、alpha2、alpha3阶段代码质量，保证需求进版质量。RD开发后的功能最终是否能进版QA具有决定权（通常是质量达不到要求被QA拒绝进版）

### 发版流程图
![](/assets/images/2017/release_1.png)
*  微博团队采用Git管理代码，开发都沿着dev分之进行
*  几个时间点：<strong>单周三</strong>、<strong>双周二</strong>、<strong>双周三</strong>
*  涉及分支：RD各自的<strong>feature</strong>分支、<strong>dev</strong>、<strong>release</strong>
*  1：RD从dev拉出分支如图<strong>feature1</strong>，进行开发，开发完毕，将feature1分支的build包交付给测试团队进行测试，直到bugfix完毕，测试通过，最终确保将feature1代码在<strong>单周三</strong>之前merge到<strong>dev</strong>。
*  2：单周三下午，从<strong>dev</strong>拉出这次要发版的<strong>release</strong>分支，在<strong>release</strong>分支打包，交付给测试，进入alpha1阶段。（alpha1阶段主要是做bugfix，测试不停的报bug，然后RD不停的fix），这个alpha阶段都围绕<strong>release</strong>分支进行
*  3:<strong>alpha1</strong>阶段持续到双周二下午，等alpha1bugfix完毕，build出alpha2的包交付给测试，
*  测试团队通过<strong>alpha2</strong>的包回归测试alpha1提出的bug
*  4:<strong>alpha2</strong>阶段有一天时间，持续到第二天下午，打出release包，RD需要在这个时间点前fix掉<strong>alpha2</strong>阶段发现的bug
*  5:<strong>release</strong>包交付给测试，回归alpha2阶段的bug，简单的回归功能点，最终测试通过，打最终的release包交付appstore
*  6:<strong>release</strong>分支merge至<strong>dev</strong>。周期完成


###  各阶段详解
#### 1.需求开发阶段（feature分支阶段）
![](/assets/images/2017/release_3.png)
功能开发阶段，即alpha1（拉出<strong>release</strong>分支）之前，RD可在任何时节点拉出自己的<strong>feature</strong>分支进行开发、打包、fix、打包，直到测试完成，方允许把<strong>feature</strong>分支合并至<strong>dev</strong>分支。

#### 2.集成测试阶段（release分支阶段）
![](/assets/images/2017/release_4.png)
<strong>release</strong>分支包含了本次发版的所有feature，有<strong>alpha1</strong>、<strong>alpha2</strong>、<strong>releas</strong>e三轮测试，所有RD均在<strong>release</strong>分支做bugfix即可。

### feature阶段流程图
![](/assets/images/2017/release_5.png)

### alpha阶段流程图
![](/assets/images/2017/release_6.png)
dev_xxx == release

### 写在最后
发版机制的几个优点：
*   build、alpha1、alpha2、release阶段四轮测试，保证质量
*   release分支一旦拉出，所有后续完成的feature不再允许合入release分支，保证了发版分之代码的质量



   
   