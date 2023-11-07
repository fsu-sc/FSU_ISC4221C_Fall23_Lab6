# FSU_ISC4221C_Fall23_Lab6  K-Means Clustering

## Goals

### Part I - Clustering Data Sets using K-Means

The first goal of this lab is to write a function that performs K-Means clustering of a finite set of records. Input to your function should include:

- The number of clusters
- The initial centers/generators
- The data to be clustered (a matrix with each row being a record)
- Tolerance for convergence
- Maximum number of iterations (default to 100)

The code should output the total cluster variance after convergence is reached (or max iterations)
 plus information for plotting the clusters (clusters centers); the code should output 
 whether or not convergence was obtained. 
For each problem, your *calling or main* routine for the function should generate several 
initial choices for centers and choose the result which produces the smallest cluster variance. 
In the first exercise, you will try out your code on different data sets.

Sometimes when you have data that you want to cluster, you don't know how many clusters to use. In theory, 
the more clusters we add, the smaller the cluster variance should become. Often however, if we have 
data which naturally fits into say five clusters, then when we use more than five clusters our total 
cluster variance will probably not decrease significantly after five clusters. So one way to decide 
the natural number of clusters is to run the algorithm for different numbers of clusters and plot 
the cluster variance as a function of the number of clusters. This is explored in Part #2.

In the next problem we want to look at using a different distance function in K-Means and apply it to classifying document data.

# Part 1

## Problem 1 (10 Pts) 
Write a code to implement the K-Means algorithm with the attributes described above using the standard Euclidean distance. As a convergence test use

$$\max_{1\leq i \leq k} |c_i^n - c_i^{n-1}|^2 \leq \text{tolerance}$$

where $n$ denotes the iteration number and $c_i$ are the $k$ centers of the clusters.

The data set `bank_notes.txt` contains 200 records containing information about properties of bank notes. 
There are 100 genuine notes and 100 forgeries. Cluster the data using your K-means algorithm (with two clusters) 
and compare with the actual clusters via a plot (actual data separated in files `bank_forge.txt`, 
`bank_genuine.txt`). For the plot use attributes #4 and #5. Use a tolerance of $10^{-2}$; be sure to run 
your code with several choices of the initial centers and choose the case which gives the lower 
cluster variance. When you are done, use the record given below to determine if it is a forgery.

```
214.9 130.2 130.3 9.2 9.8 140.1
```

## Problem 2 (10 Pts) 
The data `iris.txt` is a well-known data set for clustering; it includes four measurements (**sepal length, 
sepal width, petal length, and petal width**) based on the petals and sepals of different species 
of iris; there should be 150 records.

a. (5 pts)  Your first task is to use K-Means to cluster this data assuming we don't know a priori how 
many clusters to use. Let $k$ be the number of clusters. As your initial generators choose $k$ random 
records from the data file. Calculate the total cluster variance for each value of $k$. For each value
 of $k$ you should run several different choices of the initial generators (chosen randomly from the data) 
 and choose the one which has the smallest variance. Plot the total cluster variance versus 
 $k$ for $k = 1, 2, 3, 4, 5, 6$ and choose the value of $k$ which you believe is the natural
  number of clusters for this data; justify your answer.

b. (5 pts) Now you want to compare your clusters with the actual data. The data file `iris.txt` was created from data 
from three species of iris: *iris virginica*, *iris setosa*, and *iris versicolor*. Make plots of 
the **sepal width** vs **sepal length** and **petal width** vs **petal length** for the actual data; 
then do the same for your cluster data and discuss 
your results for your optimal choice of $k$ in part (a). Discuss whether you feel K-means 
was successful in determining the actual clusters; if not, why do you expect this to be the case.

## Problem 3 (10 Pts) 
In this exercise, we modify K-means to use a distance function other than the standard Euclidean length; specifically, we will use

$$d(u, v) = \sqrt{ \sum_{i=1}^{m} |u_i - v_i| }$$

where $u$ and $v$ are vectors in $ \mathbb{R}^m $. Use your new distance function in K-means to 
classify the document data in `documents.txt`.  In this example our goal is to classify document data. 
In this case the data consists of two types of text documents which involve (i) human-computer interaction and (ii) graphs. (Reference: Indexing by Latent Semantic Analysis, Deerwester et al.) There are 9 titles which need to be grouped. The number in the table indicates the frequency with which a term occurs in the abstract of each of 9 papers.

You can assume that the number of clusters is **two**. For 
your initial centers, choose **two different records randomly**. Use the **first two attributes** of the data 
for your distance calculation. Discuss your results.

| | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |  
|-|-|-|-|-|-|-|-|-|-|
|human|1|0|0|1|0|0|0|0|0|
|interface|1|0|1|0|0|0|0|0|0|
|computer|1|1|0|0|0|0|0|0|0|  
|user|0|1|1|0|1|0|0|0|0|
|system|0|1|1|2|0|0|0|0|0|
|response|0|1|0|0|1|0|0|0|0|
|time|0|1|0|0|1|0|0|0|0|
|EPS|0|0|1|1|0|0|0|0|0|
|survey|0|1|0|0|0|0|0|0|1|
|trees|0|0|0|0|0|1|1|1|0|
|graph|0|0|0|0|0|0|1|1|1|
|minors|0|0|0|0|0|0|0|1|1|

Use different initial guesses (from the data) to determine the clustering of the data which gives the smallest total cluster variance. As output give your results for five different choices of the initial clusters and give the optimal final clustering (i.e., for each record indicate which cluster it is in).