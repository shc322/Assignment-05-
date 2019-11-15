# Assignment-05-

rm(list=ls(all=TRUE))
cat("\014") 

getwd()

file.edit(".gitignore")

ptm <- proc.time()
DF <- read.csv("UNRATE.csv")
CSV_READ_TIME <- (proc.time() - ptm)
CSV_READ_TIME


class(DF)
typeof(DF)
str(DF)

if (!require("data.table")) install.packages("data.table")
library("data.table")

#Checking and setting number of cpu threads
getDTthreads()
getDTthreads(verbose=TRUE)
setDTthreads(0)
getDTthreads()

ptm <- proc.time()
DF <- fread("UNRATE.csv", header="auto", 
            data.table=FALSE)
FREAD_READ_TIME <- (proc.time() - ptm)
FREAD_READ_TIME

class(DF)
typeof(DF)
str(DF)
names(DF)

ptm <- proc.time()
header <- read.table("UNRATE.csv", header = TRUE,
                     sep=",", nrow = 1)
DF <- fread("UNRATE.csv", skip=1, sep=",",
                  header=FALSE, data.table=FALSE)
setnames(DF, colnames(header))
rm(header)
FREAD_READ_TIME <- (proc.time() - ptm)
FREAD_READ_TIME
