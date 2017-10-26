---
title: 解决spring boot项目多个类implements于同一个接口类，使用注解需要多个@Qualifier
date: 2017-10-26 16:27:30
tags: [Java,Spring boot]
categories: [Java,Spring boot]
---
```java
  @Autowired
  private List<Itest> testList;
```
再通过遍历testList寻找相应的实例