# Indexation

## Create index

Elasticsearch favors convention over configuration, making it possible to perform most operations without including any configuration at all.

### Create index with default configuration

#### Request

```
curl -XPUT 'http://localhost:9200/test?pretty=true'
```

In this case, an index named ```test``` should be created. The ```pretty``` parameter tells elasticsearch to provide the response in a human readable format.

#### Response

```
{
  "acknowledged" : true
}
```

Note that if the index already exists, an error response would be returned:

```
{
  "error" : "IndexAlreadyExistsException[[test] already exists]",
    "status" : 400
}
```

### Create index providing configuration

There is a large set of possibilities to configure an index and all the information is described [here](http://www.elasticsearch.org/guide/en/elasticsearch/reference/current/index-modules.html).
This example includes only a few options.

#### Request

```
curl -XPOST localhost:9200/other_test?pretty=true -d '{
    "settings" : {
        "number_of_shards" : 1
    },
    "mappings" : {
        "type1" : {
            "_source" : { "enabled" : false },
            "properties" : {
                "field1" : { "type" : "string", "index" : "not_analyzed" }
            }
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

