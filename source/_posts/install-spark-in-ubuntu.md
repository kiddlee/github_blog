---
layout: post
title: "Install Spark In Ubuntu"
date:   2016-06-18
description: Install Spark In Ubuntu
categories: Spark
tags: spark
---

## Installation
You need three things to run spark in Ubuntu. Java Scala & Spark. So download them as follow:

* [JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
* [Scala](http://www.scala-lang.org/)
* [Spark](http://spark.apache.org/downloads.html)

**NOTICE:** Spark has 2 types, spark & spark-hadoop, if you need spark-stream, download spark-hadoop.

After you get those tgz files, release them under folder /opt. Then edit /etc/profile as follow:

```
#JDK environment variable
export JAVA_HOME=/opt/jdk
export JRE_HOME=${JAVA_HOME}/jre
export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
export PATH=${JAVA_HOME}/bin:${JRE_HOME}/bin:$PATH

#Scala environment variable
export SCALA_HOME=/opt/scala
export PATH=${SCALA_HOME}/bin:$PATH

#Spark  environment variable
export SPARK_HOME=/opt/spark-hadoop/

#PythonPath Add pySpark from Spark to Python
export PYTHONPATH=/opt/spark-hadoop/python
```

**NOTICE:** If you install java before, just make sure JAVA_HOME JRE_HOME CLASSPATH PATH be configurated correct.

Then restart computer to make configuration work forever or run command 
```
source /etc/profile
```
to make it work temporary.
## Test
Switch to /opt/spark-hadoop in terminal. Run 
```
./bin/spark-shell
```
, then you will get spark lauch information and scala command.
