# Indexation

## Create index

Elasticsearch favors convention over configuration, making it possible to perform most operations without including any configuration at all.

### Create index with default configuration

#### Request

``` bash
curl -XPUT 'http://localhost:9200/test_index?pretty=true'
```

In this case, an index named ```test_index``` should be created. The ```pretty``` parameter tells elasticsearch to provide the response in a human readable format.

#### Response

``` json
{
  "acknowledged" : true
}
```

Note that if the index already exists, an error response would be returned:

``` json
{
  "error" : "IndexAlreadyExistsException[[test_index] already exists]",
    "status" : 400
}
```

### Create index providing configuration

There is a large set of possibilities to configure an index and all the information is described [here](http://www.elasticsearch.org/guide/en/elasticsearch/reference/current/index-modules.html).
This example includes only a few options.

#### Request

``` bash
curl -XPOST localhost:9200/other_test?pretty=true -d '
{
  "settings" : {
    "number_of_shards" : 1
  },
  "mappings" : {
    "type1" : {
      "properties" : {
        "field1" : { "type" : "string", "index" : "not_analyzed" },
        "field2" : { "type" : "double", "index" : "no" }
      }
    }
  }
}'
```

#### Response

``` json
{
  "acknowledged" : true
}
```

This example shows that it is possible to define mappings for an index when creating it.
Although, it is also possible to define them in an independent request, as explained in [other section](mapping.md).


## Index a document

#### Request

```

```

#### Response

```

```

