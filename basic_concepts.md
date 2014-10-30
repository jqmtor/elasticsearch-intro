# Basic concepts

Elasticsearch is a flexible search and analytics engine. Here is a list of its main features:
- Near real-time - there is a latency of approximately one second from the time a document is indexed until it becomes searchable;
- Distributed - built to scale horizontally with minimal effort;
- Highly available - clusters have the capability of removing failed nodes and reorganize themselves to ensure availability;
- Conflict management - optimistic version control can be used where needed;
- Full text search - multi-language, powerful query language, geolocation, context aware did-you-mean suggestions, autocomplete;
- Schemaless
- RESTful-ish
- Lucene-based
- Open source

### Full text, analysis and terms

The following figure illustrates how the concepts relate to each other.

![Analysis](images/analysis.png)

Full text is any kind of ordinary and unstructured text, like the value of a field in the database or this sentence.
By default, full text is converted into terms, through a process called analysis.
It is this process, both at index time and search time, that allows elasticsearch to perform full text queries.

### Index

An [index](#index) is like a *database* in a relational database. It contains one or more [types](#type), which are defined using a [mapping](#mapping).

### Type

A [type](#type) is like a *table* in a relational database. It has a list of [fields](#field) that can be specified for [documents](#document) of that type.

### Field

A [field](#field) is like a *column* in a relational database. It is a key-value pair that belongs to a [document](#document).
The value of a [field](#field) can be a scalar value (e.g. a string, integer or date) or a nested structure like an array or an object.

### Document

A [document](#document) is like a *row* in a relational database and it is represented by a JSON document that is stored in elasticsearch.

### Mapping

A [mapping](#mapping) is like a *schema definition* in a relational database.
Each [index](#index) defines a [mapping](#mapping) which defines each [type](#type) within the [index](#index) and a number of index-wide settings.
It is the mapping that defines how a document should be mapped to the search engine, i.e., it defines what fields are indexed and if/how they are analyzed.

