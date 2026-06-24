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

The four notebooks are:

1. `00_data_collection.ipynb`
2. `01_data_access.ipynb`
3. `02_data_cleaning_and_analysis.ipynb`
4. `03_wikidata_enhancement.ipynb`

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
│       └── europeana_india_unique_titles_enhanced_top15_providers.csv
├── notebooks/
│   ├── README.md
│   ├── 00_data_collection.ipynb
│   ├── 01_data_access.ipynb
│   ├── 02_data_cleaning_and_analysis.ipynb
│   └── 03_wikidata_enhancement.ipynb
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

The Wikidata enrichment added structured provider information while preserving uncertainty. Possible matches that could not be confirmed were marked as `uncertain`.

## Search ambiguity

One important methodological issue is the ambiguity of the term “Indian.”

In some records, it refers to India or South Asia. In historical metadata, however, it may refer to Indigenous peoples of the Americas.

The `possible_false_positive` field is used as a screening aid. It is rule-based and should not be interpreted as a definitive classification. Ambiguous cases require contextual human review.

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
- some provider matches remain uncertain.

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
