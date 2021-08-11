---
title: "Bienvenido/a a R, RStudio y tidyverse"
linktitle: "2: RMarkdown"
date: "2020-01-13"
menu:
  example:
    parent: Ejemplos
    weight: 2
type: docs
toc: true
editor_options:
  chunk_output_type: console
---

## 0. Objetivo del práctico

El objetivo de este práctico es introducirnos al **lenguaje Markdown** y creación de archivos con formato **RMarkdown**, para ello veremos conceptos básicos y los pasos principales para que en un futuro puedan desarrollar sus informes en este formato, que fomenta la reproducibilidad del conocimiento.

###  Materiales de la clase

Recuerden que los archivos asociados a este práctico se pueden decargar acá:

## Rprojects

- [<i class="fas fa-file-archive"></i> `01-class.zip`](../../projects/02-class/02practico.zip) 

## 1. Markdown y RMarkdown

[**Markdown**](https://learn-r-uah.netlify.app/resource/markdown/) es una forma de escritura, sencilla visualizada en una sintaxis de formato para la creación de documentos en el _**Lenguaje de Marcado de Hipertexto (HTML)**_ (código usado en la creación de páginas web). El objetivo principal de este lenguaje universal en texto plano es la búsqueda de ser fácil y legible.  

Por otro lado un [**RMarkdown**](https://rmarkdown.rstudio.com/) es un archivo que puede integrar código de R (mediante chunks) y texto en Markdown a la vez. Todo el sitio web de este curso está creado con RMarkdown (y [un paquete llamado **blogdown**](https://bookdown.org/yihui/blogdown/)). Estos archivos tienen una estructura de al menos 3 partes

1. Encabezado (YAML)
2. Código de R
3. Texto

Sus principales ventajas son:

- Los documentos de R Markdown son completamente reproducibles. 
- Es gratuito y de código abierto.
- Se puede utilizar varios lenguajes, incluidos R, Python y SQL.
- R Markdown admite docenas de formatos de salida estáticos y dinámicos, incluidos HTML , PDF , MS Word , diapositivas, libros, sitios web e incluso [cuadros de mando interactivos](https://rmarkdown.rstudio.com/flexdashboard/index.html).
- Puede incorporar gráficos, tablas y otros resultados de R directamente en su documento. 


## 1.1 Términos claves

Dentro de la creación de archivos en RMarkdown, hay algunos conceptos claves que serán de utilidad para comprender el proceso de trabajo, estos serán desarrollados a lo largo del práctico, pero mientras vamos a familiarizarnos con ellos:

- Chunk: Son **trozos** de códigos de R, estor permiten hacer análisis estadísticos dentro del documento visualizando los resultados en el documento final 

- Knit: Es un boton el cual generará un documento que incluye tanto el contenido como la salida de cualquier trozo de código R incrustado en el documento (se debe instalar un paquete). Este boton combina (teje) el texto y el código en una misma hoja, facilitando diferentes opciones de formato de salida (html, pdf, word). Cuando se **Knitea** (teje) un documento, R ejecuta cada uno de los trozos secuencialmente y convierte la salida de cada trozo en Markdown. Luego, R ejecuta el documento tejido a través de [pandoc](https://pandoc.org/) para convertirlo en HTML o PDF o Word (o cualquier salida que haya seleccionado).

 <img src="/img/assignments/knit-button.png" width="30%" />

- YAML: Es un encabezado al inicio del documento que inicia y acaba con tres guiones **---***. Acá se introducen aspectos básicos del documento, como el título, el autor, la fecha y el formato de salida (output)


## 2. Chunks

Los chunks lucen así:

    ````markdown
    ```{r}
    # Code goes here
    ```
    ````

## 2.1 Anadir Chunks

Hay tres formas de insertar chunks:

1. Pulsar `⌘⌥I` en macOS o `control + alt + I` en Windows.

2. Pulsa el botón "Insert" en la parte superior de la ventana del editor

 <img src="/img/reference/insert-chunk.png" width="30%" />

3. Escribirlo manualmente (no recomendado)

## 2.2 Nombrar chunks

Se puede añadir nombres a los chunks para hacer más facil la navegación por el documento. Si haces clic en el pequeño menú desplegable en la parte inferior de tu editor en RStudio, puedes ver una tabla de contenidos que muestra todos los títulos y chunks. Si nombras los chunks, aparecerán en la lista. Si no incluyes un nombre, el chunk seguirá apareciendo, pero no sabrás lo que hace.

<img src="/img/reference/chunk-toc.png" width="40%" />

Para añadir un nombre, inclúyelo inmediatamente después de la `{r` en la primera línea del chunk. Los nombres no pueden contener espacios, pero sí guiones bajos y guiones. **Todos los nombres de chunk de tu documento deben ser únicos.

````markdown
```r ''````{r nombre-de-este-chunk}
# El código va aquí
```
````

## 2.3 Opciones de chunks

Hay un montón de opciones diferentes que puedes establecer para cada chunk. Puedes ver una lista completa en la [Guía de referencia de RMarkdown](https://rstudio.com/wp-content/uploads/2015/03/rmarkdown-reference.pdf) o en el [sitio web de **knitr**](https://yihui.org/knitr/options/).

Las opciones van dentro de la sección `{r}` del chunk:

````markdown
```r ''````{r nombre-de-este-chunk, warning=FALSE, message=FALSE}
# El código va aquí
```
````

Las opciones de chunk más comunes son estas:

- `fig.width=5` y `fig.height=3` (*o el número que quieras*): Establece las dimensiones de las figuras
- `echo=FALSE`: El código no se muestra en el documento final, pero los resultados si
- `message=FALSE`: Se omiten los mensajes que genera R (como todas las notas que aparecen después de cargar un paquete)
- `warning=FALSE`: Se omiten las advertencias que genera R
- `include=FALSE`: El chunk se sigue ejecutando, pero el código y los resultados no se incluyen en el documento final

También puedes configurar las opciones del chunk haciendo clic en el pequeño icono del engranaje en la esquina superior derecha de cualquier chunk:

<img src="/img/reference/chunk-options.png" width="70%" />


## 3. Formatos de salida (Output formats)

### 3.1 YAML 

Los formatos de salida se ven en el encabezado (**YAML**) del documento, acá puedes especificar en qué formato quieres que te entregue tu archivo. DE esta forma puedes especificar qué tipo de documento creas cuando _"Kniteas"_ o _"tejes"_ 

```yaml
title: "Mi documento"
output:
  html_document: default
  pdf_document: default
  word_document: default
```

También puedes hacer clic en la flecha hacia abajo del botón "Knit" para elegir la salida *y* generar el YAML apropiado. Si hace clic en el icono del engranaje junto al botón "Knit" y elige "Output options" (opciones de salida), puede cambiar la configuración para cada tipo de salida en específico, como las dimensiones de las figuras por defecto o si se incluye o no un índice.

<img src="/img/reference/output-options.png" width="35%" />

El primer tipo de salida que aparece en `output:` será el que se genere al pulsar el botón "Knit" o al pulsar el atajo de teclado (`⌘⇧K` en macOS; `control + shift + K` en Windows). Si elige una salida diferente con el menú del botón "Knit", esa salida se moverá a la parte superior de la sección `output`.

### 3.2 Salidas de formato

El encabezado o YAML es importante, especialmente cuando tienes configuraciones anidadas bajo cada tipo de salida. Así es como una sección `output` suele verse:


```yaml
---
title: "My document"
author: "My name"
date: "January 13, 2020"
output: 
  html_document: 
    toc: yes
    fig_caption: yes
    fig_height: 8
    fig_width: 10
  pdf_document: 
    latex_engine: xelatex  # More modern PDF typesetting engine
    toc: yes
  word_document: 
    toc: yes
    fig_caption: yes
    fig_height: 4
    fig_width: 5
---
```

Es en el **YAML** o **encabezado** del documento, se puede modificar el nombre (title) del documento, el autor, la fecha y las opciones de salida para html, pdf, MsWord, entre otros. 


### 4. Formatos básicos de Markdown

En esta sección veremos formatos básicos de Markdown, sin embargo pueden repasarlo [en la sección recurso](https://learn-r-uah.netlify.app/resource/markdown/) o [acá](https://www.rstudio.com/wp-content/uploads/2015/02/rmarkdown-cheatsheet.pdf)


#### Títulos o encabezados

Estos se hacen con # pueden llegar hasta el título 6

```
# Título 1

## Título 2

```

#### _Cursiva_ y **negrita**

````
_cursiva_ o *cursiva*

**negrita** o __negrita__

_**Cursiva y negrita**_

````

#### Enlaces

````
[Página del curso](https://learn-r-uah.netlify.app/)

[**Página del curso en negrita**](https://learn-r-uah.netlify.app/)

[**_Página del curso en negrita y cursiva_**](https://learn-r-uah.netlify.app/)

````
[Página del curso](https://learn-r-uah.netlify.app/)

[**Página del curso en negrita**](https://learn-r-uah.netlify.app/)

[**_Página del curso en negrita y cursiva_**](https://learn-r-uah.netlify.app/)


#### Imágenes

````
#imágen de internet
![](url de imágen)

#imágen de carpeta local
![](dirección de la carpeta)

````

Tambien se pueden agregar imágenes con chunks

````
<img src="ruta de la carpeta/imagen.png" width="60%" />
````

<img src="../www-learn-R-uah/static/img/example/02practico/logo.png" width="60%" />

#### Citas

````
>  Puedes dejar una línea como cita o

Recuerda que también

> Puede ser un párrafo completo
>
> Solo asegurate de poner > en cada espacio

````
> ¡inténtalo!

#### Listas

````
1. Puedes tener una lista numerando así
1. Porque automáticamente se numerara 
1. Así misma

Recuerda que

1. Tambien puedes numerar con un orden predeterminado
2. Sólo asegurate de llevarlo de forma ordenada
3. Para no tener una numeración repetida

No olvides que

* Además puedes listar cosas desordenadas
  * Inclusive ser más específic-
  * Luego podras volver
* Al formato anterior

````


#### Lineas horizontales

Para esto hay dos opciones

````
Opción 1

-

Opción 2

***

````

#### Ecuaciones

Para ello debes poner el símnolo de peso ($), si te interesa puedes encontrar más información [haciendo click acá](https://learn-r-uah.netlify.app/resource/markdown/)

````
La ecuación cuadratica es la siguiente

$x = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}$
````

Pero ¿qué pasa entonces si quiero escriir el símbolo peso sin referirme a una ecuación matemática? 

Debes anteponer un \, así:

Me debes \$1.000


#### Tablas

Para hacer tablas debes usar | de forma horizontal como separador de columnas y vertical como separador de filas

````
| Right | Left | Default | Center |
|------:|:-----|---------|:------:|
|   12  |  12  |    12   |    12  |
|  123  |  123 |   123   |   123  |
|    1  |    1 |     1   |     1  |

Tabla: Descripción de la tabla
````


#### Pies de página

Para los pies de página debes tener saber(1) cual será tu identificador y (2) lo que quieres escribir en el pie de página. El identificador puede ser lo que tu quieras: pueden ser números como [^1], pero también pueden ser letras.


````
Aquí escribo una referencia de mi tesis[^1] y aquí otra más

[^note-sobre-marx].

[^1]: Esta es una nota

[^note-sobre-marx]: Marx, lo más genial. 

Y bueno, aquí sigo escribiendo
````

Estos y más ejemplos los encontrarás en la sección [Recursos](https://learn-r-uah.netlify.app/resource/) de la página del curso. 


## 5. Creando nuestro primer Markdown


### 5.1 Instalación de paquetes

Previo a la creación de nuestro primer Markdown debemos tener en cuenta algo, para que este archivo pueda convertirse a un formato html, pdf u otro. En el transcurso deben cargarse una serie de paquetes que cumliran con las funciones que necesitamos.

Usualmente para cargar paquetes lo hacemos de la siguiente manera:


```r
  install.packages("paquete")
  library(paquete)
```

Pero en esta ocasion utilizaremos un paquete llamado **pacman**, este facilita y agiliza la lectura de los paquetes a utilizar en R. DE esta forma lo instalamos 1 única vez así:


```r
install.packages("pacman")
library (pacman)
```

Luego cargaremos así los paquetes de R, esto agiliza la carga de paquetes. Para este práctico cargaremos el paquete **rmarkdown** y **knit**.


```r
pacman::p_load(rmarkdown,
               knit)
```


### 5.2 Cómo abrir un Rmarkdown

1. Una vez cargados los paquetes deben dirigirse en File > New File > R Markdown

<img src="../www-learn-R-uah/static/example/02practico/open_rmark_file.png" width="60%" />

2. Luego deben darle un título, poner su nombre y especificar un _formato de salida_ ya sea en **HTML**, **PDF** o **Word**

<img src="../www-learn-R-uah/static/img/example/02practico/open_rmark_file2.png" width="60%" />

3. Les creará un archivo con un **_YAML_**, que tendrá la información general del documento y un **_chunk_** 

<img src="../www-learn-R-uah/static/img/example/02practico/open_rmark_file.png" width="60%" />

4. Ya pueden comenzar a escribir sus informes en RMarkdown


## 6. Actividad del práctico

La actividad tendra relación con la entrega de la **Tarea 1**. Esta actividad consiste en la creación de un RMarkdown que contenga lo siguiente:

* Un encabezado (YAML) con el título: "Práctico 2". También deben incorporar su nombre y fecha

* Este encabezado debe tener una salida (output), pueden elegir entre html o pdf

* En el código deben incorporar un chunk, en este deben llamar al grafico01 que se encuentra en el zip

* Finalmente, deben crear una tabla simple.


## 7. Recursos

- [R Markdown](https://rmarkdown.rstudio.com/) 
- [Tutoriales Markdown](https://rmarkdown.rstudio.com/lesson-1.html) 
- [cheatsheets](https://www.rstudio.com/wp-content/uploads/2015/02/rmarkdown-cheatsheet.pdf)
- Para practicar ir a [Tutorial de Markdown](https://www.markdowntutorial.com/es/)

## 8. Reporte de progreso

