# Dplython: Dplyr for Python

[![Build Status](https://travis-ci.org/dodger487/dplython.svg?branch=master)](https://travis-ci.org/dodger487/dplython)

Welcome to Dplython: Dplyr for Python.

Dplyr is a library for the language R designed to make data analysis fast and easy.
The philosophy of Dplyr is to constrain data manipulation to a few simple functions that correspond to the most common tasks.
This maps thinking closer to the process of writing code, helping you move closer to analyze data at the "speed of thought".

The goal of this project is to implement the functionality of the R package Dplyr on top of Python's pandas.

* Dplyr: [Click here](https://cran.rstudio.com/web/packages/dplyr/vignettes/introduction.html)
* Pandas: [Click here](http://pandas.pydata.org/pandas-docs/stable/10min.html)

This is version 0.0.7.
It's experimental and subject to change.

## Introductory Video
Here is a 20 minute video explaining dplython, given at PyGotham 2016.

[![PyGotham Dplython video](http://img.youtube.com/vi/4YAcwCe1mAE/0.jpg)](https://www.youtube.com/watch?v=4YAcwCe1mAE "PyGotham Dplython Video")

Click the awkward picture above to see the talk!
Note that sound doesn't start until about 1 minute in due to microphone issues.

## Installation
To install, use pip:
```
pip install dplython
```

To get the latest development version, you can clone this repo or use the command:
```
pip install git+https://github.com/dodger487/dplython.git
```

## Contributing
We welcome your feature requests, open issues, bug reports, and pull requests!
Please use GitHub's interface.
Also consider joining the [dplython mailing list](https://groups.google.com/forum/#!forum/dplython).

## Example usage
```python
import pandas
from dplython import (DplyFrame, X, diamonds, select, sift, sample_n,
    sample_frac, head, arrange, mutate, group_by, summarize, DelayFunction) 

# The example `diamonds` DataFrame is included in this package, but you can 
# cast a DataFrame to a DplyFrame in this simple way:
# diamonds = DplyFrame(pandas.read_csv('./diamonds.csv'))

# Select specific columns of the DataFrame using select, and 
#   get the first few using head
diamonds >> select(X.carat, X.cut, X.price) >> head(5)
"""
Out:
   carat        cut  price
0   0.23      Ideal    326
1   0.21    Premium    326
2   0.23       Good    327
3   0.29    Premium    334
4   0.31       Good    335
"""

# Filter out rows using sift
diamonds >> sift(X.carat > 4) >> select(X.carat, X.cut, X.depth, X.price)
"""
Out:
       carat      cut  depth  price
25998   4.01  Premium   61.0  15223
25999   4.01  Premium   62.5  15223
27130   4.13     Fair   64.8  17329
27415   5.01     Fair   65.5  18018
27630   4.50     Fair   65.8  18531
"""

# Sample with sample_n or sample_frac, sort with arrange
(diamonds >> 
  sample_n(10) >> 
  arrange(X.carat) >> 
  select(X.carat, X.cut, X.depth, X.price))
"""
Out:
       carat        cut  depth  price
37277   0.23  Very Good   61.5    484
17728   0.30  Very Good   58.8    614
33255   0.32      Ideal   61.1    825
38911   0.33      Ideal   61.6   1052
31491   0.34    Premium   60.3    765
37227   0.40    Premium   61.9    975
2578    0.81    Premium   60.8   3213
15888   1.01       Fair   64.6   6353
26594   1.74      Ideal   62.9  16316
25727   2.38    Premium   62.4  14648
"""

# You can: 
#   add columns with mutate (referencing other columns!)
#   group rows into dplyr-style groups with group_by
#   collapse rows into single rows using sumarize
(diamonds >> 
  mutate(carat_bin=X.carat.round()) >> 
  group_by(X.cut, X.carat_bin) >> 
  summarize(avg_price=X.price.mean()))
"""
Out:
       avg_price  carat_bin        cut
0     863.908535          0      Ideal
1    4213.864948          1      Ideal
2   12838.984078          2      Ideal
...
27  13466.823529          3       Fair
28  15842.666667          4       Fair
29  18018.000000          5       Fair
"""

# If you have column names that don't work as attributes, you can use an 
# alternate "get item" notation with X.
diamonds["column w/ spaces"] = range(len(diamonds))
diamonds >> select(X["column w/ spaces"]) >> head()
"""
Out:
   column w/ spaces
0                 0
1                 1
2                 2
3                 3
4                 4
5                 5
6                 6
7                 7
8                 8
9                 9
"""

# It's possible to pass the entire dataframe using X._ 
diamonds >> sample_n(6) >> select(X.carat, X.price) >> X._.T
"""
Out:
         18966    19729   9445   49951    3087    33128
carat     1.16     1.52     0.9    0.3     0.74    0.31
price  7803.00  8299.00  4593.0  540.0  3315.00  816.00
"""

# To pass the DataFrame or columns into functions, apply @DelayFunction
@DelayFunction
def PairwiseGreater(series1, series2):
  index = series1.index
  newSeries = pandas.Series([max(s1, s2) for s1, s2 in zip(series1, series2)])
  newSeries.index = index
  return newSeries

diamonds >> PairwiseGreater(X.x, X.y)


# Passing entire dataframe and plotting with ggplot
from ggplot import ggplot, aes, geom_point, facet_wrap
ggplot = DelayFunction(ggplot)  # Simple installation
(diamonds >> ggplot(aes(x="carat", y="price", color="cut"), data=X._) + 
  geom_point() + facet_wrap("color"))
```
![Ggplot example 1](http://dodger487.github.com/figs/dplython/ggplot_img1.png)

```python
(diamonds >>
  sift((X.clarity == "I1") | (X.clarity == "IF")) >> 
  ggplot(aes(x="carat", y="price", color="color"), X._) + 
    geom_point() + 
    facet_wrap("clarity"))
```
![Ggplot example 2](http://dodger487.github.com/figs/dplython/ggplot_img2.png)

```python
# Matplotlib works as well!
import pylab as pl
pl.scatter = DelayFunction(pl.scatter)
diamonds >> sample_frac(0.1) >> pl.scatter(X.carat, X.price)
```
![MPL example 2](http://dodger487.github.com/figs/dplython/plt_img1.png)


This is very new and I'm matching changes.
Let me know if you'd like to see a feature or think there's a better way I can do something.

## Other approaches
* [pandas-ply](http://pythonhosted.org/pandas-ply/)

Development of dplython began before I knew pandas-ply existed.
After I found it, I chose "X" as the manager to be consistent.
Pandas-ply is a great approach and worth taking a look.
The main contrasts between the two are that:
* dplython uses dplyr-style groups, as opposed to the SQL-style groups of pandas and pandas-ply
* dplython maps a little more directly onto dplyr, for example having mutate instead of an expanded select.
* Use of operators to connect operations instead of method-chaining
