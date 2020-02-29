---
title: Sample annotation file
#permalink: /docs/sample_annotation.html
---

The ``sample annotation sheet`` is a `.csv` file containing information about all samples (or peices of data) in a project. **One row corresponds to one sample** (or, equivalently, one pipeline run).

A sample annotation sheet may contain any number of columns you need for your project. You can think of these columns as `sample attributes`, and you may use these columns later in your pipelines or analysis (for example, you could define a column called ``organism`` and use this to adjust the reference genome to use for each sample). For this reason, we sometimes use the word `column` and `attribute` interchangeably. 

### Special columns

Certain keyword columns are required or provide looper-specific features. Any additional columns become attributes of your sample and will be part of the project's metadata for the samples. Mostly, you have complete control over any other column names you want to add, but there are a few reserved column names:

- ``sample_name`` - a **unique** string identifying each sample [^1]. This is **required** for ``Sample`` construction.  The only required column.

- ``organism`` - a string identifying the organism ("human", "mouse", "mixed"). **Recommended** but not required.

- ``protocol`` - While not needed to build a ``Sample``, this column is required for submission of job(s). It specifies the source of data for the sample (*e.g.* ATAC-seq, RNA-seq, RRBS). ``Looper`` uses this information to determine which pipelines are relevant for the ``Sample``.

- ``data_source`` - This column is used by default to specify the location of the input data file. Usually you want your annotation sheet to specify the locations of files corresponding to each sample. You can use this to simplify pointing to file locations with a neat string-replacement method that keeps things clean and portable. For more details, see the advanced section on [derived columns](/docs/derived_columns). Really, you just need any column specifying at least 1 data file for input.

- ``toggle`` - If the value of this column is not 1, Looper will not submit the pipeline for that sample. This enables you to submit a subset of samples.


Here are a few example annotation sheets:


```
   "sample_name", "protocol", "organism", "flowcell", "lane", "BSF_name", "data_source"
   "albt_0h", "RRBS", "albatross", "BSFX0190", "1", "albt_0h", "bsf_sample"
   "albt_1h", "RRBS", "albatross", "BSFX0190", "1", "albt_1h", "bsf_sample"
   "albt_2h", "RRBS", "albatross", "BSFX0190", "1", "albt_2h", "bsf_sample"
   "albt_3h", "RRBS", "albatross", "BSFX0190", "1", "albt_3h", "bsf_sample"
   "frog_0h", "RRBS", "frog", "", "", "", "frog_data"
   "frog_1h", "RRBS", "frog", "", "", "", "frog_data"
   "frog_2h", "RRBS", "frog", "", "", "", "frog_data"
   "frog_3h", "RRBS", "frog", "", "", "", "frog_data"
```

[1]:
This should be a string without whitespace (space, tabs, etc...). If it contains whitespace, an error will be thrown. Similarly, looper will not allow any duplicate entries under sample_name.
