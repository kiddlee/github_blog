---
layout: post
title: "RDD编程"
date:   2016-11-23
description: RDD编程
categories: Spark
tags: spark
---

RDD(Resilient Distributed Dataset弹性分布式数据集)其实就是分布式的元素集合。用户可以使用两种方式创建RDD：读取一个外部数据集，或在驱动器程序里分发驱动器程序中的对象集合（list和set）。

```
//读取一个外部数据集
var lines = sc.textFile("/path/to/README.md")
//在驱动器程序里分发驱动器程序中的对象集合
var lines = sc.parallelize(List("pandas", "dogs"))
```

创建出来后，RDD支持两种类型的操作：转化操作（transformation）和行动操作（action）。转化操作会有一个RDD生成一个新的RDD。行动操作会对RDD计算出一个结果，并把结果返回到驱动器程序中，或者把结果存储到外部存储系统中（如HDFS）

### 常见的转化操作
**示例数据{1，2，3，3}**

- map

> 目的：将函数应用于RDD中的每个元素, 将返回值构成新的RDD<br />
> 示例：rdd.map(x=>x+1)<br />
> 结果：{2,3,4,4}

- flatMap

> 目的：将函数应用于RDD中的每个元素, 将返回的迭代器的所有内容构成新的RDD。通常用来切分单词<br />
> 示例：rdd.flatMap(x => x.to(3))<br />
> 结果：{1,2,3,2,3,3}

|函数名|目的|示例|结果|备注|
|---|---|---|---|---|
|map()|将函数应用于RDD中的每个元素, 将返回值构成新的RDD|rdd.map(x=>x+1)|{2,3,4,4}||
|flatMap()|将函数应用于RDD中的每个元素, 将返回的迭代器的所有内容构成新的RDD。通常用来切分单词|rdd.flatMap(x => x.to(3))|{1,2,3,2,3,3}||
|filter()|返回一个由通过传给filter()的函数的元素组成的RDD|rdd.filter(x => x!=1)|{2,3,3}||
|distinct()|去重|rdd.distinct()|{1,2,3}|开销很大，因为需要将所有数据通过网络进行混洗|
|sample(withReplacement, fraction, [seed])|对RDD采样，以及是否替换|rdd.sample(false, 0.5)|非确定||

**示例数据{1,2,3}{3,4,5}**

|函数名|目的|示例|结果|备注|
|---|---|---|---|---|
|union()|生成一个包含两个RDD中所有元素的RDD|rdd.union(other)|{1,2,3,3,4,5}||
|intersection()|求两个RDD共同元素的RDD|rdd.intersection(other)|{3}|性能差，需要网络混洗数据来发现共同元素|
|subtract()|移除一个RDD中的内容|rdd.subtract(other)|{1,2}|需要数据混洗|
|cartesian()|与另一个RDD的笛卡尔积|rdd.cartesian(other)|{ {1,3},{1,4},...,{3,5} }|求大规模RDD开销巨大|

### 常见的行为操作
**示例数据{1,2,3,3}**

|函数名|目的|示例|结果|备注|
|---|---|---|---|---|
|collect()|返回RDD中的所有元素|rdd.collect()|{1,2,3,3}||
|count()|RDD中的元素个数|rdd.count()|4||
|countByValue()|各元素在RDD中出现的次数|rdd.countByValue()|{(1,1),(2,1),(3,2)}||
|take(num)|从RDD中返回num个元素|rdd.take(2)|{1,2}||
|top(num)|从RDD中返回最前面的num个元素|rdd.top(2)|{3,3}||
|takeOrdered(num)(ordering)|从RDD中按照提供的顺序返回最前面的num个元素|rdd.takeOrdered(2)(myOrdering)|(3,3)||
|takeSample(withReplacement, num, [seed])|从RDD中返回任意一些元素|rdd.takeSample(false, 1)|||
|reduce(func)|并行整合RDD中所有数据(例如sum)|rdd.reduce((x,y)=>x+y)|9||
|fold(zero)(func)|和reduce一样，但需要提供初始值|rdd.fold(0)((x,y)=>x+y)|9||
|**aggregate(zeroValue)(seqOp, combOp)**|和reduce相似，但通常不返回同类型的函数|rdd.aggregate(0,0)((x,y)=>(x.\_1+y,x.\_2+1),(x,y)=>(x.\_1+y.\_1,x.\_2+y.\_2))|{9,4}||
|foreach(func)|对RDD中的每个元素使用给定的函数|rdd.foreach(func)|||

### 持久化
```
val result = input.map(x => x * x) 
result.persist(StorageLevel.DISK_ ONLY) 
println(result.count()) 
println(result.collect().mkString(","))
```
|级别|使用的空间|CPU时间|是否在内存中|是否在硬盘中|备注|
|---|---|---|---|---|---|
|MEMORY_ONLY|高|低|是|否||
|MEMORY_ONLY_SER|低|高|是|否||
|MEMORY_AND_DISK|高|中等|部分|部分|如果数据在内存中放不下，<br />则溢写到磁盘上|
|MEMORY_AND_DISK_SER|低|高|部分|部分|如果数据在内存中放不下，<br />则溢写到磁盘上。在内存中存放序列化后的数据|
|DISK_ONLY|低|高|否|是||	