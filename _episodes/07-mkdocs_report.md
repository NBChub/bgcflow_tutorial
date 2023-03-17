---
title: "Exploring BGCFlow result with MKDocs"
teaching: 5
exercises: 0
questions:
- "How do I look at BGCFlow results?"
objectives:
- "Starting an mkdocs server of BGCFlow results"
- "Exploring and using BGCFlow Jupyter Notebooks template"
keypoints:
- "For each BGCFlow projects, the result is structured as an interactive Markdown documentation that can be modified"
- "Reports are made using Jupyter notebooks running on Python or R environments"
---

## Pre-requisite
- Activate the BGCFlow conda environment (see Part 1 - Introduction)
```bash
conda activate bgcflow
```

## Getting a demo report
- Download an example report from [Zenodo](https://zenodo.org/record/7740349#.ZBMDNnbMJaQ)
```bash
wget -O Lactobacillus_delbrueckii_report.zip https://zenodo.org/record/7740349/files/Lactobacillus_delbrueckii_report.zip?download=1
unzip Lactobacillus_delbrueckii_report.zip
```

## Starting BGCFlow mkdocs server
- Move to the report directory and use `bgcflow serve` command to start up a http file server and mkdocs:
```bash
cd Lactobacillus_delbrueckii_report/Lactobacillus_delbrueckii
bgcflow serve --project Lactobacillus_delbrueckii
```
- The report can be accessed in http://localhost:8001/

{% include links.md %}

