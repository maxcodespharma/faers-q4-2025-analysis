FAERS Q4 2025 Adverse Event Analysis


Disclaimer: 
This README was created using Claude and the entire project was suggested by Claude as a good 
way for me to learn SQL, PANDAS, and Jupyter Notebooks with minimal focus on Matplotlib visualization toward the end. The actual analysis within the markdown cells is primarily my own commentary after data analysis and consulting with Claude. This is a practice exercise designed to showcase my self-taught ability to perform data analysis using advanced tools and programming despite being a pre-Pharmacy student. 


Project Overview
This project analyzes publicly available FDA Adverse Event Reporting System (FAERS) data from Q4 2025 (October–December). FAERS is an FDA database containing post-market drug safety reports submitted by patients, healthcare providers, and manufacturers. The goal of this analysis is to identify patterns in serious adverse outcomes — specifically deaths and hospitalizations — across drug classes, patient demographics, and reporting sources using a combined SQL and Python workflow.
Data Source

FDA FAERS Q4 2025 ASCII files
Download: https://www.fda.gov/drugs/questions-and-answers-fdas-adverse-event-reporting-system-faers/fda-adverse-event-reporting-system-faers-latest-quarterly-data-files
7 tables, approximately 385,000 case reports
Tables: DEMO, DRUG, REAC, OUTC, INDI, THER, RPSR

Tools Used

Python, pandas, sqlite3
SQLite via DB Browser for SQLite
Matplotlib
Jupyter Notebook
Claude LLM 

Workflow
Raw FAERS ASCII files were imported into a local SQLite database using DB Browser. Python was connected to the database via sqlite3, SQL queries were written directly inside Jupyter using pd.read_sql(), and results were returned as pandas DataFrames for analysis and visualization. This mirrors the standard RWE industry workflow where data lives in relational databases and analysts query and analyze programmatically.
Key Findings
1. Death and hospitalization have distinct drug profiles
Primary suspect drugs in death cases skew heavily toward oncology — checkpoint inhibitors and targeted cancer therapies. Hospitalization cases are dominated by mainstream chronic disease drugs including biologics for autoimmune conditions and GLP-1 receptor agonists for diabetes and weight loss.
2. Off-label use is the dominant reaction signal across both serious outcome categories
Off-label use was the single highest reported reaction term in both death and hospitalization cases, excluding the outcome term itself. This consistent cross-cutting signal suggests patients on drugs outside their approved indications are disproportionately represented in serious adverse outcomes — a meaningful pharmacovigilance finding.
3. Physician-filtered data reveals a cleaner, more specific signal
Filtering death cases to physician-reported primary suspect drugs dramatically changes the drug list and reduces noise. The unfiltered list reflects prescribing volume across the general population. The physician-filtered list reflects deliberate clinical causality judgment — and tells a far more specific oncology story.
4. Elderly patients are disproportionately represented in death outcomes
Elderly patients appear at more than twice the rate of middle-aged patients in death cases, consistent with known patterns of polypharmacy, immunosenescence, and reduced physiologic reserve in older populations.
5. Women report more adverse events overall but men die at higher rates
Women comprise approximately 60% of known reporters in FAERS, consistent with higher healthcare utilization rates among women. However, men outnumber women in death cases — a pattern consistent with broader epidemiological mortality data.
Limitations

FAERS contains a combination of mandatory reports (manufacturers) and voluntary reports (patients, providers). Voluntary reports are not representative of all adverse events occurring in the population.
No denominator is available. Report counts cannot be interpreted as incidence rates without knowing total drug exposure in the population.
Duplicate reports exist. A single adverse event may be submitted independently by the patient, their physician, and the drug manufacturer, inflating raw counts.

How to Replicate
The raw SQLite database is not included in this repository due to file size. To replicate this analysis, download the FAERS Q4 2025 ASCII files from the FDA link above, import each .txt file into a SQLite database using DB Browser for SQLite with a $ delimiter, and connect to the database using the path specified in the notebook.
