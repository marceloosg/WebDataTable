---
title       : Web DataTable
subtitle    : Html table extractor for data analysis
author      : Marcelo Guimarães
job         : Data Scientist
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides

---
## Web DataTable

*Project*: Reproducible Pitch Presentation (Coursera: Data Products)

*Problem*: In many non-governamental sites there is data available only thought html, without a file export option. This makes specifict data collection difficult.

*Project Objectives*: To extract data from html tables into a data.frame object and perform preliminary analysis.
*Scope*: HTML pages with "**\<table\>**", "**\<th\>**", "**\<tr\>**", "**\<td\>**" tags, ***properly*** used.
Example of a valid html  table:
<!--html_preserve-->
<style>
#my-div
{
    width    : 100%;
    height   : 800px;
    overflow : hidden;
    position : relative;
}

#my-iframe
{
    position : absolute;
    top      : -500px;
    left     : 0px;
    width    : 100%;
    height   :400;
}
strong {
  font-weight: bold;
}
em {
  font-style: italic
}

#linkh{
color:blue;
}

.element{background-color:white;}
</style>
<div id="linkh">https://www.cpubenchmark.net/cpu_list.php</div>
<div id="my-div">
<iframe id="my-iframe" src="https://www.cpubenchmark.net/cpu_list.php">  </iframe>
</div>
<!--/html_preserve-->

--- 
## Solution

We constructed an web application capable of extracting the values from a html "**\<table\>**" tag using R code:

```r
source("assets/R/ReadWebTable.R");
url="https://www.cpubenchmark.net/cpu_list.php"
db=get_db_from_web(url);
```

```
## [1] "Title: PassMark - CPU Benchmarks - List of Benchmarked CPUs"
```

```
##             CPU Name Passmark CPU Mark Rank CPU Value  Price
## 9   AMD A10-5700 APU              4195  571     23.98 175.00
## 14 AMD A10-5800K APU              4633  494     22.06 209.99
## 15  AMD A10-6700 APU              4590  504     36.15 126.99
## 16 AMD A10-6700T APU              3693  659     25.16 146.79
## 17 AMD A10-6790K APU              4657  491     31.72 146.80
```
---

---
## Web Application

Bellow is an application example for the https://www.cpubenchmark.net/cpu_list.php webpage:
<!--/html_preserve-->
<style>
.scrollable{
width: 850px !important;
height: 250px !important;
margin-left: 8%;
}
</style>
<div class="scrollable" style="overflow: auto">
<img src="assets/img/loaded.png"></img>
</div>
<!--/html_preserve-->

 1. The selected url is  https://www.cpubenchmark.net/cpu_list.php.
 2. The "Get Table" extracts **all** tables from the page. The table is displayed on the right.
 3. We filter only the lines where the "CPU Name" column contains the "Intel" text.
 4. Then We selected the mean of the "Price(USD)" column. 
 5. On the left is the resulting mean, number of NA values, number of valid occurrencies and a boxplot of the selected column.
 
---

---
## Considerations

 1. The application works well on raw **html** pages when the  "**\<table\>**", "**\<th\>**", "**\<tr\>**", "**\<td\>**" tags, are ***properly*** used.
 2. Any function can be included in the option list easyly.
 3. It is straightforward to include cleaning functions, in order to apply a numeric functions on mixed text-number columns.
 4. It does not work on webpages that require some function to run in order to produce the tables, e. g., javascript.
 5. It fails to recognized missing tags, which causes the table to be missfilled.
 6. Some pages explicitly forbids this kind of web crawling (data extracting). Read the terms of use of the page you want to extract before using this application.



