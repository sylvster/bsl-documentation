---
title: DBSCAN
parent: Machine Learning Project
layout: default
nav_order: 3
---

# DBSCAN

## The Algorithm

Now, here is the big question: How do we obtain the training data required to detect errors within our seismometer readings? For broadband alone, there are over 14,000 pieces of PDF files being created annually in the server (try `cd /ref/dc14/PDF/STATS` and check for yourself).

The current answer to that is [Scikit-Learn](https://scikit-learn.org/stable/)'s DBSCAN algorithm. DBSCAN is a [clustering algorithm](https://www.google.com/search?q=clustering+algorithm) that places an emphasis on clustering based on density. Based on the epsilon, or the given distance threshold parameter, DBSCAN will combine groups of data with close enough distances into one cluster.

![image](/assets/dbscan.jpg)

In other words, we will be treating each seismometer reading data as individual data points, just like the ones in the graph above. Then, we will define a custom distance metric that will allow us to tell which graphs are similar (and thus, close together in distance), and which ones are not so similar (and therefore further apart).

![image](/assets/distance_metric.png)

For now, we simply use the absolute difference between matrices to get our distance metric.

![image](/assets/math_one.png)
![image](/assets/math_two.png)

where `a(i, j)` and `b(i, j)` refers to each individual points on the seismometer reading. Recall that the broadband sensor readings can be represented as a two-dimensional matrices of 122 by 151 values, holding a value between 0 and 1 at each point.

Although the current distance metric is by no means perfect, it gives a good approximation of how similar certain graphs are to each other. The sum of all `c(i, j)` will be huge if the graphs are completely different, and very small if they are overlapping in many places.

## Implementing DBSCAN

Here are some recommended links to solidify the concepts of DBSCAN before actually looking at the implementation:

- [YouTube video explaining DBSCAN](https://www.youtube.com/watch?v=RDZUdRSDOok)
- [DBSCAN Docs](https://scikit-learn.org/stable/modules/generated/sklearn.cluster.DBSCAN.html)

Please note that we are running DBSCAN with our own custom distance metric, so our implementation will look slightly different from any examples on the internet. Don't worry if it takes a bit of time to get a conceptual grasp of what is happening in our DBSCAN implementation.

TODO: write documentation on scraping data

If you are coming from TODO, by this point you should have a folder containing all the scraped data from `/ref/dc14/PDF/STATS` neatly organized under one directory, like this:

![image](/assets/dbscan_files.png)

Now, we will be running DBSCAN on this folder, looking through one thousand files at a time. Please refer to the [git repository](https://github.com/sylvster/BSL-DBSCAN) for this project and follow along.

There are a lot of minor technical details within this DBSCAN file that can be left for one's own time. This tutorial will only cover the variables that might need to be modified to run a successful DBSCAN across tens of thousands of files.

![image](/assets/dbscan_git1.png)

First, we define `data_dir` and `output_dir`. `data_dir` refers to the data directory, where all the seismometer sensor readings currently exist. This is equivalent to the `broadband_data` folder in the image above this one. `output_dir` is where the output of the DBSCAN will go. Create a new directory for this variable. By the end of DBSCAN, all the files from `data_dir` will be transferred into `output_dir` in an organized way.

![image](/assets/dbscan_git2.png)

A `batch_num` (batch number) refers to the current batch we are on. Each batch refers to the 1000 data points passed into DBSCAN, and separated into groups. You must update this `batch_num` every time we run a DBSCAN, starting from 1, then 2, then 3, and so forth. Batch 1 will contain the first 1000 data from `data_dir`, batch 2 will contain the second 1000 data, and so forth. Don't worry about updating `starting_index` ever, but `num_data` can be changed if we are at the last batch and there is less than 1000 data left.

![image](/assets/dbscan_git3.png)

Lastly, the `eps` parameter stands for the epsilon value, which determines the threshold for two data points to be considered in one group. 
- Low epsilon: Only extremely close readings will be put into one group, resulting in a higher number of groups.
- High epsilon: DBSCAN will be lenient and put readings that are further apart into the same group, resulting in a lower number of groups.

So far, 23 is tested to be a good number to run a DBSCAN on broadband, strong motion, and geophone data.

This is an example of what a single batch looks like, after running every single cell inside DBSCAN.

![image](/assets/dbscan_git4.png)

As you can see, similar graphs have been put into one cluster. The outlier group, -1, shows graphs that do not belong in any particular cluster.

This example should make it obvious that DBSCAN allows us to very quickly extract general trends of seismometer readings. In this example, it's clear that group 1, as well as some from group -1, contain problematic graphs. We can extract those to put into our machine learning model labeled as "incorrect" data.

TODO: Write about after DBSCAN