The vocabulary management process supports the resolution of vocabularies that have been accumulated (usually through an instance of the VertNet Migrator toolkit - https://github.com/VertNet/toolkit) and not yet standardized or vetted. Vocabularies are stored in a copy of the VocabulariesMaster.mdb database and managed from the VocabulariesManager.mdb database, which has queries and macros to assess and help to complete and standardize vocabularies such as geography and taxonomy. 
It is possible to have multiple instances of the VocabularyMaster database, but the authoritative and cumulative version is the one in the master directory of the DwCvocabs repository. For information on how to merge instances of VocabularyMaster.mdb into the authoritative version, see README - MergerSteps.txt. 

Managing an instance of a master vocabulary

1) With the two files VocabulariesManager.mdb and VocabulariesMaster.mdb in the directory c:\tempvertnetprocessing\source, open the file VocabulariesManager.mdb.

2) Open the macro "Unchecked local vocabs". This will open a series of queries for unresolved verbatim values of distinct vocabularies in data sheet view. Normally, many of these queries will be empty, as it is uncommon to encounter new values. Not all available vocabulary checking queries are opened by default. To change which vocabularies appear in this step, edit the macro "Unchecked local vocabs" and turn on or off any queries as desired.

3) For each window, resolve as many verbatim values to standard values as possible, filling in as many of the fields as possible. See the section "Common Vocabulary Fields" at the end of this document for explanations of the fields found in all of the vocabulary tables. Set the value of the field called "checked" to true (check the box) when the record is complete. Close each window when finished resolving that vocabulary. It is ok to close the window without completing all records in the vocabulary. Note that if you close the window, sort the contents, or change views for the query, all records that are checked (have a check in the checked field) will disappear from the query. There are additional tools and considerations to complete taxonomy and geography, as described in the sections below.

Check LookupClassification
4) With the query "Check Lookup Classification" open, sort on the genus field. To see if any of the genera on the list can be resolved with either the ITIS vertebrate authority or the AmphibiaWeb authority, which have been incorporated into the vocabulary manager, run the macro "Update Classification from Authorities". Any genera that could be resolved in this way will be in the query with the standardGenus, authority, standard, and checked fields all filled in. Only those that remain unchecked will have to be resolved. A good source of classification information in general is the Global Names Resolver (http://resolver.globalnames.org/). Copy the values of the genus field for unchecked records into the web user interface and click on the button labelled "Resolve Names". When all genera are resolved, close the query. Following are some notes on filling in specific classification fields:

genus - the original value of the genus field from the source. Never change values in this field.

standardGenus - should be the currently valid and accepted name for the given original genus. If a given genus is actually a name for a higher rank that genus, leave the standardGenus field blank.

family through kingdom - try to fill in all of these fields that apply. VertNet makes an attempt to be consistent with classification at higher levels, but the classifications given by distinct sources do not always match. This problem is prevalent in the higher classification of "fishes", for which we maintain classes for Acanthodii, Actinopterygii, Agnatha, Cephalaspidomorphi, Elasmobrachii, Galeaspida, Holocephali, Hyperoartia, Leptocardii, Myxini, Osteostraci, Petromyzontida, Placodermi, Pteraspidomorphi, Sarcopterygii. Try to be consistent with the higher classifications already found in the 
LookupClassification table and use the classifications in the same priority order as found in the authorities description below.

authority - the preferred authorities for VertNet differ by clade - AmphibiaWeb for amphibians, The Reptile database for reptiles, Avibase for birds, Catalog of Fishes for fish, Mammal Species of the World for mammals, then ITIS, then Catalog of Life, then Paleobiology Database, then Interim Register of Marine and Nonmarine Genera, then World Register of Marine Species, then any other available source. For any source in the priority list following Paleobiology Database, we do not consider the names to be "standard" and do not check the box for the field called "standard" in the LookupClassification table.

standard - false by default. Set to true (check the box) if the given genus matches the standardGenus and the authority used is one of those considered to be standard (see the explanation for the authority field, above).

error - the nature of the problem that makes the given genus not currently valid and accepted. The most common errors are the following:
"Genus misspelled." 
"Genus not found."
"Genus contains a subgenus."
"Genus is a synonym."
"Genus is a family."
"Genus contains an identification qualifier."
"Genus is a common name."
"Not a genus."
"Genus is a hybrid."
"Genus contains a specific epithet."

resolvelater - can be used to mark records that are for classifications that do not need to be resolved immediately (such as plants from a migrator run by VertNet, because VertNet only commits to resolving chordate classifications).

uri - a resolvable global unique identifier to the taxon name (Darwin Core scientificNameID) associated with the standardGenus. This is currently a placeholder and is not used.

Check LookupGeography
5) Before completing this step, make sure that there are no unchecked records in the query "Check LookupCountryCode". If there are, resolve them and close that query. 
With the query "GeogChecker" open, sort on the field called "key". For the GeogChecker query in particular, take heed that if you close the window, sort the contents, or change views, all records that are checked will disappear from the query. So do not do any of these actions until you are prepared to have those records no longer appear. 
To fill in as much of the geography as possible from accumulated knowledge in the LookupGeography and associated tables, run the macro "Update Geography - fill as possible". The result of this macro will be to fill in standard values in the open GeogChecker query to the extent possible. These values do need to be checked, as the process is not perfect nor necessarily complete. For example, the process does not fill in information for the fields waterbody, islandgroup, island, or municipality. It does generally fill in values for continent, country, countrycode, stateprovince, and county, but not necessarily completely.
Go through each record in the GeogChecker and resolve the ones you are committed to resolving. For VertNet, for example, we try to resolve all records completely for the United States, Canada, and Mexico and as many others as time and priorities permit.  

Following are some notes on specific geography fields:
key - the original combination of higher geographic fields (continent;country;stateProvince;county;island;islandGroup;waterbody;municipality) from the source. Never change the values in this field.

verbatimXXX - where XXX is the name of the Darwin Core field from which the original data were derived. Contains the original value of the field as found in the source. Never change the values in these fields.

continent - the standard value for the continent (if any) in which the geography in the record lies. The standard values for continents are associated with ISO3166-1 regions where possible in the table "CountryCodeCountries" and will be provided by the "Update Geography - fill as possible" macro if the records in the query "Check LookupCountryCode" have been fully resolved. The country codes for which the continent is indeterminate (and may therefore only be determined by more specific information in the record) are:
BV (Bouvet Island) has no continent
ES (Spain) may be Europe or Africa
IO (British Indian Ocean Territory) has no continent
RU (Russia) may be Europe or Asia
SH (Saint Helena Ascension, and Tristan da Cunha) has no continent
US (United States) may be North America or Oceania

country - the standard english common name for the country or territory given in the countrycode.

countrycode - the ISO3166-1 alpha-2 two-letter country code in which the entirety of the geography region lies. If the geography lies within no such region or in more than one, leave countrycode blank.

stateprovince - the standard vernacular name for the administrative geographic region at the next more specific level in common use within the country. Use the official name of the region in the most common official language of that region. In some countries, high-level administrative regions may exist for organizational purposes, but that are not in common use. Omit these. For example, do not use the five regions of Brazil, such as "Região Norte". Instead, stateprovince should be filled with unidades federativas (states), such as "Amazonas". 

county - the standard vernacular name for the administrative geographic region at the next more specific level in common use within the region given in the stateprovince field. Use the official name of the region in the most common official language of that region.

municipality - the standard vernacular name for the most specific administrative geographic region possible if more specific than the region given in the county field. Use the official name of the region in the most common official language of that region.

waterbody - the standard vernacular name for the water body. If the water body lies within a region with a single official language, use the name of that water body in that language, otherwise use the name of that water body in english. Fill in values in the waterbody field only if the key refers to a water body. For example, do not add "Caribbean Sea" for records of Jamaica unless the verbatim geography states includes that information. 

islandgroup - the standard vernacular name for the island group. If the island group lies within a region with a single official language, use the name of that island group in that language, otherwise use the name of that island group in english. Fill in the most specific named island group that encompasses the geography. For example, use "Sverdrup Islands" (which lie with the Queen Elizabeth Islands, which lie within the Canadian Arctic Arhipelago) for the geography of Ellef Ringnes Island.

island - the standard vernacular name for a single island. If the island lies within a region with a single official language, use the name of that island in that language, otherwise use the name of that island in english. Be sure to fill in the island group as appropriate.

error - a description of inconsistencies found or reference to geographic features not found from the original record. Following are some examples of error descriptions:
"Unable to unambiguously locate X within Y."
"X not found within Y."
"X not found."
"X has been subdivided."

incorrectable - false by default. Set to true if the original geography contains information that can not all be true simultaneously. For example, if the value of the field "key" is ";US;California;Mohave County;;;;", set the value of the field "incorrectable" to true, continent to "North America", country to "United States", countrycode to "US", and error to "Mohave County not found in California". Leave stateprovince and county blank. Do not set this field to true if the information in geography is consistent yet ambiguous. For example, if the value of the field "key" is ";ARG;Buenos Aires;;;;;", leave the value of the field "incorrectable" as false, set continent to "South America", country to "Argentina", countrycode to "AR", and error to "Unable to unambiguously locate Buenos Aires in Argentina". Leave stateprovince blank.

notHigherGeography - every part of the original geography in the field called "key" that is not an administrative region or waterbody or island or island group. For example, if value of the field "key" is "Europe;USSR;;;;;;", put "USSR" in the field "notHigherGeography". There is no need to add anything in the field "error" for these cases. If the value of the field "key" is "NORTH AMERICA;MEXICO;Veracruz, Tuxtla Mts, 0.5km W. of Cerro Balzapote BioStation B14;;;;;", put "Tuxtla Mts, 0.5km W. of Cerro Balzapote BioStation B14" in the field "notHigherGeography". Do use the information to provide the most specific geography possible. In the last example, for example, the county should be set to "San Andrés Tuxtla", as the specific location given in the original geography lies within that administrative division even though it was not stated in the original.

uri - a resolvable global unique identifier to the single most specific feature in the standardized higher geography (Darwin Core higherGeographyID). This is currently a placeholder and is not used.

Note: Do not edit any fields in geography other than those on the following list:
continent
country
countrycode
stateprovince
country
municipality
waterbody
islandgroup
island
notHigherGeography
uri
opinionBy
opinionDate
error
incorrectable

Note: Do not fill in geography for any part of the original geography that is ambiguous. For example, If the verbatimstateprovince is given as "Buenos Aires" and no other information is given, leave all geography blank, as it is not possible to isolate which of many possible features to which the geography may refer. If the verbatimstateprovince is given as "Buenos Aires" and the country is given as "Argentina", leave stateprovince blank because "Buenos Aires" may refer to the province of that name or to the capital city, which is an another first-level administrative division of Argentina.

Note: Do not include the administrative region type in the names of geographic fields unless the failure to do so will create confusion. For example, use "Jefferson" rather than "Jefferson County" in the county field; use "Ellesmere" rather than "Ellesmere Island" in the island field; but use "Long Island" for the island on which Queens County New York is found.

Note: At times the geography lies on the border of and contains more than one region at a given geographic administrative level. In these cases, the regions should be separated by a comma and placed in alphabetical order. If more a more specific administrative level in the same record also has multiple values, separate those values by a comma as well, but order them to correspond with the order of the values in the higher geographic administrative level. For example, if the value of the field "key" is ";USA;Oregon/California;Curry/Del Norte;;;;", set stateprovince to "California, Oregon" and county to Del Norte, Curry".

Common Vocabulary Fields
verbatimXXX - where XXX is the name of the field to which the vocabulary table applies. Contains the original value of the field as found in the source. Never change the values in these fields.

standardXXX - where XXX is the name of the field to which the vocabulary table applies. Gives the standard value that should be provided in place of the verbatimXXX value.

checked - false by default. Set to true (check the box) if the entire record is complete and correct.

uri - a resolvable global unique identifier to the standardized value for the term. For most vocabularies this is currently a placeholder and is not used. Exceptions include basisOfRecord, license, and type.

opinionBy - The name of the person who provided the most recent checked version of the record.

opinionDate - the date on which the most recent checked version of the record was made by the person in the opinionBy field.
