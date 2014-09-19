ffbase2
=======

Next version of `ffbase`
- dplyr on ff

Working, but documentation is not yet CRAN ready...

[![Build Status](https://travis-ci.org/edwindj/ffbase2.svg?branch=master)](https://travis-ci.org/edwindj/ffbase2)

## Install

`ffbase` is currently only available from github. To install it, run the following
script.
```S
# install.packages("devtools")
devtools::install_github("edwindj/ffbase2")
```

### CRAN-readiness

- Documentation needs to be completed
- Add more tests
- copy some `dplyr` internal functions into ffbase2
- Phase out dependency on `ffbase` (version 1)

## Usage


Creating a tbl_ffdf: this will create/use a temporary ffdf data.frame in 
`options("fftempdir")`.

```S
iris_f <- tbl_ffdf(iris)

species <- 
   iris_f %>%
   group_by(Species) %>%
   summarise(petal_width = sum(Petal.Width))
```

Use `src_ffdf` for storing your data in a directory 

```r
library(ffbase2)
# store a ffdf data.frame in "db_ff"" directory
cars <- tbl_ffdf(mtcars, src="db_ff", name="cars")

src <- src_ffdf("db_ff")
print(src)
```

```
## src: ffdf ['db_ff']
## tbls: cars
```

```r
#retrieve table from directory 
my_tbl <- tbl(src, from="cars")
print(my_tbl, n=2)
```

```
## Source:     ffdf ('db_ff/cars') [32 x 11]
## 
##    mpg cyl disp  hp drat    wt  qsec vs am gear carb
## 1   21   6  160 110  3.9 2.620 16.46  0  1    4    4
## 2   21   6  160 110  3.9 2.875 17.02  0  1    4    4
## .. ... ...  ... ...  ...   ...   ... .. ..  ...  ...
```

```
## [1] TRUE
```

Use `copy_to` to add data to a `src_ffdf`


