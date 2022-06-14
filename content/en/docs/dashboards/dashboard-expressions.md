---
title: Dashboard Example Expressions
slug: dashboard-expressions
description: Using common dashboard expressions
date: 2022-06-07T07:39:48
---

## Description


Data in dashboards can be augmented with expressions.  There are two primary types of expressions, metrics and calculated columns.  Both can be written and modified with PostgreSQL-flavored SQL.

## Navigating to a dataset
In order to view and edit metrics and calculated expressions, perform the following steps:
1.  Sign into plaidcloud.com and navigate to dasboards
2.  From within visualize.plaidcloud.com, navigate to Data > Datasets
3.  Search for a dataset to view or modify
4.  Modify the dataset by hovering over the `edit` button beneath `Actions`

Each dataset will contain a section for Metrics and a section for Calulated Columns.


## Metrics
Metrics are expressions that are typically used to describe a field, including how it will be consolidated.

### Examples
A simple count
```
COUNT(*)
```

min
```
min("MyColumnName")
```

max
```
max("MyColumnName")
```

coalesce (useful for converting nulls to 0.0, for instance)
```
coalesce("BaselineCost",0.0)
```

divide, with a hack for avoiding DIV/0 errors
```
sum("so_infull")/(count(*)+0.00001)
```
{{<note>}}
A better way to do this would be to check for a null or zero denominator and then coalese to zero rather than attempting the division.
{{</note>}}



Conditional statement
```
CASE WHEN "Field_A"= 'Foo' THEN max(coalesce("Value_A",0.0)) - max(coalesce("Value_B",0.0)) END


## Calculated Columns
Calculated columns are typically additional columns made by combining logic and existing columns.

Convert a date to text
```
to_char("week_ending_sol_del_req", 'YYYY-mm-dd')
```


