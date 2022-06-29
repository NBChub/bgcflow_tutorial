---
title: "BGCflow data structure"
teaching: 0
exercises: 5
questions:
- "Where can I find the analysis result of my run?"
objectives:
- "Finding relevant BGCflow analysis result"
keypoints:
- "BGCflow adopt the cookiecutter data science directory structure"
- "Output files can be found in the `data` directory, and are splitted into three different stages"
- "The `processed` directory contained most of the output required for downstream analysis"
---
## Exploring the output of BGCflow
In this workshop, we have finished running all analysis for our s_venezuelae project. You can find the result in the VM at: `/datadrive/bgcflow/data`. 
```bash
tree -L 2 /datadrive/bgcflow/data/
```

You can also generate a symlink to that directory so you can explore it using VS Code:
```bash
tree -L 3 /datadrive/bgcflow/data/
```

BGCflow adopt the cookiecutter data science directory structure. Output files can be found in the `data` directory, and are splitted into three different stages:
- The `processed` directory contained most of the output required for downstream analysis
- The `interim` directory contained a direct output from each rules that are not fined tuned for downstream analysis
- The `raw` directory contained user provided input files

Give yourself time to look through the different output directories.

## Which files are important?
It depends. Different research questions will require different analysis, and therefore different files are required for downstream analysis.
In the Natural Products Genome Mining group, we aim to aid students and researchers by giving an example of Jupyter notebooks to process each output types.
It is a work in progress and we are open to anyone who would like to contribute.

In the next session, I will give an example to do exploratory data analysis on BiG-SLICE query result against the BiG-FAM database.
{% include links.md %}

