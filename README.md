# MDI Tools Suite Template

The [Michigan Data Interface](https://midataint.github.io/) (MDI) 
is a framework for developing, installing and running 
Stage 1 HPC **pipelines** and Stage 2 interactive web applications 
(i.e., **apps**) in a standardized design interface.

This is a **repository template** you can use to
create a new **MDI tools suite**. Follow the instructions
below to copy this repository, then fill your copy with code to define 
a suite of your own data analysis pipelines and/or apps.

The steps below were performed and provided as a separate working 
tool suite repository you can use to validate your MDI installation 
with a simple demo pipeline and app.

- <https://github.com/MiDataInt/demo-mdi-tools.git>

## Template usage

### Create a new repository from this template

**To get started quickly**, 
[click here to create a new suite repository from this template](https://github.com/MiDataInt/mdi-suite-template/generate).

You will be prompted for the user and name of the repository you would like 
to create. We recommend **NAME-mdi-tools**, replacing 'NAME' with a specific, 
informative name of your choosing, e.g., 'johndoelab'.

### Copy and use the _template pipeline or app

The easiest way to start a new tool is to copy and modify the _\_template_
pipeline or app, which provides a working boilerplate for all required code. 
Copy/paste, change the folder name, and start coding. Along the way,
write documentation files for your tools.

### Additional instructions

Please see the following documentation pages for detailed information
on using the features of your new tool suite and the MDI frameworks
to quickly develop pipelines and apps:

- [Tool suite template documentation](https://midataint.github.io/mdi-suite-template)
- [MDI pipelines framework documentation](https://midataint.github.io/mdi-pipelines-framework)
- [MDI apps framework documentation](https://midataint.github.io/mdi-apps-framework)

---
## Quick Start 1: single-suite installation

In single-suite mode, you will:
- clone this tool suite repository
- call its _install.sh_ script to create a suite-specific MDI installation
- OPTIONAL: call _alias.pl_ to create an alias to the suite's _run_ utility
- call its _run_ utility to use its tools

### Install this tool suite

```bash
git clone https://github.com/GIT_USER/NAME-mdi-tools.git
cd NAME-mdi-tools
./install.sh
```

### Create an alias to the suite's _run_ utility

```bash
perl alias.pl NAME # you can use a different alias name if you'd like
```

### Execute a Stage 1 pipeline from the command line

For help, call the _run_ utility with no arguments.

```bash
./run
NAME # if you created an alias above
```

### Launch the Stage 2 web server

While you can launch the MDI web server using the command line utility,
it is much better to use the [MDI Desktop app](https://midataint.github.io/mdi-desktop-app),
which allows you to control both local and remote MDI web servers.

---
## Quick Start 2: multi-suite installation

In multi-suite mode, you will:
- clone and install the MDI
- add this tool suite (and potentially others) to your configuration file
- re-install the MDI to add this tool suite to your MDI installation
- call the _mdi_ utility to use its tools

### Install the MDI framework

Please read the _install.sh_ menu options and the 
[MDI installer instructions](https://github.com/MiDataInt/mdi.git) to decide
which installation option is best for you. Briefly, choose option 1
if you will only run Stage 1 HPC pipelines from your installation.

```bash
git clone https://github.com/MiDataInt/mdi.git
cd mdi
./install.sh
```

### Add an alias to _.bashrc_ (optional)

These commands will help you create a permanent named alias to the _mdi_
target script in your new installation.

```bash
./mdi alias --help
./mdi alias --alias mdi # change the alias name if you'd like 
`./mdi alias --alias mdi --get` # activate the alias in the current shell (or log back in)
mdi
```

### Add this tool suite to your MDI installation

Edit file _mdi/config/suites.yml_ as follows:

```yml
# mdi/config/suites.yml
suites:
    - GIT_USER/NAME-mdi-tools
```

and re-run _install.sh_. 
Alternatively, you can install this suite from within the 
Stage 2 web server, or run the following from the command line:

```bash
mdi add -p -s GIT_USER/NAME-mdi-tools 
```

### Execute a Stage 1 pipeline from the command line

For help, call the _mdi_ utility with no arguments.

```bash
mdi
```

### Launch the Stage 2 web server

While you can launch the MDI web server using the command line utility,
it is much better to use the [MDI Desktop app](https://midataint.github.io/mdi-desktop-app),
which allows you to control both local and remote MDI web servers.
