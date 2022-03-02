Descriptivos
================
LLECE: Taller de Análisis II
Marzo 2 de 2022

# Librerias a instalar

``` r
# -------------------------------------------------------------------
# librerias
# -------------------------------------------------------------------

# Nota: instalar librerias manualmente.

#------------------------------------------------
# librerias para instalar librerias remotas
#------------------------------------------------

install.packages('devtools')
install.packages('remotes')

#------------------------------------------------
# libreria ERCE con datos
#------------------------------------------------

devtools::install_github(
  'dacarras/erce',
  auth_token = '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',
  force = TRUE)

#------------------------------------------------
# librerías en uso
#------------------------------------------------

install.packages('tidyverse')
install.packages('mitools')
install.packages('survey')
install.packages('srvyr')

#------------------------------------------------
# libreria con lodown::MIsvyciprop()
#------------------------------------------------

remotes::install_github("ajdamico/lodown")
```

# Código 1.1: pesos BRR con pesos estandarizados o pesos SENATE

``` r
# -------------------------------------------------------------------
# BRR con pesos senate
# -------------------------------------------------------------------

#------------------------------------------------
# BRR/WT factor del BRR sobre los observados
#------------------------------------------------

data_a6 <- erce::erce_2019_qa6 %>%
mutate(repws001 = BRR1/WT * WS) %>%
mutate(repws002 = BRR2/WT * WS) %>%
mutate(repws003 = BRR3/WT * WS) %>%
mutate(repws004 = BRR4/WT * WS) %>%
mutate(repws005 = BRR5/WT * WS) %>%
mutate(repws006 = BRR6/WT * WS) %>%
mutate(repws007 = BRR7/WT * WS) %>%
mutate(repws008 = BRR8/WT * WS) %>%
mutate(repws009 = BRR9/WT * WS) %>%
mutate(repws010 = BRR10/WT * WS) %>%
mutate(repws011 = BRR11/WT * WS) %>%
mutate(repws012 = BRR12/WT * WS) %>%
mutate(repws013 = BRR13/WT * WS) %>%
mutate(repws014 = BRR14/WT * WS) %>%
mutate(repws015 = BRR15/WT * WS) %>%
mutate(repws016 = BRR16/WT * WS) %>%
mutate(repws017 = BRR17/WT * WS) %>%
mutate(repws018 = BRR18/WT * WS) %>%
mutate(repws019 = BRR19/WT * WS) %>%
mutate(repws020 = BRR20/WT * WS) %>%
mutate(repws021 = BRR21/WT * WS) %>%
mutate(repws022 = BRR22/WT * WS) %>%
mutate(repws023 = BRR23/WT * WS) %>%
mutate(repws024 = BRR24/WT * WS) %>%
mutate(repws025 = BRR25/WT * WS) %>%
mutate(repws026 = BRR26/WT * WS) %>%
mutate(repws027 = BRR27/WT * WS) %>%
mutate(repws028 = BRR28/WT * WS) %>%
mutate(repws029 = BRR29/WT * WS) %>%
mutate(repws030 = BRR30/WT * WS) %>%
mutate(repws031 = BRR31/WT * WS) %>%
mutate(repws032 = BRR32/WT * WS) %>%
mutate(repws033 = BRR33/WT * WS) %>%
mutate(repws034 = BRR34/WT * WS) %>%
mutate(repws035 = BRR35/WT * WS) %>%
mutate(repws036 = BRR36/WT * WS) %>%
mutate(repws037 = BRR37/WT * WS) %>%
mutate(repws038 = BRR38/WT * WS) %>%
mutate(repws039 = BRR39/WT * WS) %>%
mutate(repws040 = BRR40/WT * WS) %>%
mutate(repws041 = BRR41/WT * WS) %>%
mutate(repws042 = BRR42/WT * WS) %>%
mutate(repws043 = BRR43/WT * WS) %>%
mutate(repws044 = BRR44/WT * WS) %>%
mutate(repws045 = BRR45/WT * WS) %>%
mutate(repws046 = BRR46/WT * WS) %>%
mutate(repws047 = BRR47/WT * WS) %>%
mutate(repws048 = BRR48/WT * WS) %>%
mutate(repws049 = BRR49/WT * WS) %>%
mutate(repws050 = BRR50/WT * WS) %>%
mutate(repws051 = BRR51/WT * WS) %>%
mutate(repws052 = BRR52/WT * WS) %>%
mutate(repws053 = BRR53/WT * WS) %>%
mutate(repws054 = BRR54/WT * WS) %>%
mutate(repws055 = BRR55/WT * WS) %>%
mutate(repws056 = BRR56/WT * WS) %>%
mutate(repws057 = BRR57/WT * WS) %>%
mutate(repws058 = BRR58/WT * WS) %>%
mutate(repws059 = BRR59/WT * WS) %>%
mutate(repws060 = BRR60/WT * WS) %>%
mutate(repws061 = BRR61/WT * WS) %>%
mutate(repws062 = BRR62/WT * WS) %>%
mutate(repws063 = BRR63/WT * WS) %>%
mutate(repws064 = BRR64/WT * WS) %>%
mutate(repws065 = BRR65/WT * WS) %>%
mutate(repws066 = BRR66/WT * WS) %>%
mutate(repws067 = BRR67/WT * WS) %>%
mutate(repws068 = BRR68/WT * WS) %>%
mutate(repws069 = BRR69/WT * WS) %>%
mutate(repws070 = BRR70/WT * WS) %>%
mutate(repws071 = BRR71/WT * WS) %>%
mutate(repws072 = BRR72/WT * WS) %>%
mutate(repws073 = BRR73/WT * WS) %>%
mutate(repws074 = BRR74/WT * WS) %>%
mutate(repws075 = BRR75/WT * WS) %>%
mutate(repws076 = BRR76/WT * WS) %>%
mutate(repws077 = BRR77/WT * WS) %>%
mutate(repws078 = BRR78/WT * WS) %>%
mutate(repws079 = BRR79/WT * WS) %>%
mutate(repws080 = BRR80/WT * WS) %>%
mutate(repws081 = BRR81/WT * WS) %>%
mutate(repws082 = BRR82/WT * WS) %>%
mutate(repws083 = BRR83/WT * WS) %>%
mutate(repws084 = BRR84/WT * WS) %>%
mutate(repws085 = BRR85/WT * WS) %>%
mutate(repws086 = BRR86/WT * WS) %>%
mutate(repws087 = BRR87/WT * WS) %>%
mutate(repws088 = BRR88/WT * WS) %>%
mutate(repws089 = BRR89/WT * WS) %>%
mutate(repws090 = BRR90/WT * WS) %>%
mutate(repws091 = BRR91/WT * WS) %>%
mutate(repws092 = BRR92/WT * WS) %>%
mutate(repws093 = BRR93/WT * WS) %>%
mutate(repws094 = BRR94/WT * WS) %>%
mutate(repws095 = BRR95/WT * WS) %>%
mutate(repws096 = BRR96/WT * WS) %>%
mutate(repws097 = BRR97/WT * WS) %>%
mutate(repws098 = BRR98/WT * WS) %>%
mutate(repws099 = BRR99/WT * WS) %>%
mutate(repws100 = BRR100/WT * WS) 
```

# Codigo 1.2: porcentaje con variable observada

``` r
# -------------------------------------------------------------------
# estudiantes que han repetido
# -------------------------------------------------------------------

#------------------------------------------------
# inspeccionar variable original
#------------------------------------------------

dplyr::count(data_a6, E6IT16, REPC)
```

    ## # A tibble: 5 × 3
    ##                     E6IT16                 REPC     n
    ##                  <dbl+lbl>            <dbl+lbl> <int>
    ## 1  1 [Nunca he repetido.]   0 [Nunca]           63958
    ## 2  2 [Una vez.]             1 [Una o más veces]  9403
    ## 3  3 [Dos veces o más.]     1 [Una o más veces]  2504
    ## 4  4 [No sé, no recuerdo.] NA                    1001
    ## 5 NA                       NA                    3961

``` r
#------------------------------------------------
# crear base BRR
#------------------------------------------------

library(srvyr)
data_brr <- data_a6 %>%
            erce::remove_labels() %>%
            as_survey_rep(
            type = 'Fay', 
            repweights = starts_with('repws'),
            weights = 'WS',
            combined_weights = TRUE,
            rho = .5,
            mse = TRUE
            )

# Opción: corección a unidad primaria de muestreo que resulte 
# única al estrato

library(survey)
options(survey.lonely.psu="adjust")

#------------------------------------------------
# producir porcentaje regional
#------------------------------------------------
 
tabla_1 <- data_brr %>%
summarize(
  proportion = survey_mean(REPC,na.rm=TRUE, 
  prop_method = 'logit',
  vartype = "ci", 
  level = c(0.95)
    )
  )

#------------------------------------------------
# mostrar tabla
#------------------------------------------------

knitr::kable(tabla_1, digits = 2)
```

| proportion | proportion_low | proportion_upp |
|-----------:|---------------:|---------------:|
|       0.17 |           0.17 |           0.18 |

# Codigo 1.3: porcentaje con variable observada (TSL)

``` r
# -------------------------------------------------------------------
# estudiantes que han repetido
# -------------------------------------------------------------------
#------------------------------------------------
# unir datos y crear cluster únicos
#------------------------------------------------

erce_a6 <- data_a6 %>%
erce::remove_labels() %>%
mutate(id_k = as.numeric(as.factor(paste0(IDCNTRY)))) %>%
mutate(id_s = as.numeric(as.factor(paste0(IDCNTRY, "_", STRATA)))) %>%
mutate(id_j = as.numeric(as.factor(paste0(IDCNTRY, "_", IDSCHOOL)))) %>%
mutate(id_i = seq(1:nrow(.))) 

#------------------------------------------------
# base de datos con diseño
#------------------------------------------------
# survey method: taylor series linearization library(srvyr)
library(srvyr)
data_tsl <- erce_a6 %>% 
            as_survey_design(
            strata = id_s, 
            ids = id_j, 
            weights = WS, 
            nest = TRUE)
# Opción: corección a unidad primaria de muestreo que resulte 
# única al estrato
library(survey)
options(survey.lonely.psu="adjust")
#------------------------------------------------
# producir porcentaje regional
#------------------------------------------------
tabla_2 <- data_tsl %>%
summarize(
  proportion = survey_mean(REPC,na.rm=TRUE, 
  prop_method = 'logit',
  vartype = "ci", 
  level = c(0.95)
    )
  )
#------------------------------------------------
# mostrar tabla
#------------------------------------------------
knitr::kable(tabla_2, digits = 2)
```

| proportion | proportion_low | proportion_upp |
|-----------:|---------------:|---------------:|
|       0.17 |           0.17 |           0.18 |

# Codigo 1.4: porcentaje con variable observada, para un solo país (BRR)

``` r
# -------------------------------------------------------------------
# estudiantes que han repetido
# -------------------------------------------------------------------

#------------------------------------------------
# crear base BRR para un país
#------------------------------------------------

library(srvyr)
ury_brr <- data_a6 %>%
           erce::remove_labels() %>%
           dplyr::filter(COUNTRY == 'URY') %>%
           as_survey_rep(
           type = 'Fay', 
           repweights = starts_with('repws'),
           weights = 'WS',
           combined_weights = TRUE,
           rho = .5,
           mse = TRUE
           )

# Opción: corección a unidad primaria de muestreo que resulte 
# única al estrato

library(survey)
options(survey.lonely.psu="adjust")

#------------------------------------------------
# producir porcentaje regional
#------------------------------------------------

tabla_3 <- ury_brr %>%
summarize(
  proportion = survey_mean(REPC,na.rm=TRUE, 
  prop_method = 'logit',
  vartype = "ci", 
  level = c(0.95)
    )
  )
#------------------------------------------------
# mostrar tabla
#------------------------------------------------
knitr::kable(tabla_3, digits = 2)
```

| proportion | proportion_low | proportion_upp |
|-----------:|---------------:|---------------:|
|       0.19 |           0.17 |           0.21 |

# Codigo 1.5: percentiles para un país (BRR)

``` r
# -------------------------------------------------------------------
# medianas y percentiles de un país
# -------------------------------------------------------------------

#------------------------------------------------
# crear base BRR para un país
#------------------------------------------------

library(srvyr)
ury_brr <- data_a6 %>%
           erce::remove_labels() %>%
           dplyr::filter(COUNTRY == 'URY') %>%
           as_survey_rep(
           type = 'Fay', 
           repweights = starts_with('repws'),
           weights = 'WS',
           combined_weights = TRUE,
           rho = .5,
           mse = TRUE
           )

# Opción: corección a unidad primaria de muestreo que resulte 
# única al estrato

library(survey)
options(survey.lonely.psu="adjust")

#------------------------------------------------
# producir percentiles
#------------------------------------------------

tabla_4 <- ury_brr %>%
summarize(
  per  = survey_quantile(ISECF,na.rm=TRUE, 
          quantiles = c(.25, .50, .75),
          vartype = "ci", 
          level = c(0.95)
          )
  )
#------------------------------------------------
# mostrar tabla
#------------------------------------------------

tabla_4 %>%
knitr::kable(. , digits = 2)
```

| per_q25 | per_q50 | per_q75 | per_q25_low | per_q50_low | per_q75_low | per_q25_upp | per_q50_upp | per_q75_upp |
|--------:|--------:|--------:|------------:|------------:|------------:|------------:|------------:|------------:|
|    0.05 |    0.63 |     1.2 |       -0.01 |        0.58 |         1.2 |        0.12 |         0.7 |         1.3 |

# Codigo 1.6: medianas y percentil 50 para un país (BRR)

``` r
# -------------------------------------------------------------------
# medianas y percentiles de un país
# -------------------------------------------------------------------

#------------------------------------------------
# crear base BRR para un país
#------------------------------------------------

library(srvyr)
ury_brr <- data_a6 %>%
           erce::remove_labels() %>%
           dplyr::filter(COUNTRY == 'URY') %>%
           as_survey_rep(
           type = 'Fay', 
           repweights = starts_with('repws'),
           weights = 'WS',
           combined_weights = TRUE,
           rho = .5,
           mse = TRUE
           )

# Opción: corección a unidad primaria de muestreo que resulte 
# única al estrato

library(survey)
options(survey.lonely.psu="adjust")

#------------------------------------------------
# producir percentil 50 y mediana
#------------------------------------------------
 
tabla_5 <- ury_brr %>%
summarize(
  per  = survey_quantile(ISECF,na.rm=TRUE, 
          quantiles = c(.50),
          vartype = "ci", 
          level = c(0.95)
          ),
  med = survey_median(ISECF,na.rm=TRUE,
           vartype = "ci", 
           level = c(0.95)
          )
  )

#------------------------------------------------
# mostrar tabla
#------------------------------------------------

tabla_5 %>%
tidyr::pivot_longer(
  names(.),
  names_to = 'quantiles',
  values_to = 'values'
  ) %>%
arrange(quantiles) %>%
knitr::kable(. , digits = 2)
```

| quantiles   | values |
|:------------|-------:|
| med         |   0.63 |
| med_low     |   0.58 |
| med_upp     |   0.70 |
| per_q50     |   0.63 |
| per_q50_low |   0.58 |
| per_q50_upp |   0.70 |

``` r
# Nota: estamos "volteando" la tabla con
#       tidyr::pivot_longer, 
#       para que sea más legible.
```

# Codigo 1.7: medias de varios países (BRR)

``` r
# -------------------------------------------------------------------
# medianas y percentiles de 
# -------------------------------------------------------------------

#------------------------------------------------
# crear base BRR para la region
#------------------------------------------------

library(srvyr)
erce_brr <- data_a6 %>%
            erce::remove_labels() %>%
            as_survey_rep(
            type = 'Fay', 
            repweights = starts_with('repws'),
            weights = 'WS',
            combined_weights = TRUE,
            rho = .5,
            mse = TRUE
            )

# Opción: corección a unidad primaria de muestreo que resulte 
# única al estrato

library(survey)
options(survey.lonely.psu="adjust")

#------------------------------------------------
# producir medias para cada país
#------------------------------------------------
 
tabla_6 <- erce_brr %>%
           group_by(COUNTRY) %>%
summarize(
  mean = survey_mean(ISECF,na.rm=TRUE, 
  vartype = "ci", 
  level = c(0.95)
    )
  )

#------------------------------------------------
# mostrar tabla
#------------------------------------------------

tabla_6 %>%
arrange(mean) %>%
knitr::kable(. , digits = 2)
```

| COUNTRY |  mean | mean_low | mean_upp |
|:--------|------:|---------:|---------:|
| NIC     | -0.64 |    -0.69 |    -0.60 |
| HND     | -0.52 |    -0.61 |    -0.44 |
| GTM     | -0.47 |    -0.54 |    -0.40 |
| SLV     | -0.28 |    -0.34 |    -0.22 |
| PER     | -0.21 |    -0.28 |    -0.14 |
| PAN     | -0.12 |    -0.20 |    -0.03 |
| PRY     |  0.03 |    -0.02 |     0.08 |
| COL     |  0.04 |    -0.04 |     0.11 |
| MEX     |  0.04 |    -0.02 |     0.11 |
| DOM     |  0.05 |     0.00 |     0.11 |
| ECU     |  0.08 |     0.02 |     0.14 |
| CUB     |  0.13 |     0.09 |     0.17 |
| BRA     |  0.32 |     0.26 |     0.38 |
| CRI     |  0.34 |     0.27 |     0.40 |
| ARG     |  0.57 |     0.52 |     0.61 |
| URY     |  0.66 |     0.61 |     0.71 |

# Codigo 1.8: Porcentajes de estudiantes sobre el mínimo de competencia de logro en Lenguaje (Estudiantes 6to Grado, ERCE 2019)

``` r
# -------------------------------------------------------------------
# porcentajes con valores plausibles
# -------------------------------------------------------------------

#------------------------------------------------
# cluster únicos
#------------------------------------------------
           
data_a6 <- data_a6 %>%
erce::remove_labels() %>%
mutate(id_s = as.numeric(as.factor(paste0(IDCNTRY, "_", STRATA)))) %>%
mutate(id_j = as.numeric(as.factor(paste0(IDCNTRY, "_", IDSCHOOL)))) %>%
mutate(id_i = seq(1:nrow(.)))

#------------------------------------------------
# variable dummy para los niveles esperados
#------------------------------------------------

data_a6 <- data_a6 %>%
           mutate(all = 1) %>%
           mutate(lan_min_1 = case_when(
           LAN_L1 == 'I'   ~ 0,
           LAN_L1 == 'II'  ~ 0,
           LAN_L1 == 'III' ~ 1,
           LAN_L1 == 'IV'  ~ 1)) %>%
           mutate(lan_min_2 = case_when(
           LAN_L2 == 'I'   ~ 0,
           LAN_L2 == 'II'  ~ 0,
           LAN_L2 == 'III' ~ 1,
           LAN_L2 == 'IV'  ~ 1)) %>%
           mutate(lan_min_3 = case_when(
           LAN_L3 == 'I'   ~ 0,
           LAN_L3 == 'II'  ~ 0,
           LAN_L3 == 'III' ~ 1,
           LAN_L3 == 'IV'  ~ 1)) %>%
           mutate(lan_min_4 = case_when(
           LAN_L4 == 'I'   ~ 0,
           LAN_L4 == 'II'  ~ 0,
           LAN_L4 == 'III' ~ 1,
           LAN_L4 == 'IV'  ~ 1)) %>%
           mutate(lan_min_5 = case_when(
           LAN_L5 == 'I'   ~ 0,
           LAN_L5 == 'II'  ~ 0,
           LAN_L5 == 'III' ~ 1,
           LAN_L5 == 'IV'  ~ 1)
           )

#------------------------------------------------
# base de datos con diseño
#------------------------------------------------

erce_tsl  <- survey::svydesign(
             data    = data_a6, 
             weights = ~WS,
             strata  = ~id_s,
             id = ~id_j,
             nest = TRUE)

# Opción: corección a unidad primaria de muestreo que resulte 
# única al estrato

library(survey)
options(survey.lonely.psu="adjust")

# Nota: withPV() solo funciona con Taylor Series Linearization


dplyr::glimpse(data_a6)
```

    ## Rows: 80,827
    ## Columns: 412
    ## $ IDSTUD    <dbl> 10010502, 10010503, 10010504, 10010505, 10010506, 10010507, …
    ## $ IDCLASS   <dbl> 100105, 100105, 100105, 100105, 100105, NA, 100105, 100105, …
    ## $ IDSCHOOL  <dbl> 1001, 1001, 1001, 1001, 1001, 1001, 1001, 1001, 1001, 1001, …
    ## $ IDCNTRY   <dbl> 170, 170, 170, 170, 170, 170, 170, 170, 170, 170, 170, 170, …
    ## $ COUNTRY   <chr> "COL", "COL", "COL", "COL", "COL", "COL", "COL", "COL", "COL…
    ## $ STRATA    <dbl> 61702111, 61702111, 61702111, 61702111, 61702111, 61702111, …
    ## $ GRADE     <dbl> 6, 6, 6, 6, 6, 6, 6, 6, 6, 6, 6, 6, 6, 6, 6, 6, 6, 6, 6, 6, …
    ## $ QA6       <dbl> 1, 1, 1, 1, 1, 0, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, …
    ## $ WT        <dbl> 211, 211, 211, 211, 211, 211, 211, 211, 211, 211, 211, 211, …
    ## $ WS        <dbl> 0.25, 0.25, 0.25, 0.25, 0.25, 0.25, 0.25, 0.25, 0.25, 0.25, …
    ## $ WI        <dbl> 8.3, 8.3, 8.3, 8.3, 8.3, 8.3, 8.3, 8.3, 8.3, 8.3, 8.3, 8.3, …
    ## $ WJ        <dbl> 25, 25, 25, 25, 25, 25, 25, 25, 25, 25, 25, 25, 25, 25, 25, …
    ## $ E6IT01    <dbl> 4, 5, 3, 5, 3, NA, 2, 6, 5, 1, 3, 2, 2, 5, 6, 2, 3, 2, 3, 2,…
    ## $ E6IT02    <dbl> 2, 2, 2, 2, 2, NA, 1, 2, 2, 1, 2, 1, 1, 2, 1, 2, 2, 1, 2, 2,…
    ## $ E6IT03_01 <dbl> NA, 1, 2, 2, 1, NA, 2, NA, 2, 1, 2, 1, 1, 1, 1, 1, 1, 2, 1, …
    ## $ E6IT03_02 <dbl> 1, 2, 2, 1, 2, NA, 1, 2, 1, 1, 2, 1, 2, 2, NA, 2, 1, 2, 2, 1…
    ## $ E6IT03_03 <dbl> NA, 2, 2, 2, 1, NA, 1, NA, 1, 2, 2, 1, 1, 1, NA, 1, 1, 1, 1,…
    ## $ E6IT03_04 <dbl> NA, 2, 1, 2, 1, NA, 2, 2, 1, 2, 1, 1, 1, 2, NA, 2, 2, 1, 1, …
    ## $ E6IT03_05 <dbl> NA, 2, 2, 2, 1, NA, 2, 2, 1, 2, 2, NA, 1, 2, 2, 2, 2, 1, 2, …
    ## $ E6IT03_06 <dbl> NA, 1, 2, 2, 1, NA, 1, 2, 1, 2, 1, NA, 1, 2, NA, 1, 2, 2, 2,…
    ## $ E6IT04    <dbl> 1, 1, 1, 1, 1, NA, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1,…
    ## $ E6IT05    <dbl> 2, 2, 2, 2, 2, NA, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2,…
    ## $ E6IT05A   <dbl> NA, NA, NA, NA, 6, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ E6IT06    <dbl> 1, 1, 1, 1, 1, NA, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1,…
    ## $ E6IT06A   <dbl> 99, 99, 99, 99, 99, NA, 99, 15, 99, 99, 99, 99, 99, 99, 99, …
    ## $ E6IT07    <dbl> NA, 1, 1, 1, 1, NA, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
    ## $ E6IT08    <dbl> NA, 1, 1, 1, 1, NA, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
    ## $ E6IT09    <dbl> 99, 5, 2, 7, 3, NA, 3, 6, 2, 7, 3, 3, 7, 2, 5, 2, 5, 1, 3, 3…
    ## $ E6IT10    <dbl> 2, 2, 1, 2, 2, NA, 2, 4, 3, 2, 3, 4, 3, 2, 5, 2, 3, 1, 5, 3,…
    ## $ E6IT11_01 <dbl> 4, 2, 4, 3, 4, NA, 3, 4, 3, 4, 4, 3, 4, 3, 3, 4, 3, NA, 4, 1…
    ## $ E6IT11_02 <dbl> NA, 2, 4, 3, 3, NA, 4, 3, 3, 3, 4, 4, 4, 3, 4, 3, 4, NA, 4, …
    ## $ E6IT11_03 <dbl> NA, 3, 4, 3, 3, NA, 3, 4, 3, 4, 4, 3, 4, 3, 3, 4, 4, NA, 4, …
    ## $ E6IT11_04 <dbl> NA, 1, 3, 3, 3, NA, 3, 3, 4, 3, 3, 2, 3, 2, 4, 3, 2, NA, 4, …
    ## $ E6IT12_01 <dbl> NA, 2, 2, 2, 2, NA, 1, 1, 1, 1, 2, 2, 2, 2, 2, 1, 1, NA, 2, …
    ## $ E6IT12_02 <dbl> 1, 2, 2, 2, 2, NA, 1, 2, 1, 1, 2, 2, 2, 2, 1, 1, 1, NA, 2, 2…
    ## $ E6IT12_03 <dbl> NA, 2, 2, 2, 2, NA, 2, 1, 1, 2, 2, 2, 2, 2, 2, 2, 2, NA, 2, …
    ## $ E6IT12_04 <dbl> NA, 1, 2, 2, 1, NA, 1, 2, 1, 1, 1, 1, 1, 1, 1, 1, 1, NA, 1, …
    ## $ E6IT12_05 <dbl> NA, 1, 1, 1, 1, NA, 1, 1, 2, 2, 1, 1, 1, 1, 1, 1, 1, NA, 1, …
    ## $ E6IT12_06 <dbl> NA, 2, 2, 2, 2, NA, 2, 1, 2, 2, 2, 2, 2, 2, 1, 2, 1, NA, 2, …
    ## $ E6IT13_01 <dbl> 1, 2, 1, 2, 1, NA, 4, 2, 2, 1, 1, 1, 1, 1, 1, 2, 1, NA, 1, 2…
    ## $ E6IT13_02 <dbl> NA, 2, 1, 2, 1, NA, 2, 1, 2, 1, NA, 2, 2, 1, 2, 1, 1, NA, 1,…
    ## $ E6IT13_03 <dbl> NA, 2, 1, 2, 1, NA, 1, 3, 3, 1, 2, 2, 2, 2, 3, 1, 2, NA, 1, …
    ## $ E6IT13_04 <dbl> NA, 4, 1, 3, 1, NA, 3, 3, 3, 2, 2, 1, 3, 3, 2, 2, 2, NA, 2, …
    ## $ E6IT13_05 <dbl> NA, 2, 1, 2, 1, NA, 1, 3, 1, 1, 1, 1, 1, 1, 1, 1, 1, NA, 1, …
    ## $ E6IT13_06 <dbl> NA, 1, 1, 1, 1, NA, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, NA, 1, …
    ## $ E6IT13_07 <dbl> NA, 2, 1, 2, 1, NA, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, NA, 1, …
    ## $ E6IT13_08 <dbl> NA, 2, 1, 2, 1, NA, 1, 3, 1, 1, 1, 1, 1, 1, 1, 1, 1, NA, 1, …
    ## $ E6IT14    <dbl> 2, 1, 1, 1, 1, NA, 1, 1, 2, 1, 1, 2, 1, 2, 2, 2, 1, 1, 1, 2,…
    ## $ E6IT15    <dbl> 1, 4, 5, 4, 6, NA, 2, 5, 2, 6, 6, 2, 5, 6, 2, 2, 5, 5, 5, 5,…
    ## $ E6IT16    <dbl> 2, 3, 1, 3, 2, NA, 1, 2, 2, 1, 1, 1, 2, 3, 3, 1, 1, 1, 1, 1,…
    ## $ E6IT17    <dbl> 5, 3, 1, 1, 3, NA, 1, 6, 6, 1, 1, 1, 1, 3, 2, 4, 4, 5, 1, 5,…
    ## $ E6IT18    <dbl> 5, 1, 1, 4, 6, NA, 3, 6, 3, 1, 2, 1, 1, 3, 2, 1, 1, 5, 1, 6,…
    ## $ E6IT19_01 <dbl> 2, 2, 2, 2, 1, NA, 2, 2, 1, 2, 1, 2, 2, 1, 2, 2, 2, NA, 2, 2…
    ## $ E6IT19_02 <dbl> NA, 2, 2, 2, 1, NA, 2, 1, 2, 1, 1, 2, 2, 1, 2, 1, 2, NA, 1, …
    ## $ E6IT19_03 <dbl> NA, 3, 2, 1, 1, NA, 2, 2, 2, 1, 1, 2, 2, 1, 2, 1, 2, NA, 1, …
    ## $ E6IT20_01 <dbl> 2, 1, 1, 1, 1, NA, 2, 3, 2, 2, 3, 3, 3, 1, 3, 1, 2, NA, 2, 1…
    ## $ E6IT20_02 <dbl> NA, 1, 2, 2, 1, NA, 3, 3, 2, 4, 3, 2, 3, 3, 2, 2, 3, NA, 2, …
    ## $ E6IT20_03 <dbl> NA, 2, 2, 3, 1, NA, 1, 3, 1, 4, 3, 2, 4, 2, 3, 2, 3, NA, 2, …
    ## $ E6IT20_04 <dbl> NA, 1, 1, 2, 1, NA, 2, 2, 3, 4, 3, 2, 2, 2, 1, 2, 2, NA, 2, …
    ## $ E6IT20_05 <dbl> NA, 1, 1, 2, 1, NA, 1, 2, 4, 2, 4, 2, 1, 2, NA, 3, 2, NA, 2,…
    ## $ E6IT20_06 <dbl> NA, 2, 2, 2, 2, NA, 2, 1, 1, 1, 1, 2, 1, 1, 1, 1, 1, NA, 1, …
    ## $ E6IT20_07 <dbl> NA, 1, 1, 2, 1, NA, 1, 1, 1, 2, 3, 1, 2, 2, 2, 1, 4, NA, 2, …
    ## $ E6IT21_01 <dbl> 2, 4, 4, 4, 3, NA, 2, 2, 3, 4, 2, 3, 4, 2, 3, 2, 3, NA, 2, 4…
    ## $ E6IT21_02 <dbl> NA, 3, 1, 3, 3, NA, 1, 1, 4, 3, 2, 2, 2, 2, 2, 2, 2, NA, 3, …
    ## $ E6IT21_03 <dbl> NA, 2, 2, 4, 2, NA, 2, 2, 3, 2, 1, 2, 3, 4, 3, 2, 3, NA, 3, …
    ## $ E6IT21_04 <dbl> NA, 4, 3, 2, 2, NA, 2, 1, 3, 3, 2, 2, 3, 3, 2, 1, 3, NA, 2, …
    ## $ E6IT21_05 <dbl> NA, 4, 2, 2, 1, NA, 1, 2, 2, 1, 2, 3, 1, 3, 1, 2, 2, NA, 3, …
    ## $ E6IT22_01 <dbl> 2, 2, 4, 4, 3, NA, 4, 2, 4, 4, 4, 3, 3, 4, 1, 3, 4, NA, 4, 3…
    ## $ E6IT22_02 <dbl> NA, 1, 2, 2, 3, NA, 2, 3, 4, 3, 3, 3, 3, 4, 1, 2, 3, NA, 4, …
    ## $ E6IT22_03 <dbl> NA, 1, 3, 3, 3, NA, 4, 3, 3, 4, 3, 3, 2, 3, 1, 2, 3, NA, 3, …
    ## $ E6IT22_04 <dbl> NA, 1, 2, 3, 3, NA, 3, 3, 3, 3, 3, 3, 2, 4, 3, 2, 2, NA, 4, …
    ## $ E6IT22_05 <dbl> NA, 1, 2, 4, 3, NA, 4, 2, 4, 4, 3, 3, 4, 4, 3, 3, 3, NA, 3, …
    ## $ E6IT22_06 <dbl> NA, 1, 3, 4, 3, NA, 1, 3, 3, 3, 3, 2, 3, 4, 3, 2, 4, NA, 4, …
    ## $ E6IT22_07 <dbl> NA, 1, 1, 3, 1, NA, 1, 3, 1, 1, 2, 2, 3, 1, 3, 1, 1, NA, 3, …
    ## $ E6IT22_08 <dbl> NA, 1, 2, 4, 3, NA, 4, 3, 4, 3, 3, 3, 3, 4, 3, 3, 3, NA, 4, …
    ## $ E6IT22_09 <dbl> NA, 2, 2, 4, 2, NA, 4, 4, 4, 2, 3, 2, 2, 4, 2, 2, 2, NA, 3, …
    ## $ E6IT22_10 <dbl> NA, 1, 2, 2, 1, NA, 3, 3, 4, 3, 1, 1, 3, 4, 1, 1, 1, NA, 4, …
    ## $ E6IT22_11 <dbl> NA, 4, 2, 3, 2, NA, 3, 4, 3, 3, 3, 2, 1, 4, 3, 2, 3, NA, 3, …
    ## $ E6IT23_01 <dbl> 2, 4, 4, 2, 2, NA, 3, 2, 3, 3, 3, 4, 4, 4, 3, 1, 2, NA, 3, 4…
    ## $ E6IT23_02 <dbl> NA, 2, 2, 3, 3, NA, 4, 2, 2, 3, 3, 4, 4, 4, 2, 2, 3, NA, 3, …
    ## $ E6IT23_03 <dbl> NA, 4, 2, 4, 2, NA, 3, 3, 3, 2, 3, 1, 3, 3, 1, 2, 3, NA, 3, …
    ## $ E6IT23_04 <dbl> NA, 1, 1, 2, 1, NA, 1, 2, 1, 4, 1, 1, 3, 1, 2, 1, 2, NA, 2, …
    ## $ E6IT24_01 <dbl> 2, 2, 3, 4, 3, NA, 4, 4, 4, 4, 3, 1, 3, 3, 3, 3, 4, NA, 4, 4…
    ## $ E6IT24_02 <dbl> NA, 3, 3, 4, 3, NA, 4, 4, 4, 3, 4, 1, 3, 4, 1, 3, 4, NA, 4, …
    ## $ E6IT24_03 <dbl> NA, 2, 4, 4, 3, NA, 4, 4, 4, 4, 4, 3, 4, 3, 1, 3, 3, NA, 4, …
    ## $ E6IT24_04 <dbl> NA, 4, 3, 4, 3, NA, 4, 3, 3, 3, 4, 1, 4, 1, 2, 3, 4, NA, 4, …
    ## $ E6IT24_05 <dbl> NA, 4, 3, 1, 1, NA, 2, 1, 2, 4, 2, 1, 3, 1, 3, 2, 2, NA, 4, …
    ## $ E6IT24_06 <dbl> NA, 2, 3, 1, 3, NA, 1, 1, 2, 3, 2, 2, 1, 1, 1, 1, 1, NA, 4, …
    ## $ E6IT24_07 <dbl> NA, 4, 3, 1, 1, NA, 2, 2, 1, 4, 2, 1, 2, 1, 4, 1, 2, NA, 2, …
    ## $ E6IT25_01 <dbl> 1, 4, 2, 3, 2, NA, 3, 1, 1, 4, 1, 1, 3, 1, 1, 1, 1, NA, 4, 4…
    ## $ E6IT25_02 <dbl> NA, 4, 1, 3, 1, NA, 2, 2, 1, 3, 1, 1, 2, 1, 2, 1, 1, NA, 4, …
    ## $ E6IT25_03 <dbl> NA, 4, 2, 3, 2, NA, 2, 2, 1, 4, 1, 2, 3, 1, 3, 2, 1, NA, 4, …
    ## $ E6IT25_04 <dbl> NA, 4, 2, 2, 1, NA, 1, 3, 2, 3, 1, 2, 2, 1, NA, 1, 1, NA, 4,…
    ## $ E6IT25_05 <dbl> NA, 4, 3, 1, 2, NA, 3, 3, 2, 3, 1, 2, 2, 1, NA, 1, 1, NA, 3,…
    ## $ E6IT26_01 <dbl> 2, 1, 2, 3, 1, NA, 1, 2, 1, 4, 3, 1, 2, 1, 3, 1, 2, NA, 4, 3…
    ## $ E6IT26_02 <dbl> NA, 1, 2, 2, 1, NA, 1, 3, 1, 1, 3, 1, 1, 1, 3, 1, 1, NA, 4, …
    ## $ E6IT26_03 <dbl> NA, 1, 1, 4, 2, NA, 1, 4, 1, 2, 2, 2, 1, 1, 2, 1, 1, NA, 4, …
    ## $ E6IT26_04 <dbl> NA, 1, 2, 4, 2, NA, 1, 3, 1, 3, 3, 2, 2, 1, 3, 1, 1, NA, 4, …
    ## $ E6IT26_05 <dbl> NA, 1, 2, 4, 1, NA, 1, 3, 1, 2, 3, 2, 1, 1, 3, 1, 1, NA, 3, …
    ## $ E6IT26_06 <dbl> NA, 1, 2, 4, 2, NA, 1, 3, 1, 2, 2, 2, 3, 1, 1, 2, 2, NA, 4, …
    ## $ E6IT26_07 <dbl> NA, 1, 2, 4, 2, NA, 1, 2, 3, 3, 3, 2, 2, 1, 3, 1, 3, NA, 3, …
    ## $ E6IT26_08 <dbl> NA, 1, 2, 4, 1, NA, 2, 2, 1, 4, 3, 2, 4, 1, 3, 1, 1, NA, 4, …
    ## $ E6IT26_09 <dbl> NA, 4, 2, 4, 1, NA, 2, 2, 1, 3, 3, 2, 1, 1, 2, 1, 1, NA, 4, …
    ## $ E6IT26_10 <dbl> NA, NA, 1, 4, 1, NA, 1, 3, 1, 4, 2, 2, 2, 1, NA, 1, 1, NA, 3…
    ## $ E6IT26_11 <dbl> NA, 1, 2, 4, 2, NA, 1, 4, 3, 2, 2, 2, 3, 2, NA, 2, 1, NA, 3,…
    ## $ E6IT27_01 <dbl> 2, 1, 4, 4, 2, NA, 2, 2, 4, 2, 4, 3, 2, 3, 3, 1, 2, NA, 4, 4…
    ## $ E6IT27_02 <dbl> NA, 1, 3, 3, 2, NA, 3, 4, 1, 3, 3, 2, 2, 1, 2, 2, 1, NA, 4, …
    ## $ E6IT27_03 <dbl> NA, 1, 2, 2, 1, NA, 2, 4, 1, NA, 3, 1, 2, 1, 3, 1, 1, NA, 4,…
    ## $ E6IT27_04 <dbl> NA, 1, 1, 1, 1, NA, 1, 3, 1, 1, 1, 1, 2, 1, 1, 1, 1, NA, 4, …
    ## $ E6IT28_01 <dbl> 2, 2, 2, 1, 2, NA, 4, 1, 3, 4, 1, 2, 2, 1, 3, 1, 2, NA, 4, 4…
    ## $ E6IT28_02 <dbl> NA, 2, 1, 3, 2, NA, 2, 2, 3, 3, 1, 2, 2, 1, 3, 1, 2, NA, 4, …
    ## $ E6IT28_03 <dbl> NA, 1, 2, 3, 2, NA, 3, 2, 3, 2, 1, 2, 2, 1, 2, 2, 1, NA, 4, …
    ## $ E6IT28_04 <dbl> NA, 1, 3, 3, 2, NA, 2, 3, 3, 3, 1, 2, 2, 1, 3, 1, 1, NA, 4, …
    ## $ E6IT28_05 <dbl> NA, 1, 3, 2, 3, NA, 2, 3, 3, 4, 1, 2, 3, 1, NA, 2, 1, NA, 4,…
    ## $ E6IT29_01 <dbl> 2, 4, 2, 4, 2, NA, 3, 2, 4, 4, 4, 2, 3, 4, 1, 2, 4, NA, 4, 4…
    ## $ E6IT29_02 <dbl> NA, 4, 2, 4, 2, NA, 3, 3, 4, 3, 3, 2, 2, 4, 3, 2, 4, NA, 4, …
    ## $ E6IT29_03 <dbl> NA, 4, 3, 4, 2, NA, 3, 2, 4, 4, 3, 2, 4, 4, 2, 2, 4, NA, 4, …
    ## $ E6IT29_04 <dbl> NA, 4, 3, 4, 2, NA, 3, 3, 4, 3, 3, 2, 3, 4, 1, 2, 4, NA, 4, …
    ## $ E6IT29_05 <dbl> NA, 4, 2, 4, 2, NA, 3, 2, 4, 4, 4, 2, 3, 4, 3, 2, 1, NA, 4, …
    ## $ E6IT29_06 <dbl> NA, 4, 3, 4, 2, NA, 3, 2, 4, 2, 4, 3, 4, 4, 2, 2, 3, NA, 4, …
    ## $ E6IT29_07 <dbl> NA, 4, 3, 4, 2, NA, 3, 2, 4, 3, 3, 2, 3, 4, 1, 2, 2, NA, 4, …
    ## $ E6IT29_08 <dbl> NA, 4, 3, 4, 2, NA, 3, 3, 4, 4, 4, 3, 1, 4, 4, 3, 2, NA, 4, …
    ## $ E6IT29_09 <dbl> NA, 2, 3, 4, 1, NA, 3, 3, 4, 3, 3, 3, 3, 4, 2, 3, 1, NA, 4, …
    ## $ E6IT29_10 <dbl> NA, 2, 1, 4, 1, NA, 2, 2, 4, 3, 2, 2, 3, 1, 1, 2, 1, NA, 4, …
    ## $ E6IT29_11 <dbl> NA, 4, 3, 4, 2, NA, 4, 4, 4, 3, 4, 3, 3, 4, 3, 3, 4, NA, 4, …
    ## $ E6IT30_01 <dbl> 3, 4, 2, 4, 3, NA, 2, 2, NA, 3, 4, 3, 2, 4, 1, 2, 4, NA, 4, …
    ## $ E6IT30_02 <dbl> NA, 4, 2, 4, 2, NA, 3, 2, NA, 2, 4, 2, 3, 4, 2, 2, 3, NA, 4,…
    ## $ E6IT30_03 <dbl> NA, 4, 2, 4, 2, NA, 2, 2, NA, 3, 3, 1, 4, 4, 3, 3, 2, NA, 4,…
    ## $ E6IT30_04 <dbl> NA, 1, 1, 2, 1, NA, 1, 3, NA, 1, 1, 1, 3, 1, 1, 1, 2, NA, 4,…
    ## $ E6IT31    <dbl> NA, 5, 4, 3, 3, NA, 1, 5, 6, 6, 4, 3, 5, 3, 5, 4, 5, 2, 2, 5…
    ## $ E6IT32    <dbl> 3, 3, 2, 3, 3, NA, 2, 4, 2, 2, 2, 3, 4, 3, 3, 4, 3, 4, 4, 4,…
    ## $ E6IT33_01 <dbl> 2, 1, 2, 2, 2, NA, 4, 2, 2, 4, 3, 2, 4, 3, 2, 2, 2, NA, 4, 4…
    ## $ E6IT33_02 <dbl> NA, 4, 4, 2, 4, NA, 3, 3, NA, 4, 4, 3, 3, 2, 3, 2, 2, NA, 4,…
    ## $ E6IT33_03 <dbl> NA, 4, 2, 2, 4, NA, 2, 3, 3, 4, 4, 2, 3, 4, 4, 3, 4, NA, 4, …
    ## $ E6IT33_04 <dbl> NA, 3, 2, 2, 3, NA, 4, 3, 4, 3, 4, 2, 4, 3, 1, 3, 4, NA, 4, …
    ## $ E6IT34    <dbl> 1, 1, 2, 1, 1, NA, 1, NA, 1, 1, 1, 1, NA, 3, 1, 1, 3, 1, NA,…
    ## $ E6IT34A   <dbl> NA, NA, 2, NA, NA, NA, NA, NA, NA, NA, NA, NA, 1, NA, NA, NA…
    ## $ E6IT34B   <dbl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, 1, 3, NA, NA…
    ## $ E6IT35    <dbl> 2, NA, 2, 2, NA, NA, 2, 1, 1, 2, NA, 1, 1, 1, 1, 3, 1, 2, 3,…
    ## $ E6IT36_01 <dbl> 1, 2, 2, 2, 2, NA, 2, 2, NA, NA, 2, 2, 2, NA, 2, 2, 2, NA, 2…
    ## $ E6IT36_02 <dbl> NA, 1, 1, 1, 1, NA, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
    ## $ BRR1      <dbl> 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, …
    ## $ BRR2      <dbl> 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, …
    ## $ BRR3      <dbl> 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, …
    ## $ BRR4      <dbl> 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, …
    ## $ BRR5      <dbl> 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, …
    ## $ BRR6      <dbl> 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, …
    ## $ BRR7      <dbl> 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, …
    ## $ BRR8      <dbl> 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, …
    ## $ BRR9      <dbl> 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, …
    ## $ BRR10     <dbl> 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, …
    ## $ BRR11     <dbl> 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, …
    ## $ BRR12     <dbl> 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, …
    ## $ BRR13     <dbl> 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, …
    ## $ BRR14     <dbl> 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, …
    ## $ BRR15     <dbl> 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, …
    ## $ BRR16     <dbl> 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, …
    ## $ BRR17     <dbl> 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, …
    ## $ BRR18     <dbl> 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, …
    ## $ BRR19     <dbl> 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, …
    ## $ BRR20     <dbl> 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, …
    ## $ BRR21     <dbl> 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, …
    ## $ BRR22     <dbl> 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, …
    ## $ BRR23     <dbl> 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, …
    ## $ BRR24     <dbl> 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, …
    ## $ BRR25     <dbl> 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, …
    ## $ BRR26     <dbl> 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, …
    ## $ BRR27     <dbl> 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, …
    ## $ BRR28     <dbl> 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, …
    ## $ BRR29     <dbl> 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, …
    ## $ BRR30     <dbl> 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, …
    ## $ BRR31     <dbl> 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, …
    ## $ BRR32     <dbl> 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, …
    ## $ BRR33     <dbl> 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, …
    ## $ BRR34     <dbl> 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, …
    ## $ BRR35     <dbl> 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, …
    ## $ BRR36     <dbl> 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, …
    ## $ BRR37     <dbl> 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, …
    ## $ BRR38     <dbl> 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, …
    ## $ BRR39     <dbl> 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, …
    ## $ BRR40     <dbl> 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, …
    ## $ BRR41     <dbl> 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, …
    ## $ BRR42     <dbl> 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, …
    ## $ BRR43     <dbl> 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, …
    ## $ BRR44     <dbl> 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, …
    ## $ BRR45     <dbl> 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, …
    ## $ BRR46     <dbl> 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, …
    ## $ BRR47     <dbl> 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, …
    ## $ BRR48     <dbl> 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, …
    ## $ BRR49     <dbl> 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, …
    ## $ BRR50     <dbl> 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, …
    ## $ BRR51     <dbl> 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, …
    ## $ BRR52     <dbl> 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, …
    ## $ BRR53     <dbl> 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, …
    ## $ BRR54     <dbl> 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, …
    ## $ BRR55     <dbl> 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, …
    ## $ BRR56     <dbl> 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, …
    ## $ BRR57     <dbl> 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, …
    ## $ BRR58     <dbl> 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, …
    ## $ BRR59     <dbl> 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, …
    ## $ BRR60     <dbl> 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, …
    ## $ BRR61     <dbl> 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, …
    ## $ BRR62     <dbl> 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, …
    ## $ BRR63     <dbl> 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, …
    ## $ BRR64     <dbl> 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, …
    ## $ BRR65     <dbl> 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, …
    ## $ BRR66     <dbl> 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, …
    ## $ BRR67     <dbl> 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, …
    ## $ BRR68     <dbl> 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, …
    ## $ BRR69     <dbl> 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, …
    ## $ BRR70     <dbl> 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, …
    ## $ BRR71     <dbl> 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, …
    ## $ BRR72     <dbl> 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, …
    ## $ BRR73     <dbl> 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, …
    ## $ BRR74     <dbl> 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, …
    ## $ BRR75     <dbl> 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, …
    ## $ BRR76     <dbl> 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, …
    ## $ BRR77     <dbl> 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, …
    ## $ BRR78     <dbl> 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, …
    ## $ BRR79     <dbl> 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, …
    ## $ BRR80     <dbl> 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, …
    ## $ BRR81     <dbl> 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, …
    ## $ BRR82     <dbl> 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, …
    ## $ BRR83     <dbl> 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, …
    ## $ BRR84     <dbl> 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, …
    ## $ BRR85     <dbl> 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, …
    ## $ BRR86     <dbl> 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, …
    ## $ BRR87     <dbl> 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, …
    ## $ BRR88     <dbl> 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, …
    ## $ BRR89     <dbl> 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, …
    ## $ BRR90     <dbl> 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, …
    ## $ BRR91     <dbl> 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, …
    ## $ BRR92     <dbl> 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, …
    ## $ BRR93     <dbl> 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, …
    ## $ BRR94     <dbl> 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, …
    ## $ BRR95     <dbl> 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, …
    ## $ BRR96     <dbl> 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, …
    ## $ BRR97     <dbl> 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, …
    ## $ BRR98     <dbl> 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, 316, …
    ## $ BRR99     <dbl> 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, …
    ## $ BRR100    <dbl> 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, 105, …
    ## $ MAT_1     <dbl> 588, 750, 687, 792, 703, 683, 661, 697, 726, 659, 795, 578, …
    ## $ MAT_2     <dbl> 635, 699, 688, 769, 714, 665, 715, 702, 672, 646, 787, 624, …
    ## $ MAT_3     <dbl> 630, 668, 710, 763, 668, 721, 678, 681, 740, 660, 730, 606, …
    ## $ MAT_4     <dbl> 499, 644, 712, 763, 730, 646, 704, 680, 696, 670, 704, 632, …
    ## $ MAT_5     <dbl> 612, 643, 638, 800, 668, 719, 660, 680, 678, 623, 797, 570, …
    ## $ MAT_L1    <chr> "I", "II", "II", "III", "II", "I", "I", "II", "II", "I", "II…
    ## $ MAT_L2    <chr> "I", "II", "II", "II", "II", "I", "II", "II", "I", "I", "II"…
    ## $ MAT_L3    <chr> "I", "I", "II", "II", "I", "II", "I", "I", "II", "I", "II", …
    ## $ MAT_L4    <chr> "I", "I", "II", "II", "II", "I", "II", "I", "II", "I", "II",…
    ## $ MAT_L5    <chr> "I", "I", "I", "III", "I", "II", "I", "I", "I", "I", "III", …
    ## $ LAN_1     <dbl> 716, 846, 710, 770, 772, 501, 650, 671, 686, 668, 788, 645, …
    ## $ LAN_2     <dbl> 655, 827, 724, 671, 788, 679, 603, 613, 664, 630, 778, 562, …
    ## $ LAN_3     <dbl> 684, 799, 643, 654, 741, 560, 644, 662, 650, 670, 835, 676, …
    ## $ LAN_4     <dbl> 645, 812, 656, 707, 773, 531, 639, 633, 639, 587, 802, 617, …
    ## $ LAN_5     <dbl> 681, 852, 690, 784, 780, 508, 606, 594, 626, 604, 740, 646, …
    ## $ LAN_L1    <chr> "II", "IV", "II", "III", "III", "I", "II", "II", "II", "II",…
    ## $ LAN_L2    <chr> "II", "IV", "II", "II", "III", "II", "I", "II", "II", "II", …
    ## $ LAN_L3    <chr> "II", "III", "II", "II", "II", "I", "II", "II", "II", "II", …
    ## $ LAN_L4    <chr> "II", "IV", "II", "II", "III", "I", "II", "II", "II", "I", "…
    ## $ LAN_L5    <chr> "II", "IV", "II", "III", "III", "I", "I", "I", "II", "I", "I…
    ## $ SCI_1     <dbl> 642, 786, 617, 788, 717, 632, 676, 627, 602, 685, 886, 585, …
    ## $ SCI_2     <dbl> 618, 782, 692, 754, 801, 622, 636, 666, 621, 670, 808, 618, …
    ## $ SCI_3     <dbl> 536, 741, 589, 767, 718, 627, 613, 691, 552, 702, 842, 556, …
    ## $ SCI_4     <dbl> 596, 731, 685, 766, 696, 606, 656, 654, 595, 719, 852, 621, …
    ## $ SCI_5     <dbl> 630, 721, 637, 782, 741, 657, 648, 627, 597, 578, 852, 644, …
    ## $ SCI_L1    <chr> "I", "III", "I", "III", "II", "I", "II", "I", "I", "II", "IV…
    ## $ SCI_L2    <chr> "I", "III", "II", "II", "III", "I", "I", "I", "I", "II", "II…
    ## $ SCI_L3    <chr> "I", "II", "I", "II", "II", "I", "I", "II", "I", "II", "III"…
    ## $ SCI_L4    <chr> "I", "II", "II", "II", "II", "I", "I", "I", "I", "II", "III"…
    ## $ SCI_L5    <chr> "I", "II", "I", "III", "II", "I", "I", "I", "I", "I", "III",…
    ## $ SEX       <dbl> 0, 0, 0, 0, 0, 1, 1, 0, 0, 1, 0, 1, 1, 0, 1, 0, 0, 1, 0, 0, …
    ## $ DEP       <dbl> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, …
    ## $ RURAL     <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ EDU       <dbl> 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, …
    ## $ SPESC     <dbl> 0.647, -1.882, 0.696, -0.781, -0.232, NA, -0.321, 0.151, -0.…
    ## $ VIOES     <dbl> -0.660, 1.407, -1.272, 1.321, -1.272, NA, 0.664, 1.476, 0.71…
    ## $ ASISP     <dbl> 1.02, 2.39, 1.91, 1.26, -0.85, NA, 1.91, 1.18, 1.07, 0.42, -…
    ## $ CLBIE     <dbl> -0.77, -1.92, -1.59, -0.85, -2.40, NA, -1.23, -0.36, -0.54, …
    ## $ DISMA     <dbl> -0.14, 1.29, 0.43, 1.38, 0.51, NA, -0.37, -0.75, 1.34, 1.02,…
    ## $ AAEMA     <dbl> -1.042, -2.449, -0.965, 0.374, -0.404, NA, -0.022, -0.459, 0…
    ## $ ORGMA     <dbl> -0.894, -0.159, -0.675, -0.260, -0.780, NA, 0.415, -1.073, -…
    ## $ EFMAT     <dbl> -1.13, -1.04, 0.14, 1.45, -0.18, NA, 1.45, 1.45, 1.45, 0.84,…
    ## $ DISCI     <dbl> -0.951, 2.431, -0.234, 0.917, -0.564, NA, 0.068, 0.075, -0.9…
    ## $ AAECI     <dbl> -1.00, -2.96, -1.42, 0.62, -1.98, NA, -2.57, -0.38, -2.37, -…
    ## $ ORGCI     <dbl> -0.875, -2.500, -0.079, -0.079, -1.484, NA, -0.681, 0.442, -…
    ## $ DISLA     <dbl> 0.046, -0.517, 0.059, 0.660, 0.122, NA, 0.860, 0.100, 1.117,…
    ## $ AAELA     <dbl> -1.029, 1.696, -0.677, 1.696, -1.319, NA, -0.154, -0.755, 1.…
    ## $ ORGLA     <dbl> -0.19, 1.33, -1.20, 1.33, -0.98, NA, -0.63, -1.20, NA, -0.78…
    ## $ INVAP     <dbl> -0.197, -0.071, -0.667, -1.207, 0.139, NA, -0.290, -0.570, -…
    ## $ ISECF     <dbl> 0.204, -0.430, -2.443, -1.480, 0.020, -0.994, -1.229, -1.495…
    ## $ AURES     <dbl> 33, 41, 52, 48, 41, 43, 55, 61, 49, 49, 51, 44, 51, NA, 34, …
    ## $ EMPAT     <dbl> 43, 39, 43, 52, 42, 42, 57, 54, 52, 46, 42, 38, 49, NA, 39, …
    ## $ APDIV     <dbl> 37, 46, 62, 46, 47, 46, 52, 62, 47, 48, 47, 36, 47, NA, 34, …
    ## $ EDAD      <dbl> 13, 14, 12, 14, 12, NA, 11, 15, 14, 10, 12, 11, 11, 14, 15, …
    ## $ PREE      <dbl> 0, 1, 1, 1, 1, NA, 1, 1, 0, 1, 1, 0, 1, 0, 0, 0, 1, 1, 1, 0,…
    ## $ REPC      <dbl> 1, 1, 0, 1, 1, NA, 0, 1, 1, 0, 0, 0, 1, 1, 1, 0, 0, 0, 0, 0,…
    ## $ AUSE      <dbl> 1, 1, 0, 0, 1, NA, 0, NA, NA, 0, 0, 0, 0, 1, 0, 1, 1, 1, 0, …
    ## $ ATRE      <dbl> 1, 0, 0, 1, NA, NA, 1, NA, 1, 0, 0, 0, 0, 1, 0, 0, 0, 1, 0, …
    ## $ LIBH      <dbl> 1, 1, 0, 1, 1, NA, 1, 3, 2, 1, 2, 3, 2, 1, 4, 1, 2, 0, 4, 2,…
    ## $ TSTU      <dbl> NA, 1, 1, 1, 1, NA, 0, 1, NA, NA, 1, 1, 1, 1, 1, 1, 1, 0, 0,…
    ## $ INDI      <dbl> 0, 0, 0, 0, 0, NA, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,…
    ## $ IMMI      <dbl> 0, 0, 0, 0, 0, NA, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,…
    ## $ repws001  <dbl> 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, …
    ## $ repws002  <dbl> 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, …
    ## $ repws003  <dbl> 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, …
    ## $ repws004  <dbl> 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, …
    ## $ repws005  <dbl> 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, …
    ## $ repws006  <dbl> 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, …
    ## $ repws007  <dbl> 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, …
    ## $ repws008  <dbl> 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, …
    ## $ repws009  <dbl> 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, …
    ## $ repws010  <dbl> 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, …
    ## $ repws011  <dbl> 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, …
    ## $ repws012  <dbl> 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, …
    ## $ repws013  <dbl> 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, …
    ## $ repws014  <dbl> 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, …
    ## $ repws015  <dbl> 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, …
    ## $ repws016  <dbl> 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, …
    ## $ repws017  <dbl> 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, …
    ## $ repws018  <dbl> 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, …
    ## $ repws019  <dbl> 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, …
    ## $ repws020  <dbl> 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, …
    ## $ repws021  <dbl> 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, …
    ## $ repws022  <dbl> 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, …
    ## $ repws023  <dbl> 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, …
    ## $ repws024  <dbl> 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, …
    ## $ repws025  <dbl> 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, …
    ## $ repws026  <dbl> 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, …
    ## $ repws027  <dbl> 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, …
    ## $ repws028  <dbl> 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, …
    ## $ repws029  <dbl> 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, …
    ## $ repws030  <dbl> 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, …
    ## $ repws031  <dbl> 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, …
    ## $ repws032  <dbl> 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, …
    ## $ repws033  <dbl> 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, …
    ## $ repws034  <dbl> 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, …
    ## $ repws035  <dbl> 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, …
    ## $ repws036  <dbl> 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, …
    ## $ repws037  <dbl> 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, …
    ## $ repws038  <dbl> 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, …
    ## $ repws039  <dbl> 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, …
    ## $ repws040  <dbl> 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, …
    ## $ repws041  <dbl> 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, …
    ## $ repws042  <dbl> 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, …
    ## $ repws043  <dbl> 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, …
    ## $ repws044  <dbl> 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, …
    ## $ repws045  <dbl> 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, …
    ## $ repws046  <dbl> 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, …
    ## $ repws047  <dbl> 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, …
    ## $ repws048  <dbl> 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, …
    ## $ repws049  <dbl> 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, …
    ## $ repws050  <dbl> 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, …
    ## $ repws051  <dbl> 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, …
    ## $ repws052  <dbl> 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, …
    ## $ repws053  <dbl> 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, …
    ## $ repws054  <dbl> 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, …
    ## $ repws055  <dbl> 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, …
    ## $ repws056  <dbl> 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, …
    ## $ repws057  <dbl> 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, …
    ## $ repws058  <dbl> 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, …
    ## $ repws059  <dbl> 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, …
    ## $ repws060  <dbl> 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, …
    ## $ repws061  <dbl> 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, …
    ## $ repws062  <dbl> 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, …
    ## $ repws063  <dbl> 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, …
    ## $ repws064  <dbl> 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, …
    ## $ repws065  <dbl> 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, …
    ## $ repws066  <dbl> 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, …
    ## $ repws067  <dbl> 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, …
    ## $ repws068  <dbl> 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, …
    ## $ repws069  <dbl> 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, …
    ## $ repws070  <dbl> 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, …
    ## $ repws071  <dbl> 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, …
    ## $ repws072  <dbl> 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, …
    ## $ repws073  <dbl> 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, …
    ## $ repws074  <dbl> 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, …
    ## $ repws075  <dbl> 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, …
    ## $ repws076  <dbl> 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, …
    ## $ repws077  <dbl> 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, …
    ## $ repws078  <dbl> 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, …
    ## $ repws079  <dbl> 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, …
    ## $ repws080  <dbl> 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, …
    ## $ repws081  <dbl> 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, …
    ## $ repws082  <dbl> 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, …
    ## $ repws083  <dbl> 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, …
    ## $ repws084  <dbl> 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, …
    ## $ repws085  <dbl> 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, …
    ## $ repws086  <dbl> 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, …
    ## $ repws087  <dbl> 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, …
    ## $ repws088  <dbl> 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, …
    ## $ repws089  <dbl> 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, …
    ## $ repws090  <dbl> 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, …
    ## $ repws091  <dbl> 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, …
    ## $ repws092  <dbl> 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, …
    ## $ repws093  <dbl> 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, …
    ## $ repws094  <dbl> 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, …
    ## $ repws095  <dbl> 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, …
    ## $ repws096  <dbl> 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, …
    ## $ repws097  <dbl> 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, …
    ## $ repws098  <dbl> 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, 0.37, …
    ## $ repws099  <dbl> 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, …
    ## $ repws100  <dbl> 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, 0.12, …
    ## $ id_s      <dbl> 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, …
    ## $ id_j      <dbl> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, …
    ## $ id_i      <int> 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 1…
    ## $ all       <dbl> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, …
    ## $ lan_min_1 <dbl> 0, 1, 0, 1, 1, 0, 0, 0, 0, 0, 1, 0, 0, 1, 0, 0, 0, 0, 0, 0, …
    ## $ lan_min_2 <dbl> 0, 1, 0, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 1, 0, 0, 1, 0, 0, 0, …
    ## $ lan_min_3 <dbl> 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 1, 0, 0, 1, 0, 0, 0, …
    ## $ lan_min_4 <dbl> 0, 1, 0, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 1, 0, 0, 1, 0, 0, 0, …
    ## $ lan_min_5 <dbl> 0, 1, 0, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 1, 0, 0, 0, …

``` r
#------------------------------------------------
# producir porcentajes con valores plausibles
#------------------------------------------------

options(scipen = 999)
options(digits = 5)


tabla_7 <- mitools::withPV(
   mapping = lan_min ~ lan_min_1 + lan_min_2 + lan_min_3 + lan_min_4 + lan_min_5,
   data = erce_tsl,
   action = quote(
   svyby( ~lan_min, 
    by = ~COUNTRY, 
    design = erce_tsl,
    FUN = svymean
      )
    )
   )

#------------------------------------------------
# combinar resultados
#------------------------------------------------

library(mitools)
summary(mitools::MIcombine(tabla_7))
```

    ## Multiple imputation results:
    ##       withPV.survey.design(mapping = lan_min ~ lan_min_1 + lan_min_2 + 
    ##     lan_min_3 + lan_min_4 + lan_min_5, data = erce_tsl, action = quote(svyby(~lan_min, 
    ##     by = ~COUNTRY, design = erce_tsl, FUN = svymean)))
    ##       MIcombine.default(tabla_7)
    ##     results        se  (lower  upper) missInfo
    ## ARG 0.31862 0.0120848 0.29493 0.34232      4 %
    ## BRA 0.43514 0.0164518 0.40271 0.46756     14 %
    ## COL 0.37490 0.0174680 0.34065 0.40916      4 %
    ## CRI 0.54052 0.0175564 0.50570 0.57534     21 %
    ## CUB 0.44568 0.0123999 0.42135 0.47001      6 %
    ## DOM 0.16386 0.0109618 0.14237 0.18535      3 %
    ## ECU 0.26106 0.0100840 0.24127 0.28086      7 %
    ## GTM 0.15938 0.0101114 0.13954 0.17921      6 %
    ## HND 0.16188 0.0148347 0.13277 0.19099      6 %
    ## MEX 0.41612 0.0139756 0.38852 0.44371     16 %
    ## NIC 0.12971 0.0083517 0.11318 0.14624     19 %
    ## PAN 0.17483 0.0098372 0.15549 0.19417     11 %
    ## PER 0.48989 0.0139409 0.46254 0.51724      5 %
    ## PRY 0.18757 0.0105858 0.16674 0.20840     12 %
    ## SLV 0.29335 0.0124945 0.26867 0.31802     17 %
    ## URY 0.43723 0.0133617 0.41084 0.46362     17 %

# Codigo 1.9: Porcentajes de estudiantes sobre el mínimo de competencia de logo en Lenguaje (BRR) (Estudiantes 6to Grado, ERCE 2019)

``` r
# -------------------------------------------------------------------
# porcentajes con valores plausibles con BRR
# -------------------------------------------------------------------

#------------------------------------------------
# cluster únicos y recodificaciones
#------------------------------------------------
           
arg_a6 <- data_a6 %>%
          erce::remove_labels() %>%
          dplyr::filter(COUNTRY == 'ARG') %>%
mutate(id_s = as.numeric(as.factor(paste0(IDCNTRY, "_", STRATA)))) %>%
mutate(id_j = as.numeric(as.factor(paste0(IDCNTRY, "_", IDSCHOOL)))) %>%
mutate(id_i = seq(1:nrow(.))) %>%
           mutate(all = 1) %>%
           mutate(lan_min_1 = case_when(
           LAN_L1 == 'I'   ~ 0,
           LAN_L1 == 'II'  ~ 0,
           LAN_L1 == 'III' ~ 1,
           LAN_L1 == 'IV'  ~ 1)) %>%
           mutate(lan_min_2 = case_when(
           LAN_L2 == 'I'   ~ 0,
           LAN_L2 == 'II'  ~ 0,
           LAN_L2 == 'III' ~ 1,
           LAN_L2 == 'IV'  ~ 1)) %>%
           mutate(lan_min_3 = case_when(
           LAN_L3 == 'I'   ~ 0,
           LAN_L3 == 'II'  ~ 0,
           LAN_L3 == 'III' ~ 1,
           LAN_L3 == 'IV'  ~ 1)) %>%
           mutate(lan_min_4 = case_when(
           LAN_L4 == 'I'   ~ 0,
           LAN_L4 == 'II'  ~ 0,
           LAN_L4 == 'III' ~ 1,
           LAN_L4 == 'IV'  ~ 1)) %>%
           mutate(lan_min_5 = case_when(
           LAN_L5 == 'I'   ~ 0,
           LAN_L5 == 'II'  ~ 0,
           LAN_L5 == 'III' ~ 1,
           LAN_L5 == 'IV'  ~ 1)
           )

#------------------------------------------------
# distinguir entre valores plausibles y otras variables
#------------------------------------------------

plausible_values <- dplyr::select(arg_a6, 
                    lan_min_1, lan_min_2, lan_min_3, lan_min_4, lan_min_5)


non_plausible_values  <- dplyr::select(arg_a6, -one_of(names(plausible_values)))

# -----------------------------------------------
# crear bases de datos por valor plausible
# -----------------------------------------------

data_1 <- non_plausible_values %>%
          dplyr::left_join(., dplyr::select(arg_a6, id_i, lan_min_1), by = 'id_i') %>% 
          rename(lan_min = lan_min_1)

data_2 <- non_plausible_values %>%
          dplyr::left_join(., dplyr::select(arg_a6, id_i, lan_min_2), by = 'id_i') %>% 
          rename(lan_min = lan_min_2)

data_3 <- non_plausible_values %>%
          dplyr::left_join(., dplyr::select(arg_a6, id_i, lan_min_3), by = 'id_i') %>% 
          rename(lan_min = lan_min_3)

data_4 <- non_plausible_values %>%
          dplyr::left_join(., dplyr::select(arg_a6, id_i, lan_min_4), by = 'id_i') %>% 
          rename(lan_min = lan_min_4)

data_5 <- non_plausible_values %>%
          dplyr::left_join(., dplyr::select(arg_a6, id_i, lan_min_5), by = 'id_i') %>% 
          rename(lan_min = lan_min_5)


#------------------------------------------------
# crear lista de datos imputados
#------------------------------------------------

arg_a6_imputed <- mitools::imputationList(
                list(data_1, data_2, data_3, data_4, data_5)
                )

#------------------------------------------------
# crear objeto BRR con los datos imputados
#------------------------------------------------

library(survey)
arg_brr <- survey::svrepdesign(
                data    = arg_a6_imputed,
                type    = 'Fay', 
                rho     = .5,
                weights = ~WS,
                repweights = "repws[0-9]+",
                combined.weights = TRUE
                )


library(survey)
options(survey.lonely.psu="adjust")

#------------------------------------------------
# producir porcentajes con valores plausibles
#------------------------------------------------

options(scipen = 999)
options(digits = 5)

tabla_8 <- lodown::MIsvyciprop(
            ~lan_min, 
            design = arg_brr, 
            method = "logit", 
            level = 0.95, 
            df = mean(unlist(lapply(arg_brr$designs,survey::degf)))
            )

#------------------------------------------------
# mostrar resultados
#------------------------------------------------

tabla_8
```

    ##                2.5% 97.5%
    ## lan_min 0.319 0.296  0.34

# Codigo 1.10: percentiles con valores plausibles (BRR)

``` r
# -------------------------------------------------------------------
# percentiles con valores plausibles
# -------------------------------------------------------------------

#------------------------------------------------
# cluster únicos
#------------------------------------------------

data_example <- data_a6 %>%
                erce::remove_labels() %>%
                mutate(id_j = as.numeric(as.factor(paste0(COUNTRY, "_", IDSCHOOL)))) %>%
                mutate(id_i = seq(1:nrow(.)))

#------------------------------------------------
# separar valores plausibles
#------------------------------------------------

plausible_values <- dplyr::select(data_example, LAN_1, LAN_2, LAN_3, LAN_4, LAN_5)


non_plausible_values  <- dplyr::select(data_example, -one_of(names(plausible_values)))


# -----------------------------------------------
# crear lista de datos imputados
# -----------------------------------------------

data_1 <- non_plausible_values %>%
          dplyr::left_join(., dplyr::select(data_example, id_i, LAN_1), by = 'id_i') %>% 
          rename(lan = LAN_1)

data_2 <- non_plausible_values %>%
          dplyr::left_join(., dplyr::select(data_example, id_i, LAN_2), by = 'id_i') %>% 
          rename(lan = LAN_2)

data_3 <- non_plausible_values %>%
          dplyr::left_join(., dplyr::select(data_example, id_i, LAN_3), by = 'id_i') %>% 
          rename(lan = LAN_3)

data_4 <- non_plausible_values %>%
          dplyr::left_join(., dplyr::select(data_example, id_i, LAN_4), by = 'id_i') %>% 
          rename(lan = LAN_4)

data_5 <- non_plausible_values %>%
          dplyr::left_join(., dplyr::select(data_example, id_i, LAN_5), by = 'id_i') %>% 
          rename(lan = LAN_5)


data_imputed <- mitools::imputationList(
                list(data_1, data_2, data_3, data_4, data_5)
                )

#------------------------------------------------
# crear objeto BRR con los datos imputados
#------------------------------------------------

library(survey)
erce_brr_imp <- survey::svrepdesign(
                data    = data_imputed,
                type    = 'Fay', 
                rho     = .5,
                weights = ~WS,
                repweights = "repws[0-9]+",
                combined.weights = TRUE
                )

#------------------------------------------------
# calcular percentiles
#------------------------------------------------

percentiles_imp <- mitools::MIcombine(with(erce_brr_imp, 
                   svyquantile(~lan, design=erce_brr_imp, 
                   quantile=c(.05, .10, .25, .50, .75, .90, .95)
                   )))

#------------------------------------------------
# editar table
#------------------------------------------------

tabla_10 <- summary(percentiles_imp) %>%
            tibble::rownames_to_column("percentiles") %>%
            dplyr::rename(e = results, , se = se) %>%
            dplyr::select(percentiles, e, se)
```

    ## Multiple imputation results:
    ##       with(erce_brr_imp, svyquantile(~lan, design = erce_brr_imp, quantile = c(0.05, 
    ##     0.1, 0.25, 0.5, 0.75, 0.9, 0.95)))
    ##       MIcombine.default(with(erce_brr_imp, svyquantile(~lan, design = erce_brr_imp, 
    ##     quantile = c(0.05, 0.1, 0.25, 0.5, 0.75, 0.9, 0.95))))
    ##          results     se (lower upper) missInfo
    ## lan.0.05  519.06 2.6446 512.89 525.23     78 %
    ## lan.0.1   554.68 2.2689 549.35 560.01     80 %
    ## lan.0.25  617.60 1.7481 613.68 621.52     71 %
    ## lan.0.5   694.70 1.3864 691.79 697.61     52 %
    ## lan.0.75  775.14 1.1564 772.86 777.42     15 %
    ## lan.0.9   842.08 1.2451 839.56 844.60     36 %
    ## lan.0.95  879.16 1.2466 876.71 881.61     11 %

``` r
# -----------------------------------------------
# desplegar tabla
# -----------------------------------------------

knitr::kable(tabla_10, digits = 2)
```

| percentiles |      e |   se |
|:------------|-------:|-----:|
| lan.0.05    | 519.06 | 2.64 |
| lan.0.1     | 554.68 | 2.27 |
| lan.0.25    | 617.60 | 1.75 |
| lan.0.5     | 694.70 | 1.39 |
| lan.0.75    | 775.14 | 1.16 |
| lan.0.9     | 842.08 | 1.25 |
| lan.0.95    | 879.16 | 1.25 |

# Codigo 1.11: Medias de Lenguaje empleando valores plausibles por país (Estudiantes 6to Grado, ERCE 2019)

``` r
# -------------------------------------------------------------------
# porcentajes con valores plausibles
# -------------------------------------------------------------------

#------------------------------------------------
# cluster únicos
#------------------------------------------------
           
data_a6 <- data_a6 %>%
erce::remove_labels() %>%
mutate(id_s = as.numeric(as.factor(paste0(IDCNTRY, "_", STRATA)))) %>%
mutate(id_j = as.numeric(as.factor(paste0(IDCNTRY, "_", IDSCHOOL)))) %>%
mutate(id_i = seq(1:nrow(.)))

#------------------------------------------------
# base de datos con diseño
#------------------------------------------------

erce_tsl  <- survey::svydesign(
             data    = data_a6, 
             weights = ~WS,
             strata  = ~id_s,
             id = ~id_j,
             nest = TRUE)

# Opción: corección a unidad primaria de muestreo que resulte 
# única al estrato

library(survey)
options(survey.lonely.psu="adjust")

# Nota: withPV() solo funciona con Taylor Series Linearization

#------------------------------------------------
# producir porcentajes con valores plausibles
#------------------------------------------------

options(scipen = 999)
options(digits = 5)

tabla_11 <- withPV(
   mapping = lan ~ LAN_1 + LAN_2 + LAN_3 + LAN_4 + LAN_5,
   data = erce_tsl,
   action = quote(
   svyby( ~lan, 
    by = ~COUNTRY, 
    FUN = svymean,
    design = erce_tsl
    )
  )
)

#------------------------------------------------
# combinar resultados
#------------------------------------------------

library(mitools)
summary(mitools::MIcombine(tabla_11))
```

    ## Multiple imputation results:
    ##       withPV.survey.design(mapping = lan ~ LAN_1 + LAN_2 + LAN_3 + 
    ##     LAN_4 + LAN_5, data = erce_tsl, action = quote(svyby(~lan, 
    ##     by = ~COUNTRY, FUN = svymean, design = erce_tsl)))
    ##       MIcombine.default(tabla_11)
    ##     results     se (lower upper) missInfo
    ## ARG  697.64 3.7325 690.26 705.02     18 %
    ## BRA  734.44 3.7340 727.12 741.77      4 %
    ## COL  719.32 4.4446 710.60 728.03      4 %
    ## CRI  757.26 3.8698 749.66 764.86      8 %
    ## CUB  737.93 2.9155 732.21 743.66      7 %
    ## DOM  643.96 4.0316 636.03 651.89     12 %
    ## ECU  684.26 3.0696 678.21 690.30     12 %
    ## GTM  645.28 4.2125 636.98 653.57     13 %
    ## HND  661.26 4.5049 652.41 670.11      9 %
    ## MEX  725.56 3.4534 718.75 732.37     15 %
    ## NIC  654.15 3.0884 648.07 660.23     13 %
    ## PAN  651.62 3.8491 644.07 659.17      7 %
    ## PER  741.23 4.1043 733.18 749.28      5 %
    ## PRY  657.17 3.3849 650.48 663.86     17 %
    ## SLV  698.77 3.2176 692.43 705.11     14 %
    ## URY  734.06 3.5249 727.14 740.98      7 %

``` r
#------------------------------------------------
# editar tabla
#------------------------------------------------

estimados <- summary(mitools::MIcombine(tabla_11))
```

    ## Multiple imputation results:
    ##       withPV.survey.design(mapping = lan ~ LAN_1 + LAN_2 + LAN_3 + 
    ##     LAN_4 + LAN_5, data = erce_tsl, action = quote(svyby(~lan, 
    ##     by = ~COUNTRY, FUN = svymean, design = erce_tsl)))
    ##       MIcombine.default(tabla_11)
    ##     results     se (lower upper) missInfo
    ## ARG  697.64 3.7325 690.26 705.02     18 %
    ## BRA  734.44 3.7340 727.12 741.77      4 %
    ## COL  719.32 4.4446 710.60 728.03      4 %
    ## CRI  757.26 3.8698 749.66 764.86      8 %
    ## CUB  737.93 2.9155 732.21 743.66      7 %
    ## DOM  643.96 4.0316 636.03 651.89     12 %
    ## ECU  684.26 3.0696 678.21 690.30     12 %
    ## GTM  645.28 4.2125 636.98 653.57     13 %
    ## HND  661.26 4.5049 652.41 670.11      9 %
    ## MEX  725.56 3.4534 718.75 732.37     15 %
    ## NIC  654.15 3.0884 648.07 660.23     13 %
    ## PAN  651.62 3.8491 644.07 659.17      7 %
    ## PER  741.23 4.1043 733.18 749.28      5 %
    ## PRY  657.17 3.3849 650.48 663.86     17 %
    ## SLV  698.77 3.2176 692.43 705.11     14 %
    ## URY  734.06 3.5249 727.14 740.98      7 %

``` r
tabla_11 <- estimados %>%
              tibble::rownames_to_column("paises") %>%
              rename(
               lan = results, 
               lan_se = se,
               ll = 4,
               ul = 5,
               miss = 6
               )

# -----------------------------------------------
# mostrar tabla
# -----------------------------------------------

knitr::kable(tabla_11, digits = 2)
```

| paises |    lan | lan_se |     ll |     ul | miss |
|:-------|-------:|-------:|-------:|-------:|:-----|
| ARG    | 697.64 |   3.73 | 690.26 | 705.02 | 18 % |
| BRA    | 734.44 |   3.73 | 727.12 | 741.77 | 4 %  |
| COL    | 719.32 |   4.44 | 710.60 | 728.03 | 4 %  |
| CRI    | 757.26 |   3.87 | 749.66 | 764.86 | 8 %  |
| CUB    | 737.93 |   2.92 | 732.21 | 743.66 | 7 %  |
| DOM    | 643.96 |   4.03 | 636.03 | 651.89 | 12 % |
| ECU    | 684.26 |   3.07 | 678.21 | 690.30 | 12 % |
| GTM    | 645.28 |   4.21 | 636.98 | 653.57 | 13 % |
| HND    | 661.26 |   4.50 | 652.41 | 670.11 | 9 %  |
| MEX    | 725.56 |   3.45 | 718.75 | 732.37 | 15 % |
| NIC    | 654.15 |   3.09 | 648.07 | 660.23 | 13 % |
| PAN    | 651.62 |   3.85 | 644.07 | 659.17 | 7 %  |
| PER    | 741.23 |   4.10 | 733.18 | 749.28 | 5 %  |
| PRY    | 657.17 |   3.38 | 650.48 | 663.86 | 17 % |
| SLV    | 698.77 |   3.22 | 692.43 | 705.11 | 14 % |
| URY    | 734.06 |   3.52 | 727.14 | 740.98 | 7 %  |
