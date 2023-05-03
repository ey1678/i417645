# Polars for Python

Pandas is one of the most popular tools used by data scientists today for data manipulation in Python based pipelines. Pandas Dataframes are easy to use, very flexible, and easy to integrate into other libraries due to its popularity. However, there are a few major drawbacks to Pandas that limits its use in real world production problems:
* Speed: Pandas is single threaded. There have been other solutions that attempt to add parallelization by building on top of Pandas (ie [Dask](https://www.dask.org/), but these solutions are limited because they do not rebuild the library from the ground up. 
* Scalability: Beyond just the issues with speed, Pandas does not scale to larger problems as it must hold everything in memory. This problem is exacerbated because it uses eager execution (more on this later).
