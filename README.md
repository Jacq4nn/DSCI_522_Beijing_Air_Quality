Beijing Air Quality Analysis
================

-   [Beijing Air Quality Analysis](#beijing-air-quality-analysis)
    -   [Introduction](#introduction)
    -   [About](#about)
    -   [Report](#report)
    -   [Usage](#usage)
    -   [Dependencies](#dependencies)
    -   [License](#license)
-   [References](#references)

# Beijing Air Quality Analysis

-   Authors: Jacqueline Chong, Junrong Zhu, Macy Chan, Vadim Taskaev

Data analysis project for DSCI 522 (Data Science Workflows); a course in
the Master of Data Science program at the University of British
Columbia.

## Introduction

The objective of this project is to answer the following inferential
question: **Do PM2.5 measurements in Beijing, China collected between
2013 and 2017 show any sign of improvement?**

The capital city of Beijing, China has long struggled with poor air
quality, a result of the country’s rapid industrialization and its heavy
reliance on coal for electricity generation the North, as well as its
growing and increasingly urban middle class \[@wang2012air\]. This
analysis question is important for its timely and global implications.
As air pollution from the burning of fossil fuels and its association
with climate change and direct health outcomes poses a challenge to
nations worldwide, we explore whether we may find evidence of economic
growth coinciding with improving air quality. In fact, in September
2021, the World Health Organization revised its air quality guidelines
to more restrictive levels following the increasingly evident causal
relationships between poor air quality and its harmful health
consequences on impacted mainly urban communities \[@world2021global\].

We analyse the `Beijing Air Quality` data set, donated to the UC Irvine
Machine Learning Repository in 2019 (accessible via
[URL](https://archive-beta.ics.uci.edu/ml/datasets/beijing+multi+site+air+quality+data)),
which comprises hourly measurement of six air pollutants (including
`PM2.5`, `PM10`, `SO2`, `NO2`, `CO`, `O3`) and six meteorological
variables spanning from 2013 until 2017 across twelve of its
metropolitan data-collecting stations. While the structure of this data
set makes it suitable for multi-variate time-series regression analysis,
we focus our analysis solely on the readings of the `PM2.5` metric, a
form of fine particulate matter that is considered especially harmful
for its ability to penetrate deep into the lungs and cause long-lasting
damage to the respiratory system \[@xing2016impact\].

The report for our exploratory data analysis can be found
[here](https://github.com/UBC-MDS/DSCI_522_Beijing_Air_Quality/blob/main/src/Beijing_air_quality_EDA.md).

## About

Given that we have good sample size for both samples and the data points
are independent, we performed a **hypothesis test** to determine whether
there is statistical evidence to indicate an improvement in PM2.5
measurements in Beijing between 2013 and year 2017. We implemented
one-tailed test to answer the question since we expect to detect the
improvement in PM2.5 pollution.

-   Null Hypothesis(\*H\*\<sub>0\</sub>): The measurement of PM2.5 in
    Beijing from time_B does not show any sign of improvement comparing
    to time_A. (Point estimate of PM2.5 in time_A is less than and equal
    to the point estimate of PM2.5 in time_B)

-   Alternative Hypothesis(*H*<sub>0</sub>): The measurement of PM2.5 in
    Beijing from time_B shows an improvement comparing to time_A. (Point
    estimate of PM2.5 in time_A is greater than the point estimate of
    PM2.5 in time_B)

After conducting the permutation test in the difference of medians, we
get a p-value of 1, which is greater than the significance level
$\\\\alpha$ = 0.05.

## Report

The final report can be found
[here](https://github.com/UBC-MDS/DSCI_522_Beijing_Air_Quality/blob/main/doc/Beijing_air_quality_report.md).

## Usage

To replicate the analysis, clone this GitHub repository, install the
[dependencies](#dependencies) listed below, and run the following
commands at the command line/terminal from the root directory of this
project:

    # download data
    python src/download_data.py --url=https://archive.ics.uci.edu/ml/machine-learning-databases/00501/PRSA2017_Data_20130301-20170228.zip --out_folder=data/raw
    Rscript -e "rmarkdown::render('src/Beijing_air_quality_EDA.Rmd')"

    # run eda report
    Rscript -e "rmarkdown::render('src/Beijing_air_quality_EDA.Rmd')"

    # pre-process data
    Rscript src/pre_process_data.R --input=data/raw/PRSA_Data_20130301-20170228 --out_dir=data/processed

    # create exploratory data analysis figure and write to file
    Rscript src/eda_generate_plots.R --input=src/pre_process_data.R --out_dir=results

    # hypothesis_testing
    Rscript src/hypothesis_testing_script.R --input=data/processed/processed_data.csv --out_dir=results

    # render final report
    Rscript -e "rmarkdown::render('doc/Beijing_air_quality_report.Rmd', output_format = 'github_document')"

## Dependencies

-   Python 3.7.3 and Python packages:

    -   docopt==0.6.2
    -   requests==2.22.0
    -   pandas==0.24.2
    -   urllib.request==3.9

-   R version 3.6.1 and R packages:

    -   knitr==1.36
    -   tidyverse==1.3.1
    -   ggthemes==4.2.4
    -   here==1.0.1
    -   cowplot==1.1.1
    -   scales==1.1.1
    -   forcats==0.5.1
    -   stringr==1.4.0
    -   dplyr==1.0.7
    -   purrr==0.3.4
    -   readr==2.0.2
    -   tidyr==1.1.3
    -   tibble==3.1.5
    -   ggplot2==3.3.5
    -   infer==1.0.0

## License

This dataset is licensed under a [Creative Commons Attribution 4.0
International](https://creativecommons.org/licenses/by/4.0/legalcode) (CC
BY 4.0) license.

This allows for the sharing and adaptation of the datasets for any
purpose, provided that the appropriate credit is given.

# References
