---
title: "BGCflow project structure"
teaching: 5
exercises: 0
questions:
- "How do I set my BGCflow project?"
objectives:
- "Setting up configuration and files to start a BGCflow project"
keypoints:
- "A project requires a PEP configuration and a `.csv` file containing a list of genomes to analyse"
- "The project is then defined in the `config.yaml` file"
- An example of a project config can be found in `config/examples`
---
## Setting up your Project Config
Let's move into our freshly cloned BGCflow folder
~~~
cd bgcflow
~~~
{: .language-bash}

To run BGCFlow, we need to activate the BGCFlow conda environment and invoke the command line interface:
~~~
conda activate bgcflow
bgcflow --help
~~~
{: .language-bash}

### Setting up your project samples
In this tutorial, we will analyse 18 publicly available Streptomyces venezuelae genomes. To do that, we will need to prepare a `sample.csv` file with a list of the genome accession ids.
Please find the `sample.csv` for the tutorial here: [https://github.com/NBChub/bgcflow_tutorial/blob/gh-pages/files/samples.csv](https://github.com/NBChub/bgcflow_tutorial/blob/gh-pages/files/samples.csv).

This is how the top of the table looks like:


| genome_id       | source | organism                        | genus        | species | strain     |closest_placement_reference|
|----------------:|-------:|--------------------------------:|-------------:|--------:| ----------:|--------------------------:|
| GCF_000253235.1 | ncbi   |                                 |              |         | ATCC 10712 |                           |
| GCF_001592685.1 | ncbi   |                                 |              |         | WAC04657   |                           |
| ...             | ...    | ...                             | ...          | ..      | ...        | ...                       |

There are two required columns that needs to be filled:
- **`genome_id`** _[required]_:  The genome accession ids (with genome version for `ncbi` and `patric` genomes). For `custom` fasta file provided by users, it should refer to the fasta file names stored in `data/raw/fasta/` directory with `.fna` extension.
- **`source`** _[required]_: Source of the genome to be analyzed choose one of the following: `custom`, `ncbi`, `patric`. Where:
  - `custom` : for user provided genomes (`.fna`) in the `data/raw/fasta` directory with genome ids as filenames 
  - `ncbi` : for list of public genome accession IDs that will be downloaded from the NCBI refseq (GCF...) or genbank (GCA...) database
  - `patric`: for list of public genome accession IDs that will be downloaded from the PATRIC database 

The other optional metadata that we can provide are:
- `organism` _[optional]_ : name of the organism that is same as in the fasta header
- `genus` _[optional]_ : genus of the organism. Ideally identified with GTDBtk.
- `species` _[optional]_ : species epithet (the second word in a species name) of the organism. Ideally identified with GTDBtk.
- `strain` _[optional]_ : strain id of the organism
- `closest_placement_reference` _[optional]_: if known, the closest NCBI genome to the organism. Ideally identified with GTDBtk.

For now, we will only provide the strain information and leave the taxonomic information blank. For publicly available genomes, BGCflow will try to fetch the taxonomic placement from GTDB release 202.

To set up the config, we will create a project folder named `s_venezuelae` inside the `config` directory:
```bash
mkdir -p config/s_venezuelae
wget -O config/s_venezuelae/samples.csv https://raw.githubusercontent.com/NBChub/bgcflow_tutorial/gh-pages/files/samples.csv
```

### Define your project in the config.yaml
Now that we have our sample file ready, we need to define our project in the `config.yaml`. An example of the config file can be found in the `config/examples/_config_example.yaml`.
Let's copy that file and use it as a template:

```bash
cp config/examples/_config_example.yaml config/config.yaml
```
Let's open the newly created config.yaml. The newly copied config.yaml will have this example project defined:
```yaml
# Project 1
  - name: example
    samples: config/examples/_genome_project_example/samples.csv
    rules: config/examples/_genome_project_example/project_config.yaml
    prokka-db: config/examples/_genome_project_example/prokka-db.csv
    gtdb-tax: config/examples/_genome_project_example/gtdbtk.bac120.summary.tsv
```
Replace those lines with this:
```yaml
# Project 1
  - name: s_venezuelae
    samples: config/s_venezuelae/samples.csv
#    rules: config/examples/_genome_project_example/project_config.yaml
#    prokka-db: config/examples/_genome_project_example/prokka-db.csv
#    gtdb-tax: config/examples/_genome_project_example/gtdbtk.bac120.summary.tsv
```

For now, we will just use two mandatory variables:
- `name` : name of your project
- `samples` : a csv file containing a list of genome ids for analysis with multiple sources mentioned. Genome ids must be unique.

**PS:** Commented lines will not be processed.

### Checking the jobs with Snakemake dry-run
Before, we use the `-n` when calling `snakemake`. This parameters means a dry-run, which is used to simulate all the jobs that will be run given the information provided in the config file. You can also add the parameters `-r` to see the reason why those jobs are generated.

Let's do a dry run to check if our project is successfully configured:
```bash
snakemake -n -r
```

> ## Challenges
> - How many jobs will be generated?
> - How many `antismash` jobs will be generated?
> - Why do each jobs only run with 1 core?
> - What do you think `localrule` `all` does?
{: .discussion}

{% include links.md %}

