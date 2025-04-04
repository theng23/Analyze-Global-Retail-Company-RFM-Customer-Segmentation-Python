# Python_RFM_Analysis-Customer-segmentation
Please see the coding file attached or reach this link \
[RFM_Project_Python](https://colab.research.google.com/drive/17Dlv4VH-F0KqEzzVcZJPbQCjav0JJ4wl#scrollTo=M3_yuk2uBScA)

## I. Introduction
### 1. Business Question 
- SuperStore is a global retail company. The Marketing Department wants to run marketing campaigns during the Christmas and New Year holidays to thank customers for their past support of the company. In addition, potential customers can be upgraded to become loyal customers.
- The Marketing Director proposed a plan to run RFM Model in Python to segment customers and then launch appropriate marketing campaigns.
- Recommendation for Marketing and Sales Team: With the company's retail model, which of three indicators R,F,M shoulde be given the most attention?
### 2. Dataset
This is a file database in this topic: [**Dataset**](https://drive.google.com/drive/u/0/folders/1hguyL961Nfi8AeCFeq-3dzHdGOkhTHkS)
- Ecommerce retail: <br>
    | Field Name | Data Type |
    |-------|-------|
    |InvoiceNo|STRING|
    |StockCode|STRING|
    |Description|STRING|
    |Quantity|INTEGER|
    |InvoiceDate|DATETIME|
    |UnitPrice|FLOAT|
    |CustomerID|STRING|
    |Country|STRING|
  
- Sementation: <br>
    | Field Name | Data Type |
    |-------|-------|
    |Segment|STRING|
    |RFM Score|STRING|

### 3. RFM Model
- RFM is a method used for analyzing customer value. It is commonly used in database marketing and direct marketing and has received particular attention in retail and professional services industries
- RFM Model
    - Recency (R): How recently a customer made a purchase. Customers who made purchases more recently are typically more engaged and likely to buy again.
    - Frequency (F): How often a customer makes purchases within a given period. Frequent buyers are usually more loyal and valuable to a business.
    - Monetary (M): How much money a customer spends in total. High spenders contribute significantly to revenue and can be prioritized for premium services or offers.
- RFM analysis numerically ranks a customer in each of these three categories, generally on a scale of 1 to 5 (the higher the number, the better the result). The “best” customer would receive a top score in every category.
## II. Data Visualization with Python
### Visulization RFM Segment
- Visualize Average Recency by RFM Segment
  
![1](https://github.com/user-attachments/assets/4d68760d-570d-4fb3-bd06-12c66551362d)
- Visualize Average Frequency by RFM Segment
  
![2](https://github.com/user-attachments/assets/0f87e06f-e58d-4bf8-95d6-218aabb5d145)
- Visualize Total Cost by RFM Segment
  
![3](https://github.com/user-attachments/assets/66b4257a-48e7-474e-ab21-4d0c24da6c95)
![4](https://github.com/user-attachments/assets/6fe8ba49-d966-4367-a169-ee2fedf3b755)
- Number of customers and Percentage by RFM Segment

![5](https://github.com/user-attachments/assets/3b87c8d3-3d21-4c90-b1b4-ea44f0c6c0b1)
### Visualize Loyal and Non Loyal Segment

- Number of customers by Loyal and Non Loyal
  
![6](https://github.com/user-attachments/assets/6037f9cd-824e-48a9-8ae7-e6d06e6aadf0)

#### Loyal Segment

![7](https://github.com/user-attachments/assets/fd5607e4-9176-42d3-8dde-460d2a255342)
![8](https://github.com/user-attachments/assets/2a4e2e27-aae2-40c0-86c2-e7d35f0729ef)
![9](https://github.com/user-attachments/assets/f62374a1-ed13-4bcb-a8ac-c272cabfd7a2)
![10](https://github.com/user-attachments/assets/0aaec1cc-48cb-4a04-9283-144060cde16e)

#### Non Loyal Segment


![11](https://github.com/user-attachments/assets/e7ca467e-0e69-40c8-b888-2f5a53755a10)
![12](https://github.com/user-attachments/assets/deea6bee-98d0-44f4-9f37-46bdd9299830)
![13](https://github.com/user-attachments/assets/c8aa4b15-755f-401a-acd0-80e8f0933dab)
