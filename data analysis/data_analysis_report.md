# Product Sales Data Analysis
## Data Analyst Practical Exam
Biman Mondal\
Nov. 18, 2025

## Introduction

The sales team from Pens & Printers has requested an analysis of the effectiveness of the sales approaches on the new product line. Product sales data from the new stationery line has been provided in a comma-delimited file. The goal of the report is to extract useful information from the data provided to answer relevant information about revenue and sales approach, and other insights. 

## Data Validation

The Pandas library in Python was used to evaluate the comma-delimited file. The dataframe contains 8 columns and 15000 rows. The columns are: week|sales_method|customer_id|nb_sold|revenue|'years_as_customer'|'nb_site_visits'|'state'. Investigating datatypes shows that 3 categorical values: sales method, customer id, and state (location) of the customer. The numerical values include the number of weeks, the number of products sold, and revenue. 

Investigating the unique values of the sales methods shows that there are 5 sales method categories, but two of them are duplicates. There are actually three methods used by sales: Email, Call, and Email+Call. The duplicates 'em + call' and 'email' were appropriately assigned to 'Email + Call' and 'Email', respectively. The customer_id is a unique letters and numbers separated by dashes. Checking for duplicates shows that there are only unique customers in the dataset. Checking the state column shows that all 50 states are represented.

The number of weeks is spread as integers from 0 to 6. The number of years as a customer ranges from 0 to 63. Given that the company began in 1984, the values greater than 41 were replaced with the average years as customer of 5 years. The number of site visits ranges from 12 to 41, with the average around 25 site visits.

### Addressing Missing Values

The revenue column has 1074 missing (NaN) values. Since no other data is missing, to begin the analysis, null data were replaced with the mean of the revenue value. After visualizing the data, the missing revenue values were found to occur at random. Replacing the revenue changes the trends visualized. For this reason, a more sophisticated method of imputing the NaN values was devised by creating a linear regression fit of the NaN rows based on the sales method. The dataset was split into a revenue prediction set and a training set based on whether the revenue included a value or not. All the categorical data were replaced with numerical values, and the text-based categorical columns were dropped. The linear regression model was fit to the training set and subsequently used to predict the NaN revenue values. This iterative approach was required to arrive at a tidy dataset.

![regression_plot_revenue_vs_nb_sold](regression_plot_revenue_vs_nb_sold.png)


## Exploratory Data Analysis

A pairplot is a plotting technique used to visualize the relationships between multiple numerical features simultaneously. The distribution of each feature is given along the diagonal. Off-diagonal, there are relationships between the numerical features; note the symmetry. The following is the plot of the numerical values in the dataset.

![Pairplot](Pairplot.png)

Intuitively, a relationship between revenue and the number of items sold is visible. The scatter plot shows three different trend lines within revenue and items sold, which could mean there is another variable at play. The trend between revenue and week shows an increasing trend. The distribution of revenue at the center of the plot looks multimodal, while the number of items sold seems to skew right. The revenue distribution shows indeed that the distribution is multimodal. The number of site visits is distributed normally. The years as customer distribution skews right, indicating most of the customers have had a relationship for the last 10 years. 

The following bar charts show the location of customers. The top 10 states that result in the highest revenue are plotted on the first graph; this is the same order of states with the highest number of customers. The second bar graph represents the states with the highest revenue per visit ratio, albeit a smaller percentage of the customer base. 

![Customer_State_Plot](Customer_State_Plot.png)

A count of the sales method shows that sales by 'Email' is the primary method at 50%, 'Call' occurs at 33%, and 'E-mail + Call' is 17% of the dataset. As stated above, the total dataset includes 15000 customers. 

![SalesMethod_Proportion_PieChart](SalesMethod_Proportion_PieChart.png)


The revenue is grouped by the sales method and plotted in the following bar chart. The results show that the Email sales method generates the majority of revenue at 51%, followed by email + calling at 33% of revenue, followed by just calling at 16% of revenue. The comparison of the previous and following figures shows that calling occurs at 33% of the time, but returns only 16% of the revenue. 

![Total_Revenue_bySales](Total_Revenue_bySales.png)

The kernel density plot is a continuous distribution plot. The KDE shows a clearer interaction of the revenue streams based on the sales method. Sales method by calling results in four different modes at the lower revenue end, email sales results in a middle revenue peak that has two modes, and email and calling results in a higher revenue but a lower frequency with at least three different modes. There are five distinct clusters. There are two high-frequency segmented clusters at the lower and middle end, and 3 much smaller frequency  at the higher revenue end. Each revenue by sales method is distributed at different averages and has a distinct spread. Calling results in a lower average revenue than Email, and then Email and Calling. However, Email and Call sales have a large spread of the revenue. 

![KDE_revenue_distribution](KDE_revenue_distribution.png)

## Metric to monitor
The definition of revenue is the product of the quantity of units sold by the cost of the item. If the objective of the sales team is to maximize the revenue of each new product, the metric to target is the average revenue per week. The following plot shows the averages broken down further by sales method. We see that Call has the lowest averages per week, while Email has middle averages, and Email and Call sales have the highest averages. Note that the revenue by email shows a slowing trend in weeks 4,5,6 while the email and calling shows a healthy increase in revenue in the same weeks. Overall, the average revenue for a Call sales is \$48, the average revenue for Email sales is \$97, and the average revenue for Email and Call sales is \$184.

![Mean_Revenue_bySales_perWeek](Mean_Revenue_bySales_perWeek.png)

## Summary and Recommendation
The new stationery product sales dataset has been analyzed at the request of the sales team. Based on the data analysis performed, the Email + Call sales method has shown to generate the highest average revenue; however, the Email sales method has shown to generate the largest volume of revenue acrosss the six weeks. Given that calling can take up to thirty minutes, it is recommended that Email be leveraged and, if necessary, follow up with a phone call. Doing so would improve efficiency in sales and, based on the analysis, increase the revenue of the new stationary product line. 
