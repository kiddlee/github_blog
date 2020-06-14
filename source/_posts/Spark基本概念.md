---
layout: post
title: "Spark基本概念"
date:   2016-11-23
description: Spark基本概念
categories: Spark
tags: spark
---

Spark是一个用于集群计算的通用计算框架，数据科学应用和数据处理。
Spark项目包含多个紧密集成的组建。Spark的核心是一个对由很多计算任务组成的、运行在多个工作机器或者是一个计算集群上的应用进行调度、分发以及监控的**计算引擎**

### spark-core
实现了Spark的基本功能，包括任务调度，内存管理，错误恢复，存储系统交互以及对弹性分布式数据集(RDD)的API定义

### spark-sql
是Spark用来操作结构化数据的程序包

### spark-streaming 实时计算 
是Spark对实时数据进行流式计算的组件

### MLlib
Spark中的机器学习（ML）功能的程序库

### GraphX
操作图（如社交网络的朋友关系图）的程序库

### 集群管理器
Spark支持在各种**集群管理器(cluster manager)**上运行，包括Hadoop YARN、Apache Mesos，以及Spark自带的一个简易调度器

### RDD 弹性分布式数据集 Resillient Distributed Dataset

通过对分布式数据集的操作来表达我们的计算意图，这些计算会自动的在集群上并行进行。RDD是Spark对分布数据和计算的基本抽象