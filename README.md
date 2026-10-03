# Proyecto_final_formula1
Proyecto final curso databricks smartdata consulting
## Introducción
Este proyecto se basa en el deporte del motor **Fórmula 1**.

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

## Requerimientos

En esta parte vamos a definir claramente los requisitos de nuestro proyecto.

Agruparemos los requisitos del proyecto en cuatro áreas principales: requisitos de ingestión de datos, requisitos de transformación de datos, requisitos analíticos y de elaboración de informes y, por último, requisitos no funcionales.

Empecemos por los requisitos de ingesta de datos.

En primer lugar, necesitamos ingerir los seis conjuntos de datos: circuitos, carreras, constructores, pilotos, resultados y sprints.

Y como saben, los datos se proporcionan en una mezcla de formatos CSV y JSON.

Y durante la ingestión de esos archivos, tenemos que aplicar el esquema correcto, incluidos los nombres de columna y los tipos de datos adecuados.

También tenemos que añadir columnas de auditoría, como la fecha y hora de ingesta y el nombre del archivo de origen, para que se puedan rastrear y validar los datos.

Y todos los datos deben almacenarse en formato Delta desde el principio.

Y a lo largo de este proceso, tenemos que asegurarnos de que se mantienen la integridad y la fiabilidad de los datos.

E inicialmente implementaremos una carga completa del conjunto de datos.

Y más adelante en el curso, mejoraremos la solución para que admita cargas de datos incrementales.

Y una vez ingeridos los datos, hay que transformarlos en un modelo de datos estructurado y fiable.

Durante la transformación, limpiaremos y normalizaremos los datos para garantizar su coherencia en todos los conjuntos de datos.

Aplicaremos convenciones de nomenclatura coherentes y remodelaremos los datos cuando sea necesario, incluido el aplanamiento de estructuras anidadas.

Eliminaremos las columnas innecesarias y realizaremos comprobaciones básicas de la calidad de los datos, como la gestión de valores clave nulos y registros duplicados.

Conservaremos las claves de negocio como temporada,ronda, ID de conductor, ID de constructor, etc., para que se puedamantener la relación entre las entidades.

Se traduciran las columnas del inglés al español y valores de columnas como país, nacionalidad,región, estado, etc en el porceso de transformación de varias tablas en silver

El conjunto de datos transformado debe preparar los datos para las cargas de trabajo analíticas y de elaboración de informes en la capa gold.

A partir de los datos transformados, ahora tenemos que producir perspectivas significativas.

En concreto, las clasificaciones de los pilotos deberían estar disponibles para cada año de carrera.

La clasificación de constructores también debe generarse para cada año de carrera.

Y la solución debe permitir el análisis de los impulsores y constructores dominantes a lo largo del tiempo.

Y debe permitir el análisis tanto de las temporadas recientes como de los datos históricos.

Además, los conjuntos de datos finales deben permitir la elaboración de informes y consultas analíticas eficaces.

Además de los requisitos funcionales, también tenemos algunos requisitos no funcionales.

Si hay una carrera ese fin de semana, el pipeline debe procesar los nuevos datos.

Si no hay datos nuevos, el proceso debería completarse sin fallos.

También debemos ser capaces de supervisar la ejecución de la tubería, volvera ejecutar trabajos fallidos y configurar alertas en caso de fallos.

También debe permitirnos corregir los datos cuando sea necesario.

Ingeriremos múltiples conjuntos de datos y los almacenaremos en formato Delta desde el principio.

Transformaremos los datos en capas estructuradas y fiables.

A partir de esos datos, elaboraremos productos analíticos para informes y análisis.

Y, por último, diseñaremos la solución para que sea fiable y se gobierne desde el primer día.

Ahora que hemos definido claramente los requisitos del proyecto, enla próxima lección diseñaremos la arquitectura del lago de datos que pueda satisfacer estas necesidades.

## Arquitectura

<img width="1536" height="1024" alt="69250f5f-8623-43bb-adb0-24812ac3202e" src="https://github.com/user-attachments/assets/7da81dde-d41a-4af4-87a0-381797a6056e" />


Se tienen dos ambientes para el proyecto:

•	Desarrollo 

•	Producción 

Cada ambiente esta diferenciado por la cuenta de almacenamiento -datalake- , el workspace de databricks , credencial , conector de acceso , localizaciones externas ,tablas -las mismas pero catalogo diferente- ,esquemas y catalogo.


| Objeto | Desarrollo | Producción |
| :--- | :--- | :--- |
| **Catalogo** | Formula1 | Formula1_prod |
| **Workspace Databricks** | azdatbrfforerodev01 | azdatbrfforeroprod |
| **Datalake** | datalakefforero03 | datalakefforeroprod03 |
| **Esquema bronze** | bronze | bronze |
| **Esquema silver** | silver | silver |
| **Esquema gold** | gold | gold |
| **External location bronze** | exlt-bronze | exlt-bronze_prod |
| **External location silver** | exlt-silver | exlt-silver_prod |
| **External location gold** | exlt-gold | exlt-gold_prod |
| **External location metastore** | exlt-metastore | exlt-metastore_prod |
| **External location raw** | exlt-raw | exlt-raw_prod |
| **Credenciales de conector de acceso** | credential_formula1 | credential_formula1_prod |
| **Conectores de acceso** | acconnector_dev_formula_1 | acconnector_prod_formula_1 |
| **Jobs** | Job_Formula_1 | Job_Formula_1_prod  |

Para nuestra solución se construirá con base en la arquitectura medallion vista en clase donde se tienen tres capas: raw, bronze, silver y gold.

En la capa raw se dejan los archivos fuente:

•	circuits.csv

•	drivers.json

•	races.csv

•	constructors.json

Las carpetas que contienen varios archivos json relacionados con lo siguiente:

•	sprints

•	results

***Capa Bronze:***

En la capa bronze se construyen las tablas con el nombre de las fuentes respectivas de los datos, estableciendo los esquemas de datos, en espacial de la información que bien de  los archivos json. Se agrega las columnas relacionadas con la metadata para tener un proceso de trazabilidad del linaje de datos como los con archivo_fuente e ingesta timestamp. 
Las tablas son las siguientes:

•	circuits

•	races

•	constructors

•	drivers

•	results

•	sprints

<img width="267" height="258" alt="image" src="https://github.com/user-attachments/assets/7e1486ed-4bc6-49f5-9e5b-d5c482436a41" />

***Capa Silver:***

En la capa silver se realizan varias transformaciones relacionadas con la calidad de datos y reglas del negocio, y traducción al español de varias columnas y valores de columnas documentadas en cada notebook donde se tienen las siguientes tablas. Adicionalmente se construirá una tabla de región_nacionalidad para hacer join non las tablas de constructores y pilotos. 
Las tablas son las siguientes:

•	Circuitos

•	Carreras

•	Pilotos

•	Constructores

•	Results

•	Sprints

•	ref_nacionalidad_region

<img width="254" height="375" alt="image" src="https://github.com/user-attachments/assets/1b96bf78-4cb3-4f0a-9b0d-9cf32d040443" />

***Capa gold:***

En la capa gold a partir de las transformaciones de las tablas de la capa silver, se construye una bodega de datos con las siguientes dimensiones y fact_table, la documentación y las columnas seleccionadas para cada dimensión  y fact ,del cómo se construyeron está en cada notebook:

•	Dim_Carrerra :  Join entre la data silver de circuitos y carreras a través de la llave id_circuito.

•	Dim_Piloto: A partir de la tabla silver pilotos.

•	Dim_Constructor : A partir de la tabla silver constructores.

•	Fact_resultado_sesion: A partir  de la unión de las tablas silver de sprints y results.

<img width="240" height="235" alt="image" src="https://github.com/user-attachments/assets/9090dc24-3602-4957-b0d6-ebd356bda24d" />

## Job

En el ambiente de desarrollo se desarrollo en siguiente job -Job Formula 1-  donde primero se corren las tareas relacionadas -notebooks- con la capa bronze, luego las tablas relacionadas con silver, y finalmente las tablas de la capa gold, el la siguiente imagen se observan cómo se configuraron las dependencias.

El cluster utilizado para el funcionamiento del job fue **serveless**.

<img width="921" height="767" alt="image" src="https://github.com/user-attachments/assets/c66d399b-fe36-4bf5-ad39-5580b9570332" />

## Despliegue a producción

Para el despliegue a producción se desarrolló un archivo de despliegue donde se crean y despliegan los diferentes objetos relacionados, hacia el ambiente de producción al inicio de la sección de arquitectura -ver tabla-, de manera automática a través del archivo deploy_prod.yml.

Un requisito importante es determinar la configuración de los **token** de desarrollo y producción y los **host** de estos dos ambientes para un despliegue exitoso de los objetos.

Cada sección de despliegue esta debidamente documentada y configurada en cada tarea del archivo de despliegue.

Las evidencias acerca del despliegue a producción están en tres enlaces de videos , en la carpeta de evidencias

## Dasboards

Se desarrollaron 2 dasboards:

• Datos relevantes del piloto colombiano Juan Pablo Montoya

• Top 10 mejores pilotos de todos los tiempos

Se desarrollaron en el ambiente de desarrollo y luego se desplegaron al ambiente de producción creando un **bundle** y determinando el **warehouse_id** -modo parámetro- de cada ambiente para un despliegue exitoso.

Este despliegue se configuro en el archivo de despliegue **deploy_prod.yml** .





