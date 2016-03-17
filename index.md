---
layout: page
title: My experience with Spark
description: Testing how this works.
---

### What is Spark?

Spark is a framework. You can use it with Scala, Java, Python and R to work on large datasets on clusters.

### How to start?

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

### First look at Spark and Scala

To understand a little bit how Spark works, we will use the next material, that should be copied in a directory:

```
wget http://rubigdata.github.io/course/assignments/BigData-big-data-spark-101.snb
``` 

You can execute the comands with Shift+Enter.

Let's first make an rdd using a SparkContext(sc) with two parameters, first is a collection of elements from 0 to 999, the second one represents the number of partitions:

```scala
val rdd = sc.parallelize(0 to 999,8)
```

How can you add all the numbers that you have in your collenction?

```scala
rdd.reduce(_ + _)
```

But because rdds are lazy, they will calculate something only when an action is fired, like:

```scala
val sample = rdd.takeSample(false, 4)
```

Next, I will present the other way that you can create a rdd which is referencing a dataset in an external data system:

```scala
val lines = sc.textFile("notebooks/d100.txt.utf-8")
```

Now you have the all the lines from the text, as strings.
You can count the lines, it will also show you the result, count being an action:

```scala
println( "Lines:\t", lines.count)
```

or count the lines:

```scala
println( "Chars:\t", lines.map(s => s.length).reduce((a, b) => a + b))
```

Can you say what happens when you run:

```scala
lines.map(s => s.length)
```

Does something happen? Not really, because map is a transformation and not an action, and because it is lazy, it doesn't do anything, but it will transform the strings into the strings length at the right time.

or count the words:

```scala
val words = lines.flatMap(line => line.split(" ")).filter(_ != "").map(word => (word,1))
```

words is a special type of rdds consisting of pairs with a string and number 1.
To count all the words you can apply reduceByKey:

```scala
val wc = words.reduceByKey(_ + _)
```

it will take all the pairs, and add the values for the same keys.

To see the top ten most used words, you need to order the tuples by the value, in reverse(descending):

```scala
val top10 = wc.takeOrdered(10)(Ordering[Int].reverse.on(x=>x._2))
```

The data can be filtered by key or value:

```scala
wc.filter(_._1 == "Julia").collect
wc.filter(_._2 == 12).collect
```

For [more on Spark see this](https://spark.apache.org/docs/latest/programming-guide.html)



## Second look at Spark

```
wget http://rubigdata.github.io/course/assignments/BigData-big-data-execution-model.snb
```






For [more on Spark see this](https://spark.apache.org/docs/latest/programming-guide.html)