[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/hgNAtOO3)

Repo Organization: to add new implementation please create new branch and do merge request (do not push directly to 
main to prevent conflicts). To create new branch:
checkout to main: git checkout main
create new branch: git checkout -b branch-name


[Idea and Documentation(P1, P2 and P3) below]

Idea: Transforming Clinical Trial Descriptions into Patient-Readable Summaries

Dataset: Clinical Trails - https://huggingface.co/datasets/louisbrulenaudet/clinical-trials/viewer/default/train?views%5B%5D=train

Clinical trial registries contain valuable information, but descriptions are often technical, full of jargon, and hard for patients to understand. This creates a barrier for those considering participation.
This project aims to use NLP to convert complex trial descriptions into patient-friendly summaries, focusing on the "detailed description" field. The approach involves simplification (removing jargon, breaking down complex sentences) and summarization (condensing long text into clear explanations). The goal is to preserve essential trial information - what is being tested, for whom, and why - while improving readability. Results can be compared to the existing brief summary to ensure accuracy and reduced medical terminology.

Suggestion from P1(from TA) : You could consider building a simple LLM pipeline to identify which words are complex and then try to let llm self-explain them in simpler English.
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
