---
title: 解决Spring boot项目quartz的job没法使用注解方式实例化对象
date: 2017-10-26 16:19:45
tags: [Java,Spring boot]
categories: [Java,Spring boot]
---

使用自定义Job Factory，用于Spring注入

<!--more-->

``` java
@Component
public class CustomJobFactory extends AdaptableJobFactory {
  @Autowired
  private AutowireCapableBeanFactory capableBeanFactory;

  @Override
  protected Object createJobInstance(TriggerFiredBundle bundle) throws Exception {
    // 调用父类的方法
    Object jobInstance = super.createJobInstance(bundle);
    // 进行注入
    capableBeanFactory.autowireBean(jobInstance);
    return jobInstance;
  }
}

@Configuration
public class QuartzConfig {

  ...

  @Bean
  public SchedulerFactoryBean schedulerFactoryBean() throws IOException {
    schedulerFactory = new SchedulerFactoryBean();

    schedulerFactory.setOverwriteExistingJobs(true);

    // 延时启动
    schedulerFactory.setStartupDelay(20);

    // 加载quartz数据源配置
    schedulerFactory.setQuartzProperties(quartzProperties());

    // 自定义Job Factory，用于Spring注入
    schedulerFactory.setJobFactory(customJobFactory);

    return schedulerFactory;
  }

}

```