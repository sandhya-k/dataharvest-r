The Grammar of Graphics: Designing and Transforming Data
========================================================
author: Sandhya Kambhampati 
date: June 4, 2016
font-family: 'Helvetica'

Follow along
========================================================
<center>
bit.ly/dataharvestggplot
</center>

What is R?
========================================================
<br>
"R is a language and environment for statistical computing and graphics" 

Source: R-project.org 

What is ggplot2?
========================================================
* *ggplot2* is a data visualization package for R
  + developed by Hadley Wickham
  + inspired by Leland Wilkinson's "The Grammar of Graphics"
  + provides an organizing philosophy for building graphs -- a structured approach to graphing
</br>

> "The emphasis in *ggplot2* is reducing the amount of thinking time by making it easier to go from the plot in your brain to the plot on the page."

> Wickham, 2012

The philosophy of ggplot2
========================================================
* A *ggplot2* graph is built up from a few basic elements:
  + **Data**: the raw data you want to plot
  + **Aesthetics**: including **Mapping** e.g., which variable is on the x-axis? the y-axis? Should the color/size/position of the plotted data that be mapped to some variable?
  + **Geometries**: the geometric shapes that represent the data
  + **Statistics**: statistical transformations that are used to summarize the data

Source: [Hopper (2014)] (http://tomhopper.me/2014/03/28/a-simple-introduction-to-the-graphing-philosophy-of-ggplot2/)

How to install ggplot2
========================================================
<br>

```r
install.packages('ggplot2')
library('ggplot2')
```

<br>
Make sure you have the most recent version of R to get the most recent version of *ggplot2*

The Data: Road Casualties in Great Britain 1969–84
========================================================

```r
data(Seatbelts)
s <- as.data.frame(Seatbelts)
```
Add in the time series data 
========================================================

```r
ts <- data.frame(Year=floor(time(Seatbelts)),
Month=factor(cycle(Seatbelts),
labels=month.abb), Seatbelts)
```
The Data: Road Casualties in Great Britain 1969–84
========================================================
<br>
* **DriversKilled**: car drivers killed
* **drivers**: monthly totals of car drivers in Great Britain killed or seriously injured Jan 1969 to Dec 1984
* **front**: front-seat passengers killed or seriously injured
* **rear**: rear-seat passengers killed or seriously injured
* **kms**: distance driven
* **PetrolPrice**: price of petrol
* **VanKilled**: number of van (‘light goods vehicle’) drivers
* **law**: 0/1: was the law in effect that month?
</br>
<br>
Source: UK Driver Deaths via [R datasets](https://stat.ethz.ch/R-manual/R-devel/library/datasets/html/UKDriverDeaths.html)

Look at your data
========================================================
```
head(ts)
```

How to plot your data: quick plot
========================================================




```r
qplot( data = ts,x= Year,y= DriversKilled, main= "Drivers Killed by Year")
```

<img src="ggplot2-figure/unnamed-chunk-5-1.png" title="plot of chunk unnamed-chunk-5" alt="plot of chunk unnamed-chunk-5" style="display: block; margin: auto;" />

Basic Features of ggplot2
========================================================
* Scatter Plot
* Bar Graph
* Line Graph

Scatter Plot
========================================================


```r
ggplot(data = ts, 
       aes(x = Year, 
           y = DriversKilled)) + 
  geom_point() +
  ggtitle("Drivers killed by Year")
```

Scatter Plot
========================================================
<img src="ggplot2-figure/unnamed-chunk-7-1.png" title="plot of chunk unnamed-chunk-7" alt="plot of chunk unnamed-chunk-7" style="display: block; margin: auto;" />

Notice something?
========================================================

```r
qplot( data = ts,
       x= Year,
       y= DriversKilled,
       main= "Drivers Killed by Year")
```


```r
ggplot(data = ts, 
       aes(x = Year, 
           y = DriversKilled)) + 
  geom_point() +
  ggtitle("Drivers killed by Year")
```

Bar Graph - simple
========================================================

```r
ggplot(data = ts, 
       aes(x = Year, 
           y = VanKilled)) +
  geom_bar(stat = 'identity')
```

Bar Graph - simple
========================================================
<img src="ggplot2-figure/unnamed-chunk-11-1.png" title="plot of chunk unnamed-chunk-11" alt="plot of chunk unnamed-chunk-11" style="display: block; margin: auto;" />

Line Graph
========================================================

```r
ggplot(data = ts, 
       aes(x = Year, 
           y = front)) +
  geom_point() +
  geom_line()
```

Line Graph
========================================================
<img src="ggplot2-figure/unnamed-chunk-13-1.png" title="plot of chunk unnamed-chunk-13" alt="plot of chunk unnamed-chunk-13" style="display: block; margin: auto;" />

Now, let's make the charts a little more easy to read 
========================================================

Scatter Plot - relabel y-axis
========================================================

```r
ggplot(data = ts, 
       aes(x = Year, 
           y = DriversKilled)) + 
  geom_point() +
  scale_y_continuous(limits = c(50,200))
```

Scatter Plot - relabel y-axis
========================================================
<img src="ggplot2-figure/unnamed-chunk-15-1.png" title="plot of chunk unnamed-chunk-15" alt="plot of chunk unnamed-chunk-15" style="display: block; margin: auto;" />

Scatter Plot - color mapped to month
========================================================

```r
ggplot(data = ts, 
       aes(x = Year, 
           y = DriversKilled, 
           color = Month)) + 
  geom_point() 
```

Scatter Plot - color mapped to month
========================================================
<img src="ggplot2-figure/unnamed-chunk-17-1.png" title="plot of chunk unnamed-chunk-17" alt="plot of chunk unnamed-chunk-17" height="600px" style="display: block; margin: auto;" />

Bar Graph - simple, transparent background
========================================================

```r
ggplot(data = ts, 
       aes(x = Year, 
           y = VanKilled)) +
  geom_bar(stat = 'identity') +
  theme(panel.background = element_blank())
```

Bar Graph - transparent background
========================================================
<img src="ggplot2-figure/unnamed-chunk-19-1.png" title="plot of chunk unnamed-chunk-19" alt="plot of chunk unnamed-chunk-19" style="display: block; margin: auto;" />
The philosophy of ggplot2 - recap
========================================================
* A *ggplot2* graph is built up from a few basic elements:
  + **Data**: the raw data you want to plot
  + **Aesthetics**: including **Mapping** e.g., which variable is on the x-axis? the y-axis? Should the color/size/position of the plotted data that be mapped to some variable?
  + **Geometries**: the geometric shapes that represent the data
  + **Statistics**: statistical transformations that are used to summarize the data

Source: [Hopper (2014)] (http://tomhopper.me/2014/03/28/a-simple-introduction-to-the-graphing-philosophy-of-ggplot2/)

Resources
======================================================
* ["A Layered Grammar of Graphics"](http://vita.had.co.nz/papers/layered-grammar.html) by Hadley Wickham

* ["A Simple Introduction to the Graphing Philosophy of ggplot2"](http://tomhopper.me/2014/03/28/a-simple-introduction-to-the-graphing-philosophy-of-ggplot2/) by Tom Hopper

* [ggplot2 Cheat Sheet](https://www.rstudio.com/wp-content/uploads/2015/03/ggplot2-cheatsheet.pdf) by RStudio

* [ggplot2 Documentation](http://docs.ggplot2.org/current/) by Hadley Wickham & Winston Chang

* [Resources for Doing Data Journalism](http://rddj.info/) by Timo Grossenbacher

* [Shapes and Line Types in R](http://www.cookbook-r.com/Graphs/Shapes_and_line_types/) by Winston Chang

Advanced Features
========================================================
* Text Labels
* Facetting
* Fitted Lines

Text Labels 
========================================================

```r
ggplot(data = ts, 
       aes(x = Month, 
           y = DriversKilled)) +
        geom_text(aes(label = Year)) 
```
Text Labels
========================================================
<img src="ggplot2-figure/unnamed-chunk-21-1.png" title="plot of chunk unnamed-chunk-21" alt="plot of chunk unnamed-chunk-21" style="display: block; margin: auto;" />
Facetting
========================================================

* Facetting allows you to split up your data by one or two variables
* *facet_grid()* places one or two variables in either vertical or horizontal directions
* *facet_wrap()* places facets next to each other, wrapping with a certain # of rows and/or columns

```
facet_grid(vertical ~ horizontal)

facet_wrap(~ variable, nrow = ___, ncol = ___)
```

Advanced Line Graph
========================================================

```r
ggplot(data = ts, 
       aes(x = Year, 
           y = DriversKilled)) + 
  geom_line() +
  facet_wrap(~ Month)
```

Advanced Line Graph
========================================================
<img src="ggplot2-figure/unnamed-chunk-23-1.png" title="plot of chunk unnamed-chunk-23" alt="plot of chunk unnamed-chunk-23" height="600px" style="display: block; margin: auto;" />

Fitted Lines
========================================================
* How do we draw a fitted line through these points?

<img src="ggplot2-figure/unnamed-chunk-24-1.png" title="plot of chunk unnamed-chunk-24" alt="plot of chunk unnamed-chunk-24" style="display: block; margin: auto;" />

Fitted Lines
========================================================

```r
ggplot(data = ts, 
       aes(x = Year, 
           y = DriversKilled)) + 
  geom_point() +
  stat_smooth(method = 'lm')
```

Fitted Lines
========================================================
<img src="ggplot2-figure/unnamed-chunk-26-1.png" title="plot of chunk unnamed-chunk-26" alt="plot of chunk unnamed-chunk-26" style="display: block; margin: auto;" />

Thank You + Questions
======================================================
<br>

<center>
http://bit.ly/dataharvestggplot
</center>

<center>
Sandhya Kambhampati    
[@sandhya__k](https://twitter.com/sandhya__k)

</center>
