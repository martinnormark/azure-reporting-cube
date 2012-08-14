Windows Azure Reporting Cube
====================

POC and concept of using Windows Azure Table Storage to store denormalized, query optimized data.

## Preface
It's a well known fact that relational databases are not suited fast querying when they're normalized (even 2nd or 3rd normal form) and they contain huge amounts of data.

A common approach to solve this issue, is to de-normalize data into cubes that contains aggregated records of data, optimized for a specific report and queryable by date range, related IDs etc.

There's still a few concepts of relational databases that doesn't fit the de-normalized query model.

So I thought I'd try a little experiment using Windows Azure Table Storage to store de-normalized, queryable data and see how well it performs.

Table Storage is extremely cheap, and can store an almost endless amount of data.

With the description of the concept, bits of a small POC or tests will be build around a web analytics/tracking application.

## Concepts

* [Data model of a simple web analytics app] (https://github.com/martinnormark/azure-reporting-cube/blob/master/docs/Data%20model.md)
* [From input data, to de-normalized cube] (https://github.com/martinnormark/azure-reporting-cube/blob/master/docs/Data%20transformation.md)
* [What to use as `PartitionKey`?] (https://github.com/martinnormark/azure-reporting-cube/blob/master/docs/Partition%20keys.md)
* [What to use as `RowKey`?] (https://github.com/martinnormark/azure-reporting-cube/blob/master/docs/Row%20keys.md)
* [Querying a range of metrics] (https://github.com/martinnormark/azure-reporting-cube/blob/master/docs/Querying%20metrics.md)