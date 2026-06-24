# Data

This folder contains the raw and processed datasets used in the Europeana India metadata project.

## Folder structure

```text
data/
├── raw/
│   └── europeana_india_dataset_1500_raw.csv
├── processed/
│   ├── europeana_india_unique_titles.csv
│   ├── europeana_india_unique_titles_transformed.csv
│   ├── europeana_india_unique_titles_enhanced_sample.csv
│   └── europeana_india_unique_titles_enhanced_top15_providers.csv
└── README.md
```

## Raw data

### `raw/europeana_india_dataset_1500_raw.csv`

This is the fixed source dataset used for the project analysis.

It contains 1,500 records collected from the Europeana API using four thematic query groups:

* geographic
* colonial
* cultural
* material

The original dataset contains eight columns:

* `query_group`
* `search_term`
* `title`
* `description`
* `subject`
* `dataProvider`
* `type`
* `country`

The dataset was designed to contain 375 records from each query group.

Because Europeana is a live service, rerunning the API collection may return different records. This stored CSV should therefore be treated as the fixed raw dataset used to reproduce the analysis.

The raw file should not be manually edited.

## Processed data

### `processed/europeana_india_unique_titles.csv`

Created by:

`notebooks/01_data_access.ipynb`

This file removes duplicate records based on the `title` field.

Expected number of records:

`245`

### `processed/europeana_india_unique_titles_transformed.csv`

Created by:

`notebooks/02_data_cleaning_and_analysis.ipynb`

This file contains the deduplicated records together with derived analytical variables, including:

* `has_description`
* `title_word_count`
* `contains_india`
* `possible_false_positive`

### `processed/europeana_india_unique_titles_enhanced_sample.csv`

Created during the initial Wikidata enrichment stage in:

`notebooks/03_wikidata_enhancement.ipynb`

This file contains the first manually checked provider-enrichment sample.

### `processed/europeana_india_unique_titles_enhanced_top15_providers.csv`

Created by the final provider-enrichment stage in:

`notebooks/03_wikidata_enhancement.ipynb`

This is the final enriched dataset used for the project interpretation.

It adds the following fields:

* `wikidata_qid`
* `wikidata_label`
* `institution_type`
* `match_status`

Expected final match-status counts:

* matched: 139
* uncertain: 28
* not_checked: 78

## Data-processing workflow

```text
Europeana API
    ↓
data/raw/europeana_india_dataset_1500_raw.csv
    ↓
01_data_access.ipynb
    ↓
data/processed/europeana_india_unique_titles.csv
    ↓
02_data_cleaning_and_analysis.ipynb
    ↓
data/processed/europeana_india_unique_titles_transformed.csv
    ↓
03_wikidata_enhancement.ipynb
    ↓
data/processed/europeana_india_unique_titles_enhanced_top15_providers.csv
```

## Data-quality limitations

The dataset has several important limitations:

* Europeana metadata varies in completeness across institutions.
* Some titles and descriptions are missing or very short.
* Search results depend on Europeana indexing and ranking.
* The term “Indian” may refer either to India or, in historical metadata, to Indigenous peoples of the Americas.
* Some source records contain outdated or colonial terminology.
* Deduplication based only on title may merge distinct objects with identical titles or retain duplicate objects with different titles.
* Wikidata matching was performed manually for selected providers and does not cover every institution.
* Records marked `uncertain` were intentionally retained where an institutional match could not be confirmed confidently.

## Reuse

The CSV files contain metadata supplied through Europeana and its contributing institutions. Individual records may have different rights or reuse conditions.

Users should consult the original Europeana record and provider information before reusing metadata or images outside this research project.

