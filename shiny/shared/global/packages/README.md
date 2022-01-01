## R package dependencies

The **packages** folder provides configuration declarations for R packages 
that are common to many apps in a suite.

These same files are also used by MDI::install() to discover the R packages
that are needed.

Any app, module, analysis type, or other component can also declare its need
for a specific R package in a **module.yml** or **config.yml** file,
by adding lines in this format:

```
packages: 
   R:  
    - xxx
    - yyy
   Bioconductor: null
```

Packages declared in an apps suite are never attached using the 
<code>library()</code> function by the apps framework. Thus, you must either:

- call functions in full syntax, e.g., <code>package::function()</code> (PREFERRED)
- call <code>library(package)</code> yourself, which is DISCOURAGED because it may lead to unexpected name conflicts with the packages required to run the apps framework, i.e., you might unexpectedly break the framework when your app loads!
