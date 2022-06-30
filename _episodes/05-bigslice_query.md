---
title: "Part I: Exploring BiG-SLICE query result"
teaching: 0
exercises: 20
questions:
    - " How do I explore BiG-SLICE query result?"
objectives:
    - Visualize query hits to BiG-FAM GCF models with Cytoscape
keypoints:
    - "BGCflow returns an edge table of your BGC query to the top 10 hits of GCF models in the BiG-FAM database"
---

## Exploring BiG-SLICE Query result
In this episode, we will explore BiG-SLICE query hits of _S. venezuelae_ genomes with the [BiG-FAM database (version 1.0.0, run 6)](https://bigfam.bioinformatics.nl/home). First, let us grab the BiG-SLICE query result from bgcflow run.

If you haven't done so, generate a symlink to the bgcflow run on the VM:
```bash
ln -s /datadrive/bgcflow bgcflow
```

Open up this folder `/home/bgcflow/datadrive/bgcflow/data/processed/s_venezuelae/bigslice/query_as_6.0.1` and download the `query_network.csv` and `gcf_summary.csv` to your local computer.

Using Cytoscape, load and visualize your BiG-FAM hits following this video:
### 1. Importing network and annotation from tables
<iframe src="https://drive.google.com/file/d/193F2Mayiv9Zko86k64nbOEJDTArGm6q-/preview" width="640" height="480" allow="autoplay"></iframe>
### 2. Filtering top n hits to disentagle the network
<iframe src="https://drive.google.com/file/d/1mnQKnmQzL2Q8NiJeWvrC6BRdYYLHdh1d/preview" width="640" height="480" allow="autoplay"></iframe>

## Enriching the annotation with other results from BGCflow run
As we can see, without further annotation about the BGC information, the network does not give us much information. In the next step, we will combine summary tables from two other BGCflow outputs:
- BiG-SCAPE
- GTDB taxonomy

We have prepared a jupyter notebook table that will generate the annotation required to enrich our network.

### Getting Jupyter up and running
On your home directory, create a folder called `s_venezuelae_tutorial/notebook`. You can then download the `.ipynb` file of this episode and run it from the directory you just made.
```
mkdir -p s_venezuelae_tutorial/notebook
wget -O s_venezuelae_tutorial/notebook/05-bigslice_query.ipynb {link to .ipynb file}
```

If you're using the VM for the workshop, activate the `bgc_analytics` conda environment by:
```bash
conda activate bgc_analytics 
```

Then, run jupyter lab with:
```bash
jupyter lab --no-browser
```
VS code will forward a link to the jupyter session that you can open in your local machine.

Go to your notebook directory and start exploring the notebook to generate the table
{% include links.md %}