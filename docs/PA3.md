# Programming assignment 3 {#PA3}

<img src="img/book/spider-01.png" />

## Introduction 

In the first assignment you created a Web crawler to download Web content from the Internet. Then in the second assignment, you learned how to extract specific content from Web pages or how to identify data blocks of interest. In this last assignment you will build a simple index and implement querying against it.

## Instructions 

[A compressed file](data/pa3/PA3-data.zip) contains 1416 crawled Web pages from four different domains. Your software will need to extract textual context from the provided HTML files, perform preprocessing and store data into index. After that the built index can be used for querying. Your implementation must consist of the following parts:

1. Data processing and indexing
2. Data retrieval

### Data processing and indexing

Prior to indexing we need to retrieve textual data from web pages. To get whole textual data, you can call appropriate *text()* function from your favourite HTML parsing library. The text must be then preprocesed using tokenization (*see word_tokenize function within the [nltk.tokenize package](https://www.nltk.org/api/nltk.tokenize.html)*), stopword removal (*use [these stopwords or extend them](data/pa3/stopwords.py)*) and normalization into lowercase letters. If you apply additional preprocessing steps, document them in the report. *Note that the same preprocessing function needs to be applied to a given query by a user.*

Instead of creating your own data structure for inverted index, you will simulate it using the SQLite database with the following schema:


```sql
CREATE TABLE IndexWord (
  word TEXT PRIMARY KEY
);

CREATE TABLE Posting (
  word TEXT NOT NULL,
  documentName TEXT NOT NULL,
  frequency INTEGER NOT NULL,
  indexes TEXT NOT NULL,
  PRIMARY KEY(word, documentName),
  FOREIGN KEY (word) REFERENCES IndexWord(word)
);
```

The table *IndexWord* must contain a list of all words that are indexed by your system. Related table *Posting* contains frequencies and offset indexes for a word in a specific document. Let's say that a word *davek* appears three times at indexes 2, 34 and 894 in a document *evem.gov.si/evem.gov.si.4.html*. A record in a *Posting* table would look like the following: ('davek', 'evem.gov.si/evem.gov.si.4.html', 3, '2,34,894').

### Data retrieval

The data retrieval part of your software should use the index built in the part above and return search results for a given query.

For a multi-word query, the algorithm must merge the results by document and return results descending by the sum of frequencies. The search should just check for indexed words that exactly match words from a query.

The output of search results must contain also snippets around the indexed words (neighbourhood of three words wrapped with three dots) as in the following example (*/implementation-indexing/run-sqlite-search.py "Sistem SPOT"*):


```bash
Results for a query: "Sistem SPOT"

  Results found in 4ms.

  Frequencies Document                                  Snippet
  ----------- ----------------------------------------- -----------------------------------------------------------
  4           evem.gov.si/evem.gov.si.666.html          Sistem SPOT je eden boljši ... dosedanje delovanje SPOT ni zadovoljivo za ... je bila zaključena. Sistem ni deloval dobro ...
  1           e-uprava.gov.si/e-uprava.gov.si.42.html   ... ministrstvo je nadgradilo sistem za učinkovitejšo uporabo.
```

In the report include the results for the following queries:

* "predelovalne dejavnosti"
* "trgovina"
* "social services"
* Define additional three queries consisting of 1-5 words that have at least one result.

Searching using the SQLite database should be quite fast (in our toy scenario). 

To get a feeling of a speed-up in search using an inverted index, implement searching without the SQLite database. Instead of using the database, your algorithm should sequentially open each file, process it and merge the results. The parsing and preprocessing part must be the same as in searching with the SQLite database. Use the same search queries with this naive approach and compare the query execution times to inverted index implementation */implementation-indexing/run-basic-search.py SEARCH_PARAM*.

During the lab session we will present how to use SQLite database in Python for those who have not yet used it in practice:

* Jupyter notebook tutorial [SQLite database](notebooks/SQLite database.zip) that introduces the basic usage of SQLite to start working on the assignment.

## What to include in the report

The report should follow the [standard structure](https://fri.uni-lj.si/sl/napotki-za-pisanje-porocila).

In the report include the following:

* All the specifics and decisions you made based on the instructions above and the description of the implementation. Separately describe (A) data processing with indexing, (B) data retrieval with inverted index and (C) data retrieval without inverted index.
* Describe the database (number of indexed words, words and documents with the highest frequencies, ...).
* Describe and comment on the results of the test queries.

## What to submit

Push your work into the same repository as you used for the first assignment. Structure of the repository must comply with the following structure:


 * a file */implementation-indexing/inverted-index.db* - SQLite database file, generated by your indexing part.
 * a file */report-indexing.pdf* - PDF report.
 * a file *README.md* - Short description of the project and instructions to install, set up and run the indexing and data retrieval (keep instructions for previous assignments).
 * a folder */implementation-indexing* - Implementation of the methods along with run-sqlite-search.py and run-basic-search.py. CAUTION: Use relative paths so that anyone can run your scripts. Also, all the dependencies and instructions to run this part must be clearly described in README.md.
 
## Grading schema

All the submissions will be manually graded by the assistant. Also plagiarism check will be run across all the submissions. Grading will begin after the last late submission day. The submission time will be selected as the last commit time in the repository. 

The maximum score of 100 will roughly consist of the following:

Points | Item
------ | ----
30 | Inverted database check
40 | Data retrieval and ranking (inverted index) results and implementation
20 | Data retrieval and ranking (sequential file reading) results and implementation
10 | Submission repository compliance


Selected groups will need to defend their work during the lab hours. If a group does not agree with their achieved score, it will be able to "negotiate"/defend their programming assignment submission.

