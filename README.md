
# LLECE: Taller Análisis II

-   Taller de Análisis de datos de ERCE 2019

    -   Taller conducido de forma remota los días Marzo 02 y 03 de 2022

-   Contenidos del taller

    -   [01
        introduccion](https://www.dropbox.com/s/m8pd9ub8o4ek8sk/01_introduccion.pdf?dl=1)
        -   introducción a estudios de gran escala
    -   [02
        desarollo](https://www.dropbox.com/s/7z1p1g9z98gq7av/02_desarrollo.pdf?dl=1)
        -   análisis de datos como desarollo
    -   [03
        descriptivos](https://www.dropbox.com/s/2g4pwxl178605xl/03_descriptivos.pdf?dl=1)
        -   como estimar porcentajes, percentiles, y medias
    -   [04
        regresiones](https://www.dropbox.com/s/2bkue9vox99jfws/04_regresiones.pdf?dl=1)
        -   como ajustar regresiones con diseño muestral
    -   [05
        resultados](https://www.dropbox.com/s/5v0od8absek2lp1/05_resultados.pdf?dl=1)
        -   desarollo y reproducción de resultados
    -   [06
        multinivel](https://www.dropbox.com/s/ydezg9t7n8wi7bl/06_multinivel.pdf?dl=1)
        -   como ajustar modelos multinivel con diseño muestral

# erce

-   librería generada para el taller de análisis de datos de ERCE 2019,
    Taller II
-   esta librería facilita el proceso de acceder a los datos del estudio
    ERCE 2019
-   además contiene funciones auxiliares para facilitar el proceso de
    análisis de datos

## Instalar librería con datos

``` r
devtools::install_github(
  'dacarras/erce',
  force = TRUE)
```

> Nota: librería en desarollo. Creada para la realización del taller.

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

[Bajar todas las
láminas](https://www.dropbox.com/sh/cvhydi7akjhrct9/AADTyDIAd9DXjQe9HQvpb6kPa?dl=1)

# Ejemplos

[Bajar todos los códigos de
ejemplos](https://www.dropbox.com/sh/6nfjtrorh2hm0ot/AACdjXLYqih518Hrohhc8dUHa?dl=1)
