---
title: "Introduction"
teaching: 5
exercises: 0
questions:
- "How do I run BGCflow in my computer?"
objectives:
- "Getting a copy of BGCflow in your own machine"
keypoints:
- "A Snakemake environment is required to run BGCflow"
- "`bgcflow_wrapper` provides shortcut to commonly used Snakemake commands and other tools integrated in BGCFlow"
---

Welcome to the BGCFlow tutorial! BGCFlow is a stack of bioinformatic tools that enables you to analyze biosynthetic gene clusters (BGCs) across large collections of genomes (pangenomes) using the Snakemake workflow manager. In this tutorial, you will learn how to set up and use BGCFlow to streamline your BGC analysis.


> ## Before you start
> Before you dive into using BGCFlow, there are a few prerequisites you need to have in place
> ### Access to a Linux Environment
> BGCFlow is currently tested on Linux (specifically Ubuntu 22). If you're a Windows user, don't worry, you have options too:
> - You can set up a Linux virtual machine (VM) using cloud providers like Microsoft Azure, AWS, or Google Cloud.
> - Windows users can also utilize Windows Subsystem for Linux (WSL2) to create a Linux-like environment.
> ### Conda or Mamba Package Manager
> BGCflow requires a UNIX based environment with Conda installed. If you're not familiar with Conda, you can find installation instructions [here](https://docs.conda.io/projects/conda/en/latest/user-guide/install/linux.html). Additionally, we recommend considering [Mamba](https://github.com/mamba-org/mamba), an alternative package manager. If you're not using [Mambaforge](https://github.com/conda-forge/miniforge#mambaforge), you can install Mamba into any other Conda-based Python distribution with the following command:
> ```bash
> conda install -n base -c conda-forge mamba
> ```
> With these essentials in place, you're ready to proceed with setting up BGCFlow!

## Installing BGCFlow environments
### Creating a Conda Environment
Let's start by creating a dedicated Conda environment for BGCFlow:
```bash
# create and activate a new conda environment
mamba create -n bgcflow -c conda-forge python=3.11 pip openjdk -y # also install java for metabase
```
- **PS:** This environment includes Java / OpenJDK which is required for serving `metabase`.

### Installing the BGCFlow wrapper
Next, we'll install the BGCFlow wrapper, a command-line interface that makes working with BGCFlow's Snakemake workflows easier:
```bash
# activate bgcflow environment
conda activate bgcflow

# install `BGCFlow` wrapper
pip install bgcflow_wrapper

# make sure to use bgcflow_wrapper version >= 0.2.7
bgcflow --version # show the wrapper version

# Verify the installation and view available command line arguments
bgcflow --help
```

The above command will display the help function of the wrapper, providing a comprehensive list of available command line arguments:
```
$ bgcflow --help
Usage: bgcflow [OPTIONS] COMMAND [ARGS]...

  A snakemake wrapper and utility tools for BGCFlow
  (https://github.com/NBChub/bgcflow)

Options:
  --version   Show the version and exit.
  -h, --help  Show this message and exit.

Commands:
  build       Build Markdown report or use dbt to build DuckDB database.
  clone       Get a clone of BGCFlow to local directory.
  deploy      [EXPERIMENTAL] Deploy BGCFlow locally using snakedeploy.
  get-result  View a tree of a project results or get a copy using Rsync.
  init        Create projects or initiate BGCFlow config from template.
  pipelines   Get description of available pipelines from BGCFlow.
  run         A snakemake CLI wrapper to run BGCFlow.
  serve       Serve static HTML report or other utilities (Metabase,...
  sync        Upload and sync DuckDB database to Metabase.
```

### Additional pre-requisites
While the wrapper installation covers the basics, there are a few additional steps to ensure smooth operation:

- **Adjust Conda Channel Priorities:** Set the Conda channel priorities to 'flexible' for a more adaptable package resolution:
With the environment activated, install or setup this configurations:
  - Set `conda` channel priorities to `flexible`
```bash
conda config --set channel_priority disabled
conda config --describe channel_priority
```
With these steps completed, you've laid a solid foundation for using BGCFlow effectively.

## Deploying a local copy of BGCFlow
Before you can start genome mining on your dataset, you'll need to deploy the BGCFlow workflow locally. Follow the steps below to get BGCFlow set up on your machine.

### Cloning BGCFlow Repository

1. Navigate to the directory where you want to store your BGCFlow installation. Make sure you have a decent amount of storage space available.

2. Run the following command to clone the BGCFlow repository to your chosen destination:

   ```bash
   bgcflow clone <my BGCFlow folder>
   ```
Replace `<my BGCFlow folder>` with the path to your desired destination directory.

Additionally, you can specify a specific branch or release tags of BGCFlow to clone using the `--branch` option. By default, the `main` branch will be cloned.

```bash
bgcflow clone --branch v0.8.1 <my BGCFlow folder>
```

You can also manually grab other releases from the the [github repository tags](https://github.com/NBChub/bgcflow/tags) and click on the release/tags of your choice. On the assets, you can click the source code link to download it.

## Initiating configuration from template
To run BGCFlow, users need to set up a Snakemake configuration file and the PEP file for each projects. To initiate an example config.yaml from template and run an example project, do:
~~~
bgcflow init
~~~
{: .language-bash}

You can modify the configuration located in `config/config.yaml` to point out to the right project PEPs.
```yaml
projects:
  - name: config/Lactobacillus_delbruecki/project_config.yaml
```

### Running the Lactobacillus tutorial dataset
For the tutorial, we will be running a small dataset of *Lactobacillus delbrueckii* genomes from NCBI.

You can do a dry-run (checking the workflow without actually running it) using:
```bash
bgcflow run -n
```

When you are ready to run the workflow, remove the `-n` flag. You can see the full parameters by running `bgcflow run --help`. For now, let it be and skip to the next section of the tutorial.

### Download the latest release/tags
The command `bgcflow clone` utilizes git to get the latest branch of BGCFlow. You can also grab other releases from the the github repository tags at [https://github.com/NBChub/bgcflow/tags](https://github.com/NBChub/bgcflow/tags) and click on the latest release/tags. On the assets, you can click the source code link to download it.

{% include links.md %}

