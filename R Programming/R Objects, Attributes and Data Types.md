# Objects
R has five atomic classes of objects.

- characters
- numeric (real numbers)
- integers
- complex
- logical (T/F)

The most basic object is a vector.
- A vector can only contain objetcs of the same class.
- **One exception is a *list* which is represented as a vactor but can contain objects of different classes.**
- Empty vectors can be created with `vector()` function.

# Numbers
- Numbers in R are numeric objects, double precision real numbers. (1.00, 2.00)
- We can typecast to get an explicit integer by ussing L suffix. (1L)
- `Inf` can be used in ordinary calculations and is a special number. E.g. `1/inf`
- `NaN` represents undefined value, also thought of as a missing value.. E.g. `0/0; NaN`

# Attributes
- names, dimnames
- dimensions (e.g. matrices, arrays)
- class
- length
- other user-defined attributes/metadata

Attributes of an object can be accessed using `attributes()` function.

## Vectors
**Creating vectors**

- Using `c()` function.

```R
x <- c(0.5, 0.6) #numeric
x <- c(TRUE, FALSE) #logical
x <- c(T, F) #logical
x <- c("a", "b", "c") #character
x <- 9:29 # integer
x <- c(1+0i, 2+4i) # complex
```

- Using `vector()` function

```R
x <- vector("numeric", length = 10) #initialises with default value '0'
x
```

#### Mixing objects
```R
y <- c(1.7, "a") ## character  
y <- c(TRUE, 2) ## numeric 
y <- c("a", TRUE) ## character
```

Coercion occurs.

#### Explicit coercion

Using `as.` function.

```R
x <- 0:6
as.numeric(x)
as.logical(x)
as.character(x)
```

Sometimes explicit coercion will not work and result in NAs being produced.


```R
x <- c("a", "b", "c") 
as.numeric(x)
as.logical(x)
as.complex(x)
```

This is called **nonsensical** coercion.

---

## Lists
Lists are a special type of vector that can contain elements of different classes. Lists are a very important data type in R.


```R
x <- list(1, "a", TRUE, 1 + 4i) 
x
```

Elements of a list are indexed by double `[[]]` brackets as opposed to single-bracket indexation in vectors. So, each element in a list can be treated as a vector.

```R
x <- list((1:5), "a", TRUE, 1 + 4i) 
x
```


## Matrices
Matrices are vectors with a dimension attribute. The dimension attribute is itself an integer vector of length 2 (number of rows, number of columns)

```R
m <- matrix(nrow = 2, ncol = 3) 
m #initialised with NA values
m <- matrix(1:4, nrow = 2, ncol = 2)
dim(m) #returns dimensions
attributes(m) 
```

**Matrices get filled column-wise.**

#### Transforming a vector to a matrix
```R
m <- 1:10
m
dim(m) <- c(2, 5)
m
```

#### cbind-ing and rbind-ing
```R
x <- 1:3 
y <- 10:12 
cbind(x, y)
rbind(x, y)
```

## Factors
- Used to represent categorical data
- Ordered and unordered
- It is an integer vector where each integer has a *label*
- Treated specially using modelling functions like `lm()` and `glm()`
- Using factors with labels is better than using integers because factors are self-describing.

```R
x <- factor(c("yes", "yes", "no", "yes", "no"))
x
table(x)
unclass(x)
attr(x,"levels")
levels(x)
```

*Levels* is an attribute which is yes and no in this case.

==The order of the levels of a factor can be set using the levels argument to factor(). This can be important in linear modelling because the first level is used as the baseline level.==

By default, the base level is selected in alphabetical order. So "no" will be the baseline level and "yes" will be the second level. We can rectify this.

```R
x <- factor(c("yes", "yes", "no", "yes", "no"),
			levels = c("yes" , "no"))
```

## Data Frames
Data frames are used to store tabular data in R. They are an important type of object in R and are used in a variety of statistical modeling applications. Hadley Wickham’s package [dplyr](https://github.com/tidyverse/dplyr) has an optimized set of functions designed to work efficiently with data frames.

- Special type of list where every element of the list has same length
- Each element can be thought of as a column and the length of each element is the number of rows.
- Unlike matrices, each column can be of a different class.
- Data frames have a special attribute `row.names`
- Usually created by calling `read.table()` or `read.csv()`
- Can be converted to a matrix by calling `data.matrix()`; recall [[R Objects, Attributes and Data Types#Mixing objects|coercion]]

```R
x <- data.frame(foo = 1:4, bar = c(T, T, F, F)) 
x
nrow(x)
ncol(x)
```

---

# Names attribute
R objects can have names, for writing readable code and self-describing objects.

```R
x <- 1:3 
names(x)
names(x) <- c("New York", "Seattle", "Los Angeles")
x
names(x)
```

[[R Objects, Attributes and Data Types#Lists|Lists]] can also have names.

```R
x <- list("Los Angeles" = 1, Boston = 2, London = 3)
x
names(x)

x <- list("LA" = 1, "NYC" = FALSE, "SF" = 2+3i)
x
```

[[R Objects, Attributes and Data Types#Matrices|Matrices]] can have both row and column names.

```R
m <- matrix(1:4, nrow = 2, ncol = 2) 
dimnames(m) <- list(c("a", "b"), c("c", "d")) ## Recall each element is a vector
m
```

Column names and row names can be set separately using the `colnames()` and `rownames()` functions.

```R
m <- matrix(1:4, nrow = 2, ncol = 2) 
rownames(m) <- c("a", "b")
colnames(m) <- c("c", "d")
m
```


## Summary
- atomic classes
- vectors, lists
- factors
- data frames and matrices
- names
