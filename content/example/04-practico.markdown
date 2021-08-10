---
title: "Transformar y seleccionar variables"
linktitle: "4: Transformar y seleccionar variables"
date: "2021-08-30"
menu:
  example:
    parent: Ejemplos
    weight: 4
type: docs
toc: true
editor_options: 
  chunk_output_type: console
---

## 0. Objetivo de la práctica

El objetivo del práctico, es avanzar en el procesamiento de los datos a través de la transformación de las variables a utilizar. Para ello revisaremos procedimientos básicos para el manejo de datos con Rstudio.


## 1. Recursos de la práctica

En este práctico utilizaremos la base de datos de la [**Encuesta Desigualdades Económicas y Sociales (Desiguales)(2016)**](https://www.estudiospnud.cl/bases-de-datos_proc/desigualdades-economicas-y-sociales-desiguales-2016/), la cual fue procesada en el [Práctico anterior]().Recuerden siempre consultar el [**manual/libro de códigos**](https://www.estudiospnud.cl/wp-content/uploads/2020/04/DES_2016_manual-2.pdf) antes de trabajar una base de datos.


## 2. Librerias a utilizar

En este práctico utilizaremos cuatro paquetes, el primero se llama **pacman** este facilita y agiliza la lectura de los paquetes a utilizar en R; el segundo es **sjmisc**, el tercero es **car** para recodificar y el cuarto es **Tidyverse**, este es una colección de paquetes de código abierto. De este último utilizaremos **Dplyr y Forcast**, si quieres averiguar más puedes ir [acá](https://www.tidyverse.org/)

> Recuerden que previo a cargar la base de datos, se deben cargar los paquetes

Primero instalamos pacman por unica vez


```r
install.packages("pacman")
library (pacman)
```

Luego cargaremos así los paquetes de R




```r
pacman::p_load(tidyverse,
               car,
               sjmisc)
```


## 3. Cargar base de datos y explorarla




```r
datos <- read_sav("../Rproject/datos_proc.sav") 
```

En el panel **Environment**, visualizamos el nuevo objeto, que posee 2.613 observaciones (o filas), y 329 variables (o columnas). También podemos explorar la base de datos con los siguientes comandos


```r
dim(datos) # nos entrega las dimensiones, es decir el numero de observaciones y el número de variables
view(datos) # se usa para visualizar la base de datos
find_var() # se utiliza para encontrar variables
names(datos) # entrega los nombres de las variables que componen el dataset
head(datos) # muestra las primeras filas presentes en el marco de datos
```

## 4. Aspectos claves antes de comenzar 

Previo a trabajar con la base de datos, debemos conocer aspectos claves que facilitaran el uso y entendimiento de Rstudio

### Operador pipeline %>%

El operador pipe %>% es útil para concatenar múltiples operaciones, el comando para usarlo es **Ctrl + shift + M** o **Cmd + shift + M** 

### boolaenos y operadores lógicos

Estos son símbolos lógicos que son utilizados en R para designar funciones.

1. En primer lugar están los **operadores relacionales**, estos se usan para hacer comparaciones 


```r
<		Este signo se usa para designar que un valor es menor que otro
>		Este es para designar que un valor es mayor que otro
==		Con este se señala que un valor es igual que otro
<=		La composición de estos dos símbolos se usa para decir que un valor es menor o igual que otro
>=		Esta para decir que un valor es mayor o igual que otro
!=		Este para decir que el valor es diferente que otro
%in%		Este significa que un valor pertenece al conjunto designado
is.na		Este es para asignar un valor como pérdido o NA
!is.na		Este para decir que un valor no es NA
```


2. En segundo lugar, están los **operadores aritméticos**, los cuales realizan operaciones, como la suma, resta, división, entre otros.

3. En tercer lugar, los **operadores de asignación**, es decir que están encargados de asignar valores a objetos

4. Finalmente, los **operadores booleanos**, los cuales describen relaciones lógicas, como:


```r
&		Este operador es la condición y, es decir si se cumplen todas condiciones mencionadas
|		Este es la condición o, es decir si se cumple una condición u otra mencionada
xor()		Este excluye o saca la condición mencionada
!		Significa que no es la condición que se menciona
any		Significa que ninguna de las condiciones serán utilizadas
all 		Significa que todas las condiciones serán utilizadas
```


<img src="../www-learn-R-uah/static/img/example/operad.png" width="60%" />



## 5. Transformación y selección de variables con tidyverse:Dplyr

Dplyr proporciona una gramática de manipulación de datos, proporcionando un conjunto consistente de verbos que ayudan a resolver desafíos de manipulación de datos más comunes. Este posee diversas funciones, en estre práctico veremos las principales:

### 5.1 select()

Nuestra función select escoge variables basándose en sus nombres o funciones

####  selección de las variables en la base de datos a utilizar 

Como lo vieron en el [Práctico anterior]() se deben seleccionar las variables a utilizar, para ello usaremos la funcion select, sin embargo en este práctico profundizaremos sobre su uso.


```r
datos_proc <- datos %>% # se crea un nuevo objeto llamado datos_proc_proc a partir de la base de datos_proc cargada, esto más el operador pipe
  select(edad = V6,     # Con esta función se seleccionan las variables a utilizar en el práctico, asignándoles con "=" el nuevo nombre que llevará
         sexo = V2,   
         garan_min_vid = V146,
         clase_sub = V70,
         just_pago_educ = V117)
```


Se seleccionaron las variables

- Edad
- Sexo
- Rol Gobierno: garantizar minimo vida
- ¿En que clase social ubicaría a la gente como usted?
- Justo: mas pago, mejor educacion

{{< div "note" >}}

Forcats de Tidyverse proporciona un conjunto de herramientas útiles que resuelven problemas comunes con factores. R usa factores para manejar variables categóricas, variables que tienen un conjunto fijo y conocido de valores posibles. Para eso asignaremos valores a las varibales que estan codificadas de forma numerica, pero son factores. 
{{< /div >}}



```r
as_factor (datos_proc$sexo) 
```


####  selección de las variables por *indexación* 

Además, se puede seleccionar variables, donde a partir de los datos_proc procesados se seleccionarán los casos que estén entre 1 y 2 de la variable *'garan_min_vid'*, que tiene como categoría de respuesta

1 Muy de acuerdo

2 De acuerdo

3 Ni de acuerdo ni en desacuerdo

4 En desacuerdo

5 Muy en desacuerdo

Para ello seleccionaremos sólo a las personas que estan de acuerdo de que el gobierno garantice un mínimo de vida.


```r
datos_proc %>% select(1:2, garan_min_vid) # seleccionan las categorias de respuesta y luego la variable de donde lo seleccionarán
```


```r
## # A tibble: 2,613 x 3
##    edad       sexo      garan_min_vid
##   <dbl>  <dbl+lbl>          <dbl+lbl>
## 1    40 1 [Hombre] 1 [Muy de acuerdo]
## 2    18 1 [Hombre] 1 [Muy de acuerdo]
## 3    66 2 [Mujer]  1 [Muy de acuerdo]
## 4    56 2 [Mujer]  2 [De acuerdo]    
## 5    63 1 [Hombre] 1 [Muy de acuerdo]
## 6    62 2 [Mujer]  1 [Muy de acuerdo]
## 7    54 1 [Hombre] 2 [De acuerdo]    
## 8    75 2 [Mujer]  2 [De acuerdo]    
## 9    36 2 [Mujer]  2 [De acuerdo]    
##10    40 2 [Mujer]  2 [De acuerdo]    
## # ... with 2,603 more rows
```

En este caso seleccionamos todo según los datos de la variable garan_min_vid, con **everything()**. Que selecciona todas las columnas o las columnas que quedan después de aplicar las funciones de selección. Es decir las personas que estan de acuerdo con que el gobienro garantice un mínimo de vida.


```r
datos_proc %>%  select(garan_min_vid, everything())
```

```
## # A tibble: 2,613 x 5
##        garan_min_vid  edad      sexo        clase_sub             just_pago_educ
##            <dbl+lbl> <dbl> <dbl+lbl>        <dbl+lbl>                  <dbl+lbl>
##  1 1 [Muy de acuerd~    40 1 [Hombr~ 4 [Clase media ~ 4 [En desacuerdo]         
##  2 1 [Muy de acuerd~    18 1 [Hombr~ 3 [Clase media]  3 [Ni de acuerdo ni en de~
##  3 1 [Muy de acuerd~    66 2 [Mujer] 3 [Clase media]  4 [En desacuerdo]         
##  4 2 [De acuerdo]       56 2 [Mujer] 5 [Clase baja]   4 [En desacuerdo]         
##  5 1 [Muy de acuerd~    63 1 [Hombr~ 5 [Clase baja]   4 [En desacuerdo]         
##  6 1 [Muy de acuerd~    62 2 [Mujer] 4 [Clase media ~ 1 [Muy de acuerdo]        
##  7 2 [De acuerdo]       54 1 [Hombr~ 4 [Clase media ~ 2 [De acuerdo]            
##  8 2 [De acuerdo]       75 2 [Mujer] 5 [Clase baja]   4 [En desacuerdo]         
##  9 2 [De acuerdo]       36 2 [Mujer] 4 [Clase media ~ 4 [En desacuerdo]         
## 10 2 [De acuerdo]       40 2 [Mujer] 5 [Clase baja]   4 [En desacuerdo]         
## # ... with 2,603 more rows
```

#### Selección y renombrar

También podemos *seleccionar y renombrar*, es decir, seleccionar según *garan_min_vid* y renombrar la variable cómo *acuerdo_garan_min_vid*


```r
datos_proc %>%  select(garan_min_vid, acuerdo_garan_min_vid = garan_min_vid ,everything())
```

```
## # A tibble: 2,613 x 5
##    acuerdo_garan_min_~  edad      sexo       clase_sub            just_pago_educ
##              <dbl+lbl> <dbl> <dbl+lbl>       <dbl+lbl>                 <dbl+lbl>
##  1  1 [Muy de acuerdo]    40 1 [Hombr~ 4 [Clase media~ 4 [En desacuerdo]        
##  2  1 [Muy de acuerdo]    18 1 [Hombr~ 3 [Clase media] 3 [Ni de acuerdo ni en d~
##  3  1 [Muy de acuerdo]    66 2 [Mujer] 3 [Clase media] 4 [En desacuerdo]        
##  4  2 [De acuerdo]        56 2 [Mujer] 5 [Clase baja]  4 [En desacuerdo]        
##  5  1 [Muy de acuerdo]    63 1 [Hombr~ 5 [Clase baja]  4 [En desacuerdo]        
##  6  1 [Muy de acuerdo]    62 2 [Mujer] 4 [Clase media~ 1 [Muy de acuerdo]       
##  7  2 [De acuerdo]        54 1 [Hombr~ 4 [Clase media~ 2 [De acuerdo]           
##  8  2 [De acuerdo]        75 2 [Mujer] 5 [Clase baja]  4 [En desacuerdo]        
##  9  2 [De acuerdo]        36 2 [Mujer] 4 [Clase media~ 4 [En desacuerdo]        
## 10  2 [De acuerdo]        40 2 [Mujer] 5 [Clase baja]  4 [En desacuerdo]        
## # ... with 2,603 more rows
```


#### Selección que inicia con prefijos (starts_with) y termina con sufijos (ends_with)

El primer ejemplo muestra la selección de casos que inicien con la variable edad y que terminen con sexo


```r
datos_proc %>% select(starts_with("edad"), ends_with("sexo"))
```

```
## # A tibble: 2,613 x 2
##     edad       sexo
##    <dbl>  <dbl+lbl>
##  1    40 1 [Hombre]
##  2    18 1 [Hombre]
##  3    66 2 [Mujer] 
##  4    56 2 [Mujer] 
##  5    63 1 [Hombre]
##  6    62 2 [Mujer] 
##  7    54 1 [Hombre]
##  8    75 2 [Mujer] 
##  9    36 2 [Mujer] 
## 10    40 2 [Mujer] 
## # ... with 2,603 more rows
```

#### Selección que contiene cadenas (contains)

El segundo selecciona los casos que contienen una letra m **o** los que contienen una letra y


```r
datos_proc %>% select(contains("m")|contains("y"))
```

```
## # A tibble: 2,613 x 1
##         garan_min_vid
##             <dbl+lbl>
##  1 1 [Muy de acuerdo]
##  2 1 [Muy de acuerdo]
##  3 1 [Muy de acuerdo]
##  4 2 [De acuerdo]    
##  5 1 [Muy de acuerdo]
##  6 1 [Muy de acuerdo]
##  7 2 [De acuerdo]    
##  8 2 [De acuerdo]    
##  9 2 [De acuerdo]    
## 10 2 [De acuerdo]    
## # ... with 2,603 more rows
```

#### Selección con expresiones (matches)

El último ejemplo, selecciona las variables que contengan el nombre sexo


```r
datos_proc %>% select(matches("sexo"))
```

```
## # A tibble: 2,613 x 1
##          sexo
##     <dbl+lbl>
##  1 1 [Hombre]
##  2 1 [Hombre]
##  3 2 [Mujer] 
##  4 2 [Mujer] 
##  5 1 [Hombre]
##  6 2 [Mujer] 
##  7 1 [Hombre]
##  8 2 [Mujer] 
##  9 2 [Mujer] 
## 10 2 [Mujer] 
## # ... with 2,603 more rows
```

#### Selección y función where

La función select puede combinarse con la función where, es decir selecciona con la condición cuando, en este caso selecciona cuando el valor es numérico.  


```r
datos_proc %>% select(where(is.numeric))
```

```
## # A tibble: 2,613 x 5
##     edad      sexo     garan_min_vid        clase_sub             just_pago_educ
##    <dbl> <dbl+lbl>         <dbl+lbl>        <dbl+lbl>                  <dbl+lbl>
##  1    40 1 [Hombr~ 1 [Muy de acuerd~ 4 [Clase media ~ 4 [En desacuerdo]         
##  2    18 1 [Hombr~ 1 [Muy de acuerd~ 3 [Clase media]  3 [Ni de acuerdo ni en de~
##  3    66 2 [Mujer] 1 [Muy de acuerd~ 3 [Clase media]  4 [En desacuerdo]         
##  4    56 2 [Mujer] 2 [De acuerdo]    5 [Clase baja]   4 [En desacuerdo]         
##  5    63 1 [Hombr~ 1 [Muy de acuerd~ 5 [Clase baja]   4 [En desacuerdo]         
##  6    62 2 [Mujer] 1 [Muy de acuerd~ 4 [Clase media ~ 1 [Muy de acuerdo]        
##  7    54 1 [Hombr~ 2 [De acuerdo]    4 [Clase media ~ 2 [De acuerdo]            
##  8    75 2 [Mujer] 2 [De acuerdo]    5 [Clase baja]   4 [En desacuerdo]         
##  9    36 2 [Mujer] 2 [De acuerdo]    4 [Clase media ~ 4 [En desacuerdo]         
## 10    40 2 [Mujer] 2 [De acuerdo]    5 [Clase baja]   4 [En desacuerdo]         
## # ... with 2,603 more rows
```

### 5.2 filter()

La función filter de dplyr, escoge o extrae filas basados en sus valores, subdivide un data frame, reteniendo todas las filas que satisfacen sus condiciones. 

Antes de esto, hay que tener en cuenta que para establecer las condiciones a utilizar en las funciones debemos usar **operadores**, ya que la estructutra será **filter(data, variable (operador lógico) condición)**

#### Filtar según caracteres 

A la hora de filtrar según caracteres nuestro primer ejemplo nos muestra cómo filtrar los datos excluyendo el sexo Hombre


```r
filter(datos_proc, sexo  != "Hombre")
```


```r
## # A tibble: 1,601 x 5
##    edad sexo       garan_min_vid            clase_sub        just_pago_educ
##   <dbl> <fct>          <dbl+lbl>            <dbl+lbl>             <dbl+lbl>
## 1    66 Mujer 1 [Muy de acuerdo] 3 [Clase media]      4 [En desacuerdo]    
## 2    56 Mujer 2 [De acuerdo]     5 [Clase baja]       4 [En desacuerdo]    
## 3    62 Mujer 1 [Muy de acuerdo] 4 [Clase media baja] 1 [Muy de acuerdo]   
## 4    75 Mujer 2 [De acuerdo]     5 [Clase baja]       4 [En desacuerdo]    
## 5    36 Mujer 2 [De acuerdo]     4 [Clase media baja] 4 [En desacuerdo]    
## 6    40 Mujer 2 [De acuerdo]     5 [Clase baja]       4 [En desacuerdo]    
## 7    29 Mujer 2 [De acuerdo]     2 [Clase media alta] 4 [En desacuerdo]    
## 8    53 Mujer 2 [De acuerdo]     3 [Clase media]      4 [En desacuerdo]    
## 9    31 Mujer 2 [De acuerdo]     5 [Clase baja]       5 [Muy en desacuerdo]
## 10    48 Mujer 2 [De acuerdo]     3 [Clase media]      5 [Muy en desacuerdo]
## # ... with 1,591 more rows
> 
```

Ahora si queremos filtrar y dejar sólo a los hombres, se usa el operador ==


```r
filter(datos_proc, sexo == "hombre") 
```


```r
## # A tibble: 0 x 5
## # ... with 5 variables: edad <dbl>, sexo <fct>, garan_min_vid <dbl+lbl>, clase_sub <dbl+lbl>, just_pago_educ <dbl+lbl>
```

En este caso no sirvio el comando porque no esta escrito correctamente (Sin mayúscula)


```r
filter(datos_proc, sexo == "Hombre")
```


```r
## # A tibble: 1,012 x 5
##    edad sexo                        garan_min_vid            clase_sub                     just_pago_educ
##   <dbl> <fct>                           <dbl+lbl>            <dbl+lbl>                          <dbl+lbl>
## 1    40 Hombre 1 [Muy de acuerdo]                 4 [Clase media baja] 4 [En desacuerdo]                 
## 2    18 Hombre 1 [Muy de acuerdo]                 3 [Clase media]      3 [Ni de acuerdo ni en desacuerdo]
## 3    63 Hombre 1 [Muy de acuerdo]                 5 [Clase baja]       4 [En desacuerdo]                 
## 4    54 Hombre 2 [De acuerdo]                     4 [Clase media baja] 2 [De acuerdo]                    
## 5    18 Hombre 2 [De acuerdo]                     5 [Clase baja]       4 [En desacuerdo]                 
## 6    20 Hombre 2 [De acuerdo]                     4 [Clase media baja] 3 [Ni de acuerdo ni en desacuerdo]
## 7    23 Hombre 2 [De acuerdo]                     4 [Clase media baja] 3 [Ni de acuerdo ni en desacuerdo]
## 8    26 Hombre 1 [Muy de acuerdo]                 4 [Clase media baja] 3 [Ni de acuerdo ni en desacuerdo]
## 9    27 Hombre 3 [Ni de acuerdo ni en desacuerdo] 4 [Clase media baja] 3 [Ni de acuerdo ni en desacuerdo]
## 10    63 Hombre 2 [De acuerdo]                     3 [Clase media]      2 [De acuerdo]                    
## # ... with 1,002 more rows
```

Finalmente, si queremos filtrar según un conjunto de caracteres, usamos el operador %in% y nos quedamos con mujeres y hombres


```r
filter(datos_proc, sexo %in% c("Mujer", "Hombre"))
```

```
## # A tibble: 0 x 5
## # ... with 5 variables: edad <dbl>, sexo <dbl+lbl>, garan_min_vid <dbl+lbl>,
## #   clase_sub <dbl+lbl>, just_pago_educ <dbl+lbl>
```

#### Filtar según números

Ahora filtraremos según datos numéricos

En este caso queremos dejar todos los casos que sean de clase media, clase media baja, o clase baja


```r
filter(datos_proc, clase_sub > 3)
```

```
## # A tibble: 1,284 x 5
##     edad       sexo      garan_min_vid            clase_sub       just_pago_educ
##    <dbl>  <dbl+lbl>          <dbl+lbl>            <dbl+lbl>            <dbl+lbl>
##  1    40 1 [Hombre] 1 [Muy de acuerdo] 4 [Clase media baja] 4 [En desacuerdo]   
##  2    56 2 [Mujer]  2 [De acuerdo]     5 [Clase baja]       4 [En desacuerdo]   
##  3    63 1 [Hombre] 1 [Muy de acuerdo] 5 [Clase baja]       4 [En desacuerdo]   
##  4    62 2 [Mujer]  1 [Muy de acuerdo] 4 [Clase media baja] 1 [Muy de acuerdo]  
##  5    54 1 [Hombre] 2 [De acuerdo]     4 [Clase media baja] 2 [De acuerdo]      
##  6    75 2 [Mujer]  2 [De acuerdo]     5 [Clase baja]       4 [En desacuerdo]   
##  7    36 2 [Mujer]  2 [De acuerdo]     4 [Clase media baja] 4 [En desacuerdo]   
##  8    40 2 [Mujer]  2 [De acuerdo]     5 [Clase baja]       4 [En desacuerdo]   
##  9    31 2 [Mujer]  2 [De acuerdo]     5 [Clase baja]       5 [Muy en desacuerd~
## 10    18 1 [Hombre] 2 [De acuerdo]     5 [Clase baja]       4 [En desacuerdo]   
## # ... with 1,274 more rows
```

Acá podemos ver que parten desde *Clase media baja*, pero si queremos considerar la **Clase media**, usamos el operador **mayor o igual**. Además con el operador & nos añadirá también a las mujeres


```r
filter(datos_proc, clase_sub >= 3)
```

```
## # A tibble: 2,174 x 5
##     edad      sexo     garan_min_vid        clase_sub             just_pago_educ
##    <dbl> <dbl+lbl>         <dbl+lbl>        <dbl+lbl>                  <dbl+lbl>
##  1    40 1 [Hombr~ 1 [Muy de acuerd~ 4 [Clase media ~ 4 [En desacuerdo]         
##  2    18 1 [Hombr~ 1 [Muy de acuerd~ 3 [Clase media]  3 [Ni de acuerdo ni en de~
##  3    66 2 [Mujer] 1 [Muy de acuerd~ 3 [Clase media]  4 [En desacuerdo]         
##  4    56 2 [Mujer] 2 [De acuerdo]    5 [Clase baja]   4 [En desacuerdo]         
##  5    63 1 [Hombr~ 1 [Muy de acuerd~ 5 [Clase baja]   4 [En desacuerdo]         
##  6    62 2 [Mujer] 1 [Muy de acuerd~ 4 [Clase media ~ 1 [Muy de acuerdo]        
##  7    54 1 [Hombr~ 2 [De acuerdo]    4 [Clase media ~ 2 [De acuerdo]            
##  8    75 2 [Mujer] 2 [De acuerdo]    5 [Clase baja]   4 [En desacuerdo]         
##  9    36 2 [Mujer] 2 [De acuerdo]    4 [Clase media ~ 4 [En desacuerdo]         
## 10    40 2 [Mujer] 2 [De acuerdo]    5 [Clase baja]   4 [En desacuerdo]         
## # ... with 2,164 more rows
```

### 5.3 mutate ()

La función de mutate añade nuevas variables que son funciones de variables existentes, es decir transforma datos existentes de un data frame a nuevas columnas.

####  creación de variable a partir de cálculos

En nuestro primer ejemplo, crearemos una variable a partir de un cálculo, la llamaremos nueva variable y será la suma de 2 y 3, su estructura será **mutate(datos_proc, nueva_variable = calculo/condicion)**


```r
mutate(datos_proc, nueva_variable = 3+2)
```

```
## # A tibble: 2,613 x 6
##     edad     sexo   garan_min_vid   clase_sub      just_pago_educ nueva_variable
##    <dbl> <dbl+lb>       <dbl+lbl>   <dbl+lbl>           <dbl+lbl>          <dbl>
##  1    40 1 [Homb~ 1 [Muy de acue~ 4 [Clase m~ 4 [En desacuerdo]                5
##  2    18 1 [Homb~ 1 [Muy de acue~ 3 [Clase m~ 3 [Ni de acuerdo n~              5
##  3    66 2 [Muje~ 1 [Muy de acue~ 3 [Clase m~ 4 [En desacuerdo]                5
##  4    56 2 [Muje~ 2 [De acuerdo]  5 [Clase b~ 4 [En desacuerdo]                5
##  5    63 1 [Homb~ 1 [Muy de acue~ 5 [Clase b~ 4 [En desacuerdo]                5
##  6    62 2 [Muje~ 1 [Muy de acue~ 4 [Clase m~ 1 [Muy de acuerdo]               5
##  7    54 1 [Homb~ 2 [De acuerdo]  4 [Clase m~ 2 [De acuerdo]                   5
##  8    75 2 [Muje~ 2 [De acuerdo]  5 [Clase b~ 4 [En desacuerdo]                5
##  9    36 2 [Muje~ 2 [De acuerdo]  4 [Clase m~ 4 [En desacuerdo]                5
## 10    40 2 [Muje~ 2 [De acuerdo]  5 [Clase b~ 4 [En desacuerdo]                5
## # ... with 2,603 more rows
```

#### Mutate y filter

Pero ¿Qué pasa si quiero crear una variable y filtrar?, para eso usaremos el operador pipe. Entonces a partir de los datos, unimos las operaciones de filter, que nos extraerá los valores que sean mayores o iguales a 3 (clase media) y que además estén en conjunto de mujeres. Además unimos la operación de mutare que creará una nueva variable que será igual al valor 5


```r
datos_proc %>% 
  filter(clase_sub >= 3 & sexo %in% c("Mujer")) %>% 
  mutate(nueva_variable = 3+2)
```

```
## # A tibble: 0 x 6
## # ... with 6 variables: edad <dbl>, sexo <dbl+lbl>, garan_min_vid <dbl+lbl>,
## #   clase_sub <dbl+lbl>, just_pago_educ <dbl+lbl>, nueva_variable <dbl>
```

### 5.3.1 recode()  

La función denominada *recode* puede reemplazar valores numéricos en base a su posición o su nombre, y valores de caracteres o factores sólo por su nombre. 

#### Factors

Para reemplazar caracteres o factores en este caso de la variable sexo, transformaremos las categorias de respuestas de Mujer a Femenino y de Hombre a Masculino



```r
datos_proc %>% 
  mutate(sexo = recode(sexo, "Mujer" = "Femenino", "Hombre" = "Masculino"))
```


```r
## # A tibble: 2,613 x 5
##    edad sexo           garan_min_vid            clase_sub                     just_pago_educ
##   <dbl> <fct>              <dbl+lbl>            <dbl+lbl>                          <dbl+lbl>
## 1    40 Masculino 1 [Muy de acuerdo] 4 [Clase media baja] 4 [En desacuerdo]                 
## 2    18 Masculino 1 [Muy de acuerdo] 3 [Clase media]      3 [Ni de acuerdo ni en desacuerdo]
## 3    66 Femenino  1 [Muy de acuerdo] 3 [Clase media]      4 [En desacuerdo]                 
## 4    56 Femenino  2 [De acuerdo]     5 [Clase baja]       4 [En desacuerdo]                 
## 5    63 Masculino 1 [Muy de acuerdo] 5 [Clase baja]       4 [En desacuerdo]                 
## 6    62 Femenino  1 [Muy de acuerdo] 4 [Clase media baja] 1 [Muy de acuerdo]                
## 7    54 Masculino 2 [De acuerdo]     4 [Clase media baja] 2 [De acuerdo]                    
## 8    75 Femenino  2 [De acuerdo]     5 [Clase baja]       4 [En desacuerdo]                 
## 9    36 Femenino  2 [De acuerdo]     4 [Clase media baja] 4 [En desacuerdo]                 
## 10    40 Femenino  2 [De acuerdo]     5 [Clase baja]       4 [En desacuerdo]                 
## # ... with 2,603 more rows
```


#### Numeric

Luego transformaremos las categorias de respuesta de 1 a 5 en el grado de acuerdo o desacuerdo. Previo a esto es necesario recodificar la variable como caracter, en este caso se establece que los numeros que tiene la variable son categorias, es decir 1 es la categoría 1 y no un número. [Ver la diferencia entre character y factor en el práctico anterior]()


```r
datos_proc$just_pago_educ <- as.character(datos_proc$just_pago_educ) 

datos_proc %>% 
  mutate(just_pago_educ = recode (just_pago_educ, "1" = "Muy de acuerdo", "2" = "De acuerdo", "3" = "Ni de acuerdo ni en desacuerdo", "4" = "En desacuerdo", "5" = "Muy en desacuerdo"))
```


```r
## # A tibble: 2,613 x 5
##    edad sexo        garan_min_vid            clase_sub just_pago_educ                
##   <dbl> <fct>           <dbl+lbl>            <dbl+lbl> <chr>                         
## 1    40 Hombre 1 [Muy de acuerdo] 4 [Clase media baja] En desacuerdo                 
## 2    18 Hombre 1 [Muy de acuerdo] 3 [Clase media]      Ni de acuerdo ni en desacuerdo
## 3    66 Mujer  1 [Muy de acuerdo] 3 [Clase media]      En desacuerdo                 
## 4    56 Mujer  2 [De acuerdo]     5 [Clase baja]       En desacuerdo                 
## 5    63 Hombre 1 [Muy de acuerdo] 5 [Clase baja]       En desacuerdo                 
## 6    62 Mujer  1 [Muy de acuerdo] 4 [Clase media baja] Muy de acuerdo                
## 7    54 Hombre 2 [De acuerdo]     4 [Clase media baja] De acuerdo                    
## 8    75 Mujer  2 [De acuerdo]     5 [Clase baja]       En desacuerdo                 
## 9    36 Mujer  2 [De acuerdo]     4 [Clase media baja] En desacuerdo                 
## 10    40 Mujer  2 [De acuerdo]     5 [Clase baja]       En desacuerdo                 
## # ... with 2,603 more rows
```

Si bien en este caso más simple usar el comando de Forcast as_factor, en ocasiones la/el investigador puede requerir tener distintos nombres de categorias, por lo que resultaría más útil este procedimiento.

### 5.3.2 if_else() 

La función if_else comprueba condiciones lógicas en su primer argumento, en este caso queremos crear una nueva variable denominada d_sexo que cumpla la condición que la categoría Mujer sea visualizado como 1 y los demás como 0, su estructura será **if_else(condition, Verdadero, Falso)**


```r
datos_proc %>% 
 		 mutate(d_sexo = if_else(sexo == "Mujer", 1, 0))
```


```r
## # A tibble: 2,613 x 6
##    edad sexo        garan_min_vid            clase_sub just_pago_educ d_sexo
##   <dbl> <fct>           <dbl+lbl>            <dbl+lbl> <chr>           <dbl>
## 1    40 Hombre 1 [Muy de acuerdo] 4 [Clase media baja] 4                   0
## 2    18 Hombre 1 [Muy de acuerdo] 3 [Clase media]      3                   0
## 3    66 Mujer  1 [Muy de acuerdo] 3 [Clase media]      4                   1
## 4    56 Mujer  2 [De acuerdo]     5 [Clase baja]       4                   1
## 5    63 Hombre 1 [Muy de acuerdo] 5 [Clase baja]       4                   0
## 6    62 Mujer  1 [Muy de acuerdo] 4 [Clase media baja] 1                   1
## 7    54 Hombre 2 [De acuerdo]     4 [Clase media baja] 2                   0
## 8    75 Mujer  2 [De acuerdo]     5 [Clase baja]       4                   1
## 9    36 Mujer  2 [De acuerdo]     4 [Clase media baja] 4                   1
## 10    40 Mujer  2 [De acuerdo]     5 [Clase baja]       4                   1
## # ... with 2,603 more rows
```


En nuestro segundo ejemplo, creamos una variable llamada validador, que si just_pago_educ tiene un caso NA la variable tendrá categoría de respuesta False y sino será True


```r
datos_proc %>% 
  mutate(validador = if_else(is.na(just_pago_educ), FALSE, TRUE))
```

```
## # A tibble: 2,613 x 6
##     edad      sexo   garan_min_vid     clase_sub        just_pago_educ validador
##    <dbl> <dbl+lbl>       <dbl+lbl>     <dbl+lbl>             <dbl+lbl> <lgl>    
##  1    40 1 [Hombr~ 1 [Muy de acue~ 4 [Clase med~ 4 [En desacuerdo]     TRUE     
##  2    18 1 [Hombr~ 1 [Muy de acue~ 3 [Clase med~ 3 [Ni de acuerdo ni ~ TRUE     
##  3    66 2 [Mujer] 1 [Muy de acue~ 3 [Clase med~ 4 [En desacuerdo]     TRUE     
##  4    56 2 [Mujer] 2 [De acuerdo]  5 [Clase baj~ 4 [En desacuerdo]     TRUE     
##  5    63 1 [Hombr~ 1 [Muy de acue~ 5 [Clase baj~ 4 [En desacuerdo]     TRUE     
##  6    62 2 [Mujer] 1 [Muy de acue~ 4 [Clase med~ 1 [Muy de acuerdo]    TRUE     
##  7    54 1 [Hombr~ 2 [De acuerdo]  4 [Clase med~ 2 [De acuerdo]        TRUE     
##  8    75 2 [Mujer] 2 [De acuerdo]  5 [Clase baj~ 4 [En desacuerdo]     TRUE     
##  9    36 2 [Mujer] 2 [De acuerdo]  4 [Clase med~ 4 [En desacuerdo]     TRUE     
## 10    40 2 [Mujer] 2 [De acuerdo]  5 [Clase baj~ 4 [En desacuerdo]     TRUE     
## # ... with 2,603 more rows
```

## 5.3.3 mutate group_by n()

La función group_by toma datos existentes y lo convierte en datos agrupados, en nuestro primer ejemplo, los agrupa por la variable sexo y luego crearemos la variable n_sexo


```r
datos_proc %>% 
  group_by(sexo)
```

```
## # A tibble: 2,613 x 5
## # Groups:   sexo [2]
##     edad      sexo     garan_min_vid        clase_sub             just_pago_educ
##    <dbl> <dbl+lbl>         <dbl+lbl>        <dbl+lbl>                  <dbl+lbl>
##  1    40 1 [Hombr~ 1 [Muy de acuerd~ 4 [Clase media ~ 4 [En desacuerdo]         
##  2    18 1 [Hombr~ 1 [Muy de acuerd~ 3 [Clase media]  3 [Ni de acuerdo ni en de~
##  3    66 2 [Mujer] 1 [Muy de acuerd~ 3 [Clase media]  4 [En desacuerdo]         
##  4    56 2 [Mujer] 2 [De acuerdo]    5 [Clase baja]   4 [En desacuerdo]         
##  5    63 1 [Hombr~ 1 [Muy de acuerd~ 5 [Clase baja]   4 [En desacuerdo]         
##  6    62 2 [Mujer] 1 [Muy de acuerd~ 4 [Clase media ~ 1 [Muy de acuerdo]        
##  7    54 1 [Hombr~ 2 [De acuerdo]    4 [Clase media ~ 2 [De acuerdo]            
##  8    75 2 [Mujer] 2 [De acuerdo]    5 [Clase baja]   4 [En desacuerdo]         
##  9    36 2 [Mujer] 2 [De acuerdo]    4 [Clase media ~ 4 [En desacuerdo]         
## 10    40 2 [Mujer] 2 [De acuerdo]    5 [Clase baja]   4 [En desacuerdo]         
## # ... with 2,603 more rows
```



```r
datos_proc %>% 
  mutate(n_sexo = n())
```

```
## # A tibble: 2,613 x 6
##     edad      sexo   garan_min_vid      clase_sub          just_pago_educ n_sexo
##    <dbl> <dbl+lbl>       <dbl+lbl>      <dbl+lbl>               <dbl+lbl>  <int>
##  1    40 1 [Hombr~ 1 [Muy de acue~ 4 [Clase medi~ 4 [En desacuerdo]         2613
##  2    18 1 [Hombr~ 1 [Muy de acue~ 3 [Clase medi~ 3 [Ni de acuerdo ni en~   2613
##  3    66 2 [Mujer] 1 [Muy de acue~ 3 [Clase medi~ 4 [En desacuerdo]         2613
##  4    56 2 [Mujer] 2 [De acuerdo]  5 [Clase baja] 4 [En desacuerdo]         2613
##  5    63 1 [Hombr~ 1 [Muy de acue~ 5 [Clase baja] 4 [En desacuerdo]         2613
##  6    62 2 [Mujer] 1 [Muy de acue~ 4 [Clase medi~ 1 [Muy de acuerdo]        2613
##  7    54 1 [Hombr~ 2 [De acuerdo]  4 [Clase medi~ 2 [De acuerdo]            2613
##  8    75 2 [Mujer] 2 [De acuerdo]  5 [Clase baja] 4 [En desacuerdo]         2613
##  9    36 2 [Mujer] 2 [De acuerdo]  4 [Clase medi~ 4 [En desacuerdo]         2613
## 10    40 2 [Mujer] 2 [De acuerdo]  5 [Clase baja] 4 [En desacuerdo]         2613
## # ... with 2,603 more rows
```


También podemos hacer ambas operaciones en un sólo comando


```r
datos_proc %>% 
  group_by(sexo) %>% 
  mutate(n_sexo = n())
```

```
## # A tibble: 2,613 x 6
## # Groups:   sexo [2]
##     edad      sexo   garan_min_vid      clase_sub          just_pago_educ n_sexo
##    <dbl> <dbl+lbl>       <dbl+lbl>      <dbl+lbl>               <dbl+lbl>  <int>
##  1    40 1 [Hombr~ 1 [Muy de acue~ 4 [Clase medi~ 4 [En desacuerdo]         1012
##  2    18 1 [Hombr~ 1 [Muy de acue~ 3 [Clase medi~ 3 [Ni de acuerdo ni en~   1012
##  3    66 2 [Mujer] 1 [Muy de acue~ 3 [Clase medi~ 4 [En desacuerdo]         1601
##  4    56 2 [Mujer] 2 [De acuerdo]  5 [Clase baja] 4 [En desacuerdo]         1601
##  5    63 1 [Hombr~ 1 [Muy de acue~ 5 [Clase baja] 4 [En desacuerdo]         1012
##  6    62 2 [Mujer] 1 [Muy de acue~ 4 [Clase medi~ 1 [Muy de acuerdo]        1601
##  7    54 1 [Hombr~ 2 [De acuerdo]  4 [Clase medi~ 2 [De acuerdo]            1012
##  8    75 2 [Mujer] 2 [De acuerdo]  5 [Clase baja] 4 [En desacuerdo]         1601
##  9    36 2 [Mujer] 2 [De acuerdo]  4 [Clase medi~ 4 [En desacuerdo]         1601
## 10    40 2 [Mujer] 2 [De acuerdo]  5 [Clase baja] 4 [En desacuerdo]         1601
## # ... with 2,603 more rows
```

# 5.4 summarise 

La función summarise resume dato a una sola fila de valores, en nuestro primer ejemplo, toma los datos creados anteriormente y los resume a un solo valor 


```r
datos_proc %>%
  summarise(n_sexo = n())
```

```
## # A tibble: 1 x 1
##   n_sexo
##    <int>
## 1   2613
```

En nuestro segundo ejemplo, creamos una nueva tabla donde nos agrupara los datos según sexo y además resumirá los casos


```r
datos_proc %>% 
  group_by(sexo) %>% 
  summarise(n_sexo = n())
```

```
## # A tibble: 2 x 2
##         sexo n_sexo
##    <dbl+lbl>  <int>
## 1 1 [Hombre]   1012
## 2 2 [Mujer]    1601
```


## 6. Resumen con procesamiento de las variables

Previo a la manipulación de los datos es necesario conocer como se distribuye esta por eso el paso inicial es un descriptivo de las variables a procesar. Para ello, usaremos la función frq del paquete **sjmisc**, que  permite analizar la frecuencia las variables que **no sean numericas**. Para las variables numericas, en cambio, usaremos la función **descr** del mismo paquete, que nos entregará las **medidas de tendencia central, dispersión y posición** de la variable. [Ver práctico anterior]()


```r
descr(datos_proc$edad) #Usar la función descr con la variable edad de los datos datos_proc.
```

```
## 
## ## Basic descriptive statistics
## 
##  var    type        label    n NA.prc  mean    sd   se md trimmed      range
##   dd numeric Edad (anyos) 2613      0 45.54 17.68 0.35 45   44.75 78 (18-96)
##  iqr skew
##   29 0.29
```

```r
frq(datos_proc$sexo)
```

```
## 
## Sexo del entrevistado (x) <numeric>
## # total N=2613  valid N=2613  mean=1.61  sd=0.49
## 
## Value |  Label |    N | Raw % | Valid % | Cum. %
## ------------------------------------------------
##     1 | Hombre | 1012 | 38.73 |   38.73 |  38.73
##     2 |  Mujer | 1601 | 61.27 |   61.27 | 100.00
##  <NA> |   <NA> |    0 |  0.00 |    <NA> |   <NA>
```

```r
frq(datos_proc$garan_min_vid)
```

```
## 
## P35 - Rol Gobierno: garantizar minimo vida (x) <numeric>
## # total N=2613  valid N=2613  mean=2.09  sd=1.24
## 
## Value |                          Label |    N | Raw % | Valid % | Cum. %
## ------------------------------------------------------------------------
##     1 |                 Muy de acuerdo |  836 | 31.99 |   31.99 |  31.99
##     2 |                     De acuerdo | 1226 | 46.92 |   46.92 |  78.91
##     3 | Ni de acuerdo ni en desacuerdo |  285 | 10.91 |   10.91 |  89.82
##     4 |                  En desacuerdo |  153 |  5.86 |    5.86 |  95.68
##     5 |              Muy en desacuerdo |   67 |  2.56 |    2.56 |  98.24
##     8 |                   NS (no leer) |   41 |  1.57 |    1.57 |  99.81
##     9 |                   NR (no leer) |    5 |  0.19 |    0.19 | 100.00
##  <NA> |                           <NA> |    0 |  0.00 |    <NA> |   <NA>
```

```r
frq(datos_proc$clase_sub)
```

```
## 
## P14 - ¿En qué clase social ubicaría a la gente como usted? (x) <numeric>
## # total N=2613  valid N=2613  mean=3.47  sd=1.09
## 
## Value |            Label |   N | Raw % | Valid % | Cum. %
## ---------------------------------------------------------
##     1 |       Clase alta | 119 |  4.55 |    4.55 |   4.55
##     2 | Clase media alta | 320 | 12.25 |   12.25 |  16.80
##     3 |      Clase media | 890 | 34.06 |   34.06 |  50.86
##     4 | Clase media baja | 807 | 30.88 |   30.88 |  81.75
##     5 |       Clase baja | 468 | 17.91 |   17.91 |  99.66
##     8 |     NS (no leer) |   9 |  0.34 |    0.34 | 100.00
##     9 |     NR (no leer) |   0 |  0.00 |    0.00 | 100.00
##  <NA> |             <NA> |   0 |  0.00 |    <NA> |   <NA>
```

```r
frq(datos_proc$just_pago_educ)
```

```
## 
## P25 - Justo: mas pago, mejor educacion (x) <numeric>
## # total N=2613  valid N=2613  mean=3.50  sd=1.29
## 
## Value |                          Label |   N | Raw % | Valid % | Cum. %
## -----------------------------------------------------------------------
##     1 |                 Muy de acuerdo | 157 |  6.01 |    6.01 |   6.01
##     2 |                     De acuerdo | 559 | 21.39 |   21.39 |  27.40
##     3 | Ni de acuerdo ni en desacuerdo | 346 | 13.24 |   13.24 |  40.64
##     4 |                  En desacuerdo | 997 | 38.16 |   38.16 |  78.80
##     5 |              Muy en desacuerdo | 528 | 20.21 |   20.21 |  99.00
##     8 |                   NS (no leer) |  20 |  0.77 |    0.77 |  99.77
##     9 |                   NR (no leer) |   6 |  0.23 |    0.23 | 100.00
##  <NA> |                           <NA> |   0 |  0.00 |    <NA> |   <NA>
```

Luego debemos recodificar las variables según sean necesario, para ello utilizaremos las librerias car y Dplyr

Para la libreria car recodificaremos todas las categorias de respuesta como no sabe (NS) o no responde(NR) en NA's



```r
datos_proc$garan_min_vid <- car::recode(datos_proc$garan_min_vid, "c(8, 9)=NA") #acá con :: especificamos qué libreria usar
datos_proc$clase_sub <- car::recode(datos_proc$clase_sub, "c(8, 9)=NA")
datos_proc$just_pago_educ <- car::recode(datos_proc$just_pago_educ, "c(8, 9)=NA")
```


Tambien podemos recodificar para agruparlas


```r
datos_proc$just_pago_educ <- car::recode(datos_proc$just_pago_educ, "1:2=1;3=2;4:5=3")
```


Luego con Dplyr le asignamos nuevos valores 


```r
datos_proc %>% 
  mutate(just_pago_educ = recode (just_pago_educ, "1" = "a favor", "2" = "neutro", "3" = "en contra"))
```


```r
## # A tibble: 2,613 x 5
##    edad sexo        garan_min_vid            clase_sub just_pago_educ
##   <dbl> <fct>           <dbl+lbl>            <dbl+lbl> <chr>         
## 1    40 Hombre 1 [Muy de acuerdo] 4 [Clase media baja] en contra     
## 2    18 Hombre 1 [Muy de acuerdo] 3 [Clase media]      neutro        
## 3    66 Mujer  1 [Muy de acuerdo] 3 [Clase media]      en contra     
## 4    56 Mujer  2 [De acuerdo]     5 [Clase baja]       en contra     
## 5    63 Hombre 1 [Muy de acuerdo] 5 [Clase baja]       en contra     
## 6    62 Mujer  1 [Muy de acuerdo] 4 [Clase media baja] a favor       
## 7    54 Hombre 2 [De acuerdo]     4 [Clase media baja] a favor       
## 8    75 Mujer  2 [De acuerdo]     5 [Clase baja]       en contra     
## 9    36 Mujer  2 [De acuerdo]     4 [Clase media baja] en contra     
## 10    40 Mujer  2 [De acuerdo]     5 [Clase baja]       en contra      
## # ... with 2,603 more rows
```


## 7. Guardar base procesada

Para guardar la base de datos procesada, debes dirigir la ruta hacia tu Rproject


```r
save(datos_proc, data = "../Rproject/datos_proc.RData")
```


## 8. Reporte de progreso
  
¡Recuerda rellenar tu reporte de progreso! En https://learn-r.formr.org/. Te llegó un código único a tu correo electrónico. Mediante él debes acceder para actualizar tu estado de avance del curso.

