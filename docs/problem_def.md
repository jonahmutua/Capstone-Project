Project Name: StockGuide 

Project Title: 
Design and Development of an affordable sales-based inventory restocking recommendation system for small retail business.

Target users:
 Small retail businesses currently using basic POS applications, spreadsheets or manual inventory records.

Gap:
Small retail business owners often struggle to determine which product need restocking, when to place new order and how much stock to purchase. Poor restocking decisions can result in overstocking, stockouts, tied-up business capital and lost sales revenue.

Proposed Solution:
StockGuide will analyse historical products sales, current stock levels and supplier lead times to estimate future demand and recommend which products should be restocked, when to restock them and how much to purchase.

Features:
1. Simple demand-based recommendations - Generate restocking recommendations without requiring users to configure a complex ERP system.
2. Explainable recommendations - Explain why a particular product needs resttocking and how the recommendation quantity was arrived at. 


Recommendation Engine:
Step 1: 
    Calculate average daily sales ( How quickly the product sells )

    Avg Daily sales = Total units sold / Number of days
Step 2:
    Estimate Future Demand 
    Use daily says to estimate how many units customers a likely to purchase during supplier's deliverly time. 

    Expected demand = AVg daily sales * Supplier lead time

Step 3:
    Calculate Reorder point 
    This tells the business owner when to initiate new purchase.

    Reorder point = Expected demand + Safety Stock ( additional stock maintained to absorb spikes in Demand and Supplier delays)
   