---
title: "Exploring BGCFlow result database using Metabase"
teaching: 5
exercises: 0
questions:
- "How do I explore and query tabular data from BGCFlow result?"
objectives:
- "Start a local Metabase server"
- "Loadi BGCFlow OLAP database (DuckDB) in metabase"
keypoints:
- "All of the tabular ouputs from BGCFlow are loaded and transformed into an OLAP database (DuckDB)"
- "A business intelligence tools such as Metabase, can be used to interactively explore the database and build SQL queries"
---

## Pre-requisite
- Activate the BGCFlow conda environment and make sure you have a clone of BGCFlow installed locally (see Part 1 - Introduction)
```bash
cd <your BGCFlow path>
conda activate bgcflow
```
- Download and extract a BGCFlow project demo (see Part 7)

## Starting Metabase server
- Make sure you are in your bgcflow directory. Metabase can then be started using:
```bash
bgcflow serve --metabase
```
- Metabase will be launched in locally in http://localhost:3000/

## Setting a local Metabase account
- Follow the steps to set up your account
- Choose DuckDB as the database type and give the DuckDB Path: `/home/<my_user_name>/Lactobacillus_delbrueckii_report/Lactobacillus_delbrueckii/dbt_as_6.1.1/`

{% include links.md %}

