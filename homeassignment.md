# HomeAssignment 1
````python
#%%
import pandas as pd 
#%%
import numpy as np 
#%%
import matplotlib.pyplot as plt 
# %%
import seaborn as sb 
# %%
df = pd.read_csv("Documentation/Iris.csv")
# %%
df
#%%
last_digits = 25
# %%
df =df.iloc[last_digits:,]
# %%
df
# %%
df.describe()
# %%
#Aggregate function based on which columns and which function needed 
stat_df = df.agg({  
    "SepalLength": ["mean", "median", "std"], 
    "SepalWidth" : ["mean", "median", "std"]
})

# %%
stat_df
# %%
plt.hist(df["SepalLength"],bins = 5,  color= "blue",) #Make the histogram for SepalLength
plt.title("Histogram of Sepal Length") #Main title 
plt.xlabel("Sepal Length") #X-label text
plt.ylabel("Frequency") #Y-label text 
plt.show
# %%
plt.hist(df["SepalWidth"],bins = 5,  color= "red",) #Make the histogram for SepalWidth
plt.title("Histogram of Sepal Width")#Main Title
plt.xlabel("Sepal Width") #X-label text 
plt.ylabel("Frequency") #y-label text
plt.show
# %%
x = df["Species"]
y = df["PetalLength"]
# %%
sb.boxplot(x = "Species", y="PetalLength", data = df, palette={'Iris-setosa': 'red', 'Iris-versicolor': 'blue', 'Iris-virginica': 'green'})
plt.title = "Petal Length for different Species"
plt.xlabel = "species"
plt.ylabel = "Petal Length"
plt.show()


# %%
plt.figure(figsize=(8, 6))  # Set the figure size
plt.scatter(df['PetalLength'], df['PetalWidth'], color='blue', label='Petal Width')  # Blue points

# add another series in red, similar to the image
plt.scatter(df['PetalLength'], df['PetalWidth']+0.1, color='red', label='Petal Length')  # Red points

# Add title and labels
plt.title('Scatter Plot Petal Length vs Petal Width', fontsize=16, fontweight='bold')
plt.xlabel('Petal Length', fontsize=14)
plt.ylabel('Petal Width', fontsize=14)

# Add legend
plt.legend(loc='best')

# Show plot
plt.show()
# %%

````
![boxplot_petallength_species](https://github.com/user-attachments/assets/1ee167d1-0944-4698-8090-535540e5a479)
![Histogram_sepallength](https://github.com/user-attachments/assets/c158a76f-af7f-46e3-9320-e6e61836feb2)
![Histogram_sepalWidth](https://github.com/user-attachments/assets/cd65861a-eee2-4767-bdc6-b978f9eb4c81)
![scatter with both](https://github.com/user-attachments/assets/70751547-38af-4a7a-b4c4-8fe207a8608d)
![Scatter_petal Length and Width](https://github.com/user-attachments/assets/3d9155ee-f1c8-47a8-985a-ca5cabf67ef8)


````r
library('tidyverse')
library('ggplot2')
library('viridis')
library('viridisLite')

student_data <- read.csv("student_data_exam.csv", header = TRUE, sep =";")
stud_data <- read.csv("student_data_exam.csv", header = TRUE, sep =";")

student_data$Education[student_data$Education =='some college'] <- 'college'

student_data$Education[student_data$Education == "master's degree"] <- "college"

student_data$Education[student_data$Education == "bachelor's degree"] <- "college"

student_data$Education[student_data$Education == "bachelor's degree"] <- "college"

student_data$Education[student_data$Education == "associate's degree"] <- "college"

student_data$Education[student_data$Education =='some high school'] <- 'high school'

student_data$Lunch[student_data$Lunch == 'free/reduced'] <- 'reduced'

student_data$Gender <- as.factor(student_data$Gender) #Converting the Gender variable into a factor for analytical purposes. 1 = Female, 2 = Male 

student_data$Ethnicity <- as.factor(student_data$Ethnicity) #Converting the Ethnicity into a facrot for Analytical purposes for the further analysis. 

student_data$TestPreparation <- as.factor(student_data$TestPreparation) #Converting the TestPreparation into factor for Analytical purposes 2 = Complete, 1 = None 

student_data$Education <- as.factor(student_data$Education)

student_data$Lunch <- as.factor(student_data$Lunch)

options(max.print=999999)

print(is.na(student_data)) #Checking the dataset to be without any N/A

summary(student_data)


#Section 2: data visiualization and summary tables:
#I)
student_data %>%
  ggplot(aes(x = TestPreparation, y = Math, fill = TestPreparation)) +
  geom_boxplot() +
  scale_fill_viridis(discrete = TRUE, alpha = 0.6) +
  geom_jitter(color = "black", size = 0.4, alpha = 0.5) +
  theme_minimal() +  # Use a minimal ggplot2 theme
  theme(
    legend.position = "none",
    plot.title = element_text(size = 11),
    axis.text.x = element_text(angle = 45, hjust = 1)  # Rotate x-axis labels if needed
  ) +
  ggtitle("Math Reusults compared with Test Preparations") +
  xlab("Test Preparations") +
  ylab("Math Results")


#II)
#Histogram of Math scores compared with ethnicity 
ggplot(student_data, aes(x = Math, fill = Ethnicity)) +
  geom_histogram(binwidth = 7, position = "dodge", color = "black") +  # Use position = "dodge" to separate bins by Ethnicity
  labs(
    title = "Histogram of Math Scores by Ethnicity",
    x = "Math Score",
    y = "Frequency"
  ) +
  theme_minimal() +
  theme(
    plot.title = element_text(hjust = 0.5, face = "bold", size = 14),
    axis.title = element_text(size = 12)
  )

#Histogram of Reading Scores compared with Ethnicity
ggplot(student_data, aes(x = Reading, fill = Ethnicity)) +
  geom_histogram(binwidth = 7, position = "dodge", color = "black") +  # Use position = "dodge" to separate bins by Ethnicity
  labs(
    title = "Histogram of Reading Scores by Ethnicity",
    x = "Reading Scores",
    y = "Fre                                                                                                                                                                                                                                                                                                                    quency"
  ) +
  theme_minimal() +
  theme(
    plot.title = element_text(hjust = 0.5, face = "bold", size = 14),
    axis.title = element_text(size = 12)
  )

#Histogram of Writing Scores compared with Ethnicity
ggplot(student_data, aes(x = Writing, fill = Ethnicity)) +
  geom_histogram(binwidth = 7, position = "dodge", color = "black") +  # Use position = "dodge" to separate bins by Ethnicity
  labs(
    title = "Histogram of Writing Scores by Ethnicity",
    x = " Writing Score",
    y = "Frequency"
  ) +
  theme_minimal() +
  theme(
    plot.title = element_text(hjust = 0.5, face = "bold", size = 14),
    axis.title = element_text(size = 12)
  )

#Section 3: Data modelling and Logistic Regression. 

stud_data$Gender[stud_data$Gender == 'male'] <- 1
stud_data$Gender[stud_data$Gender == 'female'] <- 0
stud_data$TestPreparation[stud_data$TestPreparation == 'none'] <- 0
stud_data$TestPreparation[stud_data$TestPreparation == 'completed'] <- 1
stud_data$Education[stud_data$Education =='some college'] <- 'college'
stud_data$Education[stud_data$Education == "master's degree"] <- "college"
stud_data$Education[stud_data$Education == "bachelor's degree"] <- "college"
stud_data$Education[stud_data$Education == "bachelor's degree"] <- "college"
stud_data$Education[stud_data$Education == "associate's degree"] <- "college"
stud_data$Education[stud_data$Education =='some high school'] <- 'high school'
stud_data$Lunch[stud_data$Lunch == 'free/reduced'] <- 'reduced'
````
### Outcome: 
![Histogram_sepalwidth](https://github.com/user-attachments/assets/12050ccd-f947-4aca-8ab6-d5842505d0ae)

![Historgram_sepallength](https://github.com/user-attachments/assets/06f9a939-62b6-47fb-b73a-900907003086)

![Boxplot on PetalLength cs Species](https://github.com/user-attachments/assets/7d07dfc8-b7ed-4df7-8b92-db233c69e3e8)

![Scatterplot_petal_length_width](https://github.com/user-attachments/assets/ac0c1896-4c89-4840-b3b5-c2da9131fafd)

# HomeAssignment 2
````python
#Section 1.1: Loading and Examining the Dataset.
#%%
import pandas as pd #importing pandas to 
# %%
import matplotlib.pyplot as plt
# %%
import numpy as np 

#%%
df =  pd.read_csv("titanic.csv") #Importing the CSV file to the function

#%%
def load_and_describe_data(): #Defining the function
    df_adj = df.iloc[0:10] #using the iloc function to get the 10 first row from the dataset
    summary = df.describe() #using the describe function to create a summary with basic statistics 
    return df_adj, summary #end the function with returning the variables. 
df_adj, summary = load_and_describe_data()
print('_'*60)
print(df_adj)
print('_'*60)
print(summary)
print('_'*60)
# %%
load_and_describe_data() #calling the function who describe the results.

#%%
#Section 1.2: Analyzing Categorical Data
# Define a function to analyze categorical data, including missing values and basic statistics
def analyze_categorical_data(df, column_name):
    # Calculate basic statistics
    total = len(df[column_name])
    missing = df[column_name].isnull().sum()  # creating a variable for number of missing values
    count = df[column_name].count()  # creating a variable for number of non-missing values
    unique = df[column_name].nunique()  # creating a variable for number of unique values
    mode_value = df[column_name].mode()[0]  # Most frequent value
    mode_frequency = df[column_name].value_counts().iloc[0]  # Frequency of the mode
    
    # Create a summary dataframe
    stats_df = pd.DataFrame({
        'Total': [total],
        'Missing': [missing],
        'Non-Missing': [count],
        'Unique': [unique],
        'Mode': [mode_value],
        'Mode Frequency': [mode_frequency]
    })
    
    return stats_df  # Return the summary dataframe

# List of categorical columns you want to analyze
categorical_columns = ['Sex', 'Embarked', 'Pclass']

# Analyze and plot frequencies for each categorical column
for column in categorical_columns:
    stats_df = analyze_categorical_data(df, column)  # Get the statistical summary dataframe
    
    # Print the summary dataframe
    print('-'*60)
    print(f"Statistical summary for column '{column}':")
    print('-'*60)
    print(stats_df)
    print('-'*60)
    print("\n")  # Add a newline for readability
    
    # Plotting the bar chart
    freq = df[column].value_counts(dropna=False)  # Include missing values in the frequency count
    plt.figure(figsize=(8, 6))
    plt.bar(freq.index.astype(str), freq.values)  # Convert the index to string to handle NaN
    
    # Adding titles and labels
    plt.title(f"Frequency for column {column}")
    plt.xlabel(column)
    plt.ylabel("Frequency")
    
    # Show the plot
    plt.show()
# %%

#%%
#Section 1.3: Survival Rate Calculation by Feature 
#Defining the survival rate based on the columns 
def calculate_survival_rate(df, feature):
    categories = df[feature].astype(str).unique()
    print('-'*60)
    print(f'Survival rates by {feature}:') 
    print('-'*60)

    for category in categories: #Creating the for-loop to go strategic through the dataset 
        total_count = len(df[df[feature].astype(str)==category]) #Creating the variable for the total of each category.
        survived_count = len(df[(df[feature].astype(str) == category) & (df['Survived'] == 1)]) #Creating the variable that counting the survivals 

        if total_count > 0:#Establish an logic if statment to count if the condition of survival is 1 ( true ) or 0 (false) so we can create a percentage
            survival_rate = (survived_count/total_count) * 100
        else: 
            survival_rate = 0

    
        print(f' {category}: {survival_rate:.2f}% survival rate') #printing the outcome from the function
    

calculate_survival_rate(df, 'Sex')
calculate_survival_rate(df, 'Embarked')
calculate_survival_rate(df, 'Pclass')



#%%
#Section 2.1: Visualizing relationships betwwen features
def plot_relationship(df, x, y, hue): #Defining the function for scatterplots 
    if x in df.columns and y in df.columns and hue in df.columns:

        unique_categories = df[hue].unique() #Extracting unique values in the cateogires for the hue columns
        colors = ['blue', 'red', 'orange', 'purple', 'pink', 'gray', 'orange', 'olive', 'cyan'] # Defining which colors that is selecte for each variabel 

        #Creating the scatter plots conditions and effects 
        plt.figure(figsize=(8, 6))
        for idx, category in enumerate(unique_categories):
            subset = df[df[hue] == category] #filtering the df for each category 
            plt.scatter(subset[x], subset[y], color=colors[idx & len(colors)], label=str(category), edgecolor = 'black')
        
        plt.title(f'Relationship between {x}, {y}, and {hue}') #Creating the top tittle for the chart
        plt.xlabel(x)
        plt.ylabel(y)

        plt.legend(title=hue) #Creating the legend to get the scatter more readable 
        plt.show()
    else: 
        print(f'Invalid columns provider for x={x}, y={y} or hue={hue}')
plot_relationship(df, 'Age', 'Fare', 'Survived')

#%%
# Section 2.2.: Analyzing Survival Rates by Different Features: 
# Create age groups using pandas cut function
age_bins = [0, 10, 20, 30, 40, 50, 60, 70, 80, 90]  # Define the age intervals with a variable from 0 to 90 
age_labels = ['0-10', '11-20', '21-30', '31-40', '41-50', '51-60', '61-70', '71-80', '81-90']   # creating a variable dat set the age intervals to labels
df['AgeGroup'] = pd.cut(df['Age'], bins=age_bins, labels=age_labels, right=False)  # Assign age groups to a new column, AgeGroup

# Calculating survival rate for each age group
survival_rate_by_age_group = df.groupby('AgeGroup')['Survived'].mean() * 100  # Survival rate in percentages
total_passengers_by_age_group = df['AgeGroup'].value_counts(sort=False)  # Total passengers in each age group
survivors_by_age_group = df[df['Survived'] == 1]['AgeGroup'].value_counts(sort=False)  # Survivors in each age group

# Creating the Plot a pie chart
plt.figure(figsize=(8, 6))

plt.pie(survivors_by_age_group, autopct='%1.1f%%', pctdistance=1.1 , labeldistance=.2, colors=plt.cm.Paired.colors) #The pie chart 
plt.title('Survival Rates by Age Group')
plt.axis('equal')  # Ensure the pie chart is a circle
plt.legend(age_labels)
plt.show()

# Display survival rates for each age group
print("Survival rates by age group:")
for age_group, rate in survival_rate_by_age_group.items(): #To get the value to percentage
    print(f'{age_group}: {rate:.2f}%')

# analysis
highest_survival_rate_group = survival_rate_by_age_group.idxmax()
lowest_survival_rate_group = survival_rate_by_age_group.idxmin()

print(f"\nThe age group with the highest survival rate is: {highest_survival_rate_group}")
print(f"The age group with the lowest survival rate is: {lowest_survival_rate_group}")

# %%
#Section 2.3: How does family size affect the likelihood of survival? 
df.head() #To find out of all the columns for the next section. 
# %%

#%%

# Create a new column for FamilySize
df['FamilySize'] = df['SibSp'] + df['Parch'] + 1  # FamilySize includes the passenge too 

# Step 2: Calculate the survival rate for each family size
survival_rate_by_family_size = df.groupby('FamilySize')['Survived'].mean() * 100  # Survival rate in percentages
total_passengers_by_family_size = df['FamilySize'].value_counts(sort=False)  # Total passengers in each family 
survivors_by_family_size = df[df['Survived'] == 1]['FamilySize'].value_counts(sort=False)  # Survivors in each family 
non_survivors_by_family_size = df[df['Survived'] == 0]['FamilySize'].value_counts(sort=False)  # Non-survivors in each family 

# Create a DataFrame for heatmap visiualization
heatmap_data = pd.DataFrame({
    'Survivors': survivors_by_family_size,
    'Non-Survivors': non_survivors_by_family_size
}).fillna(0)  # Fill missing values with 0 to get a reliabel dataset 

# Prepare data for heatmap
data_matrix = heatmap_data.T.values  # Amending the columns and rows

#Plot the heatmap using matplotlib
plt.figure(figsize=(10, 6)) #Defining the figures size 
plt.imshow(data_matrix, cmap='YlGnBu', aspect='auto', interpolation='none')

# Adding color bar
plt.colorbar(label="Count")

# Set x and y labels
plt.xticks(ticks=np.arange(len(heatmap_data.index)), labels=heatmap_data.index)
plt.yticks(ticks=[0, 1], labels=['Survivors', 'Non-Survivors'])

# Add title and axis labels
plt.title('Count of Survivors and Non-Survivors by Family Size')
plt.xlabel('Family Size')
plt.ylabel('Status')

# Annotate the heatmap with the exact numbers
for i in range(data_matrix.shape[0]):  # Iterate over rows
    for j in range(data_matrix.shape[1]):  # Iterate over columns
        plt.text(j, i, f'{data_matrix[i, j]:.0f}', ha='center', va='center', color='black')

# Show the plot
plt.show()

#Displaying survival rates for each family size
print("Survival rates by family size:")
for family_size, rate in survival_rate_by_family_size.items():
    print(f'Family Size {family_size}: {rate:.2f}%')

# Brief analysis of how family size get affected
highest_survival_rate_family_size = survival_rate_by_family_size.idxmax()
lowest_survival_rate_family_size = survival_rate_by_family_size.idxmin()

#Displaying the highes and lowest survivalrate in count of families. 
print(f"\nThe family size with the highest survival rate is: {highest_survival_rate_family_size}")
print(f"The family size with the lowest survival rate is: {lowest_survival_rate_family_size}")

````


# HomeAssignment 3

````r
#Installing all packages needed for this homeassignment 
library('AmesHousing')
library('dplyr')
library('ggplot2')
library('corrplot')

dff <- make_ames()
df <- read.csv('AmesHousing.csv')
df

# Section 1.2: Functions and Data Structures in R 
if (setequal(colnames(df), colnames(dff))){
  print('The two loading datasets gives the same outputs')
} else {
  print('Two loading datasets differs from eachother')
}

house_summary <- function(SalePrice) {
  result <- list(
    minimum = min(SalePrice, na.rm = TRUE),
    maximum = max(SalePrice, na.rm = TRUE),
    mean = mean(SalePrice, na.rm = TRUE),
    median = median(SalePrice, na.rm = TRUE),
    std_dev = sd(SalePrice, na.rm = TRUE)
  )
  
  return(result)
}

result <- house_summary(df$SalePrice)
result

# Randomly select 10 house square footages
square_footage <- sample(df$Gr.Liv.Area, 10)
print(square_footage)

# Create a 3x3 matrix with random sale prices
sale_prices_matrix <- matrix(sample(100000:400000, 9, replace = TRUE), nrow = 3, ncol = 3)
print(sale_prices_matrix)

# Randomly selecting 10 houses' IDs, neighborhoods, and sale prices
house_IDs <- sample(df$PID, 10)
neighborhoods <- sample(df$Neighborhood, 10)
sale_prices <- sample(df$SalePrice, 10)

# Create the data frame
house_data <- data.frame(PID =house_IDs , Neighborhood = neighborhoods, SalePrice = sale_prices)
print(house_data)


second_element <- square_footage[2]
print(second_element)

element_matrix <- sale_prices_matrix[3, 2]
print(element_matrix)

neighborhood_column <- house_data$Neighborhood
print(neighborhood_column)

# Create a data frame with the count of houses per neighborhood
neighborhood_count <- as.data.frame(table(df$Neighborhood))

# Rename columns for better readability
colnames(neighborhood_count) <- c("Neighborhood", "Count")

# Create a bar plot for the Neighborhood 
barplot(table(df$Neighborhood),
        ylab = "Count",      
        ylim = c(0, 500),    
        col = "blue",        
        las = 2)             

# Add the x-axis label
mtext("Neighborhoods", side = 1, line = 6, cex = 1.2)  # X-axis label


# Display the structure of the dataset
str(df)

# Provide summary statistics of the dataset
summary(df)

# Check for missing values in the dataset
missing_values <- colSums(is.na(df))
print(missing_values)


# Remove rows with missing values
df_clean <- na.omit(df)  # Removes rows with any NA values


# Create a histogram of SalePrice
ggplot(df, aes(x = SalePrice)) +
  geom_histogram(binwidth = 10000, fill = "midnightblue", color = "white", alpha = 0.8) +
  geom_density(aes(y = ..count..), color = "red", size = 1, linetype = "dashed") +  # Add a density curve
  theme_minimal() +
  labs(
    title = "Distribution of Sale Prices",
    x = "Sale Price",
    y = "Count"
  ) +
  theme(
    plot.title = element_text(hjust = 0.5, face = "bold", size = 14),  # Center and style the title
    axis.title = element_text(size = 12),  # Style axis labels
    panel.grid.major = element_line(color = "gray80")  # Light grid lines for clarity
  ) +
  scale_x_continuous(labels = scales::comma) 

# Scatter plot between Gr.Liv.Area and SalePrice
ggplot(df, aes(x = Gr.Liv.Area, y = SalePrice)) +
  geom_point(color = "midnightblue", alpha = 0.6, size = 2) +  # Scatter points with transparency
  geom_smooth(method = "lm", color = "red", se = FALSE, linetype = "dashed") +  # Linear regression line
  theme_minimal() +
  labs(
    title = "SAbove Ground Living Area vs. Sale Price",
    x = "Above Ground Living Area",
    y = "Sale Price"
  ) +
  theme(
    plot.title = element_text(hjust = 0.5, face = "bold", size = 14),  # Center and bold the title
    axis.title = element_text(size = 12),  # Style axis labels
    panel.grid.major = element_line(color = "gray76")  # Soft grid lines for clarity
  )




# Create the ggplot2 boxplot for neigthborhood vs sale price
ggplot(df, aes(x = Neighborhood, y = SalePrice, fill = Neighborhood)) +
  geom_boxplot(outlier.colour = "black", outlier.size = 1, outlier.alpha = 0.6) +
  theme_minimal() +
  labs(
    title = "Sale Prices across Neighborhoods",
    x = "Neighborhood",
    y = "Sale Price"
  ) +
  theme(
    axis.text.x = element_text(angle = 90, vjust = 0.5, hjust = 1, size = 9),  # Rotate x-axis labels
    axis.text.y = element_text(size = 10),
    legend.position = "none",  # Remove legend since it's redundant
    plot.title = element_text(hjust = 0.5, face = "bold")  # Center and bold the title
  ) +
  scale_fill_manual(values = rep("red", length(unique(df$Neighborhood))))  # Set fill color

# Descriptive statistics for Lot.Area, Gr.Liv.Area, and SalePrice

# Mean
mean_lot_area <- mean(df$Lot.Area, na.rm = TRUE)
mean_gr_liv_area <- mean(df$Gr.Liv.Area, na.rm = TRUE)
mean_sale_price <- mean(df$SalePrice, na.rm = TRUE)

# Median
median_lot_area <- median(df$Lot.Area, na.rm = TRUE)
median_gr_liv_area <- median(df$Gr.Liv.Area, na.rm = TRUE)
median_sale_price <- median(df$SalePrice, na.rm = TRUE)

# Standard deviation
sd_lot_area <- sd(df$Lot.Area, na.rm = TRUE)
sd_gr_liv_area <- sd(df$Gr.Liv.Area, na.rm = TRUE)
sd_sale_price <- sd(df$SalePrice, na.rm = TRUE)

# Print the results
cat("Mean, Median, and Standard Deviation:\n")
cat("Lot Area - Mean:", mean_lot_area, "Median:", median_lot_area, "SD:", sd_lot_area, "\n")
cat("Gr.Liv.Area - Mean:", mean_gr_liv_area, "Median:", median_gr_liv_area, "SD:", sd_gr_liv_area, "\n")
cat("SalePrice - Mean:", mean_sale_price, "Median:", median_sale_price, "SD:", sd_sale_price, "\n")


# Group by Bldg.Type and calculate the average SalePrice for each group
avg_saleprice_by_bldgtype <- df %>%
  group_by(Bldg.Type) %>%
  summarise(avg_SalePrice = mean(SalePrice, na.rm = TRUE))

# Print the result
print(avg_saleprice_by_bldgtype)



# Select the key numeric variables
numeric_vars <- df %>% select(Lot.Area, Gr.Liv.Area, Overall.Qual, Year.Built, SalePrice)

# Calculate the correlation matrix
correlation_matrix <- cor(numeric_vars, use = "complete.obs")  # 'complete.obs' ignores rows with missing values

# Print the correlation matrix
print(correlation_matrix)

# Create the TotalSF feature
df$TotalSF <- df$Gr.Liv.Area + df$Total.Bsmt.SF + df$Garage.Area

# Print the first few rows to check the new feature
head(df$TotalSF)


# Create the Age feature (assuming the current year is 2023)
df$Age <- 2023 - df$Year.Built

# Print the first few rows to check the new feature
head(df$Age)


# Min-max normalization function
normalize <- function(x) {
  return((x - min(x, na.rm = TRUE)) / (max(x, na.rm = TRUE) - min(x, na.rm = TRUE)))
}

# Normalize Gr.Liv.Area and SalePrice columns
df$Gr.Liv.Area.Normalized <- normalize(df$Gr.Liv.Area)
df$SalePrice.Normalized <- normalize(df$SalePrice)

# Print the first few rows to check the normalized columns
head(df[, c("Gr.Liv.Area.Normalized", "SalePrice.Normalized")])


# Convert Bldg.Type to a factor
df$Bldg.Type <- as.factor(df$Bldg.Type)

# Print the structure to check the changes
str(df$Bldg.Type)


# Set a seed for reproducibility
set.seed(123)

# Introduce missing values in 5% of the Lot.Area 
na_indices <- sample(1:nrow(df), size = 0.05 * nrow(df))
df$Lot.Area[na_indices] <- NA

# Check how many missing values were introduced
sum(is.na(df$Lot.Area))

# Calculate the median of Lot.Area, ignoring NA values
median_lot_area <- median(df$Lot.Area, na.rm = TRUE)

# Impute missing values with the median
df$Lot.Area[is.na(df$Lot.Area)] <- median_lot_area

# Check if there are any remaining missing values
sum(is.na(df$Lot.Area))

````

# HomeAssignment 4

````r
library('tidyverse')
library('ggplot2')
library('viridis')
library('viridisLite')

student_data <- read.csv("student_data_exam.csv", header = TRUE, sep =";")
stud_data <- read.csv("student_data_exam.csv", header = TRUE, sep =";")

student_data$Education[student_data$Education =='some college'] <- 'college'

student_data$Education[student_data$Education == "master's degree"] <- "college"

student_data$Education[student_data$Education == "bachelor's degree"] <- "college"

student_data$Education[student_data$Education == "bachelor's degree"] <- "college"

student_data$Education[student_data$Education == "associate's degree"] <- "college"

student_data$Education[student_data$Education =='some high school'] <- 'high school'

student_data$Lunch[student_data$Lunch == 'free/reduced'] <- 'reduced'

student_data$Gender <- as.factor(student_data$Gender) #Converting the Gender variable into a factor for analytical purposes. 1 = Female, 2 = Male 

student_data$Ethnicity <- as.factor(student_data$Ethnicity) #Converting the Ethnicity into a facrot for Analytical purposes for the further analysis. 

student_data$TestPreparation <- as.factor(student_data$TestPreparation) #Converting the TestPreparation into factor for Analytical purposes 2 = Complete, 1 = None 

student_data$Education <- as.factor(student_data$Education)

student_data$Lunch <- as.factor(student_data$Lunch)

options(max.print=999999)

print(is.na(student_data)) #Checking the dataset to be without any N/A

summary(student_data)


#Section 2: data visiualization and summary tables:
#I)
student_data %>%
  ggplot(aes(x = TestPreparation, y = Math, fill = TestPreparation)) +
  geom_boxplot() +
  scale_fill_viridis(discrete = TRUE, alpha = 0.6) +
  geom_jitter(color = "black", size = 0.4, alpha = 0.5) +
  theme_minimal() +  # Use a minimal ggplot2 theme
  theme(
    legend.position = "none",
    plot.title = element_text(size = 11),
    axis.text.x = element_text(angle = 45, hjust = 1)  # Rotate x-axis labels if needed
  ) +
  ggtitle("Math Reusults compared with Test Preparations") +
  xlab("Test Preparations") +
  ylab("Math Results")


#II)
#Histogram of Math scores compared with ethnicity 
ggplot(student_data, aes(x = Math, fill = Ethnicity)) +
  geom_histogram(binwidth = 7, position = "dodge", color = "black") +  # Use position = "dodge" to separate bins by Ethnicity
  labs(
    title = "Histogram of Math Scores by Ethnicity",
    x = "Math Score",
    y = "Frequency"
  ) +
  theme_minimal() +
  theme(
    plot.title = element_text(hjust = 0.5, face = "bold", size = 14),
    axis.title = element_text(size = 12)
  )

#Histogram of Reading Scores compared with Ethnicity
ggplot(student_data, aes(x = Reading, fill = Ethnicity)) +
  geom_histogram(binwidth = 7, position = "dodge", color = "black") +  # Use position = "dodge" to separate bins by Ethnicity
  labs(
    title = "Histogram of Reading Scores by Ethnicity",
    x = "Reading Scores",
    y = "Fre                                                                                                                                                                                                                                                                                                                    quency"
  ) +
  theme_minimal() +
  theme(
    plot.title = element_text(hjust = 0.5, face = "bold", size = 14),
    axis.title = element_text(size = 12)
  )

#Histogram of Writing Scores compared with Ethnicity
ggplot(student_data, aes(x = Writing, fill = Ethnicity)) +
  geom_histogram(binwidth = 7, position = "dodge", color = "black") +  # Use position = "dodge" to separate bins by Ethnicity
  labs(
    title = "Histogram of Writing Scores by Ethnicity",
    x = " Writing Score",
    y = "Frequency"
  ) +
  theme_minimal() +
  theme(
    plot.title = element_text(hjust = 0.5, face = "bold", size = 14),
    axis.title = element_text(size = 12)
  )

#Section 3: Data modelling and Logistic Regression. 

stud_data$Gender[stud_data$Gender == 'male'] <- 1
stud_data$Gender[stud_data$Gender == 'female'] <- 0
stud_data$TestPreparation[stud_data$TestPreparation == 'none'] <- 0
stud_data$TestPreparation[stud_data$TestPreparation == 'completed'] <- 1
stud_data$Education[stud_data$Education =='some college'] <- 'college'
stud_data$Education[stud_data$Education == "master's degree"] <- "college"
stud_data$Education[stud_data$Education == "bachelor's degree"] <- "college"
stud_data$Education[stud_data$Education == "bachelor's degree"] <- "college"
stud_data$Education[stud_data$Education == "associate's degree"] <- "college"
stud_data$Education[stud_data$Education =='some high school'] <- 'high school'
stud_data$Lunch[stud_data$Lunch == 'free/reduced'] <- 'reduced'

````
