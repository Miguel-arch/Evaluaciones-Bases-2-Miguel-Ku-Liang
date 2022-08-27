> Bases de Datos 2, Prueba corta 1  
> Miguel Ku Liang - 2019061913

# 1. Explique en que consisten los siguientes conceptos:

## a. Data Warehouse

Los data warehouse consisten en un almacen de datos en donde se pueden realizar operaciones de escritura y lectura de datos. Para beneficiarse de este almacen, se necesitaría de un data pipeline para extraer los datos de un sistema y guardarlos en el almacen.

## b. Data Lake

Los data lake contienen grandes cantidades de datos en su formato original que están guardados en repositorios para poder analizar los datos y así utilizar las tecnologías de Big Data.

## c. Data Mart

Los data mart son un data warehouse especializado en un área de funcionalidad específica, como en negocios, marketing, entre otras áreas.

# 2. De que forma se benefician las aplicaciones del uso de Columnar Storage

Las consultas de entrada y salida son más eficientes ya que la base de datos solo tiene que leer las columnas que se piden en la consulta. Esto nos garantiza que todos los datos de una columna que nos devuelve son del mismo tipo, por lo que podemos realizar operaciones más eficientes para los datos en la columna solicitada.

# 3. En que consiste streaming y batch processing

Streaming consiste en la recolección, almacenamiento y procesamiento de datos de las aplicaciones web, celulares, aplicaciones y servicios.  
Batch processing se divide en dos procesos. Extract Transform Load es el proceso de extraer los datos de un sistema para procesarlos y guardarlos en un sistema de almacén de datos para ser analizados. Extract Load Transform guarda los datos extraídos en el sistema de almacén de datos y luego los procesa.

# 4. En que consiste datos estructurados, semi estructurados y no estructurados

Los datos estructurados son los datos que siguen un esquema fijo, por ejemplo una tabla de una base de datos relacional. Los datos semi estructurados son los datos que no siempre tienen los mismos atributos, por ejemplo los archivos xml y json. Los datos no estructurados son los datos que no siguen un patrón, por ejemplo los textos.