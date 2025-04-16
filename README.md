# 📊 Analyze Global Retail Company RFM Customer Segmentation| Python, GoogleColab
Please see the coding file attached or reach this link: [RFM_Project_Python](https://colab.research.google.com/drive/17Dlv4VH-F0KqEzzVcZJPbQCjav0JJ4wl#scrollTo=M3_yuk2uBScA)

## 📑 I. Introduction
### 📖 What is this project about?
- SuperStore is a global retail company. The Marketing Department wants to run marketing campaigns during the Christmas and New Year holidays to thank customers for their past support of the company. In addition, potential customers can be upgraded to become loyal customers.
- The Marketing Director proposed a plan to run RFM Model in Python to segment customers and then launch appropriate marketing campaigns.
- Recommendation for Marketing and Sales Team: With the company's retail model, which of three indicators R,F,M shoulde be given the most attention?
### ❓ Business Question 
- How can the Marketing department classify customer segments effectively to deploy tailored for each **customer segment** to run marketing campaigns for Christmas and New Year, appreciating loyal customers and attracting potential ones?
- How can the **RFM (Recency, Frequency, Monetary)** model be used to segment customers and optimize marketing strategies for higher engagement and revenue?

### 📌 RFM Model
- RFM is a method used for analyzing customer value. It is commonly used in database marketing and direct marketing and has received particular attention in retail and professional services industries
- RFM Model
    - Recency (R): How recently a customer made a purchase. Customers who made purchases more recently are typically more engaged and likely to buy again.
    - Frequency (F): How often a customer makes purchases within a given period. Frequent buyers are usually more loyal and valuable to a business.
    - Monetary (M): How much money a customer spends in total. High spenders contribute significantly to revenue and can be prioritized for premium services or offers.
- RFM analysis numerically ranks a customer in each of these three categories, generally on a scale of 1 to 5 (the higher the number, the better the result). The “best” customer would receive a top score in every category.
  
### 📂2. Dataset
This is a file database in this topic: [**Dataset**](https://drive.google.com/drive/u/0/folders/1hguyL961Nfi8AeCFeq-3dzHdGOkhTHkS)
<details> 
<summary>Table 1: Ecommerce retail:</summary>

| Field Name | Data Type | Description |
|-------|-------|-------|
|InvoiceNo|STRING| Invoice number. Nominal, a 6-digit integral number uniquely assigned to each transaction. If this code starts with letter 'C', it indicates a cancellation.|
|StockCode|STRING|Product (item) code. Nominal, a 5-digit integral number uniquely assigned to each distinct product.|
|Description|STRING| Product (item) name. Nominal.|
|Quantity|INTEGER|The quantities of each product (item) per transaction. Numeric.|
|InvoiceDate|DATETIME|Invoice Date and time. Numeric, the day and time when each transaction was generated.|
|UnitPrice|FLOAT|Unit price. Numeric, Product price per unit in sterling.|
|CustomerID|STRING|Customer number. Nominal, a 5-digit integral number uniquely assigned to each customer.|
|Country|STRING|Country name. Nominal, the name of the country where each customer resides.|

</details>
  
Table 2: Sementation: <br>
| Field Name | Data Type | Description |
|-------|-------|-------|
|Segment|STRING|Segment of Customer|
|RFM Score|STRING|Score of RFM|

## ⚒️ II.Main Process
1️⃣ Load Dataset
```python
e_retail = pd.read_excel(Path + '/ecommerce retail.xlsx',sheet_name= 'ecommerce retail')
e_retail.head(5)
```

![9e0d5280-ded5-43da-b91c-78c3d0c95b81](https://github.com/user-attachments/assets/4597f6de-6925-4f60-8468-a0a394b227b4)



2️⃣ Exploratory Data Analysis (EDA)
```python
e_retail.info()
print('----------')
e_retail.describe()
```

![d941aeb8-c468-4c34-a163-78d9035728e3](https://github.com/user-attachments/assets/12678fb7-482a-4b2b-a7c0-56a03b79d43b)


#### Summary of pre-processing steps
➡️ Convert Datatype: <br>
- Columns: `InvoiceNO`, `StockCode`, `Description`, `CustomerID`, `Country` converted to String for consistency.
    
➡️ Remove invalid data: <br>
Remove records that have:
- `Quantity < 0 `
- `UnitPrice < 0`
- `Cancel_list = True`
- `Description` is missing value. Next step: Replace missing value `nan`, `Nan`, `<NA>` to `None`

➡️ Handle missing value:
- Check missing value and `CustomerID` is missing.\
👉🏻 Next action Delete `CustomerID` missing as RFM analysis is not possible for these customer

➡️ Handle duplicate value:
- While detect value kind of columns: `InvoiceNo`, `StockCode`, `InvoiceDate`, `CustomerID` is duplicated value.\
👉🏻 Next action -> Delete duplicated value. This ensures that each transaction is only counted once in the RFM analysis.


#### Detect value

```python
e_retail[e_retail['Quantity']<0]
```

![f5649a0f-623f-4a9f-a4dd-dd3f32f47cdd](https://github.com/user-attachments/assets/fb0c64db-f11a-4fc2-b60d-fcfe51993241)


```python
# The symbol C in "InvoiceN0" means the order is canceled. Check if the Quantity is negative, is the order canceled?
# Create a column to check the cancellation status of the data
e_retail['Cancel_list'] = e_retail['InvoiceNo'].apply(lambda x: True if str(x)[0] == 'C' else False)
e_retail[(e_retail['Quantity']<0) & (e_retail['Cancel_list'] == True)].head(10)
```
Create Cancel_list to check Cancel InvoiceN0

```python
# KCheck for False Cancel orders and quantity < 0
e_retail[(e_retail['Quantity']<0) & (e_retail['Cancel_list'] == False)].head(10)
```
![674bb826-61ed-456f-8869-c06feedd8037](https://github.com/user-attachments/assets/0565fbcc-26e7-4d6a-bba3-9e7a84cd70eb)


Check reason why `Cancel_list = False` and `Quantity < 0`

![1e1bc705-d8ab-4e1a-994d-8ef5b00ea1c0](https://github.com/user-attachments/assets/c8ebf7a7-32ff-45e3-9519-ee8466da0afa)


```python
#Handle abnormal data values
e_retail = e_retail[e_retail['Quantity']>=0]
e_retail = e_retail[e_retail['Cancel_list'] == False] 

```
Drop `Cancel_list = False` and `Quantity <0` to clean data


```python
e_retail[e_retail['UnitPrice']<0]
```

![7c3b6ec8-3724-4467-83d4-71f9ba6c864e](https://github.com/user-attachments/assets/ee20dc5d-7907-4aa8-8c02-327406ed205e)

Checking `Unitprice < 0` and reason `Unitprice < 0` is "Adjust bad debt"

```python
#Cleaning UnitPrice and Description
e_retail = e_retail[e_retail['UnitPrice'] >= 0]
e_retail = e_retail[e_retail['Description'] != '<Na>']
```
Handle abnormal data values from `Quantity` and `Description`


```python
#Check missing value
missing_value = {
                 'volume': e_retail.isnull().sum(),
                 'percent':e_retail.isnull().sum()/ (e_retail.shape[0])
                 }
missing_value = pd.DataFrame(missing_value)
missing_value
```
![e1eb0a23-0366-4630-957a-ece40b65b754](https://github.com/user-attachments/assets/fce1b201-0ae7-4113-830c-1b8e1dce3051)




```python
#Handle missing value
e_retail = e_retail[e_retail['CustomerID'].notnull()]
```


```python
#Check duplicate
dup_retail = e_retail[e_retail.duplicated(subset = ['InvoiceNo','StockCode','InvoiceDate','CustomerID'], keep = 'first')]
dup_retail.head()
```

```python
#Handle duplicate and final dataframe
final_retail = e_retail.drop_duplicates(subset = ['InvoiceNo','StockCode','InvoiceDate','CustomerID'], keep = 'first')
final_retail.head()

```

```python
#Create cost, day, month, year
final_retail['cost'] = final_retail['Quantity'] * final_retail['UnitPrice']
final_retail['Day'] = final_retail['InvoiceDate'].dt.day
final_retail['Month'] = final_retail['InvoiceDate'].dt.month
final_retail['Year'] = final_retail['InvoiceDate'].dt.year
final_retail.head()
```
Create `cost`, `Day`, `Month`, `Year` to prepare for data process step

```python
final_retail.info()
```

![fc2f6020-79a6-475c-8b31-b512c8846b88](https://github.com/user-attachments/assets/22e1b1af-36cc-4ed2-b094-d38370f765f1)

👉 Dataframe after detect and Expoloratory Data Analysis


#### 🔥 Data Process

```python
#Calculate Recency, Frequency, Monetory
RFM = final_retail.groupby('CustomerID').agg({'InvoiceDate': lambda x: (final_retail['InvoiceDate'].max() - x.max()).days,
                                              'InvoiceNo': lambda x: len(x),
                                              'cost': lambda x: x.sum()

                                            }).reset_index()
RFM.columns = ['CustomerID','Recency','Frequency','Monetary']
RFM.head(10)
```
Define Recency, Frenquency, Monetoray in RFM dataframe


```python
#Get R, F, M score by using qcut
#Get label for qcut
lab_des = [5,4,3,2,1]
lab_asc = [1,2,3,4,5]

#Using qcut
#qcut is a function used to divide data into equal-sized bins based on quantiles
RFM['R'] = pd.qcut(RFM['Recency'], q = 5, labels = lab_des) #Score desc
RFM['F'] = pd.qcut(RFM['Frequency'], q = 5, labels = lab_asc)
RFM['M'] = pd.qcut(RFM['Monetary'], q = 5, labels = lab_asc)
RFM['RFM'] = RFM['R'].astype(str) + RFM['F'].astype(str) + RFM['M'].astype(str)
RFM['RFM'] = RFM['RFM'].astype('string')
RFM.head(5)
```

![a0925824-934e-4eda-bb56-c22e7d1c3fa8](https://github.com/user-attachments/assets/10a35ade-963c-4678-b3f8-7bf8ace4be30)

👉 Apply quintile by using qcut in Python to divide the dataset into 5 ranges:

```python
Segmentation = pd.read_excel('ecommerce_retail.xlsx',sheet_name= 'Segmentation')
RFM_final = RFM.merge(Segmentation, how = 'left', left_on = 'RFM', right_on = 'RFM Score')
RFM_final.head(10)
```

👉 Merge `Segmentation` and `RFM` to segment customer by `RFM Score`

```python
RFM_final.describe()
```

![5e79ffef-d537-435c-a9a7-abd732d00cf1](https://github.com/user-attachments/assets/cb6c1bd1-7eb0-4ffb-a1b4-2e4d6cb49325)

- Recency (R): The median is 50 days, but the wide range (min 0, max 373) indicates a mix of active and inactive customers.
- Frequency (F): The average is 89 purchases, but the max reaches 7477, suggesting a small portion of highly engaged customers driving most transactions.
- Monetary (M): The median spending is 658.64, but the max is 280,206, hinting at the presence of a few extremely high-value customers.

**Recommendation**
Since a small percentage of customers contribute significantly to revenue, focus on loyalty programs or exclusive offers for frequent and high-spending customers to maximize retention. Meanwhile, inactive customers (high recency, low frequency) could be re-engaged through personalized promotions or reminder emails.

## 📖III. Data Visualization with Python
### 📝Visulization RFM Segment
#### 📜Visualize Number of customers by RFM Segments
```python

fig, ax1 = plt.subplots(1,figsize = (10,5))
ax2 = ax1.twinx()
sns.barplot(data= segmentation_data,
            x='Segment',
            y= 'cus_count',
           # palette='tab10',
            ax=ax1)

sns.lineplot(data = segmentation_data.sort_values('rate_customer'),
             x = 'Segment',
             y = 'rate_customer',
             marker = 'o',
             color = 'red')
ax1.set(xlabel='Segment', ylabel='Number of Customers')
ax2.set(ylabel='Percentage of Customers')
ax1.tick_params(axis='x', rotation=90)
plt.title('Number of customers by RFM Segments')
plt.show()
```

![download](https://github.com/user-attachments/assets/7e818f67-f673-46a9-8597-c096a113459c)

👉🏻 The number of Hibernating customers is highest with 809 customers and 18.64%. Beside, Champions have 804 customers and 18.53%\
👉🏻 Cannot Lose Them segment have the lowest customer even so rate customer with 89 customers and 2.05%

#### 📜Total cost
```python
colors = ['#91DCEA', '#64CDCC', '#5FBB68',
          '#F9D23C', '#F9A729', '#FD6F30']
#
count_map1 = sq.plot(sizes=segmentation_data['rate_monetory'],
                    label=segmentation_data['Segment'],
                    alpha=.8,
                    text_kwargs={'fontsize':6},
                    value=[f'{x}%' for x in segmentation_data['rate_monetory']],
                    color = colors)
plt.title('Total Cost by RFM Segments')
plt.axis("off")
plt.show()
```

![download (1)](https://github.com/user-attachments/assets/8dd51212-c8b9-4c1c-b9d9-3604c195ff3f)

👉🏻 Segment with the highest total cost revenue: Champions(5462794.0 dollars, equivalent to 61,76%) and Loyal segment(974973.7 dollars and equivalent to 11.02%)\
👉🏻 Segment with the lowest total cost: About To Sleep(53231.2 dollars, equivaltent to 0.6%), New Customers(63949.4 dollars, equivalent to 0.72%)

**Recommnedation**
- Champions & Loyal Customers
    - Offer exclusive discounts, VIP memberships, or early access to new products.
    - Implement a loyalty rewards program to encourage continuous spending.
- At Risk & Cannot Lose Them
    - Send personalized retention emails, highlighting their past interactions and offering incentives to return.
    - Create targeted reactivation campaigns with special offers and reminders.
- New & Lost Customers
    - Improve onboarding experience (welcome emails, personalized recommendations, discounts for first purchases).
    - Implement remarketing campaigns for lost customers via email or social ads.

#### 📜Visualize Recency & Frequency rate by Segment
```python
# Set up figsize
fig, ax = plt.subplots(1, figsize=(18, 6))

# Line plot
ax.plot(segmentation_data['Segment'], segmentation_data['rate_recency'], marker='o', color='blue', label='Rate Recency')
ax.plot(segmentation_data['Segment'], segmentation_data['rate_frequency'], marker='s', color='red', label='Rate Frequency')

# Label and Tittle
ax.set_title('Recency and Frequency rate by Segments')
ax.set_xlabel('SEGMENTS')
ax.set_ylabel('Percentage')
ax.grid(True)
ax.legend()
```  

![download (2)](https://github.com/user-attachments/assets/78920108-0ea8-4964-a01f-7aa0cb9008f5)

- Champions and Loyal show high frequency and low recency, meaning they are highly engaged and valuable
- At Risk & Cannot Lose Them have low frequency but high recency
- Lost Customers & Hibernating Customers have both high recency and low frequency, indicating they are no longer contributing to business revenue.
- New Customers & Promising Customers have moderate frequency but low recency, meaning they have potential but are not fully engaged yet.

**Recommendation**
- Champions & Loyal Customers
    - Implement a VIP program or exclusive rewards to maintain loyalty.
    - Send personalized early-access offers or targeted discounts.
- At Risk & Cannot Lose Them
    - Launch re-engagement campaigns via email or retargeting ads.
    - Offer win-back promotions to encourage them to purchase again.
- Lost Customers & Hibernating Customers
    - Identify reasons for disengagement through feedback surveys.
    - Provide a limited-time special offer tailored to their past purchasing behavior.
- New & Promising Customers
    - Enhance onboarding experience with personalized product recommendations.
    - Use welcome discounts or incentives to increase conversion rates.

### 📝Visualize Loyal and Non Loyal Segment

#### 📜Loyal Segment
**AOV** - Average Order Value is a key metric in e-commerce and business analytics that measures the average amount of money spent per order.
```python
fig, (ax0, ax1) = plt.subplots(1, 2, figsize=(14,7), sharey=False)
###Set plot for Avg_order_value
sns.barplot(data=segment_potential, x='Segment', y='Avg_order_value',hue = 'Year',palette='tab10', ax=ax0)
ax0.set_title('Avg_order_value by Segment', fontsize=14)
ax0.set_xlabel('Segment')
ax0.set_ylabel('Value')
ax0.tick_params(axis='x', rotation=-45)
for p in ax0.patches:
    if p.get_height() > 0:
      ax0.annotate(format(p.get_height(), '.2f'),
                     (p.get_x() + p.get_width() / 2., p.get_height()),
                     ha='center', va='center',
                     xytext=(0, 5),
                     textcoords='offset points')


###Set plot for Avg Sales by Segment
sns.barplot(data=segment_potential, x='Segment', y='Sales_mean',hue = 'Year', palette='plasma', ax=ax1)
ax1.set_title('Avg Sales by Segment', fontsize=14)
ax1.set_xlabel('Segment', fontsize=12)
ax1.set_ylabel('Sales Mean', fontsize=12)
ax1.tick_params(axis='x', rotation=-45)
for p in ax1.patches:
    if p.get_height() > 0:
      ax1.annotate(format(p.get_height(), '.2f'),
                     (p.get_x() + p.get_width() / 2., p.get_height()),
                     ha='center', va='center',
                     xytext=(0, 5),
                     textcoords='offset points')

plt.tight_layout()
plt.show()
```



![download (3)](https://github.com/user-attachments/assets/09bbc969-0e16-482c-839e-fcd9fab9efb7)

**Conclude:** Although the average sale is down, the value of each order is high. Customers tend to buy fewer products but the value of each product is high. It is necessary to add more products at average prices or launch promotions to attract customers to come back to shop. In addition, the company should launch promotions as well as reduce the value of each order to be more balanced.

```python
fig, (ax0) = plt.subplots(1, figsize=(12, 6))
ax1 = ax0.twinx()
# Bar plot (Total Sales)
sns.barplot(data=segment_potential.sort_values('Sales_sum'),
            x='Segment',
            y='Sales_sum',
            hue='Year',
            palette='tab10',
            ax=ax0)

# Line plot (Sales Rate)
sns.lineplot(data=segment_potential.sort_values('Rate_sale'),
             x='Segment',
             y='Rate_sale',
             marker='o',
             color='red',
             markersize=5,
             ax=ax1,
             legend=False)

# Formatting
ax0.set_title('Total Sales by Segment', fontsize=14)
ax0.set_xlabel('Segment')
ax0.set_ylabel('Total Sales')

ax1.set_title('Sales Rate by Segment', fontsize=14)
ax1.set_xlabel('Segment')
ax1.set_ylabel('Sale Rate (%)')

ax1.tick_params(axis='x', rotation=90)

plt.tight_layout()
plt.show()
```

![download (4)](https://github.com/user-attachments/assets/743456c4-6678-499d-8cbf-4778481e5e11)




- The Champions segment maintains the highest sales and sale rate, emphasizing its strong purchasing power and engagement.
- Loyal Customers demonstrate moderate sales growth but a relatively lower sale rate, showing potential for retention strategies.
- Potential Loyalists have the lowest sale rate, indicating they need targeted engagement efforts to boost frequency.


**Recommendation**
- Increase engagement with Champions → Exclusive rewards and priority access can sustain their loyalty.
- Enhance retention strategies for Loyal Customers → Upselling opportunities and personalized offers can improve sales.
- Boost Potential Loyalists' purchasing frequency → Re-engagement campaigns can encourage more transactions.


#### 📜Non Loyal Segment

```python
fig, (ax0, ax1) = plt.subplots(1, 2, figsize=(14,7), sharey=False)
###Set plot for Avg_order_value
sns.barplot(data=seg_non_potential, x='Segment', y='Avg_order_value',hue = 'Year',palette='tab10', ax=ax0)
ax0.set_title('Avg_order_value by Segment', fontsize=14)
ax0.set_xlabel('Segment')
ax0.set_ylabel('Value')
ax0.tick_params(axis='x', rotation=-90)
for p in ax0.patches:
    if p.get_height() > 0:
      ax0.annotate(format(p.get_height(), '.2f'),
                     (p.get_x() + p.get_width() / 2., p.get_height()),
                     ha='center', va='center',
                     xytext=(0, 5),
                     textcoords='offset points')


###Set plot for Avg Sales by Segment
sns.barplot(data=seg_non_potential, x='Segment', y='Sales_mean',hue = 'Year', palette='plasma', ax=ax1)
ax1.set_title('Avg Sales by Segment', fontsize=14)
ax1.set_xlabel('Segment', fontsize=12)
ax1.set_ylabel('Sales Mean', fontsize=12)
ax1.tick_params(axis='x', rotation=-90)
for p in ax1.patches:
    if p.get_height() > 0:
      ax1.annotate(format(p.get_height(), '.2f'),
                     (p.get_x() + p.get_width() / 2., p.get_height()),
                     ha='center', va='center',
                     xytext=(0, 5),
                     textcoords='offset points')

plt.tight_layout()
plt.show()
```

![download (6)](https://github.com/user-attachments/assets/ebab1763-1142-479d-bf85-f01f3e5247c7)

- The analysis highlights strong revenue growth in Promising and Cannot Lose Them segments, emphasizing their importance.
- At Risk customers require retention efforts, as their purchase frequency declines despite an increase in order value.
- Hibernating & Lost customers show slight engagement but need reactivation strategies to boost sales.
- Optimizing loyalty programs, upselling, and personalized campaigns will enhance customer retention and revenue growth


```python
fig, (ax0) = plt.subplots(1, figsize=(12, 6))
ax1 = ax0.twinx()
# Bar plot (Total Sales)
sns.barplot(data=seg_non_potential.sort_values('Sales_sum'),
            x='Segment',
            y='Sales_sum',
            hue='Year',
            palette='tab10',
            ax=ax0)

# Line plot (Sales Rate)
sns.lineplot(data=seg_non_potential.sort_values('Rate_sale'),
             x='Segment',
             y='Rate_sale',
             marker='o',
             color='red',
             markersize=5,
             ax=ax1,
             legend=False)

# Formatting
ax0.set_title('Total and rate Sales by Segment', fontsize=14)
ax0.set_xlabel('Segment')
ax0.set_ylabel('Total Sales')
ax1.set_xlabel('Segment')
ax1.set_ylabel('Sale Rate (%)')

ax1.tick_params(axis='x', rotation=90)

for p in ax0.patches:
    height = p.get_height()
    if height > 0:
        ax0.annotate(format(height, '.2f'),
                     (p.get_x() + p.get_width() / 2., height / 2),
                     ha='center', va='center',
                     fontsize=10, color='black',
                     fontweight='bold')


plt.tight_layout()
plt.show()
```



![download (5)](https://github.com/user-attachments/assets/0e30bc72-55a0-4b18-8f8c-f31bb806672b)

- High-value customers like Champions & Loyal Customers contribute significantly to revenue, warranting strategies that enhance retention and engagement.
- Segments like At Risk & Promising Customers show mixed signals—high sales but potential disengagement—suggesting the need for targeted retention strategies.
- Upselling and cross-selling could be leveraged to increase AOV across all segments.



## 🔎 III. Insight and Recommendations


