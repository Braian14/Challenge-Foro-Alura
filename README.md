# Challenge_Foro_Alura
Foro alura donde todos los alumnos de la plataforma Alura pueden colocar sus preguntas sobre determinados cursos.  Podrán Crear, Actualizar, Eliminar y Mostrar todos los topicos o 1 topico en especifico. #Oracle_One #Grupo7 #alura  Challenge Foro Alura.

Descripción

La API de Foro Hub es una aplicación backend desarrollada para facilitar funcionalidades de foros de discusión. Construida con Java y Spring Boot, proporciona endpoints RESTful robustos para gestionar tópicos, mensajes, autenticación de usuarios y más.

Funcionalidades
Gestión de Usuarios: Registro de nuevos usuarios y autenticación de usuarios existentes mediante tokens JWT (JSON Web Tokens).
Gestión de Tópicos: Creación, actualización y cierre de tópicos de discusión.
Gestión de Mensajes: Adición, eliminación y recuperación de mensajes dentro de los tópicos.
Filtrado por Curso: Filtrado de tópicos basado en cursos asociados.
Paginación: Uso de solicitudes paginables para una recuperación eficiente de datos.


Clonar el Repositorio:
git clone (https://github.com/Braian14/Challenge-Foro-Alura.git)
Ejecutar la Aplicación:
Abra el proyecto en IntelliJ IDEA.
Configure la conexión segura de la base de datos MySQL en application.properties mediante el uso de variables de entorno:

spring.datasource.url=jdbc:mysql://${MYSQL_HOST}/${MYSQL_NAME}

spring.datasource.username=${MYSQL_USER}

spring.datasource.password=${MYSQL_PASS}

Compila y ejecuta la aplicación.

Tecnologías Utilizadas
Java 17: Lenguaje de programación para lógica backend.
Spring Boot 2.6.5: Marco de trabajo para construir y desplegar aplicaciones Java.
Swagger 3.0: Herramienta de documentación y exploración de API.
MySQL 8: Sistema de gestión de base de datos relacional para almacenamiento de datos.
Insomnia 2024.1: Cliente API RESTful para probar endpoints.


