
## Project Overview

This project explores co-purchasing behavior in online grocery shopping using the Instacart Online Grocery Basket dataset. By analyzing over 33 million product-level transactions, we aim to uncover frequently bought-together products, helping retailers improve shelf layouts, bundle promotions, and reorder timing strategies. 

Using Apache Spark and FP-Growth, we identify high-confidence product associations and segment them by department, basket size, and shopping patterns.

---

## Dataset

We worked with the Instacart dataset from Kaggle, which includes:

- Over 3 million customer orders  
- Approximately 34 million individual product line-items  
- Six tables containing information on products, orders, aisles, departments, and order-product mappings

After merging and cleaning the raw data, we constructed a master table containing enriched, analysis-ready records of every item purchased, along with product metadata and order context.

---

## Workflow and Tools

Initial data exploration, cleaning, and model prototyping were performed locally using Dockerized Jupyter notebooks running Apache Spark. Once tested, we transitioned to AWS EMR to process the full dataset at scale. Cleaned data was stored in Amazon S3 for easy access across EMR nodes.

This hybrid approach allowed us to iterate quickly on samples while leveraging distributed computing for full-scale processing.

---

## Exploratory Data Analysis

We examined department-level volumes, reorder timing, basket size patterns, and weekday shopping behavior. Key findings included:

- Produce, Dairy & Eggs, and Snacks account for the majority of all line-items
- Clear weekly and monthly reorder rhythms
- Minimal variation in basket size or reorder rate by day of week

These insights guided our segmentation and modeling strategy.

---

## Modeling Approach

We applied FP-Growth on cleaned transaction data to extract frequent itemsets. Key steps included:

- Grouping each order into sets of products
- Running FP-Growth at product and aisle levels
- Labeling pairs as same-department or cross-department
- Segmenting results by small (≤10 items) and large (>10 items) baskets
- Analyzing in-cart sequences based on `add_to_cart_order`

---

## Key Results

- Most frequent same-department pair: Bananas + Organic Strawberries (Produce)  
- Most frequent cross-department pair: Coffee + Half-and-Half (Beverage ↔ Dairy)  
- Most common cart path transition: Produce → Frozen Fruit  
- Simulated improvements show a potential 4–6% lift in average basket value

---

## Tools Used

- Apache Spark 3.5  
- Docker + Jupyter (for local development)  
- AWS EMR (for large-scale data processing)  
- Amazon S3 (for cloud-based data storage)  
- Git & GitHub (for version control)

---

## Reference

Dataset: Instacart Online Grocery Basket Analysis — Kaggle  
https://www.kaggle.com/datasets/psparks/instacart-market-basket-analysis

