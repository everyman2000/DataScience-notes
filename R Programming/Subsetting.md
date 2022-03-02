# Subsetting

## Basics

There are three operators that can be used to extract subsets of R objects. 
• The `[` operator always returns an object of the same class as the original. It can be used to select multiple elements of an object 
• The `[[` operator is used to extract elements of a list or a data frame. It can only be used to extract a single element and the class of the returned object will not necessarily be a list or data frame. 
• The `$` operator is used to extract elements of a list or data frame by literal name. Its semantics are similar to that of `[[`.

```R
x <- c("a", "b", "c", "c", "d", "a")
x[1]
x[2]
x[1:4]
x[c(1,3,4)]
x[x > "a"]  #logical
u <- x>"a"
u
x[u]
```

## Subsetting lists

[[R Objects, Attributes and Data Types#Lists|Refer lists]]

```R
x <- list(foo = 1:4, bar = 0.6)
x[1] # gives a list
x[[1]]
x$bar
x[["bar"]]
x["bar"] #will give a list since we are subsetting a list
```

To extract multiple elements of a list we use `[`
```R
x <- list(foo = 1:4, bar = 0.6, baz = "hello"
x[c(1,3)]
```

**Note: A difference between `[[` and `$`**
Double brackets can be used with computed indices; $ can only be used with literal names

```R
x <- list(foo = 1:4, bar = 0.6, baz = "hello"
name <- "foo"
x[[name]] # computed index
x$name # element "name" does not exist. Will return NA
x$foo
```

## Subsetting nested elements of a List
The `[[` operator can take an integer sequence if you want to extract a nested element of a list.
```R
x <- list(a = list(10, 12, 14), b = c(3.14, 2.81))
x[[c(1, 3)]] #Get 3rd element of 1st element
x[[1]] [[3]] #same as above
x[c(2,1)] #1st element of 2nd element
```

```R
> x <- list(a = list(10, 12, 14), b = c(3.14, 2.81))



> x[1]
$a
$a[[1]]
[1] 10

$a[[2]]
[1] 12

$a[[3]]
[1] 14

> str(x[1])
List of 1
 $ a:List of 3
  ..$ : num 10
  ..$ : num 12
  ..$ : num 14

# returning the first element as a list

> x[[1]]
[[1]]
[1] 10

[[2]]
[1] 12

[[3]]
[1] 14

> str(x[[1]])
List of 3
 $ : num 10
 $ : num 12
 $ : num 14

# also returning as a list

> x[[1]][[3]]
[1] 14

> str(x[[1]][[3]])
 num 14


> x[1][3]
$<NA>
NULL

> str(x[1][3])
List of 1
 $ NA: NULL

> x[1][[3]]
Error in x[1][[3]] : subscript out of bounds

> x[[1]][3]
[[1]]
[1] 14

> str(x[[1]][3])
List of 1
 $ : num 14

# Note difference from x[[1]][[3]]

> x$a[[3]]
[1] 14

> str(x$a[[3]])
 num 14

# returns numeric

> x$a[3]
[[1]]
[1] 14

> str(x$a[3])
List of 1
 $ : num 14

# returns list

> y <- x[1]
> y[3]
$<NA>
NULL

> y
$a
$a[[1]]
[1] 10

$a[[2]]
[1] 12

$a[[3]]
[1] 14


> y$a[3]
[[1]]
[1] 14
```

## Subsetting Matrices
```R
> x <- matrix(1:6, 2, 3)
> x
     [,1] [,2] [,3]
[1,]    1    3    5
[2,]    2    4    6

> x[1,2]
[1] 3
> x[2,1]
[1] 2
> x[1,]  # access entire first row
[1] 1 3 5
> x[,2]  # access entire second column
[1] 3 4
```

**By default, when a single element of a matrix is retrieved, it is returned as a vector of length 1 rather than a 1×1 matrix. Often, this is exactly what we want, but this behavior can be turned off by setting drop = FALSE**

```R
> x <- matrix(1:6, 2, 3)
> x[1,2]
[1] 3
> x[1,2, drop="FALSE"]
     [,1]
[1,]    3
```
Similarly, when we extract a single row or column of a matrix, R by default drops the dimension of length 1, so instead of getting a 1 × 3 matrix after extracting the first row, we get a vector of length 3. This behavior can similarly be turned off with the drop = FALSE option.

```R
> x <- matrix(1:6, 2, 3) 
> x[1, ] 
[1] 1 3 5 
> x[1, , drop = FALSE] 
     [,1] [,2] [,3]
[1,]    1    3    5
```

