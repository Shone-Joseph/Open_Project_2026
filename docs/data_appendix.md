# Data Appendix

## Purpose

This appendix documents the variables used in the Europeana India metadata project.

It distinguishes between:

* fields obtained from the Europeana API;
* project-created analytical fields;
* manually added Wikidata-enrichment fields;
* manually added relevance-review and completeness fields.

The authoritative raw dataset is:

`data/raw/europeana_india_dataset_1500_raw.csv`

The final enriched dataset is:

`data/processed/europeana_india_unique_titles_enhanced_extended.csv`

---

## Dataset overview

| Dataset                                                      | Description                                          | Expected rows |
| ------------------------------------------------------------ | ----------------------------------------------------- | ------------: |
| `europeana_india_dataset_1500_raw.csv`                       | Raw Europeana API collection                           |         1,500 |
| `europeana_india_unique_titles.csv`                          | Deduplicated by title                                  |           245 |
| `europeana_india_unique_titles_transformed.csv`              | Deduplicated data with analytical variables            |           245 |
| `europeana_india_unique_titles_enhanced_sample.csv`          | Initial Wikidata-enrichment sample                     |           245 |
| `europeana_india_unique_titles_enhanced_top15_providers.csv` | Top-15-provider Wikidata enrichment                    |           245 |
| `europeana_india_unique_titles_enhanced_extended.csv`        | Final enrichment: further provider matching, relevance review, completeness indicators |           245 |

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
Frequently missing in some provider collections. 92 of 245 records have no description.

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
Empty for all 245 records in this dataset (see `has_subject` below).

**Limitations:**

* institutions use different vocabularies;
* values may not be standardised;
* multiple subjects may be compressed into one exported value;
* terminology may reflect colonial or outdated classification systems;
* in this dataset, the field carries no usable signal at all, since it was never populated by any contributing provider in the sample.

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
* manual Wikidata enrichment, later extended to further frequent providers.

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

Europeana's data model requires at least one of several descriptive properties (subject, coverage, type, spatial, temporal) to be present; `type` appears to be the property providers in this sample rely on to satisfy that requirement, since `subject` is never populated (see above).

---

## `country`

**Type:** Text / categorical
**Origin:** Europeana metadata

**Description:**
Country information associated with the Europeana record or contributing provider.

**Limitations:**

* the field may refer to the provider country rather than the object's place of origin;
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
* relevant records may not explicitly use the word "India";
* historical uses of "Indian" may refer to Indigenous peoples of the Americas.

---

## `possible_false_positive`

**Type:** Boolean
**Created in:** `02_data_cleaning_and_analysis.ipynb`

**Description:**
Flags records that may have been retrieved by an India-related search but appear potentially unrelated to India.

**Purpose:**
Supports manual inspection of search ambiguity and possible irrelevant results.

**Values in this dataset:**
17 of 245 records are flagged `True`. All 17 were subsequently reviewed manually in `04_relevance_review.ipynb` (see `record_relevance_status` below); every one was confirmed to refer to Indigenous peoples of the Americas rather than to India, most often through the German cataloguing term "Indianer."

**Limitations:**

* this is a heuristic project variable;
* it is not a definitive classification on its own — the definitive judgement is recorded separately in `record_relevance_status`;
* false negatives are possible: records not flagged here were not individually re-verified as India-related;
* multilingual and historically complex records may be incorrectly flagged or missed.

The field should be interpreted as a screening aid rather than a final judgement; the final judgement for flagged records is in `record_relevance_status`.

---

# Wikidata-enrichment fields

## `wikidata_qid`

**Type:** Text
**Created in:** `03_wikidata_enhancement.ipynb`, extended in `04_relevance_review.ipynb`

**Description:**
Stores the Wikidata identifier associated with a manually reviewed data provider.

Example format:

`Q123456`

**Missing values:**
Blank for providers that were not matched or not reviewed.

**Limitations:**

* enrichment focused mainly on high-frequency providers;
* not every provider was checked (54 of 245 records remain `not_checked` in the final dataset);
* institutional mergers, renaming, or organisational hierarchies may complicate matching.

---

## `wikidata_label`

**Type:** Text
**Created in:** `03_wikidata_enhancement.ipynb`, extended in `04_relevance_review.ipynb`

**Description:**
Stores the preferred Wikidata label of the matched provider entity.

**Limitations:**

* Wikidata labels may differ from the provider name used by Europeana;
* labels may change over time;
* the selected label may be language-dependent.

---

## `institution_type`

**Type:** Text / categorical
**Created in:** `03_wikidata_enhancement.ipynb`, extended in `04_relevance_review.ipynb`

**Description:**
A simplified institution category assigned during enrichment.

Possible categories may include:

* museum;
* library;
* archive;
* university;
* photographic archive;
* cultural heritage institution;
* film archive / media institution;
* museum organisation;
* other institutional categories used in the notebooks.

**Limitations:**

* some institutions have multiple functions;
* simplified categories may not capture organisational complexity;
* classifications depend on available Wikidata and institutional information;
* at least one provider in this category set (a private commercial photo agency) is not a public heritage institution in the conventional sense, which is worth bearing in mind when interpreting `institution_type` distributions.

---

## `match_status`

**Type:** Text / categorical
**Created in:** `03_wikidata_enhancement.ipynb`, extended in `04_relevance_review.ipynb`

**Possible values:**

* `matched`
* `uncertain`
* `not_checked`
* `needs_manual_review` (introduced in `04_relevance_review.ipynb`)

### `matched`

The provider was confidently connected to a Wikidata entity, supported by documented evidence.

### `uncertain`

A possible Wikidata entity was identified, but the match could not be confirmed with sufficient confidence.

### `not_checked`

The provider was outside the selected enrichment scope or had not been manually reviewed.

### `needs_manual_review`

No institution could be confidently identified for the provider name from the available evidence. This status was preserved rather than resolved through a forced or uncertain match.

**Match-status counts after `03_wikidata_enhancement.ipynb`:**

| Match status  | Records |
| ------------- | ------: |
| `matched`     |     139 |
| `uncertain`   |      28 |
| `not_checked` |      78 |
| **Total**     | **245** |

**Final match-status counts, after `04_relevance_review.ipynb`:**

| Match status           | Records |
| ----------------------- | ------: |
| `matched`                |     188 |
| `uncertain`               |       0 |
| `not_checked`             |      54 |
| `needs_manual_review`     |       3 |
| **Total**                 | **245** |

**Limitations:**
Match status reflects the project's manual review process and should not be interpreted as an assessment of the quality of the original institution or metadata. Full institutional coverage was not achieved: 54 records remain outside the enrichment scope, and 3 could not be confidently matched to any institution.

---

## `provider_enrichment_notes`

**Type:** Text
**Created in:** `04_relevance_review.ipynb`

**Description:**
Documents the reasoning behind each provider-enrichment decision made in this notebook — the evidence consulted and why a match was judged confident, uncertain, or unresolved.

**Missing values:**
Blank for records whose provider was not touched by this notebook's enrichment pass.

**Limitations:**
Free text; not a structured or machine-checkable field. Intended for human review and audit rather than computation.

---

## `wikidata_url`

**Type:** Text (URL)
**Created in:** `04_relevance_review.ipynb`

**Description:**
A clickable Wikidata link (`https://www.wikidata.org/wiki/{QID}`), generated automatically from `wikidata_qid` for every record with a confirmed identifier.

**Missing values:**
Blank wherever `wikidata_qid` is blank (57 of 245 records in the final dataset).

**Limitations:**
This is a deterministic formatting step over already-verified identifiers; it introduces no new judgement and is only as reliable as the underlying `wikidata_qid` value.

---

# Relevance-review fields

## `record_relevance_status`

**Type:** Text / categorical
**Created in:** `04_relevance_review.ipynb`

**Description:**
Records the outcome of a manual relevance review for records flagged by `possible_false_positive`.

**Values in this dataset:**
`likely_not_india_related` for all 17 reviewed records; blank/unset for the remaining 228 records.

**Limitations:**

* only the 17 flagged records were reviewed — a blank value does **not** mean a record was confirmed as India-related, only that it was not individually reviewed;
* the review is limited to this 245-record sample and should not be generalised.

---

## `relevance_notes`

**Type:** Text
**Created in:** `04_relevance_review.ipynb`

**Description:**
A short, record-specific justification for each relevance judgement in `record_relevance_status` — typically the place name, community name, or contextual detail that identified the record's true subject.

**Missing values:**
Blank wherever `record_relevance_status` is blank.

**Limitations:**
Free text; intended for human review rather than computation.

---

# Metadata-completeness fields

## `has_subject`

**Type:** Boolean
**Created in:** `04_relevance_review.ipynb`

**Description:**
Indicates whether the `subject` field contains a non-empty value.

**Values in this dataset:**
`False` for all 245 records — see the `subject` field entry above.

---

## `has_country`

**Type:** Boolean
**Created in:** `04_relevance_review.ipynb`

**Description:**
Indicates whether the `country` field contains a non-empty value.

**Values in this dataset:**
`True` for all 245 records.

---

## `description_word_count`

**Type:** Integer
**Created in:** `04_relevance_review.ipynb`

**Description:**
Counts the number of words in the `description` field (0 where missing). A finer-grained completeness measure than the boolean `has_description`.

**Limitations:**
Same word-count caveats as `title_word_count` (spacing, punctuation, language differences).

---

## `provider_is_enriched`

**Type:** Boolean
**Created in:** `04_relevance_review.ipynb`

**Description:**
`True` where `match_status == "matched"`, else `False`. A simple rollup for filtering on enrichment completeness.

---

## `enrichment_scope`

**Type:** Text / categorical
**Created in:** `04_relevance_review.ipynb`

**Description:**
A readable category mapped from `match_status`, for presentation and summary purposes:

* `matched` → `provider_confirmed`
* `uncertain` → `provider_candidate_unconfirmed`
* `needs_manual_review` → `provider_unidentified`
* `not_checked` → `provider_not_reviewed`

---

# Missing-value handling

Missing values are generally preserved rather than replaced with invented information.

During analysis:

* missing descriptions are used to calculate `has_description` and `description_word_count`;
* missing categorical values may be displayed as `Missing` in summary tables;
* missing Wikidata values remain blank when no confident match is available;
* uncertain and needs_manual_review matches are not automatically converted into confirmed matches;
* records not individually reviewed for relevance are left with a blank `record_relevance_status` rather than assumed relevant.

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
* the distribution of participating European institutions;
* the completeness of Europeana's own descriptive fields (e.g. the empty `subject` field across this sample).

Quantitative results should therefore be interpreted together with historical, institutional, and ethical context.
