This page provides codes to enhance the efficency during an data analysis: 



## Normal Distribution 

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
### Ooutcome: 

![image](https://github.com/user-attachments/assets/8892a51f-4fa8-4d27-af0c-a200b3e198ef)
