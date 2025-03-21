# Programming assignment 1 {#PA1}

<img src="img/book/spider-01.png" />

## Introduction

The goal of this programming assignment is to build a standalone crawler that will crawl websites within your chosen domain. The crawler will roughly consist of the following components (Figure \@ref(fig:crawlerArchitecture)):

* HTTP downloader and renderer: To retrieve and render a web page.
* Data extractor: Minimal functionalities to extract images and hyperlinks.
* Duplicate detector: To detect already parsed pages.
* URL frontier: A list of URLs waiting to be parsed.
* Datastore: To store the data and additional metadata used by the crawler.

<div class="figure" style="text-align: center">
<img src="img/pa1/crawler.png" alt="Web crawler architecture." width="500" />
<p class="caption">(\#fig:crawlerArchitecture)Web crawler architecture.</p>
</div>

## Instructions

Implement a web crawler that will crawl websites within your chosen domain. You can choose a programming language of your choice.

Choose a domain you will be exploring in your project assignments. We have prepared some domains that could be interesting: 

- *University of Ljubljana (UL) and Faculty of Computer and Information Science (FRI) regulations*: Create a system for answering quesitons about the study process at the University of Ljubljana. The goal is to answer questions like: "What are the requirements for enrolling in a higher grade", "What is the class web information extraction and retrieval about?" or "What is the Code of Ethics at UL". To achieve this, you should crawl the [UL website](https://www.uni-lj.si/) and [FRI website](https://www.fri.uni-lj.si/sl) and create a database of information with special emphasis on regulatory documents. In this domain, the amount of documents will be smaller; however, you will need to extract information from PDF documents, which can be more challenging than extracting information from HTML pages.

- *Slo-Tech*: Extract discussions, trends, and insights by crawling Slo-Tech, a Slovenian online portal focused on the field of information technologies from a webpage [slo-tech.com](https://slo-tech.com/).

- *Workaway*: Crate a system for answering questions about global volunteering opportunities by crawling the platform [Workaway](https://www.workaway.info/) that connects travellers with hosts worldwide. The goal is to extract publicly available information (e.g., host descriptions, FAQs)

- *Med.Over.Net*: Gather useful advice on a variety of topics by crawling [Med.Over.Net](https://med.over.net/). Med.Over.Net is a forum that contains discussions about health related issues.

- *Slovenian legal domain*: Crawl documents available on [sodnapraksa.si](https://www.sodnapraksa.si/). The website offers a large repository of legal documents structured in HTML format, which should help your chatbot answer legal questions.

- *Other domains*: If you would like to explore a different domain, let us know and we can determine the details.


The crawler needs to be implemented with multiple workers that retrieve different web pages in parallel. The number of workers should be a parameter when starting the crawler. The frontier strategy needs to follow the preferential strategy. In the report explain how your strategy is implemented.

Check and respect the [*robots.txt*](https://en.wikipedia.org/wiki/Robots_exclusion_standard) file for each domain if it exists. Correctly respect the commands *User-agent*, *Allow*, *Disallow*, *Crawl-delay* and *Sitemap*. Make sure to respect *robots.txt* as sites that define special crawling rules often contain [spider traps](https://en.wikipedia.org/wiki/Spider_trap). Also make sure that you follow ethics and do not send request to the same server more often than one request in 5 seconds (not only domain but also IP!).

In a database store canonicalized URLs only!

During crawling you need to detect duplicate web pages. The easiest solution is to check whether a web page with the same page content was already parsed (hint: you can extend the database with a hash, otherwise you need compare exact HTML code). If your crawler gets a URL from a frontier that has already been parsed, this is not treated as a duplicate. In such cases there is no need to re-crawl the page, just add a record into to the table *link* accordingly.  

  * BONUS POINTS: Deduplication using exact match is not efficient as some minor content can be different but two web pages can still be the same. Implement one of the [Locality-sensitive hashing](https://en.wikipedia.org/wiki/Locality-sensitive_hashing) methods to find collisions and then apply Jaccard distance (e.g. using unigrams) to detect a possible duplicate. Also, select parameters for this method. Document your implementation and include an example of duplicate detection in the report. Note, you need to implement the method yourself to get bonus points.
  
When your crawler fetches and renders a web page, do some simple parsing to detect images and next links.

  * When parsing links, include links from *href* attributes and *onclick* Javascript events (e.g. *location.href* or *document.location*). Be careful to correctly extend the relative URLs before adding them to the frontier.
  * Detect images on a web page only based on *img* tag, where the *src* attribute points to an image URL.
  * BONUS POINTS: Implement a strategy for preferential crawling. Detect the relevance of each link to your domain and crawl more relevant links first. This will also help with your second and third tasks as you will have more relavant pages to work with. 
  
Donwload HTML content only (and PDF where required for the domain). List all other content (*.doc*, *.docx*, *.ppt* and *.pptx*) in the *page_data* table - there is no need to populate *data* field (i.e. binary content). In case you put a link into a frontier and identify content as a binary source, you can just set its *page_type* to *BINARY*. The same holds for the image data.

In your crawler implementation you can use libraries that implement headless browsers but not libraries that already implement web crawler functionality. Therefore, some useful libraries that you can use are:

  * [HTML Cleaner](http://htmlcleaner.sourceforge.net/)
  * [HTML Parser](http://htmlparser.sourceforge.net/)
  * [JSoup](https://jsoup.org/)
  * [Jaunt API](https://jaunt-api.com/)
  * [HTTP Client](http://hc.apache.org/)
  * [Selenium](https://www.seleniumhq.org/)
  * [phantomJS](http://phantomjs.org/)
  * [HTMLUnit](http://htmlunit.sourceforge.net/)
  * etc.

On the other hand, you **MUST NOT** use libraries like the following:

  * [Scrapy](https://scrapy.org/)
  * [Apache Nutch](https://nutch.apache.org/)
  * [crawler4j](https://github.com/yasserg/crawler4j)
  * [gecco](https://github.com/xtuhcy/gecco)
  * [Norconex HTTP Collector](https://www.norconex.com/collectors/collector-http/)
  * [webmagic](https://github.com/code4craft/webmagic)
  * [Webmuncher](https://github.com/dadepo/Webmuncher)
  * etc.

To make sure that you correctly gather all the needed content placed into the DOM by Javascript, you should use headless browsers. Googlebot implements this as a two-step process or expects to retrieve dynamically built web page from an HTTP server. A nice session on crawling modern web sites built using JS frameworks, link parsing and image indexing was a part of Google IO 2018 and it is suggested for you to check it:

<center><iframe width="560" height="315" src="https://www.youtube.com/embed/PFwUbgvpdaQ" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></center>

<!--
Useful links
 https://www.elephate.com/blog/javascript-seo-experiment/ 
 https://searchengineland.com/tested-googlebot-crawls-javascript-heres-learned-220157
 https://webmasters.googleblog.com/
-->


Examples of enabling javascript in a web browser or not:

<table class="additionalSources">
<tr>
<td><center><b>Javascript enabled</b></center></td>
<td><center><b>Javascript disabled</b></center></td>
</tr>
<tr>
<td><img src="img/pa1/ess-javascript.png" /></td>
<td><img src="img/pa1/ess-brez.png" /></td>
</tr>
<tr>
<td><img src="img/pa1/arso-javascript.png" /></td>
<td><img src="img/pa1/arso-brez.png" /></td>
</tr>
</table>

In your implementation you must set the *User-Agent* field of your bot to *fri-wier-NAME_OF_YOUR_GROUP*.

### Crawldb design

Below there is a model of a crawldb database that your crawler needs to use. This is just a base model, which you **MUST NOT** change, but you can extend it with additional fields, tables, ... that your crawler might need. You should use PostgreSQL database and create a schema using a [prepared SQL script](data/pa1/crawldb.sql).

<center><iframe width="879" height="814" src="data/pa1/crawldb.html" frameborder="0" scrolling="no"></iframe></center>

Table *site* contains web site specific data. Each site can contain multiple web pages - table *page*. Populate all the fields accordingly when parsing. If a page is of type HTML, its content should be stored as a value within *html_content* attribute, otherwise (if crawler detects a binary file - e.g. .doc), *html_content* is set to *NULL* and a record in the *page_data* table is created. Available page type codes are *HTML*, *BINARY*, *DUPLICATE* and *FRONTIER*. The duplicate page should not have set the *html_content* value and should be linked to a duplicate version of a page. 

You can optionally use table *page* also as a current frontier queue storage. 

## Basic tools

We propose to run the notebook using an Anaconda environment. Prepare the environment as follows:

```bash
# Create and activate environment (activate it before each use)
conda create -n wier python=3.9
conda activate wier

# Install dependencies
conda install selenium psycopg2 nb_conda requests
conda install -c anaconda flask pyopenssl
conda install -c conda-forge flask-httpauth

# Run Jupyter notebook
jupyter notebook 
```

During the lab session we will present basic tools for those who are not well experienced in Web scraping and database access:

* Jupyter notebook tutorial [Web crawling - basic tools](notebooks/Web crawling - basic tools.ipynb) that introduces the basic tools to start working on the assignment.
* A showcase of server ([Remote crawler database (server)](notebooks/Remote crawler database (server).ipynb)) and client ([Remote crawler database (client)](notebooks/Remote crawler database (client).ipynb)) implementation in case you would like to run multiple crawlers (e.g. from each group member homes) and have the same crawler database.
* Jupiter notebook tutorial on [Preferential crawling](notebooks/Preferential crawling.ipynb).
* Jupiter notebook tutorial on [Vector databases](notebooks/introduction_to_vector_databases.ipynb). **This introductory tutorial to vector databases is NOT applicable for PA1**

## What to include in the report

The report should follow the [standard structure](https://fri.uni-lj.si/sl/napotki-za-pisanje-porocila). It should not exceed 2-3 pages. You can include extra pages if you need them for visualisations of the database or large tables.

In the report include the following:

* All the specifics and decisions you make based on the instructions above and describe the implementation of your crawler.
* Document also parameters that are needed for your crawler, specifics, problems that you had during the development and solutions.
* For the sites that are given in the instructions' seed list and also for the whole crawldb together (for both separately) report general statistics of crawldb (number of sites, number of web pages, number of duplicates, number of binary documents by type, number of images, average number of images per web page, ...). 
* Visualize links and include images into the report. If the network is too big, take only a portion of it or high-level representation (e.g. interconnectedness of specific domains). Use visualization libraries such as [D3js](https://d3js.org/), [visjs](http://visjs.org/), [sigmajs](http://sigmajs.org/) or [gephi](https://gephi.org/).
* Describe how you implemented deduplication strategy with partial matching.
* Describe how you implemented a strategy for preferential crawling.
* Describe how you implemented a strategy for preferential crawling.

## What to submit

Only one of the group members should make a submission of the assignment in moodle. The submission should contain only a link to the repository that contains the following which you will use for all the submissions during the course:

 * a file *pa1/db*
 * a file *pa1/report.pdf* - PDF report.
 * a file *pa1/README.md* - Short description of the project and instructions to install, set up and run the crawler.
 * a folder *pa1/crawler* - Implementation of the crawler.

> **NOTE:** The database dump you submit should not contain images or binary data. Filename *db* should be of **Custom** export format that you can export directly using pgAdmin:
>
> <center><img src="img/pa1/Export1.png" /></center>
> <center><img src="img/pa1/Export2.png" /></center>
>
> The exported data file should not be larger than 100MB. If you get a larger file after exporting the database, please upload it to a cloud service like Google drive and include a text file with a link in your repository.
>
> For this assignment it is enough to retrieve data from 5.000 web pages in total (number of records in table *page* of type HTML from your domain). If there is less than 5000 pages available in your domain you should collect all relevant pages and describe in your report how you determined that there are no more useful pages.
 
<!--
## Grading schema

All the submissions will be manually graded by the assistant. Also, plagiarism check will be run across all the submissions. Grading will begin after the last late submission day. The submission time will be selected as the last commit time in the repository. 

The maximum score of 100 (+10 bonus points) will consist of the following:

Points | Item
------ | ----
20 | Database dump check (selected web pages, robots.txt compliance, rough number of web pages match)
30 | Crawler implementation details (multiple workers, BFS frontier, robots.txt and sitemap check, binary files saving, non-crawler libraries usage, javascript rendering)
10 | Duplicate detection (URL canonicalization, content matching)
10 | Duplicate detection (BONUS)
10 | Image and link detection (image tags and saving, HTML and JS)
20 | Retrieved pages analysis (statistics and visualization; justification of retrieved pages wrt. crawler running time)
10 | Submission compliance (report of work and issues description, readme instructions, source code availability - 0 points for the whole project if not available)

Selected groups will need to defend their work during the lab hours. If a group does not agree with their achieved score, it will be able to "negotiate"/defend their programming assignment submission.
-->
