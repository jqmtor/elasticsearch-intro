# Terminology

### Full text
Full text is any kind of ordinary and unstructured text, like the value of a field in the database or this sentence.
In most cases, and by default, full text will be converted before being stored in an index.

### Analysis
The process of converting full text before storing it in an index.

### Term
The result of the analysis process. A term is an exact value that is indexed in elasticsearch.
The analysis process may result, and it oftenly does, in multiple terms.

![full_text-analysis-terms](images/full_text-analysis-terms.png)


