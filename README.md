# Performance-Tuning-in-MySql

**Aim**

1. Write a query generate a table which 
   
                            •	Calculates gross_price_total and 
                            •	Retrieves pre invoice discount pct
   
    To subsequently calculate net_invoice_sales for a given financial year.

2. Optimizing the query by creating a lookup table
3. Optimizing the query by adding a extra and reducing join

**Description**

**Atliq** is a hardware company which manufactures electronic hardware items like PC, Laptop, Hard Drive, mouse, Keyboards, pendrives etc It has operations all over the globe.

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

1. Analyze with EXPLAIN and Check the query execution plan.
   
**Important points to consider when optimizing complex queries:**

1. **Create indexes** on columns frequently used in WHERE, JOIN, ORDER BY, and GROUP BY clauses.

2. **Avoid SELECT * (Wildcard)**
   
   Specify only the columns you need in your SELECT statement rather than using SELECT *.
   
   This reduces the amount of data transferred and processed.

3. **Optimize Joins**
   
   Ensure that the columns you're joining on are indexed.
   
   Use INNER JOIN where possible instead of OUTER JOIN if you only need matching records.
   
   Be mindful of the join order — in some cases, the order in which tables are joined can impact performance.

4. **Limit Rows (Pagination)**
   
If you only need a subset of data, use LIMIT to restrict the number of rows returned.

This is especially useful in cases of large result sets (e.g., pagination in a web app).

5. **Use WHERE Clauses Wisely**
   
Be as specific as possible in the WHERE clause to reduce the number of rows MySQL has to scan.

Avoid using functions like LIKE '%text%' or NOT IN, which can prevent indexes from being used effectively.

6. **Consider Query Execution Plan (EXPLAIN)**
   
Use the EXPLAIN keyword to analyze query performance and understand how MySQL executes your query. 

This shows how indexes are being used, the order of joins, and whether full table scans are happening.

Look for full table scans, file sort, or temporary tables that might indicate areas of inefficiency.

7. **Avoid Subqueries Where Possible**
    
Subqueries (especially in SELECT statements) can be inefficient, particularly when the result set is large.

Try to rewrite subqueries as joins, or use derived tables if appropriate.

8. **Optimize Aggregate Functions**
    
When using aggregate functions like COUNT(), SUM(), or AVG(), ensure that the data you're aggregating is filtered appropriately.

Use indexes on columns used for GROUP BY to speed up the process.

9. **Consider Query Caching**
    
MySQL has a query cache that can store the result of a query. 

For repetitive queries that don’t change frequently, query caching can speed up retrieval.

Be aware of cache invalidation when data is updated.

10. **Denormalization (When Appropriate)**
    
In some cases, denormalizing tables (storing redundant data) can help reduce complex joins and improve query speed, especially for read-heavy operations. But be cautious of the data redundancy trade-offs.

11. **Use Proper Data Types**
    
Ensure that the data types of your columns match the data you're storing (e.g., use INT instead of VARCHAR for numeric data). This saves space and reduces the overhead of type conversions.

For dates and times, use appropriate date/time types (DATE, DATETIME, etc.) instead of strings.

12. **Partition Large Tables**
 
For very large tables, partitioning can improve performance by dividing the table into smaller, more manageable pieces, making queries more efficient.

13. **Avoid Complex Expressions in WHERE Clause**
    
Expressions in the WHERE clause, such as YEAR(date_column) = 2025, can prevent the use of indexes efficiently. 

Instead, try to filter by range (e.g., date_column BETWEEN '2025-01-01' AND '2025-12-31').

14. **Use Batch Processing for Large Datasets**
    
When dealing with very large datasets, batch processing (dividing the workload into smaller chunks) can help avoid locking issues and reduce load.

15. **Optimize Temporary Tables and Sorting**
    
If MySQL has to create temporary tables or use filesort (for sorting), this can negatively impact performance. 

Consider optimizing queries to avoid these operations when possible.

16. **Limit Use of OR Conditions**
    
Using OR in queries can prevent MySQL from using indexes effectively.

If possible, break the query into multiple queries or use UNION instead.

17. **Avoid Using DISTINCT Unnecessarily**
    
The DISTINCT keyword can be computationally expensive, so avoid using it unless necessary. Sometimes, refactoring the query can eliminate the need for DISTINCT.

18. **Optimize Data Storage and Indexing**
    
Ensure that data storage is optimized by regularly optimizing and analyzing tables (OPTIMIZE TABLE), especially for large datasets.

Regularly defragment tables and indexes to ensure that query performance remains optimal.

19. **Review and Optimize Application Logic**

Sometimes the problem isn't just the query but how the application handles it. 

Ensure that application logic (such as filtering, pagination, etc.) is optimized to minimize the amount of data being queried and processed.

**Conclusion:**

Optimizing complex queries involves understanding the data structure, knowing how MySQL executes queries, and leveraging indexing, filtering, and query rewriting to improve performance. 

By examining the execution plan and considering strategies like reducing joins, limiting result sets, and properly indexing tables, you can make significant improvements to query performance. 

Always test and measure before and after optimization to confirm the improvements.



