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

## Reproducibility note

For ordinary reproduction of the analysis, begin with `01_data_access.ipynb` using the raw CSV already stored in `data/raw/`.

Notebook `00_data_collection.ipynb` is optional because it requires an API key and depends on the current state of the Europeana API.

Run the notebooks in numerical order and save all outputs before continuing to the next notebook.

