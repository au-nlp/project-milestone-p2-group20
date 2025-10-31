[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/hgNAtOO3)
# Bridging the Language Gap: A Systematic Approach to Generating Patient-Friendly Clinical Study Descriptions

## Repo Organization: 
To add new implementation please create new branch and do merge request (do not push directly to 
main to prevent conflicts). To create new branch:
- checkout to main: git checkout main
- create new branch: git checkout -b branch-name

[Idea, Abstract,Methods other Documentation(P1, P2 and P3) below]

Idea: Transforming Clinical Trial Descriptions into Patient-Readable Summaries

Dataset: Clinical Trails - https://huggingface.co/datasets/louisbrulenaudet/clinical-trials/viewer/default/train?views%5B%5D=train

## Abstract:
Communicating clinical study information in patient-friendly language is crucial for helping people understand a trial’s purpose and requirements. Originally, resources like ClinicalTrials.gov were intended to be “consumer-friendly” for patients and the public. In practice, however, many trial descriptions remain too technical for non-specialised medical personnel. This project aims to design and test a systematic approach for producing patient-friendly summaries of clinical studies. We will start by identifying key data fields from study records—such as condition, intervention, study type, duration, and participant criteria—and create a step-by-step framework to translate them into plain language. Our goal is to simplify technical information without losing meaning, ensuring patients can clearly understand a study’s purpose and what participation involves. A single command-line pipeline takes a trial’s nct_id and produces three 
artifacts per trial: "Patient Summary" – a short, plain-English overview of the trial (what, for whom, why, how). "Term Explanations" – a glossary of the trial’s technical terms explained in simple language. "Faithfulness & Readability Report" – a compact report showing that essential facts are preserved and that the text is easier to read than the original (and how it compares to the provided brief_summary).
We would like for this project to be of help for people that want to join a clinical trial and need to know which one to choose from. So our goal is to help them better understand and make it sure they find one that fits their needs.

## Contribution / Novelty:
This project introduces a user-centered framework for generating patient-friendly clinical study descriptions to help individuals find clinical trials that best match their needs and circumstances. Unlike existing trial listings that use technical, hard-to-read language, our method focuses on translating complex study data into clear, accessible summaries that patients can easily understand and compare. The novelty lies in combining structured data inputs (such as condition, intervention, and eligibility) with plain-language generation techniques and readability evaluation, making it possible to automatically produce consistent, comprehensible summaries at scale. By improving how study information is presented,
this approach empowers patients to make more informed decisions and enhances accessibility to clinical research opportunities.

## Methods for Phase 2

This project follows a structured, multi-phase methodology designed to analyze, clean, and prepare clinical trial text data for generating patient-friendly study descriptions. In Phase 1 (Data Understanding & Feasibility), we load the dataset from Hugging Face, inspect its structure, assess completeness, and identify key fields such as condition, intervention, and detailed descriptions. We evaluate missing values, summarize metadata distributions (study type, phase, status, enrollment), and document filtering decisions to ensure a representative, high-quality dataset. Phase 2 (Text Exploration) focuses on understanding textual complexity through word and sentence length distributions, readability metrics, vocabulary analysis, and jargon density. We visualize linguistic patterns, such as part-of-speech distributions and frequent medical terms, to quantify how technical or specialized the text is. Phase 3 (Text Preprocessing) standardizes and cleans the text through lowercasing, punctuation and HTML removal, sentence segmentation, tokenization, stopword removal, and lemmatization, ensuring the corpus is ready for modeling. Rare word handling and storage of cleaned text in structured columns provide a reusable data pipeline. Phase 4 (Descriptive Summaries & Visualization) compiles readability, vocabulary, and complexity metrics into comparative dashboards and visualizations, highlighting key trends across study types and conditions. Finally, Phase 5 (Synthesis & Next Steps) summarizes insights—confirming that clinical trial texts are lengthy and highly technical—and outlines the next stage of the project, which involves applying NLP methods for text simplification and summarization. Together, these phases ensure a transparent, reproducible process from raw data inspection to a ready-to-model dataset aimed at producing clear, accessible clinical trial summaries for patients.


## Methods for Phase 3
Building on these preparation phases, the next stage implements a patient-summary generation pipeline that transforms the cleaned trial data into lay-friendly narratives through a sequence of NLP-driven modules. The process begins with data ingestion, where key fields such as nct_id, brief_title, study_type, conditions, and detailed_description are retrieved for processing. Next, a jargon detection module uses tokenization and medical term recognition via resources like UMLS, MeSH, and spaCy’s named entity recognition to identify complex terms, acronyms, and domain-specific language. Each identified term is categorized (e.g., medication, biomarker, Latinism) and scored for complexity based on word frequency and external difficulty indices. In the simplification stage, each technical term is rewritten or annotated with plain-English definitions using a combination of rule-based mappings, dictionary lookups, and LLM-assisted paraphrasing. These simplified terms feed into a summary generation module, which constructs a concise, coherent narrative covering the study’s purpose, population, intervention, design, and outcomes. The model integrates template-based sentence framing with transformer-based summarization (e.g., BART or T5) to maintain factual accuracy while reducing linguistic complexity. The generated summary is annotated with inline glossary explanations and then passed through a faithfulness validation step, where semantic similarity scoring (e.g., Sentence-BERT embeddings) checks alignment between the simplified summary and original content to ensure key study facts are preserved. Finally, the pipeline performs readability evaluation (Flesch–Kincaid, Gunning Fog, and jargon density metrics) and ethical filtering to remove prescriptive or misleading language before exporting structured outputs—including a Markdown summary, a glossary JSON, and a report JSON containing readability and alignment scores. This end-to-end process produces traceable, patient-oriented summaries that preserve medical accuracy while improving accessibility and comprehension.



P1: Suggestions(from TA)
__________________________________________

You could consider building a simple LLM pipeline to identify which words are complex and then try to let llm self-explain them in simpler English.
Reference : https://aclanthology.org/P11-2117.pdf. 
Overall, I don’t think you need to cover too many aspects; instead, you could identify what you believe are the most critical challenges in this task and explore them in depth.


P2 : Doubts and Clarifications/Suggestions
____________________________________________
 
1) How to use other features than “detailed description” for summarization / this field is enough? 
It’s up to us, better we try different ways and find out (consider brief summary filed and see). But it is ok even if we use one column until and unless we cover all the steps in the pipeline and have good accuracy.
Discuss(for us) : The use of a brief summary field.
2) Currently thinking , we will do the summarization of the column first (which will still contain technical/complex words) and then replace those with human friendly words (like a summarization and then a simplification)  - or do it the other way around?  
It is better to do the summary first and then replace/simplify.
Summary metric(eg :simple english metric)  - pick some examples from this and compare/validate
3) Is the scope we are proposing enough to meet the mark? Yes
4) For P2, what is the expected implementation scope/ how far we should implement? Should we do things like tokenisation and stop word removal or just understand the data? - No specific expectation, try to add findings (try many ways and explain why we choose this way/hypothesis - arguments to validate our methods kind of)
5) Structure of the whole final product / Is there any expectation on this ? Not really, just notebook +  report(P3) and notebook for P2 
6) Evaluation/score/survey of the model/system - Summary metric(eg :simple english metric). Also, will have time to discuss this later(mostly for P3)
