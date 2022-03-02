## What is R? 
This is an easy question to answer. R is a dialect of S. 

## What is S? 
- S is a language that was developed by John Chambers and others at the old Bell Telephone Laboratories, originally part of AT&T Corp. 
- S was initiated in 1976 as an internal statistical analysis environment—originally implemented as Fortran libraries. 
- Early versions of the language did not even contain functions for statistical modeling. 
- In 1988 the system was rewritten in C and began to resemble the system that we have today (this was Version 3 of the language). The book Statistical Models in S by Chambers and Hastie (the white book) documents the statistical analysis functionality. 
- Version 4 of the S language was released in 1998 and is the version we use today. The book Programming with Data by John Chambers (the green book) documents this version of the language.

## The S Philosophy
In "Stages in the Evolution of S", John Chambers writes: “We wanted users to be able to begin in an interactive environment, where they did not consciously think of themselves as programming. Then as their needs became clearer and their sophistication increased, they should be able to slide gradually into programming, when the language and system aspects would become more important.”

## Back to R
- In 1991, R was created by Ross Ihaka and Robert Gentleman in the Department of Statistics at the University of Auckland. In 1993 the first announcement of R was made to the public. Ross’s and Robert’s experience developing R is documented in a 1996 paper in the Journal of Computational and Graphical Statistics.
- In 1995, Martin Mächler made an important contribution by convincing Ross and Robert to use the GNU General Public License⁴ to make R free software. This was critical because it allowed for the source code for the entire R system to be accessible to anyone who wanted to tinker with it (more on free software later).

## Features of R
- Lean software and modular packages
- Sophisticated graphics capabilities
- Interactive + powerful
- Active user community (R-help and Stack Overflow)
- Free Software! 
	- Freedom to run for any purpose
	- Access to source code
	- Freedom to redistribute
	- Freedom to release improvement to public

## Drawbacks of R
- 40 year old technology
- Minimal built-in support for dynamic graphics
- Functionality based on consumer demand and user contributions
- Objects must be generally stored in physical memory, but there have been advancements
- Not ideal for all possible situations

## Design of R System
- Base R system from CRAN
- Everything else. 4000 user-contributed packages on CRAN.
- Bioconductor project
- Personal packages