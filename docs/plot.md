---
title: PlotPDF
parent: Machine Learning Project
layout: default
nav_order: 2
---

# Plotting a Sensor Reading

Let's try plotting a sensor reading using Python! By now, Taka may have mentioned **broadband** and **strong motion** sensors to you.

![image](/assets/broadband_plot.png)

Let's analyze this broadband sensor plot from a programmer's perspective, ignoring the seismology background. The y-values for the plot represents Power, and ranges from values between -50 to -200, for a total of 151 points. The x-axis can be represented by the period. Notice that it displays a logarithmic trend, starting from somewhere around 10 ^ -2 going to around 10 ^ 2. Lastly, at each x and y pair, there is a small, colored cell that represents a probability value ranging from 0 to 0.30.

If any of the above description was unclear, this plot can basically be treated as a [heat map](https://www.atlassian.com/data/charts/heatmap-complete-guide) for our purposes.

We will be trying to plot a broadband sensor in this documentation. This is an <a href="/assets/broadband_example.pdf" download> example </a> of a broadband reading that can be plotted. Although it has a `.pdf` extension, note that PDF here stands for Power Density Function, and not the traditional Portable Document Format we use in every day life. The file should be opened raw on VSCode, without any pdf readers.

![image](/assets/broadband.png)

Now, you will see that the first column corresponds to the x-axis (raised to the power of 10) -- turns out, there are 121 values. The second column corresponds to the y-axis (ranging from -200 to -50), and the third column corresponding to the probability at that exact x and y. Using the `numpy` and `matplotlib` libraries, we can make a plot of this.

![image](/assets/broadband_code.png)

Try recreating the above in your own `.ipynb` file in your server! Don't forget to import the necessary libraries. Here are a few inputs to help understand `plotPDF`:
- Using `np.fromfile(filepath, sep=" ")` allows us to parse the PDF file into a one-dimensional array consisting of every element.
- We now reshape this one-dimensional array so that we can extract the x, y and z (probability) values by themselves. For purposes of creating a color mesh (feel free to skim over this detail; not too important), x and y has repeating values.
- Finally, we define the lower and upper range of x and y values in `ax.axis` and create a map of x and y to probability values.