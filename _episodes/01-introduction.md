---
title: "Introduction"
teaching: 5
exercises: 0
questions:
- "How do I get BGCflow into my computer?"
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
BGCflow requires a UNIX based environment with conda installed.   

### Installing Snakemake
Installing Snakemake using [Mamba](https://github.com/mamba-org/mamba) is advised. In case you don’t use [Mambaforge](https://github.com/conda-forge/miniforge#mambaforge) you can always install [Mamba](https://github.com/mamba-org/mamba) into any other Conda-based Python distribution with:

~~~
conda install -n base -c conda-forge mamba
~~~
{: .language-bash}

Then install Snakemake (version 7.6.1) with:

~~~
mamba create -c conda-forge -c bioconda -n snakemake snakemake=7.6.1
~~~
{: .language-bash}

If you already have Snakemake, then update it to version 7.6.1 that is supported by BGCflow with:

~~~
mamba update -c conda-forge -c bioconda -n snakemake snakemake=7.6.1
~~~
{: .language-bash}

For installation details, see the [instructions in the Snakemake documentation](https://snakemake.readthedocs.io/en/stable/getting_started/installation.html).

## Getting a clone of BGCflow
### Using `git clone`
To clone the BGCflow repository to your local system, do:
~~~
git clone git@github.com:NBChub/bgcflow.git
~~~
{: .language-bash}

Make sure to have the right access / SSH Key.

### Download the latest release/tags
Go to the github repository tags at [https://github.com/NBChub/bgcflow/tags](https://github.com/NBChub/bgcflow/tags) and click on the latest release/tags. On the assets, you can click the source code link to download it.

{% include links.md %}

