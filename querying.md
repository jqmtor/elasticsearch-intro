# Querying

## Queries and filters

- The difference between queries and filters

- Performance differences

- When to use which

## Performing query

#### Request

``` bash
curl -XGET 'http://localhost:9200/test_index/test_type/_search?pretty' -d '
{
  "query" : {
    "term" : { "name" : "john" }
  }
}'
```

#### Response

``` json
{
  "took" : 2,
  "timed_out" : false,
  "_shards" : {
    "total" : 5,
    "successful" : 5,
    "failed" : 0
  },
  "hits" : {
    "total" : 1,
    "max_score" : 0.19178301,
    "hits" : [ {
      "_index" : "test_index",
      "_type" : "test_type",
      "_id" : "1",
      "_score" : 0.19178301,
      "_source": { "name": "John Doe" }
    } ]
  }
}
```

## Filtering documents

#### Request

``` bash
curl -XGET 'http://localhost:9200/test_index/test_type/_search?pretty' -d '
{
  "filter" : {
    "term" : { "name" : "john" }
  }
}'
```

#### Response

``` json
{
  "took" : 0,
  "timed_out" : false,
  "_shards" : {
    "total" : 5,
    "successful" : 5,
    "failed" : 0
  },
  "hits" : {
    "total" : 1,
    "max_score" : 1.0,
    "hits" : [ {
      "_index" : "test_index",
      "_type" : "test_type",
      "_id" : "1",
      "_score" : 1.0,
      "_source": { "name": "John Doe" }
    } ]
  }
}
```

## Sorting

- http://www.elasticsearch.org/guide/en/elasticsearch/reference/current/search-request-sort.html#search-request-sort

- How mapping affects sorting


