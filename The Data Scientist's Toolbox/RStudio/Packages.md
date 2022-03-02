## R Packages
- Install from Cran repository
	`install.packages("ggplot2")`

- Install from Bioconductor
	```R
	source("https://bioconductor.org/biocLite.R")
	biocLite()
	biocLite("GenomicFeatures")
	```
	
- Install from GitHub
```R
	install.packages("devtools")
	library(devtools)
	install_github("author/package")
```

- Load a package
    `library()`
	`library(ggplot2)`
	
- What packages are installed?
	`installed.packages()` or `library(ggplot2)`

	==Note: No double quotes while loading packages== 

- Upadating packages
	`old.packages()`
	`update.packages()`
	`install.packages("packagename")`

- Unloading a package in the middle of a script due to conflicting packages
	`detach()`
	`detach("package:ggplot2", unload=TRUE)`

- Removing packages
	`remove.packages("ggplot2")`

**Important command: `sessionInfo()` - useful for posting to forums**

Help for package functions
`help(package = "ggplot2")`

Package vignettes - clear instructions on how to use included functions
`browseVignettes("ggplot2")`

	
