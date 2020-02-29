---
title: A simple example
#permalink: /docs/example/
---

<img src="/img/pep_contents.svg" alt="" style="float:right; margin-left:20px" width="350px">

To use the PEP toolkit, you first need a *project*, which is nothing more than a collection of data with its metadata. To create a PEP to represent your dataset, you simply describe your data using PEP structure, which is composed of 2 files:



1. **Project config file** - a ``yaml`` file describing file paths and optional project settings
2. **Sample annotation sheet** - a ``csv`` file with 1 row per sample


In the simplest case, ``project_config.yaml`` is just a few lines of ``yaml``. Here's a minimal example `project_config.yaml`:


```{yaml}
metadata:
 output_dir: /path/to/output/folder
 sample_annotation: /path/to/sample_annotation.csv
```

If you're not already familiar with `yaml`, it's a simple and widely used hierarchical markup language used to store key-value pairs; you can <a href="http://www.yaml.org/start.html">read more about yaml here</a>.

The `output_dir` key specifies where to save results. The `sample_annotation` key points to the second key part of a *PEP*, a comma-separated value (``csv``) file describing samples in the project. Here's a small example of `sample_annotation.csv`:

```{csv}
"sample_name", "protocol", "file"
"frog_1", "RNA-seq", "frog1.fq.gz"
"frog_2", "RNA-seq", "frog2.fq.gz"
"frog_3", "RNA-seq", "frog3.fq.gz"
"frog_4", "RNA-seq", "frog4.fq.gz"
```

With those two simple files, you are ready to use the pepkit tools! Now, with a single line of code, you could load your metadata into R using <a href="/docs/pepr/">pepr</a>, into python using <a href="/docs/pep/">pep</a>, or run each sample through an arbitrary command-line pipeline using <a href="/docs/looper/">looper</a>. 

If you make a habit of describing all your projects like this, you'll never parse another sample annotation sheet again. You'll never write another pipeline submission loop.

This simple example presents a basic, minimal, functioning PEP. In practice, there is lots more to learn about advanced features of PEP structure. You can add additional sections to your configuration ``yaml`` file and to your sample annotation ``csv`` file to tailor it for specific tools. But at its core, PEP is simple and generic; this way, you can start with the basics, and only add more complexity as you need it.

The next sections in this documentation will introduce the advanced details of both annotation sheets and project config files.
