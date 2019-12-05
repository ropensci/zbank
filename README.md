zbank
=====



[![Project Status: Active - The project has reached a stable, usable state and is being actively developed.](https://www.repostatus.org/badges/latest/active.svg)](https://www.repostatus.org/#active)
[![cran checks](https://cranchecks.info/badges/worst/zbank)](https://cranchecks.info/pkgs/zbank)
[![Build Status](https://travis-ci.org/ropensci/zbank.svg?branch=master)](https://travis-ci.org/ropensci/zbank)
[![codecov.io](https://codecov.io/github/ropensci/zbank/coverage.svg?branch=master)](https://codecov.io/github/ropensci/zbank?branch=master)
[![rstudio mirror downloads](https://cranlogs.r-pkg.org/badges/zbank)](https://github.com/metacran/cranlogs.app)
[![cran version](https://www.r-pkg.org/badges/version/zbank)](https://cran.r-project.org/package=zbank)

ZooBank API Client

## ZooBank API Docs

See <http://zoobank.org/Api>

## High vs. Low level package APIs

__High level API__

High level functions do the HTTP request and parse data to a data.frame for
ease of downstream use. The high level functions have no underscore on the end
of the function name, e.g., `zb_name_usages`

__Low level API__

The parsing to data.frame in the high level API does take extra time. The low
level API only does the HTTP request, and gives back JSON without doing any
more parsing. The low level functions DO have an underscore on the end
of the function name, e.g., `zb_name_usages_`

## Install

CRAN version


```r
install.packages("zbank")
```

Development version


```r
devtools::install_github("ropensci/zbank")
```


```r
library("zbank")
```

## Examples

Name usages


```r
zb_name_usages(name = "Pseudanthias carlsoni")
#> # A tibble: 1 x 14
#>   tnuuuid originalreferen… protonymuuid label value lsid  parentname namestring
#>   <chr>   <chr>            <chr>        <chr> <chr> <chr> <chr>      <chr>     
#> 1 6ea8bb… 427d7953-e8fc-4… 6ea8bb2a-a5… carl… carl… urn:… ""         carlsoni  
#> # … with 6 more variables: rankgroup <chr>, usageauthors <chr>,
#> #   taxonnamerankid <chr>, parentusageuuid <chr>, cleanprotonym <chr>,
#> #   nomenclaturalcode <chr>
```

Publications


```r
zb_publications(query = "pyle")
#> # A tibble: 157 x 22
#>    referenceuuid label value authorlist year  title citationdetails volume
#>    <chr>         <chr> <chr> <chr>      <chr> <chr> <chr>           <chr> 
#>  1 A91FACC3-F39… <Uns… <Uns… <Unspecif… ""    [Ori… ""              ""    
#>  2 24689AE4-C77… Alon… Alon… Alonso-Za… 2016  Manu… <em>ZooKeys</e… 550   
#>  3 CB272EFD-80D… Aran… Aran… Arango, B… 2019  Thre… <em>ZooKeys</e… 835   
#>  4 913BB1FB-1C2… Asgh… Asgh… Asghari, … 2015  Desc… <em>Zootaxa</e… 3986  
#>  5 F8ECE6CE-E77… Bald… Bald… Baldwin, … 1998  <i>B… <I>Ichthyologi… 45    
#>  6 72D9641B-2A9… Bass… Bass… Basset, Y… 1997  Para… <em>AMBIO: A J… ""    
#>  7 5CB7EE8B-042… Bass… Bass… Basset, Y… 2000  Quan… <em>Bioscience… 50    
#>  8 A06A8B51-46B… Bass… Bass… Bassett, … 1997  Para… <em>AMBIO: A J… ""    
#>  9 FAFE53C6-FDD… Bous… Bous… Boustany,… 2002  Sate… <em>Nature</em… 415   
#> 10 18985DB2-CC5… Bush… Bush… Bush, Eli… 1997  Taxo… <em>Harvard Pa… 2     
#> # … with 147 more rows, and 14 more variables: number <chr>, edition <chr>,
#> #   publisher <chr>, placepublished <chr>, pagination <chr>, startpage <chr>,
#> #   endpage <chr>, language <chr>, languageid <chr>, referencetype <chr>,
#> #   lsid <chr>, parentreferenceid <chr>, parentreference <chr>, authors <list>
```

Authors


```r
zb_authors(query = "Schmutz")
#> # A tibble: 3 x 9
#>   agentnameid label value zblsid familyname givenname preferreduuid agentid
#>   <chr>       <chr> <chr> <chr>  <chr>      <chr>     <chr>         <chr>  
#> 1 F16D374C-5… Achi… Achi… urn:l… Achitte-S… Helga C.  F16D374C-531… F16D37…
#> 2 EC923CC6-E… Schm… Schm… urn:l… Schmutz    Karl      EC923CC6-E5E… EC923C…
#> 3 2E04A84F-4… Schm… Schm… ""     Schmutzler Clarence… 2E04A84F-459… 2E04A8…
#> # … with 1 more variable: isuser <chr>
```

Get info by any ZooBank identifier


```r
zb_id(id = "6EA8BB2A-A57B-47C1-953E-042D8CD8E0E2")
#> # A tibble: 3 x 10
#>   identifier identifierdomain abbreviation identifierurl registeringagen…
#>   <chr>      <chr>            <chr>        <chr>         <chr>           
#> 1 66491      CAS Ichthy Spec… CAS_SPC      http://resea… ""              
#> 2 643345     Taxonomic Seria… ITIS-TSN     http://www.i… ""              
#> 3 urn:lsid:… ZooBank Nomencl… ZB-Act       http://zooba… William N.      
#> # … with 5 more variables: registeringagentfamilyname <chr>,
#> #   registeringagentorganizationname <chr>, identifieruuid <chr>,
#> #   domainlogourl <chr>, resolutionnote <chr>
```

Matching taxon name service


```r
zb_matching(id = "FFF7160A-372D-40E9-9611-23AF5D9EAC4C")
#> # A tibble: 36 x 8
#>    protonymuuid acceptedprotony… protonymuuidarr… fullnamestring
#>    <chr>        <chr>            <chr>            <chr>         
#>  1 FFF7160A-37… FFF7160A-372D-4… FBDC898C-F1EA-4… Cheilodipteru…
#>  2 FFF7160A-37… FFF7160A-372D-4… 97CE20CD-4D6E-4… Gasterosteus …
#>  3 FFF7160A-37… FFF7160A-372D-4… 97CE20CD-4D6E-4… Gaſteroſteus …
#>  4 FFF7160A-37… FFF7160A-372D-4… 4D4EC609-D241-4… Pomatomus sal…
#>  5 FFF7160A-37… FFF7160A-372D-4… 4D4EC609-D241-4… Pomatomus sal…
#>  6 FFF7160A-37… FFF7160A-372D-4… 67D18558-763F-4… Temnodon salt…
#>  7 FFF7160A-37… FFF7160A-372D-4… FBDC898C-F1EA-4… Cheilodipteru…
#>  8 FFF7160A-37… FFF7160A-372D-4… 97CE20CD-4D6E-4… Gasterosteus …
#>  9 FFF7160A-37… FFF7160A-372D-4… 97CE20CD-4D6E-4… Gaſteroſteus …
#> 10 FFF7160A-37… FFF7160A-372D-4… 4D4EC609-D241-4… Pomatomus sal…
#> # … with 26 more rows, and 4 more variables: nomenclaturalcodeid <int>,
#> #   taxonrank <chr>, synonymtype <int>, referencecount <int>
```

ZooBank usage stats


```r
zb_stats(start_date = "2018-03-01", end_date = "2018-04-01")
#> # A tibble: 96 x 3
#>    identifierdomain day        recordcount
#>    <chr>            <chr>      <chr>      
#>  1 ZooBank Author   2018-03-01 39         
#>  2 ZooBank Author   2018-03-02 25         
#>  3 ZooBank Author   2018-03-03 9          
#>  4 ZooBank Author   2018-03-04 6          
#>  5 ZooBank Author   2018-03-05 23         
#>  6 ZooBank Author   2018-03-06 17         
#>  7 ZooBank Author   2018-03-07 27         
#>  8 ZooBank Author   2018-03-08 20         
#>  9 ZooBank Author   2018-03-09 19         
#> 10 ZooBank Author   2018-03-10 3          
#> # … with 86 more rows
```

## Meta

* Please [report any issues or bugs](https://github.com/ropensci/zbank/issues).
* License: MIT
* Get citation information for `zbank` in R doing `citation(package = 'zbank')`
* Please note that this project is released with a [Contributor Code of Conduct][coc]
By participating in this project you agree to abide by its terms.

[![rofooter](https://ropensci.org/public_images/github_footer.png)](https://ropensci.org)

[coc]: https://github.com/ropensci/zbank/blob/master/CODE_OF_CONDUCT.md
