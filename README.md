# lab3-IO_performance-SantiagoAcevedo
Repositorio con la solución del laboratorio 3 del curso Estructuras de Datos.

## Identificación de la Tecnología de Almacenamiento

El sistema cuenta con dos dispositivos de almacenamiento: un HDD y un SSD NVMe. Las pruebas se realizaron sobre el HDD debido a limitaciones de espacio en el SSD, por lo que los resultados corresponden a esa tecnología.

| Recurso                | Requerimiento           |
| ---------------------- | ----------------------- |
| Espacio libre en disco | **908 GB**              |
| Memoria RAM            | **8 GB**                |
| CPU                    | Intel Core i3           |
| Sistema operativo      | Windows 11              |

## Caracterización del Equipo
Estas son algunas de las características fundamentales del equipo que influirán en la interpretación del resultado.

| Parámetro | Valor Observado |
| --- | --- |
| **Sistema Operativo** | Windows 11 25H2 |
| **CPU (Modelo y Frecuencia)** | Intel Core i3-10110U @ 2.10GHz |
| **Arquitectura y Núcleos** | x64 / 2 núcleos físicos |
| **Memoria RAM Total** | 8 GB DDR4 |
| **Tecnología de Almacenamiento** | HDD SATA |
| **Carga de CPU en Reposo (%)** | ~8.5% |

## Punto de control 1 — Revisión conceptual

1. ¿Qué representa la latencia en este laboratorio?
2. ¿Qué representa el throughput?
3. ¿Por qué en acceso secuencial normalmente se asume que $M \approx 1$?
4. ¿Por qué en acceso aleatorio $M$ tiende a ser mayor?

### Respuestas

- Respuesta 1: La latencia representa el tiempo que tardan los datos en ser transportados, osea, cuando se buscan y justo salen de su origen hasta que llegan a su destino final.
- Respuesta 2: El throughput representa que tantos datos se pueden transportar por cada unidad de tiempo.
- Respuesta 3: Porque solo se accede a los datos una sola vez y a partir de ahí se busca sin saltarse nada, aunque pueda ocurrir que se revisen todos los datos antes de llegar al requerido.
- Respuesta 4: Porque aquí ya no revisa todo en orden sin saltarse nada, sino que realiza saltos entre distintos lugares del disco, y cada salto aumente la $M$.

## Punto de control 2 — Reflexión sobre la configuración

1. **Tamaño del archivo:** ¿Es suficiente para superar la caché RAM de su equipo? Compare con los valores de RAM registrados en la Etapa 1 de la guía.

2. **Tamaño de bloque:** Los tamaños evaluados (4 KB, 16 KB, 64 KB, 256 KB) corresponden a tamaños típicos de páginas en sistemas operativos y motores de bases de datos. ¿Cuál esperaría que tuviera mejor rendimiento en acceso aleatorio y por qué?

3. **Entorno de ejecución:** ¿Está ejecutando en local o en Google Colab? Recuerde que en Colab los tiempos medidos corresponden al hardware de Google, no al suyo.

### Respuestas

- Respuesta 1: El archivo tiene 1 GB, y ya que mi computador tiene 8 GB de RAM, el archivo todavía cabe en la memoria, pero es bastante grande como para que no toda la lectura se haga directamente ahí, entonces si se podrá ver como funciona el HDD.
- Respuesta 2: Los bloques más pequeños, como 4 KB, tardan más en las lecturas aleatorias porque el disco tiene que moverse muchas veces para leer cada pedacito. Creo que los bloques más grandes, como los de 64 KB o 256 KB, deberían ir más rápido porque cada movimiento del disco lee más datos y se pierde menos tiempo.
- Respuesta 3: Lo estoy ejecutando en el local, entonces los tiempos medidos si corresponden al hardware de mi computador.

## Creación y análisis del archivo de prueba

Después de crear el archivo, responda:

1. ¿Qué papel cumple este archivo dentro del experimento?
2. ¿Por qué es útil trabajar con un archivo relativamente grande?
3. ¿Qué cree que ocurriría si el archivo fuera demasiado pequeño?

### Respuestas

- Respuesta 1: Este archivo cumple el papel de poner a prueba el rendimiento del disco HDD, ya que al tener un tamaño tan grande nos permitirá explorar el comportamiento del disco en disntas situaciones.
- Respuesta 2: Porque este archivo, al ser bastante grande en comparación con los archivos que se manejan en la memoria RAM, obliga a que no sea ahi sino en el disco HDD en donde se procese.
- Respuesta 3: Si el archivo fuera demasiado pequeño, seria procesado por el caché del sistema operativo, el cual trabaja a una velocidad demasiado superior al del disco HDD, por lo que no podríamos analizar verdaderamente el rendimiento I/O del sistema.

## Análisis de resultados empíricos

Observe la tabla generada y responda:

1. ¿Cuál patrón de acceso fue más rápido para cada tamaño de bloque?
2. ¿El throughput cambió al aumentar el tamaño de bloque?
3. ¿En qué caso observó la mayor diferencia entre secuencial y aleatorio?

> **Criterio mínimo:** la respuesta 3 debe incluir valores numéricos concretos obtenidos de la tabla (throughput en MiB/s o tiempo en s).

### Respuestas
- Respuesta 1: Para los 3 bloques más pequeños, que eran de 4 KB, 16 KB y 64 KB, la lectura secuencial fue más rápida. Para el bloque más grande, el de 256 KB, el tiempo que tardó la lectura secuencial fue muy similar a la aleatoria, así que ambos patrones rinden parecido.
- Respuesta 2: Sí, el throughput aumentó mucho a medida que el tamaño de bloque crecía. Los bloques pequeños leen menos datos por cada operación, por lo que tardan más, pero los bloques grandes aprovechan mejor el disco y el throughput se eleva de la misma forma.
- Respuesta 3: La mayor diferencia entre secuencial y aleatorio en cuestiones de tiempo fue en la prueba con el bloque de 16 KB, pues con el acceso secuencial tardó 0.5154 segundos, mientras que con el aleatorio solo tardó 0.0411 segundos. En cuanto a throughput, la diferencia más grande estub¿vo en el caso del bloque de 4 KB, pues el throughput del acceso aleatorio fue de 298.46 MiB/s, mientras que el secuencial fue prácticamente el doble, así que en este caso en específico es muy más eficiente el acceso secuencial en cuanto a throughput, ya que su tiempo también aumentó considerablemennte.