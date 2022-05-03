--- 
title: "Web Information Extraction and Retrieval"
author: "assist. prof. dr. Slavko Žitnik and prof. dr. Marko Bajec"
date: "Tuesday, 03. May, 2022"
site: bookdown::bookdown_site
output: bookdown::gitbook
documentclass: book
description: "Instructions for the Web Information Extraction and Retrieval course labs"
---

# About the course {-}

<img src="img/book/oil-rig.png" width="359" style="display: block; margin: auto;" />

This script includes instructions for the lab work for the [**Web Information Extraction and Retrieval**](https://ucilnica.fri.uni-lj.si/course/view.php?id=284) course at the [Faculty for computer and information science](http://www.fri.uni-lj.si/), [University of Ljubljana](http://www.uni-lj.si/).

## Lab work {-}

The lab work in this course is consultation-like, so we do not check attendance. The assistant is available during the scheduled times and you can select the time to ask questions in person, while you are also encouraged to use [the course Discord channel](https://discord.gg/WBSkNtGE9G).


## Programming assignments {-}

* Programming assignment 1: Web crawling
* Programming assignment 2: Document parsing
* Programming assignment 3: Indexing & querying
    
More information available in the course Moodle classroom.    
  
### Course projects (alternative to the programming assignments) {-}   
If there is someone (or a group) that is interested in a specific field of information retrieval, we can arrange a custom assignment for her/him/them instead working on the above three assignments. Such project can also be extended into a masters thesis.

Proposed projects:

* *Slovenian support for Apache Solr*: [Apache Solr](https://solr.apache.org) is an open-source search engine and widely adopted. It allows for rich customization and definition of own filters, tokenizers, processes, etc. The idea of the project is to implement an Apache Solr plugin that would integrate [CLASSLA library](https://github.com/clarinsi/classla) - e.g., lemmatization, tokenization, named entity recognition.
  * Expected project deliverables are (a) implemented plugin in a source code repository with documentation, (b) written report, and (c) practical presentation of your work.
* *Information retrieval systems evaluation*: Some information retrieval systems have been developed into rich systems that require some knowledge and configuration to create a useful search engine. The idea of the project is that you are given crawled data from PA1 and then you use an information retrieval system to create a Web-based search engine. The selection of a search engine must be agreed with the assistant - e.g.  [milvus search engine](https://milvus.io/)). 
  * Expected project deliverables are (a) Docker-based implementation of a search engine with documentation, (b) Web-based functions for searching and documents insert (bulk), and (c) written report.
