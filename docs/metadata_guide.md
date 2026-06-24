# Metadata Guide

## Project title

**Representations of India in Europeana Metadata**

## Creator

Shone Joseph

## Institution and course

TU Darmstadt
MA Data and Discourse Studies

## Project purpose

This project investigates how India is represented in metadata supplied by European cultural heritage institutions through Europeana.

The analysis focuses on:

* thematic search categories;
* object types;
* metadata completeness;
* contributing institutions;
* potentially ambiguous or false-positive search results;
* provider enrichment using Wikidata.

## Data source

The source records were collected from the Europeana Search API.

Europeana aggregates metadata from museums, archives, libraries, galleries, and other cultural heritage institutions.

The project uses a fixed copy of the collected data stored at:

`data/raw/europeana_india_dataset_1500_raw.csv`

## Data-access method

Records were collected programmatically using:

`notebooks/00_data_collection.ipynb`

The Europeana API key is loaded through the environment variable:

`EUROPEANA_API_KEY`

The API key is not stored in the repository.

## Collection design

The collection was organised into four thematic query groups:

### Geographic

Searches intended to retrieve records directly associated with India as a place or geographic category.

### Colonial

Searches related to British colonial rule, the British Raj, the East India Company, and colonial collections.

### Cultural

Searches related to Indian art, museum collections, exhibitions, ethnography, and South Asian cultural heritage.

### Material

Searches related to specific object or material categories such as textiles, manuscripts, photographs, maps, and prints.

The target was 375 records per query group, producing 1,500 records in total.

## Search terms

The data-collection notebook documents the exact search terms used for each thematic group.

Search terms include examples such as:

* India
* Indian
* British India
* colonial India
* British Raj
* East India Company
* Indian art
* ethnography India
* Indian textile
* Indian manuscript
* Indian photograph
* Indian map
* Indian print

## Raw dataset

File:

`data/raw/europeana_india_dataset_1500_raw.csv`

Expected size:

* 1,500 rows
* 8 columns

Original fields:

* `query_group`
* `search_term`
* `title`
* `description`
* `subject`
* `dataProvider`
* `type`
* `country`

## Processed datasets

### Deduplicated data

File:

`data/processed/europeana_india_unique_titles.csv`

Created by:

`notebooks/01_data_access.ipynb`

Records were deduplicated using the `title` field.

Expected size:

* 245 rows

### Transformed data

File:

`data/processed/europeana_india_unique_titles_transformed.csv`

Created by:

`notebooks/02_data_cleaning_and_analysis.ipynb`

Added analytical fields:

* `has_description`
* `title_word_count`
* `contains_india`
* `possible_false_positive`

### Wikidata-enriched data

Final file:

`data/processed/europeana_india_unique_titles_enhanced_top15_providers.csv`

Created by:

`notebooks/03_wikidata_enhancement.ipynb`

Added enrichment fields:

* `wikidata_qid`
* `wikidata_label`
* `institution_type`
* `match_status`

Expected match-status counts:

* matched: 139
* uncertain: 28
* not_checked: 78

## Languages and geographic scope

The metadata originates from institutions in multiple European countries and may contain several European languages.

The research topic is India, but some search results may refer to other places or communities because of ambiguous historical terminology.

The term “Indian” is especially ambiguous in older metadata. Some records may concern Indigenous peoples of the Americas rather than India.

## Metadata completeness

Metadata completeness varies substantially between records and institutions.

Possible issues include:

* missing descriptions;
* missing subject information;
* short or generic titles;
* inconsistent provider naming;
* different language conventions;
* outdated cataloguing terminology;
* inconsistent geographic labels.

## Wikidata enrichment method

Provider names were matched manually to Wikidata entities for selected high-frequency institutions.

The enrichment focused mainly on the top 15 data providers.

Each record was assigned one of the following statuses:

### `matched`

The provider was confidently matched to a Wikidata entity.

### `uncertain`

A possible match was identified, but the institution could not be verified with sufficient confidence.

### `not_checked`

The provider was outside the selected enrichment scope or had not yet been manually reviewed.

Uncertain matches were not forced into the matched category.

## Versioning and reproducibility

Europeana is a live service. Search results may change because of:

* new records;
* removed records;
* altered metadata;
* ranking changes;
* indexing updates;
* provider changes.

For this reason, the raw CSV in the repository is the authoritative source dataset for reproducing the analysis.

Notebook `00_data_collection.ipynb` documents the collection procedure but may not reproduce the exact same 1,500 records in the future.

## Ethical and interpretive considerations

Cultural heritage metadata is not neutral.

The records reflect institutional cataloguing practices, collection histories, colonial classifications, and historical naming conventions.

Important concerns include:

* colonial provenance;
* uneven representation of communities;
* outdated or harmful terminology;
* European institutional perspectives dominating the metadata;
* ambiguity in geographic and cultural labels;
* limited participation of represented communities in metadata creation.

The project analyses metadata representation rather than making claims about Indian culture as a whole.

## Rights and reuse

Europeana records may contain different rights statements depending on the contributing institution and object.

The dataset in this project is used for research and teaching.

Anyone reusing individual records, images, or descriptive metadata should check the original Europeana record and the contributing institution’s rights information.
