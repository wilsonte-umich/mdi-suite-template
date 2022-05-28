---
title: Pipeline Config Files
parent: Stage 1 Pipelines
has_children: false
nav_order: 30
---

## {{page.title}}

Each pipeline must have a configuration file named
**pipelines/\<pipeline\>/pipeline.yml**
with metadata about the pipeline.  

Please see the comments in the _template pipeline.yml file in addition 
to the guidance below.

### condaFamilies

All pipelines use conda to construct an appropriate execution
environment with proper versions of all required program
dependencies, for explicit version control, reproducibility
and portability. These might include any program called from 
the command line or a shell script to do data analysis work.
