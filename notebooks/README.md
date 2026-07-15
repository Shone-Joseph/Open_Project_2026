# Notebooks

This folder contains the Jupyter notebooks used for data collection, processing, analysis, and metadata enrichment.

## Recommended execution order

### 00_data_collection.ipynb

Collects records from the Europeana API using four thematic query groups:

* geographic
* colonial
* cultural
* material

The notebook saves the collected dataset to:

`data/raw/europeana_india_dataset_1500_raw.csv`

This notebook requires a Europeana API key stored in the environment variable:

`EUROPEANA_API_KEY`

Because Europeana is a live service, rerunning the data collection may return slightly different records. The raw CSV stored in the repository should therefore be treated as the fixed dataset used for the project analysis.

### 01_data_access.ipynb

Loads the raw Europeana dataset, checks its structure, examines the query-group balance, removes duplicate titles, and saves the deduplicated dataset to:

`data/processed/europeana_india_unique_titles.csv`

Expected number of unique titles:

`245`

### 02_data_cleaning_and_analysis.ipynb

Loads the deduplicated dataset, creates derived analytical variables, performs descriptive analysis, and generates figures and summary tables.

Main processed output:

`data/processed/europeana_india_unique_titles_transformed.csv`

Main figures:

* `outputs/figures/object_type_distribution.png`
* `outputs/figures/query_group_distribution.png`

Main summary tables:

* `outputs/tables/object_type_summary.csv`
* `outputs/tables/query_group_summary.csv`

### 03_wikidata_enhancement.ipynb

Loads the transformed dataset and enriches selected provider names with manually checked Wikidata identifiers and institution types.

Final enriched output:

`data/processed/europeana_india_unique_titles_enhanced_top15_providers.csv`

Expected final match-status counts:

* matched: 139
* uncertain: 28
* not_checked: 78

### 04_relevance_review.ipynb

Loads the enriched dataset produced by `03_wikidata_enhancement.ipynb` and performs a further round of provider enrichment, a manual relevance review of records flagged as possible false positives, and adds metadata-completeness indicators alongside clickable Wikidata links. Running this notebook after `03_wikidata_enhancement.ipynb` produces the final, fully enriched dataset automatically.

Final enriched output:

`data/processed/europeana_india_unique_titles_enhanced_extended.csv`

Expected final match-status counts:

* matched: 188
* uncertain: 0
* not_checked: 54
* needs_manual_review: 3 (new status, introduced in this notebook for providers that could not be confidently identified)

New columns added in this notebook:

* `provider_enrichment_notes` — documented reasoning for each provider enrichment decision
* `record_relevance_status` — relevance judgement for records flagged by `possible_false_positive`
* `relevance_notes` — reasoning for each relevance judgement
* `has_subject`, `has_country` — metadata-completeness indicators
* `description_word_count` — word count of the `description` field
* `provider_is_enriched`, `enrichment_scope` — summaries of provider-enrichment status
* `wikidata_url` — clickable Wikidata link for every row with a verified `wikidata_qid`

## Reproducibility note

For ordinary reproduction of the analysis, begin with `01_data_access.ipynb` using the raw CSV already stored in `data/raw/`.

Notebook `00_data_collection.ipynb` is optional because it requires an API key and depends on the current state of the Europeana API.

Run the notebooks in numerical order and save all outputs before continuing to the next notebook.

