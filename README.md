Exercices pratiques cadrés sur le module 3 Modèle linéaire : Maturation
des ovocytes
================

<!--- do not edit readme.md ---->

# Avant-propos

Cette séance d’exercices est en cours de développement. N’hésitez pas à
vérifier le lien suivant afin de voir si des modifications n’ont pas été
apportées dans les consignes :
<https://github.com/BioDataScience-Course/B03Ga_ovocyte>

# Introduction

``` r
ovo <- read("data/ovocyte.rds") %>.%
  mutate(., mat = as.factor(mat))
```

Le jeu de données `ovocyte.rds` que vous allez utiliser porte sur la
maturation d’ovocytes. Afin de faire maturer les ovocytes, différentes
concentrations connue d’hypoxantine sont testées.

La fonction suivante, vous donne une représentation des données
contenues dans `ovocyte.rds` :

``` r
skimr::skim(ovo)
```

|                                                  |      |
| :----------------------------------------------- | :--- |
| Name                                             | ovo  |
| Number of rows                                   | 280  |
| Number of columns                                | 3    |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_   |      |
| Column type frequency:                           |      |
| character                                        | 1    |
| factor                                           | 1    |
| numeric                                          | 1    |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ |      |
| Group variables                                  | None |

Data summary

**Variable type: character**

| skim\_variable | n\_missing | complete\_rate | min | max | empty | n\_unique | whitespace |
| :------------- | ---------: | -------------: | --: | --: | ----: | --------: | ---------: |
| ind            |          0 |              1 |   1 |   1 |     0 |         7 |          0 |

**Variable type: factor**

| skim\_variable | n\_missing | complete\_rate | ordered | n\_unique | top\_counts    |
| :------------- | ---------: | -------------: | :------ | --------: | :------------- |
| mat            |          0 |              1 | FALSE   |         2 | 0: 174, 1: 106 |

**Variable type: numeric**

| skim\_variable | n\_missing | complete\_rate | mean |   sd | p0 |  p25 | p50 | p75 | p100 | hist  |
| :------------- | ---------: | -------------: | ---: | ---: | -: | ---: | --: | --: | ---: | :---- |
| conc           |          0 |              1 | 1.54 | 1.41 |  0 | 0.25 |   1 |   3 |    4 | ▇▂▂▂▂ |

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

# Objectif

Ce projet est un projet **individuel**, **court** et **cadré** qui doit
être **terminé pour la fin du module 3**.

# Consignes

1.  Résumez le tableau de données afin d’obtenir la proportion
    d’ovocytes ayant maturé.

2.  Réalisez un graphique permetant de représenter la proportion
    d’ovocytes ayant maturé en fonction de la concentration
    d’hypoxantine .

3.  Réalisez un modèle linéaire génaralisé afin d’étudier la proportion
    d’ovocytes ayant maturé.

4.  Consignez vos résultats dans un document structuré au format R
    Markdorwn. Utilisez le template (`ovocytes.Rmd`) mis à votre
    disposition dans le dossier `docs`. Ce document doit contenir :
    
      - une courte introduction sur l’hypoxantine et l’effet de cette
        substance sur les ovocytes.
      - une section analyse avec la description des données et la
        réalisation du modèle linéaire généralisé. Chaque tableau et
        graphique doit avoir une légende claire et précise comme montré
        dans l’exemple. Tout comme dans les revues scientifiques, les
        tableaux et graphiques doivent être cité dans le texte.
      - une section discussion et conclusion
