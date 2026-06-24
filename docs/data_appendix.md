# Data Appendix

## Purpose

This appendix documents the variables used in the Europeana India metadata project.

It distinguishes between:

* fields obtained from the Europeana API;
* project-created analytical fields;
* manually added Wikidata-enrichment fields.

The authoritative raw dataset is:

`data/raw/europeana_india_dataset_1500_raw.csv`

The final enriched dataset is:

`data/processed/europeana_india_unique_titles_enhanced_top15_providers.csv`

---

## Dataset overview

| Dataset                                                      | Description                                 | Expected rows |
| ------------------------------------------------------------ | ------------------------------------------- | ------------: |
| `europeana_india_dataset_1500_raw.csv`                       | Raw Europeana API collection                |         1,500 |
| `europeana_india_unique_titles.csv`                          | Deduplicated by title                       |           245 |
| `europeana_india_unique_titles_transformed.csv`              | Deduplicated data with analytical variables |           245 |
| `europeana_india_unique_titles_enhanced_sample.csv`          | Initial Wikidata-enrichment sample          |           245 |
| `europeana_india_unique_titles_enhanced_top15_providers.csv` | Final top-provider enrichment               |           245 |

---

# Original Europeana and collection fields

## `query_group`

**Type:** Text / categorical
**Origin:** Created during API collection
**Possible values:**

* `geographic`
* `colonial`
* `cultural`
* `material`

**Description:**
Identifies the thematic search category through which the record was collected.

Each query group originally contributed up to 375 records.

**Limitations:**
The value describes the search strategy, not necessarily the actual subject of the cultural heritage object.

A record retrieved through the `colonial` group, for example, may not primarily concern colonial history.

---

## `search_term`

**Type:** Text
**Origin:** Created during API collection

**Description:**
Stores the exact search term that retrieved the record from the Europeana API.

Examples include:

* `India`
* `British India`
* `Indian art`
* `Indian textile`
* `Indian manuscript`

**Limitations:**
A record may match more than one search term, but the dataset stores the term under which it was first collected within the project workflow.

Search-term relevance depends on Europeana indexing and ranking.

---

## `title`

**Type:** Text
**Origin:** Europeana metadata

**Description:**
The title supplied for the cultural heritage record.

This field was used for deduplication in `01_data_access.ipynb`.

**Missing values:**
May be missing or contain generic descriptive labels.

**Limitations:**

* different objects may have the same title;
* the same object may appear with different titles;
* titles may be multilingual;
* historical terminology may be retained from source catalogues.

Deduplication by title is therefore an operational project decision rather than proof that records represent identical objects.

---

## `description`

**Type:** Text
**Origin:** Europeana metadata

**Description:**
A descriptive text associated with the record.

The amount and quality of information vary significantly between providers.

**Missing values:**
Frequently missing in some provider collections.

**Limitations:**

* descriptions may be short, incomplete, or absent;
* languages vary;
* terminology may reflect older institutional cataloguing practices;
* descriptions may describe the digital record rather than the physical object.

---

## `subject`

**Type:** Text
**Origin:** Europeana metadata

**Description:**
A subject term or classification associated with the record.

**Missing values:**
May be missing.

**Limitations:**

* institutions use different vocabularies;
* values may not be standardised;
* multiple subjects may be compressed into one exported value;
* terminology may reflect colonial or outdated classification systems.

---

## `dataProvider`

**Type:** Text / categorical
**Origin:** Europeana metadata

**Description:**
The institution or organisation identified as the provider of the record to Europeana.

Examples include museums, libraries, archives, photographic collections, and other cultural heritage organisations.

**Use in analysis:**

* provider-frequency analysis;
* selection of the top 15 providers;
* manual Wikidata enrichment.

**Limitations:**

* provider names may appear in different languages;
* institutional names may have changed;
* one provider may appear under multiple name variants;
* the listed data provider is not always the institution that physically owns the object.

---

## `type`

**Type:** Text / categorical
**Origin:** Europeana metadata

**Description:**
The broad Europeana object type assigned to a record.

Common values may include:

* `IMAGE`
* `TEXT`
* `SOUND`
* `VIDEO`
* `3D`

**Use in analysis:**
Used to examine the distribution of object types in the deduplicated dataset.

**Limitations:**
This is a broad digital-object category and does not provide a detailed material or curatorial classification.

For example, photographs, paintings, maps, and scanned objects may all appear under `IMAGE`.

---

## `country`

**Type:** Text / categorical
**Origin:** Europeana metadata

**Description:**
Country information associated with the Europeana record or contributing provider.

**Limitations:**

* the field may refer to the provider country rather than the object’s place of origin;
* values may be missing;
* geographic meanings may vary between records;
* the field should not automatically be interpreted as the cultural origin of the object.

---

# Derived analytical fields

## `has_description`

**Type:** Boolean
**Created in:** `02_data_cleaning_and_analysis.ipynb`

**Description:**
Indicates whether the `description` field contains a non-empty value.

**Typical values:**

* `True`
* `False`

**Purpose:**
Used as a simple measure of metadata completeness.

**Limitations:**
A value of `True` does not indicate that the description is detailed, accurate, or meaningful. It only indicates that some content is present.

---

## `title_word_count`

**Type:** Integer
**Created in:** `02_data_cleaning_and_analysis.ipynb`

**Description:**
Counts the number of words in the title.

**Purpose:**
Provides a basic indicator of title length and descriptive detail.

**Limitations:**

* word counts depend on spacing and punctuation;
* languages differ in word structure;
* longer titles are not necessarily more informative;
* short titles may still be accurate and specific.

---

## `contains_india`

**Type:** Boolean
**Created in:** `02_data_cleaning_and_analysis.ipynb`

**Description:**
Indicates whether project-defined India-related text appears in selected metadata fields.

**Purpose:**
Used as a basic relevance check for records retrieved by India-related searches.

**Limitations:**

* the rule is keyword-based;
* spelling and language variation may be missed;
* the presence of a keyword does not guarantee that the object is about India;
* relevant records may not explicitly use the word “India”;
* historical uses of “Indian” may refer to Indigenous peoples of the Americas.

---

## `possible_false_positive`

**Type:** Boolean
**Created in:** `02_data_cleaning_and_analysis.ipynb`

**Description:**
Flags records that may have been retrieved by an India-related search but appear potentially unrelated to India.

**Purpose:**
Supports manual inspection of search ambiguity and possible irrelevant results.

**Limitations:**

* this is a heuristic project variable;
* it is not a definitive classification;
* false positives and false negatives are possible;
* multilingual and historically complex records may be incorrectly flagged;
* flagged records require contextual human review.

The field should be interpreted as a screening aid rather than a final judgement.

---

# Wikidata-enrichment fields

## `wikidata_qid`

**Type:** Text
**Created in:** `03_wikidata_enhancement.ipynb`

**Description:**
Stores the Wikidata identifier associated with a manually reviewed data provider.

Example format:

`Q123456`

**Missing values:**
Blank for providers that were not matched or not reviewed.

**Limitations:**

* enrichment focused mainly on high-frequency providers;
* not every provider was checked;
* institutional mergers, renaming, or organisational hierarchies may complicate matching.

---

## `wikidata_label`

**Type:** Text
**Created in:** `03_wikidata_enhancement.ipynb`

**Description:**
Stores the preferred Wikidata label of the matched provider entity.

**Limitations:**

* Wikidata labels may differ from the provider name used by Europeana;
* labels may change over time;
* the selected label may be language-dependent.

---

## `institution_type`

**Type:** Text / categorical
**Created in:** `03_wikidata_enhancement.ipynb`

**Description:**
A simplified institution category assigned during enrichment.

Possible categories may include:

* museum;
* library;
* archive;
* university;
* photographic collection;
* cultural heritage institution;
* other institutional categories used in the notebook.

**Limitations:**

* some institutions have multiple functions;
* simplified categories may not capture organisational complexity;
* classifications depend on available Wikidata and institutional information.

---

## `match_status`

**Type:** Text / categorical
**Created in:** `03_wikidata_enhancement.ipynb`

**Possible values:**

* `matched`
* `uncertain`
* `not_checked`

### `matched`

The provider was confidently connected to a Wikidata entity.

### `uncertain`

A possible Wikidata entity was identified, but the match could not be confirmed with sufficient confidence.

### `not_checked`

The provider was outside the selected enrichment scope or had not been manually reviewed.

**Expected final counts:**

| Match status  | Expected records |
| ------------- | ---------------: |
| `matched`     |              139 |
| `uncertain`   |               28 |
| `not_checked` |               78 |
| **Total**     |          **245** |

**Limitations:**
Match status reflects the project’s manual review process and should not be interpreted as an assessment of the quality of the original institution or metadata.

---

# Missing-value handling

Missing values are generally preserved rather than replaced with invented information.

During analysis:

* missing descriptions are used to calculate `has_description`;
* missing categorical values may be displayed as `Missing` in summary tables;
* missing Wikidata values remain blank when no confident match is available;
* uncertain matches are not automatically converted into confirmed matches.

This approach prioritises transparency over artificially complete data.

---

# Deduplication method

The raw dataset contains 1,500 records.

Notebook `01_data_access.ipynb` removes duplicate records based on the `title` field, producing 245 unique-title records.

This method was chosen because a stable Europeana record identifier was not retained in the original eight-column export.

Important consequences include:

* separate objects with the same title may be merged;
* duplicate objects with slightly different titles may remain;
* multilingual variants may not be recognised as duplicates.

The deduplicated dataset should therefore be understood as a unique-title dataset, not as a guaranteed set of unique physical objects.

---

# Interpretation guidance

The dataset represents search results and institutional metadata, not a comprehensive account of India or Indian cultural heritage.

Observed patterns may reflect:

* Europeana search ranking;
* the chosen English-language search terms;
* institutional digitisation priorities;
* colonial collecting histories;
* provider metadata practices;
* missing or inconsistent descriptions;
* the distribution of participating European institutions.

Quantitative results should therefore be interpreted together with historical, institutional, and ethical context.
