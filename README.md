# Performance-Tuning-in-MySql

**Aim**

1. Write a query generate a table which 
   
                            •	Calculates gross_price_total and 
                            •	Retrieves pre invoice discount pct
   
    To subsequently calculate net_invoice_sales for a given financial year.

2. Optimizing the query by creating a lookup table
3. Optimizing the query by adding a extra and reducing join

**Description**

The **Gross Price** refers to the total price of a product or service before any deductions, such as taxes, discounts, or other costs, are subtracted.

A **Pre invoice Deductions** refers to a reduction or discount applied to the price of goods or services before the final invoice is issued.

**Net invoice sales** refers to the total amount of sales revenue that a company recognizes on an invoice after accounting for any deductions, such as discounts, allowances, returns, or any other reductions that might apply.

                                          Net invoice sales = Gross Price - Pre invoice Deductions
                                          


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


1. Understanding Top Markets and the strategy and plan upcoming events

2. Understanding Top Products and the strategy and plan upcoming  product events

3. Understanding Top customers and and the strategy and plan relationships with them.

4. Slice and dice data to drill down the hidden insights
