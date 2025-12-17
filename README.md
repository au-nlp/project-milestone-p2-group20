[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/hgNAtOO3)
# Bridging the Language Gap: A Systematic Approach to Generating Patient-Friendly Clinical Study Descriptions

Idea: Transforming Clinical Trial Descriptions into Patient-Readable Summaries

Dataset: Clinical Trails - https://huggingface.co/datasets/louisbrulenaudet/clinical-trials/viewer/default/train?views%5B%5D=train

## Abstract:
Communicating clinical study information in patient-friendly language is crucial for helping people understand a trial’s purpose and requirements. Originally, resources like ClinicalTrials.gov were intended to be “consumer-friendly” for patients and the public. In practice, however, many trial descriptions remain too technical for non-specialised medical personnel. This project aims to design and test a systematic approach for producing patient-friendly summaries of clinical studies. We will start by identifying key data fields from study records—such as condition, intervention, study type, duration, and participant criteria—and create a step-by-step framework to translate them into plain language. Our goal is to simplify technical information without losing meaning, ensuring patients can clearly understand a study’s purpose and what participation involves. A single command-line pipeline takes a trial’s nct_id and produces three 
artifacts per trial: "Patient Summary" – a short, plain-English overview of the trial (what, for whom, why, how). "Term Explanations" – a glossary of the trial’s technical terms explained in simple language. "Faithfulness & Readability Report" – a compact report showing that essential facts are preserved and that the text is easier to read than the original (and how it compares to the provided brief_summary).
We would like for this project to be of help for people that want to join a clinical trial and need to know which one to choose from. So our goal is to help them better understand and make it sure they find one that fits their needs.

## Contribution / Novelty:
This project introduces a user-centered framework for generating patient-friendly clinical study descriptions to help individuals find clinical trials that best match their needs and circumstances. Unlike existing trial listings that use technical, hard-to-read language, our method focuses on translating complex study data into clear, accessible summaries that patients can easily understand and compare. The novelty lies in combining structured data inputs (such as condition, intervention, and eligibility) with plain-language generation techniques and readability evaluation, making it possible to automatically produce consistent, comprehensible summaries at scale. By improving how study information is presented,
this approach empowers patients to make more informed decisions and enhances accessibility to clinical research opportunities.

## Methodology Overview and Milestones for P2:
### 1. Feature Understanding

The first stage of the methodology focused on understanding the dataset’s structure and identifying which fields are most relevant for the task of generating patient-friendly summaries. The dataset, sourced from the Clinical Trials registry, contains a large variety of metadata fields—ranging from study identifiers and administrative timestamps to long free-text descriptions of the trials. Through a systematic schema inspection and exploration of data samples, we categorized each feature according to its potential contribution to the summarization and simplification objectives.
Features such as the detailed_description, brief_summary, and eligibility_criteria were identified as core text sources, since they contain the essential information patients would need to understand what a clinical trial is about, who it targets, and why it is being conducted. Supplementary fields like keywords and mesh terms were classified as optional—potentially useful for contextual or personalized summaries. Conversely, administrative or highly technical identifiers (e.g. org_study_id_info, and raw date fields) were considered irrelevant for the linguistic analysis and were dropped to streamline processing.
This step culminated in the creation of a feature selection table that clearly outlines for each column whether it should be kept, treated as optional, or excluded, along with the rationale for its categorization. This structured overview ensures transparency and consistency throughout the project.

### 2. Data Quality and Missingness

Once the relevant features were identified, the next step was to assess data quality and completeness. A detailed missingness analysis was conducted across all fields, quantifying the percentage of missing values and visualizing their distribution to identify problematic attributes. Some fields, such as interventions, were found to have substantial missing data, making them unreliable for consistent modeling.
To ensure the dataset remains robust, we defined a filtering rule: trials without meaningful descriptive text—specifically those lacking a detailed_description—were excluded from the working subset. After this filtering, a sufficient number of records remained, confirming that the dataset is large enough to support model training and evaluation. We also enriched rows where maximum age, minimum age and study population was missing.

### 3. Text Analysis and Readability

The third stage aimed to characterize the linguistic properties of the clinical trial texts to better understand the nature of the simplification challenge. For each record, we measured text lengths (in words). We then applied standard readability formulas—such as the Flesch Reading Ease, Flesch-Kincaid Grade Level, and Gunning Fog Index—to estimate how difficult the texts would be for an average reader to comprehend.
The results confirmed that typical detailed_description sections are lengthy, dense, and written at an advanced academic or professional level, often corresponding to university-level readability. These findings quantitatively validate the hypothesis that the language used in clinical trial registries poses a barrier to patients and lay readers.
In addition, we identified and analyzed technical or medical jargon through a heuristic approach that combines word frequency statistics, biomedical suffix detection (e.g., “-itis”, “-oma”, “-genic”), and acronym recognition. A measure of jargon density was introduced to estimate the proportion of complex or specialized terms per document. This provides a foundation for designing simplification strategies—such as substituting jargon with simpler synonyms or adding short explanations to improve accessibility.

### 4. Key Findings and Conclusion

The exploratory analysis led to several important insights that guide the next stages of the project. First, while roughly one-third of clinical trials lack sufficient textual descriptions to be useful, the remaining data form a large, diverse, and high-quality corpus suitable for fine-tuning summarization models. Second, readability metrics demonstrate that the language of clinical trial descriptions is far beyond typical patient reading levels, confirming the practical need for automated simplification.
Third, several metadata features—such as conditions, phases, and study_population—show potential for enhancing summary generation by providing contextual cues. For example, knowing that a study involves pediatric participants or oncology trials could help tailor the level of explanation and tone in the output summaries.
Overall, these analyses establish a clear empirical basis for proceeding to the modeling phase. The dataset is now clean, well-understood, and ready for use in developing and fine-tuning NLP models that can generate simplified, patient-readable summaries of clinical trials while preserving essential medical information and factual accuracy.


## Proposed timeline:

1. Finetune a pretrained summarization model with respect to our chosen features (2.5 weeks)
2. Choose a good model to do the simplification of the summary from the first step (2.5 weeks)
3. Identify jargon words in the trial and generate a glossary of their explanation (1 week)

## Methodology Overview and Milestones for P3:

### 1. Patient-Friendly Summary Generation

The third milestone moves from exploratory analysis to model-based text generation. The first component of this stage focuses on generating patient-friendly summaries of clinical trial descriptions. Using the insights gained from the readability and jargon analysis in P2, we fine-tune a pretrained sequence-to-sequence summarization model on clinical trial text. The model is trained to condense long and technical descriptions into shorter summaries that preserve essential information such as the purpose of the study, the target population, and the main intervention.

The summarization step is applied primarily to the detailed_description field, which contains the most comprehensive information about each trial. The resulting summaries are evaluated using readability metrics introduced earlier in the project, allowing comparison between the original description, the generated summary, and the provided brief_summary. This makes it possible to assess whether the generated output is both shorter and easier to read, while still remaining faithful to the source content.

---

### 2. Simplification and Readability-Oriented Evaluation

Beyond length reduction, an important goal of the summarization component is linguistic simplification. To assess this, multiple readability measures are applied to the generated summaries, including Flesch Reading Ease and Flesch–Kincaid Grade Level. These metrics are used to quantify improvements in accessibility compared to the original clinical trial text.

In addition to standard readability formulas, a simple-English–oriented analysis is conducted by estimating jargon density. This analysis helps identify whether the summarization model successfully reduces the proportion of complex or specialized terms, or whether additional support is needed to help users understand the remaining technical language. The findings from this step motivate the introduction of an explicit glossary component.

---

### 3. Medical Term Identification and Glossary Construction

Even after summarization, clinical trial descriptions often contain unavoidable medical terminology that cannot be safely removed without loss of meaning. To address this, a glossary generation module is introduced to complement the patient-friendly summaries. The goal of this component is to automatically identify medical terms in the text and provide short, accessible explanations for each one.

Medical term extraction is primarily performed using a domain-specific Named Entity Recognition model from scispaCy, which is designed for scientific and biomedical text. Compared to earlier approaches, this model offers broader coverage of clinically relevant concepts, including conditions, procedures, biological processes, and interventions. Abbreviation detection is included to handle common medical acronyms and their expanded forms, which are frequently used in clinical trial documentation.

To improve coverage, a controlled fallback mechanism is added for terms that are not detected as named entities. This fallback combines word rarity statistics with rule-based medical patterns, such as common biomedical prefixes, suffixes, and substrings. A blacklist of known non-medical words is used to reduce noise and prevent common trial-related language from being incorrectly classified as medical terminology.

---

### 4. Definition Retrieval and External Knowledge Sources

For each extracted medical term, a short explanation is retrieved from external knowledge bases. BioPortal is used as the primary source of definitions, with the MeSH ontology selected due to its standard use in biomedical contexts and broad coverage of clinical terminology. These definitions provide concise and medically grounded explanations suitable for clinical concepts.

When no suitable definition is available through BioPortal, Wikipedia is used as a fallback source. Wikipedia summaries are generally more accessible and easier to understand for non-expert users, making them appropriate for patient-facing explanations. To improve efficiency and ensure consistent results, retrieved definitions are cached locally using a lightweight SQLite database, reducing repeated external requests when processing multiple trials.

---
### 6. LLM-Based Generation with Groq and LLaMA

In the final stage of the pipeline, a large language model is used to generate patient-friendly summaries based on the processed clinical trial text. For this purpose, we integrate the Groq API with a LLaMA-based instruction-tuned model. This setup allows for fast inference while maintaining high-quality natural language generation.

The LLM is prompted with structured inputs derived from earlier pipeline stages, including cleaned trial descriptions and relevant contextual information. The model is instructed to produce concise, plain-English summaries that focus on the key aspects of a clinical trial, such as its purpose, target population, and main intervention. Special care is taken in prompt design to encourage faithful rewriting rather than the introduction of new or speculative information.

This LLM-based generation step complements the earlier summarization and glossary components. While traditional summarization models help reduce text length and complexity, the LLaMA-based model further improves fluency and readability, making the final output more suitable for non-expert users. By combining deterministic preprocessing steps with generative modeling, the pipeline balances control, interpretability, and linguistic quality.

The use of Groq enables efficient experimentation and rapid iteration, which is particularly useful in a research and prototyping setting. Overall, this component completes the system by producing coherent, patient-oriented summaries that integrate seamlessly with the glossary and readability evaluation outputs developed in earlier stages.



##  Overall Conclusion

The final system integrates all components developed throughout the project into a single pipeline. Given a clinical trial identifier, the pipeline produces three complementary artifacts: a patient-friendly summary of the trial, a glossary of medical terms with explanations, and a set of readability and faithfulness metrics comparing the generated text to the original description. Together, these outputs aim to improve both accessibility and transparency of clinical trial information.

This milestone completes the project’s objective of bridging the language gap between clinical research documentation and patient understanding. By combining summarization, simplification, and targeted explanation of medical terminology, the system provides a practical and extensible approach for making clinical trial information more accessible to non-expert audiences.

Across all milestones, this project demonstrates that a systematic NLP pipeline can significantly improve the accessibility of clinical trial descriptions without sacrificing essential medical information. The combination of data analysis, model-based summarization, readability evaluation, and glossary generation offers a comprehensive framework for patient-centered clinical text processing. The final system is modular and can be extended in future work to support personalization, multilingual output, or integration with real-world clinical trial platforms.



## Repo Organization: 
To add new implementation please create new branch and do merge request (do not push directly to 
main to prevent conflicts). To create new branch:
- checkout to main: git checkout main
- create new branch: git checkout -b branch-name


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
