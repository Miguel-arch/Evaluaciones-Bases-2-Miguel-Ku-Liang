> Bases de Datos 2, Prueba corta 9  
> Miguel Ku Liang - 2019061913

# 1.

Los problemas de rendimiento pueden proceder de entradas excesivas en la memoria caché. Cuando la memoria caché aumenta, tarda más tiempo en buscar las entradas para utilizarlas. Poco a poco, este comportamiento hace que el rendimiento del sistema se reduzca por el uso elevado del CPU.

# 2.

Las particiones tienen menos registros que la base de datos completa, por lo que ocupa menos tiempo en recuperar la información o ejecutar una consulta, mejorando el tiempo de respuesta del sistema. También, evita la interrupción total del sistema ya que un error en una partición no afecta en el funcionamiento de las otras particiones. Las particiones permiten agregar más recursos para manejar el escalado de la base de datos. Además, se puede crear más particiones durante la ejecución sin afectar el sistema.

# 3.

Los exclusive locks se generan cuando en uno de dos o más procesos es un write. Este proceso bloquea los demás procesos para realizar su escritura. Este bloqueo ocasiona que los otros procesos esten esperando a que termine el proceso de write que llegó primero, por lo que el rendimiento de la base de datos baja.

# 4.

Dependiendo del disco, puede tener un alto o bajo IOPS, afectando la cantidad de datos que puede transferir por unidad de tiempo y por ello, la velocidad de procesamiento de la base de datos. Además, la latencia del disco que determina el tiempo que tarda en ejecutar una transferencia de datos. 