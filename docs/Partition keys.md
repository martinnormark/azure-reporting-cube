# What should the partition key contain?

With Windows Azure Table Storage, entities with the same `PartitionKey` [can be queried faster] [1] than those with a different `PartitionKey`.

This makes it inevitable to make the name of the cube (or maybe the report) the `PartitionKey`.

Remember that each entity should be a 'stats record' that contains a number of metrics (columns/properties) per hour that can be queried.

The stats-record might contain too many metrics for one to use for certain reports, but that should be solved by the query using [projection] [2], another Azure Table Storage feature.

[1]: https://www.windowsazure.com/en-us/develop/net/how-to-guides/table-services/#add-entity "Adding entities"
[2]: https://www.windowsazure.com/en-us/develop/net/how-to-guides/table-services/#query-entity-properties "Querying a subset of Entity Properties"