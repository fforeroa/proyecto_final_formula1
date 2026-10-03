# Proyecto_final_formula1
Proyecto final curso databricks smartdata consulting
## Introducción
Este proyecto se basa en el deporte del motor Fórmula 1.

Para asegurarnos de que todo el mundo está cómodo, empezaremos con un breve resumen
de cómo está estructurada la Fórmula 1.

Comprendemos  que no todo el mundo esté familiarizado con este deporte, así que explicaré los conceptos clave en términos sencillos antes
de pasar a los datos propiamente dichos.

Similar a otros deportes populares, como la Premier League inglesa de fútbol una temporada de Fórmula 1 también se disputa una
vez al año y consta de unas 20 carreras.

Cada carrera se celebra durante un fin de semana, de viernes a domingo. Veamos ahora quién participa en una carrera.

Cada carrera tiene lugar en un circuito específico, y los circuitos están situados en diferentes países, y la mayoría de los circuitos acogen una carrera por temporada.

En cada temporada participan aproximadamente entre 10 y 12 equipos.

También se les denomina constructores en la Fórmula 1.

Cada equipo diseña su propio coche para la carrera,y un equipo suele tener dos pilotos, y a cada piloto se le asigna un coche específico.

Los pilotos compiten en las carreras representando a su constructor o a los equipos.

Durante un fin de semana de carreras, su objetivo es sumar el mayor número posible de puntos, tanto para ellos como para su equipo.

Un fin de semana de carreras se compone de varias sesiones.

Hay sesiones de entrenamientos que permiten al equipo probar su coche y prepararse para la carrera.

Los equipos y los pilotos no puntúan en las sesiones de entrenamientos.

Hay una sesión de clasificación antes de la carrera.

Los resultados de la clasificación deciden la posición en la parrilla desde la que un piloto comenzará la carrera.

Cuanto más alto se clasifique un piloto, más adelante saldrá, lo que supone una gran ventaja en la Fórmula 1.

Y, por último, está la carrera principal, en la que los pilotos compiten a lo largo de varias vueltas para terminar en la posición más alta posible.

En función de los resultados de la carrera, los pilotos reciben puntos según sus posiciones finales.

Los constructores reciben el código de puntos combinado de los dos pilotos del equipo.

Estos puntos contribuyen a la clasificación del campeonato de pilotos y del campeonato de constructores.

En las últimas temporadas, también se han introducido carreras al sprint durante los fines de semana de carreras de verano.

Las carreras sprint se introdujeron para añadir más emoción al fin de semana de carreras.

Las carreras sprint son básicamente carreras más cortas que otorgan puntos adicionales e influyen en el resultado global del fin de semana.

Los corredores de sprint también tienen su propia sesión clasificatoria, que determina la nota de salida para la carrera de sprint.

Al final de la temporada, el piloto que encabece la clasificación se convertirá en el campeón de pilotos.

Del mismo modo, el equipo que lidera la clasificación de constructores se convierte en el campeón de constructores.


Para este proyecto, nos centraremos en los resultados principales de las carreras, como las temporadas, los circuitos, los constructores, los pilotos, los resultados de las carreras y los resultados de los sprints.

No modelaremos los datos de la sesión de entrenamientos ni los datos detallados de la sesión de clasificación.

Esto se debe a que nuestro objetivo es analizar el rendimiento en carrera y los puntos a lo largo de las temporadas.

Ahora que ya sabemos cómo se estructura el deporte, veamos cómo se representa la estructura en los datos.

He descargado los datos para este proyecto desde el repositorio de GitHub, jolpica-f1.

Este repositorio ofrece una API de código abierto que permite recuperar los datos en distintos formatos.

También he formateado los datos específicamente para este proyecto.

Tenemos seis tablas principales, circuitos, corredores, constructores, pilotos, resultados y sprints.

La tabla de circuitos contiene información sobre cada circuito de carreras, como el nombre del circuito, la ubicación y el país.

Cada circuito se identifica unívocamente por el id_circuito.

A continuación, tenemos la tabla de carreras.

La tabla de carreras representa carreras individuales dentro de una temporada.

Una carrera se identifica de forma única por la combinación de temporada y ronda.

Cada carrera está asociada a un circuito específico a través del id_circuito, por lo que es una clave foránea en esta tabla.

Luego tenemos la tabla del constructor.

Esta tabla contiene información sobre los equipos participantes en el campeonato.

Cada constructor se identifica unívocamente por el construct riding.

Del mismo modo, tenemos la tabla de pilotos, que contiene información sobre los pilotos.

Cada piloto es, de nuevo, identificado de forma única por id_piloto.

Pasemos ahora a la tabla de resultados.

La tabla de resultados registra el resultado de cada carrera para cada piloto.

Aquí, la clave principal es la clave compuesta formada por temporada, ronda, Id_constructor y Id_piloto.

Esto refleja la estructura del propio deporte.
En una temporada y ronda determinadas, un piloto específico que representa a un constructor específico tiene un resultado.

La tabla de resultados contiene información como la posición en parrilla, el número de vueltas completadas, el código de puntos, la posición final, etc.

Por último, tenemos la tabla de sprints.

La tabla de sprints tiene una estructura muy similar a la tabla de resultados.

También utiliza temporada, ronda, Id_constructor y Id_piloto como clave compuesta.

La diferencia clave es que almacena los resultados de la carrera sprint en lugar de los de la carrera principal.

En general, este modelo de datos refleja fielmente la estructura de la Fórmula 1.

Tenemos temporadas y rondas que definen carreras, carreras vinculadas a circuitos, pilotos que representan a constructores y resultados registrados por piloto y carrera.

Ahora veamos cómo se almacena físicamente en los archivos.

Los conjuntos de datos sobre circuitos y racistas se facilitan en formato CSV.

Esto nos da una estructura de comprimido directa, que suele ser la forma más sencilla de ingerir.

Los constructores y los conjuntos de datos del piloto se proporcionan como un archivo JSON de una sola línea.

El archivo del controlador también contiene una estructura JSON anidada.

JSON de una sola línea significa simplemente que cada registro se devuelve en una sola línea, lo que facilita su paso mediante lectores JSON estándar.

El conjunto de datos de resultados se proporciona como JSON de una sola línea por su reproducción en varios archivos.

Esto simula un escenario más realista en el que los datos llegan por lotes en lugar de como un único archivo de gran tamaño.

Por último, el conjunto de datos de sprints se proporciona como JSON multilínea y también se divide en varios archivos.

El JSON multilínea requiere un manejo ligeramente diferente en comparación con el JSON de una sola línea.

Esto nos permitirá explorar distintas técnicas adyacentes como parte del proyecto.

Así que, en general, estamos tratando con una mezcla de CSV, JSON de una sola línea y JSON de varias líneas, y algunos de los cuales también se dividen en varios archivos.

Esto nos da la oportunidad de manejar diferentes formatos de archivo y patrones de ingesta de forma práctica.

Ahora que entendemos cómo está estructurado el deporte y cómo se representa la estructura en los datos, el siguiente paso es definir lo que queremos construir con estos datos.


de pasar a diseñar la arquitectura.
