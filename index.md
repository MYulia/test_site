---
layout: page
title: My experience with Spark
description: Testing how this works.
---

## What is Spark?

Spark is a framework. You can use it with Scala, Java, Python and R to work on large datasets on clusters.

## How to start?

If you don't want to install everything, you can use docker, whitch has everything you need.

To set up docker use [docker documentation](https://docs.docker.com/engine/installation/)

To test if docker is running use in terminal:
```
docker run hello-world
```

To set up Spark notebook:
```
docker pull andypetrella/spark-notebook:0.6.2-scala-2.11.7-spark-1.6.0-hadoop-2.7.1-with-hive-with-parquet
```

```
docker run -p 9000:9000 -p 4040-4045:4040-4045 andypetrella/spark-notebook:0.6.2-scala-2.11.7-spark-1.6.0-hadoop-2.7.1-with-hive-with-parquet
```

## First look at Spark and Scala

To understand a little bit how Spark works, we will use the next material, that should be copied in a directory:
```
wget http://rubigdata.github.io/course/assignments/BigData-big-data-spark-101.snb
``` 

## Second look at Spark

```
wget http://rubigdata.github.io/course/assignments/BigData-big-data-execution-model.snb
```
