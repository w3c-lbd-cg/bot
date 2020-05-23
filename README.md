# BOT: Building Topology Ontology 

## BOT in the literature

### Reference publication

*Mads Holten Rasmussen, Maxime Lefrançois, Georg Ferdinand Schneider, Pieter Pauwels (2020). [BOT: the Building Topology Ontology of the W3C Linked Building Data Group](http://www.semantic-web-journal.net/content/bot-building-topology-ontology-w3c-linked-building-data-group-0), Semantic Web Journal, IOS Press*

### Previous publications

*Mads Holten Rasmussen, Pieter Pauwels, Christian Anker Hviid and Jan Karlshøj (2017) Proposing a Central AEC Ontology That Allows for Domain Specific Extensions, Lean and Computing in Construction Congress (LC3): Volume I – Proceedings of the Joint Conference on Computing in Construction (JC3), July 4-7, 2017, Heraklion, Greece, pp. 237-244 [http://itc.scix.net/cgi-bin/works/Show?lc3-2017-153](http://itc.scix.net/cgi-bin/works/Show?lc3-2017-153)*

*Mads Holten Rasmussen, Pieter Pauwels, Maxime Lefrançois, Georg Ferdinand Schneider, Christian Anker Hviid and Jan Karlshøj (2017) Recent changes in the Building Topology Ontology, 5th Linked Data in Architecture and Construction Workshop (LDAC2017), November 13-15, 2017, Dijon, France, [https://www.researchgate.net/publication/320631574_Recent_changes_in_the_Building_Topology_Ontology](https://www.researchgate.net/publication/320631574_Recent_changes_in_the_Building_Topology_Ontology)*

*Mads Holten Rasmussen, Christian Anker Hviid and Jan Karlshøj (2017) Web-based topology queries on a BIM model, 5th Linked Data in Architecture and Construction Workshop (LDAC2017), November 13-15, 2017, Dijon, France, [https://www.researchgate.net/publication/320757039_Web-based_topology_queries_on_a_BIM_model](https://www.researchgate.net/publication/320757039_Web-based_topology_queries_on_a_BIM_model)*

*Georg Ferdinand Schneider (2017) Towards Aligning Domain Ontologies with the Building Topology Ontology, 5th Linked Data in Architecture and Construction Workshop (LDAC2017), November 13-15, 2017, Dijon, France, [https://www.researchgate.net/publication/320878270_Towards_Aligning_Domain_Ontologies_with_the_Building_Topology_Ontology](https://www.researchgate.net/publication/320878270_Towards_Aligning_Domain_Ontologies_with_the_Building_Topology_Ontology)*

## HTML Documentation

Latest versions of BOT: 

- URI: [https://w3id.org/bot#](https://w3id.org/bot#).
- Canonical URI for the HTML Representation [https://w3id.org/bot/bot.html](https://w3id.org/bot/bot.html).
- Canonical URI for the Turtle Representation [https://w3id.org/bot/bot.ttl](https://w3id.org/bot/bot.ttl).


## Adding content to BOT

1. Fork this repository. 
2. Add contribution to bot or separate alignment file.
3. Validate that the turtle file is still valid using for example Protegé or http://ttl.summerofcode.be/
4. Commit your changes and submit a [pull request](https://github.com/w3c-lbd-cg/bot/pulls).
5. w3c-lbd administrators will review your pull request and merge it if everything looks correct. Once the pull request is merged, the changes go live immediately.


## Live demos using BOT

[Step by step introduction with visualizations](https://w3c-lbd-cg.github.io/bot/tutorial/)

[Queries on a 3D-model](https://forge-sparql.herokuapp.com/)


## BOT and reasoning
[Hylar](https://www.npmjs.com/package/hylar) is a simple js library for doing reasoning on a set of triples. To get it up and running, do the following:

1) Initialize a new project with ```npm init```
2) Add Hylar as dependency ```npm install --save hylar``` (first you need node and node-gyp: [https://github.com/nodejs/node-gyp](https://github.com/nodejs/node-gyp))
3) Adjust the following code sample to your needs and try it out
```javascript
var Hylar = require('hylar');
var fs = require('fs');
h = new Hylar();

//Files and settings
var mimeType = 'text/turtle';
var files = [];
files.push('triples.ttl');
files.push('bot.ttl');

var query = "PREFIX bot: <https://w3id.org/bot#>\
SELECT * WHERE {?subject a bot:Zone}";

//Get file content
triples = '';
for(var i in files){
    var string = fs.readFileSync(files[i], "utf8").toString();
    if(i == 0){
        triples = string;
    }else{
        triples+='\n'+string;
    }
}

//Do reasoning and run query
h.load(triples, mimeType)
    .then(response => {
        return h.query(query);
    })
    .then(results => {
        console.log(results) // log results to console
    });
```

