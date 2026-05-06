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
