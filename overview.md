---
title: "Tool Suite Template"
has_children: false
nav_order: 0
---
<!--- edit the title above with the short name of your repository, 
      e.g, "My Tools", which will appear on the menu tab item -->

<!-- please do not alter the next line -->
{% include mdi-project-overview.md %} 

<!-- replace this section with markdown content describing your tool suite -->
<!-- https://www.markdownguide.org/basic-syntax/ -->

Stage 1 Pipelines and Stage 2 Apps are carried in 
[tool suites](https://midataint.github.io/docs/project-structure/#tool-suites)
offered by various code developers. 

These pages document the use of the **MDI tool suite template**, 
which you can use to launch your own suite of pipelines and apps. 

- <https://github.com/MiDataInt/mdi-suite-template>

### Quick Start

[**Click here**](https://github.com/MiDataInt/mdi-suite-template/generate) to create a new suite repository from this template.

>We recommend **NAME-mdi-tools** as the name of your 
repository, replacing 'NAME' with an informative name of your choosing, 
e.g., 'johndoelab'.

Open and edit the following files, following the instructions in comments
to find lines to edit to match your needs:

- _config.yml
- overview.md
- LICENSE (adjust the license type, year, and licensee)
- aws-mdi.md (specify the resources needed for a public server, if relevant)
- README.md (delete the developer instructions, if desired)

Then copy and modify the '_template' pipeline or app, which provides working boilerplates for all required tool code. 

<!-- please do not alter the next line -->
{% include mdi-project-documentation.md %}
