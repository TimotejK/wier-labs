# Programming assignment 3 {#PA3}

<img src="img/book/spider-01.png" />

## Introduction 


In previous assignments, you developed a web crawler and gained insights into extracting and processing content from web pages. For this final assignment, you will shift your focus to Retrieval-Augmented Generation (RAG), an innovative approach that integrates information retrieval with language modeling to effectively answer queries.

Your task is to implement a RAG system capable of addressing questions in two distinct modes:

1. **With Context** – Generate answers to queries based on relevant documents retrieved from the tables you established in the second assignment.
2. **Without Context** – Generate answers directly using the large language model, independent of external content.

This assignment will enhance your understanding of the trade-offs involved in both modes of operation within your RAG system.


## Instructions

This assignment is an extension of previous work in document processing and indexing, with a focus on incorporating vector-based similarity searches in practical application, i.e., a RAG system. One of your tasks is also to assess the RAG system performance, investigating how the relevance of documents influences the quality of generated responses. They will also reflect on the trade-offs between semantic retrieval and purely generative responses. The final system illustrates the fundamental principles behind cutting-edge question-answering pipelines, balancing memory (retrieval) and reasoning (generation).

### Provided Material

[The compressed file](data/pa3/PA3 API starter.zip) contains:

* A basic FastAPI API server (main.py)

* A simple HTML/CSS/JS UI (templates/index.html)

* Example request logic in JavaScript

* Minimal placeholder logic for the backend

You’ll build on this foundation to add your RAG functionality. You can use [this notebook](https://colab.research.google.com/drive/1K8jwIkxRrhG6E2c5YD0Es3C6pqwLxFUG) as a reference.


### Instructions

First, setup the environment by unzipping the starter code and installing the neccessary dependencies. You may need to install additional libraries depending on your implementation.

To implement the backend of a RAG system, you begin by setting up a local API using a lightweight framework like FastAPI. The backend serves as the core controller that receives user queries from the front-end interface and processes them based on the selected response mode. 
As the source of context, you should use the information retreival system you desighed in PA2. When the user submits a query, search the database (from PA2) for the most relevant chunk of text based on vector embeddings. Use this chunk (or multiple chunks) as the context for your language model.

Next, you integrate a large language model (LLM) by defining a function that queries the LLM. Depending on the mode selected by the user, the system either uses the retrieved context to build a prompt (in "With Context" mode) or sends the question directly to the LLM (in "Without Context" mode). In the contextual case, a new prompt is constructed by concatenating the relevant text chunks with the user query, encouraging the LLM to generate an informed answer. Your API should implement a route /question, which accepts a POST request containing the mode and the question (see example impelemtation provided above).

Finally, the backend returns the LLM’s response to the frontend as a JSON object, where it is displayed to the user. This modular approach makes the system easy to maintain and extend. For example, you could plug in different embedding models or swap out the LLM provider. The backend cleanly separates the logic for query embedding, retrieval, and generation, allowing for detailed evaluation of how each part contributes to overall system performance.

### Evaluation

Provide qualitative or quantitative evidence of retrieval accuracy and effectiveness for your RAG system. Define at least six queries that produce good retrieval accuracy and three queries that produce bad retrieval accuracy. In addition, compare answers yielded by the RAG system for the two working modes, i.e., with context and without context, and study the responses.

## What to include in the report

Your report should clearly document your design decisions, implementation approach, and evaluation. The report should follow the [standard structure](https://fri.uni-lj.si/sl/napotki-za-pisanje-porocila). Please include the following sections:

### Implementation Summary

Describe all key implementation decisions you made based on the instructions and starter code. Include:

(A) The embedding model and LLM you used.

(B) How you structured and stored your documents.

(C) How you integrated retrieval and generation logic.

(D) Any additional tools or libraries used.

### System Evaluation Criteria
Explain the criteria you used to assess the following components of your RAG system:

(A) Data Processing
Describe how you evaluated the quality of your data preparation pipeline, including how documents were chunked (e.g., by sentence, paragraph, token limits). Discuss any trade-offs you encountered, such as chunk size vs. retrieval granularity.

(B) Data Retrieval.
Your system from PA2 utilizes direct similarity-based retrieval. Describe how many top-k documents were retrieved per query. How did you judge whether the retrieved chunks were relevant or informative? Explain the impact of retrieval quality on the RAG system.

(C) Evaluation
Provide qualitative or quantitative evidence of retrieval accuracy and effectiveness for your RAG system. Prepare a table that includes queries as well as comparisons of answers yielded by the RAG system for the two working modes, i.e., with context and without context, and your comments. Specifically, discuss the potential benefits and limitations.


## What to submit

Push your work into the same repository as you used for the first assignment. Structure of the repository must comply with the following structure:

 * a file */PA3/report.pdf* - PDF report.
 * a file */PA3/README.md* - Short description of the project and instructions on how to set-up and use your RAG system.
 * a folder */PA3/rag/* - Implementation of the RAG system. Also, all the dependencies and instructions to run this part must be clearly described in README.md.
 
<!--
## Grading schema

All the submissions will be manually graded by the assistants. Also plagiarism check will be run across all the submissions. Grading will begin after the last late submission day. The submission time will be selected as the last commit time in the repository. 

The maximum score of 100 will roughly consist of the following:

Points | Item
------ | ----
30 | Inverted database check
40 | Data retrieval and ranking (inverted index) results and implementation
20 | Data retrieval and ranking (sequential file reading) results and implementation
10 | Submission repository compliance


Selected groups will need to defend their work during the lab hours. If a group does not agree with their achieved score, it will be able to "negotiate"/defend their programming assignment submission.
-->
