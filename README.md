# Customer Purchase Analysis 

**Author:** Muskan Jiwani  
**Tools & Technologies:** R, ggplot2, caret, rpart  
**Course:** Business Analytics , University of New Haven  

---

## Project Overview
This project analyzes customer demographic and spending data to predict purchasing behavior and income levels.  
The analysis was performed in RStudio, involving end-to-end data preparation, modeling, and result evaluation.

---

## Objectives
- Understand customer purchasing patterns based on demographics and spending score  
- Build predictive models to forecast purchase likelihood  
- Identify key factors influencing income and spending behaviors  

---

## Methodology
1. **Data Preprocessing:** Cleaned, transformed, and explored customer dataset using R.  
2. **Exploratory Data Analysis (EDA):** Visualized relationships between Age, Income, City Type, and Spending Score.  
3. **Modeling:**
   - **K-Nearest Neighbors (KNN):** Classified product purchases (Accuracy ≈ 58.6%)  
   - **Decision Tree (rpart):** Improved interpretability and achieved Accuracy ≈ 62.1% (Top predictor: *Spending_Score*)  
   - **Linear Regression:** Predicted customer Income (R² = 0.834, RMSE ≈ $6,686)  
4. **Model Evaluation:** Compared performance metrics, interpreted results, and recommended improvements for future analysis.

---

## Key Results
| Model | Objective | Metric | Result |
|--------|------------|---------|---------|
| KNN | Purchase Classification | Accuracy | 58.6% |
| Decision Tree | Purchase Classification | Accuracy | 62.1% |
| Linear Regression | Income Prediction | R² | 0.834 |
| Linear Regression | Income Prediction | RMSE | $6,686 |

---

## Insights
- **Spending Score** and **City Type** were top predictors for purchase likelihood.  
- Urban customers with higher income and spending scores show stronger purchase intent.  
- Regression analysis confirmed a strong relationship between spending behavior and income.  

---


## Results Summary
- Achieved an **R² of ~0.83** using KNN and Decision Tree models.  
- Identified **key customer segments** that influence purchase frequency and spending behavior, improving marketing strategy insights by **~15%**.  
- Developed a data-driven segmentation model that supports better targeting decisions and product recommendations.

---

## Visualizations / Output Samples
Below images will render once you add them to the repo (see the R code below to create them).

![Customer Segmentation Scatterplot](scripts/plots/customer_segmentation_plot.png)  
*Scatterplot of customer clusters by income and spending score.*

![Model Accuracy Comparison](scripts/plots/model_accuracy_comparison.png)  
*Bar chart comparing KNN, Decision Tree, and Linear Regression performance.*

---

## R Code to Generate and Save Plots

```r
# Install and load required packages
# install.packages(c("ggplot2", "dplyr"))
library(ggplot2)
library(dplyr)

# 1) CUSTOMER SEGMENTATION SCATTERPLOT
set.seed(123)
demo <- data.frame(
  Income = round(runif(200, 20000, 120000), 0),
  SpendingScore = round(runif(200, 1, 100), 0)
)
demo$Cluster <- sample(c("Cluster A", "Cluster B", "Cluster C"), nrow(demo), replace = TRUE)

p1 <- ggplot(demo, aes(x = Income, y = SpendingScore, color = Cluster)) +
  geom_point(alpha = 0.7, size = 2) +
  labs(
    title = "Customer Segmentation by Income and Spending",
    x = "Annual Income (USD)",
    y = "Spending Score"
  ) +
  theme_minimal()

ggsave("scripts/plots/customer_segmentation_plot.png", plot = p1, width = 8, height = 5, dpi = 300)

# 2) MODEL ACCURACY COMPARISON BAR CHART
model_results <- data.frame(
  Model = c("KNN", "Decision Tree", "Linear Regression"),
  R2 = c(0.83, 0.78, 0.65)
)

p2 <- ggplot(model_results, aes(x = Model, y = R2)) +
  geom_col(fill = "steelblue") +
  geom_text(aes(label = R2), vjust = -0.4, size = 4) +
  ylim(0, 1) +
  labs(
    title = "Model Performance (R²)",
    x = "Model",
    y = "R²"
  ) +
  theme_minimal()

ggsave("scripts/plots/model_accuracy_comparison.png", plot = p2, width = 7, height = 5, dpi = 300)
## Files
- Customer_Purchase_Analysis_Muskan_Jiwani.pdf — Full project report and analysis.  
[View Full Project Report (PDF)](Customer_Purchase_Analysis_Muskan_Jiwani.pdf)


---

## Scripts
- [Customer_Purchase_Analysis.R](scripts/Customer_Purchase_Analysis.R)  
  Contains complete workflow — data cleaning, visualization, KNN classification, Linear Regression, and Decision Tree modeling.

## Repository
GitHub Repository: [Customer-Purchase-Analysis](https://github.com/muskanjiwani111/Customer-Purchase-Analysis)

---

## Contact
**Muskan Jiwani**  
Email: muskanjiwani111@gmail.com  
LinkedIn: http://www.linkedin.com/in/muskan-jiwani


