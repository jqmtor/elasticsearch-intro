# Analysis

Analysis is the process of converting full text into terms and the entity responsible to perform the conversion is an analyzer.
Depending on the analyzer used, the resulting terms will probably be different.
The choice of the right analyzer is extremely important, as it determines how a certain piece of text will be searchable.

An analyzer is composed of a single tokenizer and zero or more token filters.

![Analysis focus](images/analysis_focus.png)

### Tokenizer

A tokenizer breaks a string down into a stream of tokens. The [whitespace tokenizer](http://www.elasticsearch.org/guide/en/elasticsearch/reference/current/analysis-whitespace-tokenizer.html) for example, divides text at whitespace.
A full list of the tokenizers is available [here](http://www.elasticsearch.org/guide/en/elasticsearch/reference/current/analysis-tokenizers.html).

### Token filter

A token filter receives a stream of tokens from a tokenizer and modifies them. [Lowercasing](http://www.elasticsearch.org/guide/en/elasticsearch/reference/current/analysis-lowercase-tokenfilter.html), [remove stop words](http://www.elasticsearch.org/guide/en/elasticsearch/reference/current/analysis-stop-tokenfilter.html) or [ascii folding](http://www.elasticsearch.org/guide/en/elasticsearch/reference/current/analysis-asciifolding-tokenfilter.html) are just some examples.
A full list of token filters is available [here](http://www.elasticsearch.org/guide/en/elasticsearch/reference/current/analysis-tokenfilters.html).

### Testing analyzers

Elasticsearch provides an endpoint for testing analyzers against a certain piece of text.
It is extremely useful to test your analyzers to understand whether they are adequate for your use cases, or why a certain piece of text is not being indexed as you expected.

#### Request

``` bash
curl -XGET 'localhost:9200/_analyze?analyzer=standard&pretty=true' -d 'this is a test'
```

#### Response

``` json
{
  "tokens" : [ {
    "token" : "this",
    "start_offset" : 0,
    "end_offset" : 4,
    "type" : "word",
    "position" : 1
  }, {
    "token" : "is",
    "start_offset" : 5,
    "end_offset" : 7,
    "type" : "word",
    "position" : 2
  }, {
    "token" : "a",
    "start_offset" : 8,
    "end_offset" : 9,
    "type" : "word",
    "position" : 3
  }, {
    "token" : "test",
    "start_offset" : 10,
    "end_offset" : 14,
    "type" : "word",
    "position" : 4
  } ]
}
```

