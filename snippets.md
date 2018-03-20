Opencart 1.5.6.4
================

* check duplicate accounts, show orders by customer_id

```sql
SELECT 
  c.email, 
  COUNT(c.customer_id) as total, 
  GROUP_CONCAT(CONCAT(o.customer_id, ' - ', c.email, ' - ', c.date_added, ' - ', total_order)) 
FROM 
  oc_customer c 
  JOIN (
    SELECT 
      customer_id, 
      COUNT(order_id) as total_order 
    FROM 
      oc_order 
     GROUP BY customer_id) as o 
  ON o.customer_id = c.customer_id 
WHERE 
  c.date_added > '2018' 
GROUP BY 
  c.email 
HAVING 
  total > 1
```
