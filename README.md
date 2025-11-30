# Transpaer

The goal of the Transpaer project is to gather all publicly available
information about of products available on the market and their
producers to allow consumers make choices more aligned with their values.

# Files

This repository contains some of the source files used for generating the
database for the Transpaer project.

## `origin` directory

The `origin` directory contains files provided by organizations certifying
products or companies (usually ecolabels). Those are the original files copied
"as is" from the Internet.

 - `bcorp.csv` - data about the B-Corporations (source: [https://data.world/
blab/b-corp-impact-data](https://data.world/blab/b-corp-impact-data))

 - `eu_ecolabel_products.csv` - data from the EU eco-label. (source: [https://
data.europa.eu/data/datasets/eu-ecolabel-products](https://data.europa.eu/data/
datasets/eu-ecolabel-products))

## `meta` directory

The `meta` directory contains helper data needed to process the `origin` data.
The `origin` data frequently contains entries specific to the source, e.g.
names of regions or categories. In the `meta` data we map them to the
Transpaer equivalents. This data rwquires manual editing and automated updates.

### `meta/matches.yaml`

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

## `substrate` direcotry

The `substrate` directory contains data from varioues sources originally prepared
in the substrate format.

## `support` directory

The `source` directory contains data gathered by our team. Those are partial data
from certifying organizations that do not provide their data in an easy to process format.

### `support/fashion_transparency_index.yaml`

Data from Fashion Transparency Index gathered from their [2023 report](https://
www.fashionrevolution.org/about/transparency/).

The data is stored in YAML format as a list of entries with the following
fields:

- `name` - name of the fashion company (as in the reports summary)

- `wiki` - ID of the Wikidata entry about that company

- `score` - overall score of that company (from `0` for `100`)

## `library` directory

The `library` directory contains markdown files containing various articles
displayed on the Transpaer web-page.

### `library/library.yaml`

This file provides entries for the "library" section of the Transpaer web-page
containing various articles (mainly about the Transpaer itself and on our data
sources).

The data is stored in YAML format as a list of entries with the following
fields:

 - `id` - ID of this entry in the database. This is also name of the markdown
file in `library` directory containing the article text

 - `title` - title of the article

 - `summary` - a very short summary of the article used in the UI as a subtitle

# Future

Our goal is to process as much data as possible to provide as detailed
information to our users as possible. Hence, in the future manual data
preparation won't we possible. We plan to introduce a protocol and a file schema
that will allow

 - producers to share with us data about their products

 - certifiers to share with us details of their company and product
certifications.

