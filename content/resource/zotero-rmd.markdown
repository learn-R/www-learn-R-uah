---
title: "Zotero + RMarkdown"
date: "2021-08-13"
menu:
  resource:
    parent: Talleres
type: docs
weight: 4
toc: true

---

# 0. Objetivo del taller

Este taller tiene por objetivo conocer el software **Zotero** para
facilitar la incorporación de *citas y referencias* en archivos
RMarkdown.

# 1. Recursos del práctico

Para este práctico utilizaremos una colección hecha para el taller de *Zotero*, que
nos facilitará la realización de los ejercicios.

-   [<i class="fas fa-file-archive"></i> `material-taller.zip`](https://github.com/learn-R/taller-zotero/raw/main/material-taller.zip)

# 2. Flujo de trabajo

Como se vio en el [tutorial de
instalación](https://www.youtube.com/watch?v=w-qGJH2uswk), una vez
teniendo instalado el software y sus complementos, es necesario tener en
cuenta el flujo de trabajo.

Es importante entender el flujo de trabajo de Zotero + RMarkdown, ya que
resume todo lo visto, mientras más nos acostumbremos a este flujo de
trabajo más simple se hará el proceso de referenciar a través de Zotero.

![](https://github.com/learn-R/taller-zotero/raw/main/input/img/flujo-zotero.png)

## 3 Almacenar

El primer paso es almacenar los datos que se han leído y recopilado. El
almacenamiento inmediato de estos datos será de utilidad para el
reporte.

-   Una de las ventajas de realizar el proceso de almacenar de esta
    forma es que se lleva un registro de lo leído, evitando la pérdida
    de información.

Para esto **Zotero**, no sólo tiene la solución, sino que también
existen diversas formas de hacerlo. Las cuales veremos a continuación

### 3.1 Almacenar referencias de forma manual

Una de las formas más comunes (aunque no más fácil) es almacenar las
referencias de forma manual.

Se debe considerar que si bien esto facilita el proceso, hay formas más
expeditas de almacenamiento.

Para esto debemos seguir los siguientes pasos:

-   Paso 1: Abrir Zotero

-   Paso 2: Dirigirse al botón verde con un signo “+” y seleccionar el
    tipo de archivo a almacenar (artículo, libro, vídeo, etc.)

![](https://github.com/learn-R/taller-zotero/raw/main/input/img/almac-manual.png)

-   Paso 3: Finalmente, deben llenar las secciones que aparecen en el
    lado derecho.

![](https://github.com/learn-R/taller-zotero/raw/main/input/img/llenado-manual.png)

### 3.2 Almacenar a través de la extensión de navegador

Almacenar a través de la extensión del navegador web, es una de las
opciones más simples de almacenamiento, solo debes seguir los siguientes
pasos:

-   Paso 1: Dirigirte al artículo, [noticia](https://www.cnnchile.com/coronavirus/chile-71-poblacion-6-17-recibido-primera-dosis_20211019/), vídeo que quieras almacenar

-   Paso 2: Apretar el botón de la extensión

-   Paso 3: Seleccionar la carpeta donde se almacenará

![](https://github.com/learn-R/taller-zotero/raw/main/input/img/zotero-conector.png)

¡Listo!

![](https://github.com/learn-R/taller-zotero/raw/main/input/img/resultado-zotero-conect.png)

### 3.3 Almacenar a través del identificador

Otra de las opciones que ofrece Zotero es el almacenamiento a través del
identificador (DOI, ISBN, PMID o arXiv ID), los pasos a seguir son los
siguientes:

-   Paso 1: Tener el identificador copiado (para este ejemplo
    utilizaremos este 978-84-459-0745-0, ustedes también pueden probar
    con ese ISBN)

-   Paso 2: Abrir Zotero Paso 3: Ir a al dibujo de una “varita”

-   Paso 3: Ingresar el identificador

![](https://github.com/learn-R/taller-zotero/raw/main/input/img/almacen-identificador.png)

¡Listo!

### 3.4 Almacenar por archivo

Una última forma de almacenar referencias es a través de archivos.

-   Paso 1: Tener un archivo para almacenar

    ![](https://github.com/learn-R/taller-zotero/raw/main/input/img/arch-almac.png)

-   Paso 2: Moverlo a Zotero

    ![](https://github.com/learn-R/taller-zotero/raw/main/input/img/result-save-arch.png)

¡Listo!

## 4. Exportar y formatos

Una vez almacenados, se viene la siguiente etapa de nuestro flujo: la de
***exportación*** y hay dos opciones para exportar los archivos

Opción 1: Exportar archivos con formato .bib

-   Paso 1: Botón derecho a la carpeta a exportar

-   Paso 2: Apretar en **“Exportar colección”**

    ![](https://github.com/learn-R/taller-zotero/raw/main/input/img/export.png)

-   Paso 3: Seleccionar formato BibTeX

    ![](https://github.com/learn-R/taller-zotero/raw/main/input/img/bib-exp.png)

-   Paso 4: Seleccionar carpeta donde alojaremos el archivo (input) y
    guardar

    ![](https://github.com/learn-R/taller-zotero/raw/main/input/img/bib.png)

Opción 2: Exportar archivos con BetterBibTeX

Con esta opción Rstudio automáticamente reconoce la biblioteca, los
pasos son los siguientes:

-   Paso 1: Botón derecho a la carpeta a exportar

-   Paso 2: Apretar en **“Exportar colección”**

    ![](https://github.com/learn-R/taller-zotero/raw/main/input/img/export.png)

-   Paso 3: Seleccionar formato BibTeX y opción **keep updates**

    ![](https://github.com/learn-R/taller-zotero/raw/main/input/img/bbt.png)

-   Paso 4: Seleccionar carpeta donde alojaremos el archivo (input) y
    guardar

    ![](https://github.com/learn-R/taller-zotero/raw/main/input/img/bibliot-bibtex.png)

## 4.1 Carpeta

![](https://github.com/learn-R/slides/raw/main/img/01/flow-rproject.png)

## 4.2 YAML: bibliography y csl

Para incluir las citas en un documento RMarkdown se debe tener en
consideración dos aspectos, el archivo que almacena las citas y el
formato en el que queremos referenciar. Por eso en el YAML se deben
especificar estos dos aspectos

### 4.2.1 Especificar carpeta de donde se extraen las referencias

Para este aspecto en el encabezado (YAML) debe especificarse con
`bibliography` la ruta hacia el archivo, el nombre del archivo y su
extensión

Nuestro YAML quedaría así

    ---
    title: "taller zotero"
    author: "Dafne Jaime Vargas"
    date: "30-09-2021"
    output: html_document
    bibliography: input/taller.bib
    link-citations: yes
    ---

### 4.2.2 formato de citación

Tan relevante como el reverenciar, lo es el formato en el que se
referencia, para ello debemos ir al siguiente
[link](https://www.zotero.org/styles) y descargar el formato con el que
se quiere citar

![](https://github.com/learn-R/taller-zotero/raw/main/input/img/styles.png)

¿Cómo se descarga?, para este proceso hay más de una opción:

Opción 1: Descargar el archivo

-   Paso 1: Poner en el buscador el estilo de citación y hacerle click

![](https://github.com/learn-R/taller-zotero/raw/main/input/img/ej.png)

-   Paso 2: Una vez les salga el mensaje de “Zotero Connector,” apretar
    en **cancel**

    ![](https://github.com/learn-R/taller-zotero/raw/main/input/img/sinc-aut-zot.png)

-   Les descargará un archivo con extensión .csl

    ![](https://github.com/learn-R/taller-zotero/raw/main/input/img/csl-archivo.png)

-   Finalmente, en su archivo RMarkdown, en la sección del YAML deben
    dejar la ruta hacia el archivo, el nombre del archivo y su formato

``` r
---
title: "taller zotero"
author: "Dafne Jaime Vargas"
date: "30-09-2021"
output: html_document
bibliography: input/taller.bib
csl: input/cambridge-university-press-numeric.csl
---
```

¡Listo!

Opción 2:

-   Paso 1: Poner en el buscador el estilo de citación y hacerle click

    ![](https://github.com/learn-R/taller-zotero/raw/main/input/img/styles.png)

-   Paso 2: Una vez les salga el mensaje de “Zotero Connector,” apretar
    en **OK**

    ![](https://github.com/learn-R/taller-zotero/raw/main/input/img/sinc-aut-zot.png)

-   Luego ir a preferencias de Zotero

![](https://github.com/learn-R/taller-zotero/raw/main/input/img/pref.png)

-   En la sección “Exportar” deben elegir formato predeterminado

    ![](https://github.com/learn-R/taller-zotero/raw/main/input/img/conf-zot-apa.png)

-   Actualizar los datos en caso de ser BetterBibTeX o volver a exportar en caso de archivo BibTeX

-   En esta ocasión nuestro en nuestro YAML no habría que especificar un
    estilo de citación

¡Listo!

# 5. Citar en RMarkdown

-   Ahora ya podemos citar, y es muy simple sólo debemos abrir nuestro
    RMarkdown

-   Hacer click en Addins &gt; insert citations o citr:::insert\_citation()

-   Luego hacer knit

¡Listo!

{{&lt; div “note” &gt;}}

### BONUS

En Zotero no sólo se puede almacenar los datos de la referencia y sus
archivos, sino que se pueden añadir notas, apuntes, etiquetas, entre
otros

![](https://github.com/learn-R/taller-zotero/raw/main/input/img/apuntes.png)

{{&lt; /div &gt;}}

Ya puedes volver a leer, Zotero hará todo lo demás por ti. Solo recuerda
los pasos a seguir

![](https://github.com/learn-R/taller-zotero/raw/main/input/img/flujo-zotero.png)

-   Luego, deben abrir el archivo descargado

![](https://github.com/learn-R/taller-zotero/blob/main/input/img/image%20(11).png?raw=true)

-   Una vez abran el archivo descargado, les aparecerá esta ventana donde deben apretar el botón *Continuar o Next &gt;*

![](https://github.com/learn-R/taller-zotero/raw/main/input/img/image%20(1).png)

-   Deben seleccionar la opción *Standard*

![](https://github.com/learn-R/taller-zotero/raw/main/input/img/image%20(12).png)

-   Luego establecer la ubicación del programa deben apretar *Upgrade*

![](https://github.com/learn-R/taller-zotero/raw/main/input/img/image%20(13).png)

-   finalmente deben apretar en *Finish*

![](https://github.com/learn-R/taller-zotero/raw/main/input/img/image%20(15).png)

-   Al abrirlo les aparecerá la interfaz del software

![](https://github.com/learn-R/taller-zotero/raw/main/input/img/image%20(16).png)

Ahora ya tenemos instalado Zotero, sin embargo no es suficiente, también debemos instalar la extensión BBT para facilitar la sincronización de los datos con el informe que queramos crear.

# 2.1 Zotero y BBT

Para descargar BBT deben ir al [link](https://retorque.re/zotero-better-bibtex/) y en la sección More ir a *Download*

![](https://github.com/learn-R/taller-zotero/raw/main/input/img/image%20(7).png)

-   Luego deben hacer click en el archivo con extensión .xpi, pero no deben abrirlo

![](https://github.com/learn-R/taller-zotero/raw/main/input/img/image%20(9).png)

{{&lt; div “note” &gt;}}

Dentro de BBT hay varias versiones las cuales pueden irse actualizando, estas se encuentran en el botón compare

![](https://github.com/learn-R/taller-zotero/raw/main/input/img/image%20(8).png)

{{&lt; /div &gt;}}

Para incorporarlo deben ir a Zotero en *Tools y Add-ons* / En español es en *Herramientas y complementos*

![](https://github.com/learn-R/taller-zotero/raw/main/input/img/image%20(17).png)

-   Les aparecerá una ventana emergente, deben ir a la esquina superior derecha, al icono de tuerca

![](https://github.com/learn-R/taller-zotero/raw/main/input/img/image%20(18).png)

-   Luego deben ir a *Install Add-on from file*, encontrar el archivo descargado (.xpi) de BBT

![](https://github.com/learn-R/taller-zotero/raw/main/input/img/image%20(19).png)

-   Una vez se encuentra se debe apretar el boton *Install Now*

![](https://github.com/learn-R/taller-zotero/raw/main/input/img/image%20(21).png)

-   Luego se debe reiniciar con el botón *Restart Now*

![](https://github.com/learn-R/taller-zotero/raw/main/input/img/image%20(22).png)

![](https://github.com/learn-R/taller-zotero/raw/main/input/img/image%20(23).png)

Ahora ya tenemos el software que gestiona las referencias y la extensión para mantener sincronizadas las referencias. Sin embargo previo a ver como funcionan dejaremos instaladas las extensiones

## 2.2 Instalación de extensión

Para incluir la extensión de navegador de Zotero hay varias opciones según el navegador que utilicen

-   [Chrome](https://chrome.google.com/webstore/detail/zotero-connector/ekhagklcjbdpajgpjgmbionohlpdbjgc?hl=es)

    ![](https://github.com/learn-R/taller-zotero/raw/main/input/img/image%20(24).png)

-   [Firefox](https://www.zotero.org/download/connectors)

    ![](https://github.com/learn-R/taller-zotero/raw/main/input/img/image%20(29).png)

-   [Microsoft Edge](https://www.zotero.org/download/connectors)

    ![](https://github.com/learn-R/taller-zotero/raw/main/input/img/image%20(30).png)

class: title title-8

# 2.3 Creación de cuenta

Para crearse una cuenta deben ir al siguiente [link](https://www.zotero.org/user/register)

![](https://github.com/learn-R/slides/raw/main/img/03/regist.png)

No es necesario crearse una cuenta para usar Zotero, pero si es recomendable

# 3. Puente entre Rstudio y Zotero

Para conectar Zotero con Rstudio y facilitar la incorporación de referencias en RMarkdown, necesitamos un conector y para ello tenemos dos opciones: el paquete `citr` y el editor visual.

Opción 1:

`citr` este es un paquete que nos facilitara la conexión entre Zotero y Rstudio

Se puede instalar de varias formas

-   con `install.packages`

-   Mediante `devtools::install_github("crsh/citr")`

-   O descargando una antigua versión del [CRAN](https://cran.r-project.org/src/contrib/Archive/citr/)

Se reinicia R y luego podrán verlo en la sección **Addins**

-   Editor visual

{{&lt; div “note” &gt;}}

Lo más probable es que `citr` genere problemas en su instalación, debido a que fue removido del CRAN, sin embargo la opción más factible es usar el editor visual o utilizar una versión antigua del paquete

{{&lt; /div &gt;}}

# 3. Flujo de trabajo

Una vez teniendo instalado el software y todo lo necesario para empezar estableceremos el flujo de trabajo. Se debe considerar que este proceso es cíclico.

Es importante entender el flujo de trabajo de Zotero + RMarkdown, porque resume todo lo visto, mientras más nos acostumbremos a este flujo de trabajo más simple se hará el proceso de referenciar a través de Zotero.

![](https://github.com/learn-R/taller-zotero/raw/main/input/img/flujo-zotero.png)

# 4. Video tutorial en Youtube

Recuerden que el [video de asociado a este tutorial](https://youtu.be/w-qGJH2uswk) y muchos más podrán encontrarlos en el [canal de youtube del curso](https://www.youtube.com/channel/UCqBUeqBttVjS6h8fawK8sWg)
