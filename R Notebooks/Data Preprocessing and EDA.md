
```{r}
install.packages("ggplot2")
library(ggplot2)
```
# Data Structure

# 1. Vectors

```{r}
# create a vector
age <- c(23, 14, 67, 4)
age
```


```{r}
print(age)
```


```{r}
# checks if variable is a vector
is.vector(age)
```


```{r}
# checks data length of variable
length(age)
```


```{r}
typeof(age)
```


```{r}
age <- c(age, 16)
age
```



```{r}
# creates a categorical vector using jane, john, jerry, james
names <- c("jane", "john", "jerry", "james")
names
```


```{r}
names<-c(names, "joy")
names
```


```{r}
names <- c(names, 1)
names
```


```{r}
names <- names[1:5]
names
```

# 2. Lists

```{r}
info <- list("Azhar", 25, 'EDS6436')
info
```


```{r}
typeof(info)
```


```{r}
info_vector <- unlist(info)
info_vector
```


```{r}
# Create a list from vectors
my_list <- list(Name = c('Azhar', 'Alisha'), Age = c(25, 23), Gender = c('M', 'F'))
my_list
```


```{r}
list_df <- as.data.frame(my_list)
list_df
```

# 3. Matrices
```{r}
my_matrix <- matrix(1:9, nrow = 3, ncol =3 )
my_matrix
```


```{r}
is.matrix(my_matrix)
```


```{r}
# Extract a specific element: To extract the element in the second row and third column:
element <- my_matrix[2, 3]
element
```


```{r}
# Extract a submatrix: To extract the top-left 2x2 submatrix:
submatrix <- my_matrix[1:2, 1:2]
submatrix
```

# 4. Arrays

```{r}
# Creating a 3x3x2 array
my_array <- array(1:18, dim = c(2, 3, 3))
# Print the array
print(my_array)

```


```{r}
# Extracting a specific element (2nd row, 3rd column, 2nd slice/matrix)
element <- my_array[2, 3, 2]
element
```


```{r}
# Flatten the array into a vector
flattened_array <- as.vector(my_array)
flattened_array
```

# 5. Factors

```{r}
# Creating a factor with levels
my_factor <- factor(c("low", "medium", "high", "medium", "low"))
my_factor
```


```{r}
# Print the levels of the factor
print(levels(my_factor))
```


```{r}
# Reorder levels of the factor
reordered_factor <- factor(my_factor, levels = c("high", "medium", "low"))
print(reordered_factor)
```


```{r}
# You can convert a factor to a character vector to work with it as text
char_vector <- as.character(my_factor)
print(char_vector)
```

# 6. DataFrames

```{r}
student <- data.frame(Student_Name = names, Age = age)
student
```


```{r}
# checks data dimension
dim(student)
```


```{r}
# counts the number of rows and columns
nrow(student)
```


```{r}
ncol(student)
```


```{r}
# Displays the first few rows of the dataset, the head() has a second parameter that accepts the number of rows to be displayed
head(student, 3)
```


```{r}
# Displays the last few rows of the dataset,
tail(student, 3)
```


```{r}
# To subset: [reference rows : reference columns]
student[1,2]

```
```{r}
# subset rows 1 and 2 of columns 1 and 2 of the dataset
student[1:2,1:2]
```
#Load data

```{r}
data('mtcars')
head(mtcars)
```
#iris

```{r}
dim(iris)
```

# In Class Hands on Work 2

```{r}
# Creating an empty DataFrame
gradebook <- data.frame(C1 = c(10, 15, 20, 25, 30,NA, 40),
                 C2 = c(25, 30, 35, 40, 45, 50, 55),
                 C3 = c('A','B','A',NA,'D','E','C'))

print(gradebook)
# Display the empty DataFrame

```


```{r}
# Description of the dataset
str(gradebook)
```


```{r}
# Checking for missing values
missing_values <- is.na(gradebook)
missing_values
```


```{r}
#Sum of null values in each row
rowSums(is.na(gradebook))
```


```{r}
#Accessing the required ROW
gradebook$C2
```


```{r}
# Replace null values
gradebook$C1[is.na(gradebook$C1)] <- 0

gradebook
```


```{r}
gradebook$C1[gradebook$C1 == 0] <- NA

gradebook
```

# Mean Imputation
```{r}
# Calculate the mean of the Age column excluding NA values
mean_C1 <- mean(gradebook$C1, na.rm = TRUE)

gradebook$C1[is.na(gradebook$C1)] <- mean_C1

gradebook
```
# Mode Imputation

```{r}
mode_C3 <- names(sort(table(gradebook$C3), decreasing = TRUE))[1]

gradebook$C3[is.na(gradebook$C3)] <- mode_C3

gradebook
```


```{r}
install.packages("psych")
library(psych)
```

# EDA
```{r}
boxplot(gradebook$C1, main = "Box Plot of C1", ylab = "C1" , col = "lightgreen")
```

# Take Home Assignment:

# Loading the dataset R_test_data.csv
```{r}
data <- read.csv("/Users/azharmadanisyed/Downloads/Data Mining/R_test_data.csv")
data
```


```{r}
# Removing the first unnecessary column
install.packages("dplyr")
library(dplyr)

data <- data %>% select(-X)
```


```{r}
data
```

# Let's perform data cleaning process
```{r}

# Dimension of the data
dim(data)
```

# Understanding more about the data
```{r}
# First five rows of the data
head(data)
```
# Summary of the data

```{r}
# Install and load the skimr package
install.packages("skimr")
library(skimr)
```


```{r}
# Use skim to summarize the data
skim(data)
```

# Checking for missing values
```{r}
# Check for missing values in the entire data frame
```


```{r}
data
```
# We can see there are missing values in almost all the columns, but they haven't been named anything (N/A), We can replace these values with NaN values, and then replace/impute of miising values depending on the number of missing values.
```{r}
sum(is.na(data))
```

```{r}
# Count missing values in each column
colSums(is.na(data))
```
# These values are misleading us, that there are no null values in the data, so first lets replace them with N/A.

```{r}
data[data == ""] <- NA
data
```


```{r}
sum(is.na(data))
```


```{r}
colSums(is.na(data))
```
# Now we got the correct number of missing values in the dataset.
# There are no missing values in the last three numerical columns...
# For numerical, only NrSiblings have the null values...we shall replace them with mean/median values.
# For Categorical, there are bunch of missing values..which we shall replace by mode or bfill/ffill values

```{r}
#Checking the structure of the data/datatypes
str(data)
```

```{r}
# No missing values here
sum(is.na(data$MathScore))
sum(is.na(data$ReadingScore))
sum(is.na(data$WritingScore))
```


```{r}

sum(is.na(data$NrSiblings))
```


```{r}
# Lets replace this using median imputation
data$NrSiblings[is.na(data$NrSiblings)] <- median(data$NrSiblings, na.rm = TRUE)
colSums(is.na(data))
```
# All the numerical columns have been imputed.
# Let's replace the categorical columns with the mode values.

```{r}
# Categorical columns
categorical_columns <- data %>% select_if(is.character)
categorical_columns
```


```{r}
# Step 1: Define a function to find the mode (most frequent value)
mode_function <- function(x) {
  ux <- unique(x)
  ux[which.max(tabulate(match(x, ux)))]
}
```


```{r}
# Step 2: Apply mode imputation to all selected categorical columns
# Loop through each column in the categorical data frame
for (col in names(categorical_columns)) {
  data[[col]][is.na(data[[col]])] <- mode_function(data[[col]])
}

# Step 3: Verify the changes
# Check to confirm that the missing values have been filled
colSums(is.na(data))
```
# Checking for the duplicate values

```{r}
sum(duplicated(data))
```


```{r}
# Removing duplicates
data <- data[!duplicated(data), ]
```


```{r}
# Verify that no duplicates remain
sum(duplicated(data))
```
# There was one duplicate value, we removed them.

# Checking for the outliers in the data.

# There are few outliers in all the features.
```{r}
# Use sapply to find columns with numeric data type
numeric_columns <- sapply(data, is.numeric)

# Loop through each numerical column and create boxplots
for (col in names(data)[numeric_columns]) {
    # Create a boxplot for each numerical column
    boxplot(data[[col]], main = paste("Boxplot for", col), ylab = col)
}
```

# Outlier detection in the numerical columns.


```{r}
# Define a function to identify and extract outliers based on the IQR method
get_outliers <- function(column_data) {
  # Calculate the first (Q1) and third (Q3) quartiles, and the interquartile range (IQR)
  Q1 <- quantile(column_data, 0.25, na.rm = TRUE)
  Q3 <- quantile(column_data, 0.75, na.rm = TRUE)
  IQR_value <- Q3 - Q1
  
  # Calculate the lower and upper bounds for outliers
  lower_bound <- Q1 - 1.5 * IQR_value
  upper_bound <- Q3 + 1.5 * IQR_value
  
  # Return the values that are outliers
  outliers <- column_data[column_data < lower_bound | column_data > upper_bound]
  return(outliers)
}

# Function to identify and display outliers for each numerical column in a dataset
identify_outliers <- function(data) {
  # Get the list of numerical columns in the data
  numerical_columns <- sapply(data, is.numeric)
  
  # Iterate through each numerical column and find outliers
  for (col_name in names(data)[numerical_columns]) {
    cat("Outliers for", col_name, ":\n")
    outliers <- get_outliers(data[[col_name]])
    
    # Display the outlier values, if any
    if (length(outliers) > 0) {
      print(outliers)
    } else {
      cat("No outliers found.\n")
    }
    cat("\n")  # Add a blank line for readability
  }
}

identify_outliers(data)
```

# Sublings can be 7, so I don't consider this as an outlier.
# There are different range of values in Mathscore, reading and writing, a person who did not study well has the chances of getting less values. So, these are also the correct values.

# Inspecting the categorical column values
```{r}
categorical_columns <- c("Gender", "EthnicGroup", "TestPrep", "TransportMeans", "LunchType", 
                         "ParentMaritalStatus", "PracticeSport", "IsFirstChild")
for (col in categorical_columns) {
    cat("Unique values in", col, ":\n")
    print(unique(data[[col]]))
    cat("\n")
}
```

# All the values look okay for me.

# Exploratory Data Analysis

# 1. Numerical Columns (Histograms)

# This plots gives us the picture of how well the data is distributed across the varaibles.
```{r}
# Plot histograms for all numerical columns
numeric_columns <- sapply(data, is.numeric)
for (col in names(data)[numeric_columns]) {
    hist(data[[col]], main = paste("Histogram of", col), xlab = col, col = "lightblue", breaks = 20)
}
```

# 2. Categorical Variables (Bar plots)

# It gives the count of each category for the variables.

```{r}
# Plot bar charts for categorical variables

for (col in categorical_columns) {
    barplot(table(data[[col]]), main = paste("Bar plot of", col), col ="blue")
}
```
# Correlation Matrix:

# Correlation Matrix helps is understanding whether there is any correlation (linear relationship) between the numerical variables.
```{r}
# Create a correlation matrix for numerical variables
cor_matrix <- cor(data[, numeric_columns], use = "complete.obs")
print(cor_matrix)

# Visualize the correlation matrix using a heatmap
heatmap(cor_matrix, main = "Correlation Heatmap", col = colorRampPalette(c("blue", "white", "red"))(20), scale = "none")
```

# Summary of the what I have done:

- Loaded the dataset in csv format.
- Checked the dimension, head and summary of the data.
- Checked if there are any missing values in the dataset and then removed them using median method for numerical variables and mode for the categorical variables.
- Checked if there are any duplicates in the data and then removed them.
- Checked the outliers and evaluated by checking them, I found them as the valid numbers, so decided not to drop them.
- Finally performed Exploratory data Analysis: Histograms, Barplots, and Correlation matrix.


# Saving Data Frame as CSV file

```{r}
write.csv(data, "/Users/azharmadanisyed/Downloads/Data Mining/R_test_data_cleaned.csv", row.names = FALSE)
```


```{r}
rmarkdown::render("Lab_2316906.rmd", output_format = "html_document")
```


# I got the cleaned R test data in the csv format.

