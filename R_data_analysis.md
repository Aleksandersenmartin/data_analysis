This page provides codes to enhance the efficency during an data analysis: 



# Normal Distribution 

````R
#Calculating and creating a histogram as a normal distribution for the Cholestrol of the survey 
age_mean <- mean(df$age, na.rm = TRUE) #Calculating the mean
age_sd <- sd(df$age, na.rm = TRUE) #Calculating the standard deviation

# Calculate bin width based on the range of data divided by bins
bin_width <- (max(df$age, na.rm = TRUE) - min(df$age, na.rm = TRUE)) / 50  

# Plot with histogram and normal curve overlay
ggplot(data = df, aes(x = age)) +
  geom_histogram(color = "grey", fill = "tomato", bins = 50, aes(y = ..density..)) +  # Use density for y to align with normal curve
  stat_function(
    fun = dnorm,
    args = list(mean = age_mean, sd = age_sd),
    color = "blue",
    size = 1
  ) +
  labs(
    title = "Age by Frequency",
    x = "Age",
    y = "Density"
  ) +
  theme_minimal() +
  theme(
    plot.title = element_text(hjust = 0.5, size = 16, face = "bold"),
    axis.title = element_text(size = 12),
    axis.text.x = element_text(size = 10),
    legend.position = "
none"
````
### Outcome: 

![image](https://github.com/user-attachments/assets/8892a51f-4fa8-4d27-af0c-a200b3e198ef)

# Corelation and heatmaps: 

````r
Corelation:
co <- colorRampPalette(c("red", "yellow", "darkgreen"))
corr_male[is.na(corr_male)] <- 0  # Replace NA with 0
corr_male[is.nan(corr_male)] <- 0  # Replace NaN with 0
corr_male[is.infinite(corr_male)] <- 0 
````
````r
Heatmap: 
heatmap_male<- 
  heatmap.2(corr_male, 
          trace = "none", #Aviding the measure in the plot
          dendrogram = "none", #Avoding much mess in the measure between the col
          notecex  = 2.0,
          col=co, #Defining the color         
          margins = c(6.0,5.0), #Defining the wide of the plot 
          Rowv = TRUE,
          Colv = FALSE,
          key = TRUE, #allow us to get the ledger color to be 
          key.par = list(
            mar = c(5, 1, 2, 2), 
            las = 1),#To get the values in the value bar vertical and not horizontal 
          srtCol = 45, #get the x labs to 45 degrees  
          key.title = "Corelation", #the key title for measuring the values 
          density.info = c("none"),
          cexRow = 1.5, #The row font size 
          cexCol =1.5, #The column font size 
          main = "Heart Disease Corelation Matrix - Male" #The Title Name 
          )

````

### Outcome: 

![image](https://github.com/user-attachments/assets/91411e59-4bf5-42d8-9699-057c3ad0a2bb)


# Linear Regression 

# Generalized Linear Regression 

# Logistic Regression 

# Confusion Matrix 

When to use a confusion Matrix

A confusion Matrix is used when evaluating the performance of a classification model, especially for binary or multiclass classification takes. It provides a detailed breakdown of the model's predictions compared to the actual outcomes, rather than a single metric like accuracy. 

Use Cases: 

1. Binary Classification :
		a. Example: span detection (spam/not spam)
2. Multiclass classification 
		a. Examples :image recognition (cat/dog/bird), sentiment analysis ( positive/neutral/negative) 

Why use it: 
	- Detailed insight: it shows counts of true positives, true negatives, false positives, and false negatives, helping identify specific error made by the model. 
	- Metric Calculation: Metrics like precision, recall, F1-Score, and accuracy are derived from the confusion matrix 
	- Handling imbalanced data: useful when one class significantly outweight the other, where accuracy alone might be mislead 

Structure of a Confusion Matrix: 

For binary classification 

Predicted: Positive	Predicted: Negative
Actual: Positive	True Positives (TP)	False Negatives (FN)
Actual: Negative 	False Positve (FP)	True Negative (TN) 

Advantages of a confusion Matrix

1. Clarity: 
		a. Provides a granular view of model performance across classes 
2. Error Analysis: 
		a. Helps pinpoint where the model is failing (e.g., high false positives ro false negatives)
3. Metrics Calculation:
		a. Enables compution of various performance metrics tailored to the task

 ````r
		set.seed(4000)
		index <- sample(1:nrow(df_log), size = 0.7 * nrow(df_log)) #70% for the training 
		training_set <- df_log[index, ]
		testing_set <- df_log[-index, ]
	
		actual_classes <- df_log$exang 
		conf_matrix <- table(predict_ = predicted_classes, actual = actual_classes )
		
		print(conf_matrix)
		
		accuracy <- sum(diag(conf_matrix)) / sum(conf_matrix)
		
		# Precision
		precision <- conf_matrix[2, 2] / sum(conf_matrix[2, ])
		
		# Recall
		recall <- conf_matrix[2, 2] / sum(conf_matrix[, 2])
		
		# F1 Score
		f1_score <- 2 * (precision * recall) / (precision + recall)
		
		# Display metrics
		cat("Accuracy:", accuracy, "\n")
		cat("Precision:", precision, "\n")
		cat("Recall:", recall, "\n")
		cat("F1 Score:", f1_score, "\n")
		
````

