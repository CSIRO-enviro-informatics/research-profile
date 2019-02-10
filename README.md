# Metadata profiles for research dataset discovery and assessment

_Adapted from content originally prepared through the [W3C DXWG](https://github.com/w3c/dxwg/wiki/Data-aspects-semantics)_

Generic metadata such as [DCAT](https://w3c.github.io/dxwg/dcat/) and [schema.org](https://schema.org/) is used in indexes to support dataset discovery.
Basic DCAT supports the indication of dataset semantics through
* [dcat:keyword](https://w3c.github.io/dxwg/dcat/#Property:dataset_keyword) - which has a literal value
* [dcat:theme](https://w3c.github.io/dxwg/dcat/#Property:dataset_theme) - which uses a `skos:Concept` from a controlled vocabulary
* [dct:subject](http://www.dublincore.org/documents/dcmi-terms/#terms-subject) - intended to be used with a link to a value in a controlled vocabulary

The semantics of these properties are relatively non-specific, particularly in relation to the properties associated with scientific observations that usually involve a well-defined protocol or sensor.
Additional predicates (or specializations of the generic predicates) might be used to provide more explicit descriptions of datasets, to support cross-domain research data **discovery** and initial **assessment**.

Suitable additional properties typically correspond with slots within more specialized generic- and domain-specific (metadata) standards such as [schema.org](https://schema.org/), [W3C SSN](https://www.w3.org/TR/vocab-ssn/), [DDI/DISCO](https://www.ddialliance.org/Specification/RDF/Discovery), [DATS](https://datatagsuite.github.io/docs/html/), [ISO 19115 (Geospatial)](http://wiki.esipfed.org/index.php/Category:ISO_Explorer). Information should be copied up from the specialized metadata records to support description using a x-domain research data description standard.

## Related work

- [Science on schema.org](https://github.com/ESIPFed/science-on-schema.org/blob/master/guides/Dataset.md) adapted from [NSF-EarthCube project 418](https://github.com/earthcubearchitecture-project418/p418Vocabulary)
- [Inventory of relevant metadata schemas](https://ddi-alliance.atlassian.net/wiki/spaces/DDI4/pages/535494691/Background+Materials+for+Use+in+Workshop)
    - [ISO 19115](https://ddi-alliance.atlassian.net/wiki/spaces/DDI4/pages/548405259/ISO+19115+Geographic+Information+--+Metadata)
- [Research Objects](http://www.researchobject.org/specifications/)

## Candidate properties

| Vocabulary | prefix | properties |
|--|--| -- |
| [W3C SSN](https://www.w3.org/TR/vocab-ssn/) | `ssn:` `sosa:` `ssn-ext:` | [sosa:observedProperty](https://www.w3.org/TR/vocab-ssn/#SOSAobservedProperty) [sosa:hasFeatureOfInterest](https://www.w3.org/TR/vocab-ssn/#SOSAhasFeatureOfInterest) [sosa:usedProcedure](https://www.w3.org/TR/vocab-ssn/#SOSAusedProcedure) [sosa:madeBySensor](https://www.w3.org/TR/vocab-ssn/#SOSAmadeBySensor) [sosa:phenomenonTime](https://www.w3.org/TR/vocab-ssn/#SOSAphenomenonTime) [ssne:hasUltimateFeatureOfInterest](https://w3c.github.io/sdw/proposals/ssn-extensions/#ssn-ext:hasUltimateFeatureOfInterest) |
| [W3C Data Cube](https://www.w3.org/TR/vocab-data-cube/) | `qb:` | [qb:concept](https://www.w3.org/TR/vocab-data-cube/#reference-concepts) [qb:componentProperty](https://www.w3.org/TR/vocab-data-cube/#reference-compspec) (also sub-properties [qb:dimension](https://www.w3.org/TR/vocab-data-cube/#reference-compspec) [qb:measure](https://www.w3.org/TR/vocab-data-cube/#reference-compspec) [qb:attribute](https://www.w3.org/TR/vocab-data-cube/#reference-compspec) |
| [DDI DISCO](https://htmlpreview.github.io/?https://raw.github.com/linked-statistics/disco-spec/master/discovery.html) | `disco:` |  `disco:variable` `disco:universe` `disco:analysisUnit` |
| [DATS](http://www.github.com/biocaddie/WG3-MetadataSpecifications) | `dats:` | [dats:isAbout](https://github.com/biocaddie/WG3-MetadataSpecifications/blob/master/json-schemas/dataset_schema.json) [dats:producedBy](https://github.com/biocaddie/WG3-MetadataSpecifications/blob/master/json-schemas/dataset_schema.json) [dats:types](https://github.com/biocaddie/WG3-MetadataSpecifications/blob/master/json-schemas/dataset_schema.json) [dats:dimensions](https://github.com/biocaddie/WG3-MetadataSpecifications/blob/master/json-schemas/dataset_schema.json) |
| [schema.org](https://schema.org/docs/schemas.html) | `s:` | [s:variableMeasured](https://pending.schema.org/variableMeasured) [s:measurementTechnique](https://schema.org/measurementTechnique) [s:instrument](https://schema.org/instrument) [s:usesDevice](http://schema.org/usesDevice) [s:object](https://schema.org/object) |
| [ISO 19115](https://ddi-alliance.atlassian.net/wiki/spaces/DDI4/pages/548405259/ISO+19115+Geographic+Information+--+Metadata) | `iso19115:` | `iso19115:extent` `iso19115:rangeElementDescription` `iso19115:instrument` `iso19115:acquisitionInformation` |

### Approximate equivalences
* `ssn-ext:hasUltimateFeatureOfInterest` ~ `disco:universe` ~ `iso19115:extent`
* `sosa:hasFeatureOfInterest` ~ `disco:analysisUnit` ~ `dats:isAbout` ~ `s:object`
* `sosa:observedProperty` ~ `qb:concept` ~ `disco:variable` ~ `dats:dimensions` ~ `iso19115:rangeElementDescription`~ `s:variableMeasured`
* `sosa:madeBySensor` ~ `iso19115:instrument` ~ `s:instrument`  (also `s:usesDevice` for medical applications)
* `sosa:usedProcedure` ~ `dats:producedBy` ~ `iso19115:acquisitionInformation` ~ `s:measurementTechnique`

![Metadata for 'rectangular' datasets](image/Rectangular%20data.png)

## Starting points
### DCAT augmented for research data

![DCAT research profile](image/DCAT%20research%20data%20profile.png)

In this strawman the DCAT `Dataset` description is augmented with additional properties and classes, taken from W3C RDF vocabularies where available. The set of additional properties were identified in the workshop on [Interoperability of Metadata Standards in Cross-Domain Science, Health, and Social Science Applications](https://ddi-alliance.atlassian.net/wiki/spaces/DDI4/pages/433553433/Interoperability+of+Metadata+Standards+in+Cross-Domain+Science+Health+and+Social+Science+Applications) based on requirements from the three pilot projects of the [CODATA Data Integration Initiative](http://www.codata.org/strategic-initiatives/commission-on-standards). 

`res:` is a new namespace for research dataset metadata

### schema.org selected for research data

![schema.org research profile](image/schema.org%20dataset.png)

The properties shown in this strawman are associated with the **schema.org** classes indicated, as listed at [s:Dataset](https://schema.org/Dataset), [s:Action](https://schema.org/Action). Under schema.org semantics there is no limitation on use of properties to describe any Type, but this diagram indicates the normal expectations, as given by the `s:domainIncludes` and `s:rangeIncludes` descriptors for the properties shown.

`s:Action` is a potential super-class for _act-of-observation_. It is introduced here to show some useful properties of research data that are not normally associated with "continuant" entities, but are likely to be useful in research dataset discovery. (Would [s:AchieveAction](https://schema.org/AchieveAction) or [s:CreateAction](https://schema.org/CreateAction) be better?)

## Other concerns
from **DDI**
* collectionFrequency (different to accrualPeriodicity)
* summary statistics ...
* questionaire is a kind of sensor or instrument

from **Geospatial**
* spatial resolution
* spatial aggregation level

Other important sources to correlate
* THREDDS/netCDF
