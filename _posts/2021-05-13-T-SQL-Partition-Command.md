---
layout: post
title: T-SQl Partition Command - Simple Use Cases
categories: [T-SQl, Partition Command]
tags: [T-SQl, Partition Command, Group By]
mermaid: true 
---

## OVER (PARTITION BY `*`value_expression`*` )


>Divides the query result set into partitions. The window function is applied to each partition separately and computation restarts for each partition.



##  Use Cases

### Delete Duplicate Grouped Records (Make and Keep 1-element Groups)

assume you group your table based on Type. You only want keep one record for each group say older one.

#### using nested query:

```sql
  delete FROM table1
  where Id not in
  (
      select Id from 

      (select Id,min(CreationDateTime) 
  over(partition by [Type]) min1
   FROM table1)

   ) 
```
#### using cte:
```sql
  with cte as(
  select Id,row_number()  over(partition by [Type])  row1
   FROM table1
   where 
)
delete from cte where row1>1
```

### Other Use Cases:

It can be used to find the rank( or distant to max/min) of each row in coresponding partition or group based of defined fields.
