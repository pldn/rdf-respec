# rdf-respec
A tool for showing rdf in respec-based technical documents and web standards

## Use cases

- As a developer, I want to understand the model from a website;
- As a modeler, I want to show my model, using regular publishing tools (static websites, etc, etc);

## Requirements

- Should be able to process RDF in different serialisations (turtle, json-ld, XML-RDF);
- Should be able to process common vocabularies, such as:
  - SKOS (lists of concepts and definitions, taxonomies);
  - OWL/RDFS (vocabularies: class, properties, taxonomies, ontologies - structures);
  - SHACL (shapes, data models, profiles);
  - DCAT / Dublin core (models as assets, datasets, descriptions of models and links to source documents)
- Should be able to generate tables and sections with descriptions from the RDF data;
- Should be able to generate diagrams (preferable without using external tools).

## Possible solutions

- Generating MD or HTML files from RDF files;
  - Pro: resulting MD/HTML files can be read directly by the browser, no need for extra libraries
  - Con: changes to a RDF file requires regeneration
  - Con: not possible to use directly with a dynamic solution (e.g. a triplestore, etc)
- Interpreting RDF files on the fly, using custom libraries
  - Pro: works just like yml, but now its turtle
  - Pro: can be customised at runtime, so can be used with different solutions (respec, jekyll, etc)
  - Con: requires external libraries

## First MVP

We opt for the generation of MD file from RDF files:
- The generation will be performed by a single java jar;
- The execution can be made part of git actions, so a developer only needs to commit the turtle;
- Actually, this is the way respec pages are created, we only add an additional step;
- The java jar can also be used locally, or part of some other build pipeline.

Creating a javascript library for runtime interpretation might still be something for the furture.
