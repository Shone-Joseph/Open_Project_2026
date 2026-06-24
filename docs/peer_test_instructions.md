# Peer Testing Instructions

## Purpose

Please test whether this project can be understood and reproduced using only the repository contents.

The project author should not explain the workflow before the test. This allows unclear documentation, missing files, and broken steps to become visible.

## Where to begin

Start with the main:

`README.md`

Then inspect the repository structure and follow the documented notebook workflow.

For reproducing the analysis, use the fixed raw dataset:

`data/raw/europeana_india_dataset_1500_raw.csv`

Notebook `00_data_collection.ipynb` is optional because it requires a Europeana API key and accesses a live service.

## Recommended notebook order

1. `notebooks/01_data_access.ipynb`
2. `notebooks/02_data_cleaning_and_analysis.ipynb`
3. `notebooks/03_wikidata_enhancement.ipynb`

## Expected results

After running the workflow, the following should be available:

* `data/processed/europeana_india_unique_titles.csv`
* `data/processed/europeana_india_unique_titles_transformed.csv`
* `data/processed/europeana_india_unique_titles_enhanced_top15_providers.csv`
* figures in `outputs/figures/`
* summary tables in `outputs/tables/`

Useful checks:

* raw records: 1,500
* deduplicated records: 245
* matched providers: 139
* uncertain providers: 28
* not-checked providers: 78

## What to record

While testing, note:

* any instruction that is unclear;
* any file that is difficult to locate;
* any notebook cell that fails;
* any missing software package;
* any mismatch between documentation and actual filenames;
* any output that is missing or different from what is described;
* any point where additional explanation from the author feels necessary.

Please include the relevant file, notebook, or error message when reporting a problem.

## After the test

The project author will use the feedback to correct unclear instructions, broken paths, missing dependencies, and documentation inconsistencies before final submission.
