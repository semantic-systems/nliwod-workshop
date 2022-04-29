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

If you would like to participate in either of the tasks, please register on the link: [https://forms.gle/pMHfXK3ZaZW4Hoc98](https://forms.gle/pMHfXK3ZaZW4Hoc98)  (one registration per team is enough). 

## Task 1: Multilingual Question Answering over Knowledge Graphs

Given the diversity of languages used on the Web, there is an increasing need to facilitate multilingual access to semantic data. The core task of QALD is thus to retrieve answers from an RDF data repository given an information need expressed in a variety of natural languages.
Linked data, often referring to RDF datasets, can be accessed and read by SPARQL query. However, users without background knowledge in querying language find it hard to retrieve the answer since engines can not understand the natural language questions. Therefore, a key challenge in question answering over data is to transfer human language into SPARQL, which can be formally defined as:

Given RDF datasets (often stored in knowledge graphs) and a question readable by a human, output a correct answer from the knowledge graph, often a SPARQL corresponding to the intention of the question. 

The underlying RDF dataset was a fixed Wikidata dump with meta-data. The participants had to develop their systems using a special version of QALD-9-plus [https://github.com/KGQA/qald_9_plus](https://github.com/KGQA/qald_9_plus) for training and local testing.

This year’s private test set (the one that will be used for building the leaderboard) contained 394 novel, manually created questions to satisfy also data-hungry algorithms. The questions varied in complexity and each was annotated with a manually specified SPARQL query and answers. The evaluation was based on the established QALD-F1-measure.

The train and test data for this challenge was published at [https://github.com/KGQA/QALD_10](https://github.com/KGQA/QALD_10).

The SPARQL queries ran against the knowledge graph from this docker image  [https://hub.docker.com/r/qacompany/hdt-query-service](https://hub.docker.com/r/qacompany/hdt-query-service) which runs currently under this URL [http://sems-vm-1.informatik.uni-hamburg.de:443/api/endpoint/sparql/](http://sems-vm-1.informatik.uni-hamburg.de:443/api/endpoint/sparql/). We provided a fixed endpoint to ensure replicability.
The test and train data followed this QALD_JSON format:
```
{
	"id": "99",
	"question": [{
			"language": "en",
			"string": "What is the time zone of Salt Lake City?"
		},
		{
			"language": "de",
			"string": "In welcher Zeitzone liegt Salt Lake City?"
		},
		{
			"language": "ru",
			"string": "Какой часовой пояс в Солт-Лейк-Сити"
		}
	],
	"query": {
		"sparql": "SELECT DISTINCT ?o1 WHERE { <http://www.wikidata.org/entity/Q23337>  <http://www.wikidata.org/prop/direct/P421>  ?o1 .  }"
	},
	"answers": [{
		"head": {
			"vars": [
				"o1"
			]
		},
		"results": {
			"bindings": [{
					"o1": {
						"type": "uri",
						"value": "http://www.wikidata.org/entity/Q3134980"
					}
				},
				{
					"o1": {
						"type": "uri",
						"value": "http://www.wikidata.org/entity/Q2212"
					}
				}
			]
		}
	}]
}
```

### Training data
The training data was based on the QALD-9-plus [https://github.com/KGQA/qald_9_plus](https://github.com/KGQA/qald_9_plus), a well-known dataset for KGQA. We kept the wikidata part and filtered out empty and timeout answers. Therefore, we had **412 question-answer pairs** left, with questions in 9 different languages: English, German, Russian, French, Armenian, Belarusian, Lithuanian, Bashkir, and Ukrainian. Some of the questions had several alternative writings in particular languages, for example, we presented 1133 Russian, 541 German, and 458 Ukrainian questions based on 412 unique questions. Those questions belonged to general and open-domain factual questions, for instance:
```
en: What is the time zone of Salt Lake City?
de: In welcher Zeitzone liegt Salt Lake City?
ru :Was ist die Zeitzone von Salt Lake City?       
ru: Какой часовой пояс в Солт-Лейк-Сити
ru: В каком часовом поясе расположен Солт-Лейк-Сити?
uk: Який часовий пояс у Солт-Лейк Сіті?
lt: Kokia Solt Leik Sičio laiko zona?
be: Які гадзінны пояс у Солт-Лэйк-Сіці
lt: Kokia laiko juosta yra Solt Leik Sityjes
ba: Ниндей вакыт поясы Солт-Лейк-Ситила
```
### Test Data
The test dataset consisted of **394 similar human-curated questions**. The test set included questions in the following languages: English, German, Chinese and Russian. All questions were real-world questions posted by different users to offer unbiased questions expressing real-world information needs. Note that each question had English, German and Russian forms, apart from 382 questions among 394, all other questions did have Chinese forms. This was due to missing Chinese translations of certain entities in wikidata, for instance, the entity “The Vanishing Half” (Q98476957) in question: “In which year was the author of “The Vanishing Half” born?” did not offer a Chinese form.

### Dataset features
In the data, we strived to include different types of questions, including questions with counts (e.g., How many grand-children did Jacques Cousteau have?), superlatives (e.g., Which poet wrote the most books?), comparatives (e.g., Show me all basketball players that are higher than 2 meters.), and temporal aggregators (e.g., Give me all libraries established before 1400.). Each question was annotated with a manually specified SPARQL query and answers. In the case above, the SPARQL query would be as follows:
```
REFIX wdt: <http://www.wikidata.org/prop/direct/> 
PREFIX wd: <http://www.wikidata.org/entity/> 
SELECT DISTINCT ?uri 
WHERE { ?uri wdt:P106 wd:Q49757 . ?x wdt:P50 ?uri ; wdt:P31 wd:Q571 . }
 GROUP BY ?uri ORDER BY DESC(COUNT(?x)) LIMIT 1"
```
And the answer is [http://www.wikidata.org/entity/Q198644](http://www.wikidata.org/entity/Q198644).

### Evaluation Metric
The 10th QALD challenge offered its evaluation session on an automatic evaluation tool, namely GERBIL QA [https://semantic-web-journal.net/system/files/swj1578.pdf](https://semantic-web-journal.net/system/files/swj1578.pdf), which is open source and available for everyone to re-use. The GERBIL QA platform is accessible online so that participants can simply upload the answers produced by their system or even check their system via a web service [https://gerbil-qa.aksw.org/gerbil/config-qald](https://gerbil-qa.aksw.org/gerbil/config-qald).
Each experiment has a citable, time-stable and archivable URI that is both human- and machine-readable (e.g. [https://gerbil-qa.aksw.org/gerbil/experiment?id=202204260003](https://gerbil-qa.aksw.org/gerbil/experiment?id=202204260003)). The final run URI had to be send via email to the organizers.

Participants were encouraged to provide source code (that can be executed or started as a single system) or/and to show an online demo at the workshop.
The QA systems were evaluated using precision and recall and QALD-F1 (see GERBIL QA paper): 
* recall(q) = number of correct system answers for q/number of gold standard answers for q 
* precision(q) = number of correct system answers for q/number of system answers for q 

The metrics use the following additional semantic information:
* If the golden answerset is empty and the system does respond with an empty answer, we set precision, recall and F-measure to 1.
* If the golden answerset is empty but the system responds with any answerset, we set precision, recall and F-measure to 0.
* If there is a golden answer but the QA system responds with an empty answerset, we assume the system could not respond. Thus we set the precision to 0 and the recall and F-measure to 0.
* In any other case, we calculate the standard precision, recall and F-measure per question.

The evaluation also computed the macro and micro F-measure of a system over all test questions. For micro F-measure, we summed up all true and false positives and negatives and calculated the precision, recall and F-measure at the end. For the macro measures, we calculated precision, recall and F-measure per question and averaged the values at the end. 

⚠️ For the final evaluation, we focused only on the Macro F1 QALD metric. That is, we decided to have a metric more comparable to older QALD challenges and also to follow community requests. 

####  How to participate (Quick Guide):

* <del> Write a registration using the form https://forms.gle/pMHfXK3ZaZW4Hoc98 </del>
* A file-based submission using the QALD-JSON format via a novel, simplified web-interface: [https://gerbil-qa.aksw.org/gerbil/config-qald](https://gerbil-qa.aksw.org/gerbil/config-qald). This is based on [GERBIL QA](https://gerbil-qa.aksw.org/gerbil). You can try it out as often as you like. 
* The endpoint is based on [https://hub.docker.com/r/qacompany/hdt-query-service](https://hub.docker.com/r/qacompany/hdt-query-service) and can be queried under [http://sems-vm-1.informatik.uni-hamburg.de:443/api/endpoint/sparql](http://sems-vm-1.informatik.uni-hamburg.de:443/api/endpoint/sparql)
* The test data can be found under [https://github.com/KGQA/QALD_10](https://github.com/KGQA/QALD_10)
* Send us your final run, i.e. the GERBIL QA URI, via email to [xi.yan@uni-hamburg.de](<mailto:xi.yan@uni-hamburg.de>).
* Participants must submit a 4-page paper describing the approach via the main [easychair instance](https://easychair.org/conferences/?conf=nliwod7) until  28th May 2022, midnight Berlin time zone or their systems will be rejected.
* We will award winning systems at the conference.
* Participants are encouraged to provide source code (that can be executed / started as a single system) or/and show an online demo at the workshop! Please inform Xi Yan. 
* If you have any questions, write an email to [xi.yan@uni-hamburg.de](<mailto:xi.yan@uni-hamburg.de>) and [ricardo.usbeck@uni-hamburg.de](<mailto:ricardo.usbeck@uni-hamburg.de>).

## Task 2: Multilingual Comparative Question Answering Using Knowledge Bases

The new task introduced this year will use a public data source [Wikidata](https://www.wikidata.org/) as a target repository for answering comparative questions. Question answering platforms such as Yahoo! Answers or Quora always contained questions that ask other humans for help when comparing two or more options. Since nowadays more and more people also “talk” to their devices, such comparative questions are also part of the query stream that major search engines receive. Although leading Web search engines index a plethora of information, they do not perform well on cQA information needs. 

The goal of this task is to directly combine the available facts, opinions using structured knowledge bases by analyzing Wikidata and DBpedia as additional sources of (structured) information. The training data includes 100 open-domain factual comparative questions per language in multiple low-resource languages (Amharic, Bengali and Hindi) as well as high-resource languages (Arabic, French, German, and English). The questions originally formulated should be answered using both DBpedia and Wikidata. Therefore, the participants’ systems will have to deal with a different data representation structure. Our main addition here is that the data is composed of 50 questions that are represented in 7 languages, mostly low-resource languages in order to evaluate how generic the approaches are and which knowledge base is more geared towards multilinguality. The remaining 50 queries per language are language and culture specific, to allow the development of methods that are geared towards solvign cQA for low-resource setups. 

A dev data is represented here: https://docs.google.com/spreadsheets/d/15Du-C6VtvK2A48rZEjdV-VdSNkS9vIWwoSLNSzLPWWg/edit?usp=sharing 
In this task, given a natural language query such as: Who is richer, Bill Gates or Jeff Bezos?, the participant should find the entity related to the first object Bill Gate", the entity related to the second Object: "Jeff Bezos", as well as the entity that helps answer the query (in this case NEt Worth). The participants should ideally also output 1 or 2 for indicating if the query is in favor for Object 1 or Object 2, or 0 if they are equal. 


## Timeline:
See [https://www.nliwod.org/important-dates](https://www.nliwod.org/important-dates)

