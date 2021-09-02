
<!-- README.md is generated from README.Rmd. Please edit that file -->

# rinja

<!-- badges: start -->

[![Lifecycle:
experimental](https://img.shields.io/badge/lifecycle-experimental-orange.svg)](https://lifecycle.r-lib.org/articles/stages.html#experimental)
[![CRAN
status](https://www.r-pkg.org/badges/version/rinja)](https://CRAN.R-project.org/package=rinja)
[![Codecov test
coverage](https://codecov.io/gh/davidchall/rinja/branch/master/graph/badge.svg)](https://codecov.io/gh/davidchall/rinja?branch=master)
[![R-CMD-check](https://github.com/davidchall/rinja/workflows/R-CMD-check/badge.svg)](https://github.com/davidchall/rinja/actions)
<!-- badges: end -->

rinja is a templating engine for R, powered by the
[inja](https://github.com/pantor/inja) C++ library and inspired by the
[jinja](https://jinja.palletsprojects.com/) Python package.

## Installation

You can install the development version from GitHub:

``` r
# install.packages("remotes")
remotes::install_github("davidchall/rinja")
```

## Usage

``` r
library(rinja)

render("Hello {{ name }}!", list(name = "world"))
#> [1] "Hello world!"
```

Here’s a more advanced example, using loops and conditional statements:

``` r
template <- '
{% for person in people -%}
{%- if "A New Hope" in person.films and default(person.species, "Unknown") == "Human" -%}
  * {{ person.name }} ({{ person.homeworld }})
{%- endif -%}
{%- endfor %}
'

text <- render(template, list(people = dplyr::starwars))
writeLines(text)
#> 
#> * Luke Skywalker (Tatooine)
#> * Darth Vader (Tatooine)
#> * Leia Organa (Alderaan)
#> * Owen Lars (Tatooine)
#> * Beru Whitesun lars (Tatooine)
#> * Biggs Darklighter (Tatooine)
#> * Obi-Wan Kenobi (Stewjon)
#> * Wilhuff Tarkin (Eriadu)
#> * Han Solo (Corellia)
#> * Wedge Antilles (Corellia)
#> * Jek Tono Porkins (Bestine IV)
#> * Raymus Antilles (Alderaan)
```