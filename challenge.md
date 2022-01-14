---
title: Challenge
tagline: 
permalink: /challenge.html
ref: challenge
---

# Challenge

## QALD - 10

This year's *Question Answering over Linked Data* challenge, better known as *QALD*, focuses on **Question Answering over Wikidata**. This will force QA systems to adapt to a new graph as QALD has been DBpedia-centric so far. We will have a novel sub-task on low-resource language QALD to drive accessibility in these languages forward. In particular, QA systems over multilingual KGs widen the access to the Web of Data to lay users. Thus, QA systems increase the accessibility of the Web in general.

We also introduce a **new task on comparative QA**, where the goal is to efficiently answer factual multilingual comparative questions using knowledge basesComparative QA has a wide range of use cases, such as academic search engines or e-commerce.

### Task 1: Multilingual Question Answering over Knowledge Graphs

Given the diversity of languages used on the Web, there is an increasing need to facilitate multilingual access to semantic data. The core task of QALD is thus to retrieve answers from an RDF data repository given an information need expressed in a variety of natural languages.

The underlying RDF dataset is a fixed Wikidata dump with meta-data. The evaluation, i.e. train and test, dataset are based on roughly 450 QALD-9 questions but extended by more than 100 % to satisfy also data-hungry algorithms. The questions vary with respect to their complexity and each is annotated with a manually specified SPARQL query and answers. The evaluation will be based on the established QALD-F1-measure.

### Task 2: Multilingual Comparative Question Answering Using Knowledge Bases

The new task introduced this year will use a public data source [Wikidata](https://www.wikidata.org/) as a target repository for answering comparative questions. Question answering platforms such as Yahoo! Answers or Quora always contained questions that ask other humans for help when comparing two or more options. Since nowadays more and more people also “talk” to their de-vices, such comparative questions are also part of the query stream that major search engines receive. Although leading Web search engines index a plethora of information, they do not perform well on cQA information needs. 

The goal of this task is to directly combine the available facts, opinions using structured knowledge bases by analyzing Wikidata and DBpedia as additional sources of (structured) information. The training data includes 100 open-domain factual comparative questionsin multiple low-resource languages (Amharic, Bengali and Hindi) as well as high-resource languages (Arabic, French, German, and English). The questions originally formulated should be answered using both DBpedia and Wikidata. Therefore, the participants’ systems will have to deal with a different data representation structure. Our main addition here is that the questions are represented in 9 languages, mostly low-resource languages. This task will help to evaluate how generic the approaches are and which knowledge base is more geared towards multilinguality. 
