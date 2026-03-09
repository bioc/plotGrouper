
<!-- README.md is generated from README.Rmd. Please edit that file -->

# plotGrouper <img src="vignettes/logo.png" align="right" height="150px" width="150px" />

*by **John D. Gagnon*** <br> *University of California, San Francisco*

<a href="https://app.travis-ci.com/jdgagnon/plotGrouper"><img border='0' src="https://app.travis-ci.com/jdgagnon/plotGrouper.svg?branch=master" title="Travis-CI build status."/></a>
<br>
<!-- <a href="#archives"><img border="0" src="https://bioconductor.org/shields/availability/plotGrouper.svg" title="Whether the package is available on all platforms; click for details."/></a></span> -->
<!-- <a href="http://bioconductor.org/packages/stats/bioc/plotGrouper/"><img border='0' src="https://bioconductor.org/shields/downloads/plotGrouper.svg" title="Ranking by number of downloads. A lower number means the package is downloaded more frequently. Determined within a package type (software, experiment, annotation, workflow)."/></a> -->
<a href="http://bioconductor.org/checkResults/devel/bioc-LATEST/plotGrouper/"><img border='0' src="https://bioconductor.org/shields/build/devel/bioc/plotGrouper.svg" title="build results; click for full report"/></a>
<a href="http://bioconductor.org/packages/stats/bioc/plotGrouper/"><img border='0' src="https://bioconductor.org/shields/downloads/release/plotGrouper.svg" title="Ranking by number of downloads. A lower number means the package is downloaded more frequently. Determined within a package type (software, experiment, annotation, workflow)."/></a>
<a href="https://support.bioconductor.org/t/plotgrouper/"><img border='0' src="https://img.shields.io/badge/support-plotGrouper-blue.svg" title="Support site activity, last 6 months: tagged questions/avg. answers per question/avg. comments per question/accepted answers, or 0 if no tagged posts."/></a>
<a href="#since"><img border="0" src="https://bioconductor.org/shields/years-in-bioc/plotGrouper.svg" title="How long since the package was first in a released Bioconductor version (or is it in devel only)."/></a>
<a href="http://bioconductor.org/checkResults/devel/bioc-LATEST/plotGrouper/"><img border='0' src="https://bioconductor.org/shields/last-commit/devel/bioc/plotGrouper.svg" title="time since last commit. possible values: today, < 1 week, < 1 month, < 3 months, since release, before release"/></a>

### Table of Contents

**[Overview](#overview)**<br> **[Installation](#installation)**<br>
**[Usage](#usage)**<br> **[Session info](#session-info)**<br>
**[License](#license)**<br>

## Overview

A shiny app-based GUI wrapper for ggplot2 with built-in statistical
analysis. Import data from file and use dropdown menus and checkboxes to
specify the plotting variables, graph type, and look of your plots. Once
created, plots can be saved independently or stored in a report that can
be saved as a pdf. If new data are added to the file, the report can be
refreshed to include new data. Statistical tests can be selected and
added to the graphs. <br>

Analysis of flow cytometry data is especially integrated with
plotGrouper. Count data can be transformed to return the absolute number
of cells in a sample (this feature requires inclusion of the number of
beads per sample and information about any dilution performed). <br>

Examples of some of the types of plots you can create: <br>

<img src="vignettes/Bar_Violin_example.png" style="width:100.0%" />
<br><br>

<img src="vignettes/Box_Crossbar_example.png" style="width:100.0%" />

## Installation

- If you do not already have R installed, or your version is out of
  date, download and install the latest
  [version](https://cran.r-project.org).

  - Optionally, install the latest version of [RStudio
    Desktop](https://www.rstudio.com/products/rstudio/#Desktop).

- Download the package from Bioconductor.

``` r
if (!requireNamespace("BiocManager", quietly = TRUE))
  install.packages("BiocManager")
  BiocManager::install("plotGrouper")
```

- Or install the development version of the package from Bioconductor:

``` r
'Bioconductor'
BiocManager::install("plotGrouper", version = "devel")
```

- Or GitHub:

``` r
BiocManager::install("jdgagnon/plotGrouper")
```

## Usage

Load the package into the R session.

`library(plotGrouper)`

To initialize the shiny app, paste the following code in your R console
and run it.

`plotGrouper()`

Once the web app opens, you can access the `iris` dataset by clicking
the iris button to learn how to use the app. After the `iris` data
loads, the selection windows will be automatically populated and a graph
should be displayed.  
The `Raw Data` tab displays the structure of the data loaded. Your file
should be organized in the following way:

| Unique identifier |  Comparisons  |     Variables      |
|:-----------------:|:-------------:|:------------------:|
|   ***Sample***    | ***Species*** | ***Sepal.Length*** |
|     setosa_1      |    setosa     |        5.1         |
|     setosa_2      |    setosa     |        4.9         |
|   versicolor_1    |  versicolor   |         7          |
|   versicolor_2    |  versicolor   |        6.4         |
|    virginica_1    |   virginica   |        6.3         |
|    virginica_2    |   virginica   |        5.8         |
|       etc…        |     etc…      |        etc…        |

These columns can be titled anything you want but values in the columns
are important.

- The `Unique identifier` column should contain only unique values that
  identify each individual sample (e.g., `Sample` within `iris`
  `Raw Data`).

- The `Comparisons` column should contain replicated values that
  identify each individual as belonging to a group (e.g., `Species`
  within `iris` `Raw Data`).

- The `Variables` column(s) should created for each variable you wish to
  plot. The values in these columns must be numeric (e.g.,
  `Sepal.Length`, `Sepal.Width`, `Petal.Length`, `Petal.Width` within
  `iris` `Raw Data`)

After importing a data file, a `Sheet` column will be created and
populated with the sheet name(s) from the file if it came from an excel
spreadsheet or the file name if it came from a csv or tsv file.

- The `Variables to plot` selection window is used to choose which
  variable(s) to plot (e.g., `Sepal.Width` from the `iris` data). If
  multiple are selected, they will be grouped according to the
  `Independent variable` selected.

- The `Comparisons` selection window is used to choose which column
  contains the information that identifies which condition each sample
  belongs to (e.g., the `Species` column within the `iris` data).

- The `Independent variable` selection window is used to select how the
  plots should be grouped. If `variable` is selected (the default), the
  plots will be grouped by the values in `Variables to plot`.

- Use the `Shapes` selector to change the shape of the points for each
  comparison variable.

- Use the `Colors` selector to change the point colors for each
  comparison variable.

- Use the `Fills` selector to change the fill color for the other geoms
  being plotted for each comparison variable.

To prevent the `Shapes`, `Colors`, or `Fills` from reverting to their
defaults, click the `Lock` checkboxes.

Individual plots can be saved by clicking `Save` on the `Plot` tab or
multiple plots may be arranged on a single page by clicking
`Add plot to report`. Clicking this button will send the current plot to
the `Report` tab and assign it a number in the `Report plot #` dropdown
menu. To revisit a plot stored in the `Report` tab, select the plot you
wish to restore and click `Load plot from report`. Changes can be made
to this plot and then updated in the `Report` by clicking
`Update plot in report`.

- The statistics calculated for the current plot being displayed in the
  `Plot` tab are stored in the `Statistics` tab. These can be saved by
  clicking the `Download` button on the `Statistics` tab.

- The `Plot Data` tab contains the reorganized subset of data being
  plotted.

- The `Raw Data` tab displays the dataframe that was created upon import
  of the file along with the automatically created `Sheet` column.

## Session info

Here is the output of `sessionInfo()` on the system on which this
package was developed:

``` r
sessionInfo()
#> R version 4.5.1 (2025-06-13 ucrt)
#> Platform: x86_64-w64-mingw32/x64
#> Running under: Windows 11 x64 (build 26200)
#> 
#> Matrix products: default
#>   LAPACK version 3.12.1
#> 
#> locale:
#> [1] LC_COLLATE=English_United States.utf8 
#> [2] LC_CTYPE=English_United States.utf8   
#> [3] LC_MONETARY=English_United States.utf8
#> [4] LC_NUMERIC=C                          
#> [5] LC_TIME=English_United States.utf8    
#> 
#> time zone: America/New_York
#> tzcode source: internal
#> 
#> attached base packages:
#> [1] stats     graphics  grDevices utils    
#> [5] datasets  methods   base     
#> 
#> other attached packages:
#> [1] rmarkdown_2.30
#> 
#> loaded via a namespace (and not attached):
#>  [1] digest_0.6.39     R6_2.6.1         
#>  [3] fastmap_1.2.0     xfun_0.56        
#>  [5] tidyselect_1.2.1  magrittr_2.0.4   
#>  [7] glue_1.8.0        tibble_3.3.0     
#>  [9] knitr_1.51        htmltools_0.5.9  
#> [11] pkgconfig_2.0.3   dplyr_1.1.4      
#> [13] generics_0.1.4    lifecycle_1.0.5  
#> [15] cli_3.6.5         vctrs_0.6.5      
#> [17] rsconnect_1.7.0   compiler_4.5.1   
#> [19] rstudioapi_0.18.0 tools_4.5.1      
#> [21] evaluate_1.0.5    pillar_1.11.1    
#> [23] yaml_2.3.12       otel_0.2.0       
#> [25] rlang_1.1.6
```

<br><br>

## License

[GNU GPL-3.0-or-later](https://www.gnu.org/licenses/gpl.txt)
