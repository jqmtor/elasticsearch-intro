# Mapping

As [described before](basic_concepts.md#mapping), a mapping defines how a document is mapped to the search engine.
For each type in an index, there is a mapping that describes what fields are indexed and how.
It is possible to index documents without defining a mapping, and in that case, elasticsearch will try to infer the adequate mapping for each field automatically.
In most cases, this is not enough, making it extremely useful to have a good understanding of this process.

### Define mapping

In a [previous section](basic_operations_intro.md#create-index-providing-configuration) is shown how to define the mappings for an index when creating it.
The following example shows how to define it independently

#### Request

**NOTE:** Make sure you the index already exists before issuing this request.

``` bash
curl -XPUT 'http://localhost:9200/test_index/_mapping/test_type?pretty=true' -d '
{
  "test_type" : {
    "properties" : {
      "field1" : {"type" : "string", "index" : "no" },
      "field2" : {"type" : "string", "index" : "analyzed", "analyzer" : "standard"}
    }
  }
}'
```

#### Response

```
{
  "acknowledged" : true
}
```

