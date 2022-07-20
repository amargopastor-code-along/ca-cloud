# Module 5: Storage and Databases

<p align="center">
  <img src="./img/img47.png" style="width: 65%">
</p>

## AWS Storage

Existen 3 tipos de almacenamiento. No sólo en Amazon sino que es un estándar en el mundo cloud:

- `Almacenamiento en Bloques o EBS`: En un disco duro físico. Títipco de e-commerce.
- `Almacenamiento de Objetos`: S3. Similar a un dropbox: vídeos, archivos, música...
- `Almacenamiento de Archivos`: EFS o FSx. Disco duro en red. Archivos de una compañía que requieren constante edición. Cuando necesitamos compartir archivos internamente, editar los archivos, los arhcivos a compartir son de carácter privado.

<p align="center">
  <img src="./img/img48.png" style="width: 65%">
</p>

## Almacenamiento en Bloques

Almacenamiento en bloque se emplea con las instancias EC2:

<p align="center">
  <img src="./img/img49.png" style="width: 65%">
</p>

## Instance Store

Disco duro para almacenar información temporal. Por ejemplo, se puede emplear para ETL (transformación y limpieza de datos desde un werehouse).

<p align="center">
  <img src="./img/img50.png" style="width: 65%">
</p>

## EBS volumens

Almacenan información de carácter persistente.

<p align="center">
  <img src="./img/img51.png" style="width: 65%">
</p>

## EBS snapshots

Son backups incrementales de los datos almacenados en un EBS.

Creación de backups de nuestros discos duros EBS (cuya información es de carácter persistente) para que podamos reestablecer información en otra máquina.

Es posible establecer políticas de configuración para la reación de los mismos snapshots (diario, mensual...). Los snapshots consecutivos "reutilizan" la información guardada en el anterior snapshots y le añadimos la nueva información.

De ahí su nombre: discos duros basados en bloque.

<p align="center">
  <img src="./img/img52.png" style="width: 65%">
</p>

## Questions

- `Instance store`: almacenar información temporal
- `EBS`: persistencia de datos en el tiempo

## Objets storage on Amazon Simple Storage Service (Amazon S3)

S3 es un servicio de almacenamiento de objetos teniendo como característica principal que el acceso a los datos es frecuente y rápido.

Cada objeto consiste de una data, metadata y key. Una analogía podría ser dropbox: carpetas que almacenan distinta información. Todo ello recibe el nombre de Amazon S3. Estos poseen hasta 3 replican en la misma región. Si queremos replicar a otra región a mayores, debemos configurarlo.

<p align="center">
  <img src="./img/img53.png" style="width: 65%">
</p>

Amazon Simple Storage Service (Amazon S3) es un servicio de almacenamiento de objetos.

<p align="center">
  <img src="./img/img54.png" style="width: 65%">
</p>

- Los buckets deben tener un nombre únicos.
- Establecemos permisos para cada usuario y sus acciones a mis buckets
- Seleccionar un rango de ...

Exiten distintos modelos o capas de almacenamiento:

1. Todos los archivos guardados se almacenarán en un `S3 standar` o capa genérica. La información almacenada en una región se duplica en 3 AZ (sin coste adicional para que exista alta disponibilidad d ela info).La disponibilidad de archivos será alta.

2. `Standar IA`: almacena archivos con un precio más bajo que la S3 standar. Ideal para consulta de archivos más espaciada en el tiempo.

Ver [pricing](https://aws.amazon.com/es/s3/pricing/).

3. One Zone-IA: Para información que no pasa nada si perdemos (solo estará en una zona de disponibilidad). Información que puedo volver a generar (por ejemplo, un cierre bancario).

4. Inteligent-Tiering: Cuando no sabemos cual emplear

5. `Glacier`: puede tardar horas en devolver la info (1-2 horas), pero es económica.

6. `Glacier depp archive`: mas económica, pero se recupera la info de manera más lenta (12 horas).

La diferencia entre las mismas son los costos y el comportamiento a la hora de acceder a la información.

<p align="center">
  <img src="./img/img56.png" style="width: 65%">
</p>

## File storage

`File storage o EFS`: acceso a nuestros archivos mediante distintas aplicaciones o servidores.

<p align="center">
  <img src="./img/img57.png" style="width: 65%">
</p>

## Elastic file system

Acceso multiregional:

<p align="center">
  <img src="./img/img58.png" style="width: 65%">
</p>

## Database types

- `BBDD relacionales`: tablas bajo la premisa entre entidad relación. Se consulta a través de SQL.
- `BBDD no relacionales`: almacena documentos (más rápidas)

<p align="center">
  <img src="./img/img59.png" style="width: 65%">
</p>

<p align="center">
  <img src="./img/img60.png" style="width: 65%">
</p>

## Relational Database Service RDS

En AWS trabajamos mediante Relational Database Service las bbdd relacionales.

Existe almacenamiento en tránsito y descanso. La data está encriptada si no es esta consultando o enviando. Si la data se consume viajará encriptada.

<p align="center">
  <img src="./img/img61.png" style="width: 65%">
</p>

Motores soportados por RDS:

<p align="center">
  <img src="./img/img62.png" style="width: 65%">
</p>

Amazon Aurora tiene 2 tipos:

- Amazon Aurora RDS
- Amazon Aurora Serverless

1. Aurora está diseñana para soporta alto tráfico de clientes (lectura y escritura) y almacenar gran cantidad de datos.

2. Se reduce el coste eliminando entrada y salida de datos superfluos.

3. Hasta 6 copias (sin coste adicional) en 3 AZ.

<p align="center">
  <img src="./img/img63.png" style="width: 65%">
</p>

## BBDD nonrelational

BBDD dinámica de documentos con pares de key-value (id) identificables.

<p align="center">
  <img src="./img/img64.png" style="width: 65%">
</p>

`Amazon DynamoDB` para el consumo de este tipo de bbdd:

<p align="center">
  <img src="./img/img65.png" style="width: 65%">
</p>

## Database Migration Service

Database Migration Service verifica la bbdd fuente, la bbdd destino y en el medio esité una EC2 que consulta la info y gestiona el traslado.

<p align="center">
  <img src="./img/img66.png" style="width: 65%">
</p>

- Almacenar datos en una bbdd relacional: RDS
- Ejecutar una BBDD serverles (suele ser no relacional las serveless): Aurora o DynamoDB (mejor lo último si es no-relacional)
- BBDD orientada a key-value: DynamoDB
- Usar SQL para organizar la data: Amazon RDS
- Salcar 10 trillones de request al día: DynamoDB
- Almacenar data en una bbdd Amazon Aurora: Amazon RDS

## BBDD aditional services

`Redshift`: Para datawerehouse. Crear un almacen de datos de alto volumen.

`DocumentDB`: Si empleamos mongoDB podemos migrar nuestro sistema de bbdd no relacional

`Neptune`: bbdd orientada a grafos

`QLDB`: BBDD cuya función es registrar transacciónes de manera transparente e inalterable. Verificable a través de cryptografía. La información de esta BBDD no puede ser modificada ni manipulada (seguros, banda, RRHH...)

<p align="center">
  <img src="./img/img67.png" style="width: 65%">
</p>

`: centralizada `:orientada a memoria
``: funciona con dynamodb: los nilisegundos de dynamodb de tiempo de consulta pasa a microsegundos.

<p align="center">
  <img src="./img/img68.png" style="width: 65%">
</p>

## Questions

<p align="center">
  <img src="./img/img69.png" style="width: 65%">
</p>

<p align="center">
  <img src="./img/img70.png" style="width: 65%">
</p>

<p align="center">
  <img src="./img/img71.png" style="width: 65%">
</p>

<p align="center">
  <img src="./img/img72.png" style="width: 65%">
</p>

<p align="center">
  <img src="./img/img73.png" style="width: 65%">
</p>
