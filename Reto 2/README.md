# info de la materia: Tópicos especiales en Telemática
# Estudiante: David Ruiz Echeverri, druize@eafit.edu.co

# Reto 2
1. breve descripción de la actividad
## 1.1. Que aspectos cumplió o desarrolló de la actividad propuesta por el profesor (requerimientos funcionales y no funcionales)
Dentro del reto 2 se cumplieron los requisitos de crear varias instancias, las cuales se comunican entre sí. Se puede evidenciar esta comunicación en Postman y en el rabbitMQ.

1.2. Que aspectos NO cumplió o desarrolló de la actividad propuesta por el profesor (requerimientos funcionales y no funcionales)
Se tuvo dificultades con el search.

2. información general de diseño de alto nivel, arquitectura, patrones, mejores prácticas utilizadas.
   
4. IPs utulizadas
52.44.176.235 - GRPC 172.31.45.241
50.17.117.231 - MOM 172.31.46.185
18.214.3.66- API 172.31.34.59

# Descripción General
El proyecto implementa un sistema que permite listar y buscar archivos en un directorio, utilizando un servidor gRPC para las operaciones de búsqueda y un consumidor de mensajes RabbitMQ para la notificación de errores. Se utiliza Node.js para desarrollar el servidor y el consumidor.

# Parte 1: Servidor gRPC - Listado y Búsqueda de Archivos
Requisitos Previos
Asegúrate de tener las siguientes dependencias instaladas:

@grpc/grpc-js
path
fs

Funcionamiento
Se crea un servidor gRPC que ofrece dos servicios: ListFiles y SearchFiles.
El servidor carga la definición de servicio desde service.proto utilizando @grpc/proto-loader.
Los servicios permiten listar archivos en un directorio y buscar archivos por nombre, respectivamente.
Las direcciones IP no juegan un papel directo en este componente, ya que se enlaza al 0.0.0.0 para escuchar en todas las interfaces de red disponibles.

ejecutar: sudo node server.js 


# Parte 2: Consumidor RabbitMQ - Notificación de Errores
Requisitos Previos

Funcionamiento
Se implementa un consumidor RabbitMQ que escucha la cola my_app.
El consumidor recibe mensajes que pueden ser comandos de listado (list) o mensajes de búsqueda (Search/nombre).
En caso de error en el servidor gRPC, se envían mensajes a la cola para notificar y procesar los errores.

ejecutar: sudo docker start rabbit-server

# Parte 3: Servicio Web Express 

 Funcionamiento
Se crea un servicio web utilizando Express que interactúa con el servidor gRPC y RabbitMQ.
Dos endpoints están disponibles: /list para listar archivos y /search para buscar archivos por nombre.
Las direcciones IP se utilizan para establecer conexiones tanto con el servidor gRPC como con RabbitMQ.

ejecutar: sudo node server.js 

5. Descripción del ambiente de EJECUCIÓN (en producción) lenguaje de programación, librerias, paquetes, etc, con sus numeros de versiones.
El proyecto se realizó en node.js y python.
