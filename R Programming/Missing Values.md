## Missing Values

Missing values are denoted by NA or [[R Objects, Attributes and Data Types#Numbers|NaN]] for undefined mathematical operations. NA means data is missing for unknown reasons while NaN means "not a number".

- `is.na()` is used to test objects if they are NA
- `is.nan()` is used to test for NaN
- NA values have a class, for example integer NA, character NA, etc
- A NaN value is also NA but the converse is not true

```R
x <- c(1, 2, NA, 10, 3)
is.na(x)
is.nan(x)
y <- c(1, 2, NaN, NA, 4)
is.na(y)
is.nan(y)
```

