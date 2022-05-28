---
title: Singularity Containers
has_children: false
nav_order: 50
published: true # set to false to remove this tab from your suite's doc site
---

## {{page.title}}

Developers can help users speed installation and enjoy the most controlled possible 
pipeline execution by supporting Singularity containers.
You can choose to wrap your entire tool suite, or just individual pipelines, in 
container images that you distribute in a registry, such as the GitHub Container Registry.

- Singularity: <https://sylabs.io/guides/latest/user-guide/>
- GitHub Container Registry: <https://docs.github.com/en/packages/>

### Suite-level containers

The simplest approach is to enable your entire tool suite for container support
by editing files (please see commented sections within for more information):

- _config.yml
- singularity.def

The advantage of this approach is simplicity. 
A potential disadvantages is the large size of the resulting container.

### Pipeline-level containers

Alternatively, you may prefer to place individual pipelines into their own containers.
See additional README.md documentation in the pipelines folder.
