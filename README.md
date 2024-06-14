# R & RStudio Setup
Ozan Ozbeker

# Intro

This is a hybrid blog post/README/code file where it is the actual code
file I use when I update my R environment/computer, but also I wrote
some descriptions along the way so if somebody else stumbles upon this
and likes what they see, they can copy it or maybe even find something
new that they didn’t know about before.

I original wrote this as the README for the GitHub page, but if you are
reading this in my blog, welcome!

# Packages

These are the packages I most frequently use, loosely grouped into the
categories below. This does not include dependency packages. So for
example, I use `quarto` to render Quarto documents via R code, but I
don’t directly use the `markdown` package myself, so it is not listed
below.

You can find the info page for each package at
`https://cran.r-project.org/web/packages/[package_name]/index.html`
where `[package_name]` is the name of the package.

``` r
install.packages(c(
  # Meta Packages
  'tidyverse',  # Easily Install and Load the "Tidyverse" packages | https://tidyverse.tidyverse.org
  'tidymodels', # Easily Install and Load the "Tidymodels" packages | https://tidymodels.tidymodels.org/
  
  # Programming & Development
  'purrr',    # Functional Programming Tools | https://purrr.tidyverse.org/
  'forcats',  # Tools for Working with Categorical Variables (Factors) | https://forcats.tidyverse.org/
  'keyring',  # Package for accessing OS's credential store | https://keyring.r-lib.org/
  'fs',       # Cross-Platform File System Operations Based on 'libuv' | https://fs.r-lib.org/
  'devtools', # Tools to Make Developing R Packages Easier | https://devtools.r-lib.org/

  # Import
  'readr',    # Read Rectangular Data | https://readr.tidyverse.org/
  'httr2',    # Perform HTTP Requests and Process the Responses | https://httr2.r-lib.org/
  'readxl',   # Read Excel Files | https://readxl.tidyverse.org/
  'rvest',    # Easily Harvest (Scrape) Web Pages | https://rvest.tidyverse.org/
  'jsonlite', # A Simple and Robust JSON Parser and Generator for R | https://jeroen.r-universe.dev/jsonlite
  
  # Tidy/Transform
  'dplyr',     # A Grammar of Data Manipulation | https://dplyr.tidyverse.org/
  'tidyr',     # Tidy Messy Data | https://tidyr.tidyverse.org/
  'tibble',    # Simple Data Frames | https://tibble.tidyverse.org/
  'stringr',   # Simple, Consistent Wrappers for Common String Operations | https://stringr.tidyverse.org/
  'lubridate', # Make Dealing with Dates a Little Easier | https://lubridate.tidyverse.org/
  'janitor',   # Simple Tools for Examining and Cleaning Dirty Data | https://sfirke.github.io/janitor/index.html 

  # Visualize
  'ggplot2', # Create Elegant Data Visualizations Using the Grammar of Graphics | https://ggplot2.tidyverse.org/
  
  # Model
  'rsample',   # General Re-sampling Infrastructure | https://rsample.tidymodels.org/
  'parsnip',   # A Common API to Modeling and Analysis Functions | https://parsnip.tidymodels.org/
  'recipes',   # Pre-processing and Feature Engineering Steps for Modeling | https://recipes.tidymodels.org/
  'workflows', # Modeling Workflows | https://workflows.tidymodels.org/
  'tune',      # Tidy Tuning Tools | https://tune.tidymodels.org/
  'yardstick', # Tidy Characterizations of Model Performance | https://yardstick.tidymodels.org/
  'broom',     # Convert Statistical Objects into Tidy Tibbles | https://broom.tidymodels.org/
  'dials',     # Tools for Creating Tuning Parameter Values | https://dials.tidymodels.org/
  'infer',     # Tidy Statistical Inference | https://infer.tidymodels.org/
  'corrr',     # Correlations in R | https://corrr.tidymodels.org/
  
  # Communicate
  'quarto', # R Interface to 'Quarto' Markdown Publishing System

  # Database
  'DBI',     # R Database Interface | https://dbi.r-dbi.org/index.html
  'odbc',    # Connect to ODBC Compatible Databases (using the {DBI} Interface) | https://odbc.r-dbi.org/
  'dbplyr',  # A {dplyr} Back End for Databases | https://dbplyr.tidyverse.org/
  'duckdb',  # {DBI} Package for the DuckDB Database Management System | https://r.duckdb.org/
  'duckplyr' # A DuckDB-backed Version of {dplyr} | https://duckdblabs.github.io/duckplyr/
))

# Other packages I'm interested in:
# 'profvis'  # Interactive Visualizations for Profiling R Code | https://rstudio.github.io/profvis/
# 'targets'  # Pipelining Tools in R | https://docs.ropensci.org/targets/
# 'testthat' # Unit Testing for R | https://testthat.r-lib.org
# 'usethis'  # Automate Package and Project Setup | https://usethis.r-lib.org/
# 'zoo'      # S3 Infrastructure for Regular and Irregular Time Series (Z's Ordered Observations) | https://zoo.R-Forge.R-project.org/
```

# RStudio IDE Configuration

As I’ve been using R & RStudio, I’ve learned which settings I like the
most, whether they are RStudio settings or R options, as well as some
custom snippets. This section of code takes the respective files and
copies them to where the base files for R and RStudioa are. I really
created this because of my job where we log into different virtual
machines, and I got sick of resetting all of these options by hand, so
now I just pull this repo from GitHub and run the code.

The directories don’t exist by default, they are created when you
manually change the respective settings, so this chunk takes care of
that, especially if it’s a fresh install of RStudio.

``` r
purrr::walk(
  .x = c('themes', 'keybindings', 'snippets'),
  .f = \(directory) stringr::str_c("C:/Users/", {Sys.info()[['user']]}, "/AppData/Roaming/RStudio/", directory) |> fs::dir_create()
)
```

Then we copy the files from this folder to their appropriate locations.

``` r
purrr::pwalk(
  .l = tibble::tribble(
    ~file,                   ~destination,
    'rstudio_bindings.json',  stringr::str_glue("C:/Users/{Sys.info()[['user']]}/AppData/Roaming/RStudio/keybindings/rstudio_bindings.json"),
    'KISS - OZBEKER.rstheme', stringr::str_glue("C:/Users/{Sys.info()[['user']]}/AppData/Roaming/RStudio/themes/KISS - OZBEKER.rstheme"),
    'r.snippets',             stringr::str_glue("C:/Users/{Sys.info()[['user']]}/AppData/Roaming/RStudio/snippets/r.snippets"),
    'rstudio-prefs.json',     stringr::str_glue("C:/Users/{Sys.info()[['user']]}/AppData/Roaming/RStudio/rstudio-prefs.json"),
    '.Rprofile',              stringr::str_glue("C:/Users/{Sys.info()[['user']]}/Documents/.Rprofile")),
  .f = \(file, destination) fs::file_copy(path = file, new_path = destination, overwrite = TRUE)
)
```

## “Real” Dark Mode & Theme

I hate that when you use dark mode in RStudio, it’s just this dark blue
shade for the UI, not actually dark/black. Also, I’m really not a fan of
any of the themes that come with RStudio. Luckily for me, GitHub user
[rileytwo](https://github.com/rileytwo) made a fix for both of those
problems for me.

- [{darkstudio}](https://github.com/rileytwo/darkstudio) is a package
  that turns the IDE elements to shades of black whenever you are using
  a theme with `rs-theme-is-dark: TRUE`.
- [Kiss: Keep It Stupid Simple](https://github.com/rileytwo/kiss) is a
  theme from Riley that just looks so good, it’s been my go to for over
  a year now.

If either of these interest you, please go check them out as they have
been the staple to my R experience and I like to support the creator as
best as I can.

``` r
devtools::install_github('rileytwo/darkstudio')
darkstudio::activate() # This requires admin privileges
```
