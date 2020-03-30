---
title: "R Basics 2 -Data-"
author: "Instructor: Yuta Toyama"
date: "Last updated: 2020-03-30"
output: 
  html_document:
    theme: lumen
    highlight: haddock 
    #code_folding: show
    toc: yes
    toc_depth: 2
    toc_float: true
    keep_md: true
    df_print: paged
  beamer_presentation:
    theme: "Madrid"
    colortheme: "lily"
    slide_level: 2
    includes:
      in_header: "../beamer_header.tex"
    df_print: tibble
---




# Data frame

## Acknowledgement

 This note is largely based on Applied Statistics with `R`. https://daviddalpiaz.github.io/appliedstats/


## Introduction 

- A **data frame** is the most common way that we store and interact with data in this course.


```r
example_data = data.frame(x = c(1, 3, 5, 7, 9, 1, 3, 5, 7, 9),
                          y = c(rep("Hello", 9), "Goodbye"),
                          z = rep(c(TRUE, FALSE), 5))
```

- A data frame is a **list** of vectors.
    - Each vector must contain the same data type
    - The difference vectors can store different data types.

---


```r
example_data
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["x"],"name":[1],"type":["dbl"],"align":["right"]},{"label":["y"],"name":[2],"type":["fctr"],"align":["left"]},{"label":["z"],"name":[3],"type":["lgl"],"align":["right"]}],"data":[{"1":"1","2":"Hello","3":"TRUE"},{"1":"3","2":"Hello","3":"FALSE"},{"1":"5","2":"Hello","3":"TRUE"},{"1":"7","2":"Hello","3":"FALSE"},{"1":"9","2":"Hello","3":"TRUE"},{"1":"1","2":"Hello","3":"FALSE"},{"1":"3","2":"Hello","3":"TRUE"},{"1":"5","2":"Hello","3":"FALSE"},{"1":"7","2":"Hello","3":"TRUE"},{"1":"9","2":"Goodbye","3":"FALSE"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

---

- `write.csv` save (or export) the dataframe in `.csv` format.



<!-- >
Unlike a list which has more flexibility, the elements of a data frame must all be vectors, and have the same length.


```r
example_data$x
```

```
##  [1] 1 3 5 7 9 1 3 5 7 9
```

```r
all.equal(length(example_data$x),
          length(example_data$y),
          length(example_data$z))
```

```
## [1] TRUE
```

```r
str(example_data)
```

```
## 'data.frame':	10 obs. of  3 variables:
##  $ x: num  1 3 5 7 9 1 3 5 7 9
##  $ y: Factor w/ 2 levels "Goodbye","Hello": 2 2 2 2 2 2 2 2 2 1
##  $ z: logi  TRUE FALSE TRUE FALSE TRUE FALSE ...
```

```r
nrow(example_data)
```

```
## [1] 10
```

```r
ncol(example_data)
```

```
## [1] 3
```

```r
dim(example_data)
```

```
## [1] 10  3
```
< --> 

## Load csv file

- We can also import data from various file types in into `R`, as well as use data stored in packages.
- Read `csv` file into R. 
    - `read.csv()` function as default
    - `read_csv()` function from the `readr` package. This is faster for larger data.


```r
# install.packages("readr") 
#library(readr)
#example_data_from_csv = read_csv("example-data.csv")
example_data_from_csv = read.csv("example-data.csv")
```


---

- Note: This particular line of code assumes that the file `example_data.csv` exists in your current working directory.
- The current working directory is the folder that you are working with. To see this, you type 

```r
getwd()
```

```
## [1] "C:/Users/Yuta/Dropbox/Teaching/2020_1_3_4_Applied_Metrics/Note_Github/02_RIntro"
```
- If you want to set the working directory, use `setwd()` function

```r
setwd(dir = "directory path" )
```

<!-- >


```r
example_data_from_csv
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["x"],"name":[1],"type":["int"],"align":["right"]},{"label":["y"],"name":[2],"type":["fctr"],"align":["left"]},{"label":["z"],"name":[3],"type":["lgl"],"align":["right"]}],"data":[{"1":"1","2":"Hello","3":"TRUE"},{"1":"3","2":"Hello","3":"FALSE"},{"1":"5","2":"Hello","3":"TRUE"},{"1":"7","2":"Hello","3":"FALSE"},{"1":"9","2":"Hello","3":"TRUE"},{"1":"1","2":"Hello","3":"FALSE"},{"1":"3","2":"Hello","3":"TRUE"},{"1":"5","2":"Hello","3":"FALSE"},{"1":"7","2":"Hello","3":"TRUE"},{"1":"9","2":"Goodbye","3":"FALSE"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

A tibble is simply a data frame that prints with sanity. Notice in the output above that we are given additional information such as dimension and variable type.

The `as_tibble()` function can be used to coerce a regular data frame to a tibble.


```r
library(tibble)
example_data = as_tibble(example_data)
example_data
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["x"],"name":[1],"type":["dbl"],"align":["right"]},{"label":["y"],"name":[2],"type":["fctr"],"align":["left"]},{"label":["z"],"name":[3],"type":["lgl"],"align":["right"]}],"data":[{"1":"1","2":"Hello","3":"TRUE"},{"1":"3","2":"Hello","3":"FALSE"},{"1":"5","2":"Hello","3":"TRUE"},{"1":"7","2":"Hello","3":"FALSE"},{"1":"9","2":"Hello","3":"TRUE"},{"1":"1","2":"Hello","3":"FALSE"},{"1":"3","2":"Hello","3":"TRUE"},{"1":"5","2":"Hello","3":"FALSE"},{"1":"7","2":"Hello","3":"TRUE"},{"1":"9","2":"Goodbye","3":"FALSE"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>
< -->

<!-- >
Alternatively, we could use the "Import Dataset" feature in RStudio which can be found in the environment window. 
(By default, the top-right pane of RStudio.)  
Once completed, this process will automatically generate the code to import a file. 
The resulting code will be shown in the console window. 
In recent versions of RStudio, `read_csv()` is used by default, thus reading in a tibble.
< -->

## Examine dataframe

- Inside the `ggplot2` package is a dataset called `mpg`. By loading the package using the `library()` function, we can now access `mpg`.


```r
library(ggplot2)
```

---

- Three things we would generally like to do with data:
    - Look at the raw data.
    - Understand the data. (Where did it come from? What are the variables? Etc.)
    - Visualize the data.
- To look at the data, we have two useful commands: `head()` and `str()`

```r
head(mpg, n = 10)
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["manufacturer"],"name":[1],"type":["chr"],"align":["left"]},{"label":["model"],"name":[2],"type":["chr"],"align":["left"]},{"label":["displ"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["year"],"name":[4],"type":["int"],"align":["right"]},{"label":["cyl"],"name":[5],"type":["int"],"align":["right"]},{"label":["trans"],"name":[6],"type":["chr"],"align":["left"]},{"label":["drv"],"name":[7],"type":["chr"],"align":["left"]},{"label":["cty"],"name":[8],"type":["int"],"align":["right"]},{"label":["hwy"],"name":[9],"type":["int"],"align":["right"]},{"label":["fl"],"name":[10],"type":["chr"],"align":["left"]},{"label":["class"],"name":[11],"type":["chr"],"align":["left"]}],"data":[{"1":"audi","2":"a4","3":"1.8","4":"1999","5":"4","6":"auto(l5)","7":"f","8":"18","9":"29","10":"p","11":"compact"},{"1":"audi","2":"a4","3":"1.8","4":"1999","5":"4","6":"manual(m5)","7":"f","8":"21","9":"29","10":"p","11":"compact"},{"1":"audi","2":"a4","3":"2.0","4":"2008","5":"4","6":"manual(m6)","7":"f","8":"20","9":"31","10":"p","11":"compact"},{"1":"audi","2":"a4","3":"2.0","4":"2008","5":"4","6":"auto(av)","7":"f","8":"21","9":"30","10":"p","11":"compact"},{"1":"audi","2":"a4","3":"2.8","4":"1999","5":"6","6":"auto(l5)","7":"f","8":"16","9":"26","10":"p","11":"compact"},{"1":"audi","2":"a4","3":"2.8","4":"1999","5":"6","6":"manual(m5)","7":"f","8":"18","9":"26","10":"p","11":"compact"},{"1":"audi","2":"a4","3":"3.1","4":"2008","5":"6","6":"auto(av)","7":"f","8":"18","9":"27","10":"p","11":"compact"},{"1":"audi","2":"a4 quattro","3":"1.8","4":"1999","5":"4","6":"manual(m5)","7":"4","8":"18","9":"26","10":"p","11":"compact"},{"1":"audi","2":"a4 quattro","3":"1.8","4":"1999","5":"4","6":"auto(l5)","7":"4","8":"16","9":"25","10":"p","11":"compact"},{"1":"audi","2":"a4 quattro","3":"2.0","4":"2008","5":"4","6":"manual(m6)","7":"4","8":"20","9":"28","10":"p","11":"compact"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>
<!-- >
The function `head()` will display the first `n` observations of the data frame. The `head()` function was more useful before tibbles. Notice that `mpg` is a tibble already, so the output from `head()` indicates there are only `10` observations. Note that this applies to `head(mpg, n = 10)` and not `mpg` itself. Also note that tibbles print a limited number of rows and columns by default. The last line of the printed output indicates which rows and columns were omitted.


```r
mpg
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["manufacturer"],"name":[1],"type":["chr"],"align":["left"]},{"label":["model"],"name":[2],"type":["chr"],"align":["left"]},{"label":["displ"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["year"],"name":[4],"type":["int"],"align":["right"]},{"label":["cyl"],"name":[5],"type":["int"],"align":["right"]},{"label":["trans"],"name":[6],"type":["chr"],"align":["left"]},{"label":["drv"],"name":[7],"type":["chr"],"align":["left"]},{"label":["cty"],"name":[8],"type":["int"],"align":["right"]},{"label":["hwy"],"name":[9],"type":["int"],"align":["right"]},{"label":["fl"],"name":[10],"type":["chr"],"align":["left"]},{"label":["class"],"name":[11],"type":["chr"],"align":["left"]}],"data":[{"1":"audi","2":"a4","3":"1.8","4":"1999","5":"4","6":"auto(l5)","7":"f","8":"18","9":"29","10":"p","11":"compact"},{"1":"audi","2":"a4","3":"1.8","4":"1999","5":"4","6":"manual(m5)","7":"f","8":"21","9":"29","10":"p","11":"compact"},{"1":"audi","2":"a4","3":"2.0","4":"2008","5":"4","6":"manual(m6)","7":"f","8":"20","9":"31","10":"p","11":"compact"},{"1":"audi","2":"a4","3":"2.0","4":"2008","5":"4","6":"auto(av)","7":"f","8":"21","9":"30","10":"p","11":"compact"},{"1":"audi","2":"a4","3":"2.8","4":"1999","5":"6","6":"auto(l5)","7":"f","8":"16","9":"26","10":"p","11":"compact"},{"1":"audi","2":"a4","3":"2.8","4":"1999","5":"6","6":"manual(m5)","7":"f","8":"18","9":"26","10":"p","11":"compact"},{"1":"audi","2":"a4","3":"3.1","4":"2008","5":"6","6":"auto(av)","7":"f","8":"18","9":"27","10":"p","11":"compact"},{"1":"audi","2":"a4 quattro","3":"1.8","4":"1999","5":"4","6":"manual(m5)","7":"4","8":"18","9":"26","10":"p","11":"compact"},{"1":"audi","2":"a4 quattro","3":"1.8","4":"1999","5":"4","6":"auto(l5)","7":"4","8":"16","9":"25","10":"p","11":"compact"},{"1":"audi","2":"a4 quattro","3":"2.0","4":"2008","5":"4","6":"manual(m6)","7":"4","8":"20","9":"28","10":"p","11":"compact"},{"1":"audi","2":"a4 quattro","3":"2.0","4":"2008","5":"4","6":"auto(s6)","7":"4","8":"19","9":"27","10":"p","11":"compact"},{"1":"audi","2":"a4 quattro","3":"2.8","4":"1999","5":"6","6":"auto(l5)","7":"4","8":"15","9":"25","10":"p","11":"compact"},{"1":"audi","2":"a4 quattro","3":"2.8","4":"1999","5":"6","6":"manual(m5)","7":"4","8":"17","9":"25","10":"p","11":"compact"},{"1":"audi","2":"a4 quattro","3":"3.1","4":"2008","5":"6","6":"auto(s6)","7":"4","8":"17","9":"25","10":"p","11":"compact"},{"1":"audi","2":"a4 quattro","3":"3.1","4":"2008","5":"6","6":"manual(m6)","7":"4","8":"15","9":"25","10":"p","11":"compact"},{"1":"audi","2":"a6 quattro","3":"2.8","4":"1999","5":"6","6":"auto(l5)","7":"4","8":"15","9":"24","10":"p","11":"midsize"},{"1":"audi","2":"a6 quattro","3":"3.1","4":"2008","5":"6","6":"auto(s6)","7":"4","8":"17","9":"25","10":"p","11":"midsize"},{"1":"audi","2":"a6 quattro","3":"4.2","4":"2008","5":"8","6":"auto(s6)","7":"4","8":"16","9":"23","10":"p","11":"midsize"},{"1":"chevrolet","2":"c1500 suburban 2wd","3":"5.3","4":"2008","5":"8","6":"auto(l4)","7":"r","8":"14","9":"20","10":"r","11":"suv"},{"1":"chevrolet","2":"c1500 suburban 2wd","3":"5.3","4":"2008","5":"8","6":"auto(l4)","7":"r","8":"11","9":"15","10":"e","11":"suv"},{"1":"chevrolet","2":"c1500 suburban 2wd","3":"5.3","4":"2008","5":"8","6":"auto(l4)","7":"r","8":"14","9":"20","10":"r","11":"suv"},{"1":"chevrolet","2":"c1500 suburban 2wd","3":"5.7","4":"1999","5":"8","6":"auto(l4)","7":"r","8":"13","9":"17","10":"r","11":"suv"},{"1":"chevrolet","2":"c1500 suburban 2wd","3":"6.0","4":"2008","5":"8","6":"auto(l4)","7":"r","8":"12","9":"17","10":"r","11":"suv"},{"1":"chevrolet","2":"corvette","3":"5.7","4":"1999","5":"8","6":"manual(m6)","7":"r","8":"16","9":"26","10":"p","11":"2seater"},{"1":"chevrolet","2":"corvette","3":"5.7","4":"1999","5":"8","6":"auto(l4)","7":"r","8":"15","9":"23","10":"p","11":"2seater"},{"1":"chevrolet","2":"corvette","3":"6.2","4":"2008","5":"8","6":"manual(m6)","7":"r","8":"16","9":"26","10":"p","11":"2seater"},{"1":"chevrolet","2":"corvette","3":"6.2","4":"2008","5":"8","6":"auto(s6)","7":"r","8":"15","9":"25","10":"p","11":"2seater"},{"1":"chevrolet","2":"corvette","3":"7.0","4":"2008","5":"8","6":"manual(m6)","7":"r","8":"15","9":"24","10":"p","11":"2seater"},{"1":"chevrolet","2":"k1500 tahoe 4wd","3":"5.3","4":"2008","5":"8","6":"auto(l4)","7":"4","8":"14","9":"19","10":"r","11":"suv"},{"1":"chevrolet","2":"k1500 tahoe 4wd","3":"5.3","4":"2008","5":"8","6":"auto(l4)","7":"4","8":"11","9":"14","10":"e","11":"suv"},{"1":"chevrolet","2":"k1500 tahoe 4wd","3":"5.7","4":"1999","5":"8","6":"auto(l4)","7":"4","8":"11","9":"15","10":"r","11":"suv"},{"1":"chevrolet","2":"k1500 tahoe 4wd","3":"6.5","4":"1999","5":"8","6":"auto(l4)","7":"4","8":"14","9":"17","10":"d","11":"suv"},{"1":"chevrolet","2":"malibu","3":"2.4","4":"1999","5":"4","6":"auto(l4)","7":"f","8":"19","9":"27","10":"r","11":"midsize"},{"1":"chevrolet","2":"malibu","3":"2.4","4":"2008","5":"4","6":"auto(l4)","7":"f","8":"22","9":"30","10":"r","11":"midsize"},{"1":"chevrolet","2":"malibu","3":"3.1","4":"1999","5":"6","6":"auto(l4)","7":"f","8":"18","9":"26","10":"r","11":"midsize"},{"1":"chevrolet","2":"malibu","3":"3.5","4":"2008","5":"6","6":"auto(l4)","7":"f","8":"18","9":"29","10":"r","11":"midsize"},{"1":"chevrolet","2":"malibu","3":"3.6","4":"2008","5":"6","6":"auto(s6)","7":"f","8":"17","9":"26","10":"r","11":"midsize"},{"1":"dodge","2":"caravan 2wd","3":"2.4","4":"1999","5":"4","6":"auto(l3)","7":"f","8":"18","9":"24","10":"r","11":"minivan"},{"1":"dodge","2":"caravan 2wd","3":"3.0","4":"1999","5":"6","6":"auto(l4)","7":"f","8":"17","9":"24","10":"r","11":"minivan"},{"1":"dodge","2":"caravan 2wd","3":"3.3","4":"1999","5":"6","6":"auto(l4)","7":"f","8":"16","9":"22","10":"r","11":"minivan"},{"1":"dodge","2":"caravan 2wd","3":"3.3","4":"1999","5":"6","6":"auto(l4)","7":"f","8":"16","9":"22","10":"r","11":"minivan"},{"1":"dodge","2":"caravan 2wd","3":"3.3","4":"2008","5":"6","6":"auto(l4)","7":"f","8":"17","9":"24","10":"r","11":"minivan"},{"1":"dodge","2":"caravan 2wd","3":"3.3","4":"2008","5":"6","6":"auto(l4)","7":"f","8":"17","9":"24","10":"r","11":"minivan"},{"1":"dodge","2":"caravan 2wd","3":"3.3","4":"2008","5":"6","6":"auto(l4)","7":"f","8":"11","9":"17","10":"e","11":"minivan"},{"1":"dodge","2":"caravan 2wd","3":"3.8","4":"1999","5":"6","6":"auto(l4)","7":"f","8":"15","9":"22","10":"r","11":"minivan"},{"1":"dodge","2":"caravan 2wd","3":"3.8","4":"1999","5":"6","6":"auto(l4)","7":"f","8":"15","9":"21","10":"r","11":"minivan"},{"1":"dodge","2":"caravan 2wd","3":"3.8","4":"2008","5":"6","6":"auto(l6)","7":"f","8":"16","9":"23","10":"r","11":"minivan"},{"1":"dodge","2":"caravan 2wd","3":"4.0","4":"2008","5":"6","6":"auto(l6)","7":"f","8":"16","9":"23","10":"r","11":"minivan"},{"1":"dodge","2":"dakota pickup 4wd","3":"3.7","4":"2008","5":"6","6":"manual(m6)","7":"4","8":"15","9":"19","10":"r","11":"pickup"},{"1":"dodge","2":"dakota pickup 4wd","3":"3.7","4":"2008","5":"6","6":"auto(l4)","7":"4","8":"14","9":"18","10":"r","11":"pickup"},{"1":"dodge","2":"dakota pickup 4wd","3":"3.9","4":"1999","5":"6","6":"auto(l4)","7":"4","8":"13","9":"17","10":"r","11":"pickup"},{"1":"dodge","2":"dakota pickup 4wd","3":"3.9","4":"1999","5":"6","6":"manual(m5)","7":"4","8":"14","9":"17","10":"r","11":"pickup"},{"1":"dodge","2":"dakota pickup 4wd","3":"4.7","4":"2008","5":"8","6":"auto(l5)","7":"4","8":"14","9":"19","10":"r","11":"pickup"},{"1":"dodge","2":"dakota pickup 4wd","3":"4.7","4":"2008","5":"8","6":"auto(l5)","7":"4","8":"14","9":"19","10":"r","11":"pickup"},{"1":"dodge","2":"dakota pickup 4wd","3":"4.7","4":"2008","5":"8","6":"auto(l5)","7":"4","8":"9","9":"12","10":"e","11":"pickup"},{"1":"dodge","2":"dakota pickup 4wd","3":"5.2","4":"1999","5":"8","6":"manual(m5)","7":"4","8":"11","9":"17","10":"r","11":"pickup"},{"1":"dodge","2":"dakota pickup 4wd","3":"5.2","4":"1999","5":"8","6":"auto(l4)","7":"4","8":"11","9":"15","10":"r","11":"pickup"},{"1":"dodge","2":"durango 4wd","3":"3.9","4":"1999","5":"6","6":"auto(l4)","7":"4","8":"13","9":"17","10":"r","11":"suv"},{"1":"dodge","2":"durango 4wd","3":"4.7","4":"2008","5":"8","6":"auto(l5)","7":"4","8":"13","9":"17","10":"r","11":"suv"},{"1":"dodge","2":"durango 4wd","3":"4.7","4":"2008","5":"8","6":"auto(l5)","7":"4","8":"9","9":"12","10":"e","11":"suv"},{"1":"dodge","2":"durango 4wd","3":"4.7","4":"2008","5":"8","6":"auto(l5)","7":"4","8":"13","9":"17","10":"r","11":"suv"},{"1":"dodge","2":"durango 4wd","3":"5.2","4":"1999","5":"8","6":"auto(l4)","7":"4","8":"11","9":"16","10":"r","11":"suv"},{"1":"dodge","2":"durango 4wd","3":"5.7","4":"2008","5":"8","6":"auto(l5)","7":"4","8":"13","9":"18","10":"r","11":"suv"},{"1":"dodge","2":"durango 4wd","3":"5.9","4":"1999","5":"8","6":"auto(l4)","7":"4","8":"11","9":"15","10":"r","11":"suv"},{"1":"dodge","2":"ram 1500 pickup 4wd","3":"4.7","4":"2008","5":"8","6":"manual(m6)","7":"4","8":"12","9":"16","10":"r","11":"pickup"},{"1":"dodge","2":"ram 1500 pickup 4wd","3":"4.7","4":"2008","5":"8","6":"auto(l5)","7":"4","8":"9","9":"12","10":"e","11":"pickup"},{"1":"dodge","2":"ram 1500 pickup 4wd","3":"4.7","4":"2008","5":"8","6":"auto(l5)","7":"4","8":"13","9":"17","10":"r","11":"pickup"},{"1":"dodge","2":"ram 1500 pickup 4wd","3":"4.7","4":"2008","5":"8","6":"auto(l5)","7":"4","8":"13","9":"17","10":"r","11":"pickup"},{"1":"dodge","2":"ram 1500 pickup 4wd","3":"4.7","4":"2008","5":"8","6":"manual(m6)","7":"4","8":"12","9":"16","10":"r","11":"pickup"},{"1":"dodge","2":"ram 1500 pickup 4wd","3":"4.7","4":"2008","5":"8","6":"manual(m6)","7":"4","8":"9","9":"12","10":"e","11":"pickup"},{"1":"dodge","2":"ram 1500 pickup 4wd","3":"5.2","4":"1999","5":"8","6":"auto(l4)","7":"4","8":"11","9":"15","10":"r","11":"pickup"},{"1":"dodge","2":"ram 1500 pickup 4wd","3":"5.2","4":"1999","5":"8","6":"manual(m5)","7":"4","8":"11","9":"16","10":"r","11":"pickup"},{"1":"dodge","2":"ram 1500 pickup 4wd","3":"5.7","4":"2008","5":"8","6":"auto(l5)","7":"4","8":"13","9":"17","10":"r","11":"pickup"},{"1":"dodge","2":"ram 1500 pickup 4wd","3":"5.9","4":"1999","5":"8","6":"auto(l4)","7":"4","8":"11","9":"15","10":"r","11":"pickup"},{"1":"ford","2":"expedition 2wd","3":"4.6","4":"1999","5":"8","6":"auto(l4)","7":"r","8":"11","9":"17","10":"r","11":"suv"},{"1":"ford","2":"expedition 2wd","3":"5.4","4":"1999","5":"8","6":"auto(l4)","7":"r","8":"11","9":"17","10":"r","11":"suv"},{"1":"ford","2":"expedition 2wd","3":"5.4","4":"2008","5":"8","6":"auto(l6)","7":"r","8":"12","9":"18","10":"r","11":"suv"},{"1":"ford","2":"explorer 4wd","3":"4.0","4":"1999","5":"6","6":"auto(l5)","7":"4","8":"14","9":"17","10":"r","11":"suv"},{"1":"ford","2":"explorer 4wd","3":"4.0","4":"1999","5":"6","6":"manual(m5)","7":"4","8":"15","9":"19","10":"r","11":"suv"},{"1":"ford","2":"explorer 4wd","3":"4.0","4":"1999","5":"6","6":"auto(l5)","7":"4","8":"14","9":"17","10":"r","11":"suv"},{"1":"ford","2":"explorer 4wd","3":"4.0","4":"2008","5":"6","6":"auto(l5)","7":"4","8":"13","9":"19","10":"r","11":"suv"},{"1":"ford","2":"explorer 4wd","3":"4.6","4":"2008","5":"8","6":"auto(l6)","7":"4","8":"13","9":"19","10":"r","11":"suv"},{"1":"ford","2":"explorer 4wd","3":"5.0","4":"1999","5":"8","6":"auto(l4)","7":"4","8":"13","9":"17","10":"r","11":"suv"},{"1":"ford","2":"f150 pickup 4wd","3":"4.2","4":"1999","5":"6","6":"auto(l4)","7":"4","8":"14","9":"17","10":"r","11":"pickup"},{"1":"ford","2":"f150 pickup 4wd","3":"4.2","4":"1999","5":"6","6":"manual(m5)","7":"4","8":"14","9":"17","10":"r","11":"pickup"},{"1":"ford","2":"f150 pickup 4wd","3":"4.6","4":"1999","5":"8","6":"manual(m5)","7":"4","8":"13","9":"16","10":"r","11":"pickup"},{"1":"ford","2":"f150 pickup 4wd","3":"4.6","4":"1999","5":"8","6":"auto(l4)","7":"4","8":"13","9":"16","10":"r","11":"pickup"},{"1":"ford","2":"f150 pickup 4wd","3":"4.6","4":"2008","5":"8","6":"auto(l4)","7":"4","8":"13","9":"17","10":"r","11":"pickup"},{"1":"ford","2":"f150 pickup 4wd","3":"5.4","4":"1999","5":"8","6":"auto(l4)","7":"4","8":"11","9":"15","10":"r","11":"pickup"},{"1":"ford","2":"f150 pickup 4wd","3":"5.4","4":"2008","5":"8","6":"auto(l4)","7":"4","8":"13","9":"17","10":"r","11":"pickup"},{"1":"ford","2":"mustang","3":"3.8","4":"1999","5":"6","6":"manual(m5)","7":"r","8":"18","9":"26","10":"r","11":"subcompact"},{"1":"ford","2":"mustang","3":"3.8","4":"1999","5":"6","6":"auto(l4)","7":"r","8":"18","9":"25","10":"r","11":"subcompact"},{"1":"ford","2":"mustang","3":"4.0","4":"2008","5":"6","6":"manual(m5)","7":"r","8":"17","9":"26","10":"r","11":"subcompact"},{"1":"ford","2":"mustang","3":"4.0","4":"2008","5":"6","6":"auto(l5)","7":"r","8":"16","9":"24","10":"r","11":"subcompact"},{"1":"ford","2":"mustang","3":"4.6","4":"1999","5":"8","6":"auto(l4)","7":"r","8":"15","9":"21","10":"r","11":"subcompact"},{"1":"ford","2":"mustang","3":"4.6","4":"1999","5":"8","6":"manual(m5)","7":"r","8":"15","9":"22","10":"r","11":"subcompact"},{"1":"ford","2":"mustang","3":"4.6","4":"2008","5":"8","6":"manual(m5)","7":"r","8":"15","9":"23","10":"r","11":"subcompact"},{"1":"ford","2":"mustang","3":"4.6","4":"2008","5":"8","6":"auto(l5)","7":"r","8":"15","9":"22","10":"r","11":"subcompact"},{"1":"ford","2":"mustang","3":"5.4","4":"2008","5":"8","6":"manual(m6)","7":"r","8":"14","9":"20","10":"p","11":"subcompact"},{"1":"honda","2":"civic","3":"1.6","4":"1999","5":"4","6":"manual(m5)","7":"f","8":"28","9":"33","10":"r","11":"subcompact"},{"1":"honda","2":"civic","3":"1.6","4":"1999","5":"4","6":"auto(l4)","7":"f","8":"24","9":"32","10":"r","11":"subcompact"},{"1":"honda","2":"civic","3":"1.6","4":"1999","5":"4","6":"manual(m5)","7":"f","8":"25","9":"32","10":"r","11":"subcompact"},{"1":"honda","2":"civic","3":"1.6","4":"1999","5":"4","6":"manual(m5)","7":"f","8":"23","9":"29","10":"p","11":"subcompact"},{"1":"honda","2":"civic","3":"1.6","4":"1999","5":"4","6":"auto(l4)","7":"f","8":"24","9":"32","10":"r","11":"subcompact"},{"1":"honda","2":"civic","3":"1.8","4":"2008","5":"4","6":"manual(m5)","7":"f","8":"26","9":"34","10":"r","11":"subcompact"},{"1":"honda","2":"civic","3":"1.8","4":"2008","5":"4","6":"auto(l5)","7":"f","8":"25","9":"36","10":"r","11":"subcompact"},{"1":"honda","2":"civic","3":"1.8","4":"2008","5":"4","6":"auto(l5)","7":"f","8":"24","9":"36","10":"c","11":"subcompact"},{"1":"honda","2":"civic","3":"2.0","4":"2008","5":"4","6":"manual(m6)","7":"f","8":"21","9":"29","10":"p","11":"subcompact"},{"1":"hyundai","2":"sonata","3":"2.4","4":"1999","5":"4","6":"auto(l4)","7":"f","8":"18","9":"26","10":"r","11":"midsize"},{"1":"hyundai","2":"sonata","3":"2.4","4":"1999","5":"4","6":"manual(m5)","7":"f","8":"18","9":"27","10":"r","11":"midsize"},{"1":"hyundai","2":"sonata","3":"2.4","4":"2008","5":"4","6":"auto(l4)","7":"f","8":"21","9":"30","10":"r","11":"midsize"},{"1":"hyundai","2":"sonata","3":"2.4","4":"2008","5":"4","6":"manual(m5)","7":"f","8":"21","9":"31","10":"r","11":"midsize"},{"1":"hyundai","2":"sonata","3":"2.5","4":"1999","5":"6","6":"auto(l4)","7":"f","8":"18","9":"26","10":"r","11":"midsize"},{"1":"hyundai","2":"sonata","3":"2.5","4":"1999","5":"6","6":"manual(m5)","7":"f","8":"18","9":"26","10":"r","11":"midsize"},{"1":"hyundai","2":"sonata","3":"3.3","4":"2008","5":"6","6":"auto(l5)","7":"f","8":"19","9":"28","10":"r","11":"midsize"},{"1":"hyundai","2":"tiburon","3":"2.0","4":"1999","5":"4","6":"auto(l4)","7":"f","8":"19","9":"26","10":"r","11":"subcompact"},{"1":"hyundai","2":"tiburon","3":"2.0","4":"1999","5":"4","6":"manual(m5)","7":"f","8":"19","9":"29","10":"r","11":"subcompact"},{"1":"hyundai","2":"tiburon","3":"2.0","4":"2008","5":"4","6":"manual(m5)","7":"f","8":"20","9":"28","10":"r","11":"subcompact"},{"1":"hyundai","2":"tiburon","3":"2.0","4":"2008","5":"4","6":"auto(l4)","7":"f","8":"20","9":"27","10":"r","11":"subcompact"},{"1":"hyundai","2":"tiburon","3":"2.7","4":"2008","5":"6","6":"auto(l4)","7":"f","8":"17","9":"24","10":"r","11":"subcompact"},{"1":"hyundai","2":"tiburon","3":"2.7","4":"2008","5":"6","6":"manual(m6)","7":"f","8":"16","9":"24","10":"r","11":"subcompact"},{"1":"hyundai","2":"tiburon","3":"2.7","4":"2008","5":"6","6":"manual(m5)","7":"f","8":"17","9":"24","10":"r","11":"subcompact"},{"1":"jeep","2":"grand cherokee 4wd","3":"3.0","4":"2008","5":"6","6":"auto(l5)","7":"4","8":"17","9":"22","10":"d","11":"suv"},{"1":"jeep","2":"grand cherokee 4wd","3":"3.7","4":"2008","5":"6","6":"auto(l5)","7":"4","8":"15","9":"19","10":"r","11":"suv"},{"1":"jeep","2":"grand cherokee 4wd","3":"4.0","4":"1999","5":"6","6":"auto(l4)","7":"4","8":"15","9":"20","10":"r","11":"suv"},{"1":"jeep","2":"grand cherokee 4wd","3":"4.7","4":"1999","5":"8","6":"auto(l4)","7":"4","8":"14","9":"17","10":"r","11":"suv"},{"1":"jeep","2":"grand cherokee 4wd","3":"4.7","4":"2008","5":"8","6":"auto(l5)","7":"4","8":"9","9":"12","10":"e","11":"suv"},{"1":"jeep","2":"grand cherokee 4wd","3":"4.7","4":"2008","5":"8","6":"auto(l5)","7":"4","8":"14","9":"19","10":"r","11":"suv"},{"1":"jeep","2":"grand cherokee 4wd","3":"5.7","4":"2008","5":"8","6":"auto(l5)","7":"4","8":"13","9":"18","10":"r","11":"suv"},{"1":"jeep","2":"grand cherokee 4wd","3":"6.1","4":"2008","5":"8","6":"auto(l5)","7":"4","8":"11","9":"14","10":"p","11":"suv"},{"1":"land rover","2":"range rover","3":"4.0","4":"1999","5":"8","6":"auto(l4)","7":"4","8":"11","9":"15","10":"p","11":"suv"},{"1":"land rover","2":"range rover","3":"4.2","4":"2008","5":"8","6":"auto(s6)","7":"4","8":"12","9":"18","10":"r","11":"suv"},{"1":"land rover","2":"range rover","3":"4.4","4":"2008","5":"8","6":"auto(s6)","7":"4","8":"12","9":"18","10":"r","11":"suv"},{"1":"land rover","2":"range rover","3":"4.6","4":"1999","5":"8","6":"auto(l4)","7":"4","8":"11","9":"15","10":"p","11":"suv"},{"1":"lincoln","2":"navigator 2wd","3":"5.4","4":"1999","5":"8","6":"auto(l4)","7":"r","8":"11","9":"17","10":"r","11":"suv"},{"1":"lincoln","2":"navigator 2wd","3":"5.4","4":"1999","5":"8","6":"auto(l4)","7":"r","8":"11","9":"16","10":"p","11":"suv"},{"1":"lincoln","2":"navigator 2wd","3":"5.4","4":"2008","5":"8","6":"auto(l6)","7":"r","8":"12","9":"18","10":"r","11":"suv"},{"1":"mercury","2":"mountaineer 4wd","3":"4.0","4":"1999","5":"6","6":"auto(l5)","7":"4","8":"14","9":"17","10":"r","11":"suv"},{"1":"mercury","2":"mountaineer 4wd","3":"4.0","4":"2008","5":"6","6":"auto(l5)","7":"4","8":"13","9":"19","10":"r","11":"suv"},{"1":"mercury","2":"mountaineer 4wd","3":"4.6","4":"2008","5":"8","6":"auto(l6)","7":"4","8":"13","9":"19","10":"r","11":"suv"},{"1":"mercury","2":"mountaineer 4wd","3":"5.0","4":"1999","5":"8","6":"auto(l4)","7":"4","8":"13","9":"17","10":"r","11":"suv"},{"1":"nissan","2":"altima","3":"2.4","4":"1999","5":"4","6":"manual(m5)","7":"f","8":"21","9":"29","10":"r","11":"compact"},{"1":"nissan","2":"altima","3":"2.4","4":"1999","5":"4","6":"auto(l4)","7":"f","8":"19","9":"27","10":"r","11":"compact"},{"1":"nissan","2":"altima","3":"2.5","4":"2008","5":"4","6":"auto(av)","7":"f","8":"23","9":"31","10":"r","11":"midsize"},{"1":"nissan","2":"altima","3":"2.5","4":"2008","5":"4","6":"manual(m6)","7":"f","8":"23","9":"32","10":"r","11":"midsize"},{"1":"nissan","2":"altima","3":"3.5","4":"2008","5":"6","6":"manual(m6)","7":"f","8":"19","9":"27","10":"p","11":"midsize"},{"1":"nissan","2":"altima","3":"3.5","4":"2008","5":"6","6":"auto(av)","7":"f","8":"19","9":"26","10":"p","11":"midsize"},{"1":"nissan","2":"maxima","3":"3.0","4":"1999","5":"6","6":"auto(l4)","7":"f","8":"18","9":"26","10":"r","11":"midsize"},{"1":"nissan","2":"maxima","3":"3.0","4":"1999","5":"6","6":"manual(m5)","7":"f","8":"19","9":"25","10":"r","11":"midsize"},{"1":"nissan","2":"maxima","3":"3.5","4":"2008","5":"6","6":"auto(av)","7":"f","8":"19","9":"25","10":"p","11":"midsize"},{"1":"nissan","2":"pathfinder 4wd","3":"3.3","4":"1999","5":"6","6":"auto(l4)","7":"4","8":"14","9":"17","10":"r","11":"suv"},{"1":"nissan","2":"pathfinder 4wd","3":"3.3","4":"1999","5":"6","6":"manual(m5)","7":"4","8":"15","9":"17","10":"r","11":"suv"},{"1":"nissan","2":"pathfinder 4wd","3":"4.0","4":"2008","5":"6","6":"auto(l5)","7":"4","8":"14","9":"20","10":"p","11":"suv"},{"1":"nissan","2":"pathfinder 4wd","3":"5.6","4":"2008","5":"8","6":"auto(s5)","7":"4","8":"12","9":"18","10":"p","11":"suv"},{"1":"pontiac","2":"grand prix","3":"3.1","4":"1999","5":"6","6":"auto(l4)","7":"f","8":"18","9":"26","10":"r","11":"midsize"},{"1":"pontiac","2":"grand prix","3":"3.8","4":"1999","5":"6","6":"auto(l4)","7":"f","8":"16","9":"26","10":"p","11":"midsize"},{"1":"pontiac","2":"grand prix","3":"3.8","4":"1999","5":"6","6":"auto(l4)","7":"f","8":"17","9":"27","10":"r","11":"midsize"},{"1":"pontiac","2":"grand prix","3":"3.8","4":"2008","5":"6","6":"auto(l4)","7":"f","8":"18","9":"28","10":"r","11":"midsize"},{"1":"pontiac","2":"grand prix","3":"5.3","4":"2008","5":"8","6":"auto(s4)","7":"f","8":"16","9":"25","10":"p","11":"midsize"},{"1":"subaru","2":"forester awd","3":"2.5","4":"1999","5":"4","6":"manual(m5)","7":"4","8":"18","9":"25","10":"r","11":"suv"},{"1":"subaru","2":"forester awd","3":"2.5","4":"1999","5":"4","6":"auto(l4)","7":"4","8":"18","9":"24","10":"r","11":"suv"},{"1":"subaru","2":"forester awd","3":"2.5","4":"2008","5":"4","6":"manual(m5)","7":"4","8":"20","9":"27","10":"r","11":"suv"},{"1":"subaru","2":"forester awd","3":"2.5","4":"2008","5":"4","6":"manual(m5)","7":"4","8":"19","9":"25","10":"p","11":"suv"},{"1":"subaru","2":"forester awd","3":"2.5","4":"2008","5":"4","6":"auto(l4)","7":"4","8":"20","9":"26","10":"r","11":"suv"},{"1":"subaru","2":"forester awd","3":"2.5","4":"2008","5":"4","6":"auto(l4)","7":"4","8":"18","9":"23","10":"p","11":"suv"},{"1":"subaru","2":"impreza awd","3":"2.2","4":"1999","5":"4","6":"auto(l4)","7":"4","8":"21","9":"26","10":"r","11":"subcompact"},{"1":"subaru","2":"impreza awd","3":"2.2","4":"1999","5":"4","6":"manual(m5)","7":"4","8":"19","9":"26","10":"r","11":"subcompact"},{"1":"subaru","2":"impreza awd","3":"2.5","4":"1999","5":"4","6":"manual(m5)","7":"4","8":"19","9":"26","10":"r","11":"subcompact"},{"1":"subaru","2":"impreza awd","3":"2.5","4":"1999","5":"4","6":"auto(l4)","7":"4","8":"19","9":"26","10":"r","11":"subcompact"},{"1":"subaru","2":"impreza awd","3":"2.5","4":"2008","5":"4","6":"auto(s4)","7":"4","8":"20","9":"25","10":"p","11":"compact"},{"1":"subaru","2":"impreza awd","3":"2.5","4":"2008","5":"4","6":"auto(s4)","7":"4","8":"20","9":"27","10":"r","11":"compact"},{"1":"subaru","2":"impreza awd","3":"2.5","4":"2008","5":"4","6":"manual(m5)","7":"4","8":"19","9":"25","10":"p","11":"compact"},{"1":"subaru","2":"impreza awd","3":"2.5","4":"2008","5":"4","6":"manual(m5)","7":"4","8":"20","9":"27","10":"r","11":"compact"},{"1":"toyota","2":"4runner 4wd","3":"2.7","4":"1999","5":"4","6":"manual(m5)","7":"4","8":"15","9":"20","10":"r","11":"suv"},{"1":"toyota","2":"4runner 4wd","3":"2.7","4":"1999","5":"4","6":"auto(l4)","7":"4","8":"16","9":"20","10":"r","11":"suv"},{"1":"toyota","2":"4runner 4wd","3":"3.4","4":"1999","5":"6","6":"auto(l4)","7":"4","8":"15","9":"19","10":"r","11":"suv"},{"1":"toyota","2":"4runner 4wd","3":"3.4","4":"1999","5":"6","6":"manual(m5)","7":"4","8":"15","9":"17","10":"r","11":"suv"},{"1":"toyota","2":"4runner 4wd","3":"4.0","4":"2008","5":"6","6":"auto(l5)","7":"4","8":"16","9":"20","10":"r","11":"suv"},{"1":"toyota","2":"4runner 4wd","3":"4.7","4":"2008","5":"8","6":"auto(l5)","7":"4","8":"14","9":"17","10":"r","11":"suv"},{"1":"toyota","2":"camry","3":"2.2","4":"1999","5":"4","6":"manual(m5)","7":"f","8":"21","9":"29","10":"r","11":"midsize"},{"1":"toyota","2":"camry","3":"2.2","4":"1999","5":"4","6":"auto(l4)","7":"f","8":"21","9":"27","10":"r","11":"midsize"},{"1":"toyota","2":"camry","3":"2.4","4":"2008","5":"4","6":"manual(m5)","7":"f","8":"21","9":"31","10":"r","11":"midsize"},{"1":"toyota","2":"camry","3":"2.4","4":"2008","5":"4","6":"auto(l5)","7":"f","8":"21","9":"31","10":"r","11":"midsize"},{"1":"toyota","2":"camry","3":"3.0","4":"1999","5":"6","6":"auto(l4)","7":"f","8":"18","9":"26","10":"r","11":"midsize"},{"1":"toyota","2":"camry","3":"3.0","4":"1999","5":"6","6":"manual(m5)","7":"f","8":"18","9":"26","10":"r","11":"midsize"},{"1":"toyota","2":"camry","3":"3.5","4":"2008","5":"6","6":"auto(s6)","7":"f","8":"19","9":"28","10":"r","11":"midsize"},{"1":"toyota","2":"camry solara","3":"2.2","4":"1999","5":"4","6":"auto(l4)","7":"f","8":"21","9":"27","10":"r","11":"compact"},{"1":"toyota","2":"camry solara","3":"2.2","4":"1999","5":"4","6":"manual(m5)","7":"f","8":"21","9":"29","10":"r","11":"compact"},{"1":"toyota","2":"camry solara","3":"2.4","4":"2008","5":"4","6":"manual(m5)","7":"f","8":"21","9":"31","10":"r","11":"compact"},{"1":"toyota","2":"camry solara","3":"2.4","4":"2008","5":"4","6":"auto(s5)","7":"f","8":"22","9":"31","10":"r","11":"compact"},{"1":"toyota","2":"camry solara","3":"3.0","4":"1999","5":"6","6":"auto(l4)","7":"f","8":"18","9":"26","10":"r","11":"compact"},{"1":"toyota","2":"camry solara","3":"3.0","4":"1999","5":"6","6":"manual(m5)","7":"f","8":"18","9":"26","10":"r","11":"compact"},{"1":"toyota","2":"camry solara","3":"3.3","4":"2008","5":"6","6":"auto(s5)","7":"f","8":"18","9":"27","10":"r","11":"compact"},{"1":"toyota","2":"corolla","3":"1.8","4":"1999","5":"4","6":"auto(l3)","7":"f","8":"24","9":"30","10":"r","11":"compact"},{"1":"toyota","2":"corolla","3":"1.8","4":"1999","5":"4","6":"auto(l4)","7":"f","8":"24","9":"33","10":"r","11":"compact"},{"1":"toyota","2":"corolla","3":"1.8","4":"1999","5":"4","6":"manual(m5)","7":"f","8":"26","9":"35","10":"r","11":"compact"},{"1":"toyota","2":"corolla","3":"1.8","4":"2008","5":"4","6":"manual(m5)","7":"f","8":"28","9":"37","10":"r","11":"compact"},{"1":"toyota","2":"corolla","3":"1.8","4":"2008","5":"4","6":"auto(l4)","7":"f","8":"26","9":"35","10":"r","11":"compact"},{"1":"toyota","2":"land cruiser wagon 4wd","3":"4.7","4":"1999","5":"8","6":"auto(l4)","7":"4","8":"11","9":"15","10":"r","11":"suv"},{"1":"toyota","2":"land cruiser wagon 4wd","3":"5.7","4":"2008","5":"8","6":"auto(s6)","7":"4","8":"13","9":"18","10":"r","11":"suv"},{"1":"toyota","2":"toyota tacoma 4wd","3":"2.7","4":"1999","5":"4","6":"manual(m5)","7":"4","8":"15","9":"20","10":"r","11":"pickup"},{"1":"toyota","2":"toyota tacoma 4wd","3":"2.7","4":"1999","5":"4","6":"auto(l4)","7":"4","8":"16","9":"20","10":"r","11":"pickup"},{"1":"toyota","2":"toyota tacoma 4wd","3":"2.7","4":"2008","5":"4","6":"manual(m5)","7":"4","8":"17","9":"22","10":"r","11":"pickup"},{"1":"toyota","2":"toyota tacoma 4wd","3":"3.4","4":"1999","5":"6","6":"manual(m5)","7":"4","8":"15","9":"17","10":"r","11":"pickup"},{"1":"toyota","2":"toyota tacoma 4wd","3":"3.4","4":"1999","5":"6","6":"auto(l4)","7":"4","8":"15","9":"19","10":"r","11":"pickup"},{"1":"toyota","2":"toyota tacoma 4wd","3":"4.0","4":"2008","5":"6","6":"manual(m6)","7":"4","8":"15","9":"18","10":"r","11":"pickup"},{"1":"toyota","2":"toyota tacoma 4wd","3":"4.0","4":"2008","5":"6","6":"auto(l5)","7":"4","8":"16","9":"20","10":"r","11":"pickup"},{"1":"volkswagen","2":"gti","3":"2.0","4":"1999","5":"4","6":"manual(m5)","7":"f","8":"21","9":"29","10":"r","11":"compact"},{"1":"volkswagen","2":"gti","3":"2.0","4":"1999","5":"4","6":"auto(l4)","7":"f","8":"19","9":"26","10":"r","11":"compact"},{"1":"volkswagen","2":"gti","3":"2.0","4":"2008","5":"4","6":"manual(m6)","7":"f","8":"21","9":"29","10":"p","11":"compact"},{"1":"volkswagen","2":"gti","3":"2.0","4":"2008","5":"4","6":"auto(s6)","7":"f","8":"22","9":"29","10":"p","11":"compact"},{"1":"volkswagen","2":"gti","3":"2.8","4":"1999","5":"6","6":"manual(m5)","7":"f","8":"17","9":"24","10":"r","11":"compact"},{"1":"volkswagen","2":"jetta","3":"1.9","4":"1999","5":"4","6":"manual(m5)","7":"f","8":"33","9":"44","10":"d","11":"compact"},{"1":"volkswagen","2":"jetta","3":"2.0","4":"1999","5":"4","6":"manual(m5)","7":"f","8":"21","9":"29","10":"r","11":"compact"},{"1":"volkswagen","2":"jetta","3":"2.0","4":"1999","5":"4","6":"auto(l4)","7":"f","8":"19","9":"26","10":"r","11":"compact"},{"1":"volkswagen","2":"jetta","3":"2.0","4":"2008","5":"4","6":"auto(s6)","7":"f","8":"22","9":"29","10":"p","11":"compact"},{"1":"volkswagen","2":"jetta","3":"2.0","4":"2008","5":"4","6":"manual(m6)","7":"f","8":"21","9":"29","10":"p","11":"compact"},{"1":"volkswagen","2":"jetta","3":"2.5","4":"2008","5":"5","6":"auto(s6)","7":"f","8":"21","9":"29","10":"r","11":"compact"},{"1":"volkswagen","2":"jetta","3":"2.5","4":"2008","5":"5","6":"manual(m5)","7":"f","8":"21","9":"29","10":"r","11":"compact"},{"1":"volkswagen","2":"jetta","3":"2.8","4":"1999","5":"6","6":"auto(l4)","7":"f","8":"16","9":"23","10":"r","11":"compact"},{"1":"volkswagen","2":"jetta","3":"2.8","4":"1999","5":"6","6":"manual(m5)","7":"f","8":"17","9":"24","10":"r","11":"compact"},{"1":"volkswagen","2":"new beetle","3":"1.9","4":"1999","5":"4","6":"manual(m5)","7":"f","8":"35","9":"44","10":"d","11":"subcompact"},{"1":"volkswagen","2":"new beetle","3":"1.9","4":"1999","5":"4","6":"auto(l4)","7":"f","8":"29","9":"41","10":"d","11":"subcompact"},{"1":"volkswagen","2":"new beetle","3":"2.0","4":"1999","5":"4","6":"manual(m5)","7":"f","8":"21","9":"29","10":"r","11":"subcompact"},{"1":"volkswagen","2":"new beetle","3":"2.0","4":"1999","5":"4","6":"auto(l4)","7":"f","8":"19","9":"26","10":"r","11":"subcompact"},{"1":"volkswagen","2":"new beetle","3":"2.5","4":"2008","5":"5","6":"manual(m5)","7":"f","8":"20","9":"28","10":"r","11":"subcompact"},{"1":"volkswagen","2":"new beetle","3":"2.5","4":"2008","5":"5","6":"auto(s6)","7":"f","8":"20","9":"29","10":"r","11":"subcompact"},{"1":"volkswagen","2":"passat","3":"1.8","4":"1999","5":"4","6":"manual(m5)","7":"f","8":"21","9":"29","10":"p","11":"midsize"},{"1":"volkswagen","2":"passat","3":"1.8","4":"1999","5":"4","6":"auto(l5)","7":"f","8":"18","9":"29","10":"p","11":"midsize"},{"1":"volkswagen","2":"passat","3":"2.0","4":"2008","5":"4","6":"auto(s6)","7":"f","8":"19","9":"28","10":"p","11":"midsize"},{"1":"volkswagen","2":"passat","3":"2.0","4":"2008","5":"4","6":"manual(m6)","7":"f","8":"21","9":"29","10":"p","11":"midsize"},{"1":"volkswagen","2":"passat","3":"2.8","4":"1999","5":"6","6":"auto(l5)","7":"f","8":"16","9":"26","10":"p","11":"midsize"},{"1":"volkswagen","2":"passat","3":"2.8","4":"1999","5":"6","6":"manual(m5)","7":"f","8":"18","9":"26","10":"p","11":"midsize"},{"1":"volkswagen","2":"passat","3":"3.6","4":"2008","5":"6","6":"auto(s6)","7":"f","8":"17","9":"26","10":"p","11":"midsize"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>
< -->

--- 

- The function `str()` will display the "structure" of the data frame.
    - It will display the number of **observations** and **variables**, list the variables, give the type of each variable, and show some elements of each variable. 
    - This information can also be found in the "Environment" window in RStudio.

```r
str(mpg)
```

```
## Classes 'tbl_df', 'tbl' and 'data.frame':	234 obs. of  11 variables:
##  $ manufacturer: chr  "audi" "audi" "audi" "audi" ...
##  $ model       : chr  "a4" "a4" "a4" "a4" ...
##  $ displ       : num  1.8 1.8 2 2 2.8 2.8 3.1 1.8 1.8 2 ...
##  $ year        : int  1999 1999 2008 2008 1999 1999 2008 1999 1999 2008 ...
##  $ cyl         : int  4 4 4 4 6 6 6 4 4 4 ...
##  $ trans       : chr  "auto(l5)" "manual(m5)" "manual(m6)" "auto(av)" ...
##  $ drv         : chr  "f" "f" "f" "f" ...
##  $ cty         : int  18 21 20 21 16 18 18 18 16 20 ...
##  $ hwy         : int  29 29 31 30 26 26 27 26 25 28 ...
##  $ fl          : chr  "p" "p" "p" "p" ...
##  $ class       : chr  "compact" "compact" "compact" "compact" ...
```

<!-- >
It is important to note that while matrices have rows and columns, data frames (tibbles) instead have observations and variables. When displayed in the console or viewer, each row is an observation and each column is a variable. However generally speaking, their order does not matter, it is simply a side-effect of how the data was entered or stored.

In this dataset an observation is for a particular model-year of a car, and the variables describe attributes of the car, for example its highway fuel efficiency.

To understand more about the data set, we use the `?` operator to pull up the documentation for the data.


```r
?mpg
```
< -->

---

-  `names()` function to obtain names of the variables in the dataset

```r
names(mpg)
```

```
##  [1] "manufacturer" "model"        "displ"        "year"         "cyl"         
##  [6] "trans"        "drv"          "cty"          "hwy"          "fl"          
## [11] "class"
```

- To access one of the variables **as a vector**, we use the `$` operator.

```r
mpg$year
```

```
##   [1] 1999 1999 2008 2008 1999 1999 2008 1999 1999 2008 2008 1999 1999 2008 2008
##  [16] 1999 2008 2008 2008 2008 2008 1999 2008 1999 1999 2008 2008 2008 2008 2008
##  [31] 1999 1999 1999 2008 1999 2008 2008 1999 1999 1999 1999 2008 2008 2008 1999
##  [46] 1999 2008 2008 2008 2008 1999 1999 2008 2008 2008 1999 1999 1999 2008 2008
##  [61] 2008 1999 2008 1999 2008 2008 2008 2008 2008 2008 1999 1999 2008 1999 1999
##  [76] 1999 2008 1999 1999 1999 2008 2008 1999 1999 1999 1999 1999 2008 1999 2008
##  [91] 1999 1999 2008 2008 1999 1999 2008 2008 2008 1999 1999 1999 1999 1999 2008
## [106] 2008 2008 2008 1999 1999 2008 2008 1999 1999 2008 1999 1999 2008 2008 2008
## [121] 2008 2008 2008 2008 1999 1999 2008 2008 2008 2008 1999 2008 2008 1999 1999
## [136] 1999 2008 1999 2008 2008 1999 1999 1999 2008 2008 2008 2008 1999 1999 2008
## [151] 1999 1999 2008 2008 1999 1999 1999 2008 2008 1999 1999 2008 2008 2008 2008
## [166] 1999 1999 1999 1999 2008 2008 2008 2008 1999 1999 1999 1999 2008 2008 1999
## [181] 1999 2008 2008 1999 1999 2008 1999 1999 2008 2008 1999 1999 2008 1999 1999
## [196] 1999 2008 2008 1999 2008 1999 1999 2008 1999 1999 2008 2008 1999 1999 2008
## [211] 2008 1999 1999 1999 1999 2008 2008 2008 2008 1999 1999 1999 1999 1999 1999
## [226] 2008 2008 1999 1999 2008 2008 1999 1999 2008
```

```r
mpg$hwy
```

```
##   [1] 29 29 31 30 26 26 27 26 25 28 27 25 25 25 25 24 25 23 20 15 20 17 17 26 23
##  [26] 26 25 24 19 14 15 17 27 30 26 29 26 24 24 22 22 24 24 17 22 21 23 23 19 18
##  [51] 17 17 19 19 12 17 15 17 17 12 17 16 18 15 16 12 17 17 16 12 15 16 17 15 17
##  [76] 17 18 17 19 17 19 19 17 17 17 16 16 17 15 17 26 25 26 24 21 22 23 22 20 33
## [101] 32 32 29 32 34 36 36 29 26 27 30 31 26 26 28 26 29 28 27 24 24 24 22 19 20
## [126] 17 12 19 18 14 15 18 18 15 17 16 18 17 19 19 17 29 27 31 32 27 26 26 25 25
## [151] 17 17 20 18 26 26 27 28 25 25 24 27 25 26 23 26 26 26 26 25 27 25 27 20 20
## [176] 19 17 20 17 29 27 31 31 26 26 28 27 29 31 31 26 26 27 30 33 35 37 35 15 18
## [201] 20 20 22 17 19 18 20 29 26 29 29 24 44 29 26 29 29 29 29 23 24 44 41 29 26
## [226] 28 29 29 29 28 29 26 26 26
```

---

- We can use the `dim()`, `nrow()` and `ncol()` functions to obtain information about the dimension of the data frame.


```r
dim(mpg)
```

```
## [1] 234  11
```

```r
nrow(mpg)
```

```
## [1] 234
```

```r
ncol(mpg)
```

```
## [1] 11
```

## Subsetting data

- Subsetting data frames can work much like subsetting matrices using square brackets, `[,]`. 
- Here, we find fuel efficient vehicles earning over 35 miles per gallon and only display `manufacturer`, `model` and `year`.

```r
mpg[mpg$hwy > 35, c("manufacturer", "model", "year")]
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["manufacturer"],"name":[1],"type":["chr"],"align":["left"]},{"label":["model"],"name":[2],"type":["chr"],"align":["left"]},{"label":["year"],"name":[3],"type":["int"],"align":["right"]}],"data":[{"1":"honda","2":"civic","3":"2008"},{"1":"honda","2":"civic","3":"2008"},{"1":"toyota","2":"corolla","3":"2008"},{"1":"volkswagen","2":"jetta","3":"1999"},{"1":"volkswagen","2":"new beetle","3":"1999"},{"1":"volkswagen","2":"new beetle","3":"1999"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

---

- An alternative would be to use the `subset()` function, which has a much more readable syntax.


```r
subset(mpg, subset = hwy > 35, select = c("manufacturer", "model", "year"))
```

---

- Lastly, we could use the `filter` and `select` functions from the `dplyr` package which introduces the `%>%` operator from the `magrittr` package. 

```r
library(dplyr)
mpg %>% 
filter(hwy > 35) %>% 
select(manufacturer, model, year)
```
- I will give you an assignment about `dplyr` package in the `DataCamp` as a makeup lecture.

<!-- >
All three approaches produce the same results. Which you use will be largely based on a given situation as well as user preference.

When subsetting a data frame, be aware of what is being returned, as sometimes it may be a vector instead of a data frame. Also note that there are differences between subsetting a data frame and a tibble. A data frame operates more like a matrix where it is possible to reduce the subset to a vector. A tibble operates more like a list where it always subsets to another tibble.
< -->
