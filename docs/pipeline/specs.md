
# Specs

This document describes the specifications of the different resources rdf-respec works with.

## tool parameters

should be able to set input file.\
should be able to set output file.\
should be able to choose configuration file.

```
java -jar rdf-respec-0.1.0-SNAPSHOT.jar \
-c /path/to/source/config.yml \
-i /path/to/input.ttl \
-o /path/to/output.md 
```

## configuration file

should be able to set configurations per objecttype. e.g one configuration for skos:Concept and one for skos:ConceptScheme each.\
should be able to set which properties are used to build the hierarchy.\
should be able to set which property us used to select the section title.\
should be able to set prefixes.\
should be able to select language.

```
sources:
  reSpecMapping:
    type: hierarchical
    prefixes:
      rdfs: "http://www.w3.org/2000/01/rdf-schema#"
      skos: "http://www.w3.org/2004/02/skos/core#"
    config:
        -
            target: skos:Concept
            hierarchicalRelation: 
            direction: upward
            predicates:
                - skos:broader
            sectionTitlePredicate: skos:prefLabel
            attributeMapping:
            voorkeursterm: skos:prefLabel
            alternatieve term: skos:altLabel
            definitie: skos:definition
            bovenliggende begrip: skos:broader
            behoort tot: skos:inScheme
            exact overeenkomstig: skos:exactMatch
```

## input file 

rdf-respec only works with what is explicitly stated in the rdf-graph. 

```
@prefix skos: <http://www.w3.org/2004/02/skos/core#> .
@prefix sor: <https://begrippen.geostandaarden.nl/sor/nl/page/> .
@prefix dc: <http://purl.org/dc/terms/> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .

sor:constructie
  skos:narrower sor:pyloon, sor:zwembad, sor:geleideconstructie, sor:bordes, sor:sloof, sor:openbouwwerk, sor:afvalcontainer, sor:opslagtank, sor:gebouw, sor:installatie, sor:balkon, sor:reservoir, sor:toegangsdeur, sor:dek, sor:muur, sor:laadperron, sor:sluisdeur, sor:ruimte, sor:putdeksel, sor:straatmeubilair, sor:afdak, sor:bouwlaag, sor:landhoofd, sor:toegangstrap, sor:loopbrug, sor:verharding, sor:scherm, sor:paal, sor:hek, sor:dakkapel, sor:pijler, sor:kolk, sor:dok, sor:mast, sor:kunstwerk ;
  dct:created "2020-12-01"^^xsd:date ;
  dct:source "Basismodel Geo-informatie (NEN 3610:2020)"@nl ;
  skos:inScheme <https://begrippen.geostandaarden.nl/sor/nl> ;
  rdfs:label "Constructie"@nl ;
  skos:broader sor:object ;
  skos:exactMatch <https://begrippen.geostandaarden.nl/nen3610/nl/page/Constructie> ;
  a skos:Concept ;
  skos:prefLabel "Constructie"@nl ;
  skos:definition "Gebouwd object dat direct of indirect met de grond is verbonden en bedoeld is om ter plaatse te functioneren."@nl ;
  skos:altLabel "Bouwwerk"@nl .

sor:afdak
  dc:created "2021-02-12"^^xsd:date ;
  skos:closeMatch <http://ont.cbnl.org/cb/def/CB01101> ;
  dc:source "Samenhangende Objectenregistratie (SOR)"@nl ;
  skos:broader sor:constructie ;
  skos:inScheme <https://begrippen.geostandaarden.nl/sor/nl> ;
  skos:definition "Constructie aangebracht en vast verbonden aan de gevel van een pand, gericht op beschutting tegen weersinvloeden."@nl ;
  skos:prefLabel "Afdak"@nl ;
  a skos:Concept .
```

## output file

should have one section per resource\
should have at one table per section\
should have a unique Heading ID for each section `### My Great Heading {#custom-id}`\
should prune rows from table that have no value.\
should link to other sections in the document using Heading IDs (e.g. `| breder begrip | [Fiets](#begrip-Fiets)`)\
should not contain any styling

example:
```
## Constructie {#begrip-Constructie}
| Begrip               | https://begrippen.geostandaarden.nl/sor/nl/page/constructie                                                   |
| -------------------- | ------------------------------------------------------------------------------------------------------------- |
| voorkeursterm        | Constructie                                                                                                   |
| alternatieve term    | Bouwwerk                                                                                                      |
| definitie            | Gebouwd object dat direct of indirect met de grond is verbonden en bedoeld is om ter plaatse te functioneren. |
| bovenliggende begrip | [Object]{#begrip-Object}]                                                                                     |
| behoort tot          | [SOR thesaurus](#begrippenkader-SORThesaurus)                                                                 |
| exact overeenkomstig | https://begrippen.geostandaarden.nl/nen3610/nl/page/Constructie                                               |

### Afdak {#begrip-Afdak}
| Begrip               | https://begrippen.geostandaarden.nl/sor/nl/page/afdak                                                             |
| -------------------- | ----------------------------------------------------------------------------------------------------------------- |
| voorkeursterm        | Afdak                                                                                                             |
| definitie            | Constructie aangebracht en vast verbonden aan de gevel van een pand, gericht op beschutting tegen weersinvloeden. |
| bovenliggende begrip | [Constructie]{#begrip-Constructie}]                                                                               |
| behoort tot          | [SOR thesaurus](#begrippenkader-SORThesaurus)                                                                     |

```
