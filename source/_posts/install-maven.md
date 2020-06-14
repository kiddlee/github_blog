---
layout: post
title: "Install Maven On Mac"
date:   2016-07-24
description: Install Maven On Mac
categories: Java
tags:
- maven
- java
---

## Installation
* Download [maven](http://maven.apache.org)
* Ensure JAVA_HOME environment variable is set and points to your JDK installation
* Extract distribution archive in any directory, like /opt
* Check environment variable value $JAVA_HOME
* Adding to PATH
```
export PATH=/opt/apache-maven/bin:$PATH
```
* Confirm with 
```
mvn -v 
```
to make sure maven work well.

## Build
```
mvn package
``` 