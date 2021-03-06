Regresiones
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

# algunos computadores requieren esta opcion, cuando tienen instalado git
credentials::set_github_pat()

# la presente libreria se encuentra en desarollado y no es de acceso libre
devtools::install_github(
  'dacarras/erce',
  force = TRUE)

#------------------------------------------------
# librerías en uso
#------------------------------------------------

install.packages('tidyverse')
install.packages('mitools')
install.packages('survey')
install.packages('srvyr')
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
           erce::remove_labels() %>%
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

# Codigo 1.2 regresion de puntajes de matemáticas a nivel socioeconómico, empleando datos de la región (Estudiantes 6to grado, ERCE 2019)

``` r
# -------------------------------------------------------------------
# regresion con valores plausibles y TSL
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
```

    ## Loading required package: grid

    ## Loading required package: Matrix

    ## Loading required package: survival

    ## 
    ## Attaching package: 'survey'

    ## The following object is masked from 'package:graphics':
    ## 
    ##     dotchart

``` r
options(survey.lonely.psu="adjust")

# Nota: withPV() solo funciona con Taylor Series Linearization

#------------------------------------------------
# ajustar regresión
#------------------------------------------------

options(scipen = 999)
options(digits = 10)

tabla_1 <- mitools::withPV(
   mapping = mat ~ MAT_1 + MAT_2 + MAT_3 + MAT_4 + MAT_5, #<<
   data = erce_tsl,
   action = quote(survey::svyglm(mat ~ 1 + ISECF, design = erce_tsl)),
   rewrite=TRUE
   )

#------------------------------------------------
# combinar resultados
#------------------------------------------------

library(mitools)
summary(mitools::MIcombine(tabla_1))
```

    ## Multiple imputation results:
    ##       withPV.survey.design(mapping = mat ~ MAT_1 + MAT_2 + MAT_3 + 
    ##     MAT_4 + MAT_5, data = erce_tsl, action = quote(survey::svyglm(mat ~ 
    ##     1 + ISECF, design = erce_tsl)), rewrite = TRUE)
    ##       MIcombine.default(tabla_1)
    ##                 results           se       (lower       upper) missInfo
    ## (Intercept) 697.5691108 1.0017864349 695.54088295 699.59733857     36 %
    ## ISECF        36.1518283 0.7905758005  34.59531868  37.70833792     13 %

# Codigo 1.3 regresion con valores plausibles y valores ***p***.

``` r
# -------------------------------------------------------------------
# regresion con valores plausibles y TSL
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
# ajustar modelo
#------------------------------------------------

pv_estimates <- mitools::withPV(
   mapping = mat ~ MAT_1 + MAT_2 + MAT_3 + MAT_4 + MAT_5, #<<
   data = erce_tsl,
   action = quote(survey::svyglm(mat ~ 1 + ISECF, design = erce_tsl)),
   rewrite=TRUE
   )

#------------------------------------------------
# combinar resultados
#------------------------------------------------

tabla_2 <- erce::combine_reg(pv_estimates)

#------------------------------------------------
# mostrar tabla
#------------------------------------------------

tabla_2 %>%
knitr::kable(., digits = 2)
```

| term        |      e |   se | p_val |     lo |     hi |
|:------------|-------:|-----:|------:|-------:|-------:|
| (Intercept) | 697.57 | 1.00 |     0 | 695.54 | 699.60 |
| ISECF       |  36.15 | 0.79 |     0 |  34.60 |  37.71 |

# Codigo 1.4: regresión con BRR empleando `survey`

``` r
# -------------------------------------------------------------------
# regresion con valores plausibles y TSL
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
# lista de datos imputados
#------------------------------------------------

data_1 <- data_a6 %>% mutate(matpv = MAT_1) #<<
data_2 <- data_a6 %>% mutate(matpv = MAT_2) #<<
data_3 <- data_a6 %>% mutate(matpv = MAT_3) #<<
data_4 <- data_a6 %>% mutate(matpv = MAT_4) #<<
data_5 <- data_a6 %>% mutate(matpv = MAT_5) #<<


data_imputed <- mitools::imputationList(
                list(data_1, data_2, data_3, data_4, data_5)
                )

#------------------------------------------------
# base de datos con diseño
#------------------------------------------------

erce_brr <- survey::svrepdesign(
            data    = data_imputed,
            type    = 'Fay', 
            rho     = .5,
            weights = ~WS,
            repweights = "repws[0-9]+",
            combined.weights = TRUE
            )

# Opción: corección a unidad primaria de muestreo que resulte 
# única al estrato

library(survey)
options(survey.lonely.psu="adjust")

#-------------------------------------------------
# especificar model
#-------------------------------------------------

regression_model <- as.formula(matpv ~ 1 + ISECF )

#------------------------------------------------
# ajustar modelo
#------------------------------------------------

svyglm_estimates <- with(erce_brr, 
                    survey::svyglm(regression_model, design = erce_brr
                    ))

#------------------------------------------------
# combinar estimados
#------------------------------------------------

tabla_3 <- erce::combine_reg(svyglm_estimates)

#------------------------------------------------
# mostrar resultados
#------------------------------------------------

knitr::kable(tabla_3, digits = 2)
```

| term        |      e |   se | p_val |     lo |     hi |
|:------------|-------:|-----:|------:|-------:|-------:|
| (Intercept) | 697.57 | 0.95 |     0 | 695.62 | 699.52 |
| ISECF       |  36.15 | 0.82 |     0 |  34.54 |  37.76 |

# Codigo 1.5: regresión con TSL empleando `survey` prediciendo una variable dictómica

``` r
# -------------------------------------------------------------------
# regresión logistica con valores plausibles y TSL
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
# elegimos un país al azar
#------------------------------------------------

data_a6 <- data_a6 %>%
           dplyr::filter(IDCNTRY == 76) # Brasil



#------------------------------------------------
# recodificacion
#------------------------------------------------

rec_pv_level <- function(x){
dplyr::case_when(
  x == 'I'  ~ 0,
  x == 'II' ~ 0,
  x == 'III'~ 1,
  x == 'IV' ~ 1)
}

data_a6 <- data_a6 %>% 
           mutate(mat_mpl1 = rec_pv_level(MAT_L1)) %>% #<<
           mutate(mat_mpl2 = rec_pv_level(MAT_L2)) %>% #<<
           mutate(mat_mpl3 = rec_pv_level(MAT_L3)) %>% #<<
           mutate(mat_mpl4 = rec_pv_level(MAT_L4)) %>% #<<
           mutate(mat_mpl5 = rec_pv_level(MAT_L5))     #<<

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

#------------------------------------------------
# ajustar modelo
#------------------------------------------------

logit_estimates <- mitools::withPV(
   mapping = mat_mpl ~ mat_mpl1 + mat_mpl2 + mat_mpl3 + mat_mpl4 + mat_mpl5, #<<
   data = erce_tsl,
   action = quote(
    survey::svyglm(mat_mpl ~ 1 + EDU, 
      design = erce_tsl,
      family = 'quasibinomial'(link = "logit")
      )),
   rewrite=TRUE
   )

#------------------------------------------------
# combinar estimados
#------------------------------------------------

tabla_4 <- erce::combine_log(logit_estimates)

#------------------------------------------------
# mostrar resultados
#------------------------------------------------

knitr::kable(tabla_4, digits = 2)
```

| term        |     e |   se | p_val |    lo |    hi |   or | or_lo | or_hi |
|:------------|------:|-----:|------:|------:|------:|-----:|------:|------:|
| (Intercept) | -1.20 | 0.09 |     0 | -1.38 | -1.02 | 0.30 |  0.25 |  0.36 |
| EDU         |  1.53 | 0.13 |     0 |  1.27 |  1.79 | 4.61 |  3.55 |  6.00 |

# Codigo 1.6: regresión con BRR empleando `survey` prediciendo una variable dictómica

``` r
# -------------------------------------------------------------------
# regresión logistica con valores plausibles y BRR
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
# elegimos un país al azar
#------------------------------------------------

data_a6 <- data_a6 %>%
           dplyr::filter(IDCNTRY == 76) # Brasil

#------------------------------------------------
# recodificacion
#------------------------------------------------

rec_pv_level <- function(x){
dplyr::case_when(
  x == 'I'  ~ 0,
  x == 'II' ~ 0,
  x == 'III'~ 1,
  x == 'IV' ~ 1)
}


#------------------------------------------------
# lista de datos imputados
#------------------------------------------------

data_1 <- data_a6 %>% mutate(mat_mpl = rec_pv_level(MAT_L1)) #<<
data_2 <- data_a6 %>% mutate(mat_mpl = rec_pv_level(MAT_L2)) #<<
data_3 <- data_a6 %>% mutate(mat_mpl = rec_pv_level(MAT_L3)) #<<
data_4 <- data_a6 %>% mutate(mat_mpl = rec_pv_level(MAT_L4)) #<<
data_5 <- data_a6 %>% mutate(mat_mpl = rec_pv_level(MAT_L5)) #<<


data_imputed <- mitools::imputationList(
                list(data_1, data_2, data_3, data_4, data_5)
                )

#------------------------------------------------
# base de datos con diseño
#------------------------------------------------

erce_brr <- survey::svrepdesign(
            data    = data_imputed,
            type    = 'Fay', 
            rho     = .5,
            weights = ~WS,
            repweights = "repws[0-9]+",
            combined.weights = TRUE
            )

# Opción: corección a unidad primaria de muestreo que resulte 
# única al estrato

library(survey)
options(survey.lonely.psu="adjust")

#-------------------------------------------------
# especificar model
#-------------------------------------------------

logit_model <- as.formula(mat_mpl ~ 1 + EDU )

#------------------------------------------------
# ajustar modelo
#------------------------------------------------


svyglm_estimates <- with(erce_brr, 
                    survey::svyglm(logit_model, 
                      design = erce_brr,
                      family = 'quasibinomial'(link = "logit")
                    ))

#------------------------------------------------
# combinar estimados
#------------------------------------------------

tabla_6 <- erce::combine_log(svyglm_estimates)

#------------------------------------------------
# mostrar resultados
#------------------------------------------------

knitr::kable(tabla_6, digits = 2)
```

| term        |     e |   se | p_val |    lo |    hi |   or | or_lo | or_hi |
|:------------|------:|-----:|------:|------:|------:|-----:|------:|------:|
| (Intercept) | -1.20 | 0.08 |     0 | -1.36 | -1.04 | 0.30 |  0.26 |  0.35 |
| EDU         |  1.53 | 0.14 |     0 |  1.26 |  1.80 | 4.61 |  3.52 |  6.04 |

# Codigo 1.7: regresión variable observada, y dos predictores con TSL

``` r
# -------------------------------------------------------------------
# regresión lineal a variable observada con dos predictores
# -------------------------------------------------------------------

#------------------------------------------------
# preparacion de datos
#------------------------------------------------
           
data_a6 <- erce::erce_2019_qa6 %>%
# removemos labels
erce::remove_labels() %>%
# elegimos un solo país
dplyr::filter(IDCNTRY == 192) %>% # Cuba
mutate(id_k = as.numeric(as.factor(paste0(IDCNTRY)))) %>%
mutate(id_s = as.numeric(as.factor(paste0(IDCNTRY, "_", STRATA)))) %>%
mutate(id_j = as.numeric(as.factor(paste0(IDCNTRY, "_", IDSCHOOL)))) %>%
mutate(id_i = seq(1:nrow(.))) %>%
# centrado de nivel socioeconómico
mutate(z =   ISECF)  %>%                   # mean score
mutate(z_c = erce::c_mean(z, id_j)) %>%    # means by group
mutate(z_g = erce::c_mean(z, id_k)) %>%    # grand mean    
mutate(z_w = z - z_c   )    %>%  # centering within cluster
mutate(z_m = z - z_g   )    %>%  # centering to the grand mean
mutate(z_b = z_c - z_g )    %>%  # centered cluster means
## violencia en la escuela (indice de victimización escolar)
mutate(x =   VIOES)  %>%                   # mean score
mutate(x_c = erce::c_mean(x, id_j)) %>%    # means by group
mutate(x_g = erce::c_mean(x, id_k)) %>%    # grand mean    
mutate(x_w = x - x_c   )    %>%  # centering within cluster
mutate(x_m = x - x_g   )    %>%  # centering to the grand mean
mutate(x_b = x_c - x_g )         # centered cluster means

#------------------------------------------------
# base de datos con diseño
#------------------------------------------------

erce_tsl  <- survey::svydesign(
             data    = data_a6, 
             weights = ~WS,
             strata  = ~id_s,
             id = ~id_j,
             nest = TRUE)

library(survey)
options(survey.lonely.psu="adjust")

#------------------------------------------------
# ajustar modelo
#------------------------------------------------

svy_estimates <- survey::svyglm(AURES ~ 1 + x_m + z_w + z_b, design = erce_tsl)

#------------------------------------------------
# extraer estimados a una tabla
#------------------------------------------------

tabla_7 <- broom::tidy(svy_estimates, conf.int = TRUE)

#------------------------------------------------
# mostrar tabla
#------------------------------------------------

knitr::kable(tabla_7, digits = 2)
```

| term        | estimate | std.error | statistic | p.value | conf.low | conf.high |
|:------------|---------:|----------:|----------:|--------:|---------:|----------:|
| (Intercept) |    56.78 |      0.21 |    275.83 |    0.00 |    56.37 |     57.19 |
| x_m         |    -3.18 |      0.20 |    -16.26 |    0.00 |    -3.57 |     -2.80 |
| z_w         |     0.46 |      0.22 |      2.13 |    0.03 |     0.04 |      0.89 |
| z_b         |    -1.74 |      0.56 |     -3.13 |    0.00 |    -2.83 |     -0.64 |

# Codigo 1.8: regresión variable observada, y dos predictores con BRR

``` r
# -------------------------------------------------------------------
# regresión lineal a variable observada con dos predictores
# -------------------------------------------------------------------

#------------------------------------------------
# preparacion de datos
#------------------------------------------------
           
data_a6 <- erce::erce_2019_qa6 %>%
# removemos labels
erce::remove_labels() %>%
# elegimos un solo país
dplyr::filter(IDCNTRY == 192) %>% # Cuba
mutate(id_k = as.numeric(as.factor(paste0(IDCNTRY)))) %>%
mutate(id_s = as.numeric(as.factor(paste0(IDCNTRY, "_", STRATA)))) %>%
mutate(id_j = as.numeric(as.factor(paste0(IDCNTRY, "_", IDSCHOOL)))) %>%
mutate(id_i = seq(1:nrow(.))) %>%
# centrado de nivel socioeconómico
mutate(z =   ISECF)  %>%                   # mean score
mutate(z_c = erce::c_mean(z, id_j)) %>%    # means by group
mutate(z_g = erce::c_mean(z, id_k)) %>%    # grand mean    
mutate(z_w = z - z_c   )    %>%  # centering within cluster
mutate(z_m = z - z_g   )    %>%  # centering to the grand mean
mutate(z_b = z_c - z_g )    %>%  # centered cluster means
## violencia en la escuela (indice de victimización escolar)
mutate(x =   VIOES)  %>%                   # mean score
mutate(x_c = erce::c_mean(x, id_j)) %>%    # means by group
mutate(x_g = erce::c_mean(x, id_k)) %>%    # grand mean    
mutate(x_w = x - x_c   )    %>%  # centering within cluster
mutate(x_m = x - x_g   )    %>%  # centering to the grand mean
mutate(x_b = x_c - x_g )         # centered cluster means

#------------------------------------------------
# base de datos con diseño
#------------------------------------------------

erce_brr <- survey::svrepdesign(
            data    = data_a6,
            type    = 'Fay', 
            rho     = .5,
            weights = ~WT,
            repweights = "BRR[0-9]+",
            combined.weights = TRUE
            )

library(survey)
options(survey.lonely.psu="adjust")

#------------------------------------------------
# ajustar modelo
#------------------------------------------------

svy_estimates <- survey::svyglm(AURES ~ 1 + x_m + z_w + z_b, design = erce_brr)

#------------------------------------------------
# extraer estimados a una tabla
#------------------------------------------------

tabla_8 <- broom::tidy(svy_estimates, conf.int = TRUE)

#------------------------------------------------
# mostrar tabla
#------------------------------------------------

knitr::kable(tabla_8, digits = 2)
```

| term        | estimate | std.error | statistic | p.value | conf.low | conf.high |
|:------------|---------:|----------:|----------:|--------:|---------:|----------:|
| (Intercept) |    56.78 |      0.22 |    259.54 |    0.00 |    56.35 |     57.21 |
| x_m         |    -3.18 |      0.19 |    -16.93 |    0.00 |    -3.56 |     -2.81 |
| z_w         |     0.46 |      0.23 |      1.99 |    0.05 |     0.00 |      0.93 |
| z_b         |    -1.74 |      0.57 |     -3.03 |    0.00 |    -2.88 |     -0.60 |

# Codigo 1.9: regresión logistica variable observada, y dos predictores con TSL

``` r
# -------------------------------------------------------------------
# regresión lineal a variable observada con dos predictores
# -------------------------------------------------------------------

#------------------------------------------------
# preparacion de datos
#------------------------------------------------
           
data_a6 <- erce::erce_2019_qa6 %>%
# removemos labels
erce::remove_labels() %>%
# elegimos un solo país
dplyr::filter(IDCNTRY == 192) %>% # Cuba
mutate(id_k = as.numeric(as.factor(paste0(IDCNTRY)))) %>%
mutate(id_s = as.numeric(as.factor(paste0(IDCNTRY, "_", STRATA)))) %>%
mutate(id_j = as.numeric(as.factor(paste0(IDCNTRY, "_", IDSCHOOL)))) %>%
mutate(id_i = seq(1:nrow(.))) %>%
# centrado de nivel socioeconómico
mutate(z =   ISECF)  %>%                   # mean score
mutate(z_c = erce::c_mean(z, id_j)) %>%    # means by group
mutate(z_g = erce::c_mean(z, id_k)) %>%    # grand mean    
mutate(z_w = z - z_c   )    %>%  # centering within cluster
mutate(z_m = z - z_g   )    %>%  # centering to the grand mean
mutate(z_b = z_c - z_g )    %>%  # centered cluster means
## violencia en la escuela (indice de victimización escolar)
mutate(x =   VIOES)  %>%                   # mean score
mutate(x_c = erce::c_mean(x, id_j)) %>%    # means by group
mutate(x_g = erce::c_mean(x, id_k)) %>%    # grand mean    
mutate(x_w = x - x_c   )    %>%  # centering within cluster
mutate(x_m = x - x_g   )    %>%  # centering to the grand mean
mutate(x_b = x_c - x_g )         # centered cluster means

#------------------------------------------------
# base de datos con diseño
#------------------------------------------------

erce_tsl  <- survey::svydesign(
             data    = data_a6, 
             weights = ~WS,
             strata  = ~id_s,
             id = ~id_j,
             nest = TRUE)

library(survey)
options(survey.lonely.psu="adjust")

#------------------------------------------------
# ajustar modelo
#------------------------------------------------

svy_estimates <- survey::svyglm(REPC ~ 1 + x_m + z_w + z_b,
                 design = erce_tsl,
                 family = 'quasibinomial'(link = "logit")
                 )

#------------------------------------------------
# extraer estimados a una tabla
#------------------------------------------------

tabla_9 <- broom::tidy(svy_estimates, conf.int = TRUE) %>%
           mutate(or = exp(estimate)) %>%
           mutate(or_lo = exp(conf.low)) %>%
           mutate(or_hi = exp(conf.high))

#------------------------------------------------
# mostrar tabla
#------------------------------------------------

knitr::kable(tabla_9, digits = 2)
```

| term        | estimate | std.error | statistic | p.value | conf.low | conf.high |   or | or_lo | or_hi |
|:------------|---------:|----------:|----------:|--------:|---------:|----------:|-----:|------:|------:|
| (Intercept) |    -3.94 |      0.15 |    -27.02 |    0.00 |    -4.23 |     -3.66 | 0.02 |  0.01 |  0.03 |
| x_m         |     0.53 |      0.10 |      5.53 |    0.00 |     0.34 |      0.72 | 1.70 |  1.41 |  2.06 |
| z_w         |    -0.68 |      0.15 |     -4.37 |    0.00 |    -0.98 |     -0.37 | 0.51 |  0.37 |  0.69 |
| z_b         |     0.33 |      0.28 |      1.18 |    0.24 |    -0.22 |      0.87 | 1.39 |  0.80 |  2.39 |

# Codigo 1.10: regresión logistica variable observada, y dos predictores con BRR

``` r
# -------------------------------------------------------------------
# regresión lineal a variable observada con dos predictores
# -------------------------------------------------------------------

#------------------------------------------------
# preparacion de datos
#------------------------------------------------
           
data_a6 <- erce::erce_2019_qa6 %>%
# removemos labels
erce::remove_labels() %>%
# elegimos un solo país
dplyr::filter(IDCNTRY == 192) %>% # Cuba
mutate(id_k = as.numeric(as.factor(paste0(IDCNTRY)))) %>%
mutate(id_s = as.numeric(as.factor(paste0(IDCNTRY, "_", STRATA)))) %>%
mutate(id_j = as.numeric(as.factor(paste0(IDCNTRY, "_", IDSCHOOL)))) %>%
mutate(id_i = seq(1:nrow(.))) %>%
# centrado de nivel socioeconómico
mutate(z =   ISECF)  %>%                   # mean score
mutate(z_c = erce::c_mean(z, id_j)) %>%    # means by group
mutate(z_g = erce::c_mean(z, id_k)) %>%    # grand mean    
mutate(z_w = z - z_c   )    %>%  # centering within cluster
mutate(z_m = z - z_g   )    %>%  # centering to the grand mean
mutate(z_b = z_c - z_g )    %>%  # centered cluster means
## violencia en la escuela (indice de victimización escolar)
mutate(x =   VIOES)  %>%                   # mean score
mutate(x_c = erce::c_mean(x, id_j)) %>%    # means by group
mutate(x_g = erce::c_mean(x, id_k)) %>%    # grand mean    
mutate(x_w = x - x_c   )    %>%  # centering within cluster
mutate(x_m = x - x_g   )    %>%  # centering to the grand mean
mutate(x_b = x_c - x_g )         # centered cluster means

#------------------------------------------------
# base de datos con diseño
#------------------------------------------------

erce_brr <- survey::svrepdesign(
            data    = data_a6,
            type    = 'Fay', 
            rho     = .5,
            weights = ~WT,
            repweights = "BRR[0-9]+",
            combined.weights = TRUE
            )

library(survey)
options(survey.lonely.psu="adjust")

#------------------------------------------------
# ajustar modelo
#------------------------------------------------

svy_estimates <- survey::svyglm(REPC ~ 1 + x_m + z_w + z_b,
                 design = erce_brr,
                 family = 'quasibinomial'(link = "logit")
                 )

#------------------------------------------------
# extraer estimados a una tabla
#------------------------------------------------

tabla_10 <- broom::tidy(svy_estimates, conf.int = TRUE) %>%
            mutate(or = exp(estimate)) %>%
            mutate(or_lo = exp(conf.low)) %>%
            mutate(or_hi = exp(conf.high))

#------------------------------------------------
# mostrar tabla
#------------------------------------------------

knitr::kable(tabla_10, digits = 2)
```

| term        | estimate | std.error | statistic | p.value | conf.low | conf.high |   or | or_lo | or_hi |
|:------------|---------:|----------:|----------:|--------:|---------:|----------:|-----:|------:|------:|
| (Intercept) |    -3.94 |      0.14 |    -27.51 |    0.00 |    -4.23 |     -3.66 | 0.02 |  0.01 |  0.03 |
| x_m         |     0.53 |      0.09 |      5.66 |    0.00 |     0.34 |      0.72 | 1.70 |  1.41 |  2.05 |
| z_w         |    -0.68 |      0.15 |     -4.48 |    0.00 |    -0.98 |     -0.38 | 0.51 |  0.38 |  0.69 |
| z_b         |     0.33 |      0.30 |      1.10 |    0.27 |    -0.26 |      0.92 | 1.39 |  0.77 |  2.50 |
