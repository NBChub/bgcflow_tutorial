---
title: "Selecting rules for analysis"
teaching: 5
exercises: 0
questions:
- "How do I set which rules to run?"
objectives:
- "Getting able to select specific BGCflow rules to run"
keypoints:
- "BGCflow rules can be selected by giving a `TRUE` value to the `rules` config"
- "Global rules applied to all projects and defined in the `config.yaml`"
- "Project specific rules can be given to each project and will override the global rule"
- "Project specific rules are written as a separate `.yaml` file"
---
## Global Rules
In the previous tutorial, when doing a dry-run, Snakemake will generate this jobs:

```bash
Job stats:
job                          count    min threads    max threads
-------------------------  -------  -------------  -------------
all                              1              1              1
antismash                       18              1              1
antismash_db_setup               1              1              1
antismash_summary                1              1              1
downstream_bgc_prep              1              1              1
extract_meta_prokka             18              1              1
extract_ncbi_information         1              1              1
fix_gtdb_taxonomy                1              1              1
format_gbk                      18              1              1
gtdb_prep                       18              1              1
ncbi_genome_download            18              1              1
prokka                          18              1              1
write_dependency_versions        1              1              1
total                          115              1              1
```

In BGCflow, rules are defined globally in the `config.yaml`. Rules can be turned on or off by setting the value for each specific rules with `TRUE` or `FALSE`.
```yaml
#### GLOBAL RULE CONFIGURATION ####
# This section configures the rules to run globally.
# Use project specific rule configurations if you want to run different rules for each projects.
# rules: set value to TRUE if you want to run the analysis or FALSE if you don't
rules:
  seqfu: FALSE
  mlst: FALSE
  refseq-masher: FALSE
  mash: FALSE
  fastani: FALSE
  checkm: FALSE
  prokka-gbk: FALSE
  antismash-summary: TRUE
...
``` 
Notice that the only rules set to `TRUE` are `antismash-summary`. So why does Snakemake generate a total of 115 jobs? That is because to generate the final output of `antismash-summary`, other job outputs are required. Snakemake will trace back all the file dependency of the final output and call every jobs require to generate that file.

The rule setting in the `config.yaml` applies globally. So if you several projects that require the same analysis, the rule setting will be applied to all those projects.

## Project specific rule
What if I want to run different analysis for each projects? For this application, you can override the global rule setting by giving each project a `.yaml` file containing project specific rule setting. The file contents is exactly the same as the global rule configuration:
```yaml
#### RULE CONFIGURATION ####
# rules: set value to TRUE if you want to run the analysis or FALSE if you don't
rules:
  seqfu: TRUE
  mlst: FALSE
  refseq-masher: FALSE
  mash: FALSE
  fastani: FALSE
  checkm: FALSE
  prokka-gbk: FALSE
  antismash-summary: FALSE
  antismash-zip: FALSE
  query-bigslice: FALSE
  bigscape: FALSE
  bigslice: FALSE
  automlst-wrapper: FALSE
  arts: FALSE
  roary: FALSE
  eggnog: FALSE
  eggnog-roary: FALSE
  diamond: FALSE
  diamond-roary: FALSE
  deeptfactor: FALSE
  deeptfactor-roary: FALSE
  cblaster-genome: FALSE
  cblaster-bgc: FALSE
```
In this rule, we only set to run `seqfu`, which will quickly give us a summary statistics of our genome sequences.
Copy and paste the rule setting above to a new file called `project_config.yaml`, and save it in the project config folder: `config/s_venezuelae/project_config.yaml`.

Now, we need to edit the `config.yaml` so that BGCflow knows that we would like to override the global rule configuration for our `s_venezuelae` project.
Replace the rules values with this:
```yaml
# Project 1
  - name: s_venezuelae
    samples: config/s_venezuelae/samples.csv
    rules: config/s_venezuelae/project_config.yaml
#    prokka-db: config/examples/_genome_project_example/prokka-db.csv
#    gtdb-tax: config/examples/_genome_project_example/gtdbtk.bac120.summary.tsv
```

Let's do a dry-run again:
```bash
snakemake -n -r 
```

> ## Challenges
> - How many jobs will be generated?
> - Do we succeed in overriding the global rule settting?
{: .discussion}

{% include links.md %}

