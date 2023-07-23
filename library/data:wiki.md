# Description

Wikidata is a free, collaborative, multilingual, secondary database
that collects structured data to provide support for Wikipedia and other Wikimedia projects.
It is a document-oriented database focused on items, which represent any kind of topic, concept, or object,
and each item is allocated a unique, persistent identifier known as a "QID".

Here are three key points about Wikidata:

 - **Multilingual**: Wikidata is a multilingual database, which means that it can be used to store and
   retrieve information in many different languages.
 - **Collaborative**: Wikidata is a collaborative project that allows anyone to contribute to the database
   by adding, modifying, or deleting information.
 - **Structured data**: Wikidata is designed to manage large amounts of structured data,
   which means that the information is organized in a way that makes it easy to search, analyze, and use.

# Data sources

Wikidata is a huge knowledge graph database.
It provides [a variety of APIs](https://www.wikidata.org/wiki/Wikidata:Data_access) to access the data.
Since we need to scan all of the the entries,
we use [their database dumps](https://www.wikidata.org/wiki/Wikidata:Database_download)
which are updated periodically and
can be downloaded from [here](https://dumps.wikimedia.org/wikidatawiki/entities/).
It's worth to note that even a compressed dump still contains more than 100 GB of data. 

# How we use their data

While Wikidata contains information about many companies and products,
it's far not enough to infer any sustainability or social responsibility information. 
We use it mainly as a supplementary source of information to provide some descriptions and pictures,
and combine those with data from organisations certifing products and companies.

Combination of data from Wikidata and different sources is quite cumbersome.
Ideally we should combine them only if both the certifier data and Wikidata contain some unique identifiers,
e.g. VAT number or internet domain.
However, they are either not available in Wikidata or are not provided by the certifiers in most cases.
Therefore, not many connections can be made in this way.
To find more matches we also try looking at company names, but that's not a reliable method,
because such names are not unique.
I the future we plan to:
 - suplement Wikidata with information that we found is missing
 - actively ask vertifiers to include identifiers in their data
 - actively ask companies to fill Wikidata with information about their products.
