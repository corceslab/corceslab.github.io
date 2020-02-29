---
title: "Python package: pep"
---

<img src="/img/logo_python.svg" alt="" style="float:left; margin:20px">`pep` is a python package that loads PEPs. It instantiates an in-memory representation of your project and all of its samples, for any downstream purpose. This gives you access to your project metadata from within python.

### Code and documentation

* [User documentation and vignettes](http://pep.readthedocs.io/)
* [pep API](http://pep.readthedocs.io/en/latest/api.html)
* [Source code at Github](https://github.com/pepkit/pep)

### Quick start 

Install with:
```
pip install --user --upgrade https://github.com/pepkit/pep/zipball/master
```

Then you can load your project into Python with this code:

```
import pep

my_project = pep.Project("path/to/project_config.yaml")
my_samples = my_project.samples
```

Once you have your project and samples in your Python session, the possibilities are endless. This is the way `looper` reads your project; `looper` uses these objects to loop through each sample and submit pipelines for each. You could just as easily use these objects for other purposes; for example, one way we use these objects is for post-pipeline processing. We can load the project and it sample objects into an analysis session, where we do comparisons across samples.
