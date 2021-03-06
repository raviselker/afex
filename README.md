[![CRAN_Status_Badge](http://www.r-pkg.org/badges/version/afex)](http://cran.r-project.org/package=afex)
[![monthly downloads](http://cranlogs.r-pkg.org/badges/afex)](http://cranlogs.r-pkg.org/badges/afex)
[![total downloads](http://cranlogs.r-pkg.org/badges/grand-total/afex)](http://cranlogs.r-pkg.org/badges/grand-total/afex)
[![Research software impact](http://depsy.org/api/package/cran/afex/badge.svg)](http://depsy.org/package/r/afex)
[![Travis-CI Build Status](https://travis-ci.org/singmann/afex.svg?branch=master)](https://travis-ci.org/singmann/afex)


afex: Analysis of Factorial EXperiments
====

The two main functionalities of `afex` are (1) to provide a coherent and intuitive interface to run standard ANOVAs with any number of within- or between-subjects variables (the relevant functions are now called `aov_car`, `aov_ez`, and `aov_4`) and (2) to provide *p*-values for fixed effects in mixed models using `lme4` via function `mixed`. The default outputs of those functions can be directly passed to `lsmeans` for post-hoc tests or contrasts. 


## Installation

- `afex` is available from CRAN so the current stable version can be installed directly via: 
  `install.packages("afex")`

- To install the latest development version you will need the [`devtools`](https://github.com/hadley/devtools) package: 
  `devtools::install_github("singmann/afex@master")`


## What is New

As of version `0.14` several changes to the interface were introduced:

- ANOVA functions renamed to `aov_car`, `aov_ez`, and `aov_4`. Old ANOVA functions are now deprecated.

- new default return argument for ANOVA functions `afex_aov`, an S3 object containing the following:
  1. ANOVA table of class `"anova"`
  2. ANOVA fitted with base R's `aov` (can be passed to `lsmeans` for post-hoc tests)
  3. output from `car::Anova` (for tests of effects), ANOVA table 1. is based on this model
  4. `lm` object passed to `car::Anova`
  5. data used for estimating 2. and 4.
        
-  added support for `lsmeans`: objects of class `afex_aov` can be passed to `lsmeans` directly. `afex` now depends on `lsmeans`.

- added three new real example data sets and a [vignette](http://htmlpreview.github.io/?https://raw.githubusercontent.com/singmann/afex/master/inst/doc/anova_posthoc_singmann_klauer_2011.html) showing how to calculate contrasts after ANOVA.

-  added `expand_re` argument to `mixed` which, if `TRUE`, correctly interprets the `||` notation in random effects with factors (i.e., suppresses estimation of correlation among random effects). `lmer_alt` is a wrapper for `mixed` which uses `expand_re = TRUE`, returns an object of class `merMod` (i.e., does not calculate p-values), and otherwise behaves like `g/lmer` (i.e., does not enforce certain contrasts)

- `nice.anova` was renamed to `nice` (and now also works with `mixed` objects).

- Returned objects of `mixed` and the ANOVA functions (i.e., of class `afex_aov`) are similar:
  - Both have a numeric Anova table as first element called `anova_table` (which is of class `c("anova", "data.frame")`).
  - calling `nice` on either returns a nicely rounded Anova table (i.e., numbers converted to characters). This table is also per default printed.
  - calling `anova` on either will return the numeric Anova table (for which print methods exist as well).
    
- added `afex_options()` functionality for setting options globally.
    
- `afex` does not depend on `car` package anymore, it is only imported.

- first element in mixed object renamed to `anova_table`.
    
- `summary` method for `mixed` objects now calls `summary.merMod` on full model.

----
Please note that this project is released with a [Contributor Code of Conduct](CONDUCT.md). By participating in this project you agree to abide by its terms.
