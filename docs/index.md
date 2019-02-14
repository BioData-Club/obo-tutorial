# Introduction

In this tutorial we use a running example: histology assays of mice and rats. The example is small and fictional but it's based on real datasets. Biology and biomedicine are vast fields, and this example won't be a close fit to every reader's field of research. The advantage is that the running example keeps the tutorial concrete and practical. Once you learn the various techniques for working with this example data, hopefully you'll see how you can apply the same techniques to your work in your own field.


## Data Before

Take a look at the [data-before.csv](https://github.com/OHSU-Library/obo-tutorial/blob/master/examples/data-before.csv) file. It's just a spreadsheet in comma-separated-values format. What information does it contain? It's hard to say without some context.

Each row of the spreadsheet describes an "observation" made by an investigator of a study subject -- a mouse or a rat. The columns divide the information up into different fields. What does each column mean? Lab computers are stuffed with spreadsheets that have cryptic headers, or even lacking any headers. Those spreadsheets hang around long after the memory of what the columns mean has faded. Columns can become strange mixtures of special cases, especially when data about different sorts of things gets crammed into the same table. Some people may choose to ignore the headers and instead try to generalize from the values in the column instead.

What about the values? These are often more cryptic than the headers. What does "B6C3F1" mean? Worse, familiar names can be very misleading. Does "histology" mean a general type of assay or a specific protocol for this study? Many common date formats are completely frustrating: do they mean "MM/DD/YY" or "DD/MM/YY"?

During the study, as it's being designed and the data is being collected, the meanings of the columns and the values will be clear to the investigators -- more or less. The problem is communicating this information: to other researchers in the same lab, to researchers in other labs, and even to the original study authors at some time in the future. The solution to the communication problem is to be clear from the outset. If we are are clear enough in communicating to each other, we will also be able to communicate more clearly to our machines, resulting in better search and analysis.


## Goals

This tutorial is about some practical techniques that you can use to communicate your data better. Most of these techniques are really very simple. There are really just two hard parts: applying them consistently yourself, and coordinating with others.

These are our goals:

- communicate clearly, reduce ambiguity
- integrate data, build on existing resources
- validate data, check for errors and inconsistencies
- improve search and analysis using multiple axes of classification

Ontologies are more than just systems of names. They express statements about the things that they name: statements about things in the world. Your data also make statements about the world. We work hard to make sure that all these statements are true. We also work hard to make sure that they're useful. By using ontologies and the techniques in this tutorial, we can link our data together into a larger system of statements about the world. By communicating clearly, and sharing what we know, we make our data more valuable than ever before.


## Data After

Let's return to the [data-before.csv](https://github.com/OHSU-Library/obo-tutorial/blob/master/examples/data-before.csv) spreadsheet and get a preview of what's to come. Here's what each of the columns is supposed to mean:

- datetime: when the observation was made
- investigator: the initials of the person who made the observation
- subject: the identifier of the subject that was observed
- species: the name of the species of the subject
- strain: the name of the genetic variant that the subject belongs to
- sex: the biological sex of the subject
- group: the identifier of the group that the subject is assigned to in the study
- protocol: the name of the protocol used for the observation
- organ: the name of the subject's organ that was observed
- morphology: the name of the disease or other abnormal state of the organ
- qualifier: a keyword to further describe the morphology
- comment: unstructured notes made by the investigator about the observation

Now we'll make a table with a row for each of these. We'll describe the current format of the cells, suggest a better format, and name a technique for converting the current format to the new format. We'll see more about each of these techniques in the coming sections. 

Some of the acronyms might not yet be familiar:
- an [IRI](https://en.wikipedia.org/wiki/Internationalized_resource_identifier) is an Internationalized Resource Identifier for naming things such as people, studies, study subjects, classes of things, relations between thing, and anything else we care to give a name to
- an [ORCID](http://orcid.org) is a special IRI for a researcher
- an application ontology is a collection of ontology terms for a particular purpose; we'll use terms from these reference ontologies:
    - [NCBITaxon](http://www.obofoundry.org/wiki/index.php/NCBITaxon:Main_Page) is a translation of the [NCBI Taxonomy](http://www.ncbi.nlm.nih.gov/Taxonomy/Browser/wwwtax.cgi)
    - [PATO](http://obofoundry.org/wiki/index.php/PATO:Main_Page) is the Phenotypic Quality Ontology
    - [OBI](http://obi-ontology.org) is the Ontology for Biomedical Investigations
    - [Uberon](http://uberon.org) is an integrated cross-species ontology
    - [MPATH](http://obofoundry.org/cgi-bin/detail.cgi?id=mouse_pathology) is the Mouse Pathology Ontology


Column       |Current Format            |Better Format             |Technique
-------------|--------------------------|--------------------------|----------
datetime     |idiosyncratic date string |ISO standard              |parse/replace
investigator |investigator initials     |ORCID                     |replace
subject      |string                    |application ontology IRI  |rename
species      |English, mixed case       |NCBITaxon IRI             |MIREOT
strain       |string                    |application ontology IRI  |QTT
sex          |English, mixed case       |PATO IRI                  |MIREOT
group        |string                    |application ontology IRI  |rename
protocol     |ambiguous string          |OBI IRI                   |MIREOT
organ        |English, mixed case       |Uberon IRI                |extract
disease      |English, mixed case       |MPATH IRI                 |MIREOT
qualifier    |English, mixed case       |PATO IRI                  |MIREOT
comment      |English unstructured text |--                        |keep


The updated data is in [data-after.csv](https://github.com/OHSU-Library/obo-tutorial/blob/master/examples/data-after.csv) and the final result of this tutorial is [obo-tutorial.owl](https://github.com/OHSU-Library/obo-tutorial/raw/master/examples/obo-tutorial.owl). To learn how to get from here to there, [read on!](https://github.com/OHSU-Library/obo-tutorial/blob/master/docs/names.md).

