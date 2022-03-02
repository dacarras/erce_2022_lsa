
# LLECE: Taller Análisis II

-   01 introduccion
-   02 desarollo
-   03 descriptivos
-   04 regresiones
-   05 resultados
-   06 multinivel

# erce

-   librería generada para el taller de análisis de datos de ERCE 2019,
    Taller II
-   este taller fue conducido de forma remota entre los días Marzo 02 y
    03 de 2022
-   esta librería facilita el proceso de acceder a los datos del estudio
    ERCE 2019
-   además contiene funciones auxiliares para facilitar el proceso de
    análisis de datos

## Instalar librería con datos

``` r
devtools::install_github(
  'dacarras/erce',
  auth_token = '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',
  force = TRUE)
```

## funciones

-   `remove_labels()` elimina metadata de los datos, para que estos
    puedan ser procesados para crear objetos de base de datos con srvyr
    y survey
-   `combine_reg()` combina las estimaciones realizadas sobre valores
    plausibles, en modelos de regresión lineal
-   `combine_log()` combina las estimaciones realizadas sobre valores
    plausibles, en modelos de regresión logística
-   `c_mean()` genera medias de grupos. Función empleada para realizar
    centrados de variables.
-   `senate_weights()` calcula senate weights o pesos normalizados a una
    constante (e.g., 1000, 500 u otra constante seleccionada), y los
    agrega a los datos originales en una variable llamada `ws`
-   `lsa_weights()` calcula pesos normalizados y pesos efectivos a la
    muestra para modelos multinivel, guardando el resultado en variables
    `wa1`, `wa2`, `wb1` y `wb2`.

# Librerías requeridas

``` r
# -------------------------------------------------------------------
# librerias
# -------------------------------------------------------------------
#------------------------------------------------
# librerias para instalar librerias remotas
#------------------------------------------------

install.packages('devtools')
install.packages('remotes')

#------------------------------------------------
# para estimar modelos poblacionales
#------------------------------------------------

install.packages('tidyverse')
install.packages('mitools')
install.packages('survey')
install.packages('srvyr')

#------------------------------------------------
# para ajustar modelos multinivel
#------------------------------------------------

install.packages('MplusAutomation')
install.packages('RStata')
install.packages('WeMix')

#------------------------------------------------
# mostrar estimados
#------------------------------------------------

install.packages('texreg')
install.packages('miceadds')
```

# Láminas

[Bajar
láminas](https://www.dropbox.com/sh/cvhydi7akjhrct9/AADTyDIAd9DXjQe9HQvpb6kPa?dl=1)

# Ejemplos

[Bajar
ejemplos](https://www.dropbox.com/sh/6nfjtrorh2hm0ot/AACdjXLYqih518Hrohhc8dUHa?dl=1)
