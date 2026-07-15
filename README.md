# Representations of India in Europeana Metadata

## Project overview

This project investigates how India is represented through metadata in European digital cultural heritage collections available through Europeana.

The focus is not primarily on the physical objects themselves, but on how India-related material is described, classified, grouped, and made searchable within museum, archive, library, and cultural heritage metadata systems.

The project examines four broad dimensions:

- geographic representations of India;
- colonial and historical framing;
- cultural and heritage classifications;
- material and object categories.

The project was completed as coursework for the **MA Data and Discourse Studies** programme at **TU Darmstadt**.

## Author

**Shone Joseph**

## Research question

How is India represented in Europeana metadata, and what patterns can be identified in the retrieved records in relation to object types, thematic search categories, contributing institutions, metadata completeness, and search ambiguity?

## Research purpose

The project aims to explore:

- how India is described in European cultural heritage metadata;
- how institutional classification systems shape those representations;
- which object types dominate the retrieved records;
- how colonial, cultural, geographic, and material framings appear in the data;
- which institutions contribute the most records;
- how complete the available metadata is;
- where keyword-based searches produce ambiguous or potentially irrelevant results;
- how selected provider information can be enriched using Wikidata.

## Data source

The records were collected from the **Europeana Search API** in **May 2026**.

Europeana aggregates metadata from museums, archives, libraries, galleries, universities, and other cultural heritage organisations.

The fixed raw dataset used for this project is stored at:

`data/raw/europeana_india_dataset_1500_raw.csv`

Because Europeana is a live service, search results may change over time as records, metadata, indexing, and ranking are updated. The stored raw CSV should therefore be treated as the authoritative dataset for reproducing this project.

## Collection design

The dataset contains 1,500 records organised into four thematic query groups.

Each query group originally contributed 375 records:

| Query group | Records |
|---|---:|
| Geographic | 375 |
| Colonial | 375 |
| Cultural | 375 |
| Material | 375 |
| **Total** | **1,500** |

The search strategy used several terms rather than relying on a single keyword.

Examples include:

### Geographic

- India
- Indian
- Indien

### Colonial

- British India
- colonial India
- British Raj
- East India Company

### Cultural

- Indian art
- Indian museum collection
- South Asia collection
- ethnography India
- India exhibition

### Material

- Indian textile
- Indian manuscript
- Indian photograph
- Indian map
- Indian print

The exact collection logic is documented in:

`notebooks/00_data_collection.ipynb`

## Original metadata fields

The raw dataset contains eight fields:

- `query_group`
- `search_term`
- `title`
- `description`
- `subject`
- `dataProvider`
- `type`
- `country`

## Project workflow

The project follows a reproducible workflow for collecting, selecting, cleaning, analysing, visualising, enriching, documenting, and sharing Europeana metadata.

The five notebooks are:

1. `00_data_collection.ipynb`
2. `01_data_access.ipynb`
3. `02_data_cleaning_and_analysis.ipynb`
4. `03_wikidata_enhancement.ipynb`
5. `04_relevance_review.ipynb`

For ordinary reproduction of the project results, begin with notebook 01.

Notebook 00 is optional because it requires a Europeana API key and accesses a live service.

## Repository structure

```text
Open_Project_2026/
├── README.md
├── requirements.txt
├── .gitignore
├── data/
│   ├── README.md
│   ├── raw/
│   │   └── europeana_india_dataset_1500_raw.csv
│   └── processed/
│       ├── europeana_india_unique_titles.csv
│       ├── europeana_india_unique_titles_transformed.csv
│       ├── europeana_india_unique_titles_enhanced_sample.csv
│       ├── europeana_india_unique_titles_enhanced_top15_providers.csv
│       └── europeana_india_unique_titles_enhanced_extended.csv
├── notebooks/
│   ├── README.md
│   ├── 00_data_collection.ipynb
│   ├── 01_data_access.ipynb
│   ├── 02_data_cleaning_and_analysis.ipynb
│   ├── 03_wikidata_enhancement.ipynb
│   └── 04_relevance_review.ipynb
├── outputs/
│   ├── figures/
│   │   ├── object_type_distribution.png
│   │   └── query_group_distribution.png
│   └── tables/
│       ├── object_type_summary.csv
│       └── query_group_summary.csv
├── docs/
│   ├── metadata_guide.md
│   ├── data_appendix.md
│   ├── ai_use_statement.md
│   └── peer_test_instructions.md
└── report/
    └── project_report.md
```

## Software requirements

The project uses Python and JupyterLab.

The main required packages are:

- JupyterLab;
- pandas;
- NumPy;
- Matplotlib;
- requests;
- ipykernel.

The tested package versions are listed in:

`requirements.txt`

## Installation

### 1. Clone or download the repository

```powershell
git clone <REPOSITORY_URL>
cd Open_Project_2026
```

Replace `<REPOSITORY_URL>` with the actual GitHub repository URL.

### 2. Create a virtual environment

```powershell
python -m venv europeana-env
```

### 3. Activate the environment

On Windows PowerShell:

```powershell
.\europeana-env\Scripts\Activate.ps1
```

If PowerShell blocks activation:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
.\europeana-env\Scripts\Activate.ps1
```

### 4. Install the dependencies

```powershell
pip install -r requirements.txt
```

### 5. Launch JupyterLab

```powershell
jupyter lab
```

## Reproducing the project

### 1. Data access and deduplication

Open:

`notebooks/01_data_access.ipynb`

This notebook loads the fixed raw dataset, checks the data structure and original query-group balance, removes duplicate titles, and saves the deduplicated dataset.

Expected output:

`data/processed/europeana_india_unique_titles.csv`

Expected number of rows:

`245`

### 2. Data cleaning and analysis

Open:

`notebooks/02_data_cleaning_and_analysis.ipynb`

This notebook creates the analytical variables, examines object types and query groups, identifies potentially ambiguous records, and saves figures, tables, and the transformed dataset.

Expected transformed output:

`data/processed/europeana_india_unique_titles_transformed.csv`

Expected figures:

- `outputs/figures/object_type_distribution.png`
- `outputs/figures/query_group_distribution.png`

Expected summary tables:

- `outputs/tables/object_type_summary.csv`
- `outputs/tables/query_group_summary.csv`

### 3. Wikidata enrichment

Open:

`notebooks/03_wikidata_enhancement.ipynb`

This notebook enriches selected provider names with Wikidata information, assigns institution types, records match confidence, and saves the final enriched dataset.

Expected final output:

`data/processed/europeana_india_unique_titles_enhanced_top15_providers.csv`

Expected final match-status counts:

| Match status | Records |
|---|---:|
| `matched` | 139 |
| `uncertain` | 28 |
| `not_checked` | 78 |
| **Total** | **245** |

### 4. Relevance review and further enrichment

Open:

`notebooks/04_relevance_review.ipynb`

This notebook loads the enriched dataset from `03_wikidata_enhancement.ipynb`, extends the Wikidata enrichment to a further set of frequent providers, manually reviews the records flagged as possible false positives, adds metadata-completeness indicators, adds a clickable Wikidata link for every record with a confirmed identifier, and saves the final enriched dataset.

Expected final output:

`data/processed/europeana_india_unique_titles_enhanced_extended.csv`

Expected final match-status counts:

| Match status | Records |
|---|---:|
| `matched` | 188 |
| `uncertain` | 0 |
| `not_checked` | 54 |
| `needs_manual_review` | 3 |
| **Total** | **245** |

## Optional API collection

Notebook `notebooks/00_data_collection.ipynb` documents the original collection process.

It requires an environment variable named:

`EUROPEANA_API_KEY`

Example in PowerShell:

```powershell
$env:EUROPEANA_API_KEY="YOUR_API_KEY"
```

The API key is not stored in the repository.

Because Europeana is continuously updated, rerunning this notebook may not reproduce the exact same 1,500 records. The included raw CSV should be used to reproduce the submitted analysis.

## Main findings

After title-based deduplication, the original balanced sampling structure changed:

| Query group | Unique-title records |
|---|---:|
| Cultural | 82 |
| Material | 69 |
| Colonial | 47 |
| Geographic | 47 |
| **Total** | **245** |

The cultural and material groups retained more distinct titles, while the colonial and geographic groups contained more repeated titles.

The dataset is strongly dominated by records classified as `IMAGE`. This reflects both visual digitisation practices and Europeana's broad object-type classification.

A relatively small number of institutions contribute a substantial share of the deduplicated records, meaning that institutional collection histories, cataloguing practices, and digitisation priorities strongly influence the dataset.

The Wikidata enrichment added structured provider information while preserving uncertainty. Possible matches that could not be confirmed were marked as `uncertain`, and providers extending beyond the original enrichment scope were reviewed in a further pass, raising the total matched records to 188 of 245 while still preserving 3 records as `needs_manual_review` rather than forcing a match.

Manual review of the records flagged as possible false positives confirmed that all 17 of them (approximately 6.9 percent of the deduplicated dataset) refer to Indigenous peoples of the Americas rather than to India, most commonly through the German cataloguing term "Indianer." These records were retained in the dataset and flagged rather than removed. This finding is limited to this 245-record sample and should not be generalised to Europeana as a whole; the remaining 228 records were not individually re-verified as India-related.

The `subject` field, one of Europeana's core descriptive properties, is empty for all 245 records in the dataset. This is a plausible contributing factor to the search-ambiguity finding above: a populated, controlled-vocabulary subject field would typically distinguish India from Indigenous peoples of the Americas as separate authority terms, reducing reliance on ambiguous free-text keyword matching.

## Search ambiguity

One important methodological issue is the ambiguity of the term "Indian."

In some records, it refers to India or South Asia. In historical metadata, however, it may refer to Indigenous peoples of the Americas.

The `possible_false_positive` field was used as a rule-based screening aid to flag records that might require contextual human review. All 17 flagged records were subsequently reviewed manually in `notebooks/04_relevance_review.ipynb`, and the outcome of each review is recorded in the `record_relevance_status` and `relevance_notes` fields (see "Main findings" above).

## Limitations

The project has several limitations:

- Europeana search results are not exhaustive;
- live API results may change;
- search ranking influences retrieval;
- metadata completeness varies between institutions;
- titles, descriptions, and subjects may be missing or inconsistent;
- provider names may appear in multiple forms;
- object-type categories are broad;
- title-based deduplication may merge distinct objects;
- keyword matching may produce false positives and false negatives;
- Wikidata enrichment covers mainly the most frequent providers;
- 54 records remain outside the enrichment scope and 3 could not be confidently matched to any institution;
- the `subject` field is empty for all records in the dataset, limiting reliance on Europeana's own subject classification;
- the manual relevance review covered only the 17 records flagged as possible false positives; the remaining 228 records were not individually re-verified as India-related.

## Ethical considerations

Cultural heritage metadata is not neutral.

It may reproduce colonial collecting histories, outdated terminology, institutional classification systems, unequal visibility of communities, and European perspectives on non-European heritage.

The project preserves source metadata for analysis but does not endorse outdated terminology. Current respectful language is used in the documentation where possible.

## Supporting documentation

Additional documentation is available in:

- `data/README.md`
- `notebooks/README.md`
- `docs/metadata_guide.md`
- `docs/data_appendix.md`
- `docs/ai_use_statement.md`
- `docs/peer_test_instructions.md`

## AI assistance

Generative AI was used in a limited and supervised manner as a technical and editorial assistant.

AI-generated suggestions were manually reviewed, executed, checked, revised, or rejected by the author. The author remained responsible for the research question, data-processing decisions, code execution, validation, interpretation, ethical framing, and final coursework submission.

Full details are provided in:

`docs/ai_use_statement.md`

## Peer testing

A peer tester should begin with this README and attempt to follow the project without prior verbal explanation from the author.

Brief instructions are available at:

`docs/peer_test_instructions.md`

## Rights and reuse

The repository contains metadata retrieved through Europeana and its contributing institutions.

Rights and reuse conditions may differ between records and providers. Before reusing individual records, metadata, or images, consult the original Europeana record and relevant provider rights information.

The code and project documentation are intended for coursework, research, and reproducibility testing.
