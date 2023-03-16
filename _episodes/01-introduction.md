---
title: "Introduction"
teaching: 5
exercises: 0
questions:
- "How do I run BGCflow in my computer?"
objectives:
- "Getting a clone of BGCflow into your own machine"
keypoints:
- "A Snakemake environment is required to run BGCflow"
- "A copy of BGCflow can be acquired by using `git clone` or downloading the latest release"
---

> ## Before you start
> - **VM Access:** For workshop participants, we have set up a VM with Conda and Snakemake installed. [Please refer to setup instruction to access the VM.](https://nbchub.github.io/bgcflow_tutorial/setup.html)
> - **Accessing a private github repo:** At the moment, BGCflow repository are kept in private. To access the repository, you will need to create a github account and given access to the repository by the maintainers. Make sure you can access the repo at [https://github.com/NBChub/bgcflow](https://github.com/NBChub/bgcflow)
{: .callout}

## Software Requirements
### Installing Conda
* BGCflow requires a UNIX based environment with conda installed. See: https://docs.conda.io/projects/conda/en/latest/user-guide/install/linux.html
* We advise users to also install [Mamba](https://github.com/mamba-org/mamba). In case you don’t use [Mambaforge](https://github.com/conda-forge/miniforge#mambaforge) you can always install [Mamba](https://github.com/mamba-org/mamba) into any other Conda-based Python distribution with:

~~~
conda install -n base -c conda-forge mamba
~~~
{: .language-bash}


## Deploying a local copy of BGCFlow
### Creating Conda Environment
Let us install a conda environment called bgcflow:
~~~
mamba create -n bgcflow pip -y
~~~
{: .language-bash}

### Installing BGCFlow wrapper
We will use pip to install BGCFlow wrapper, a command line interface to help users interact with the BGCFlow snakemake workflows:
~~~
conda activate bgcflow
pip install git+https://github.com/NBChub/bgcflow_wrapper.git
bgcflow --help
~~~
{: .language-bash}

### Getting a copy of BGCFlow
Go to the directory where you want to install BGCFlow and do:
~~~
cd <my bgcflow directory>
bgcflow clone .
~~~
{: .language-bash}

Make sure to have the right access / SSH Key. If you don't have the access, ask the instructor for a zipped copy of BGCFlow releases.

### Initiating configuration from template
To run BGCFlow, users need to set up a Snakemake configuration file and the PEP file for each projects. To initiate an example config.yaml from template and run an example project, do:
~~~
bgcflow init
~~~
{: .language-bash}

You can do a dry-run (checking the workflow without actually running it) using:
~~~
bgcflow run -n
~~~
{: .language-bash}

You can modify the configuration located in `config/config.yaml`. Note that current configuration run several projects located in the `.examples` folder:
```yaml
projects:
# Project 1 (yaml object)
  - name: example
    samples: .examples/_genome_project_example/samples.csv
    rules: .examples/_genome_project_example/project_config.yaml
    prokka-db: .examples/_genome_project_example/prokka-db.csv
    gtdb-tax: .examples/_genome_project_example/gtdbtk.bac120.summary.tsv

# Project 2 (PEP file)
  - name: .examples/_pep_example/project_config.yaml
```

### Running the Lactobacillus tutorial dataset
For the tutorial, we will be running a small dataset of *Lactobacillus delbrueckii* genomes from NCBI. First, copy the folder `lactobacillus_delbruecki` from the `.examples` folder to the `config` folder:
~~~
cp .examples/lactobacillus_delbruecki config/. -r
~~~
{: .language-bash}

Then, use text editor to modify `config/config.yaml`. Change the projects to:
```yaml
projects:
  - name: config/lactobacillus_delbruecki/project_config.yaml
```

Do a dry run to make sure you are running the right project:
```bash
bgcflow run -n
```

When you are ready to run the workflow, remove the `-n` flag. You can see the full parameters by running `bgcflow run --help`.

### Download the latest release/tags
The command `bgcflow clone` utilizes git to get the latest branch of BGCFlow. You can also grab other releases from the the github repository tags at [https://github.com/NBChub/bgcflow/tags](https://github.com/NBChub/bgcflow/tags) and click on the latest release/tags. On the assets, you can click the source code link to download it.

{% include links.md %}

