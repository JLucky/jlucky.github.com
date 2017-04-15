---
layout: post
title: "Spark篇一 SparkSession创建与复用"
description: ""
category: 
tags: []
---
{% include JB/setup %}

第一篇我们来讲讲SparkSession

### 一、SparkSession的创建与获取

##### 1. 创建一个新的SparkSession
```
SparkSession.builder()
  .master("local")
  .appName("Word Count")
  .config("spark.some.config.option", "some-value")
  .getOrCreate()
```
##### 2. 获取一个已经创建的SparkSession
```
SparkSession.builder().getOrCreate()
```

### 二、应用

在实际的开发中，需要复用创建的SparkSession，这时我们可以创建一个SparkSession单例。

```
class JavaSparkSessionSingleton implements Serializable {
    private static transient SparkSession instance = null;

    public static SparkSession getInstance(SparkConf sparkConf) {
        if (instance == null) {
            instance = SparkSession.builder().config(sparkConf).getOrCreate();
        }

        return instance;
    }
}
```

这样，我们可以调用JavaSparkSessionSingleton.getInstance(conf)方法获取已经创建的SparkSession实例。

参考：

http://spark.apache.org/docs/latest/api/scala/index.html#org.apache.spark.sql.SparkSession