# Sustainity

The goal of the Sustainity project is to gather all publicly available
information about sustainability of products available in stores and their
producers to allow consumers make more sustainable choices.

# Files

This repository contains some of the source files used for generating the
database for the Sustainity project.

## `origin` directory

The `origin` directory contains files provided by organizations certifying
products or companies (usually ecolabels). Those are the original files copied
"as is" from the Internet.

 - `bcorp.csv` - data about the B-Corporations (source: [https://data.world/
blab/b-corp-impact-data](https://data.world/blab/b-corp-impact-data))

 - `eu_ecolabel_products.csv` - data from the EU eco-label. (source: [https://
data.europa.eu/data/datasets/eu-ecolabel-products](https://data.europa.eu/data/
datasets/eu-ecolabel-products))

## `source` directory

The `source` directory contains data gathered by our team. Those data either:

 - are partial data from certifying organizations that do not provide their data
in an easy to process format or

 - are supplementing data for helping our software to understand third-party
data that are not well structured.

### `source/fashion_transparency_index.yaml`

Data from Fashion Transparency Index gathered from their [2023 report](https://
www.fashionrevolution.org/about/transparency/).

The data is stored in YAML format as a list of entries with the following
fields:

- `name` - name of the fashion company (as in the reports summary)

- `wiki` - ID of the Wikidata entry about that company

- `score` - overall score of that company (from `0` for `100`)

### `source/matches.yaml`

When processing our data, we have to decide if companies or products from
various sources are the same entities or not. If the data source provides their
ID (e.g. GTIN or tax identification number) our job if easy, but frequently all
we have is their name, which is not unique (two different companies may have
the same name; one product may be known under different names). In that case we
try to match them to entries in Wikidata which contains information about many
companies and products, including their alternative names. The matching process
is time and energy consuming, so in the future we would like to get rid of it
(see the "Future" section), but for now we need it, and all the matches (from a
name to Wikidata ID) together with their accuracy we store in this file.

The data is stored in YAML format as a list of entries with the following
fields:

 - `name` - lowercase matched name (of a company or a product)

 - `ids` - list of Wikidata IDs with the highest similarity

 - `similarity` - measure of certainty that the matched Wikidata entries are
correct (from `0.0` to `1.0`)

In practice we take as matches only entries with only one matched Wikidata entry
and `similarity` scores very close to `1.0`.

### `source/open_food_facts_countries.yaml`

In our application we allow users to filter proposed alternatives by a region
where those products are available to buy. Many of the products in our database
come from Open Food Facts. They provide in their data a tag with countries where
products are available, but this tag is not structured (they probably allow
their users to enter any (even non-sense) value). We need to be able to tell what
tags correspond to what countries. This file provides that mapping.

This file can be updated using `condenser update` command, but the mapping needs
to be created manually.

The data is stored in YAML format as a list of entries with the following
fields:

 - `tag` - country tag as in the Open Food Facts data

 - `regions` - Sustainity regions corresponding to the tag. This field may have
three types:
   - `all` - (no type annotation needed) the product is available world-wide
   - `null` - (no type annotation needed) mapping to Sustainity region was not
assigned yet
   - list of countries where the product is available given as a [two-letter
code](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) - (annonated with
`list`)

 - `count` - number of Open Food Facts entries with this tag

### `source/sustainity_library.yaml`

This file provides entries for the "library" section of the Sustainity web-page
containing various articles (mainly about the Sustainity itself and on our data
sources).

The data is stored in YAML format as a list of entries with the following
fields:

 - `id` - ID of this entry in the database. This is also name of the markdown
file in `library` directory containing the article text

 - `title` - title of the article

 - `summary` - a very short summary of the article used in the UI as a subtitle

### `source/tco.yaml`

TCO certifies electronic products. They do not provide their data in a
structured and open form. While TCO certifies products, in this file we gather
only companies which have at least one product certified (extracting each
product from their web-page manually and maintaining whole such dataset would be
too much work).

The data is stored in YAML format as a list of entries with the following
fields:

 - `tco` - name of a company as displayed on the TCO web-page

 - `wiki` - ID of a Wikidata entry corresponding to that company

## `library` directory

The `library` directory contains markdown files containing various articles
displayed on the Sustainity web-page.

# Future

Our goal is to process as much data as possible to provide as detailed
information to our users as possible. Hence, in the future manual data
preparation won't we possible. We plan to introduce a protocol and a file schema
that will allow

 - producers to share with us data about their products

 - certifiers to share with us details of their company and product
certifications.

