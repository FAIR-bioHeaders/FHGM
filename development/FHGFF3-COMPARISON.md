# FHGFF3 reuse and FHGM requirements

This is a design worksheet, not a field adoption table. Start by retaining
FHGFF3 meanings wherever possible. Subtype versus sibling remains undecided.

## Baselines

The inherited [header pin](../header/provenance.json) records shared commit
`bdcaecf759b5b2be5fd61bf8f39368a7e3963315` (FHGFF3 1.0 model). It is reference
material, not a selection of that older contract for FHGM. Current shared sources
must be compared before choosing a base; record the selected commit, schema
version and relevant differences in a design PR. Do not substitute moving main
for a versioned contract.

## Comparison worksheet

| Concept | Existing FHGFF3 starting point | FHGM question / evidence needed |
| --- | --- | --- |
| Contract identity | Required `schema`, `schemaVersion` | How does a subtype or sibling declare identity and get dispatched by tools? |
| Shared required metadata | `taxon`, `version`, `metadataAuthor`, `dateCreated`, `checksum` | Preserve meanings; clarify model version and dates against actual deposits. |
| Annotation identity | Required `annotation` | Can it name the contribution without changing its meaning? |
| Reference genome | FHR `annotates` checksum link and/or complete `genomeReference` | Retain authority/cardinality rules; can deposits supply required identity? |
| Sources and methods | Optional `source`, `annotationSoftware`, `annotationProtocol` | Which evidence and curation requirements fit existing objects? |
| Publication and data identity | Optional `scholarlyArticle`, `identifier`, `accessionID`, links | Keep model deposit, article and assembly separate; check multiplicity. |
| Contributors | Shared author objects; metadata author role | How are model authors and curators credited without conflating roles? |
| Model scope | Native GFF3 `ID`/`Parent` relationships | How does the header identify its locus/models and isoforms? |
| Revision lifecycle | Parent-file provenance and source references | Define replacement, split/merge and supersession; evidence is not necessarily a parent file. |
| Reuse terms | Optional `reuseConditions` | Record actual payload permissions separately from article licensing. |
| GFF3 serialization | Version directive first, leading `#~` block, defined end boundary | Reuse placement, interleaving and embedded FASTA behavior. |
| Integrity | Exact-byte checksum, excluding root checksum line | Reuse rules; transformations require recomputation, not a copied checksum. |
| Feature layer | Ordinary GFF3 types and relationships | Which additional constraints, if any, do worked examples demonstrate? |

## Decision test

Would every valid FHGM record validate against the selected FHGFF3 base with
unchanged meanings? Test both schema shape and type-selection rules: a new schema
URL is not automatically accepted as FHGFF3. If yes, favor a documented subtype;
if requirements conflict, use a sibling contract with compatible shared objects.
Neither an `x-` experiment nor a GitHub fork establishes adoption or runtime support.

## Validation boundaries

Report header/schema validity, GFF3 feature validity, checksum integrity,
reference matching and biological evidence assessment separately. A passing result
in one category does not establish the others. Do not design new feature syntax
merely to represent file-level provenance.
