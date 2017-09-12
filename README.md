# BOT: Building Topology Ontology

## Version control
The latest version is available from w3id.org/bot#. This points to the master branch of this repository.
Developments are stored in the Development branch and feature branches are created for features that are not yet implemented in the development branch.

## Adding content to BOT
1. Fork this repository. 
2. Add contribution to bot or separate alignment file.
3. Commit your changes and submit a [pull request](https://github.com/perma-id/w3id.org/pulls).
4. w3c-lbd administrators will review your pull request and merge it if everything looks correct. Once the pull request is merged, the changes go live immediately.

## BOT in the literature
*Mads Holten Rasmussen, Pieter Pauwels, Christian Anker Hviid and Jan Karlshøj (2017) Proposing a Central AEC Ontology That Allows for Domain Specific Extensions, Lean and Computing in Construction Congress (LC3): Volume I – Proceedings of the Joint Conference on Computing in Construction (JC3), July 4-7, 2017, Heraklion, Greece, pp. 237-244 http://itc.scix.net/cgi-bin/works/Show?lc3-2017-153*

## Aligning to BOT
As BOT is proposed as a central ontology in the domain of AEC/FM industry alignments with existing domains need to be provided. Ontologies defining the alignment are given in this repository and file naming is given by <ontologname>Alignment.ttl.

So far an alignment for the following ontologied has been provided:

SAREF4Bldg [link](https://w3id.org/def/saref4bldg#)

ThinkHome [link](https://www.auto.tuwien.ac.at/downloads/thinkhome/ontology/BuildingOntology.owl)

DogOnt [link](http://elite.polito.it/ontologies/dogont.owl#)

ifcOWL [link](http://www.buildingsmart-tech.org/ifcOWL/IFC4_ADD2#)

## Example of using BOT

Example of using BOT in [Turtle syntax](https://www.w3.org/TeamSubmission/turtle/).
```turtle
@prefix bot:  <https://w3id.org/bot#> .
@prefix inst: <https://example.org/projectXX/> .
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .

inst:buildingA a bot:Building ;
               bot:hasStorey inst:storey00 ,
                             inst:storey01 .
							 
inst:storey00 a bot:Storey ;
              bot:hasSpace inst:space00aa ,
                           inst:space00cg .
						   
inst:storey01 a bot:Storey .

inst:space00aa a bot:Space ;
               bot:containsElement inst:heater235 .
               bot:adjacentElement inst:wall443 ,
                                   inst:floor23 .
								   
inst:space00cg a bot:Space .
inst:heater235 a bot:Element .
inst:wall443 a bot:Element .
inst:floor23 a bot:Element .
```
specifying classes is not necessary as these are inferred by the domain and range specified in the ontology.

## Extending BOT
### By specifying subclasses
The following will automatically infer that an instance is a bot:Element given that the instance is specified as a h:SpaceHeater:
```turtle
@prefix bot:  <https://w3id.org/bot#> .
@prefix h:  <https://example.org/heatingSystem#> .
@prefix rdf:  <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix rdfs:  <http://www.w3.org/2000/01/rdf-schema#> .
@prefix owl:  <http://www.w3.org/2002/07/owl#> .

h:SpaceHeater a owl:Class ;
              rdfs:subClassOf bot:Element .
```
### By specifying subproperties
The following will automatically infer bot:containsElement between a space and an element when the h:heatedBy property is present between the two. Furthermore it will be inferred that the element is both a h:SpaceHeater and a bot:Element.
```turtle
@prefix bot:  <https://w3id.org/bot#> .
@prefix h:  <https://example.org/heatingSystem#> .
@prefix rdf:  <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix rdfs:  <http://www.w3.org/2000/01/rdf-schema#> .
@prefix owl:  <http://www.w3.org/2002/07/owl#> .

h:SpaceHeater a owl:Class .
h:heatedBy a owl:ObjectProperty ;
             rdfs:subPropertyOf bot:containsElement ;
             rdfs:range h:SpaceHeater .
```
