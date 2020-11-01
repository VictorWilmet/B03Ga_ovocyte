Maturation des ovocytes
================
Engels Guyliann & Philippe grosjean

<!--- do not edit readme.md ---->

``` r
SciViews::R
```

    ## ── Attaching packages ───────────────────────────────────────────────────────────────────────────────────────────── SciViews::R 1.1.0 ──

    ## ✔ SciViews  1.1.0        ✔ purrr     0.3.2   
    ## ✔ chart     1.3.0        ✔ readr     1.3.1   
    ## ✔ flow      1.0.0        ✔ tidyr     0.8.3   
    ## ✔ data.io   1.2.2        ✔ tibble    2.1.1   
    ## ✔ svMisc    1.1.0        ✔ ggplot2   3.1.1   
    ## ✔ forcats   0.4.0        ✔ tidyverse 1.2.1   
    ## ✔ stringr   1.4.0        ✔ lattice   0.20.38 
    ## ✔ dplyr     0.8.0.1      ✔ MASS      7.3.51.3

    ## ── Conflicts ────────────────────────────────────────────────────────────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ✖ dplyr::select() masks MASS::select()

## Objectif

``` r
ovo <- read("data/ovocyte.rds") %>.%
  mutate(., mat = as.factor(mat))
```

Le jeu de données `ovocyte.rds` porte sur la maturation d’ovocytes. Une
concentration connue d’hypoxantine est ajouté afin de faire maturer les
ovocytes.

Vous pouvez avoir une représentation des données avec la fonction
suivante :

``` r
skimr::skim(ovo)
```

    ## Skim summary statistics
    ##  n obs: 280 
    ##  n variables: 3 
    ## 
    ## ── Variable type:character ─────────────────────────────────────────────────────────────────────────────────────────────────────────────
    ##  variable missing complete   n min max empty n_unique
    ##       ind       0      280 280   1   1     0        7
    ## 
    ## ── Variable type:factor ────────────────────────────────────────────────────────────────────────────────────────────────────────────────
    ##  variable missing complete   n n_unique            top_counts ordered
    ##       mat       0      280 280        2 0: 174, 1: 106, NA: 0   FALSE
    ## 
    ## ── Variable type:numeric ───────────────────────────────────────────────────────────────────────────────────────────────────────────────
    ##  variable missing complete   n mean   sd p0  p25 p50 p75 p100     hist
    ##      conc       0      280 280 1.54 1.41  0 0.25   1   3    4 ▇▂▁▂▁▂▁▂

La variable `mat` est a deux niveaux :

  - 0 : l’ovocyte n’est pas en maturation
  - 1 : l’ovocye a maturé

On dénombre pour chaque concentration d’hypoxantine le nombre suivant
d’ovocyte :

``` r
ovo %>.%
  group_by(., as.factor(conc)) %>.%
  summarise(., number = length(mat)) %>.%
  spread(., key = `as.factor(conc)`, value = number)
```

    ## # A tibble: 1 x 7
    ##     `0` `0.25` `0.5`   `1`   `2`   `3`   `4`
    ##   <int>  <int> <int> <int> <int> <int> <int>
    ## 1    40     40    40    40    40    40    40

> Résumez le tableau de données afin d’obtenir la proportion d’ovocytes
> ayant maturé.

> Réalisez un modèle linéaire génaralisé afin d’étudier la proportion
> d’ovocytes ayant maturé.

> Consignez vos résultats dans un document structuré au format R
> Markdorwn. Utilisez le template mis à votre disposition dans le
> dossier analysis.Ce document doit contenir une introduction sur
> l’hypoxantine et l’effet de cette substance sur les ovocytes. Ce
> document doit contenir une section analyse avec la description des
> données et la réalisation du modèle linéaire généralisé. Chaque
> tableau et graphique doit avoir une légende claire et précise comme
> montré dans l’exemple. Tout comme dans les revues scientifiques, les
> tableaux et graphiques doivent être cité dans le texte.
