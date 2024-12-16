# Challenge_Foro_Alura
Foro alura donde todos los alumnos de la plataforma Alura pueden colocar sus preguntas sobre determinados cursos.  Podrán Crear, Actualizar, Eliminar y Mostrar todos los topicos o 1 topico en especifico. #Oracle_One #Grupo7 #alura  Challenge Foro Alura. 
Descripción
La API de Foro Hub es una aplicación backend desarrollada para facilitar funcionalidades de foros de discusión. Construida con Java y Spring Boot, proporciona endpoints RESTful robustos para gestionar tópicos, mensajes, autenticación de usuarios y más. Esta API se integra perfectamente con MySQL para el almacenamiento de datos y utiliza Swagger para una documentación clara y detallada de la API.

Funcionalidades
Gestión de Usuarios: Registro de nuevos usuarios y autenticación de usuarios existentes mediante tokens JWT (JSON Web Tokens).
Gestión de Tópicos: Creación, actualización y cierre de tópicos de discusión.
Gestión de Mensajes: Adición, eliminación y recuperación de mensajes dentro de los tópicos.
Filtrado por Curso: Filtrado de tópicos basado en cursos asociados.
Paginación: Uso de solicitudes paginables para una recuperación eficiente de datos.
Demostración
A continuación se muestra cómo utilizar la API de Foro Hub mediante Swagger:

Registro de Usuario:
Dirígete a POST /usuarios/registro y completa los campos de nombre, email y clave.

registrar usuario
Verificación del Usuario Registrado:
Confirma que el usuario ha sido registrado correctamente.

usuario registrado
Autenticación:
Usa POST /auth/login para autenticarte y obtener un jwtToken.

autenticar usuario usuario autenticado
Autorizar:
Ve al icono de "Authorize" en la parte superior derecha.

autenticar usuario
Pegar Token:
Ingresa el token encriptado.

autenticar usuario
Uso de la API:
Con el usuario autenticado, podrás acceder a todas las funcionalidades de Foro Hub.

autenticar usuario
Acceso
Puede acceder a la API de Foro Hub localmente siguiendo estos pasos:

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
Código de Ejemplo
Crear un nuevo tópico
@PostMapping
public ResponseEntity<DatosRegistroTopico> registrarTopico(
        @Valid @RequestBody DatosRegistroTopico datosRegistroTopico,
        UriComponentsBuilder uriComponentsBuilder) {

    Topico topico = topicoService.registrarTopico(datosRegistroTopico);

    URI uri = uriComponentsBuilder.path("/topicos/{id}")
            .buildAndExpand(topico.getId())
            .toUri();

    return ResponseEntity.created(uri).body(datosRegistroTopico);
}
Obtener la lista de tópicos
@GetMapping
public ResponseEntity<PagedModel<EntityModel<DatosListadoTopico>>> listadoTopicos(
        @PageableDefault(size = 10, sort = "fecha", direction = Sort.Direction.ASC) Pageable paginacion) {

    Page<DatosListadoTopico> topicosPage = topicoService.listarTopicos(paginacion);

    PagedModel<EntityModel<DatosListadoTopico>> pagedModel = topicoService.convertirAPagedModel(topicosPage,
            pagedResourcesAssembler, paginacion);

    return ResponseEntity.ok(pagedModel);
}
Obtener un tópico por ID
@GetMapping("/{id}")
public ResponseEntity<EntityModel<Topico>> buscarDetalleTopicoPorId(@PathVariable Long id) {
    Optional<Topico> optionalTopico = topicoService.buscarTopicoPorId(id);

    if (optionalTopico.isPresent()) {
        Topico topico = optionalTopico.get();
        return ResponseEntity.ok(EntityModel.of(topico));
    } else {
        return ResponseEntity.notFound().build();
    }
}
Buscar tópico por curso
@GetMapping("/buscar")
public ResponseEntity<PagedModel<EntityModel<DatosListadoTopico>>> buscarTopicosPorCurso(
    @RequestParam(name = "curso") String nombreCurso,
    @PageableDefault(size = 10, sort = "fecha", direction = Sort.Direction.ASC) Pageable paginacion) {

    Page<DatosListadoTopico> datosListadoTopicoPage = topicoService.buscarTopicosPorCurso(nombreCurso, paginacion);

    PagedModel<EntityModel<DatosListadoTopico>> pagedModel = topicoService.convertirAPagedModel(datosListadoTopicoPage,
                pagedResourcesAssembler, paginacion);

    return ResponseEntity.ok(pagedModel);
}
Agregar un nuevo mensaje a un tópico existente
@PutMapping("/{id}")
public ResponseEntity <DatosListadoMensaje>actualizarTopico(@PathVariable Long id,
    @Valid @RequestBody DatosActualizarTopico datosActualizarTopico){

    topicoService.actualizarTopico(id, datosActualizarTopico);

    DatosListadoMensaje datosUltimoMensaje = topicoService.obtenerUltimoMensaje(id);

    return ResponseEntity.ok(datosUltimoMensaje);
}
Eliminar un mensaje de un tópico
@DeleteMapping("/{idTopico}/mensajes/{idMensaje}")
public ResponseEntity<String> eliminarMensaje(@PathVariable Long idTopico,
    @PathVariable Long idMensaje) {
    
    topicoService.eliminarMensaje(idTopico, idMensaje);
    return ResponseEntity.ok("Mensaje eliminado exitosamente");
}
Cerrar un tópico
@DeleteMapping("/{id}")
@Transactional
public ResponseEntity<String> cerrarTopico(@PathVariable Long id) {
        topicoService.cerrarTopico(id);
        return ResponseEntity.ok("Tópico cerrado exitosamente");
    }
