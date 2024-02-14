---
title: "Customizing BGCFlow config for analyzing fungal genomes"
teaching: 5
exercises: 0
questions:
- "How can I run BGCFlow for fungal genomes using a custom configuration?"
objectives:
- "Understand how to customize BGCFlow configuration for fungal genomes"
- "Learn how to run BGCFlow with a specific configuration for fungal genome analysis"
keypoints:
- "BGCFlow can be customized for analyzing fungal genomes using specific configurations"
- "Running BGCFlow with these configurations allows for targeted analysis of fungal genomes"
---

## Pre-requisite
- Activate the BGCFlow conda environment and make sure you have a clone of BGCFlow installed locally (see Part 1 - Introduction)

```bash
cd <your BGCFlow path>
git checkout dev-0.9.0-1
conda activate bgcflow
```
- Make sure to have the `bgcflow_wrapper` version `0.3.5` or above:

```bash
bgcflow --version
bgcflow_wrapper, version 0.3.5
```

## Set up Fungi Project Configuration
- Inside the config folder, create a new project folder named fungi, the final project configuration will look like this:

```yaml
config/
├── fungi
│   ├── project_config.yaml # BGCFlow project config
│   └── samples.csv # a csv files listing all your samples
└── config.yaml # BGCFlow global config
```

- Create the `project_config.yaml` and edit the contain to have this values:

```yaml
name: Fungi
pep_version: 2.1.0
description: "Example of a fungi project."
input_folder: "."
input_type: "gbk" # BGCFlow does not have annotation tools for eukaryotes, so we will use the genbank from NCBI
sample_table: samples.csv

#### RULE CONFIGURATION ####
# rules: set value to TRUE if you want to run the analysis or FALSE if you don't
rules:
  seqfu: TRUE
  mash: TRUE
  fastani: FALSE
  checkm: FALSE
  gtdbtk: FALSE
  prokka-gbk: FALSE
  antismash: TRUE
  query-bigslice: TRUE
  bigscape: TRUE
  bigslice: TRUE
  automlst-wrapper: FALSE
  arts: FALSE
  roary: FALSE
  eggnog: TRUE
  eggnog-roary: FALSE
  deeptfactor: FALSE
  deeptfactor-roary: FALSE
  cblaster-genome: TRUE
  cblaster-bgc: TRUE
```

- Please note that some tools are not designed for for analysing fungal genomes.
- Create or edit `samples.csv` to have this values:

```
genome_id,source,organism,genus,species,strain,closest_placement_reference,input_file
GCA_014117465.1,ncbi,,,,,,
GCA_014784225.2,ncbi,,,,,,
GCA_030515275.1,ncbi,,,,,,
GCA_014117485.1,ncbi,,,,,,

```

## Update the global configuration
- Now that we have our project ready, we need to update the global configuration so it is registered as one of the BGCFlow project to run
- Edit the `config/config.yaml` file to include only the fungal project to run:

```
# This file should contain everything to configure the workflow on a global scale.

#### PROJECT INFORMATION ####
# This section control your project configuration.
# Each project are separated by "-".
# A project can be defined as (1) a yaml object or (2) a Portable Encapsulated Project (PEP) file.
# (1) To define project as a yaml object, it must contain the variable "name" and "samples".
#   - name : name of your project
#   - samples : a csv file containing a list of genome ids for analysis with multiple sources mentioned. Genome ids must be unique.
#   - rules: a yaml file containing project rule configurations. This will override global rule configuration.
#   - prokka-db (optional): list of the custom accessions to use as prokka reference database.
#   - gtdb-tax (optional): output summary file of GTDB-tk with "user_genome" and "classification" as the two minimum columns
# (2) To define project using PEP file, only variable "name" should be given that points to the location of the PEP yaml file.
#   - pep: path to PEP .yaml file. See project example_pep for details.
# PS: the variable pep and name is an alias

projects:
# Project 2 (PEP file)
  - pep: config/fungi/project_config.yaml

bgc_projects:
  - pep: config/lanthipeptide_lactobacillus/project_config.yaml
...
```

## Running the main BGCFlow pipeline
- Run the workflow by changing the config by:

```bash
snakemake --use-conda -c 8 --config "taxonomic_mode=fungi"
```

{% include links.md %}
