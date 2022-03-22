# Programming assignment 2 {#PA2}

<img src="img/book/spider-01.png" />

## Introduction

The goal of this programming assignment is to implement three different approaches for the structured data extraction from the Web:

* (A) Using regular expressions
* (B) Using XPath
* (C) *RoadRunner*-like Wrapper implementation or other automatic content extraction

## Instructions

In [a compressed file](data/pa2/WebPages.zip) there are four Web pages - two per Web site ([Overstock](https://www.overstock.com/), [Rtvslo.si](https://www.rtvslo.si/)). In Figure \@ref(fig:overStockSample) we define the names of the data items for a data record you will need to extract from *Overstock* sample Web sites. The provided sample Web sites contain a list of data records, which all need to be processed. In Figure \@ref(fig:rtvSloSample) we also provide the names of the data items for the second sample Web sites. In the provided *Rtvslo.si* example, there is only one data record per sample page.

<div class="figure" style="text-align: center">
<img src="img/pa2/overstock.png" alt="Overstock.com Web page sample." width="600" />
<p class="caption">(\#fig:overStockSample)Overstock.com Web page sample.</p>
</div>

<div class="figure" style="text-align: center">
<img src="img/pa2/rtvslo.png" alt="RtvSlo.si Web page sample." width="800" />
<p class="caption">(\#fig:rtvSloSample)RtvSlo.si Web page sample.</p>
</div>

Similarly to given Web pages above, find **your own example of two similar Web pages** (can be either list pages or detail pages from other domains than given ones) and define the names of the data items that you will  extract. The two Web pages **must** contain some same data item types with different values and a list of data items of different lengths. 

For each of the three types of the pages, implement the following:

(A) Data extraction using regular expressions only.
(B) Data extraction using XPath only.
(C) Generation of extraction rules using automatic Web extraction algorithm.

Input HTML files to these method should be pre-rendered.

The implementation must contain a file named *run-extraction.py* that can be run from command-line to test all the methods. The file should take one parameter as input - type of extracting algorithm (A, B, C). The script will be called as follows: `python run-extraction.py A`. Output should be written to standard output for all the Web pages.

Instructions to run the code must be listed in the README.md file. 

### Regular expressions implementation

For each given Web page type implement a separate function that will take HTML code as input. The method should output extracted data in a JSON structured format to a standard output. Each data item must be directly extracted using **a single regular expression**. But you can extract multiple data items using one regular expression (this might help you when extracting optional items in list pages). 

### XPath implementation

For each given Web page type implement a separate function that will take HTML code as input. The method should output extracted data in a JSON structured format to a standard output. Each data item must be directly extracted using an XPath expression. If the extracted value should be further processed, use regular expressions or other techniques to normalize them (for text only!).

### Automatic Web extraction algorithm implementation

Implement a method that will take two HTML Web pages of the same type as input. The method should output a human-readable *wrapper* that could be used to extract data from a given type of Web pages. The wrapper can be represented as *union-free regular expression* or any other format, based on which someone could implement a Web data extractor. Web data extractor implementation is not needed for the purposes of this assignment.

You **must not** use code of the existing implementations but you can check it out or read related papers to get more in-depth knowledge if interested (not necessary for the purposes of this programming assignment). 

You can implement an algorithm of your choice. We propose to implement one of the following:

* *RoadRunner-like* implementation:
Follow the implementation guidelines presented at the lectures. Apart from the guidelines you can introduce various heuristics (e.g. taking tag attributes into account, additional rules, ...) that may help you with the wrapper generation. Also, you can implement some preprocessing steps prior to running the algorithm. It is expected, that the generated wrapper may miss some of the data items and may include other unrelevant data items in the output. You should comment or identify, which data items have not been recognized using the algorithm. Full (official) implementation of the RoadRunner algorithm proposed in [the literature](http://www.dia.uniroma3.it/db/roadRunner/publications.html) is [available online along with some examples](http://www.dia.uniroma3.it/db/roadRunner/software.html). Check also other descriptions, e.g. [paper 1](http://vldb.org/conf/2001/P109.pdf) or [paper 2](https://link.springer.com/content/pdf/10.1007%2F3-540-46140-X_21.pdf). 

* *Webstemmer-like* implementation:
Follow the implementation guidelines of the [Webstemmer algorithm](http://www.unixuser.org/~euske/python/Webstemmer/howitworks.html) and try to implement it on your own.

* Other implementations (for this option consult with the assistant):

  Search the Internet for other existing automatic extraction techniques and implement an appropriate algorithm, such as [Automatic Web Content Extraction by Combination of Learning and Grouping, Wu et al., WWW 2015](https://dl.acm.org/doi/pdf/10.1145/2736277.2741659?casa_token=-Ju2S-ZbMfUAAAAA:UVv6AqtHeu6XS_e6bmE0F5rzDZjLcJBqXdH4uaODUXy7QbszCIzezIgZ01RlPeL581w2_PGejmSa), [Automatic Extraction of Informative Blocks from Webpages, Debnath et al., SAC 2005](http://infolab.stanford.edu/~prasen9/sac05.pdf) or [Automatic data extraction of Websites using data path matching and alignment, Chu et al., 2015](https://ieeexplore.ieee.org/document/7323006). 

  You must not use libraries such as [jusText](https://github.com/miso-belica/jusText), [trafilatura](https://github.com/adbar/trafilatura), [readability](https://github.com/mozilla/readability), [Newspaper3k](https://github.com/codelucas/newspaper/), [BoilerPy3](https://github.com/jmriebold/BoilerPy3), [draget](https://github.com/dragnet-org/dragnet), [Goose3](https://github.com/goose3/goose3) or [news-please](https://github.com/fhamborg/news-please). In case you are interested in such libraries, you can re-implement one of them for the Slovene language (the work can be then extended to a MSc. thesis).

## What to include in the report

The report should follow the [standard structure](https://fri.uni-lj.si/sl/napotki-za-pisanje-porocila).

In the report include the following (max 2 pages + outputs):

* Description of the two selected Web pages and identification of data items and data records (similarly as in the instructions above).
* Regular expressions implementation: a list of regular expressions that extract data from all the pages.
* XPath implementation: a list of XPath expressions that extract data from all the pages.
* Automatic Web extraction implementation: 
  * Pseudocode of your algorithm implementation and describtion of its implementation. Explain all the  rules or heuristics. Justify each inclusion of a rule or heuristics. Also cite the source of the idea if you re-implemented some feature from somewhere else (e.g. literature, full RoadRunner implementation).
  * Provide an output *wrapper* for each Web page pair (i.e. three outputs). Each output should not exceed one A4 paper. 

## What to submit

Push your work into the same repository as you used for the first assignment. Structure the repository must comply with the following structure:

 * a file *pa2/report-extraction.pdf* - PDF report.
 * a file *pa2/README.md* - Short description of the project and instructions to install, set up and run all the methods.
 * a folder *pa2/implementation-extraction* - Implementation of the methods along with *run-extraction.py*. CAUTION: Use relative paths to files in your repository and take into account that script will be run within the *implementation-extraction* folder.
 * a folder *pa2/input-extraction* - All the three types of Web pages that implemented methods can consume.

<!-- 
## Grading schema

All the submissions will be graded semi-automatically by the assistant. Plagiarism check will be run across all the submissions. Grading will begin after the last late submission day. The submission time will be selected as the last commit time in the repository. 

The maximum score of 100 will consist of the following (tentative grading schema):

Points | Item
------ | ----
10 | Selection of two similar Web pages
20 | Regular expressions and XPath implementation
30 | Automatic Web extraction implementation and description
30 | Reproducibility of your work (10 points per method)
10 | Submission compliance (report, readme instructions, repository structure)

Selected groups will need to defend their work during the lab hours. If a group does not agree with their achieved score, it will be able to "negotiate"/defend their programming assignment submission.
-->

