# Readme - geography analysis

## Preliminaries

Feel free to use this code for your own research. To maintain the code as published, pull requests will not be considered.

All of the code provided here is available under an open-source <a href="https://opensource.org/licenses/MIT" target="_blank">MIT license</a>.

## Procedure to use code

### Preparing XML files (from PubMed)

XML files can be downloaded directly from PubMed. The search term is entered, then the full dataset is downloaded in XML format.

_The following search results were downloaded on April 17, 2018_

Filename: med-ed-2015-2016.xml
Search term - (“2015/01/01”[Date - Publication] : “2016/12/31"[Date - Publication]) AND ("Education, Medical"[MeSH Terms]) AND (English[Language])

Filename: medicine-2015-2016.xml
Search term - (“2015/01/01”[Date - Publication] : “2016/12/31"[Date - Publication]) AND ("Medicine"[MeSH Terms]) AND (English[Language])

Filename: education-2015-2016.xml
Search term - (“2015/01/01”[Date - Publication] : “2016/12/31"[Date - Publication]) AND ("Education"[MeSH Terms]) AND (English[Language])

Filename: biology-2015-2016.xml
Search term - (“2015/01/01”[Date - Publication] : “2016/12/31"[Date - Publication]) AND ("Biological Science Disciplines"[MeSH Terms]) AND (English[Language])

The files need to be placed in the "raw_data" folder. Note that the file names will be variables for the geolocation script (below).

### Required R packages

All scripts provided here run properly in R version 3.6.0. The following packages need to be installed:
* diverse
* yaml
* jsonlite
* stringr
* RCurl
* readr
* countrycode
* data.table
* rworldmap
* ggplot2
* ggthemes
* dplyr
* RColorBrewer
* wordcloud
* XML

### Running the analysis

This analysis needs to be done step by step. The first step generates files to be used in downstream steps.

Variables in most cases are file names or parts of file names (the one exception is the sampling handle indicated in step 1). In addition, it is **CRITICAL** to supply a google maps API key in a YAML file, or by adding the API key directly to the geolocation.Rmd script.

**0. Set up**
* Download data from PubMed as described above. Try using your own search terms!
* Beware that PubMed data XML fields change over time. Results from 2014 and before will not include affiliations for all authors.
* Place the XML files in the raw_data folder. Be sure to match file names and check file name strings in later steps.
* Get a google maps API key and enter it in the YAML file, or place your own API key directly in the code.
* Ensure that all required packages (listed above) are installed.

**1. geolocation.Rmd - Geolocation script**
* Variables are file name and sampling status
* You must supply an API key in a YAML file or directly in the code (see the keys_blank.yaml file for instructions)
* By toggling sampling status ON, you take a random sample of 2500 records, rather than analyzing all records

**2. frequency_map.Rmd - Create a map showing ranked frequencies of Med Ed publication**
* The Med Ed file generated in step 1 is used here
* This analysis was only done for Med Ed, so the variable names don't change in this script

**3. income_contributions.Rmd - Calculate diversity and frequency of contributions by category**
* The files generated in step 1 are used here
* Change the variable to point to either the Med Ed data, or to the individual samples from other fields

**4. text_analysis.Rmd - Create word clouds and calculate statistical significance**
* The Med Ed file generated in step 1 is used here
* This was only done for Med Ed, so the variable names don't change in this script

**5. chisq_tests.Rmd - This contains the calculations of the chi square tests comparing fields.**
