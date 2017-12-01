---
title: springmvc出现事务注解无效
date: 2017-12-01 09:58:03
tags: [Java,Spring mvc]
categories: [Java,Spring mvc]
---

旧项目使用的是spring+mvc,通过的是xml来配置。
期间出现了一个问题，事务注解无效.
通过排查发现<context:component-scan 重复扫描了两次。
还是新项目使用spring boot注入方式比较清晰。