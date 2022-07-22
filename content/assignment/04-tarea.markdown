---
title: "Tarea 4. Análisis de regresión"
linktitle: "4: Análisis de regresión"
date: "2021-10-06"
due_date: "2022-11-14"
due_time: "23:59 PM"
menu:
  assignment:
    parent: Tareas
    weight: 1
type: docs
toc: true
editor_options: 
  chunk_output_type: console
---

Esta tarea debe ser resuelta en GitHub Class Room. Para acceder a la <i class="fas fa-external-link-square-alt"></i>  [Tarea N°4 hacer click aquí](https://classroom.github.com/a/2ABddgzu). Si aún tienes dudas de cómo interactuar con [GitHub Class Roomm revisa el práctico](https://learn-r-uah.netlify.app/example/01-practico/)

## Objetivo 

El objetivo de esta tarea consiste en realizar un análisis de regresión lineal y logística utilizando R. Para ello debe utilizar los datos según según sus apellidos [(eg. 'Andrade.sav') los cuales podrán encontrar en el siguiente repositorio](https://github.com/learn-R/www-learn-R-uah/tree/master/content/assignment/05-tarea/bases/originales). Estas bases contienen una muestra aleatoria de 1000 casos de la encuesta MOVID-IMPACT (2020) del módulo “Orientaciones del Trabajo”. <br><br>

La pregunta de investigación que buscamos contestar en esta tarea es **“¿Qué factores inciden el cumplimiento de la distancia física para cuidarse del COVID-19?”** a partir de contestar la frecuencia con que se *“Evitar reunirse con más de 10 personas en un espacio cerrado”.*

Para responder a esta pregunta, nos basamos en la investigación de *Gerber et al (2021)* que indica que tanto factores psicosociales como sociodemográficos son relevantes para predecir la adherencia a las medidas de cuidado contra el COVID-19.  Desde esta investigación, planteamos las siguientes dos hipótesis:

- `\(H_1\)`: A mayor percepción de riesgo contra el COVID-19, mayor frecuencia de cumplimiento de la distancia física

- `\(H_2\)`: Las personas que trabajan presentan menor posibilidad de mantener distancia física. 


- `\(H_3\)`: Las mujeres presentarán mayor frecuencia de mantener distancia física que los hombres

- `\(H_4\)`: Los adultos mayores presentarán mayor frecuencia de mantener distancia física para cuidarse del COVID-19 que los jóvenes.

Considera las siguientes variables:

- **Mantener distancia física**: Frecuencia semanal a la frase “Evitar reunirse con más de 10 personas en un espacio cerrado” (1= Casi nunca hasta 5= Siempre), nombre a la variable: ‘cuidarse’.

  - A partir de esa variable, cree una nueva variable llamada `dummy_cuidarse` donde quiénes contesten "Frecuentemente", "Casi siempre" y "Siempre" presentarán la categoría 1, y el resto 0. 

- **Percepción de riesgo al COVID-19**: Nivel de acuerdo con la frase “¿Qué tan peligroso cree que es el coronavirus para usted y sus cercanos?” (1=Nada peligroso hasta 5=Muy peligroso), nombre de variable: ‘riesgo’

- **Trabajar**: Con la pregunta “Durante la semana pasada, ¿trabajó al menos una hora, sin considerar los quehaceres domésticos?”. (1=Si 2=No), nombre de variable: ‘trabaja’

- **Edad**: Con la pregunta “¿Cuál es su edad?” se clasificó a “Jóvenes”, “Adultos” y “Adultos mayores” (1=Jóvenes, 2=Adultos, 3= Adultos mayores), nombre de variable: ‘edad’


## I. Análisis de Correlación

*Interpretación del output*: ¿Existen asociaciones significativas entre el *cumplimiento de las medidas de cuidado* y la percepción de riesgo?

a.	Lleva a cabo un análisis de correlación entre  ambas variables [4 puntos]

b.	Describe la dirección, fuerza  y significancia de la asociación [1 puntos]

*Formato*: Para este punto puede presentar una tabla de correlaciones o gráfico. 


##	II. Regresión Lineal Múltiple

*Interpretación del output*: ¿Predicen la percepción de riesgo, el trabajar y la edad, el *cumplimiento de las medidas de cuidado*? Lleva a cabo los siguientes pasos:

a.	Lleva a cabo un análisis de regresión lineal múltiple definiendo  el *cumplimiento de las medidas de cuidado* como la variable dependiente (Y). Define la percepción de riesgo, el trabajar y la edad (Xs) [1 punto c/u]

  - Modelo 1 con percepción de riesgo como continua
  - Modelo 2 con percepción de riesgo como ordinal donde "Nada peligroso" sea la categoría de referencia


b.	Representa los modelos en una tabla única con título y columnas en español [6 puntos]

- Los modelos deben ser nombrados como "Modelo 1" y "Modelo 2"

- El nivel de significancia debe estar representado por asteriscos. El intervalo de confianza no debe aparecer

- La tabla debe contener 3 dígitos


c.	Escribe la ecuación de la recta de regresión estimada del *modelo 1* en formato LateX-Markdown [6 puntos]


d.	Interpreta los coeficientes de regresión para el modelo 2 con todas las variables independientes en términos de la dirección y fuerza de la asociación. Describe los efectos aún si los efectos no sean significativos. [3 puntos]


e.	Para cada una de las hipótesis planteadas, argumenta si observas evidencia a favor o no en los resultados de tus análisis. Para este punto es necesario que muestres un *forest plot* del modelo 2 [9 puntos]

- Muestre el intercepto, tamaño efecto y valores p, con 3 dígitos
- Título en debido formato


f.	¿Qué porcentaje de la varianza en la actitud hacia los sindicatos es explicada por el modelo 1 y 2? Reporte, además, el estadístico F[3 puntos]



*Formato*: puede ir escribiendo los `\(R^2\)` y `\(F\)` con `inline code de R` o hacer una tabla.

g.	Utiliza la ecuación estimada para calcular el cumplimiento de las medidas de cuidado *esperada* para quiénes trabajan y para quienes no lo hacen. Puedes presentar los resultados en una tabla o en un gráfico. [9 puntos]


*Formato*: en el punto N°1 debe presentar una tabla, una ecuación en formato Markdown y un forest plot.

### III. Modelo logístico

*Interpretación del output*: ¿Predicen la percepción de salarios, la discriminación y el sexo una actitud **favorable** hacia los sindicatos? Lleva a cabo los siguientes pasos:

a.	Construye múltiples modelos logísticos con la variable *dummy* actitud hacia los sindicatos [1 punto c/u]

  - Modelo nulo
  - Modelo 3 con edad
  - Modelo 4 con trabajo
  - Modelo 5 con edad y trabajo
  - Modelo 6 con todos los predictores (riesgo en factor)
  - Modelo 6 con todos los predictores para nivel polacional
  

b.	Representa los modelos en una tabla única con coeficientes exponenciados [6 puntos]


c.	Interpreta los coeficientes de regresión para el modelo con todas las variables independientes en términos de la dirección y fuerza de la asociación. Describe los efectos aún si los efectos no sean significativos. [6 puntos]

d. Realiza un gráfico de valores predichos con el modelo 6 para el cumplimiento de las medidas de cuidado según edad[9 puntos]

e. Compare la estimación del modelo 6 con R base y modelo 6 utilizando diseño complejo de encuestas. Reporte ambos modelo y reflexione sobre la importancia del uso de ciertos paquetes y argumentos para la estimación de modelos [9 puntos]

*Formato*: en este punto debe presentar una tabla y un margin plot. 

## Pauta

1. RMarkdown, este ítem evalúa aspectos propios de los archivos .Rmd, desde su estructura hasta su correcto funcionamiento. Es necesario considerar:

   a. Aspectos formales: títulos, nombres, información institucional, fecha, etc.
    
   b. Estructura de los archivos .Rmd
    
   c. Uso correcto y constante de markdown
    
   d. Aspectos solicitados según cada tarea, por ejemplo:
    - Análisis: en estos archivos irán tanto sus reportes como el análisis que realicen
    - Replicación de informes: esto incluye la replicación de análisis con sus outputs, ya sean tablas, gráficos o lo que se solicite en la respectiva tarea.



1. Flujo: Este ítem se encarga de evaluar el flujo de trabajo desarrollado en el curso, para ello se debe considerar los elementos que hacen posible el correcto uso del flujo, para obtener buen puntaje en este ítem deben:

   a. Seguir detalladamente las instrucciones
  
   b. Crear las carpetas y archivos requeridos en cada tarea
  
   c. Nombrar **adecuadamente** los archivos/datos/carpetas 
  
   d. Todos los archivos por utilizar deben estar en su lugar correspondiente.
   


1. R: Este ítem evalúa elementos relacionados a archivos .R. Este puede dividirse en dos etapas a lo largo del curso (Debe seguir un orden lógico):

   a. Carga: esta etapa es necesaria para pasar a procesamiento 
  
   b. Procesamiento: etapa donde se preparan los datos para ser utilizados en el análisis. 



1. Markdown: este ítem evalúa aspectos propios del formato en markdown, ya que su uso será constante en este curso [ver recursos](https://learn-r-uah.netlify.app/resource/markdown/) 


1. Reproducibilidad: En este curso es muy relevante la reproducibilidad, para ello es necesario tener en cuenta lo siguiente:
    
   a. El archivo .R debe poder ejecutarse sin problemas por cualquier persona con el programa, siguiendo el orden lógico requerido para ello.
  
   b. El archivo .Rmd debe poder ejecutarse sin problemas por cualquier persona con el programa. Esto implica que tanto los archivos/tablas/códigos deben visualizarse correctamente en su producto (output) final
Este punto será esencial para lo que más adelante veremos como condición de suficiencia.

1. Condición de suficiencia: son elementos esenciales que si no son cumplidos la asignación de puntaje del ítem será 0, independiente de si lo que sigue a ese punto está realizado correctamente. Deben tener en cuenta que este ítem no será inmediato, sino que será a medida vaya avanzando el curso.

1. Bonus: En el curso habrá constantemente aspectos que brindarán puntos y/o décimas dependiendo de la tarea.

1. Descuentos: ítem que considera descuentos en puntos o décimas por el no logro o ausencia de aspectos de los ítems anteriores.

Si utiliza otros paquetes para resolver la tarea **DEBE** explicar la razón del uso esos paquetes y qué ventajas tienen por sobre los utilizados en el curso, de no ser así se descontará con 0.5 puntos. 


## Formato

- Todos los reportes deben estar con 3 dígitos (*ojo* eso no implica que los cálculos estén hechos a tres dígitos)

- Todo el informe debe reemplazar los puntos decimales por comas, de modo de estar *ad hoc* a la escritura en español.

- No deben mostrar explícitamente ningún chunk en el informe generado. Noten que algunos temas en html permiten "esconder" el código, pero mostrarlo si el usuario quiere verlo. Quiénes logren hacer esta modificación en su texto tendrán un bonus de 0,2 décimas. 

## Recursos

- Recuerde revisar los materiales otorgados por las instituciones (de hecho, en algunos casos sus investigadores/as utilizan GitHub)
  

- <i class="fas fa-book"></i> Hadley Wickham, ["R para ciencia de datos - Como usar RMarkdown"](https://es.r4ds.hadley.nz/r-markdown.html) 

- <i class="fab fa-book"></i> Recursos
  - [Recursos del curso](https://learn-r-uah.netlify.app/resource/) 
  - [Tutorial dplyr](https://www.youtube.com/watch?v=APzU10EMMjg)

- <i class="fas fa-external-link-square-alt"></i> [Sesión N°2](/content/02-content)
- <i class="fas fa-external-link-square-alt"></i> [Sesión N°3](/content/03-content)
- <i class="fas fa-external-link-square-alt"></i> [Sesión N°4](/content/04-content)
- <i class="fas fa-external-link-square-alt"></i> [Sesión N°5](/content/05-content)

- <i class="fas fa-external-link-square-alt"></i> [Práctico N°2](/example/02-practico)
- <i class="fas fa-external-link-square-alt"></i> [Práctico N°3](/example/03-practico)
- <i class="fas fa-external-link-square-alt"></i> [Práctico N°4](/example/04-practico)
- <i class="fas fa-external-link-square-alt"></i> [Práctico N°5](/example/05-practico)
- <i class="fas fa-external-link-square-alt"></i> [Práctico N°6](/example/06-practico)
- <i class="fas fa-external-link-square-alt"></i> [Práctico N°7](/example/07-practico)


