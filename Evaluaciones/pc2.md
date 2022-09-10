> Bases de Datos 2, Prueba corta 2  
> Miguel Ku Liang - 2019061913

# 1.

Partition se refiere a partir el disco en segmentos para almacenar datos hasta que se llene el segmento.  
Shard son las particiones NoSQL en el cual los datos son migrados por fechas que se les asignan.  
Replica se refiere a los almacenes de información de respaldo de otro almacén para la recuperación de los datos.

# 2.

Strong consistency es cuando el almacén stand by no lee los datos del master hasta que estos estén actualizados mientras que en eventual consistency lee los datos aunque estos no esten actualizados. 

# 3.

El hot replica contiene los datos más recientes y tiene un alto uso de la memoria, CPU y disco. El warm replica contiene datos de máximo una semana antes y tiene un bajo uso del CPU y memoria, pero un alto uso del disco.

# 4.

Fail over toma acción de manera automática cuando el servicio se cae, dejando de mandar datos.  
Switch over solo avisa del estado del servicio.