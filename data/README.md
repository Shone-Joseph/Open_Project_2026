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
│   ├── europeana_india_unique_titles_enhanced_top15_providers.csv
│   └── europeana_india_unique_titles_enhanced_extended.csv
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

This is the top-15-provider enriched dataset.

It adds the following fields:

* `wikidata_qid`
* `wikidata_label`
* `institution_type`
* `match_status`

Expected match-status counts at this stage:

* matched: 139
* uncertain: 28
* not_checked: 78

### `processed/europeana_india_unique_titles_enhanced_extended.csv`

Created by:

`notebooks/04_relevance_review.ipynb`

This is the final enriched dataset used for the project interpretation. It extends the Wikidata enrichment to a further set of frequent providers, manually reviews the records flagged as possible false positives, and adds metadata-completeness indicators alongside clickable Wikidata links.

It adds the following fields, in addition to those listed above:

* `provider_enrichment_notes`
* `record_relevance_status`
* `relevance_notes`
* `has_subject`
* `has_country`
* `description_word_count`
* `provider_is_enriched`
* `enrichment_scope`
* `wikidata_url`

Expected final match-status counts:

* matched: 188
* uncertain: 0
* not_checked: 54
* needs_manual_review: 3

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
    ↓
04_relevance_review.ipynb
    ↓
data/processed/europeana_india_unique_titles_enhanced_extended.csv
```

## Data-quality limitations

The dataset has several important limitations:

* Europeana metadata varies in completeness across institutions.
* Some titles and descriptions are missing or very short.
* Search results depend on Europeana indexing and ranking.
* The term “Indian” may refer either to India or, in historical metadata, to Indigenous peoples of the Americas.
* Some source records contain outdated or colonial terminology.
* Deduplication based only on title may merge distinct objects with identical titles or retain duplicate objects with different titles.
* Wikidata matching was performed manually and does not cover every institution: 54 records remain `not_checked` and 3 remain `needs_manual_review` in the final dataset.
* Records marked `uncertain` or `needs_manual_review` were intentionally retained where an institutional match could not be confirmed confidently.
* The `subject` field is empty for all 245 records, limiting reliance on Europeana's own subject classification.
* The manual relevance review covered only the 17 records flagged as possible false positives; the remaining 228 records were not individually re-verified as India-related.

## Reuse

The CSV files contain metadata supplied through Europeana and its contributing institutions. Individual records may have different rights or reuse conditions.

Users should consult the original Europeana record and provider information before reusing metadata or images outside this research project.
