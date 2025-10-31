library(readr)
data <- read_csv("BANL 6625_Final_Exam_Dataset.csv")
View(data)

# Load necessary libraries
library(dplyr)
library(ggplot2)

# Display structure and data types
str(data)


head(data)

variable_types <- data %>%
  summarise_all(class) %>%
  t() %>%
  as.data.frame() %>%
  rename(Type = V1)

print(variable_types)

# Distinguish between numerical and categorical
numerical_vars <- names(data)[sapply(data, is.numeric)]
categorical_vars <- names(data)[sapply(data, function(x) is.character(x) || is.factor(x))]

cat("Numerical Variables:", paste(numerical_vars, collapse = ", "), "\n")
cat("Categorical Variables:", paste(categorical_vars, collapse = ", "), "\n")

# Generate summary statistics
summary(data)

# Select numerical variables
numerical_data <- data %>% select_if(is.numeric)

numerical_summary <- data.frame(
  Variable = colnames(numerical_data),
  Mean = sapply(numerical_data, function(x) round(mean(x, na.rm = TRUE), 2)),
  Median = sapply(numerical_data, function(x) round(median(x, na.rm = TRUE), 2)),
  SD = sapply(numerical_data, function(x) round(sd(x, na.rm = TRUE), 2)),
  Min = sapply(numerical_data, function(x) round(min(x, na.rm = TRUE), 2)),
  Max = sapply(numerical_data, function(x) round(max(x, na.rm = TRUE), 2))
)

# Print the summary table
print("Summary Statistics for Numerical Variables:")
print(numerical_summary)

# Identify missing values
colSums(is.na(data))

# Handle missing values in numerical columns by replacing them with the median
data$Age[is.na(data$Age)] <- median(data$Age, na.rm = TRUE)
data$Income[is.na(data$Income)] <- median(data$Income, na.rm = TRUE)
data$Spending_Score[is.na(data$Spending_Score)] <- median(data$Spending_Score, na.rm = TRUE)

# Handle missing values in categorical columns by replacing them with "Unknown"
data$City_Type[is.na(data$City_Type)] <- "Unknown"
data$Education_Level[is.na(data$Education_Level)] <- "Unknown"

# Confirm no missing values remain
missing_values_after <- colSums(is.na(data))
print("Missing Values After Handling:")
print(missing_values_after)



2.

# Histogram of Age
ggplot(data, aes(x = Age)) +
  geom_histogram(binwidth = 5, fill = "blue", color = "black") +
  labs(title = "Age Distribution", x = "Age", y = "Frequency")

ggplot(data, aes(x = City_Type, y = Income)) +
  geom_boxplot(fill = "lightblue") +
  labs(title = "Income Distribution by City Type", x = "City Type", y = "Income")

3.

# Convert categorical variables to numeric encoding (if needed for KNN)
data$City_Type <- as.numeric(as.factor(data$City_Type)) # Encode City_Type as numeric
data$Product_Purchase <- as.factor(data$Product_Purchase) # Ensure target is a factor

# Check for missing values
colSums(is.na(data))

# Remove rows with missing values (if any remain)
data <- na.omit(data)

# Split into training and testing sets
set.seed(123)
index <- createDataPartition(data$Product_Purchase, p = 0.7, list = FALSE)
train <- data[index, ]
test <- data[-index, ]

# Scale numerical predictors in training and test sets
train[, c("Age", "Income", "Spending_Score")] <- scale(train[, c("Age", "Income", "Spending_Score")])
test[, c("Age", "Income", "Spending_Score")] <- scale(test[, c("Age", "Income", "Spending_Score")])


# Load necessary library
library(class)

# Set the value of k
k <- 5

# Apply KNN
knn_pred <- knn(
  train = train[, c("Age", "Income", "Spending_Score", "City_Type")], 
  test = test[, c("Age", "Income", "Spending_Score", "City_Type")], 
  cl = train$Product_Purchase, 
  k = k
)

print(knn_pred)

# Evaluate the performance
library(caret)

# Create confusion matrix
conf_matrix <- confusionMatrix(knn_pred, test$Product_Purchase)
print(conf_matrix)

print(conf_matrix$overall["Accuracy"])

results <- data.frame(
  Actual = test$Product_Purchase,
  Predicted = knn_pred
)
print(head(results))  # First few rows of the comparison


4.

# Linear regression model
lm_model <- lm(Income ~ Age + Spending_Score + City_Type, data = data)

# Summary of the model
summary(lm_model)

# R-squared value
cat("R-squared:", summary(lm_model)$r.squared)

# Evaluate with Mean Squared Error
predicted_income <- predict(lm_model, data)
MSE <- mean((data$Income - predicted_income)^2)
cat("Mean Squared Error:", MSE)

5.

# Load required libraries
library(rpart)
library(rpart.plot)

# Build the classification tree
tree_model <- rpart(Product_Purchase ~ ., data = train, method = "class")

# Plot the tree with better visualization
rpart.plot(tree_model, type = 2, extra = 104, fallen.leaves = TRUE, cex = 0.8, 
           main = "Classification Tree for Product_Purchase")

# View the summary of the tree
summary(tree_model)


# Predict on test set
tree_pred <- predict(tree_model, newdata = test, type = "class")

# Confusion Matrix
conf_matrix_tree <- confusionMatrix(tree_pred, test$Product_Purchase)
print(conf_matrix_tree)



6.
cat("Summary of Workflow:\n")
cat("1. Loaded the data and handled missing values.\n")
cat("2. Explored data with visualizations showing distribution and trends.\n")
cat("3. Built a KNN model (Accuracy:", conf_matrix$overall["Accuracy"], ").\n")
cat("4. Developed a linear regression model (R-squared:", summary(lm_model)$r.squared, ").\n")
cat("5. Created a classification tree and identified key decision splits.\n")
cat("Actionable Insights:\n")
cat("1. Age and Spending Score are significant predictors of Income.\n")
cat("2. City Type plays a crucial role in Product Purchase prediction.\n")
cat("Recommendations:\n")
cat("Focus marketing strategies based on Spending Score and City Type to maximize purchases.\n")

   
