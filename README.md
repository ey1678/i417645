# Polars for Python

## Problems with Current Data Pipelines
Pandas is one of the most popular tools used by data scientists today for data manipulation in Python based pipelines. Pandas Dataframes are easy to use, very flexible, and easy to integrate into other libraries due to its popularity. However, there are a few major drawbacks to Pandas that limits its use in real world production problems:
* Speed: Pandas is single threaded. There have been other solutions that attempt to add parallelization by building on top of Pandas (ie [Dask](https://www.dask.org/)), but these solutions are limited because they do not rebuild the library from the ground up. 
* Scalability: Beyond just the issues with speed, Pandas does not scale to larger problems as it must hold everything in memory. This problem is exacerbated because it uses eager execution (more on this later).

To overcome these issues, many people use big data solutions like [PySpark](https://spark.apache.org/docs/latest/api/python/#). But these have their own issues as they are often cumbersome to set up, incur additional overhead due for distributed backends, and are still relatively slow. 

The primary issue is the lack of solutions that offer a good mix of high performance, scalability for larger datasets for non-distributed workloads, and ease of use. In [these](https://h2oai.github.io/db-benchmark/) results for a benchmark of database-like operations, we see several trends. Most solutions, several of which we have discussed above, are either too slow or do not scale well to larger datasets, or both. One of the few exceptions is Polars.

## What is Polars?

[Polars](https://www.pola.rs/) is a Dataframe interface built in Rust for high performance using the Apache Arrow memory model for speed and efficiency. For Python and Pandas users, it also offers a Python API that is lightweight and easy to use. It is built from the ground up for optimized multi-threaded Dataframe operations for significant improvements in speed over Pandas. It also features:
* Lazy/Eager Execution: Polars offers an API for both eager and lazy execution. Eager execution is like Pandas where commands are executed immediately upon being called with immediate results. Lazy execution is similar to Spark, where commands are queued but not run until a command to return results is called. Lazy execution allows for under-the-hood optimizations that can lead to large improvements in both speed and memory usage, especially for long chains of commands that are commonly used in data piplines. Remember the prior point about Pandas not scaling to more than memory data and eager execution? This is why that is a problem. Imagine loading a large dataset but a significant portion of the data can be filtered immediately. With Pandas, the entire dataset must first be loaded into memory before any filtering operations can take place. With Polars Lazy API, loading the dataset can be optimized to only load the data that passes the filter criteria.
* Stream querying: When using Polars Lazy, it also allows for queries to be processed in a streaming fashion. This allows for queries to be executed over chunks 
