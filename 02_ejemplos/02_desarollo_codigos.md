LLECE: Taller de Análisis II
================
dacarras
Marzo 2 de 2022

<style>
  .main-container {
    max-width: 1600px !important;
  }
  .list-group-item.active, 
  .list-group-item.active:focus, 
  .list-group-item.active:hover {
    background-color: #373334;
  }
</style>

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
  auth_token = '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',
  force = TRUE)

#------------------------------------------------
# librerías en uso
#------------------------------------------------

install.packages('tidyverse')
install.packages('mitools')
install.packages('survey')
install.packages('srvyr')
```

# Codigo 1.1: abrir los datos

-   El primer problema a resolver, consiste en como **abrir los datos**
    que queremos emplear.

    -   Algunos estudios de gran escala como ICCS 2016 por ejemplo,
        proveen de un archivo de datos por país, y por instrumento.

    -   En cambio, otros estudios de gran escala proveen de un solo
        archivo para todos los países, integrando puntajes y respuestas
        a los cuestionarios de contexto. Este es el caso de PISA 2018.

    -   **ERCE 2019** pertenece a este segundo grupo, y los datos se
        encuentran separados por población de estudiantes (Tercer y
        Sexto grado), y por instrumento o cuestionario de contexto.

``` r
# forma rápida de abrir los datos
erce_a6 <- erce::erce_2019_qa6
```

``` r
# Listado de archivos

# Base de datos de estudiantes   | # Base de datos de familias
# ERCE_2019_QA3.rds              | # ERCE_2019_QF3.rds
# ERCE_2019_QA6.rds              | # ERCE_2019_QF6.rds

# Base de datos de profesores    | # Base de datos de directores
# ERCE_2019_QP3.rds              | # ERCE_2019_QD3.rds
# ERCE_2019_QP6.rds              | # ERCE_2019_QD6.rds
```

# Codigo 1.2: Inspeccionar los datos

<img src="./files/E6IT04.jpg" width="100%" />

``` r
# muestra de 10 casos de la variable E6IT04
library(dplyr)
erce::erce_2019_qa6 %>%
dplyr::sample_n(10) %>%
dplyr::select(IDSTUD, IDSCHOOL, COUNTRY, E6IT04) %>%
erce::remove_labels() %>%
tibble::as_tibble()
```

    ## # A tibble: 10 × 4
    ##      IDSTUD IDSCHOOL COUNTRY E6IT04
    ##       <dbl>    <dbl> <chr>    <dbl>
    ##  1 11000225     1100 MEX          1
    ##  2 11760121     1176 URY         NA
    ##  3 10920127     1092 CRI          1
    ##  4 11990103     1199 SLV          1
    ##  5 12830102     1283 SLV          1
    ##  6 10890103     1089 GTM          1
    ##  7 10390105     1039 GTM          1
    ##  8 10330114     1033 PAN          1
    ##  9 10510115     1051 PAN         NA
    ## 10 11290217     1129 SLV          1

-   El segundo problema a resolver, consiste en identificar el
    **contenido de los datos**.

    -   Una base de datos, para ser informativa, requiere de
        **suplementos** para que podamos producir resultados
        interpretables.

    -   Es decir, para que podamos contestar a una pregunta del tipo
        “qué proporción de estudiantes habla en el hogar, el mismo
        lenguaje del test y los cuestionarios”, necesitamos saber **qué
        pregunta** del instrumento recoge información pertinente a esta
        pregunta.

    -   Además requerimos saber como las **respuestas** de las personas
        fueron **codificadas** en la base de datos.

    -   Para estos fines, hay dos fuentes de información relevantes. Una
        es el **manual de usuario**, el cual contiene un libro de
        códigos plasmado sobre el cuestionario aplicado.

    -   Y por otro lado, podemos recurrir a la **meta-data** de la base
        de datos, la cual también nos permite acceder a la respuesta que
        representa cada valor digitado.

``` r
# mostrar metadata en R
labelled::look_for(erce::erce_2019_qa6)
```

    ##  pos variable  label                      col_type values                    
    ##  1   IDSTUD    Identificador del estudia~ dbl                                
    ##  2   IDCLASS   Identificador del aula     dbl                                
    ##  3   IDSCHOOL  Identificador de la escue~ dbl                                
    ##  4   IDCNTRY   Identificador del país     dbl+lbl  [32] Argentina            
    ##                                                    [76] Brasil               
    ##                                                    [170] Colombia            
    ##                                                    [188] Costa Rica          
    ##                                                    [192] Cuba                
    ##                                                    [214] República Dominicana
    ##                                                    [218] Ecuador             
    ##                                                    [222] El Salvador         
    ##                                                    [320] Guatemala           
    ##                                                    [340] Honduras            
    ##                                                    [484] México              
    ##                                                    [558] Nicaragua           
    ##                                                    [591] Panamá              
    ##                                                    [600] Paraguay            
    ##                                                    [604] Perú                
    ##                                                    [858] Uruguay             
    ##  5   COUNTRY   Acrónimo del país          chr+lbl  [ARG] Argentina           
    ##                                                    [BRA] Brasil              
    ##                                                    [COL] Colombia            
    ##                                                    [CRI] Costa Rica          
    ##                                                    [CUB] Cuba                
    ##                                                    [DOM] Dominican Republic  
    ##                                                    [ECU] Ecuador             
    ##                                                    [GTM] Argentina           
    ##                                                    [HND] Guatemala           
    ##                                                    [MEX] Mexico              
    ##                                                    [NIC] Nicaragua           
    ##                                                    [PAN] Panama              
    ##                                                    [PER] Peru                
    ##                                                    [PRY] Paraguay            
    ##                                                    [SLV] El Salvador         
    ##                                                    [URY] Uruguay             
    ##  6   STRATA    Identificar del estrato d~ dbl                                
    ##  7   GRADE     Grado                      dbl+lbl  [3] Tercer grado          
    ##                                                    [6] Sexto grado           
    ##  8   QA6       Cuestionario Presente (Sí~ dbl+lbl  [0] No                    
    ##                                                    [1] Sí                    
    ##  9   WT        Peso total del estudiante  dbl                                
    ##  10  WS        Peso normalizado (escalad~ dbl                                
    ##  11  WI        Peso al interior de la es~ dbl                                
    ##  12  WJ        Peso de la escuela (en ca~ dbl                                
    ##  13  E6IT01    ¿Cuántos años tienes?      dbl+lbl  [1] 10 años o menos.      
    ##                                                    [2] 11 años.              
    ##                                                    [3] 12 años.              
    ##                                                    [4] 13 años.              
    ##                                                    [5] 14 años.              
    ##                                                    [6] 15 años o más.        
    ##  14  E6IT02    ¿Eres niña o niño?         dbl+lbl  [1] Niña                  
    ##                                                    [2] Niño                  
    ##  15  E6IT03_01 Madre.                     dbl+lbl  [1] Sí                    
    ##                                                    [2] No                    
    ##  16  E6IT03_02 Padre.                     dbl+lbl  [1] Sí                    
    ##                                                    [2] No                    
    ##  17  E6IT03_03 Hermanos.                  dbl+lbl  [1] Sí                    
    ##                                                    [2] No                    
    ##  18  E6IT03_04 Abuelos.                   dbl+lbl  [1] Sí                    
    ##                                                    [2] No                    
    ##  19  E6IT03_05 Tíos.                      dbl+lbl  [1] Sí                    
    ##                                                    [2] No                    
    ##  20  E6IT03_06 Otros.                     dbl+lbl  [1] Sí                    
    ##                                                    [2] No                    
    ##  21  E6IT04    ¿Qué idioma hablan en tu ~ dbl+lbl  [1] <Lengua oficial>      
    ##                                                    [2] <Lengua extranjera>   
    ##                                                    [3] Otra lengua extranjer~
    ##                                                    [4] <Lengua indígena 1>   
    ##                                                    [5] <Lengua indígena 2>   
    ##                                                    [6] Otra lengua indígena. 
    ##  22  E6IT05    ¿Perteneces a alguna etni~ dbl+lbl  [1] Sí                    
    ##                                                    [2] No                    
    ##  23  E6IT05A   Si perteneces a una etnia~ dbl+lbl  [1] <Pueblo originario 1> 
    ##                                                    [2] <Pueblo originario 2> 
    ##                                                    [3] <Pueblo originario 3> 
    ##                                                    [4] <Pueblo originario 4> 
    ##                                                    [5] <Pueblo originario 5> 
    ##                                                    [6] Otro pueblo originari~
    ##  24  E6IT06    ¿Naciste en <país>?        dbl+lbl  [1] Sí                    
    ##                                                    [2] No                    
    ##  25  E6IT06A   Si NO naciste en <país>, ~ dbl                                
    ##  26  E6IT07    ¿Tu madre nació en <país>? dbl+lbl  [1] Sí                    
    ##                                                    [2] No                    
    ##                                                    [3] No sé                 
    ##  27  E6IT08    ¿Tu padre nació en <país>? dbl+lbl  [1] Sí                    
    ##                                                    [2] No                    
    ##                                                    [3] No sé                 
    ##  28  E6IT09    ¿Cuál es el nivel educati~ dbl+lbl  [1] No tiene estudios.    
    ##                                                    [2] <CINE-P 1-2> incomple~
    ##                                                    [3] <CINE-P 1-2> completa.
    ##                                                    [4] <CINE-P 3> incompleta.
    ##                                                    [5] <CINE-P 3> completa.  
    ##                                                    [6] <CINE-P 4> incompleta.
    ##                                                    [7] <CINE-P 4> completa.  
    ##                                                    [8] <CINE-P 5-6> incomple~
    ##                                                    [9] <CINE-P 5-6> completa.
    ##                                                    [10] <CINE-P 7-8> incompl~
    ##                                                    [11] <CINE-P 7-8> complet~
    ##                                                    [12] No sé / No aplica.   
    ##  29  E6IT10    ¿Cuántos libros hay en tu~ dbl+lbl  [1] No hay libros.        
    ##                                                    [2] Hay 10 o menos.       
    ##                                                    [3] Hay entre 11 y 20.    
    ##                                                    [4] Hay entre 21 y 30.    
    ##                                                    [5] Hay entre 31 y 50.    
    ##                                                    [6] Hay más de 51 a 100.  
    ##                                                    [7] Hay más de 100.       
    ##  30  E6IT11_01 Me gusta ser parte de est~ dbl+lbl  [1] Muy en desacuerdo     
    ##                                                    [2] En desacuerdo         
    ##                                                    [3] De acuerdo            
    ##                                                    [4] Muy de acuerdo        
    ##  31  E6IT11_02 Me siento orgulloso de se~ dbl+lbl  [1] Muy en desacuerdo     
    ##                                                    [2] En desacuerdo         
    ##                                                    [3] De acuerdo            
    ##                                                    [4] Muy de acuerdo        
    ##  32  E6IT11_03 Me gusta venir a esta esc~ dbl+lbl  [1] Muy en desacuerdo     
    ##                                                    [2] En desacuerdo         
    ##                                                    [3] De acuerdo            
    ##                                                    [4] Muy de acuerdo        
    ##  33  E6IT11_04 Mis profesores me hacen s~ dbl+lbl  [1] Muy en desacuerdo     
    ##                                                    [2] En desacuerdo         
    ##                                                    [3] De acuerdo            
    ##                                                    [4] Muy de acuerdo        
    ##  34  E6IT12_01 ¿Tienes tu propio libro d~ dbl+lbl  [1] Sí                    
    ##                                                    [2] No                    
    ##  35  E6IT12_02 ¿Tienes tu propio libro d~ dbl+lbl  [1] Sí                    
    ##                                                    [2] No                    
    ##  36  E6IT12_03 ¿Tienes tu propio libro d~ dbl+lbl  [1] Sí                    
    ##                                                    [2] No                    
    ##  37  E6IT12_04 ¿Tienes tus propios cuade~ dbl+lbl  [1] Sí                    
    ##                                                    [2] No                    
    ##  38  E6IT12_05 ¿Tienes tus propios lápic~ dbl+lbl  [1] Sí                    
    ##                                                    [2] No                    
    ##  39  E6IT12_06 ¿Tienes tu propio computa~ dbl+lbl  [1] Sí                    
    ##                                                    [2] No                    
    ##  40  E6IT13_01 Se rieron de mi o me insu~ dbl+lbl  [1] Nunca                 
    ##                                                    [2] Algunas veces         
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Todos o casi todos lo~
    ##  41  E6IT13_02 Me dejaron fuera de sus j~ dbl+lbl  [1] Nunca                 
    ##                                                    [2] Algunas veces         
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Todos o casi todos lo~
    ##  42  E6IT13_03 Dijeron mentiras sobre mí. dbl+lbl  [1] Nunca                 
    ##                                                    [2] Algunas veces         
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Todos o casi todos lo~
    ##  43  E6IT13_04 Me robaron algo.           dbl+lbl  [1] Nunca                 
    ##                                                    [2] Algunas veces         
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Todos o casi todos lo~
    ##  44  E6IT13_05 Me golpearon o me hiriero~ dbl+lbl  [1] Nunca                 
    ##                                                    [2] Algunas veces         
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Todos o casi todos lo~
    ##  45  E6IT13_06 Me obligaron hacer cosas ~ dbl+lbl  [1] Nunca                 
    ##                                                    [2] Algunas veces         
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Todos o casi todos lo~
    ##  46  E6IT13_07 Compartieron información ~ dbl+lbl  [1] Nunca                 
    ##                                                    [2] Algunas veces         
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Todos o casi todos lo~
    ##  47  E6IT13_08 Me amenazaron.             dbl+lbl  [1] Nunca                 
    ##                                                    [2] Algunas veces         
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Todos o casi todos lo~
    ##  48  E6IT14    Antes de entrar a primer ~ dbl+lbl  [1] Sí                    
    ##                                                    [2] No                    
    ##  49  E6IT15    ¿Cuál es el nivel de educ~ dbl+lbl  [1] <CINE-P 1>            
    ##                                                    [2] <CINE-P 2>            
    ##                                                    [3] <CINE-P 3>            
    ##                                                    [4] <CINE-P 4-5>          
    ##                                                    [5] <CINE-P 6>            
    ##                                                    [6] <CINE-P 7-8>          
    ##  50  E6IT16    ¿Cuántas veces has repeti~ dbl+lbl  [1] Nunca he repetido.    
    ##                                                    [2] Una vez.              
    ##                                                    [3] Dos veces o más.      
    ##                                                    [4] No sé, no recuerdo.   
    ##  51  E6IT17    Durante el último mes, ¿c~ dbl+lbl  [1] Ninguno.              
    ##                                                    [2] 1 día.                
    ##                                                    [3] 2 días.               
    ##                                                    [4] 3 días.               
    ##                                                    [5] 4 días o más.         
    ##                                                    [6] No sé / No me acuerdo.
    ##  52  E6IT18    Durante la semana pasada,~ dbl+lbl  [1] Ninguno.              
    ##                                                    [2] 1 día.                
    ##                                                    [3] 2 días.               
    ##                                                    [4] 3 días.               
    ##                                                    [5] 4 días o más.         
    ##                                                    [6] No sé / No me acuerdo.
    ##  53  E6IT19_01 Los profesores faltan a c~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] A veces               
    ##                                                    [3] Siempre o casi siempre
    ##  54  E6IT19_02 Los profesores llegan tar~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] A veces               
    ##                                                    [3] Siempre o casi siempre
    ##  55  E6IT19_03 Los profesores se van ant~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] A veces               
    ##                                                    [3] Siempre o casi siempre
    ##  56  E6IT20_01 Los profesores se interes~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  57  E6IT20_02 Los profesores se dan cue~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  58  E6IT20_03 Los profesores me animan ~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  59  E6IT20_04 Los profesores son simpát~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  60  E6IT20_05 Si estoy triste o enojado~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  61  E6IT20_06 Los profesores se enojan ~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  62  E6IT20_07 Los profesores saben exac~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  63  E6IT21_01 Durante la clase hay deso~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  64  E6IT21_02 El profesor tiene que esp~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  65  E6IT21_03 Cuando un estudiante part~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  66  E6IT21_04 Los estudiantes se compor~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  67  E6IT21_05 Nadie se distrae en la cl~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  68  E6IT22_01 El profesor pregunta si e~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  69  E6IT22_02 El profesor nos anima a t~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  70  E6IT22_03 El profesor pide que haga~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  71  E6IT22_04 El profesor me dice lo qu~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  72  E6IT22_05 Cuando me equivoco, el pr~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  73  E6IT22_06 El profesor nos pide que ~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  74  E6IT22_07 El profesor nos pide disc~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  75  E6IT22_08 El profesor nos motiva a ~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  76  E6IT22_09 El profesor me corrige to~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  77  E6IT22_10 El profesor nos pide corr~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  78  E6IT22_11 El profesor nos hace trab~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  79  E6IT23_01 El profesor tiene listos ~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  80  E6IT23_02 El profesor nos dice qué ~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  81  E6IT23_03 El profesor hace un resum~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  82  E6IT23_04 El profesor nos deja hace~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  83  E6IT24_01 En general me va bien en ~ dbl+lbl  [1] Muy en desacuerdo     
    ##                                                    [2] En desacuerdo         
    ##                                                    [3] De acuerdo            
    ##                                                    [4] Muy de acuerdo        
    ##  84  E6IT24_02 Soy bueno para resolver p~ dbl+lbl  [1] Muy en desacuerdo     
    ##                                                    [2] En desacuerdo         
    ##                                                    [3] De acuerdo            
    ##                                                    [4] Muy de acuerdo        
    ##  85  E6IT24_03 Confío en que me irá bien~ dbl+lbl  [1] Muy en desacuerdo     
    ##                                                    [2] En desacuerdo         
    ##                                                    [3] De acuerdo            
    ##                                                    [4] Muy de acuerdo        
    ##  86  E6IT24_04 Sigo intentando resolver ~ dbl+lbl  [1] Muy en desacuerdo     
    ##                                                    [2] En desacuerdo         
    ##                                                    [3] De acuerdo            
    ##                                                    [4] Muy de acuerdo        
    ##  87  E6IT24_05 Matemática se me hace más~ dbl+lbl  [1] Muy en desacuerdo     
    ##                                                    [2] En desacuerdo         
    ##                                                    [3] De acuerdo            
    ##                                                    [4] Muy de acuerdo        
    ##  88  E6IT24_06 Matemática se me hace más~ dbl+lbl  [1] Muy en desacuerdo     
    ##                                                    [2] En desacuerdo         
    ##                                                    [3] De acuerdo            
    ##                                                    [4] Muy de acuerdo        
    ##  89  E6IT24_07 Me pongo muy nervioso cua~ dbl+lbl  [1] Muy en desacuerdo     
    ##                                                    [2] En desacuerdo         
    ##                                                    [3] De acuerdo            
    ##                                                    [4] Muy de acuerdo        
    ##  90  E6IT25_01 Durante la clase hay deso~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  91  E6IT25_02 El profesor tiene que esp~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  92  E6IT25_03 Cuando un estudiante part~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  93  E6IT25_04 Los estudiantes se compor~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  94  E6IT25_05 Nadie se distrae en la cl~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  95  E6IT26_01 El profesor pregunta si e~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  96  E6IT26_02 El profesor nos anima a t~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  97  E6IT26_03 El profesor pide que haga~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  98  E6IT26_04 El profesor me dice lo qu~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  99  E6IT26_05 Cuando me equivoco, el pr~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  100 E6IT26_06 El profesor nos pide prop~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  101 E6IT26_07 El profesor nos pide inve~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  102 E6IT26_08 El profesor nos motiva a ~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  103 E6IT26_09 El profesor me corrige to~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  104 E6IT26_10 El profesor nos pide corr~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  105 E6IT26_11 El profesor nos hace trab~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  106 E6IT27_01 El profesor tiene listos ~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  107 E6IT27_02 El profesor nos dice qué ~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  108 E6IT27_03 El profesor hace un resum~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  109 E6IT27_04 El profesor nos deja hace~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  110 E6IT28_01 Durante la clase hay deso~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  111 E6IT28_02 El profesor tiene que esp~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  112 E6IT28_03 Cuando un estudiante part~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Algunas veces         
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  113 E6IT28_04 Los estudiantes se compor~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  114 E6IT28_05 Nadie se distrae en la cl~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  115 E6IT29_01 El profesor pregunta si e~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  116 E6IT29_02 El profesor nos anima a t~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  117 E6IT29_03 El profesor pide que haga~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  118 E6IT29_04 El profesor me dice lo qu~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  119 E6IT29_05 Cuando me equivoco, el pr~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  120 E6IT29_06 El profesor nos pide que ~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  121 E6IT29_07 El profesor nos pide expr~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  122 E6IT29_08 El profesor nos motiva a ~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  123 E6IT29_09 El profesor me corrige to~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  124 E6IT29_10 El profesor nos pide corr~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  125 E6IT29_11 El profesor nos hace trab~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  126 E6IT30_01 El profesor tiene listos ~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  127 E6IT30_02 El profesor nos dice qué ~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  128 E6IT30_03 El profesor hace un resum~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  129 E6IT30_04 El profesor nos deja hace~ dbl+lbl  [1] Nunca o casi nunca    
    ##                                                    [2] Pocas veces           
    ##                                                    [3] Muchas veces          
    ##                                                    [4] Siempre o casi siempre
    ##  130 E6IT31    Durante la semana pasada,~ dbl+lbl  [1] Ninguno.              
    ##                                                    [2] 1 día.                
    ##                                                    [3] 2 días.               
    ##                                                    [4] 3 días.               
    ##                                                    [5] 4 días o más.         
    ##                                                    [6] No sé / No me acuerdo.
    ##  131 E6IT32    En general, ¿cuánto tiemp~ dbl+lbl  [1] No estudio ni hago la~
    ##                                                    [2] Menos de una hora al ~
    ##                                                    [3] De 1 a 2 horas por dí~
    ##                                                    [4] Más de 2 horas por dí~
    ##  132 E6IT33_01 Me revisaron o ayudaron h~ dbl+lbl  [1] Ninguna vez           
    ##                                                    [2] Una o dos veces       
    ##                                                    [3] Tres o cuatro veces   
    ##                                                    [4] Todos o casi todos lo~
    ##  133 E6IT33_02 Me preguntaron si hice mi~ dbl+lbl  [1] Ninguna vez           
    ##                                                    [2] Una o dos veces       
    ##                                                    [3] Tres o cuatro veces   
    ##                                                    [4] Todos o casi todos lo~
    ##  134 E6IT33_03 Me preguntaron qué hice e~ dbl+lbl  [1] Ninguna vez           
    ##                                                    [2] Una o dos veces       
    ##                                                    [3] Tres o cuatro veces   
    ##                                                    [4] Todos o casi todos lo~
    ##  135 E6IT33_04 Me preguntaron qué califi~ dbl+lbl  [1] Ninguna vez           
    ##                                                    [2] Una o dos veces       
    ##                                                    [3] Tres o cuatro veces   
    ##                                                    [4] Todos o casi todos lo~
    ##  136 E6IT34    Además de asistir a la es~ dbl+lbl  [1] No                    
    ##                                                    [2] Sí, en la casa (por ~ 
    ##                                                    [3] Sí, fuera de la casa. 
    ##  137 E6IT34A   ¿Cuánto trabajas en la ca~ dbl+lbl  [1] Lo hago solo los fine~
    ##                                                    [2] Lo hago por poco rato~
    ##                                                    [3] Lo hago la mayor part~
    ##  138 E6IT34B   ¿Cuánto trabajas fuera de~ dbl+lbl  [1] Lo hago solo los fine~
    ##                                                    [2] Lo hago por poco rato~
    ##                                                    [3] Lo hago la mayor part~
    ##  139 E6IT35    Si trabajas, ¿te pagan di~ dbl+lbl  [1] Sí.                   
    ##                                                    [2] No.                   
    ##                                                    [3] No, pero me dan cosas~
    ##  140 E6IT36_01 ¿Fue difícil responder es~ dbl+lbl  [1] Sí                    
    ##                                                    [2] No                    
    ##  141 E6IT36_02 ¿Te gustó este cuestionar~ dbl+lbl  [1] Sí                    
    ##                                                    [2] No                    
    ##  142 BRR1      Pesos Replicados 1         dbl                                
    ##  143 BRR2      Pesos Replicados 2         dbl                                
    ##  144 BRR3      Pesos Replicados 3         dbl                                
    ##  145 BRR4      Pesos Replicados 4         dbl                                
    ##  146 BRR5      Pesos Replicados 5         dbl                                
    ##  147 BRR6      Pesos Replicados 6         dbl                                
    ##  148 BRR7      Pesos Replicados 7         dbl                                
    ##  149 BRR8      Pesos Replicados 8         dbl                                
    ##  150 BRR9      Pesos Replicados 9         dbl                                
    ##  151 BRR10     Pesos Replicados 10        dbl                                
    ##  152 BRR11     Pesos Replicados 11        dbl                                
    ##  153 BRR12     Pesos Replicados 12        dbl                                
    ##  154 BRR13     Pesos Replicados 13        dbl                                
    ##  155 BRR14     Pesos Replicados 14        dbl                                
    ##  156 BRR15     Pesos Replicados 15        dbl                                
    ##  157 BRR16     Pesos Replicados 16        dbl                                
    ##  158 BRR17     Pesos Replicados 17        dbl                                
    ##  159 BRR18     Pesos Replicados 18        dbl                                
    ##  160 BRR19     Pesos Replicados 19        dbl                                
    ##  161 BRR20     Pesos Replicados 20        dbl                                
    ##  162 BRR21     Pesos Replicados 21        dbl                                
    ##  163 BRR22     Pesos Replicados 22        dbl                                
    ##  164 BRR23     Pesos Replicados 23        dbl                                
    ##  165 BRR24     Pesos Replicados 24        dbl                                
    ##  166 BRR25     Pesos Replicados 25        dbl                                
    ##  167 BRR26     Pesos Replicados 26        dbl                                
    ##  168 BRR27     Pesos Replicados 27        dbl                                
    ##  169 BRR28     Pesos Replicados 28        dbl                                
    ##  170 BRR29     Pesos Replicados 29        dbl                                
    ##  171 BRR30     Pesos Replicados 30        dbl                                
    ##  172 BRR31     Pesos Replicados 31        dbl                                
    ##  173 BRR32     Pesos Replicados 32        dbl                                
    ##  174 BRR33     Pesos Replicados 33        dbl                                
    ##  175 BRR34     Pesos Replicados 34        dbl                                
    ##  176 BRR35     Pesos Replicados 35        dbl                                
    ##  177 BRR36     Pesos Replicados 36        dbl                                
    ##  178 BRR37     Pesos Replicados 37        dbl                                
    ##  179 BRR38     Pesos Replicados 38        dbl                                
    ##  180 BRR39     Pesos Replicados 39        dbl                                
    ##  181 BRR40     Pesos Replicados 40        dbl                                
    ##  182 BRR41     Pesos Replicados 41        dbl                                
    ##  183 BRR42     Pesos Replicados 42        dbl                                
    ##  184 BRR43     Pesos Replicados 43        dbl                                
    ##  185 BRR44     Pesos Replicados 44        dbl                                
    ##  186 BRR45     Pesos Replicados 45        dbl                                
    ##  187 BRR46     Pesos Replicados 46        dbl                                
    ##  188 BRR47     Pesos Replicados 47        dbl                                
    ##  189 BRR48     Pesos Replicados 48        dbl                                
    ##  190 BRR49     Pesos Replicados 49        dbl                                
    ##  191 BRR50     Pesos Replicados 50        dbl                                
    ##  192 BRR51     Pesos Replicados 51        dbl                                
    ##  193 BRR52     Pesos Replicados 52        dbl                                
    ##  194 BRR53     Pesos Replicados 53        dbl                                
    ##  195 BRR54     Pesos Replicados 54        dbl                                
    ##  196 BRR55     Pesos Replicados 55        dbl                                
    ##  197 BRR56     Pesos Replicados 56        dbl                                
    ##  198 BRR57     Pesos Replicados 57        dbl                                
    ##  199 BRR58     Pesos Replicados 58        dbl                                
    ##  200 BRR59     Pesos Replicados 59        dbl                                
    ##  201 BRR60     Pesos Replicados 60        dbl                                
    ##  202 BRR61     Pesos Replicados 61        dbl                                
    ##  203 BRR62     Pesos Replicados 62        dbl                                
    ##  204 BRR63     Pesos Replicados 63        dbl                                
    ##  205 BRR64     Pesos Replicados 64        dbl                                
    ##  206 BRR65     Pesos Replicados 65        dbl                                
    ##  207 BRR66     Pesos Replicados 66        dbl                                
    ##  208 BRR67     Pesos Replicados 67        dbl                                
    ##  209 BRR68     Pesos Replicados 68        dbl                                
    ##  210 BRR69     Pesos Replicados 69        dbl                                
    ##  211 BRR70     Pesos Replicados 70        dbl                                
    ##  212 BRR71     Pesos Replicados 71        dbl                                
    ##  213 BRR72     Pesos Replicados 72        dbl                                
    ##  214 BRR73     Pesos Replicados 73        dbl                                
    ##  215 BRR74     Pesos Replicados 74        dbl                                
    ##  216 BRR75     Pesos Replicados 75        dbl                                
    ##  217 BRR76     Pesos Replicados 76        dbl                                
    ##  218 BRR77     Pesos Replicados 77        dbl                                
    ##  219 BRR78     Pesos Replicados 78        dbl                                
    ##  220 BRR79     Pesos Replicados 79        dbl                                
    ##  221 BRR80     Pesos Replicados 80        dbl                                
    ##  222 BRR81     Pesos Replicados 81        dbl                                
    ##  223 BRR82     Pesos Replicados 82        dbl                                
    ##  224 BRR83     Pesos Replicados 83        dbl                                
    ##  225 BRR84     Pesos Replicados 84        dbl                                
    ##  226 BRR85     Pesos Replicados 85        dbl                                
    ##  227 BRR86     Pesos Replicados 86        dbl                                
    ##  228 BRR87     Pesos Replicados 87        dbl                                
    ##  229 BRR88     Pesos Replicados 88        dbl                                
    ##  230 BRR89     Pesos Replicados 89        dbl                                
    ##  231 BRR90     Pesos Replicados 90        dbl                                
    ##  232 BRR91     Pesos Replicados 91        dbl                                
    ##  233 BRR92     Pesos Replicados 92        dbl                                
    ##  234 BRR93     Pesos Replicados 93        dbl                                
    ##  235 BRR94     Pesos Replicados 94        dbl                                
    ##  236 BRR95     Pesos Replicados 95        dbl                                
    ##  237 BRR96     Pesos Replicados 96        dbl                                
    ##  238 BRR97     Pesos Replicados 97        dbl                                
    ##  239 BRR98     Pesos Replicados 98        dbl                                
    ##  240 BRR99     Pesos Replicados 99        dbl                                
    ##  241 BRR100    Pesos Replicados 100       dbl                                
    ##  242 MAT_1     Matemáticas (valor plausi~ dbl                                
    ##  243 MAT_2     Matemáticas (valor plausi~ dbl                                
    ##  244 MAT_3     Matemáticas (valor plausi~ dbl                                
    ##  245 MAT_4     Matemáticas (valor plausi~ dbl                                
    ##  246 MAT_5     Matemáticas (valor plausi~ dbl                                
    ##  247 MAT_L1    Matemáticas (nivel de log~ chr                                
    ##  248 MAT_L2    Matemáticas (nivel de log~ chr                                
    ##  249 MAT_L3    Matemáticas (nivel de log~ chr                                
    ##  250 MAT_L4    Matemáticas (nivel de log~ chr                                
    ##  251 MAT_L5    Matemáticas (nivel de log~ chr                                
    ##  252 LAN_1     Lenguaje (valor plausible~ dbl                                
    ##  253 LAN_2     Lenguaje (valor plausible~ dbl                                
    ##  254 LAN_3     Lenguaje (valor plausible~ dbl                                
    ##  255 LAN_4     Lenguaje (valor plausible~ dbl                                
    ##  256 LAN_5     Lenguaje (valor plausible~ dbl                                
    ##  257 LAN_L1    Lenguaje (nivel de logro,~ chr                                
    ##  258 LAN_L2    Lenguaje (nivel de logro,~ chr                                
    ##  259 LAN_L3    Lenguaje (nivel de logro,~ chr                                
    ##  260 LAN_L4    Lenguaje (nivel de logro,~ chr                                
    ##  261 LAN_L5    Lenguaje (nivel de logro,~ chr                                
    ##  262 SCI_1     Ciencias (valor plausible~ dbl                                
    ##  263 SCI_2     Ciencias (valor plausible~ dbl                                
    ##  264 SCI_3     Ciencias (valor plausible~ dbl                                
    ##  265 SCI_4     Ciencias (valor plausible~ dbl                                
    ##  266 SCI_5     Ciencias (valor plausible~ dbl                                
    ##  267 SCI_L1    Ciencias (nivel de logro,~ chr                                
    ##  268 SCI_L2    Ciencias (nivel de logro,~ chr                                
    ##  269 SCI_L3    Ciencias (nivel de logro,~ chr                                
    ##  270 SCI_L4    Ciencias (nivel de logro,~ chr                                
    ##  271 SCI_L5    Ciencias (nivel de logro,~ chr                                
    ##  272 SEX       Sexo de los estudiantes    dbl+lbl  [0] Niño                  
    ##                                                    [1] Niña                  
    ##  273 DEP       Dependencia de la escuela  dbl+lbl  [1] Público               
    ##                                                    [2] Privado               
    ##                                                    [3] Otro                  
    ##  274 RURAL     Ubicación de la escuela    dbl+lbl  [0] Urbano                
    ##                                                    [1] Rural                 
    ##  275 EDU       Educación Máxima de los p~ dbl+lbl  [0] Sin Educación Terciar~
    ##                                                    [1] Educación Terciaria   
    ##  276 SPESC     Sentido de pertenencia a ~ dbl                                
    ##  277 VIOES     Violencia al interior de ~ dbl                                
    ##  278 ASISP     Asistencia y puntualidad ~ dbl                                
    ##  279 CLBIE     Interés por el bienestar ~ dbl                                
    ##  280 DISMA     Disrupción en el aula de ~ dbl                                
    ##  281 AAEMA     Apoyo al aprendizaje de l~ dbl                                
    ##  282 ORGMA     Organización de la clase ~ dbl                                
    ##  283 EFMAT     Autoeficacia en matemátic~ dbl                                
    ##  284 DISCI     Disrupción en el aula de ~ dbl                                
    ##  285 AAECI     Apoyo al aprendizaje de l~ dbl                                
    ##  286 ORGCI     Organización de la clase ~ dbl                                
    ##  287 DISLA     Disrupción en el aula de ~ dbl                                
    ##  288 AAELA     Apoyo al aprendizaje de l~ dbl                                
    ##  289 ORGLA     Organización de la clase ~ dbl                                
    ##  290 INVAP     Involucramiento parental ~ dbl                                
    ##  291 ISECF     Índice socioeconómico de ~ dbl                                
    ##  292 AURES     Autorregulación escolar    dbl                                
    ##  293 EMPAT     Empatía                    dbl                                
    ##  294 APDIV     Apertura a la diversidad   dbl                                
    ##  295 EDAD      Edad del estudiante        dbl                                
    ##  296 PREE      Asistencia del estudiante~ dbl+lbl  [0] No                    
    ##                                                    [1] Sí                    
    ##  297 REPC      Repitencia                 dbl+lbl  [0] Nunca                 
    ##                                                    [1] Una o más veces       
    ##  298 AUSE      Inasistencia a la escuela  dbl+lbl  [0] Menos de una vez al m~
    ##                                                    [1] Dos o más veces al mes
    ##  299 ATRE      Impuntualidad en la asist~ dbl+lbl  [0] Ningún día            
    ##                                                    [1] Algunos o casi todos ~
    ##  300 LIBH      Cantidad de libros en el ~ dbl+lbl  [0] No hay libros         
    ##                                                    [1] Hay 10 o menos        
    ##                                                    [2] Hay entre 11 y 20     
    ##                                                    [3] Hay entre 21 y 30     
    ##                                                    [4] Hay entre 31 y 50     
    ##                                                    [5] Hay entre 51 y 100    
    ##                                                    [6] Hay más de 100        
    ##  301 TSTU      Días de estudio a la sema~ dbl+lbl  [0] Ninguno               
    ##                                                    [1] Algunos o casi todos ~
    ##  302 INDI      Pertenencia del estudiant~ dbl+lbl  [0] No                    
    ##                                                    [1] Sí                    
    ##  303 IMMI      Inmigrante                 dbl+lbl  [0] Nació en el país      
    ##                                                    [1] No nació en el país, ~

# Codigo 1.3: Variables de diseño

## Variables de diseño

``` r
# variables de diseño
library(dplyr)
erce::erce_2019_qa6 %>%
dplyr::sample_n(10) %>%
dplyr::select(COUNTRY, STRATA, IDSCHOOL, IDSTUD, WT, WJ, WI) %>%
labelled::lookfor_to_long_format() %>%
tibble::as_tibble()
```

    ## # A tibble: 10 × 7
    ##    COUNTRY                    STRATA IDSCHOOL   IDSTUD     WT    WJ    WI
    ##    <chr+lbl>                   <dbl>    <dbl>    <dbl>  <dbl> <dbl> <dbl>
    ##  1 DOM [Dominican Republic] 62141111     1092 10920319  25.5   8.49 3.00 
    ##  2 NIC [Nicaragua]          65582112     1032 10320103  33.0  71.9  0.459
    ##  3 CUB [Cuba]               61921111     1196 11960406  17.6   4.39 4.00 
    ##  4 PER [Peru]               66042111     1118 11180102  73.1  18.3  4    
    ##  5 PER [Peru]               66042111     1247 12470221  75.8  24.2  3.13 
    ##  6 CUB [Cuba]               61921111     1060 10600224  13.4   6.52 2.06 
    ##  7 PER [Peru]               66042111     1044 10440215  62.7  31.3  2.00 
    ##  8 URY [Uruguay]            68582111     1237 12370318   7.93  2.55 3.11 
    ##  9 ARG [Argentina]          60322111     1152 11520114 215.   35.9  6    
    ## 10 URY [Uruguay]            68582111     1126 11260213   8.35  3.86 2.16

## Muestra de valores de diseño

``` r
# muestra de valores de variables de diseño
library(dplyr)
erce::erce_2019_qa6 %>%
dplyr::sample_n(10) %>%
dplyr::select(COUNTRY, STRATA, IDSCHOOL, IDSTUD, WT, WJ, WI) %>%
erce::remove_labels() %>%
tibble::as_tibble()
```

    ## # A tibble: 10 × 7
    ##    COUNTRY   STRATA IDSCHOOL   IDSTUD     WT     WJ    WI
    ##    <chr>      <dbl>    <dbl>    <dbl>  <dbl>  <dbl> <dbl>
    ##  1 SLV     62222112     1213 12130114   9.80   9.76  1.00
    ##  2 PRY     66002312     2213 22130103  69.6   47.4   1.47
    ##  3 COL     61702121     1075 10750226 144.    69.6   2.07
    ##  4 ECU     62182121     1232 12320101  54.6   51.7   1.06
    ##  5 CUB     61921112     1057 10570105  25.8   25.5   1.01
    ##  6 COL     61702311     1166 11660132 186.   133.    1.40
    ##  7 URY     68582111     1049 10490125   5.71   2.86  2   
    ##  8 DOM     62141111     1002 10020107  37.0   18.5   2   
    ##  9 BRA     60762111     1134 11340218 626.   203.    3.09
    ## 10 ARG     60322111     1227 12270325 162.    46.0   3.52

-   Dependiendo de qué tipo de pregunta o preguntas queramos abordar,
    necesitamos saber como manejar las **variables de diseño del
    estudio**.

    -   El escenario más sencillo, es cuando queremos trabajar con los
        datos de un sólo país.

    -   Sin embargo, cuando queremos producir resultados empleando más
        de un país, es posible que sea necesario tratar a las variables
        de escuelas, estratos, y pesos de diferente forma, para producir
        resultados para la región.

    -   De la misma forma, si queremos producir resultados combinando a
        la población de estudiantes de Tercer y Sexto grado, debemos
        tomar decisiones respecto a como tratar a las variables de
        diseño (e.g., escuelas, estratos, y pesos muestrales).

    -   Finalmente, si queremos vincular resultados de TERCE y ERCE,
        tambien debemos tomar decisiones de qué haremos con las
        variables de diseño (e.g., escuelas, estratos, y pesos
        muestrales).

> **Nota**: Los estudios de gran escala permiten realizar comparaciones
> con datos que empleen un diseño similar, permitiendo comparaciones con
> otros países, con otros grados, y con datos previos. Pero se requiere
> realizar algún tratamiento sobre las variables de diseño, de modo que
> el cálculo de errores, y la expansión de observaciones sea adecuada.

# Codigo 1.4: Dirección de las variables de respuesta

<img src="./files/DDIT33.jpg" width="100%" />

``` r
# muestra de valores de variables de diseño
library(dplyr)
erce::erce_2019_qd6 %>%
dplyr::select(DDIT33_07) %>%
labelled::lookfor()
```

    ##  pos variable  label                col_type values
    ##  1   DDIT33_07 Conexión a Internet. dbl+lbl  [1] Sí
    ##                                              [2] No

-   Por convención, **los valores de digitación de respuestas observadas
    se asignan en secuencias de izquierda a derecha**. De este modo, la
    primera opción de respuesta se digita como 1, la segunda como 2, y
    así sucesivamente.

    -   Considerando la regla anterior, es posible que, para extraer la
        información deseada respecto a una pregunta, el usuario
        secundario requiera **crear variables nuevas** empleando la
        información original.

    -   La variable **DDIT33_07**, nos permite obtener que porcentaje de
        estudiantes, en un país posee conexión a internet en sus
        escuelas.

    -   Si bien la variable **DDIT33_07** contiene la información de
        interés, la manera en que estan digitados los valores
        originales, no necesariamente nos facilita el trabajo para
        obtener el porcentaje de interés.

    -   De este modo, es común que previo a la generación de resultados,
        los usuarios secundarios requieran **transformar las respuestas
        digitadas**, a variables que entreguen la información buscada
        por las preguntas de interés.

> **Nota**: En este ejemplo, una forma de generar resultados consistiría
> en convertir los valores 2, en valores 0, generando otra variable, y
> con esta nueva variable calcular los porcentajes esperados.

# Codigo 1.5: Transferibilidad

<img src="./files/workflow_2.png" width="100%" />

-   Es común que la realización de ciertos análisis estadísticos
    requieran ser realizados en **diferentes software**.

-   También es común que los usuarios secundarios **colaboren con otras
    personas**, y estas otras personas empleen software diferentes a las
    que se encuentra empleando la primera persona.

-   Le llamaremos problema de **transferibilidad**, al escenario en que
    esté en juego qué tan transferibles son los datos originales a otras
    plataformas de anáisis de datos.

-   Este problema, se resuelve comúnmente, mediante la **exportación de
    datos** de un software a otro, empleando formatos determinados.

-   De este modo, es común que previo a la generación de resultados, los
    usuarios secundarios requieran **transformar las respuestas
    digitadas**, a variables que entreguen la información buscada por
    las preguntas de interés.

-   La importacion de datos, la identificación del contenido de los
    datos, la identificación de las variables de diseño, la preparación
    de variables, y la exportación de datos, previos a la generación de
    resultados, son todas etapas que las podemos considerar parte de un
    **proceso iterativo.** En otras palabras, que lo haremos no solo una
    vez, sino varias veces.

*A continuación, revisaremos algunos ejemplos de estos procesos,
empleando datos de ERCE 2019*.

------------------------------------------------------------------------

class: middle, inverse

background-image: url(img/background_02.jpeg) background-size: 100%

.line_space_01\[ Problemas y solluciones\] .line_space_01\[ .text_250\[
.bold_white\[ Abrir datos\]\]\] .line_space_01\[ Problema 1: Cómo cargar
los datos de ERCE 2019 en R\]

<br> <br>

|                                                                                        |
|----------------------------------------------------------------------------------------|
| background-image: url(img/background_03.jpeg) background-size: 100%                    |
| Problema 1: **Abrir los datos**                                                        |
| .pull_l\_50_t\_080\[                                                                   |
| La manera más sencilla de abrir los datos en R, es emplear la librería.                |
| \`\`\`r #———————————————— # Abrir los datos desde la librería erce #————————————————   |
| erce_a6 \<- erce::erce_2019_qa6 \`\`\`                                                 |
| Otra forma consiste en abrir los datos empleando los archivos `.rds`                   |
| \`\`\`r #———————————————— # abrir los datos empleando el archivo rds #———————————————— |
| data_folder \<- ‘/Users/d/ERCE 2019/’                                                  |
| erce_a6 \<- readRDS(paste0(data_folder, ‘ERCE_2019_QA6.rds’)) \`\`\`                   |
| En R también es posible abrir los datos en formato STATA `.dta`                        |
| \`\`\`r #———————————————— # abrir los datos de formato STATA #————————————————         |
| data_folder \<- ‘/Users/d/ERCE 2019/’                                                  |
| erce_a6 \<- haven::read_dta(paste0(data_folder, ‘ERCE_2019_QA6.dta’)) \`\`\`           |
| Se procede de forma similar para abrir los datos en formato SPSS `.sav`                |
| \`\`\`r #———————————————— # abrir los datos de formato SPSS #————————————————          |
| data_folder \<- ‘/Users/d/ERCE 2019/’                                                  |
| erce_a6 \<- haven::read_sav(paste0(data_folder, ‘ERCE_2019_QA6.sav’)) \`\`\`           |
| \]                                                                                     |

.pull_r\_50_t\_080\[\]

–

La segunda forma, requiere que definamos el objeto `data_folder`. Esta
es una dirección en sus computadores, donde los archivos de datos se
encuentran alojados. {{content}}

–

La tercera y cuarta forma son equivalentes a la segunda forma. La única
diferencia es que se encuentran abriendo los datos en otros formatos, en
formatos STATA y SPSS respectivamente.

|                                                                                        |
|----------------------------------------------------------------------------------------|
| background-image: url(img/background_03.jpeg) background-size: 100%                    |
| Problema 1: **Abrir los datos**                                                        |
| .pull_l\_50_t\_080\[                                                                   |
| La manera más sencilla de abrir los datos en R, es emplear la librería.                |
| \`\`\`r #———————————————— # Abrir los datos desde la librería erce #————————————————   |
| erce_a6 \<- erce::erce_2019_qa6 \`\`\`                                                 |
| Otra forma consiste en abrir los datos empleando los archivos `.rds`                   |
| \`\`\`r #———————————————— # abrir los datos empleando el archivo rds #———————————————— |
| data_folder \<- ‘/Users/d/ERCE 2019/’                                                  |
| erce_a6 \<- readRDS(paste0(data_folder, ‘ERCE_2019_QA6.rds’)) \`\`\`                   |
| En R también es posible abrir los datos en formato STATA `.dta`                        |
| \`\`\`r #———————————————— # abrir los datos de formato STATA #————————————————         |
| data_folder \<- ‘/Users/d/ERCE 2019/’                                                  |
| erce_a6 \<- haven::read_dta(paste0(data_folder, ‘ERCE_2019_QA6.dta’)) \`\`\`           |
| Se procede de forma similar para abrir los datos en formato SPSS `.sav`                |
| \`\`\`r #———————————————— # abrir los datos de formato SPSS #————————————————          |
| data_folder \<- ‘/Users/d/ERCE 2019/’                                                  |
| erce_a6 \<- haven::read_sav(paste0(data_folder, ‘ERCE_2019_QA6.sav’)) \`\`\`           |
| \]                                                                                     |

.pull_r\_50_t\_080\[\]

------------------------------------------------------------------------

class: middle, inverse

background-image: url(img/background_02.jpeg) background-size: 100%

.line_space_01\[ Problemas y soluciones\] .line_space_01\[ .text_250\[
.bold_white\[ Inspeccionar el contenido de los datos\]\]\]
.line_space_01\[ Problema 2: Cómo saber cuál es el contenido de los
datos\]

<br> <br>

|                                                                                                                                     |
|-------------------------------------------------------------------------------------------------------------------------------------|
| background-image: url(img/background_03.jpeg) background-size: 100%                                                                 |
| Problema 2: **Inspeccionar el contenido de los datos**                                                                              |
| .pull_l\_50_t\_080\[                                                                                                                |
| \- Una vez que los datos se encuentran abiertos o cargados, lo siguiente que necesitamos es poder **ver su contenido**.             |
| \- Existen **diferentes formas** de inspeccionar los datos en R, una vez que estos se encuentran cargados en la sesión. {{content}} |
| \]                                                                                                                                  |

-   Una forma global de inspeccionar los datos, es emplear el comando
    `dplyr::glimpse`. Este nos entrega el listado de variables, su tipo,
    y una muestra de los valores contenidos en cada columna de la base
    de datos.

–

.pull_r\_50_t\_080\[\]

|                                                                                                                                                                                                                                                                                                                                                                                                                    |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| background-image: url(img/background_03.jpeg) background-size: 100%                                                                                                                                                                                                                                                                                                                                                |
| Problema 2: **Inspeccionar el contenido de los datos**                                                                                                                                                                                                                                                                                                                                                             |
| .pull_l\_50_t\_080\[                                                                                                                                                                                                                                                                                                                                                                                               |
| \- Una vez que los datos se encuentran abiertos o cargadaos, lo siguiente que necesitamos es poder **ver su contenido**.                                                                                                                                                                                                                                                                                           |
| \- Existen **diferentes formas** de inspeccionar los datos en R, una vez que estos se encuentran cargados en la sesión.                                                                                                                                                                                                                                                                                            |
| \- Una forma global de inspeccionar los datos, es emplear el comando `dplyr::glimpse`. Este nos entrega el listado de variables, su tipo, y una muestra de los valores contenidos en cada columna de la base de datos.                                                                                                                                                                                             |
| \- Otra forma de inspeccionar los datos, es emplear las funciones de la librería `labelled`. Por ejemplo, empleando el comando `labelled::lookfor` podemos acceder a la meta data de los datos. Una vez aplicado este comando, podemos acceder a la descripción de las variables. Y, para el caso de las variables categóricas, al significado de los valores contenidos en cada columna (e.g., IDCNTRY, COUNTRY). |
| \]                                                                                                                                                                                                                                                                                                                                                                                                                 |

.pull_r\_50_t\_080\[\]

|                                                                                                                                                                                                                                                                                                                                                                                                                    |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| background-image: url(img/background_03.jpeg) background-size: 100%                                                                                                                                                                                                                                                                                                                                                |
| Problema 2: **Inspeccionar el contenido de los datos**                                                                                                                                                                                                                                                                                                                                                             |
| .pull_l\_50_t\_080\[                                                                                                                                                                                                                                                                                                                                                                                               |
| \- Una vez que los datos se encuentran abiertos o cargadaos, lo siguiente que necesitamos es poder **ver su contenido**.                                                                                                                                                                                                                                                                                           |
| \- Existen **diferentes formas** de inspeccionar los datos en R, una vez que estos se encuentran cargados en la sesión.                                                                                                                                                                                                                                                                                            |
| \- Una forma global de inspeccionar los datos, es emplear el comando `dplyr::glimpse`. Este nos entrega el listado de variables, su tipo, y una muestra de los valores contenidos en cada columna de la base de datos.                                                                                                                                                                                             |
| \- Otra forma de inspeccionar los datos, es emplear las funciones de la librería `labelled`. Por ejemplo, empleando el comando `labelled::lookfor` podemos acceder a la meta data de los datos. Una vez aplicado este comando, podemos acceder a la descripción de las variables. Y, para el caso de las variables categóricas, al significado de los valores contenidos en cada columna (e.g., IDCNTRY, COUNTRY). |
| \- También es posible generar un libro de códigos con `labelled`, y guardar este libro de códigos en un archivo excel.                                                                                                                                                                                                                                                                                             |
| \]                                                                                                                                                                                                                                                                                                                                                                                                                 |

.pull_r\_50_t\_080\[\]

|                                                                                                                                                                                                                                                                                                                                                                                                                    |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| background-image: url(img/background_03.jpeg) background-size: 100%                                                                                                                                                                                                                                                                                                                                                |
| Problema 2: **Inspeccionar el contenido de los datos**                                                                                                                                                                                                                                                                                                                                                             |
| .pull_l\_50_t\_080\[                                                                                                                                                                                                                                                                                                                                                                                               |
| \- Una vez que los datos se encuentran abiertos o cargadaos, lo siguiente que necesitamos es poder **ver su contenido**.                                                                                                                                                                                                                                                                                           |
| \- Existen **diferentes formas** de inspeccionar los datos en R, una vez que estos se encuentran cargados en la sesión.                                                                                                                                                                                                                                                                                            |
| \- Una forma global de inspeccionar los datos, es emplear el comando `dplyr::glimpse`. Este nos entrega el listado de variables, su tipo, y una muestra de los valores contenidos en cada columna de la base de datos.                                                                                                                                                                                             |
| \- Otra forma de inspeccionar los datos, es emplear las funciones de la librería `labelled`. Por ejemplo, empleando el comando `labelled::lookfor` podemos acceder a la meta data de los datos. Una vez aplicado este comando, podemos acceder a la descripción de las variables. Y, para el caso de las variables categóricas, al significado de los valores contenidos en cada columna (e.g., IDCNTRY, COUNTRY). |
| \- También es posible generar un libro de códigos con `labelled`, y guardar este libro de códigos en un archivo **excel**.                                                                                                                                                                                                                                                                                         |
| \]                                                                                                                                                                                                                                                                                                                                                                                                                 |
| .pull_r\_50_t\_080\[                                                                                                                                                                                                                                                                                                                                                                                               |
| <img src="./files/erce_a6_codebook.jpg" width="100%" />                                                                                                                                                                                                                                                                                                                                                            |
| \]                                                                                                                                                                                                                                                                                                                                                                                                                 |

class: middle, inverse

background-image: url(img/background_02.jpeg) background-size: 100%

.line_space_01\[ Problemas y Soluciones\] .line_space_01\[ .text_250\[
.bold_white[Variables de diseño](#variables-de-diseño)\]\]
.line_space_01\[ Cuáles son las variables de diseño\]

<br> <br>

|                                                                           |
|---------------------------------------------------------------------------|
| background-image: url(img/background_03.jpeg) background-size: 100%       |
| Problema 3: **Variables de diseño** (cuáles son las variables de diseño)  |
| .pull_l\_50_t\_080\[                                                      |
| \- Los estudios de gran escala poseen diferentes **variables de diseño**. |
| \]                                                                        |

.pull_r\_50_t\_080\[\]

|                                                                           |
|---------------------------------------------------------------------------|
| background-image: url(img/background_03.jpeg) background-size: 100%       |
| Problema 3: **Variables de diseño** (cuáles son las variables de diseño)  |
| .pull_l\_50_t\_080\[                                                      |
| \- Los estudios de gran escala poseen diferentes **variables de diseño**. |
| \- Entre las más comunes encontramos a:                                   |
| \+ Las variables de identificación de los **clusters**:                   |
| \+ El identificador de paéses (**IDCNTRY**)                               |
| \+ El identificador de estratos (**STRATA**)                              |
| \+ El identificador de escuelas (**IDSCHOOL**)                            |
| \+ El identificador de estudiantes (**IDSTUD**)                           |
| \+ Las variables de **pesos** de las observacinoes:                       |
| \+ Pesos muestrales totales (**WT**)                                      |
| \+ Pesos muestrales escalados (i.e., *senate weights*) (**WS**)           |
| \+ Peso de los estudiantes al interior de las escurlas (**WI**)           |
| \+ Pesos de las escuelas (**WJ**)                                         |
| \+ Pesos Replicados (**BRR1-BRR100**)                                     |
| \]                                                                        |

.pull_r\_50_t\_080\[\]

------------------------------------------------------------------------

class: middle, inverse

background-image: url(img/background_02.jpeg) background-size: 100%

.line_space_01\[ Problemas y soluciones\] .line_space_01\[ .text_250\[
.bold_white[Variables de diseño](#variables-de-diseño)\]\]
.line_space_01\[ Problema 3: Qué hacer con las variables de diseño, para
obtener resultados de la región\]

<br> <br>

|                                                                                                                                                                                                                                                                                                                                                                   |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| background-image: url(img/background_03.jpeg) background-size: 100%                                                                                                                                                                                                                                                                                               |
| Problema 3: **Variables de diseño** (cómo producir resultados para la región)                                                                                                                                                                                                                                                                                     |
| .pull_l\_50_t\_080\[                                                                                                                                                                                                                                                                                                                                              |
| \- Los **pesos muestrales**, en particular el peso total de las observaciones (**WT**) expande las observaciones al total esperado de la población de interés.                                                                                                                                                                                                    |
| \- Si empleáramos este peso, para tratar de reproducir los resultados regionales sobre los niveles de lectura, nuestro **estimado estaría distorsionado.**                                                                                                                                                                                                        |
| \- Los porcentajes de nivel de lectura, estarían siendo calculados **empleando el total esperado** de la población de cada país. Lo anterior, tiene como consecuencia que, países más grandes como Brasil y Mexico, contribuyen con más observaciones esperadas, en contraste a países con una población de estudiantes de menor tamaño como Uruguay, y Colombia. |
| \- Para garantizar que cada uno de los países contribuya de forma equivalente, requerimos emplear el peso escalado (**WS**). Este peso, suma a un total de mil observaciones de cada país.                                                                                                                                                                        |
| \- **En resumen**, cuando queremos calcular resultados que involucran más de un país, necesitamos elegir o crear un peso muestral que sea adecuado a nuestros propósitos. En este caso, **WS** cumple este requisito.                                                                                                                                             |
| \]                                                                                                                                                                                                                                                                                                                                                                |

.pull_r\_50_t\_080\[\]

|                                                                                                                                                                                                                                                                                                               |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| background-image: url(img/background_03.jpeg) background-size: 100%                                                                                                                                                                                                                                           |
| Problema 3: **Variables de diseño** (cómo producir resultados para la región)                                                                                                                                                                                                                                 |
| .pull_l\_50_t\_080\[                                                                                                                                                                                                                                                                                          |
| \- Un segundo aspecto a considerar son los **identificadores de clusters** (e.g., escuelas, estratos y países).                                                                                                                                                                                               |
| \- Es muy común que las variables de diseño **no sean únicas** entre las bases de datos de paises, en los estudios de gran escala. Esto quiere decir que, por ejemplo la escuela **1001** se repite entre todos los países participantes.                                                                     |
| \- La repetición de los clusters como los identificadores de escuelas, pueden hacerle creer a los software de turno que **los estudiantes de la escuela 1001 de Colombia, estan en la misma escuela 1001 de Ecuador**, y no queremos cometer este tipo de errores.                                            |
| \- De este modo, si quisiéramos implementar un metodo de corrección de calculo de errores como **Taylor Series Linearization**, necesitaremos crear identificadores de cluster que sean únicos entre países.                                                                                                  |
| \- De manera que el software que calcule los resultados no solo corrija el punto estimado de forma adecuada empleando el peso pertinente (**WS**), sino que además considere cómo estan anidados las observaciones entre las escuelas, y los estratos de cada país, para obtener tamaños de error razonables. |
| \- **En resumen**, además de elegir o crear pesos adecuados para nuestros propósitos, necesitamos **identificadores de cluster** que sean únicos entre países para este caso.                                                                                                                                 |
| \]                                                                                                                                                                                                                                                                                                            |

.pull_r\_50_t\_100\[\]

------------------------------------------------------------------------

class: middle, inverse

background-image: url(img/background_02.jpeg) background-size: 100%

.line_space_01\[ Problemas y soluciones\] .line_space_01\[ .text_250\[
.bold_white\[ Generación de resultados para la región\]\]\]
.line_space_01\[ Problema 3: Secuencia de códigos para producir un
resultado regional\]

<br> <br>

|                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| background-image: url(img/background_03.jpeg) background-size: 100%                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| Problema 3: **Variables de diseño** (cómo producir resultados para la región)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| .pull_l\_50\[                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| \`\`\`r # ——————————————————————- # nivel de lectura en la region # ——————————————————————-                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| #———————————————— # cluster únicos #————————————————                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| data_lan \<- erce::erce_2019_qa6 %>% erce::remove_labels() %>% mutate(id_s = as.numeric(as.factor(paste0(IDCNTRY, “*”, STRATA)))) %>% mutate(id_j = as.numeric(as.factor(paste0(IDCNTRY, ”*”, IDSCHOOL)))) %>% mutate(id_i = seq(1:nrow(.)))                                                                                                                                                                                                                                                                                                                                                                                                                        |
| #———————————————— # variable dummy para los niveles esperados #————————————————                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| data_lan \<- data_lan %>% mutate(all = 1) %>% mutate(lan_min_1 = case_when( LAN_L1 == ‘I’ \~ 0, LAN_L1 == ‘II’ \~ 0, LAN_L1 == ‘III’ \~ 1, LAN_L1 == ‘IV’ \~ 1)) %>% mutate(lan_min_2 = case_when( LAN_L2 == ‘I’ \~ 0, LAN_L2 == ‘II’ \~ 0, LAN_L2 == ‘III’ \~ 1, LAN_L2 == ‘IV’ \~ 1)) %>% mutate(lan_min_3 = case_when( LAN_L3 == ‘I’ \~ 0, LAN_L3 == ‘II’ \~ 0, LAN_L3 == ‘III’ \~ 1, LAN_L3 == ‘IV’ \~ 1)) %>% mutate(lan_min_4 = case_when( LAN_L4 == ‘I’ \~ 0, LAN_L4 == ‘II’ \~ 0, LAN_L4 == ‘III’ \~ 1, LAN_L4 == ‘IV’ \~ 1)) %>% mutate(lan_min_5 = case_when( LAN_L5 == ‘I’ \~ 0, LAN_L5 == ‘II’ \~ 0, LAN_L5 == ‘III’ \~ 1, LAN_L5 == ‘IV’ \~ 1)) \`\`\` |
| \]                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |

.pull_r\_50_t\_090\[\]

–

``` text
# variables de clustering

id_i = indentificador único de estudiantes
id_j = indentificador único de escuelas (i.e., primary sampling unit)
id_s = indentificador único de estratos
id_k = indentificador único de países
```

{{content}}

–

-   Otro detalle a considerar, es que muchas de las librerías que nos
    permiten realizar estimaciones a la población, esperan bases de
    datos sin meta-data. De caso contrario, no reconocen a la base de
    datos como analizable, y no pueden realizar cálculos. De este modo,
    en este ejemplo empleamos la función `erce::remove_labels()` para
    que `library(survey)` no nos genere problemas. {{content}}

–

-   Además, necesitamos tener una variable **dummy** que identifique a
    todos los estudiantes que se encuentren sobre el nivel esperado, es
    decir al menos sobre el nivel III de lectura. {{content}}

–

-   Como los niveles de desempeño sobre lectura, provienen de los
    valores plausibles, entonces necesitamos generar 5 variables de este
    tipo.

|                                                                                                                                                          |
|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| background-image: url(img/background_03.jpeg) background-size: 100%                                                                                      |
| Problema 3: **Variables de diseño** (cómo producir resultados para la región)                                                                            |
| .pull_l\_50_t\_060\[                                                                                                                                     |
| \`\`\`r # ——————————————————————- # nivel de lectura en la region # ——————————————————————-                                                              |
| # \[… continua código anterior\]                                                                                                                         |
| #———————————————— # base de datos con diseño #————————————————                                                                                           |
| # survey method: taylor series linearization data_tsl \<- survey::svydesign( data = data_lan, weights = \~WS, strata = \~id_s, id = \~id_j, nest = TRUE) |
| # Opción: corección a unidad primaria de muestreo que resulte # única al estrato                                                                         |
| library(survey) options(survey.lonely.psu=“adjust”) \`\`\`                                                                                               |
| \]                                                                                                                                                       |

.pull_r\_50_t\_090\[\]

–

-   En esta primera sección del código, estamos indicando el peso que
    necesitamos emplear (**WS**), además de las variables de cluster que
    generamos anteriormente (**id_j**, **id_s**). {{content}}

–

-   Además, necesitamos una función que nos permita combinar los
    estimados de diferentes **valores plausibles** (Rutkowski et al.,
    2010). En este caso, estamos empleando una función generada por
    Thomas Lumley, autor de la librería **survey** (Lumley, 2010), la
    cual nos permite calcular resultados para cada valor plausible, sin
    la necesidad de que tengamos que crear una lista de bases de datos.
    {{content}}

–

-   En la siguiente lámina, vamos a aplicar esta funcion **withPV()**,
    la cual facilitará el proceso de generación de resultados.

|                                                                                                                                                                                                                                                                   |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| background-image: url(img/background_03.jpeg) background-size: 100%                                                                                                                                                                                               |
| Problema 3: **Variables de diseño** (cómo producir resultados para la región)                                                                                                                                                                                     |
| .pull_l\_50_t\_100\[                                                                                                                                                                                                                                              |
| \`\`\`r # ——————————————————————- # nivel de lectura en la region # ——————————————————————-                                                                                                                                                                       |
| # \[… continua código anterior\]                                                                                                                                                                                                                                  |
| #———————————————— # nivel de lectura esperado #————————————————                                                                                                                                                                                                   |
| results \<- mitools::withPV( mapping = lan_min \~ lan_min_1 + lan_min_2 + lan_min_3 + lan_min_4 + lan_min_5, data = data_tsl, action=quote(survey::svymean(\~lan_min, design=data_tsl)), rewrite = TRUE )                                                         |
| #———————————————— # obtener resultados #————————————————                                                                                                                                                                                                          |
| summary(mitools::MIcombine(results)) \`\`\`                                                                                                                                                                                                                       |
| \`\`\`text                                                                                                                                                                                                                                                        |
| summary(mitools::MIcombine(results)) Multiple imputation results: function(mapping, design, action, …) UseMethod(“withPV”,design) MIcombine.default(results) results se (lower upper) missInfo lan_min 0.3118589523 0.003815336074 0.3041889541 0.3195289505 32 % |
| \`\`\`                                                                                                                                                                                                                                                            |
| \]                                                                                                                                                                                                                                                                |

.pull_r\_50_t\_090\[\]

–

-   Lo importante en la definición de **lan_min**, es que incluyamos los
    valores plausibles que necesitamos. En este caso, nuestro argumento
    crítico es:

<!-- -->


    lan_min ~ lan_min_1 + lan_min_2 + lan_min_3 + lan_min_4 + lan_min_5,

{{content}}

–

-   En `design =` necesitamos incluir nuestro objeto de diseño, en este
    caso **data_tsl**. Y respectivamente, necesitamos proceder de igual
    forma dentro del argumento `action =` {{content}}

–

-   La aplicación de la función **withPV** entrega una lista de
    resultados. Esta lista de resultados, necesitamos combinarla
    empleando las reglas de Rubin (Schafer, 1997). Para estos fines,
    empleamos la función `mitools::MIcombine(results)` al interior de la
    función `summary()` de modo de obtener puntos estimados, error del
    punto estimado e intervalos de confianza. {{content}}

|                                                                                                                                                                                                                                                 |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| background-image: url(img/background_03.jpeg) background-size: 100%                                                                                                                                                                             |
| Problema 3: **Variables de diseño** (cómo producir resultados para la región)                                                                                                                                                                   |
| .pull_l\_50_t\_100\[                                                                                                                                                                                                                            |
| \`\`\`r # ——————————————————————- # nivel de lectura en la region # ——————————————————————-                                                                                                                                                     |
| # \[… continua código anterior\]                                                                                                                                                                                                                |
| #———————————————— # tabla de medias #————————————————                                                                                                                                                                                           |
| estimados \<- summary(mitools::MIcombine(results))                                                                                                                                                                                              |
| table_read \<- estimados %>% tibble::rownames_to_column(“lan_min”) %>% rename( lan = results, lan_se = se, ll = 4, ul = 5, miss = 6 ) %>% mutate(lan = lan*100) %>% mutate(lan_se = lan_se*100) %>% mutate(ll = ll*100) %>% mutate(ul = ul*100) |
| # ———————————————– # mostrar tabla # ———————————————–                                                                                                                                                                                           |
| options(digits=10) options(scipen = 999999)                                                                                                                                                                                                     |
| knitr::kable(table_read, digits = 1) \`\`\`                                                                                                                                                                                                     |
| \`\`\`text                                                                                                                                                                                                                                      |
| \|lan_min \| lan\| lan_se\| ll\| ul\|miss \| \|:——-\|—-:\|——:\|—-:\|–:\|:—-\| \|lan_min \| 31.2\| 0.4\| 30.4\| 32\|32 % \|                                                                                                                      |
| \`\`\`                                                                                                                                                                                                                                          |
| \]                                                                                                                                                                                                                                              |

.pull_r\_50_t\_090\[\]

------------------------------------------------------------------------

class: middle, inverse

background-image: url(img/background_02.jpeg) background-size: 100%

.line_space_01\[ Problemas y Soluciones\] .line_space_01\[ .text_250\[
.bold_white\[ Generación de resultados para la región\]\]\]
.line_space_01\[ Resumen de todos los pasos realizados para generar un
resultado regional\]

<br> <br>

|                                                                                                                                                                                                                                                                          |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| background-image: url(img/background_03.jpeg) background-size: 100%                                                                                                                                                                                                      |
| **Generación de resultados para la región** como desarollo                                                                                                                                                                                                               |
| .pull_l\_50_t\_100\[                                                                                                                                                                                                                                                     |
| <img src="./files/erce_a6_nivel_lectura_ejecutivo.jpg" width="100%" />                                                                                                                                                                                                   |
| \`\`\`text                                                                                                                                                                                                                                                               |
| # Resultados generados empleando library(survey) y withPV()                                                                                                                                                                                                              |
| \|lan_min \| lan\| lan_se\| ll\| ul\|miss \| \|:——-\|—-:\|——:\|—-:\|–:\|:—-\| \|lan_min \| 31.2\| 0.4\| 30.4\| 32\|32 % \|                                                                                                                                               |
| \`\`\`                                                                                                                                                                                                                                                                   |
| Realizamos una **series de pasos** para poder reproducir la cifra 31.2%, la que nos indica la proporción de estudiantes que alcanza el nivel esperado de competencia de lectura en la región. A la derecha de esta lámina, incluimos un listado de los pasos realizados. |
| \]                                                                                                                                                                                                                                                                       |

.pull_r\_50_t\_090\[\]

------------------------------------------------------------------------

class: middle, inverse

background-image: url(img/background_02.jpeg) background-size: 100%

.line_space_01\[ Problemas y Soluciones\] .line_space_01\[ .text_250\[
.bold_white\[ Transferibilidad y Reproducibilidad\]\]\] .line_space_01\[
Cómo entregar los resultados generados, y como repetir este ejercicio.\]

<br> <br>

|                                                                     |
|---------------------------------------------------------------------|
| background-image: url(img/background_03.jpeg) background-size: 100% |
| **Transferibilidad y Reproducibilidad**                             |
| .pull_l\_50_t\_100\[                                                |
| <img src="./files/workflow_2.png" width="100%" />                   |
| \]                                                                  |

.pull_r\_50_t\_080\[\]

–

-   El primer aspecto refiere a la **transferibilidad**. Incluiremos
    como un problema de transferibilidad a la generación de resultados.
    Para que un resultado generado sea transferible, necesitamos poder
    **compartir** el resultado con otros usuarios, de alguna manera.
    {{content}}

–

-   Una forma de **compartir** el resultado generado, es producir una
    **tabla en excel**. Esta opción permite que muchos más usuarios
    tengan acceso a los resultados que hemos producido; y no solo entre
    usuarios de **R**.

<!-- -->

    ## Multiple imputation results:
    ##       withPV.survey.design(mapping = lan_min ~ lan_min_1 + lan_min_2 + 
    ##     lan_min_3 + lan_min_4 + lan_min_5, data = data_tsl, action = quote(survey::svymean(~lan_min, 
    ##     data_tsl)))
    ##       MIcombine.default(results)
    ##           results     se (lower upper) missInfo
    ## lan_min_1    0.31 0.0038    0.3   0.32     32 %

``` r
# -------------------------------------------------------------------
# nivel de lectura en la region
# -------------------------------------------------------------------

#------------------------------------------------
# exportar resultados
#------------------------------------------------

table_read %>%
openxlsx::write.xlsx(., 
  'tabla_porcentaje_nivel_lectura.xlsx',
  overwrite = TRUE)
```

{{content}}

| background-image: url(img/background_03.jpeg) background-size: 100%                                                                                                                                                                                                                                                         |
|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| background-image: url(img/background_03.jpeg) background-size: 100%                                                                                                                                                                                                                                                         |
| Transferibilidad y **Reproducibilidad**                                                                                                                                                                                                                                                                                     |
| .pull_l\_50_t\_100\[                                                                                                                                                                                                                                                                                                        |
| <img src="./files/reproducible_problem_3.jpg" width="100%" />                                                                                                                                                                                                                                                               |
| .text_80\[                                                                                                                                                                                                                                                                                                                  |
| \>**Nota**: imagen de como se un código reproducible (Xie, 2013), en formato **RMarkdown**. A la izquierda se encuentra el código escrito en Sublime Text, mientras que a la derecha se encuentra un *screenshot* de la terminal de **R** mostrando los logs de la ejecución exitosa del código.                            |
| Este código lo pueden bajar desde el siguiente link:                                                                                                                                                                                                                                                                        |
| \`\`\`text                                                                                                                                                                                                                                                                                                                  |
| <https://github.com/dacarras/erce_2022_lsa/blob/main/ejemplo_problema_3_resultado_regional.rmd>                                                                                                                                                                                                                             |
| \`\`\`                                                                                                                                                                                                                                                                                                                      |
| \] \]                                                                                                                                                                                                                                                                                                                       |
| .pull_r\_50_t\_080\[                                                                                                                                                                                                                                                                                                        |
| \- Finalmente, todos los pasos revisados hasta ahora, los podemos juntar en un solo **código**.                                                                                                                                                                                                                             |
| \- Desde la apertura de los datos, la creación de variables de clustering, la creación de variables, la estimación de resultados con valores plausibles, la combinación de las estimaciones realizadas, y la definición de la forma de presentación de resultados, la podemos agrupar en un mismo documento **accionable**. |
| \]                                                                                                                                                                                                                                                                                                                          |

background-image: url(img/background_03.jpeg) background-size: 100%

Transferibilidad y **Reproducibilidad**

.pull_l\_50_t\_100\[\]

.pull_r\_50_t\_080\[\]

------------------------------------------------------------------------

background-image: url(img/background_03.jpeg) background-size: 100%

Transferibilidad y **Reproducibilidad**

.pull_l\_50_t\_100\[\]

.pull_r\_50_t\_080\[\]

------------------------------------------------------------------------

background-image: url(img/background_03.jpeg) background-size: 100%

Transferibilidad y **Reproducibilidad**

.pull_l\_50_t\_100\[\]

.pull_r\_50_t\_080\[\]

------------------------------------------------------------------------

class: inverse split-two

background-image: url(img/background_02.jpeg) background-size: 100%

.column\[ .pull_l\_50_1\[\]\]

.column\[\]
