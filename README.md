# Assignment-05-
############################################################
# R script to accompany Intro to R for Business, Chapter 5 #
# Written by Troy Adair                                    #
############################################################

## Going to be reading in a lot of data, so let's empty Environment
## and clean up Console
# Clean Up 
rm(list=ls(all=TRUE))
cat("\014") 

## Reading in external data
## Prior to attempting this section, download file
## "UNRATE.csv" from the link on intro-to-r.com
## and store it in working directory for this project.
getwd()


# Also, edit the .gitignore file (if necessary) to exclude
# *.csv and *.RData files from being synced by Git. 
file.edit(".gitignore")

# Importing the file and measuring how long the import takes
### Run as a block of text to time #########
ptm <- proc.time()
DF <- read.csv("UNRATE.csv")
CSV_READ_TIME <- (proc.time() - ptm)
CSV_READ_TIME
############################################

# Looking at what we got
class(DF)
typeof(DF)
str(DF)


## Reading in our csv file using fread() from package data.table 
# Installing data.table (if required) and loading it into memory
if (!require("data.table")) install.packages("data.table")
library("data.table")

#Checking and setting number of cpu threads
getDTthreads()
getDTthreads(verbose=TRUE)
setDTthreads(0)
getDTthreads()

# Doing a timed read of the same file with fread()
### Run as a block of text to time #########
ptm <- proc.time()
DF <- fread("UNRATE.csv", header="auto", 
            data.table=FALSE)
FREAD_READ_TIME <- (proc.time() - ptm)
FREAD_READ_TIME
############################################

# Examining what we got
class(DF)
typeof(DF)
str(DF)
names(DF)

# Bringing in column headers as names and using them to set names
### Run as a block of text to time #########
ptm <- proc.time()
header <- read.table("UNRATE.csv", header = TRUE,
                     sep=",", nrow = 1)
DF <- fread("UNRATE.csv", skip=1, sep=",",
                  header=FALSE, data.table=FALSE)
setnames(DF, colnames(header))
rm(header)
FREAD_READ_TIME <- (proc.time() - ptm)
FREAD_READ_TIME