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

Elasticsearch does not require that an index exists before indexing a document.
If it doesn't, it automatically creates the index, the index type and indexes the document using the default mapping.

#### Request

``` bash
curl -XPUT 'localhost:9200/test_index/test_type/1?pretty' -d '
{
  "name": "John Doe"
}'
```

#### Response

``` json
{
  "_index" : "test_index",
  "_type" : "test_type",
  "_id" : "1",
  "_version" : 1,
  "created" : true
}
```
Note that the request above would update the document if it already existed in the index. Is is possible to force create only behavior using the ```op_type``` parameter.

### Index document with automatic ID generation

Elasticsearch allows to index documents without providing an ID, in which cases it will be generated automatically.
Indexing documents in this way is slightly different.

#### Request

```
curl -XPOST 'localhost:9200/test_index/test_type?pretty' -d '
{
  "name": "Jane Doe"
}'
```

#### Response

```
{
  "_index" : "test_index",
  "_type" : "test_type",
  "_id" : "VAtxxK79Q2mae3lsLKVoGA",
  "_version" : 1,
  "created" : true
}
```


## Retrieving the document

#### Request

``` bash
curl -XGET 'localhost:9200/test_index/test_type/1?pretty'
```

#### Response

``` json
{
  "_index" : "test_index",
  "_type" : "test_type",
  "_id" : "1",
  "_version" : 1,
  "found" : true,
  "_source": { "name": "John Doe" }
}
```

The most relevant thing to note on the response is that elasticsearch indexes the document with some metadata associated.
The metadata fields are clearly identified because their names are preceded by an underscore.

The ```_source``` field is automatically generated for each document (unless you say otherwise) and corresponds to the exact document that was provided at index time.
It is not indexed (not searchable), just stored. When performing get or search requests, this field is returned by default.

