---
title: Project config file
permalink: /docs/project_config/
---

A project config file is organized into sections. Most are optional. Here are additional details on each of the configuration sections:


### Project config section: `metadata`

The `metadata` section is **the only required section** of a PEP. It contains paths to various parts of the project: this must include pointers to at least 1) the sample annotation sheet; and 2) the parent output directory.

Here's a minimal example with just the two required variables:

	metadata:
	  sample_annotation: /path/to/sample_annotation.csv
	  output_dir: /path/to/parent/output/folder

The `sample_annotation` value can be absolute or relative; relative paths are assumed relative to the location of the `project_config.yaml` file.

The `metadata` section also allows for another attribute, called `sample_subannotation`, which points to a second annotation table to accommodate samples with multiple values for one or more attributes. Most projects do not require subannotation tables, but for more details, see the advanced section on [sample subannotation](/docs/sample_subannotation).

### Project config sections: `derived_columns` and `data_sources`

The sections called `derived_columns` and `data_sources` provide a flexible way to point to data files on disk. These two sections go together (so they aren't meaningful independently; if you define one you should define the other). 

The `derived_columns` section provides a way to link short keys to variable-encoded file paths. The variables in the file paths are formatted as `{variable}`, and are populated by sample attributes (columns in the sample annotation sheet). For example, your files may be stored in `/path/to/{sample_name}.fastq`, where `{sample_name}` will be populated individually for each sample in your PEP.

Example:

	data_sources:
	  key1: "/path/to/raw/data/{sample_name}_{sample_type}.bam"
	  key2: "/path/from/collaborator/weirdNamingScheme_{external_id}.fastq"
	  key3: "${HOME}/{test_id}.fastq"

You can also use shell environment variables (like ``${HOME}``).

The `derived_columns` section simply identifies which column names (or sample attributes) should be populated as data_sources. Corresponding sample attributes will then have as their value derived from the string replacement of sample attributes specified in the config file. This enables you to point to more than one input file for each sample. 

Example:

```
derived_columns: [read1, read2, data_1]
```

For more details and a complete example, see [derived columns](/docs/derived_columns).

### Project config section: implied_columns

``implied_columns`` lets you infer additional attributes, which can be useful for pipeline arguments. For instance, it may that one sample attribute implies several more. Rather than encoding these each as separate, non-varying columns in the annotation sheet, you may simply indicate in the `project_config.yaml` that samples of a certain type should automatically inherit additional attributes.

Example:

```
implied_columns:
  organism:
    human:
      genome: "hg38"
      macs_genome_size: "hs"
```

This example says that any sample with `organism` attribute set to the string "human" should also automatically set additional attributes of `genome` (with value "hg38") and `macs_genome_size` (with value "hs"). These implied attributes may now be used as pipeline arguments or for other analysis.

For more details, see [implied columns](/docs/implied_columns).

### Project config section: subprojects


Subprojects are useful to define multiple similar projects within a single project config file. Under the subprojects key, you can specify names of subprojects, and then underneath these you can specify any project config variables that you want to overwrite for that particular subproject. Tell looper to load a particular subproject by passing ``--sp subproject-name`` on the command line.

For example:

```
subprojects:
  diverse:
	metadata:
	  sample_annotation: psa_rrbs_diverse.csv
  cancer:
	metadata:
	  sample_annotation: psa_rrbs_intracancer.csv
```

This project would specify 2 subprojects that have almost the exact same settings, but change only their ``metadata.sample_annotation`` parameter (so, each subproject points to a different sample annotation sheet). Rather than defining two 99% identical project config files, you can use a subproject. 


# Looper sections

The following sections are specific to `looper`, which is one tool in `pepkit`. These sections are optional and only useful if you're planning to use `looper` to submit pipelines for your project.

### Project config section: metadata

The `metadata` section (described previously) has some additional attributes that are understood by `looper`. It may optionally include pointers to the submission-script subdirectory (where submit scripts are stored), the results subdirectory, and pipeline interface files.

Example:

	metadata:
	  sample_annotation: /path/to/sample_annotation.csv
	  output_dir: /path/to/parent/output/folder
	  results_subdir: results_pipeline
	  submission_subdir: submission
	  pipeline_interfaces: /path/to/pipeline_interface.yaml


### Project config section: pipeline_config

Occasionally, a particular project needs to run a particular flavor of a pipeline. Rather than creating an entirely new pipeline, you can parameterize the differences with a **pipeline config** file, and then specify that file in the **project config** file.

Example:

```
pipeline_config:
  # pipeline configuration files used in project.
  # Key string must match the _name of the pipeline script_ (including extension)
  # Relative paths are relative to this project config file.
  # Default (null) means use the generic config for the pipeline.
  rrbs.py: null
  # Or you can point to a specific config to be used in this project:
  wgbs.py: wgbs_flavor1.yaml
```

This will instruct `looper` to pass `-C wgbs_flavor1.yaml` to any invocations of wgbs.py (for this project only). Your pipelines will need to understand the config file (which will happen automatically if you use pypiper).

### Project config section: pipeline_args

Sometimes a project requires tweaking a pipeline, but does not justify a completely separate **pipeline config** file. For simpler cases, you can use the `pipeline_args` section, which lets you specify command-line parameters via the project config. This lets you fine-tune your pipeline, so it can run slightly differently for different projects.

Example:

```
pipeline_args:
  rrbs.py:  # pipeline identifier: must match the name of the pipeline script
	# here, include all project-specific args for this pipeline
	"--flavor": simple
	"--flag": null
```

For flag-like options (options without parameters), you should set the value to the yaml keyword ``null`` (which means no value). Looper will pass the key to the pipeline without a value. The above specification will now pass ``--flavor=simple`` and ``--flag`` (no parameter) whenever ``rrbs.py`` is invoked -- for this project only. This is a way to control (and record!) project-level pipeline arg tuning. The only keyword here is `pipeline_args`; all other variables in this section are specific to particular pipelines, command-line arguments, and argument values.


### Project config section: compute

You can specify project-specific compute settings in a ``compute`` section. However, you're better off specifying this globally using a ``pepenv`` environment configuration. Instructions are at the `pepenv repository <https://github.com/pepkit/pepenv>`_. If you do need project-specific control over compute settings (like submitting a certain project to a certain resource account), you can do this by specifying variables in a project config ``compute`` section, which will override global pepenv values for that project only.

```
	compute:
	  partition: project_queue_name
```


# Project config example


 Here's an example. Additional fields can be added as well and will be ignored.

	metadata:
	  # Relative paths are considered relative to this project config file.
	  # Typically, this project config file is stored with the project metadata
	  # sample_annotation: one-row-per-sample metadata
	  sample_annotation: table_experiments.csv
	  # merge_table: input for samples with more than one input file
	  merge_table: table_merge.csv
	  # compare_table: comparison pairs or groups, like normalization samples
	  compare_table: table_compare.csv
	  # output_dir: the parent, shared space for this project where results go
	  output_dir: /fhgfs/groups/lab_bock/shared/projects/example
	  # results and submission subdirs are subdirectories under parent output_dir
	  # results: where output sample folders will go
	  # submission: where cluster submit scripts and log files will go
	  results_subdir: results_pipeline
	  submission_subdir: submission
	  # pipeline_interfaces: the pipeline_interface.yaml file or files for Looper pipelines
	  # scripts (and accompanying pipeline config files) for submission.
	  pipeline_interfaces: /path/to/shared/projects/example/pipeline_interface.yaml


	data_sources:
	  # specify the ABSOLUTE PATH of input files using variable path expressions
	  # entries correspond to values in the data_source column in sample_annotation table
	  # {variable} can be used to replace environment variables or other sample_annotation columns
	  # If you use {variable} codes, you should quote the field so python can parse it.
	  bsf_samples: "$RAWDATA/{flowcell}/{flowcell}_{lane}_samples/{flowcell}_{lane}#{BSF_name}.bam"
	  encode_rrbs: "/path/to/shared/data/encode_rrbs_data_hg19/fastq/{sample_name}.fastq.gz"


    implied_columns:
	# supported genomes/transcriptomes and organism -> reference mapping
	    organism:
	      human:
	        genome: hg38
	        transcriptome: hg38_cdna
	      mouse:
	        genome: mm10
	        transcriptome: mm10_cdna

	pipeline_config:
	  # pipeline configuration files used in project.
	  # Default (null) means use the generic config for the pipeline.
	  rrbs: null
	  # Or you can point to a specific config to be used in this project:
	  # rrbs: rrbs_config.yaml
	  # wgbs: wgbs_config.yaml
	  # cgps: cpgs_config.yaml
