# Open Cultural Heritage Data Project (2026)

---

## Project Description

This project investigates how European cultural heritage institutions represent India through metadata in digital collections.

The focus is on how “India” is described, classified, and structured within museum and archival metadata systems, rather than on the physical artifacts themselves.

The dataset was collected and processed using the Europeana API in a Jupyter Notebook environment.

The analysis is based on four thematic dimensions:
- Geographic representations of India
- Colonial and historical framing
- Cultural and heritage classifications
- Material/object types

---

## Research Purpose

The purpose of this project is to explore:

- How India is represented in European cultural heritage metadata
- How institutional classification systems shape these representations
- How object types (image, text, sound, video) are distributed
- How colonial and cultural framing appears in metadata descriptions

---

## Data Origin Note

### Source:
Europeana API

### Date accessed:
May 2026

### License:
Open metadata (varies by contributing institution; many records are CC0 or openly licensed)

### Description:
The dataset consists of approximately 1500 metadata records retrieved using keyword-based queries via the Europeana API.

The data was structured into four query groups:
- Geographic terms (India, Indian, Indien)
- Colonial terms (British India, East India Company, British Raj)
- Cultural terms (Indian art, ethnography, museum collections)
- Material terms (textiles, manuscripts, maps, photographs)

Each record contains metadata fields such as:
- title
- description
- subject
- data provider
- object type
- country (when available)

---

## What Has Already Been Done to the Data

- Retrieved data using the Europeana API in Python (Jupyter Notebook)
- Applied stratified keyword-based queries across four thematic dimensions
- Constructed a structured dataset (~1500 records)
- Basic structuring and transformation into pandas dataframe
- Assigned query group labels to each record
- Performed initial exploratory analysis of metadata structure
- Saved dataset in CSV format for further analysis

---

## Workflow

This project follows a reproducible research workflow for collecting, preparing, analysing, visualising, and sharing Europeana metadata related to India. The workflow is designed so that the main steps of the project can be reconstructed from the README, notebooks, and saved data files.

### 1. Data Access

The data was accessed through the Europeana API using Python in a Jupyter Notebook environment. Keyword-based queries were used to retrieve metadata records related to India from European cultural heritage collections.

The search strategy was organised around four thematic query groups:

* Geographic terms: India, Indian, Indien
* Colonial terms: British India, East India Company, British Raj
* Cultural terms: Indian art, ethnography, museum collections
* Material terms: textiles, manuscripts, maps, photographs

The raw metadata retrieved from the API was converted into a structured CSV file for further analysis.

Main data file:

* `data/europeana_india_dataset_1500_final.csv`

Main tools:

* Europeana API
* Python
* Jupyter Notebook
* pandas

### Week 5 reproducibility update

A new notebook, `notebooks/01_data_access.ipynb`, was created to implement the first two workflow stages: data access and selection/sampling. The notebook loads the Europeana India dataset, checks the query group distribution, saves a raw copy in `data/raw/`, creates a deduplicated analytical subset based on unique titles, and saves it in `data/processed/`.

The notebook was tested by running all cells from top to bottom without errors.

### Week 6 transformation and visualisation update

A second notebook, `notebooks/02_data_cleaning_and_analysis.ipynb`, was created to transform the deduplicated dataset and produce an initial visualisation. New columns were added to describe metadata completeness, title length, India-related title references, and possible false positives.

The transformed dataset was saved as `data/processed/europeana_india_unique_titles_transformed.csv`, and the first visualisation was saved as `outputs/figures/object_type_distribution.png`.

### Week 6 Hometask 1 update

A second visualisation was added to compare the distribution of query groups in the deduplicated dataset. This analysis checks whether the original four-part sampling strategy — geographic, colonial, cultural, and material — remains balanced after duplicate titles are removed.

The visualisation was saved as `outputs/figures/query_group_distribution.png`.

### Week 7 data enhancement update

A third notebook, `notebooks/03_wikidata_enhancement.ipynb`, was created to test Wikidata-based data enhancement. The selected entity type was organisations / institutions, using the `dataProvider` column.

New columns were added for Wikidata Q-ID, standardised Wikidata label, institution type, and match status. A manual sample enhancement was applied to selected providers. The result was 64 matched rows, 24 uncertain rows, and 157 rows not yet checked.

The enhanced sample dataset was saved as `data/processed/europeana_india_unique_titles_enhanced_sample.csv`.

### 2. Selection and Sampling

The project focuses on metadata records that describe or classify India-related cultural heritage objects. Instead of using only one keyword, the dataset was built using several thematic query groups. This was done to avoid relying only on a single search term and to capture different kinds of India-related representation.

The dataset contains approximately 1,500 records. During exploration, duplicate titles and repeated records were identified. Therefore, the project distinguishes between:

* the full raw dataset of approximately 1,500 records;
* a deduplicated analytical subset based on unique titles.

This makes it possible to analyse both the overall structure of the Europeana search results and the more distinct metadata representations within the dataset.

### 3. Cleaning and Preprocessing

The dataset is cleaned and inspected before analysis. The main cleaning and preprocessing steps include:

* checking the available metadata columns;
* checking missing values in each field;
* identifying duplicated titles;
* creating a deduplicated dataset based on unique titles;
* checking object type distribution;
* identifying possible false positives or ambiguous records.

One important issue is the ambiguity of the term “Indian.” In some records, “Indian” refers to India, while in others it refers to Indigenous peoples of the Americas. This issue is documented as a methodological limitation of keyword-based metadata retrieval.

The original data file is preserved. Cleaned or processed versions are saved separately so that the workflow remains reproducible.

### 4. Enrichment and Linking

Potential enrichment may be carried out using external authority data such as Wikidata. Possible entities for enrichment include:

* countries;
* cultural heritage institutions;
* places;
* well-known works or organisations.

Possible enrichment features include:

* Wikidata Q-ID;
* standardised name;
* coordinates;
* country;
* institution type.

If this step is applied, the matching decisions and any uncertain cases will be documented in the notebook and README.

### 5. Analysis

The analysis investigates how India is represented in Europeana metadata. The main fields used for analysis are:

* `title`
* `description`
* `dataProvider`
* `type`
* `country`
* `query_group`

The analysis includes:

* counting object types;
* identifying top data providers;
* identifying contributing countries;
* comparing query groups;
* checking missing metadata fields;
* analysing frequent words in titles;
* manually coding a sample of unique titles into thematic categories.

The main thematic categories used for interpretation are:

* colonial / empire;
* material culture / textiles;
* scientific knowledge;
* cartography / geography;
* visual culture;
* music / film / performance;
* false positives or ambiguous records.

### 6. Visualisation

The project will use simple visualisations to support the analysis. Planned visualisations include:

* bar chart of object types;
* bar chart of top data providers;
* bar chart of contributing countries;
* bar chart of query groups;
* bar chart of manually coded themes;
* possible word-frequency visualisation for title metadata.

These visualisations are used to show which types of records and representational themes dominate the dataset.

### 7. Documentation

The workflow is documented in the README file and in Jupyter Notebooks. Markdown cells are used to explain the purpose of each step, and code comments are used to clarify the main actions in the code.

The documentation records:

* where the data comes from;
* which search terms were used;
* how the data was structured;
* what cleaning decisions were made;
* which files were created;
* what limitations were found.

Planned or existing notebooks include:

* `notebooks/01_data_access.ipynb`
* `notebooks/02_data_cleaning_and_analysis.ipynb`
* `notebooks/03_visualisation.ipynb`

### 8. Archiving and Sharing

The project is shared through GitHub. The repository stores the README, notebooks, data files, and analysis outputs. New changes are committed and pushed with meaningful commit messages.

The aim is to make the project transparent enough that another person can understand the sequence of steps, identify the files used at each stage, and reproduce the main analysis.

---

## What is Missing or Uncertain

- Some metadata fields are incomplete (especially descriptions and subjects)
- Object classification varies across contributing institutions
- Some records may overlap across query groups
- API results depend on indexing quality and are not exhaustive
- Institutional bias influences representation of cultural heritage materials

---

## Initial Research Steps (Reconstructed)

### 1. Data Collection
- Accessed Europeana API using Python
- Used keyword-based queries across four stratified categories
- Retrieved approximately 1500 metadata records

### 2. Data Processing
- Converted JSON responses into a structured pandas dataframe
- Added query group labels to each record

### 3. Data Exploration
- Examined metadata fields and object type distribution
- Identified dominance of image-based records
- Conducted initial checks on missing values and structure

---

## Notes

### What I did but cannot fully remember:
- Exact order of API pagination steps for some queries
- Minor iterative adjustments during query refinement

### Files that changed without full documentation:
- Intermediate CSV versions during dataset construction
- Temporary notebook outputs during testing and debugging

---

## Data File

- `data/europeana_india_dataset_1500_final.csv`

---

## Repository Structure

- `data/` → contains raw and cleaned datasets
- `notebooks/` → contains Jupyter notebooks used for processing and analysis
- `README.md` → project documentation

---

## Final Summary

This project demonstrates a reproducible workflow for collecting and analyzing cultural heritage metadata. It highlights how European institutions structure and represent India through digital archival systems and classification practices.
