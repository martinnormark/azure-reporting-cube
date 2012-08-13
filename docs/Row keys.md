To avoid using `Timestamp` in queries, which results in a [full table scan] [1], we need to make the row key some sort of timestamp.

Since this is aggregated data, it should indicate the endtime of the aggregation in UTC ticks e.g. `293819312323`.

But since we also want to indicate what any particular stats-record belongs to, we need to prefix the UTC ticks timestamp with object type and object id, to make it refer to another entity in an application.

So, in a web analytics application I want to store metrics for any given page. A page's object type is `page` with an ID of e.g. `34343` which makes the row key for the stats-record ending in UTC ticks of `293819312323` look like this:

`page_00000000000000034343_293819312323`

Notice how the ID has been padded with zero to make it the same length for all rows. Without padding IDs, querying by range will not be possible, so this is very important!

The stats-record stored at that location is an aggregation of several metrics for the past hour, e.g:

```javascript
{
    'ObjectType': 'page',
    'ObjectId': 34343,
    'PageViews': 54323,
    'Visits': 49834,
    'PageViewsPerVisit': 1.09007906,
    'OrganicSearchClicks': 19232,
    'PaidSearchClicks': 3421,
    'ReferrerClicks': 987,
    'EmailClicks': 329,
    ...
}
```

The above `RowKey` enables us to [query the table by range] [2] e.g:

```csharp
where fooEntity.PartitionKey == partionKey
    && fooEntity.RowKey.CompareTo(lowerBoundRowKey) >= 0
    && fooEntity.RowKey.CompareTo(upperBoundRowKey) <= 0
````

[1]: http://stackoverflow.com/a/5636080/2972
[2]: http://stackoverflow.com/a/5933042/2972