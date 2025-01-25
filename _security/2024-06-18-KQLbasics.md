---
layout: post
title: "KQL basics"
categories: Security
nav_exclude: false
nav_order: 3
---

{: .text-center }
# Kusto Query Language 101


![kql1](/assets/kql1.jpg){: width="auto" height="auto" }

{: .text-center }
## <span style="color: orange; font-weight: bold;">Basics for Beginners</span>

###### IN PROGRESS ***June 18, 2024***

- KQL is designed to query large data sets, it is microsoft based & cloud native.

- WORM language (Write Once Read Many)

For security purposes, KQL is often used for queries in sentinel to find logs. This can be via many different operators in the query. Simple queries may be based around longer time frames, such as 7-30 days worth of logs, or to drill down into host events, network events and more.

- Another good resource is 'kqlsearch', which provides an assistant, generator and lab. 

> These 3 links will allow you to access a test enviroment, and the video tutorial show you how to test the upcoming Query basics.
- If you would like a more hands on example, try the links below;

LAW
```scss
https://portal.azure.com/#blade/Microsoft_Azure_Monitoring_Logs/DemoLogsBlade
```
ADX
```scss
https://kusto.azure.com/publicfreecluster
```

Tutorial
```scss
https://www.youtube.com/watch?v=8JqwHaIW_Zc
```

----

A `record` will run horizontally, Marked in the <span style="color: indianred; font-weight: bold;">red</span> boxes.

A `field` will run vertically, marked in <span style="color: royalblue; font-weight: bold;">blue</span>.

> Within that database, I queried `Products` and then used the `|` operator to also sample the top 10 results with `take`.

> ![adx2.png](/assets/adx2.png){: width="auto" height="auto" }

> 

> ![law1.png](/assets/law1.jpg){: width="auto" height="auto" }

----

# Syntax and Operators:


### `where:` Filters a table to the subset of rows that satisfy a predicate.
- the `where` and `filter` statements are equivalent in KQL

### `|` ,`pipe` Seperates multiple commands for more intensive searching.

### `and:` All conditions must be true for a record to be sampled correctly.

### `take` (also `limit`) returns a specific number of records
- example `| take 50`

### `==` equals or matches

### `!=` does not equal/does not match

### `//` (comments) allows a statement or a portion of the query *not* to be ran
- allows for additional information to be tagged along in a query to guide others or help yourself.

### `or` will produce results of records/logs based on if either condition of a command is met.
- requires at least 2 commands.

### `in` allows for multiple field selectors to be chosen within a statement.
- ex. `| where Location in ('GB', 'US', 'CA')`
- similar to multiple `or` statements but simpler. 

### `project` allows us to choose multiple or a singular field to be projected.
- ex. `| project FirstName, LastnName, Cityname, Location, StateProvinceName`
- pro-jeckt not prah-jekt

### `distinct` shows all the unique values for a field.
- an example would be `| distinct Location`
- which would return something like all the Country locations `US, CA, GB` or similar.

### `sort by` allows for sorting by a specific field or multiple fields.
- default is descending, the `asc` syntax would allow for ascending.

- an example would be `| sort by FirstName asc, LastName asc`

### `search` searches all columns in the table for the value.
- example could be a hostname, devicename, username etc.

### `contains` searches for a string within a field.
- resource heavy, but effective.
- a good example can be `| where url contains 'share'`
- capitalization doesnt matter.

# Other common Syntax and Operators:

### `has`

### `startswith`

### `endswith`

### `>`

### `<`

### `getschema`

### `time`

### `ago`

### `between` `datetime`
- ex `| where TimeGenerated between (datetime(2023-12-20) .. datetime(2024-12-12))`

### `now`

### `UTC`
 

[kql cheat sheet]: https://www.cyber.engineer/kql-cheat-sheet-the-basics/

[kql cheat sheet (microsoft)]:https://learn.microsoft.com/en-us/azure/data-explorer/kusto/query/kql-quick-reference