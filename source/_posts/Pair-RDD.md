---
layout: post
title: Pair RDD
date: 2020-06-15 08:10:46
description: Pair RDD基本操作
categories: Spark
tags: spark
---

### 转化操作
**{% raw %}示例数据{{1,2},{3,4},{3,6}}{% endraw %}**

|函数名|目的|示例|结果|
|---|---|---|---|
|reduceByKey(func)|合并具有相同键的值|rdd.reduceByKey((x,y)=>x+y)|{% raw %}{{1,2},{3,10}}{% endraw %}|
|groupByKey()|对具有相同键的值进行分组|rdd.groupByKey()|{(1,[2]),(3,[4,6])}|
|combineByKey(createCombiner,mergeValue,mergeCombiners,partitioner)|使用不同的返回类型合并具有相同键的值|
|mapValues(func)|对pairRDD中的每个值应用一个函数而不改变键|rdd.mapValues(x=>x+1)|{(1,3),(3,5),(3,7)}|
|flatMapValues(func)|对pairRDD中的每个值应用一个返回迭代器的函数，然后对返回的每个元素都生成一个对应原键的键值对记录。通常用于符号化|rdd.flatMapValues(x=>(xto5))|{(1,2),(1,3),(1,4),(1,5),(3,4),(3,5)}|
|keys()|返回一个仅包含键的RDD|rdd.keys(){1,3,3}|
|values()|返回一个仅包含值的RDD|rdd.values(){2,4,6}|
|sortByKey()|返回一个根据键排序的RDD|rdd.sortByKey()|{(1,2),(3,4),(3,6)}|

**{% raw %}针对两个pairRDD的转化操作（rdd={(1,2),(3,4),(3,6)}other={(3,9)}）{% endraw %}**


|函数名|目的|示例|结果|
|---|---|---|---|
|subtractByKey|删掉RDD中键与otherRDD中的键相同的元素|rdd.subtractByKey(other)|{(1,2)}|
|join|对两个RDD进行内连接|rdd.join(other)|{(3,(4,9)),(3,(6,9))}|
|rightOuterJoin|对两个RDD进行连接操作，确保第一个RDD的键必须存在（右外连接）|rdd.rightOuterJoin(other){(3,(Some(4),9)),(3,(Some(6),9))}|
|leftOuterJoin|对两个RDD进行连接操作，确保第二个RDD的键必须存在（左外连接）|rdd.leftOuterJoin(other){(1,(2,None)),(3,(4,Some(9))),(3,(6,Some(9)))}|
|cogroup|将两个RDD中拥有相同键的数据分组到一起|rdd.cogroup(other)|{(1,([2],[])),(3,([4,6],[9]))}|

## 行为操作

**{% raw %}示例数据{(1,2),(3,4),(3,6)}{% endraw %}**

|函数名|目的|示例|结果|
|---|---|---|---|
|countByKey()|对每个键对应的元素分别计数|rdd.countByKey()|{(1,1),(3,2)}|
|collectAsMap()|将结果以映射表的形式返回，以便查询|rdd.collectAsMap()|Map{(1,2),(3,4),(3,6)}|
|lookup(key)|返回给定键对应的所有值|rdd.lookup(3)|[4,6]|