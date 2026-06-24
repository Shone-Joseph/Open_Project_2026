# Representations of India in Europeana Metadata

**Author:** Shone Joseph
**Programme:** MA Data and Discourse Studies
**Institution:** TU Darmstadt
**Data source:** Europeana Search API
**Data collection date:** May 2026

## 1. Introduction

Digital cultural heritage platforms do more than provide access to objects. They also organise objects through titles, descriptions, subject terms, institutional categories, geographic labels, and technical classifications. These metadata structures influence how users encounter and interpret cultural heritage.

This project examines how India is represented in metadata available through Europeana, a platform that aggregates records from museums, libraries, archives, universities, and other European cultural heritage institutions.

The project focuses on metadata rather than attempting to evaluate the cultural objects themselves. It asks how India-related material is described, classified, grouped, and made searchable within a European digital heritage infrastructure.

Particular attention is given to:

* thematic search categories;
* object-type distribution;
* metadata completeness;
* contributing institutions;
* ambiguity in keyword-based retrieval;
* provider enrichment using Wikidata.

The project also considers how colonial collection histories, institutional cataloguing practices, and historical terminology may shape the retrieved records.

## 2. Research question

The main research question is:

> How is India represented in Europeana metadata, and what patterns can be identified in the retrieved records in relation to object types, thematic search categories, contributing institutions, metadata completeness, and search ambiguity?

The analysis also addresses the following supporting questions:

1. Which object types dominate the retrieved records?
2. How does title-based deduplication affect the original thematic balance?
3. Which cultural heritage institutions contribute the largest number of records?
4. How complete are the titles and descriptions in the dataset?
5. Where does the search strategy produce ambiguous or potentially irrelevant results?
6. How can Wikidata improve the consistency of provider information?

## 3. Data source and collection design

The data were collected from the Europeana Search API in May 2026.

The original dataset contains 1,500 records. The collection strategy was organised into four thematic query groups, with 375 records collected for each group.

| Query group | Original records |
| ----------- | ---------------: |
| Geographic  |              375 |
| Colonial    |              375 |
| Cultural    |              375 |
| Material    |              375 |
| **Total**   |        **1,500** |

The geographic group included terms such as:

* India;
* Indian;
* Indien.

The colonial group included terms such as:

* British India;
* colonial India;
* British Raj;
* East India Company.

The cultural group included terms such as:

* Indian art;
* Indian museum collection;
* South Asia collection;
* ethnography India;
* India exhibition.

The material group included terms such as:

* Indian textile;
* Indian manuscript;
* Indian photograph;
* Indian map;
* Indian print.

Using several thematic groups reduced dependence on a single keyword and allowed the project to retrieve different forms of India-related representation.

The fixed raw dataset is stored as:

`data/raw/europeana_india_dataset_1500_raw.csv`

Europeana is a live service. Search rankings, records, provider metadata, and indexing may change over time. The saved raw dataset is therefore treated as the authoritative source for reproducing this analysis.

## 4. Data structure

The original dataset contains eight fields:

| Field          | Description                                    |
| -------------- | ---------------------------------------------- |
| `query_group`  | The thematic group used during collection      |
| `search_term`  | The search term that retrieved the record      |
| `title`        | The record title supplied through Europeana    |
| `description`  | Descriptive metadata, where available          |
| `subject`      | Subject or classification information          |
| `dataProvider` | The contributing provider or institution       |
| `type`         | Broad Europeana object type                    |
| `country`      | Country information associated with the record |

The available metadata vary in completeness and consistency. Some records contain detailed descriptions and subjects, while others contain only short titles or missing fields.

## 5. Reproducible workflow

The project workflow is organised into four Jupyter notebooks.

### 5.1 Data collection

`notebooks/00_data_collection.ipynb`

This notebook documents the original Europeana API collection procedure. It is optional for ordinary reproduction because it requires a Europeana API key and may return updated live results.

### 5.2 Data access and deduplication

`notebooks/01_data_access.ipynb`

This notebook:

* loads the fixed raw dataset;
* inspects the columns and query-group balance;
* identifies repeated titles;
* removes duplicate titles;
* saves the deduplicated dataset.

The resulting file is:

`data/processed/europeana_india_unique_titles.csv`

### 5.3 Cleaning and analysis

`notebooks/02_data_cleaning_and_analysis.ipynb`

This notebook:

* loads the deduplicated dataset;
* inspects missing values;
* creates analytical variables;
* examines object types;
* compares query-group distributions;
* creates figures and summary tables;
* saves the transformed dataset.

The transformed file is:

`data/processed/europeana_india_unique_titles_transformed.csv`

### 5.4 Wikidata enhancement

`notebooks/03_wikidata_enhancement.ipynb`

This notebook:

* identifies frequent data providers;
* manually enriches selected providers;
* adds Wikidata identifiers;
* assigns standardised labels;
* assigns institution types;
* records match confidence;
* saves the final enhanced dataset.

The final file is:

`data/processed/europeana_india_unique_titles_enhanced_top15_providers.csv`

## 6. Data cleaning and analytical variables

### 6.1 Title-based deduplication

The raw dataset contains 1,500 records.

After duplicate titles were removed, 245 unique-title records remained.

This represents a substantial reduction in the analytical dataset.

Title-based deduplication was used because a stable Europeana record identifier was not retained in the original eight-column export.

However, title-based deduplication has limitations:

* separate objects may share the same title;
* the same object may appear under slightly different titles;
* multilingual title variants may not be recognised as duplicates;
* generic titles may incorrectly collapse distinct objects.

The final dataset should therefore be understood as a unique-title dataset rather than as a guaranteed collection of unique physical objects.

### 6.2 Derived variables

The following analytical fields were created:

#### `has_description`

Indicates whether the description field contains a non-empty value.

This is used as a basic measure of metadata completeness.

#### `title_word_count`

Counts the number of words in each title.

This provides a simple indication of title length, although longer titles are not necessarily more informative.

#### `contains_india`

Checks whether selected India-related terms appear in relevant metadata fields.

This supports basic relevance checking.

#### `possible_false_positive`

Flags records that may have been retrieved through India-related queries but may not refer directly to India.

This is a rule-based screening variable rather than a definitive classification.

## 7. Results

### 7.1 Deduplicated query-group distribution

The original dataset was balanced at 375 records per query group.

After title-based deduplication, the distribution changed substantially:

| Query group | Unique-title records |
| ----------- | -------------------: |
| Cultural    |                   82 |
| Material    |                   69 |
| Colonial    |                   47 |
| Geographic  |                   47 |
| **Total**   |              **245** |

The cultural group contains the largest number of unique-title records, followed by the material group.

The colonial and geographic groups each contain 47 unique-title records.

This indicates that the original balanced collection design was not preserved after duplicate titles were removed. The colonial and geographic search terms appear to have retrieved a larger proportion of repeated titles, while the cultural and material search terms produced a greater variety of distinct titles.

This result should not be interpreted as evidence that cultural and material themes are inherently more important than colonial or geographic themes. It reflects the behaviour of the search terms, Europeana indexing, provider metadata, and the deduplication method.

The related figure is stored at:

`outputs/figures/query_group_distribution.png`

### 7.2 Object-type distribution

The dataset is strongly dominated by records classified as `IMAGE`.

This suggests that India-related material retrieved through Europeana is represented primarily through visual or digitised records.

However, `IMAGE` is a broad Europeana category. It may include:

* photographs;
* paintings;
* prints;
* maps;
* scanned documents;
* digital reproductions of physical objects.

The dominance of the image category therefore reflects both institutional digitisation practices and Europeana’s broad technical classification system.

It should not be interpreted as evidence that India-related cultural heritage consists mainly of one material form.

The related figure is stored at:

`outputs/figures/object_type_distribution.png`

### 7.3 Provider concentration

The deduplicated dataset is not evenly distributed across contributing institutions.

A relatively small group of providers contributes a substantial proportion of the records.

Frequent providers include:

* Museum of Ethnography;
* MAK;
* Deutsche Fotothek;
* Bodleian Libraries;
* Royal Museums Greenwich.

This concentration is important because the metadata representation of India is influenced strongly by the collection histories and cataloguing practices of these institutions.

The dataset therefore reflects not only India-related objects, but also:

* which European institutions digitised their holdings;
* which collections were contributed to Europeana;
* how those institutions describe and classify material;
* which objects are most visible in digital collections.

## 8. Wikidata enrichment

The `dataProvider` field contains names of institutions and organisations, but these names are not always standardised.

Provider names may vary because of:

* language differences;
* abbreviations;
* historical name changes;
* institutional restructuring;
* inconsistent metadata entry.

The project used manual Wikidata enrichment to improve provider consistency for the most frequent institutions.

The following fields were added:

* `wikidata_qid`;
* `wikidata_label`;
* `institution_type`;
* `match_status`.

The final status counts are:

| Match status  | Records |
| ------------- | ------: |
| `matched`     |     139 |
| `uncertain`   |      28 |
| `not_checked` |      78 |
| **Total**     | **245** |

A `matched` status indicates that the provider was confidently connected to a Wikidata entity.

An `uncertain` status indicates that a possible match was found but could not be verified with sufficient confidence.

A `not_checked` status indicates that the provider was outside the selected enrichment scope.

Uncertain matches were preserved rather than automatically converted into confirmed matches.

This makes the enrichment more transparent and avoids overstating the reliability of external entity linking.

## 9. Search ambiguity and false positives

One important issue is the ambiguity of the word “Indian.”

In contemporary usage, the term may refer to India or Indian nationality.

In historical European and American cataloguing, however, the same term may refer to Indigenous peoples of the Americas.

As a result, some records retrieved through India-related search terms may concern:

* Native American communities;
* Indigenous peoples of North America;
* Indigenous peoples of South America;
* historical cataloguing categories unrelated to India.

The `possible_false_positive` field was created to help identify records that may require manual inspection.

This variable has several limitations:

* it depends on keyword rules;
* it may miss relevant multilingual records;
* it may incorrectly flag historically complex records;
* the presence of “India” does not guarantee relevance;
* the absence of “India” does not prove irrelevance.

The field is therefore used as a screening tool rather than as a final classification.

## 10. Discussion

The results show that Europeana metadata does not provide a neutral or comprehensive representation of India.

Instead, the dataset reflects a combination of:

* institutional collection histories;
* digitisation priorities;
* metadata standards;
* search-engine behaviour;
* language choices;
* colonial classifications;
* provider participation;
* uneven descriptive completeness.

The strong dominance of image records shows that the platform’s representation is shaped by what has been digitised and how digital objects are technically classified.

The uneven distribution after deduplication shows that thematic search categories do not produce equally diverse results.

The concentration of records among a limited number of providers shows that a small number of institutions can have a strong influence on how India appears in the dataset.

The Wikidata enrichment demonstrates that linked open data can improve provider consistency, but it also shows that entity matching requires manual judgement and the preservation of uncertainty.

## 11. Ethical considerations

Cultural heritage metadata is not neutral.

It may reproduce:

* colonial collecting practices;
* outdated terminology;
* institutional classification systems;
* unequal representation of communities;
* European perspectives on non-European heritage;
* historical labels that represented communities may not use themselves.

This project preserves source metadata for analytical purposes but does not endorse outdated or harmful terminology.

Current respectful language is used in the project documentation wherever possible.

The project also avoids presenting uncertain matches as verified facts.

A further limitation is that the metadata are largely created and maintained by European cultural heritage institutions. The represented communities may not have participated directly in the creation of the descriptions, categories, and labels used in the records.

## 12. Limitations

The main limitations of the project are:

* the dataset is based on selected keywords;
* most search terms are in English or selected European languages;
* Europeana results are influenced by ranking and indexing;
* live API results may change;
* metadata fields are incomplete and inconsistent;
* object-type categories are broad;
* title-based deduplication is imperfect;
* the raw export does not preserve a stable record identifier;
* provider names are not fully standardised;
* the false-positive flag is rule-based;
* multilingual variation may reduce keyword accuracy;
* Wikidata enrichment focuses mainly on frequent providers;
* some provider matches remain uncertain;
* the sample does not represent all India-related cultural heritage in Europeana.

The project should therefore be understood as an analysis of one structured metadata sample rather than a comprehensive account of India in European cultural heritage collections.

## 13. Reproducibility

The project follows a documented and reproducible workflow.

For ordinary reproduction:

1. create a Python virtual environment;
2. install packages from `requirements.txt`;
3. launch JupyterLab from the project root;
4. run notebooks 01, 02, and 03 in numerical order;
5. compare the generated files and counts with the documented expected outputs.

Key expected values are:

* raw records: 1,500;
* unique-title records: 245;
* matched records: 139;
* uncertain records: 28;
* not-checked records: 78.

Notebook 00 is optional because it requires an API key and accesses the live Europeana service.

## 14. Use of AI assistance

Generative AI was used in a limited and supervised manner as a technical and editorial assistant.

It supported tasks such as:

* troubleshooting Python and Jupyter errors;
* improving file-path handling;
* suggesting documentation structure;
* improving wording and formatting;
* identifying reproducibility issues.

All suggested code was manually reviewed, executed, tested, and verified by the author.

The author remained responsible for:

* the research question;
* the data-collection design;
* the analytical choices;
* code execution;
* Wikidata review;
* result validation;
* interpretation;
* ethical framing;
* the final coursework submission.

A complete statement is available at:

`docs/ai_use_statement.md`

## 15. Conclusion

This project demonstrates how a reproducible metadata workflow can be used to examine representations of India in a European cultural heritage platform.

The results show that the retrieved representation is shaped strongly by image-based digitisation, institutional concentration, metadata completeness, search terminology, and title duplication.

The analysis also shows that keyword-based cultural heritage research requires careful attention to ambiguity, historical language, and false positives.

Wikidata enrichment improves institutional consistency, but it does not remove the need for manual verification and transparent uncertainty.

Most importantly, the project shows that cultural heritage metadata should be interpreted as a product of historical, institutional, and technical processes rather than as a neutral representation of cultural knowledge.

## 16. Supporting files

Further documentation is available in:

* `README.md`
* `data/README.md`
* `notebooks/README.md`
* `docs/metadata_guide.md`
* `docs/data_appendix.md`
* `docs/ai_use_statement.md`
* `docs/peer_test_instructions.md`
