# Performance-Tuning-in-MySql-for-Identifying-Top-Products-Markets-and-Customers

**Aim**

Generate a Report to get -

1. Calculate Net Sales (in millions)
2. Top markets by fiscal year
3. Top products by fiscal year
4. Top customers by fiscal year
5. Performance tuning of the complex queries

**Calculate Net Sales:**

The **Gross Price** refers to the total price of a product or service before any deductions, such as taxes, discounts, or other costs, are subtracted.

A **Pre invoice Deductions** refers to a reduction or discount applied to the price of goods or services before the final invoice is issued.

**Net invoice sales** refers to the total amount of sales revenue that a company recognizes on an invoice after accounting for any deductions, such as discounts, allowances, returns, or any other reductions that might apply.

                                          Net invoice sales = Gross Price - Pre invoice Deductions
                                          
**Post invoice Deductions** are reductions made to the amount due on an invoice after it has been issued. These deductions usually occur after the sale has been completed and the invoice has been sent, and they can be due to various volumne discounts, returns, product defects, shipping delays etc.

**Net sales** refers to the total revenue a company generates from selling goods or services after accounting for all deductions such as discounts, returns, allowances, and any other adjustments. It represents the actual sales the company made and is an important metric for understanding the business's true revenue.

                                          Net Sales = Net invoice Sales - Post invoice Deductions

**ETL (Extract Transform Load) Process**

Data is imported from Atliq Database

**Dimension tables** : 
1. dim_customer (customer_code, customer, platform, market, sub_zone, region)
2. dim_product (product_code, division, segment, category, product, variant)

**Fact tables/Transaction tables** : 

1. fact_sales_monthly (monthly aggregated data in start of the month date, product_code, customer_code, sold_quantity )
2. fact_freight_Cost (market, fiscal_year, freight_pct, other_cost_pct)
3. fact_gross_price (product_code, fiscal_year, gross_price)
4. fact_manufacturing_cost (product_code, cost_year/fiscal_year, manufacturing_cost)
5. fact_post_invoice_deductions (customer_code, product_code, date, discounts_pct, other_deductions_pct)
6. fact_pre_invoice_deductions (customer_code, fiscal_year, pre_invoice_discount_pct)

=======================================================================
                     

**Recommendations**

Use Report to

1. Understand monthly sales of customers and identify last sales months and strategize to improve sales  

2. Understand yearly sales of customers to get Year over year change percentage and plan accordingly

3. Quickly get the market performance by determining market badge

4. Slice and dice data to drill down the hidden insights
