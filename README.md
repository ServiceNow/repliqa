# RepLiQA - Repository of Likely Question-Answer for benchmarking

## Dataset Summary
RepLiQA is an evaluation dataset that contains Context-Question-Answer triplets, where contexts are non-factual but natural-looking documents about made up entities such as people or places that do not exist in reality. RepLiQA is human-created, and designed to test for the ability of Large Language Models (LLMs) to find and use contextual information in provided documents. Unlike existing Question-Answering datasets, the non-factuality of RepLiQA makes it so that the performance of models is not confounded by the ability of LLMs to memorize facts from their training data: one can test with more confidence the ability of a model to leverage the provided context.

Documents in RepLiQA comprise 17 topics or document categories: `Company Policies`; `Cybersecurity News`; `Local Technology and Innovation`; `Local Environmental Issues`; `Regional Folklore and Myths`; `Local Politics and Governance`; `News Stories`; `Local Economy and Market`; `Local Education Systems`; `Local Arts and Culture`; `Local News`; `Small and Medium Enterprises`; `Incident Report`; `Regional Cuisine and Recipes`; `Neighborhood Stories`; `Local Sports and Activities`; and `Local Health and Wellness`. Non-factual documents are annotated in one of these topics covering fantasy/made-up entities that are not documented anywhere. Each document is accompanied by 5 question-answer pairs.

Moreover, annotations in RepLiQA are such that approximately 20% of the questions cannot be answered from the provided documents, and models are expected to indicate that an answer cannot be obtained whenever that is the case.

## Supported Tasks
RepLiQA is designed to support at least the following tasks:
- Question-Answering
- Topic Retrieval
- Selective Question-Answering (i.e., test for the ability to refuse to answer questions that cannot be answered from the provided context.)

## Data Fields
- `document_id` (string): Uniquely identifies the **document** to which this sample pertains. Note that there are 5 questions per document, so **each `document_id` appears 5 times in the dataset**.
- `document_topic` (string): One of the 17 document topic/categories listed above.
- `document_path` (string): Relative path within this repository to the original PDF document.
- `document_extracted` (string): Text automatically extracted from the original PDF document.
- `question_id` (string): Uniquely identifies each **document-question combination**, and thus each data sample.
- `question` (string): Question that may or may not be answerable using the associated document.
- `answer` (string): Answer to the question when it can be answered using the document, and the string `UNANSWERABLE` otherwise.
- `long_answer` (string): The annotator who produced the `answer` was asked to copy-paste here the paragraph from the document in which they found the `answer`. This `long_answer` is provided as-is, with no check whether it is actually contained within the document. The `long_answer` is `NA` iff the `answer` is `UNANSWERABLE`.


## Summary of data annotation pipeline
- Topic selection.
- Produce reference documents of approximately 1000 words. When creating fictitious characters, places and organizations, annotators used random name generators and anonymization tools to cross-reference them against existing entities, in order to avoid unintentional references.
- Automatic summarizations of reference documents.
- Annotation of 5 specific and direct questions, based solely on the summary.
- Annotation of the associated answers, based on the full document and questions.
- Quality control: all samples were vetted, with a reported initial rejection rate of around 5-10%.
- Data splitting and further cleaning up to remove left out noisy content.


## Known issues
- Various irregularities have been observed, including code-like chunks (e.g., within angle `<>` or square `[]` brackets).
- Scoring RepLiQA documents with [Fast-DetectGPT](https://github.com/baoguangsheng/fast-detect-gpt) results in score that are notably different from those of [FineWeb](https://huggingface.co/datasets/HuggingFaceFW/fineweb).

(Details coming soon.)


## Update plan:
RepLiQA consists of five splits, to be released gradually over a year:
- `repliqa_0` June 12th, 2024.
- `repliqa_1` December 9th, 2024.
- `repliqa_2` February 10th, 2025.
- `repliqa_3` April 14th, 2025.
- `repliqa_4` June 9th, 2025.

By construction, these splits should all be identically distributed. This gradual release schedule is meant to avoid leaking novel data partitions and ensure models are not trained in its contexts when evaluated.

Comments and requests can addressed in the [discussions](https://huggingface.co/datasets/ServiceNow/repliqa/discussions).

## How to benchmark with RepLiQA
At term, five RepLiQA splits will be released. Because evaluating LLMs can be costly, some authors may prefer to evaluate on a subset of the released splits. We recommend the following choices of such subsets, and :
- (**latest**) If you evaluate on only one split, use the latest released split (**preferred evaluation setting**);
- (**zeroth+latest**) If you evaluate on two splits, use `repliqa_0` and the latest released split;
- (**all**) If you evaluate more than two splits, use all released splits.

In general, please clearly specify which RepLiQA splits were used, and report results for each split separately.

## See also
- [https://github.com/ServiceNow/repliqa](https://github.com/ServiceNow/repliqa)

(More coming soon.)


## Licensing Information

### [RepLiQA Dataset](https://huggingface.co/datasets/ServiceNow/repliqa)
Copyright © ServiceNow 2023-2024  
Licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)  

### [Associated Code](https://github.com/ServiceNow/repliqa)
Copyright © ServiceNow 2024  
Licensed under [MIT License](https://github.com/ServiceNow/repliqa/blob/main/LICENSE)
