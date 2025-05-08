---
title: Scraping Data
parent: Machine Learning Project
layout: default
nav_order: 1
---

# Scraping Data

Now, we are ready to begin our first step in training a machine learning model. The most essential component to any machine learning model is, obviously, the training data. We have to be able to tell the ML model which graphs are good and which graphs are bad for the model to be able to detect errors in real time.

## Location of Data

The broadband, strong motion, and geophone readings all exist within the server's `/ref/dc14/PDF/STATS` directory. Let's try navigating to the directory and running `ls`.

![image](/assets/scrape/ls.png)

As you may have read from the [background](./background.html), we have folders representing each seismic station under Berkeley Seismology Lab's supervision. Let's try navigating to the `BK.BKS.00` directory with `cd BK.BKS.00/`, which represents the BKS station located within the BK network with channel 00.

![image](/assets/scrape/cd.png)

Do any of these folders look familiar? Hopefully, you were able to notice that HH(E,N,Z) and HN(E,N,Z) correspond to the directional labels for broadband and strong motion sensors respectively (if you didn't, read the last part of the [background](./background.html) page again).

Let's try `cd HHE/` and dive into the East-West component of the `BK.BKS.00`'s broadband seismometer.

