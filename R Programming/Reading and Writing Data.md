# Reading Data

Some functions are:

- `read.table`, `read.csv` for reading tabular data
- `readLines` for reading lines of a text file
- `source`, for reading in R code files (inverse of `dump`)
- `dget` for reading in R code files (inverse of `dput`)
- `load` for reading in saved workspaces
- `unserialize` for reading single R objects in binary form

# Writing Data
- `write.table`
- `writeLines`
- `dump`
- `dput`
- `save`
- `serialize`

---

## Reading Data Files with read.table

Arguments of the function:
- file, the name of a file, or a connection
- header, logical indicating if the file has a header line
- sep, a string indicating how the columns are separated
- colClasses, a character vector indicating the class of each column
- nrows, number of rows
- comment.char, a character string indicating comment character
- skip, the number of lines to skip from the beginning
- stringsAsFactors, should character variables be coded as [[R Objects, Attributes and Data Types#Factors|factors]]?

For small to moderately sized datasets, you can usually call read.table without specifying any other arguments

```R
data <- read.table("foo.txt")
```

In this case, R will automatically 

- skip lines that begin with a # 
- figure out how many rows there are (and how much memory needs to be allocated) 
- figure what type of variable is in each column of the table.

Telling R all these things directly makes R run faster and more efficiently. The `read.csv()` function is identical to `read.table` except that some of the defaults are set differently (like the sep argument), default separator is a comma, as opposed to space. The `read.csv()` function always specifies header to be TRUE.

## Reading in Larger Datasets with read.table
With much larger datasets, there are a few things that you can do that will make your life easier and will prevent R from choking. 

• Read the help page for read.table, which contains many hints 

• Make a rough calculation of the memory required to store your dataset (see the next section for an example of how to do this). If the dataset is larger than the amount of RAM on your computer, you can probably stop right here.

• Set comment.char = "" if there are no commented lines in your file. 

• Use the colClasses argument. Specifying this option instead of using the default can make ’read.table’ run MUCH faster, often twice as fast. In order to use this option, you have to know the class of each column in your data frame. If all of the columns are “numeric”, for example, then you can just set colClasses = "numeric". A quick and dirty way to figure out the classes of each column is the following:

```R
initial <- read.table("datatable.txt", nrows = 100) 
classes <- sapply(initial, class) 
tabAll <- read.table("datatable.txt", colClasses = classes)
```

• Set nrows. This doesn’t make R run faster but it helps with memory usage. A mild overestimate is okay. You can use the Unix tool wc to calculate the number of lines in a file.

## Know your system

In general, when using R with larger datasets, it’s also useful to know a few things about your system. 

• How much memory is available on your system? 

• What other applications are in use? Can you close any of them? 

• Are there other users logged into the same system? 

• What operating system ar you using? Some operating systems can limit the amount of memory a single process can access

## Calculating memory requirements
For example, suppose I have a data frame with 1,500,000 rows and 120 columns, all of which are numeric data. Roughly, how much memory is required to store this data frame? Well, on most modern computers double precision floating point numbers are stored using 64 bits of memory, or 8 bytes. Given that information, you can do the following calculation.

1,500,000 × 120 × 8 bytes/numeric 

= 1,440,000,000 bytes 

= 1,440,000,000 / 2²⁰ bytes/MB 

= 1,373.29 MB / $2^{10}$  MB/GB

= 1.34 GB

The raw data for this is approximately 1.34 GB. A little bit more memory would be needed to read the data, because of overhead. A rule of thumb is twice the raw data.

## Textual Data Formats
- dumping and dputing are useful because the resulting textual format is edit-able, and in case of corruption, potentially recoverable.
- unlike writing out a table or csv file, dump and dput preserve the *metadata*, so that another user doesn't have to specify it again
- Textual formats work much better with VCS.
- Textual formats can be longer-lived, easier to fix in case of corruption.
- Textual formats adhere to 'Unix philosophy'
- Downside: The format is not space-efficient

## dput-ting R Objects
One way to pass data around is by deparsing the R object with dput() and reading it back in (parsing it) using dget().

```R
## Create a data frame 
y <- data.frame(a = 1, b = "a") 
## Print 'dput' output to console 
dput(y) 
```

Output: `structure(list(a = 1, b = "a"), class = "data.frame", row.names = c(NA, -1L))`

Notice that the dput() output is in the form of R code and that it preserves metadata like the class of the object, the row names, and the column names. The output of dput() can also be saved directly to a file.

```R
## Send 'dput' output to a file 
dput(y, file = "y.R") 
## Read in 'dput' output from a file 
new.y <- dget("y.R") 
new.y
```

## Dumping R Objects

Multiple objects can be deparsed at once using the dump function and read back in using source

```R
x <- "foo" 
y <- data.frame(a = 1L, b = "a")
# We can dump() R objects to a file by passing a character vector of their names.
dump(c("x", "y"), file = "data.R") 
rm(x, y)
# The inverse of dump() is source().
source("data.R") 
str(y) # Compactly displays structure of an arbitrary R object
x
```
