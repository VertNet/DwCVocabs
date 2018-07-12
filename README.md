VertNet Darwin Core Vocabularies
=========

This repository contains files containing lists of distinct combinations of verbatim original values for data passing through data set-specific instances of the VertNet Darwin Core Migrator Toolkit (https://github.com/VertNet/toolkit). As much as possible, these vocabularies have also been annotated with recommended standardized values for the verbatim orignal terms. These files are used in the VertNet Darwin Core Migrators to reconcile real-world values for Darwin Core terms to somewhat more standardized values to facilitate searching in aggregated data stores.

## Principles
We try to resolve verbatim values to standard values for terms in Darwin Core that recommend a controlled vocabulary.<br>
We try to resolve verbatim values to fully spelled out standard equivalents in English.<br>
Standardized values for items in a list are separated by " | ".<br>
We use the geopolitical concept of continents following the seven continent model, which include Africa, Antarctica, Asia, Europe, North America (with Central America and the Caribbean), Oceania (with Australasia) and South America.<br>
A water body wholly surrounded by a geopolitical continent is considered to be part of that continent.<br>

## Geography
Darwin Core geography consists of the terms continent, country, countryCode, stateProvince, county, municipality, waterbody, islandGroup, and island. Geography is reconciled as the combination of all of these terms at once, rather than individually. This is to avoid introduction of incorrect standardization when there are ambiguities, inconsistencies, or other errors within the content of the geography fields. Standardized geography is intended to reflect current administrative divisions. Multiple sources have been used to reconcile these geographic combinations, and the sources are not cited in the file. More often than not, Wikipedia has been used, though the Global Administrative Areas data set (GADM, http://www.gadm.org/) and The Getty Thesaurus of Geographic Names (TGN, http://www.getty.edu/research/tools/vocabularies/tgn/), and Google Maps have also been commonly consulted sources.

As with many of the vocabularies, not all records have been resolved for geography. VertNet makes a commitment to always resolve geography fully for the US, Canada, and Mexico. Resolution of geography from other regions varies considerably. You can see the status of geography record resolution by country in the file GeogResolutionStatus.csv (https://github.com/VertNet/DwCVocabs/blob/master/vocabs/GeogResolutionStatus.csv).

The country level regions should correspond exactly with those given a distinct ISO 3166-1-alpha-2 country code. The values for the country code should be as given in that standard. The values of the country field used in this resource are given in the file country.csv (https://github.com/VertNet/DwCVocabs/blob/master/vocabs/country.csv). 

Standard values of geographic regions more specific than the country level should be in the predominate language of that region as much as possible. 
Example: "Toscana" rather than "Tuscany".

Abbreviations should be spelled out.
Example: "Saint Thomas" rather than "St. Thomas".

Values or parts of values that do not correspond to Darwin Core higher geography (continent, country, stateprovince, county, municipality, waterbody, islandgroup, island) should be copied to the field "notHigherGeography".
Example: "Lassen National Park"

Multiple names should not be given in the standard value of a given term. These multiple values should be noted in the field "error" using the pattern "[original value that is multiple] is not a single administrative unit" for each such multiple value in the original. 
Example for "Wales/England" in stateProvince and "Breconshire/Gloucesterhire" in county: "Wales/England is not a single administrative unit. Breconshire/Gloucesterhire is not a single administrative unit."
 
If there is an inconsistency in the record (parts of the location that do not coincide) set the incorrectable field to True and include among the standard values only those parts that are not inconsistent. The inconsistency should be noted in the field "error" using the pattern "There is no [more specific named place] in [less specific named place]. 
Example: "There is no Chatham County in Florida."

Ambiguities of any part of the record that could result in a different standard interpretation if more information was given should be noted in the field "error" using the pattern "There is more than one [value that is ambiguous] in [most specific region given]" 
Example: "There is more than one Washington County in the United States."

Any part of the record that cannot be found should be noted in the field "error" using the pattern "Unable to locate [named place] in [most specific region that could be resolved]".
Example: "Unable to locate Bird Island in Barnstable County."

Waterbodies are not provided for records in which they are not given. For example, though the Hawaiian Islands are in the North Pacific Ocean, "North Pacific Ocean" is not included in records where a reference to the waterbodyis not given. The principle is that locations not in the waterbody should not include the waterbody. 
## Classification
Classification provides higher classifications (according to Catalog of Life wherever possible) based on genus only. The authority used to reconcile the standardized value is given in the file.

## Standardized Reference Data Set for Vertebrate Taxon Name Resolution

[https://github.com/tucotuco/DwCVocabs/blob/master/vocabs/tests/VertNetTaxonomyTestSet.csv](https://github.com/tucotuco/DwCVocabs/blob/master/vocabs/tests/VertNetTaxonomyTestSet.csv)

This data set consists of a random set of 1000 records of distinct taxon name combinations from the 18 April 2015 snapshot of the data aggregated in VertNet. The data were carefully vetted to track various kinds of errors as well as synonyms. Entries were resolved to determine valid taxon name wherever possible using the workflow documents at (https://github.com/tucotuco/DwCVocabs/wiki/Standardized-Reference-Data-Set-for-Vertebrate-Taxon-Name-Resolution).

Research based on these data (Zermoglio et al. 2016) has been published at http://journals.plos.org/plosone/article?id=10.1371/journal.pone.0146894.
