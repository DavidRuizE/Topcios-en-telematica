# Proyecto - Manejo de Direcciones IP
Este README proporciona una descripción general del proyecto y explica cómo funcionan las diferentes partes del código, con un enfoque especial en cómo se manejan las direcciones IP en cada componente.

# Descripción General
El proyecto implementa un sistema que permite listar y buscar archivos en un directorio, utilizando un servidor gRPC para las operaciones de búsqueda y un consumidor de mensajes RabbitMQ para la notificación de errores. Se utiliza Node.js para desarrollar el servidor y el consumidor.

# Parte 1: Servidor gRPC - Listado y Búsqueda de Archivos
Requisitos Previos
Asegúrate de tener las siguientes dependencias instaladas:

@grpc/grpc-js
@grpc/proto-loader
path
fs
fast-glob

# Funcionamiento
Se crea un servidor gRPC que ofrece dos servicios: ListFiles y SearchFiles.
El servidor carga la definición de servicio desde service.proto utilizando @grpc/proto-loader.
Los servicios permiten listar archivos en un directorio y buscar archivos por nombre, respectivamente.
Las direcciones IP no juegan un papel directo en este componente, ya que se enlaza al 0.0.0.0 para escuchar en todas las interfaces de red disponibles.
Parte 2: Consumidor RabbitMQ - Notificación de Errores
Requisitos Previos
Asegúrate de tener las siguientes dependencias instaladas:

amqplib/callback_api
# Funcionamiento
Se implementa un consumidor RabbitMQ que escucha la cola my_app.
El consumidor recibe mensajes que pueden ser comandos de listado (list) o mensajes de búsqueda (Search/nombre).
En caso de error en el servidor gRPC, se envían mensajes a la cola para notificar y procesar los errores.
Parte 3: Servicio Web Express - Interacción con el Servidor gRPC
Requisitos Previos

# Asegúrate de tener las siguientes dependencias instaladas:
express
@grpc/grpc-js
amqplib/callback_api
@grpc/proto-loader
send

# Funcionamiento
Se crea un servicio web utilizando Express que interactúa con el servidor gRPC y RabbitMQ.
Dos endpoints están disponibles: /list para listar archivos y /search para buscar archivos por nombre.
Las direcciones IP se utilizan para establecer conexiones tanto con el servidor gRPC como con RabbitMQ.

# Ejecución
Asegúrate de tener todas las dependencias instaladas en cada componente.
Ejecuta cada componente siguiendo las instrucciones proporcionadas en los respectivos README.
