---
title: Looper
---

<img src="/img/logo_looper.svg" alt="" style="float:left; margin:10px" width="80">

`looper` is a command-line job submitting engine. It's the **glue that connects your PEP project to command-line pipelines**. It can work with any pipeline that takes command-line arguments. 
`looper` is modular and totally configurable, so it scales as your needs grow. It is a cog in pepkit that makes it easy to run any kind of command-line tool serially across all the samples in your project. `looper` is not a pipeline workflow engine, which is used to build pipelines. `looper` assumes you already have pipelines built, and it helps you map samples to those pipelines. We provide a suite of already-built pipelines for ease-of-use, but you can configure it to work with just about anything. You have complete control.



### Code and documentation

* [Hello looper example repository](https://github.com/pepkit/hello_looper) - A very simple PEP and looper pipeline with hands-on tutorial to test out looper.
* [User documentation and vignettes](http://looper.readthedocs.io)
* [Source code at Github](https://github.com/pepkit/looper)

### Quick start

Install with

```{bash}
pip install https://github.com/pepkit/looper/zipball/master
```

Once your PEP project and your pipelines are configured, you run your samples through `looper`  with this command:

```{bash}
looper run project_config.yaml
```

That command will parse your PEP samples, and build jobs for each one. It’s scalable: by default, it runs your jobs sequentially on the local computer, but with a small configuration change, it will create and submit jobs to any cluster resource manager (like SLURM, SGE, or LFS).

To check on your running jobs, you run:

```{bash}
looper check project_config.yaml
```

To summarize the statistics of all the pipeline runs, you type:

```{bash}
looper summarize project_config.yaml
```


### Looper pipelines

Here is a [list of publicly available looper-compatible pipelines](https://github.com/pepkit/hello_looper/blob/master/looper_pipelines.md)
