---
title: "Bienvenido/a a R, RStudio y tidyverse"
linktitle: "2: RMarkdown"
date: "2021-08-16"
menu:
  example:
    parent: Ejemplos
    weight: 2
type: docs
toc: true
editor_options:
  chunk_output_type: console
---




## 1. Markdown

Markdown es una forma de escritura, sencilla visualizada en una sintaxis de formato para la creación de documentos HTML. Este lenguaje universal en texto plano que busca ser fácil y legible.  

## 2. RMarkdown


Es un documento de R con formato Markdown

Ventajas: 
- Los documentos de R Markdown son completamente reproducibles. 
- Es gratuito y de código abierto.
- Se puede utilizar varios lenguajes, incluidos R, Python y SQL.
- R Markdown admite docenas de formatos de salida estáticos y dinámicos, incluidos HTML , PDF , MS Word , diapositivas, libros, sitios web y más.


### Cómo abrir un Rmarkdown

1. Lo primero que debes hacer es asegurarte que tienes el paquete descargado

  install.packages("rmarkdown")

2. Una vez listo deberás tener en consideración lo siguiente

  - **Knit**  es un boton que generará un documento que incluye tanto el contenido como la salida de cualquier trozo de código R incrustado en el documento. (Asegurese de tener instalado el paquete). Este boton combina (teje) texto y código en una misma hoja, facilitando diferentes opciones de formato de salida (html, pdf, word)

3. Una vez listo debe dirigirse al boton para crear un nuevo script y aceptar la opción RMarkdown o en File > New File > R Markdown

<img src="../www-learn-R-uah/static/img/example/open_rmark_file.png" width="60%" />

4. Luego deben darle un título, poner su nombre y especificar un _formato de salida_ ya sea en **HTML**, **PDF** o **Word**

<img src="../www-learn-R-uah/static/img/example/open_rmark_file2.png" width="60%" />

5. Les creará un archivo con un **_YAML_**, que tendrá la información general del documento y un **_chunk_** 

<img src="../www-learn-R-uah/static/img/example/open_rmark_file2.png" width="60%" />

## 3.Aspectos claves

### Títulos o encabezados

````
# Título 1

## Título 2

### Título 3

#### Título 4

##### Título 5

###### Título 6
````

# Título 1

## Título 2

### Título 3

#### Título 4

##### Título 5

###### Título 6


### Cursiva y negrita

````
_cursiva_

**negrita**

_**Cursiva y negrita**_

````
_cursiva_

**negrita**

_**Cursiva y negrita**_

### Enlaces

````
[Página del curso](https://learn-r-uah.netlify.app/)

[**Página del curso en negrita**](https://learn-r-uah.netlify.app/)

[**_Página del curso en negrita y cursiva_**](https://learn-r-uah.netlify.app/)

### [**_Página del curso en negrita, cursiva y de título 3_**](https://learn-r-uah.netlify.app/)

````

[Página del curso](https://learn-r-uah.netlify.app/)

[**Página del curso en negrita**](https://learn-r-uah.netlify.app/)

[**_Página del curso en negrita y cursiva_**](https://learn-r-uah.netlify.app/)

### [**_Página del curso en negrita, cursiva y de título 3_**](https://learn-r-uah.netlify.app/)


### Imágenes

````
#imágen de internet
![](url de imágen)

#imágen de carpeta local
![](dirección de la carpeta)

````
![](https://ih1.redbubble.net/image.512529969.7087/st,small,507x507-pad,600x600,f8f8f8.u7.jpg)

### Citas

````
>  Puedes dejar una línea como cita o

Recuerda que también

> Puede ser un párrafo completo
>
> Solo asegurate de poner > en cada espacio

````

>  Puedes dejar una línea como cita o

Recuerda que también

> Puede ser un párrafo completo
>
> Solo asegurate de poner > en cada espacio

### Listas
````
1. Puedes tener una lista numerando así
1. Porque automáticamente se numerara 
1. Así misma

Recuerda que

1. Tambien puedes numerar con un orden predeterminado
2. Sólo asegurate de llevarlo de forma ordenada
3. Para no tener una numeración repetida

No olvides que

* Además puedes numerar de esta forma
  * Inclusive ser más específic-
  * Luego podras volver
* Al formato anterior

````
1. Puedes tener una lista numerando así
1. Porque automáticamente se numerara 
1. Así misma

Recuerda que

1. Tambien puedes numerar con un orden predeterminado
2. Sólo asegurate de llevarlo de forma ordenada
3. Para no tener una numeración repetida

No olvides que

* Además puedes numerar de esta forma
  * Inclusive ser más específic-
  * Luego podras volver
* Al formato anterior

## 4. Insertar chunks

Los chunks son pedazos de códigos insertados en el texto.Se crean con una linea inicial _**```{r}**_ , y se cierra con _**```**_. Tambien en Code > Insert Chunk o, con Ctrl + Alt + i

<img src="../www-learn-R-uah/static/img/example/open_rmark_file2.png" width="60%" />


### Opciones de chunks

1. Chunk que muestra código y resultado

````

```r
5*8
```

```
## [1] 40
```
````

Este es el chunk por defecto

2. Chunk que muestra solo el código

````

```r
5 * 8
```
````

3. Chunk que muestra solo el resultado

````

```
## [1] 40
```
````


4. Chunk que no muestra ni código ni resultado

````
# ```{r echo=FALSE, results='hide'}
  5 * 8
# ```
````

5. Chunk que muestra el código sin ejecutarlo


````

```r
5 * 8
```
````

6. Chunk que entrega el resultado en formato directo 

````
#```{r, results='asis'}
# stargazer(cars, type="html")
#```
````


```r
stargazer(cars, type="html")
```


<table style="text-align:center"><tr><td colspan="8" style="border-bottom: 1px solid black"></td></tr><tr><td style="text-align:left">Statistic</td><td>N</td><td>Mean</td><td>St. Dev.</td><td>Min</td><td>Pctl(25)</td><td>Pctl(75)</td><td>Max</td></tr>
<tr><td colspan="8" style="border-bottom: 1px solid black"></td></tr><tr><td style="text-align:left">speed</td><td>50</td><td>15.400</td><td>5.288</td><td>4</td><td>12</td><td>19</td><td>25</td></tr>
<tr><td style="text-align:left">dist</td><td>50</td><td>42.980</td><td>25.769</td><td>2</td><td>26</td><td>56</td><td>120</td></tr>
<tr><td colspan="8" style="border-bottom: 1px solid black"></td></tr></table>

### Las opciones principales son:

* mostrar código {r echo=TRUE/FALSE}

* mostrar resultado {r results='markup'/'hide'}


### Imagenes en chunks

````
#```{r, echo=FALSE, out.width="60%"}
    knitr::include_graphics("ruta de la carpeta/imagen.png", error = FALSE)
#```
````

<img src="../www-learn-R-uah/static/img/example/logo.png" width="60%" />

### Gráficos en R

#### Gráfico 1

````
#```{r, echo=FALSE, message=FALSE, warning=FALSE, paged.print=FALSE}

 plot_grpfrq(cars$speed, cars$dist,
            title = "Gráfico 1",
            type = "box")
#```
````

<img src="/example/02-practico_files/figure-html/unnamed-chunk-12-1.png" width="672" />


#### Gráfico 2
````
#```{r echo=FALSE, message=FALSE, warning=FALSE, results='asis'}
 plot_scatter(cars, speed, dist)
#```
````

<img src="/example/02-practico_files/figure-html/unnamed-chunk-13-1.png" width="672" />

Para continuar practicando ir a [Tutorial de Markdown](https://www.markdowntutorial.com/es/)


## Tarea 1

Envie un archivo Rmarkdown creado por usted con 1 ejemplo de cada uno de los ejercicios hechos en el práctico

