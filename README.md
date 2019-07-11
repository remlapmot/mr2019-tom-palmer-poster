Repository for my poster at the 2019 Mendelian randomization conference
================

  - The full information about the Mendelian randomization conference is
    at <https://www.mendelianrandomization.org.uk/> .
  - This poster was prepared using the `posterdown` package (Thorne
    2019).
  - The design is based on the Better Scientific Poster design by
    Morrison (2019).
  - I picked up some tips how to edit the html template for the poster
    from <https://github.com/lcolladotor/recount-brain-bog19> .

Here are the steps to recreate the poster.

1.  Install the posterdown package and, due to the edits I made to my
    HTML template file, install the version of the bookdown package at
    this commit.
    
    ``` r
    # remotes::install_github("brentthorne/posterdown") # uncomment on first run
    # remotes::install_github("rstudio/bookdown@364092a") # uncomment on first run
    ```

2.  Launch the posterdown Rmd template for the portrait version of the
    Better Scientific Poster.
    
    ``` r
    rmarkdown::draft("mr2019-tom-palmer-poster.Rmd", 
                     template = "posterdown_betterport", 
                     package = "posterdown")
    ```

3.  Edit the Rmd file with your content.
    
      - I edited the html template provided by posterdown:
          - to make the icons opaque
          - to make a level 4 header force a column break before the
            header. This is so that I could position the “Extra Figures
            & Tables” header at the top of the column. Note since I
            wanted the text of that header to be at level 1 I had to
            introduce the column break with a header level that I didn’t
            use anywhere else on the poster. I used a level 4 header, so
            in my edited template I included the following code.
        <!-- end list -->
        ``` html
        .section h4 {
            break-before: column;
        }
        ```
        Then to trigger the column break in the poster Rmd file I
        included an empty level 4 header `####`.

4.  Render the Rmd file to html. This can be achieved either by clicking
    the Knit button in RStudio or by running (change the file name for
    your poster’s Rmd file).
    
    ``` r
    rmarkdown::render('mr2019-tom-palmer-poster.Rmd',  encoding = 'UTF-8')
    ```

5.  To render on github pages:
    
      - I copied the html poster and its associated `_files` folder and
        folder of figures, `Figures`, to the `docs` folder because I
        prefer enabling github pages for a repo from the docs folder
        rather than from a separate branch. The html file is renamed to
        index.html (and its \_file folder renamed) so the github pages
        page will render.
    
    <!-- end list -->
    
    ``` r
    # install.packages("fs") # uncomment on first run
    fs::file_copy("mr2019-tom-palmer-poster.html",
                  "./docs/index.html",
                  overwrite = TRUE)
    fs::dir_copy("./Figures", "./docs/Figures", overwrite = TRUE)
    fs::dir_copy("./mr2019-tom-palmer-poster_files", 
                 "./docs/index_files", overwrite = TRUE)
    ```
    
      - I then enabled github pages for this repository in the
        repository settings on GitHub.

6.  The pdf version of the poster can be generated either by opening the
    html version in Google Chrome and selecting `Print` then `Save as
    PDF` through the menus or by using the `chrome_print()` function in
    the [`pagedown`](https://github.com/rstudio/pagedown) package as
    follows.
    
    ``` r
    pagedown::chrome_print("mr2019-tom-palmer-poster.html")
    ```
    
      - Note, I find that occasionally page and column breaks can be in
        slightly different positions in the pdf compared to the html, so
        it’s always worth opening the pdf and checking this.

7.  Note that this `README.md` file is generated by knitting
    `README.Rmd` as follows.
    
    ``` r
    rmarkdown::render('README.Rmd',  encoding = 'UTF-8')
    ```

8.  For reproducibility, I report my R session information.
    
    ``` r
    # install.packages("sessioninfo") # uncomment on first run
    sessioninfo::session_info()
    ```
    
        ## - Session info ----------------------------------------------------------
        ##  setting  value                       
        ##  version  R version 3.6.0 (2019-04-26)
        ##  os       Windows 10 x64              
        ##  system   x86_64, mingw32             
        ##  ui       RTerm                       
        ##  language (EN)                        
        ##  collate  English_United Kingdom.1252 
        ##  ctype    English_United Kingdom.1252 
        ##  tz       Europe/London               
        ##  date     2019-07-11                  
        ## 
        ## - Packages --------------------------------------------------------------
        ##  package     * version date       lib source        
        ##  assertthat    0.2.1   2019-03-21 [1] CRAN (R 3.6.0)
        ##  cli           1.1.0   2019-03-19 [1] CRAN (R 3.6.0)
        ##  crayon        1.3.4   2017-09-16 [1] CRAN (R 3.6.0)
        ##  digest        0.6.20  2019-07-04 [1] CRAN (R 3.6.0)
        ##  evaluate      0.14    2019-05-28 [1] CRAN (R 3.6.0)
        ##  htmltools     0.3.6   2017-04-28 [1] CRAN (R 3.6.0)
        ##  knitr         1.23    2019-05-18 [1] CRAN (R 3.6.0)
        ##  magrittr      1.5     2014-11-22 [1] CRAN (R 3.6.0)
        ##  Rcpp          1.0.1   2019-03-17 [1] CRAN (R 3.6.0)
        ##  rmarkdown     1.13    2019-05-22 [1] CRAN (R 3.6.0)
        ##  sessioninfo   1.1.1   2018-11-05 [1] CRAN (R 3.6.0)
        ##  stringi       1.4.3   2019-03-12 [1] CRAN (R 3.6.0)
        ##  stringr       1.4.0   2019-02-10 [1] CRAN (R 3.6.0)
        ##  withr         2.1.2   2018-03-15 [1] CRAN (R 3.6.0)
        ##  xfun          0.8     2019-06-25 [1] CRAN (R 3.6.0)
        ##  yaml          2.2.0   2018-07-25 [1] CRAN (R 3.6.0)
        ## 
        ## [1] C:/Users/palmertm/library
        ## [2] C:/Program Files/R/R-3.6.0/library

## References

<div id="refs" class="references">

<div id="ref-betterposter">

Morrison, M. A. 2019. *Better Scientific Poster*.
<https://osf.io/ef53g>.

</div>

<div id="ref-posterdown">

Thorne, W. Brent. 2019. *posterdown: An R Package Built to Generate
Reproducible Conference Posters for the Academic and Professional World
Where Powerpoint and Pages Just Won’t Cut It*.
<https://github.com/brentthorne/posterdown>.

</div>

</div>
