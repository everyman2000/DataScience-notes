# Connection interfaces

Data are read in using connection interfaces. Connections can be made to files (most common) or to other more exotic things. 
• file, opens a connection to a file 
• gzfile, opens a connection to a file compressed with gzip 
• bzfile, opens a connection to a file compressed with bzip2 
• url, opens a connection to a webpage

## File connections
Connections to text files can be created with the file() function.

```R
> str(file) 
  function (description = "", open = "", blocking = TRUE, encoding = 
  getOption("encoding"), raw = FALSE, method = getOption("url.method", "default"))
```

- `description` is the name of the file
- `open` is for code indicating
	- "r" read only 
	- "w" writing (and initializing a new file)
	- "a" appending
	- "rb", "wb", "ab" reading, writing or appending in binary mode (Windows)

## Connections
In practice, we often don’t need to deal with the connection interface directly as many functions for reading and writing data just deal with it in the background.

```R
 ## Create a connection to 'foo.txt' 
con <- file("foo.txt") 
## Open connection to 'foo.txt' in read-only mode 
open(con, "r") 
## Read from the connection 
data <- read.csv(con) 
## Close the connection 
close(con)
```

is the same as

```R
data <- read.csv("foo.txt")
```

==However connections can be useful for reading parts of a file, as illustrated below.==

### Reading Lines of a Text File
```R
## Open connection to gz-compressed text file 
con <- gzfile("words.gz") 
x <- readLines(con, 10) 
x
```

`writeLines` takes a character vector and writes each element one line at a time to a text file. Each element of the character vector becomes a line.

### Reading from a URL connection

```R
## Open a URL connection for reading 
con <- url("http://www.jhsph.edu", "r") 
## Read the web page 
x <- readLines(con) 
## Print out the first few lines 
head(x)
```
