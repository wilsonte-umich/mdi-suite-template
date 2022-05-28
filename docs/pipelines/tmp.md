---
published: false
---

### Job configuration files (specifying pipeline options)

You may provide all options through the command line 
as you would for any typical program.  Use '--help' to
see the available options. 

However, we recommend instead writing a '\<data\>.yml'
configuration file to set options, and then providing
the path to that file to the pipeline. This makes
it easy to assemble jobs and to keep a history of what
was done, especially if you use our job manager.

Config files are valid YAML files, although the interpreter
we use to read them only processes a subset of YAML features.
[Learn more about YAML on the internet](https://www.google.com/search?q=yaml+basics), 
or just proceed, it is intuitive and easy.

### Config file templates

To get a template to help you write your config file use:

```bash
mdi <pipelineName> template --help
mdi <pipelineName> template -a -c
```

In general, the syntax is:

```yml
# <data>.yml
---
pipeline: [suiteName/]pipelineName[:suiteVersion]
variables:
    VAR_NAME: value
pipelineAction:
    optionFamily:
        optionName1: $VAR_NAME # a single keyed option value
        optionName2:
            - valueA # an array of option values, executed in parallel
            - valueB
execute:
    - pipelineAction
```

The 'suiteName' and 'version' components of the pipeline declaration are optional, however, including suiteName can improve clarity and ensure that
you are always using the tool you intend. If provided, the version designation should be either:
- a suite release tag of the form 'v0.0.0'
- 'latest', to use the most recent release tag [the default]
- 'pre-release', to use the development code at the tip of the main branch
- for developers, the name of a code branch in the git repository

As a convenience for when you get tired of have many files
with the same option values (e.g., a shared data directory), you may
also create a file called 'pipeline.yml' or '\<pipelineName\>.yml'
in the same directory as '\<data\>.yml'. Options will be read
from 'pipeline.yml' first, then '\<data\>.yml', then finally
from any values you specify on the command line, with the last 
value that is read taking precedence, i.e., options specified on the 
command line have the highest precedence.

### Common workflow actions and options

Each pipeline supports parallel processing via options '--n-cpu' and '--ram-per-cpu'.

Option '--dry-run' allows a test of the action and options configuration prior to actual execution.

Many pipelines are designed to have staged execution with success monitoring. Commands 
'status' and 'rollback' provide support for monitoring and manipulating pipeline
execution status, repeating steps, etc. Pipelines that fail part-way through can be 
re-launched from the failure point by re-calling the initial action.




