# Michigan Data Interface

The [Michigan Data Interface](https://midataint.github.io/) (MDI) 
is a framework for developing, installing and running a variety of 
HPC data analysis pipelines and interactive R Shiny data visualization 
applications within a standardized design and implementation interface.

Data analysis in the MDI is separated into 
[two stages of code execution](https://midataint.github.io/docs/analysis-flow/) 
called Stage 1 HPC **pipelines** and Stage 2 web applications (i.e., **apps**).
Collectively, pipelines and apps are referred to as **tools**.
Please read the [MDI documentation](https://midataint.github.io/) for 
more information.

## Repository contents

This repository is a **repository template** you can use to easily
create a new **MDI tools suite**. Follow the instructions
below to copy this repository, then fill your copy with code to define 
a suite of your own data analysis pipelines and/or apps.

## Template usage

### Create a new repository from this template

**To get started quickly**, 
[click here to create a new suite repository from this template](https://github.com/MiDataInt/mdi-suite-template/generate).

You will be prompted for the user and name of the repository you would like 
to create. We recommend that you use **NAME-mdi-tools** as the name of your 
repository, replacing 'NAME' with a specific, informative name of your choosing, 
e.g., 'johndoelab'.

### Copy and use the _template pipeline or app

The easiest way to start a new tool is to copy and modify the '_template' 
pipeline or app, which provides a working boilerplate for all required code. 
Copy, paste, change the folder name, and start coding.

## Folder structure

The following guide shows where to put code files that define your pipelines and apps.

| Folder          | Subfolder       | Description |  
| --------------- | --------------- | ------------|  
| **pipelines**   |                 | subfolders carry scripts that define individual **Pipelines** |
| **shared**      |                 | subfolders carry scripts with code shared by multiple pipelines | 
| \|--------      | **environments**| yml files that create reusable conda environments for job execution | 
| \|--------      | **modules**     | scripts with reusable code accessible by running pipelines | 
| \|--------      | **options**     | yml files that expose reusable option families for job configuration | 
| **shiny**       |                 | carries scripts that define **R Shiny Apps** | 
| \|--------      | **apps**        | subfolders carry scripts that define individual apps | 
| \|--------      | **shared**      | subfolders carry scripts with code shared by potentially many apps | 

Thus, you should create one subfolder in 'pipelines' or 'apps' for each distinct
tool in your suite. Those tools can draw on the common code elements that you 
populate into 'shared' folders, as required. 
We encourage the use of shared components, 
which is one reason the MDI uses suite repositories carrying multiple related tools.

Note that if you define Stage 2 scripts with the same R function names as the 
[apps framework repository](https://github.com/MiDataInt/mdi-apps-framework), your files
will take precedence over the framework as they are loaded last when an app is launched.

## Suite usage and sharing

Tool suites are installed for use by the MDI installation and/or manager utilities found here:

- <https://github.com/MiDataInt/mdi>
- <https://github.com/MiDataInt/mdi-manager>

Once you have installed the MDI frameworks and created one or more tools, you must make your 
tool suite known to your MDI installation.
Do this by editing file 'mdi/config/suites.yml' as follows:

```yml
# mdi/config/suites.yml
suites:
    - https://github.com/GIT_USER/NAME-mdi-tools.git
    - GIT_USER/NAME-mdi-tools # either format works
```

and then repeating the MDI installation process, which will go much faster
as now it only needs to add new components required by your pipelines and apps.
Alternatively, you can install new suites from within the Stage 2 web server, 
or run the following from the command line:

```bash
mdi add -p -s https://github.com/GIT_USER/NAME-mdi-tools.git
mdi add -p -s GIT_USER/NAME-mdi-tools # either format works
```

If your repository is public (recommended), anyone will be able to perform the steps
above to use your tools. 

If your repository is private, you will need to provide a 
[GithHub Personal Access Token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)
to clone and use your tool suite. Pass the token to MDI commands by creating file 
'~/gitCredentials.R' (or, alternatively, 'mdi/gitCredentials.R'):

```r
# ~/gitCredentials.R
gitCredentials <- list(
    USER_NAME  = "First Name",
    USER_EMAIL = "namef@umich.edu",
    GIT_USER   = "xxx",
    GITHUB_PAT = "xxx"
)
```

## Semantic versioning

### Suite versions

You are encouraged (but not required) to use Git tags, via the 
[GitHub releases feature](https://docs.github.com/en/repositories/releasing-projects-on-github/managing-releases-in-a-repository), 
to maintain a proper version history of your tool suite.
The MDI uses the familiar 'v0.0.0' pattern called semantic versioning, described here:

- <https://semver.org/>

Ultimately, only you can decide how to implement a versioning scheme
for your tool suite, but follow these guidelines:

- advance the patch (3rd) version number for non-breaking code changes
 and small feature additions
- advance the minor (2nd) version number whenever:
    - new program dependencies are introduced, e.g., via conda
    - new pipelines, apps or other major code features are introduced
- advance the major (1st) version whenever breaking changes are introduced that
would prevent job files written for previous versions from working with the current version

Please note that such Git version/release tags apply to the entire tool suite,
not to individual pipelines or apps, which is discussed next. Thus, you 
should advance the tool suite version whenever a matching code change
occurs in any of the tools carried in the suite repository. 

If you choose not to use version/release tags for your tool suite,
users will always be placed onto the tip of the main branch, i.e., the most
recent code commit on 'main'.  If you do use versions, the tip of the main
branch can be accessed with the version directive **pre-release**, whereas
the most recent release tag can be accessed with the directive **latest**.
These last examples show the value of having release tags, as they help ensure
that 'latest' (the default) always points to stable code.

### Pipeline and app versions

Distinct from the tool suite git version tags discussed above, you may also
declare versions of specific pipelines and apps within their YAML configuration files, e.g.:

```yml
# pipeline.yml
pipeline:
    name: myPipeline
    description: "Description of myPipeline"
    version: v0.0.0
```

Such tool versions are _not_ placed into git version tags unless prefixed with the
name of the tool, e.g., 'myPipeline-v0.0.0', but this is usually not necessary. All git tags of format 'v0.0.0' are assumed to be tool suite versions. Thus, to communicate
the version of a tool it is best to simply provide the version of the tool suite that
carries it, which always has an unambiguous mapping to a tool version.

Tool versions are also optional except for pipelines that
offer Singularity containers, which are tagged with the major and minor
versions of the pipeline, e.g. 'myPipeline-v0.0'. Note that the patch version is _not_
included in container labels, so it is critical that either the minor or major pipeline
version be advanced whenever a new system or program dependency is introduced for a 
given pipeline on any of its actions. 

## Suite documentation

This template carries the configuration files needed to easily launch a documentation
web site for your new tools suite repository using a permanent, customized fork 
of the open source Jekyll theme 
[Just the Docs](https://pmarsceill.github.io/just-the-docs/), called
[just-the-docs-mdi](https://github.com/MiDataInt/just-the-docs-mdi).

### Configure your suite's basic information

Open and edit the following files, following the instructions in the comments
to find specific lines you need to edit to match your needs:

- _config.yml
- overview.md
- LICENSE (adjust the license type, year, and licensee as needed)
- aws-mdi.md (specify the resources needed for a public server, if relevant)
- README.md (delete these developer instructions, if desired)
  
### Activate your documentation web page on github.io
  
Activate your new documentation site for loading via github.io as follows:

- navigate to your new repository on GitHub
- click "Settings"
- click the "Pages" tab on the left
- edit the "Source" to be branch 'main' and folder '/root'
- click 'Save'
  
After about a minute, your site will be live at the link indicated on the
Settings / Pages page.  It will track your repository to keep your site up
to date whenever you push or merge changes into the 'main' branch.

Please note that this only works if your repository is public. 
  
### Write your documentation files

Finally, create documentation page files within any folder.
The easy way is to create [markdown](https://www.google.com/search?q=markdown+bascis) 
files similar to the 'overview.md' file you edited above.
By placing these as README.md files into the appropriate folders in your file tree,
users will be able to see them both on GitHub and in your
documentation web site. 

### Just the Docs usage

Please see the 
[Just the Docs](https://pmarsceill.github.io/just-the-docs/) 
documentation for guidance on how to use the Jekyll front matter
at the top of each markdown file to create the nested 
menu items typical of MDI documentation sites. You can see simple 
examples here to get you going:

<https://github.com/MiDataInt/mdi-documentation-template/tree/main/_docs>

## Quick Start

> Please include these instructions at the top of every tool suite, 
after **editing the suite name below** and **deleting this paragraph**.

### Install the MDI framework

First, use the MDI installer to install the code needed to run our tools.

```bash
git clone https://github.com/MiDataInt/mdi.git
cd mdi
./install.sh
```

Please read the menu options and the 
[MDI installer instructions](https://github.com/MiDataInt/mdi.git) to decide
which installation option is best for you. Briefly, choose option 1
if you will only run Stage 1 HPC pipelines, but not Stage 2 web tools,
from your installation.

### Add this tool suite to your MDI installation

Next, make this tool suite known 
to your MDI installation by editing file 'mdi/config/suites.yml' as follows:

```yml
# mdi/config/suites.yml
suites:
    - GIT_USER/NAME-mdi-tools
```

and then re-run <code>install.sh</code>, which will go much faster
the second time. Alternatively, you can install this suite from within the 
Stage 2 web server, or run the following from the command line:

```bash
mdi add -p -s GIT_USER/NAME-mdi-tools 
```

### Run a Stage 1 pipeline from the command line

The installation process above added the 'mdi' utility
to your MDI installation folder. You can use it to run
any pipeline. For help from the command line, simply call
the utility with no arguments:

```bash
mdi
```

### Run the MDI web server

If desired, run the Stage 2 apps web server as follows:

```bash
mdi run --help
mdi run
```

In a few seconds a web browser will open and you will be ready to 
load your data and run an associated app.
