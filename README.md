# Analysis-of-Customer-Behavior-and-Sales-Patterns
Objective
Enhance customer experience through  Exploratory Data Analysis (EDA) on sales data
Drive revenue growth through strategic data-driven initiatives.
Uncover valuable insights by harnessing the power of data analytics.

I utilized the following tools and technologies to analyze and visualize data:
Python: Used for data analysis and processing tasks.
Matplotlib: Employed for creating insightful visualizations.
Seaborn: Utilized for enhancing the quality of plots.
Jupyter Notebook: Served as the coding environment for the project.

# import python libraries
import numpy as np 
import pandas as pd 
import matplotlib.pyplot as plt # visualizing data
%matplotlib inline
import seaborn as sns

# import csv file
df = pd.read_csv('Diwali Sales Data.csv', encoding= 'unicode_escape')

df.shape
(11251, 15)

df.head()


"Data Cleaning: Preparing and Refining the Dataset"
df.info()
<class 'pandas.core.frame.DataFrame'>
Index: 11239 entries, 0 to 11250
Data columns (total 13 columns):
 #   Column            Non-Null Count  Dtype 
---  ------            --------------  ----- 
 0   User_ID           11239 non-null  int64 
 1   Cust_name         11239 non-null  object
 2   Product_ID        11239 non-null  object
 3   Gender            11239 non-null  object
 4   Age Group         11239 non-null  object
 5   Age               11239 non-null  int64 
 6   Marital_Status    11239 non-null  int64 
 7   State             11239 non-null  object
 8   Zone              11239 non-null  object
 9   Occupation        11239 non-null  object
 10  Product_Category  11239 non-null  object
 11  Orders            11239 non-null  int64 
 12  Amount            11239 non-null  int32 
dtypes: int32(1), int64(4), object(8)
memory usage: 1.2+ MB


#drop unrelated/blank columns
df.drop(["Status", "unnamed1"], axis = 1 ,inplace = True)

df.info()
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 11251 entries, 0 to 11250
Data columns (total 13 columns):
 #   Column            Non-Null Count  Dtype  
---  ------            --------------  -----  
 0   User_ID           11251 non-null  int64  
 1   Cust_name         11251 non-null  object 
 2   Product_ID        11251 non-null  object 
 3   Gender            11251 non-null  object 
 4   Age Group         11251 non-null  object 
 5   Age               11251 non-null  int64  
 6   Marital_Status    11251 non-null  int64  
 7   State             11251 non-null  object 
 8   Zone              11251 non-null  object 
 9   Occupation        11251 non-null  object 
 10  Product_Category  11251 non-null  object 
 11  Orders            11251 non-null  int64  
 12  Amount            11239 non-null  float64
dtypes: float64(1), int64(4), object(8)
memory usage: 1.1+ MB

#check for null values
pd.isnull(df).sum()
User_ID              0
Cust_name            0
Product_ID           0
Gender               0
Age Group            0
Age                  0
Marital_Status       0
State                0
Zone                 0
Occupation           0
Product_Category     0
Orders               0
Amount              12
dtype: int64



df.dropna(inplace = True)
drop null values

df.info()

<class 'pandas.core.frame.DataFrame'>
Index: 11239 entries, 0 to 11250
Data columns (total 13 columns):
 #   Column            Non-Null Count  Dtype  
---  ------            --------------  -----  
 0   User_ID           11239 non-null  int64  
 1   Cust_name         11239 non-null  object 
 2   Product_ID        11239 non-null  object 
 3   Gender            11239 non-null  object 
 4   Age Group         11239 non-null  object 
 5   Age               11239 non-null  int64  
 6   Marital_Status    11239 non-null  int64  
 7   State             11239 non-null  object 
 8   Zone              11239 non-null  object 
 9   Occupation        11239 non-null  object 
 10  Product_Category  11239 non-null  object 
 11  Orders            11239 non-null  int64  
 12  Amount            11239 non-null  float64
dtypes: float64(1), int64(4), object(8)
memory usage: 1.2+ MB
"Converting 'Amount' Column from Float to Integer".
Explanation: In this step, we will convert the 'Amount' column in the DataFrame from a float data type to an integer data type
df["Amount"]=df["Amount"].astype(int)

df["Amount"].dtypes
df.info()
<class 'pandas.core.frame.DataFrame'>
Index: 11239 entries, 0 to 11250
Data columns (total 13 columns):
 #   Column            Non-Null Count  Dtype 
---  ------            --------------  ----- 
 0   User_ID           11239 non-null  int64 
 1   Cust_name         11239 non-null  object
 2   Product_ID        11239 non-null  object
 3   Gender            11239 non-null  object
 4   Age Group         11239 non-null  object
 5   Age               11239 non-null  int64 
 6   Marital_Status    11239 non-null  int64 
 7   State             11239 non-null  object
 8   Zone              11239 non-null  object
 9   Occupation        11239 non-null  object
 10  Product_Category  11239 non-null  object
 11  Orders            11239 non-null  int64 
 12  Amount            11239 non-null  int32 
dtypes: int32(1), int64(4), object(8)
memory usage: 1.2+ MB

df.columns
Index(['User_ID', 'Cust_name', 'Product_ID', 'Gender', 'Age Group', 'Age',
       'Marital_Status', 'State', 'Zone', 'Occupation', 'Product_Category',
       'Orders', 'Amount'],
      dtype='object')

#rename column
df =df.rename(columns={"Marital_Status" : "Marital"})

df.columns
Index(['User_ID', 'Cust_name', 'Product_ID', 'Gender', 'Age Group', 'Age',
       'Marital', 'State', 'Zone', 'Occupation', 'Product_Category', 'Orders',
       'Amount'],
      dtype='object')

df.describe()


Exploratory data analysis (EDA)
"Gender: Understanding Patterns and Insights"
sales_gen = df.groupby(['Gender'], as_index = False)['Amount'].sum().sort_values(by = 'Amount', ascending = False)
sns.set(rc={'figure.figsize':(5,4)})
sns.set_palette("Dark2")
plt.title( "Gender-based Sales Amount Analysis" , fontsize = 10)
sns.barplot(x = 'Gender', y = 'Amount', data = sales_gen)


"Age : Uncovering Trends and Patterns"
 ax = sns.countplot(data = df, x ="Age Group", hue = 'Gender')
sns.set(rc={'figure.figsize':(16,6)})
plt.title( "Count of Buyers by Age Group and Gender" , fontsize = 10)
sns.set_palette("Dark2")
for bars in ax.containers:
ax.bar_label(bars)


sales_Age = df.groupby(['Age Group'], as_index = False)['Amount'].sum().sort_values(by = 'Amount', ascending = False)
sns.barplot(x = 'Age Group', y = 'Amount', data = sales_Age)
sns.set(rc={'figure.figsize':(16,6)})
sns.set_palette("Dark2")
plt.title("Sales Amount by Age Group and Gender", fontsize = 15)


"State: Analyzing Geographical Patterns and Insights"
sales_state = df.groupby(['State'], as_index = False)['Amount'].sum().sort_values(by='Amount', ascending=False).head(10)
sns.set(rc={'figure.figsize':(16,6)})
sns.set_palette("Dark2")
plt.title("Top 10 States with the Highest Sales Amount", fontsize = 20)
sns.barplot(data = sales_state, x = 'State',y= 'Amount')





#Top 10 States with the Highest Order Count"
sales_state = df.groupby(['State'], as_index = False)['Orders'].sum().sort_values(by='Orders', ascending=False).head(10)
sns.set(rc={'figure.figsize':(16,6)})
sns.set_palette("Dark2")
plt.title( "Top 10 States with the Highest Sales Orders" , fontsize = 20)
sns.barplot(data = sales_state, x = 'State',y= 'Orders')


"Occupation : Understanding Relationship Patterns and Implications"
ax = sns.countplot(data = df, x = 'Occupation')
sns.set(rc={'figure.figsize':(31,7)})
sns.set_palette("Dark2")
plt.title( "Occupation Distribution Analysis" , fontsize = 13)
for bars in ax.containers:
ax.bar_label(bars)


sales_Occupation = df.groupby(["Occupation"], as_index = False)['Amount'].sum().sort_values(by='Amount', ascending=False)
sns.barplot(data = sales_Occupation , x = "Occupation", y = "Amount")
plt.title("Total Sales Amount by Occupation", fontsize = 20)


"Product_Category : Understanding Relationship Patterns and Implications"
ax = sns.countplot(data = df, x = 'Product_Category')
sns.set(rc={'figure.figsize':(32,7)})
sns.set_palette("Dark2")
plt.title( "Product Category Analysis: Count Distribution", fontsize = 20)
for bars in ax.containers:
ax.bar_label(bars)


sales_Product_Category = df.groupby(["Product_Category"], as_index = False)['Amount'].sum().sort_values(by='Amount', ascending=False).head(10)
sns.set(rc={'figure.figsize':(20,7)})
sns.set_palette("Dark2")
sns.barplot(data =sales_Product_Category, x = "Product_Category", y = "Amount")
plt.title("Product Category Analysis: Sales Amount Distribution", fontsize = 20)


"Zone: Understanding Relationship Patterns and Implications"
sales_Zone = df.groupby(["Zone"], as_index = False)['Orders'].sum().sort_values(by='Orders', ascending=False).head(10)
sns.barplot(data = sales_Zone, x= "Zone" , y = "Orders")
sns.set_palette("Dark2")
plt.title("Zone with the Highest Orders", fontsize = 20)





Insights
🔍 After analyzing a large dataset, several key findings emerged:
1️⃣ Analysis of Gender: Females as the Dominant Buyers with Strong Purchasing Power 💪
2️⃣ Age Analysis: Largest Proportion of Female Buyers Falls within the 26-35 Year Age Group 🎯
3️⃣ Top States with Highest Sales Orders: Uttar Pradesh, Maharashtra, and Karnataka 🌟
4️⃣ Marital Status: Married Women Exhibit Significant Purchasing Power 💼
5️⃣ Industry Insights: IT, Healthcare, and Aviation Sectors Are Prominent Buyers 🌐
6️⃣ Top Product Categories by Sales Amount: Food, Clothing, and Electronics 🛒
7️⃣ Sales Insights by Region: Central Zone Leads, Followed by South and West ⚡

🔑 Based on these insights, I recommend offering tailored discounts, coupons, and special offers to married women aged 26-35 working in IT, healthcare, and aviation sectors from state Uttar Pradesh, Maharashtra, and Karnataka  . 🎁
📈 These findings provide valuable strategic guidance for businesses looking to optimize their marketing efforts and drive sales growth.
 GitHub: https://github.com/davidingle188 follow me on linkedin : https://www.linkedin.com/in/davidingle18082000/
Thank you!
