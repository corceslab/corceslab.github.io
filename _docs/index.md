---
title: Getting started
permalink: /docs/home/
redirect_from: /docs/index.html
---

*Portable Encapsulated Projects* (*PEP* for short) is a standardized way to organize metadata. **By *project*, we mean a collection of data, and *PEP* provides a standard way to describe that dataset**. It was designed for use in bioinformatics projects that involve lots of data for a set of samples (which could be individual experiments, organisms, cell lines, what have you). However, the concepts are fundamentally generic and could be applied to any type of project that can represent metadata in tabular form, with rows corresponding to units of interest (*i.e.* samples) and columns corresponding to attributes of those units. PEP makes it easy to:

1. describe all your projects the same way, so you only have to learn one metadata structure
2. work collaboratively, since the organization is standardized
3. share your project with others, who are already familiar with the standard
4. employ a variety of tools or pipelines without restructuring the metadata
5. analyze attributes of your project in the data analysis environment of your choice (R/python).

To use PEP, it's helpful to consider two components separately:

1. the standardized *structure* for organizing a project, which we call *PEP*
2. the *software* (or toolkit) that builds or processes a *PEP*

**Creating a PEP**. To get started, you'll first need to download or define a project (a collection of samples with associated metadata) using PEP format. This is documented here in *Creating a PEP*, which contains simple examples as well as detailed documentation for reference. This is the place to start if you're interested in using PEP structure to organize your projects and the primary source of documentation describing universal features of PEP structure. Start with [a simple example of a PEP](/docs/simple_example/).

**Using PEP tools**. With a PEP in hand, you'll then be able to use any PEP-compatible tool to process your project. This is outlined here in *Reading a PEP*. This page provides a brief introduction to each of the tools in `pepkit` that can read your project. Each tool is its own separate project and has comprehensive documentation elsewhere, which you can find linked from the individual pages here. This will give you an overview of what is already available that can get you started analyzing your PEP or building a new PEP-compatible tool.

## How is this useful?
<img src="/img/data-munging.svg" alt="" style="float:right; margin-left:20px" width="350px">

In a data analysis project, we frequently want to run many different tools on the same input data. Too often, this requires structuring the data uniquely for each tool. This makes it difficult not only to test multiple tools, but also to plug several different datasets into one analysis, because each connection structure must be defined manually.

To alleviate this challenge of linking data to tools, Portable Encapsulated Projects (PEP) standardizes the description of data collections, enabling both data providers and data users to communicate through the common interface. Practically, this means individuals who describe their projects using this format will immediately inherit both greater portability for analysis as well as greater access to external complementary data. This link operates around a simple, standard, extensible definition of a <i>project</i>, or a set of annotated sample data.

To learn more, continue to the next page to see a simple example of a PEP.
