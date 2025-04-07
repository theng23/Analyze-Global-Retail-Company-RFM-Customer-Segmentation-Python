# Python_RFM_Analysis-Customer-segmentation
Please see the coding file attached or reach this link: [RFM_Project_Python](https://colab.research.google.com/drive/17Dlv4VH-F0KqEzzVcZJPbQCjav0JJ4wl#scrollTo=M3_yuk2uBScA)

## I. Introduction
### 1. Business Question 
- SuperStore is a global retail company. The Marketing Department wants to run marketing campaigns during the Christmas and New Year holidays to thank customers for their past support of the company. In addition, potential customers can be upgraded to become loyal customers.
- The Marketing Director proposed a plan to run RFM Model in Python to segment customers and then launch appropriate marketing campaigns.
- Recommendation for Marketing and Sales Team: With the company's retail model, which of three indicators R,F,M shoulde be given the most attention?
### 2. Dataset
This is a file database in this topic: [**Dataset**](https://drive.google.com/drive/u/0/folders/1hguyL961Nfi8AeCFeq-3dzHdGOkhTHkS)
- Ecommerce retail: <br>
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
  
- Sementation: <br>
    | Field Name | Data Type | Description |
    |-------|-------|-------|
    |Segment|STRING|Segment of Customer|
    |RFM Score|STRING|Score of RFM|

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

## III. Insight and Recommendations
1.  Recency, Frequency and Monetory value of Superstore:
    - Recency: Mean (91.52), customers made their last purchase around 92 days ago, with the median being much lower (50 days). This suggests a core group of customers has engaged recently, but there are many who haven't purchased in a long time.
    - Frequency: Mean (89.39), customers purchase frequently; however, the median (41) is significantly lower, indicating a wide gap between a few very active customers (outliers) and the rest.
    - Monetary: Mean (2,038.38), average customer spending is high but is skewed by outliers, as the median is only 658.64.
2. Segments of Superstore:
- Loyal Segment
    - Saler and Order Value
        - Performance Segment:
            - Champions Segment increased modestly from 366,393.54 to 424,450.01 (2010-2011).
            - Loyal Segment growth from 45,988.35 (2010) to 77,415.45 (2011) shows positive momentum in this group.
            - Potential Loyalist Segment grew from 12,799.95 (2010) to 23,627.03 (2011).
              
          **Recommendations**: Focus on Champions and Loyal Segments with loyalty programs, exclusive offers, and personalized experiences to maintain engagement and ensure continued revenue contribution. Enhance campaign to promote more in Potential Loyalist group.
        - Average order values increased almost all the time from 2010 to 2011.
            - Champions have the most highest value between 2010 and 2011.
            - Potential Loyalist grow up slightly from 193.93 to 234.12.
    
          **Recommendations**: That is usually a positive sign. Marketing and Sale team should to focus on this groups.
        - Average Sales decreased almost all the time beside Potential Loyalist.
            - Champions still have the most highest Sales Mean with 26.25 however this segment drop slightly to 24.14 in 2011.
            - Meanwhile Potential Loyalist grew up from 8.95 to 9.73 from 2010 to 2011.
      
           **Recommend**: Company should to run campaign to attract this customers. If this trend continues, it could lead to a decrease in overall sales as customers do not return to buy as often.
    
    - Total Quantity and Order Per Unit
        - Total Quantity increased sharply over the years (2010-2011)
            - Champions: From 195,416 (2010) to 2,903,785 (2011) – a huge increase.
            - Loyal dramatically increased from 26630 to 555183.
            - Potential Loyalist rose sharply from 6507 to 177747
          
        **Recommendations**
            - An increasing trend in total Quantity is a good sign that the business is effectively attracting customers.
            - Potential Loyalist has low purchase volume, increase incentives and customer care to retain them.
            - Need to expand strategy to other segments to reduce risk and grow sustainably.
    - Order Per Unit decreased slightly during period year
        - Potential Loyalist decline dramatically from 1.01% to 0.68%
        - Champions and Loyal drop minimally 0.38% to 0.31% and 0.44% to 0.37%
      
            **Recommendations**
            - Customers buying more products in the same order can bring more revenue to the company but this reduces customer interaction when combining many orders like that.
            - It is necessary to have more promotions as well as increase customer interaction with more products.
            - Need to optimize operations and delivery processes to better handle large orders.
            - Beside, ensure that profit margins are not excessively reduced as customers switch to bulk buying behavior.
              
- Non Loyal
    - Sale and Order Value
        - Total Sales by Segment
            - Massive Growth in Total Sales Across Segments (2011):
            - At Risk: From 79,162.41 (2010) to 583,741.25 (2011)—a huge increase. However, these customers are still at risk, so continuous attention is crucial.
            - Cannot Lose Them: Sales grew nearly tenfold, from 27,508.62 (2010) to 267,359.44 (2011). This segment clearly holds immense potential, reinforcing their critical role in revenue generation.
            - Total Sale of At Risk, Need Attention, Promising, Hibernating customers is larger than total sale of Potential Loyalist in 2010-2011. Can further evaluate the segmentation of customer groups that can become Loyal Segments
        - Avg_order_value by Segment
            - Promising Segment: The average order value jumped significantly from 317.32 (2010) to 827.80 (2011). This indicates that customers in this segment may be responding well to higher-value products or pricing strategies.
            - Cannot Lose Them Segment: Although this segment only appears in 2011 with an extremely high avg_order_value of 1291.59, its introduction could represent a strategy to identify and retain high-value customers.
            - Need Attention & At Risk Segments: Both segments experienced steady growth in avg_order_value, suggesting a positive response from these customers to improved product offerings or pricing strategies.
            - Hibernating, Lost, and About To Sleep Segments: These segments saw modest increases, signaling that while they are engaging more with higher-value purchases, they remain less responsive compared to other segments.
        - Avg Sales by Segment
            - Promising Segment: Sales mean skyrocketed from 81.36 (2010) to 146.82 (2011), reflecting an increase in purchasing activity.
            - Cannot Lose Them Segment: The sales mean rose dramatically from 28.30 (2010) to 74.60 (2011), reinforcing the importance of this high-value group.
            - At Risk Segment: Despite avg_order_value increasing, sales mean decreased from 19.93 (2010) to 15.25 (2011), indicating a decline in purchase frequency or basket size.
            - About To Sleep & New Customers: Both experienced a drop in sales mean, suggesting reduced purchasing activity, which could indicate disengagement.
              
    - Recommendation:
        - Strengthen Loyalty for High-Potential Segments
            - Prioritize Cannot Lose Them and Promising Segments with personalized offers, loyalty programs, and premium experiences.
            - Implement cross-sell and upsell strategies to maximize revenue from these engaged groups.
        - Focus on High-Potential Segments
            - Promissing Segment:
                - PLeverage their growth momentum by introducing loyalty programs or exclusive offers.
                - Expand product to targeted at this segment's preferences
            - Cannot Lose Them Segment:
                - Invest in personalized marketing stratedgies and prioritize customer service for this group
            - Strengthen Retention Strategies for Hibernating & Lost Customers
                - Offer campaigns aimed at reactivating these segments, discounts or exclusive sales.
                - Analyze their purchasing history to identify products that previously resonated with them and highlight these in campaigns.
            - Re-engage Declining Segments
                - Investigate reasons for declining sales mean through surveys or feedback campaigns.
                - Reconnect with customers through personalized offers or incentives to reactivate engagement.
    - Total Quantity and OPU
        - Significant Growth in Total Quantity:
            - All customer segments show a notable increase in total quantity from 2010 to 2011, particularly:
            - At Risk: From 28,825 to 360,182 (over 10x growth).
            - Need Attention and Promising: Both segments also exhibit large jumps in order volumes.
        - Order Per Unit by Segment:
            - The Lost Customers segment consistently has the highest "order per unit" ratio, increasing from 1.13 (2010) to 1.19 (2011), suggesting effective retention or focused engagement strategies for this group.
            - The At Risk and Cannot Lose Them segments see a decrease in the "order per unit" ratio.
            - New Customers experienced a significant drop in their order-per-unit ratio from 1.50 in 2010 to 0.85 in 2011
    - Recommendations:
        - Focus on Retaining High-Value Segments
            - Target At Risk and Cannot Lose Them customers with personalized promotions or loyalty incentives to address the declining order-per-unit trend.
            - Use tailored communication to re-engage Need Attention customers who show growth potential.
        - Improve Efficiency for New Customers
            - Implement onboarding campaigns or early-stage rewards to increase engagement and orders-per-unit for New Customers.
        - Leverage Insights from Top Performers
            - Investigate what works well with Lost Customers who have the highest efficiency, and apply similar techniques to lower-performing groups.

