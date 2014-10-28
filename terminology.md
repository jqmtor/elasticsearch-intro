# Basic concepts

### Full text, analysis and terms

The following figure illustrates how the concepts relate to each other.

![full_text-analysis-terms](images/full_text-analysis-terms.png)

**Full text** is any kind of ordinary and unstructured text, like the value of a field in the database or this sentence.
By default, full text is converted into **terms**, through a process called **analysis**.
It is this process, both at index time and search time, that allows elasticsearch to perform full text queries.

### Index

An index is like a *database* in a relational database. It contains one or more types, which are defined using a mapping.

### Type

A type is like a *table* in a relational database. It has a list of fields that can be specified for documents of that type.

### Field

A field is like a *column* in a relational database. It is a key-value pair that belongs to a document.
The value of a field can be a scalar value (e.g. a string, integer or date) or a nested structure like an array or an object.

### Document

A document is like a *row* in a relational database and it is represented by a JSON document that is stored in elasticsearch.

### Mapping

A mapping is like a *schema definition* in a relational database.
Each index defines a mapping which defines each type within the index and a number of index-wide settings.
