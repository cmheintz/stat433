
# title: '433 Homework 1'
# author: "Carleigh Heintz"
# due date: "2/5/2021"

library(stringr)

x = readLines("https://guide.wisc.edu/faculty/")
ind <- grep("<br/></p></li><li><p>",x)
# each index represents a letter of the alphabet of staff memebers
data <- x[ind]
for (i in 1:length(data)) {
  data[i] <- str_split(data[i],"<p>") # split faculty members
  data[[i]] <- data[[i]][-1] # first element is html code, can be discarded
}

faculty <- data.frame(matrix(ncol = 4, nrow = 0))
for (i in 1:length(data)) {
  for (j in 1:length(data[[i]])) {
    temp <- unlist(str_split(data[[i]][j], "<br/>"))
    temp.df <- data.frame(temp[1],temp[2],temp[3],temp[4])
    faculty <- rbind(faculty, temp.df)
  }
}
cols <- c("name", "position", "department","degree information")
colnames(faculty) <- cols
# str(faculty)


