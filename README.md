## Metadata profiles for research dataset discovery and assessment

_Adapted from content originally prepared through the [W3C DXWG](https://github.com/w3c/dxwg/wiki/Data-aspects-semantics)_

Generic metadata such as [DCAT](https://w3c.github.io/dxwg/dcat/) and [schema.org](https://schema.org/) is used in indexes to support dataset discovery. 
Basic DCAT supports the indication of dataset semantics through 
* [dcat:keyword](https://w3c.github.io/dxwg/dcat/#Property:dataset_keyword) - which has a literal value
* [dcat:theme](https://w3c.github.io/dxwg/dcat/#Property:dataset_theme) - which uses a `skos:Concept` from a controlled vocabulary
* [dct:subject](http://www.dublincore.org/documents/dcmi-terms/#terms-subject) - intended to be used with a link to a value in a controlled vocabulary
The semantics of these properties are relatively non-specific, particularly in relation to the properties associated with scientific observations that usually involve a well-defined protocol or sensor. 

Specializations of these, or additional predicates might be used to support more explicit semantic descriptions of datasets, to support cross-domain research data **discovery** and initial **assessment**. 
Suitable additional properties typically correspond with slots within more specialized generic- and domain-specific (metadata) standards such as [W3C SSN](https://www.w3.org/TR/vocab-ssn/), [DDI/DISCO](https://www.ddialliance.org/Specification/RDF/Discovery), [DATS](https://datatagsuite.github.io/docs/html/), [ISO 19115 (Geospatial)](http://wiki.esipfed.org/index.php/Category:ISO_Explorer). Information should be copied up from the specialized metadata records to support description using a x-domain research data description standard. 

### Candidate properties 

| Vocabulary | properties |
|------------|------------|
| [W3C SSN](https://www.w3.org/TR/vocab-ssn/) | [sosa:observedProperty](https://www.w3.org/TR/vocab-ssn/#SOSAobservedProperty) [sosa:hasFeatureOfInterest](https://www.w3.org/TR/vocab-ssn/#SOSAhasFeatureOfInterest) [sosa:usedProcedure](https://www.w3.org/TR/vocab-ssn/#SOSAusedProcedure) [sosa:madeBySensor](https://www.w3.org/TR/vocab-ssn/#SOSAmadeBySensor) [sosa:phenomenonTime](https://www.w3.org/TR/vocab-ssn/#SOSAphenomenonTime) [ssne:hasUltimateFeatureOfInterest](https://w3c.github.io/sdw/proposals/ssn-extensions/#ssn-ext:hasUltimateFeatureOfInterest) |
| [W3C Data Cube](https://www.w3.org/TR/vocab-data-cube/) | [qb:concept](https://www.w3.org/TR/vocab-data-cube/#reference-concepts) [qb:componentProperty](https://www.w3.org/TR/vocab-data-cube/#reference-compspec) (also sub-properties [qb:dimension](https://www.w3.org/TR/vocab-data-cube/#reference-compspec) [qb:measure](https://www.w3.org/TR/vocab-data-cube/#reference-compspec) [qb:attribute](https://www.w3.org/TR/vocab-data-cube/#reference-compspec) |
| [DDI DISCO](https://htmlpreview.github.io/?https://raw.github.com/linked-statistics/disco-spec/master/discovery.html) | `disco:variable` `disco:universe` `disco:analysisUnit` |
| [DATS](http://www.github.com/biocaddie/WG3-MetadataSpecifications) | [dats:isAbout](https://github.com/biocaddie/WG3-MetadataSpecifications/blob/master/json-schemas/dataset_schema.json) [dats:producedBy](https://github.com/biocaddie/WG3-MetadataSpecifications/blob/master/json-schemas/dataset_schema.json) [dats:types](https://github.com/biocaddie/WG3-MetadataSpecifications/blob/master/json-schemas/dataset_schema.json) [dats:dimensions](https://github.com/biocaddie/WG3-MetadataSpecifications/blob/master/json-schemas/dataset_schema.json) |
| [schema.org](https://schema.org/docs/schemas.html) | [schema:variableMeasured](https://pending.schema.org/variableMeasured) [schema:measurementTechnique](https://schema.org/measurementTechnique) [schema:instrument](https://schema.org/instrument) [schema:usesDevice](http://schema.org/usesDevice) [schema:object](https://schema.org/object) |
| [ISO 19115](https://ddi-alliance.atlassian.net/wiki/spaces/DDI4/pages/548405259/ISO+19115+Geographic+Information+--+Metadata) | `iso19115:extent` `iso19115:rangeElementDescription` `iso19115:instrument` `iso19115:acquisitionInformation` |

### Approximate equivalences
* `disco:universe` ~ `ssne:hasUltimateFeatureOfInterest` ~ `iso19115:extent`
* `schema:object` ~ `sosa:hasFeatureOfInterest` ~ `disco:analysisUnit` ~ `dats:isAbout`
* `schema:variableMeasured` ~ `sosa:observedProperty` ~ `qb:concept` ~ `disco:variable` ~ `dats:dimensions` ~ `iso19115:rangeElementDescription`
* `schema:instrument` ~ `sosa:madeBySensor` (also `schema:usesDevice` for medical applications) ~ `iso19115:instrument`
* `schema:measurementTechnique` ~ `sosa:usedProcedure` ~ `dats:producedBy` ~ `iso19115:acquisitionInformation`

### Starting points
#### DCAT augmented for research data

![DCAT research profile](https://raw.githubusercontent.com/CSIRO-enviro-informatics/research-profile/master/image/DCAT%20research%20data%20profile.png)

**res:** is a new namespace for research dataset metadata

#### schema.org selected for research data

![schema.org research profile](https://raw.githubusercontent.com/CSIRO-enviro-informatics/research-profile/master/image/schema.org%20dataset.png)

The properties shown are associated with the schema.org classes indicated, as listed at [s:Dataset](https://schema.org/Dataset), [s:Action](https://schema.org/Action). 
`Action` is a potential super-class for act-of-observation - shown here to introduce some useful properties not normally associated with continuant entities, but likely to be useful in research dataset discovery. (Would [s:AchieveAction](https://schema.org/AchieveAction) or [s:CreateAction](https://schema.org/CreateAction) be better?)

### Other concerns
from **DDI**
* collectionFrequency (different to accrualPeriodicity)
* summary statistics ...
* questionaire is a kind of sensor or instrument

from **Geospatial**
* spatial resolution
* spatial aggregation level

Other important sources to correlate 
* THREDDS/netCDF 
