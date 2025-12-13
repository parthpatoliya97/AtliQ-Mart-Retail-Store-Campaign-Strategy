# Retail-Store-Campaign-Strategy

```sql
-- top 10 store based on incremental revenue generated from after promotions ?
SELECT 
    s.store_id,
    SUM(fe.base_price * fe.`quantity_sold(before_promo)`) AS revenue_before_promo,
    SUM(fe.base_price * fe.`quantity_sold(after_promo)`)  AS revenue_after_promo,
    SUM((fe.`quantity_sold(after_promo)` - fe.`quantity_sold(before_promo)`) * fe.base_price) 
        AS incremental_revenue
FROM fact_events fe
JOIN dim_stores s 
    ON fe.store_id = s.store_id
GROUP BY s.store_id
ORDER BY incremental_revenue DESC
LIMIT 10;
```



