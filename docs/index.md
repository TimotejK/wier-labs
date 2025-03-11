--- 
title: "Web Information Extraction and Retrieval"
author: "Timotej Knez, Melanija Vezočnik, prof. dr. Marko Bajec, Slavko Žitnik"
date: "torek, 11. marec, 2025"
site: bookdown::bookdown_site
output: bookdown::gitbook
documentclass: book
description: "Instructions for the Web Information Extraction and Retrieval course labs"
---

# About the course {-}

<img src="img/book/oil-rig.png" style="display: block; margin: auto;" />

This script includes instructions for the lab work for the [**Web Information Extraction and Retrieval**](https://ucilnica.fri.uni-lj.si/course/view.php?id=284) course at the [Faculty for computer and information science](http://www.fri.uni-lj.si/), [University of Ljubljana](http://www.uni-lj.si/).

## Lab work {-}

Please regularly check the Weekly plan and course announcements for possible changes. Attendance at labs is optional. However, it is mandatory to attend all programming assignments’ defences.


## Programming assignments {-}
In this project, students will build a Retrieval-Augmented Generation (RAG) chatbot for a specific domain, integrating web information extraction and retrieval with generative AI. The project will be developed across three programming assignments:  

1. **Web Crawling and Information Gathering:** Students will collect relevant domain-specific data by crawling websites and extracting useful content.  
2. **Document Parsing and Knowledge Base Construction:** Extracted data will be processed, cleaned, and structured into a knowledge base optimized for retrieval.  
3. **Question Answering System Construction:** A chatbot will be built using RAG techniques, combining information retrieval with a language model to generate accurate and context-aware responses.  

By the end of the project, students will have a functional chatbot capable of answering domain-specific queries using real-world data. 
More information available in the course Moodle classroom.
  
### Course projects (alternative to the programming assignments) {-}   
If there is someone (or a group) that is interested in a specific field of information retrieval, we can arrange a custom assignment for her/him/them instead of working on the above three assignments. Such project can also be extended into a masters thesis.

<!-- Proposed projects:

* *Slovenian support for Apache Solr (update and evaluation)*: [Apache Solr](https://solr.apache.org) is an open-source search engine and widely adopted. It allows for rich customization and definition of own filters, tokenizers, processes, etc. The idea of the project is to update and evaluate the [Apache Solr plugin for Slovene](https://github.com/UL-FRI-Zitnik/solr-classla) - e.g., lemmatization, tokenization, named entity recognition.
  * Expected project deliverables are (a) updated plugin in a forked source code repository with documentation, (b) written report, and (c) practical presentation/evaluation of your work.
* *"Production-ready" crawler setup*: There exist some open-source projects such as [Apache Nutch](https://nutch.apache.org/) that allow full crawling functionalities + extensions. The idea of the project is to get to know the specifics of a selected crawler, solve PA1 with it, and use specific extensions (e.g., custom document parsing, filtering, ...).
  * Expected project deliverables are (a) a source code repository setup and with documentation for running the crawler, (b) written report, and (c) practical presentation/evaluation of your work.
* *Information retrieval systems evaluation*: Some information retrieval systems have been developed into rich systems that require some knowledge and configuration to create a useful search engine. The idea of the project is that you are given crawled data from PA1 and then you use an information retrieval system to create a Web-based search engine. The selection of a search engine must be agreed with the assistant - e.g.  [milvus search engine](https://milvus.io/)). 
  * Expected project deliverables are (a) Docker-based implementation of a search engine with documentation, (b) Web-based functions for searching and documents insert (bulk), and (c) written report.
* *Other ideas* from the fiels of Web information extraction. You can think of graph databases; ontologies, SPARQL with databases such as Oracle Graph Database, Amazon Neptune; CKAN review and extensions; [RelFinder](http://www.visualdataweb.org/relfinder.php#:~:text=Interactive%20Relationship%20Discovery%20in%20RDF%20Data&text=The%20RelFinder%20helps%20to%20get,a%20global%20and%20detailed%20level.) rewrite to Javascript from [Adobe Flex implementation](https://github.com/VisualDataWeb/RelFinder); ... -->
