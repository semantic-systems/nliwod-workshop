---
title: QALD Challenge
tagline: 
permalink: /challenge.html
ref: challenge
---

# 10th Question Answering over Linked Data (QALD) Challenge @ ESWC 2022

This year's Question Answering over Linked Data challenge has **2 tasks** and focuses on **Question Answering over Wikidata**. This will force QA systems to adapt to a new graph as QALD has been DBpedia-centric so far. 

For QALD-10 task 1, we will have a novel sub-task on **multilingual QALD (Russian, Chinese, German, English) over Wikidata** to drive accessibility in these languages forward. In particular, QA systems over multilingual KGs widen the access to the Web of Data to lay users. Thus, QA systems increase the accessibility of the Web in general.

For QALD-10 task 2, we introduce a **new task on comparative QA**, where the goal is to efficiently answer factual multilingual comparative questions using knowledge bases. Comparative QA has a wide range of use cases, such as academic search engines or e-commerce.

If you would like to participate in either of the tasks, please register on the link: https://forms.gle/pMHfXK3ZaZW4Hoc98 (one registration per team is enough). 

## Task 1: Multilingual Question Answering over Knowledge Graphs

Given the diversity of languages used on the Web, there is an increasing need to facilitate multilingual access to semantic data. The core task of QALD is thus to retrieve answers from an RDF data repository given an information need expressed in a variety of natural languages.

The underlying RDF dataset is a fixed Wikidata dump with meta-data (TBA). The articipants will have to develop their systems using 558 [QALD-9-plus](https://github.com/Perevalov/qald_9_plus) questions for training and local testing.

This years private test set (the one that will be used for the building the leaderboard) will contain more than 500 novel, manually created questions to satisfy also data-hungry algorithms. The questions vary with respect to their complexity and each is annotated with a manually specified SPARQL query and answers. The evaluation will be based on the established QALD-F1-measure.

### How to participate:
* Write a registration using the form https://forms.gle/pMHfXK3ZaZW4Hoc98 
* A file-based submission via a novel, simplified web-interface (TBA) for [GERBIL QA](https://gerbil-qa.aksw.org/gerbil) -> send us your final run via email to (TBA)
* Participants must submit a 4-page paper describing the approach via the main [easychair instance](https://easychair.org/conferences/?conf=nliwod7) until the conference 

* Participants are encouraged to provide source code (that can be executed / started as a single system) or/and an online demo


## Task 2: Multilingual Comparative Question Answering Using Knowledge Bases

The new task introduced this year will use a public data source [Wikidata](https://www.wikidata.org/) as a target repository for answering comparative questions. Question answering platforms such as Yahoo! Answers or Quora always contained questions that ask other humans for help when comparing two or more options. Since nowadays more and more people also “talk” to their devices, such comparative questions are also part of the query stream that major search engines receive. Although leading Web search engines index a plethora of information, they do not perform well on cQA information needs. 

The goal of this task is to directly combine the available facts, opinions using structured knowledge bases by analyzing Wikidata and DBpedia as additional sources of (structured) information. The training data includes 100 open-domain factual comparative questions per language in multiple low-resource languages (Amharic, Bengali and Hindi) as well as high-resource languages (Arabic, French, German, and English). The questions originally formulated should be answered using both DBpedia and Wikidata. Therefore, the participants’ systems will have to deal with a different data representation structure. Our main addition here is that the data is composed of 50 questions that are represented in 7 languages, mostly low-resource languages in order to evaluate how generic the approaches are and which knowledge base is more geared towards multilinguality. The remaining 50 queries per language are language and culture specific, to allow the development of methods that are geared towards solvign cQA for low-resource setups. 

## Timeline:
* Release of initial data – March 1st, 2022 (see [QALD-9-plus](https://github.com/Perevalov/qald_9_plus))
* Deadline for registration April 19th, 2022 
* System submission system opens April 19th, 2022
* System submission system closes May 15th, 2022
* Challenge paper submission deadline - May 28th, 2022
* Workshop at ESWC – May 29th, 2022 (09:00AM-12:30PM) = Presentation of Results
