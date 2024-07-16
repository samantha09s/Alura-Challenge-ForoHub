<h1 align="center">ForoHub API REST</h1>

<div align="center">
  <img src="https://img.shields.io/badge/Java-17-007396?style=for-the-badge&logo=java&logoColor=white" alt="Java">
  <img src="https://img.shields.io/badge/Spring%20Boot-3.3.0-6DB33F?style=for-the-badge&logo=spring-boot&logoColor=white" alt="Spring Boot">
  <img src="https://img.shields.io/badge/GitHub-Repository-181717?style=for-the-badge&logo=github&logoColor=white" alt="GitHub">
  <img src="https://img.shields.io/badge/MySQL-8.0-4479A1?style=for-the-badge&logo=mysql&logoColor=white" alt="MySQL">
  <img src="https://img.shields.io/badge/Maven-Project%20Management-C71A36?style=for-the-badge&logo=apache-maven&logoColor=white" alt="Maven">
</div>

## Tabla de Contenidos
- [Plataforma de Comunicación](#plataforma-de-comunicación)
- [Funcionalidades Destacadas](#funcionalidades-destacadas)
- [Tecnologías Utilizadas](#tecnologías-utilizadas)
- [Estructura del Proyecto](#estructura-del-proyecto)
- [Validaciones y Tratamiento de Errores](#validaciones-y-tratamiento-de-errores)
- [Implementación de Base de Datos](#implementación-de-base-de-datos)
- [Servicio de Autenticación/Autorización](#servicio-de-autenticaciónautorización)
- [Configuración](#configuración)
- [Información de Licencia](#información-de-licencia)
- [Agradecimientos](#agradecimientos)

## Plataforma de Comunicación

**ForoHub** es una emocionante plataforma que replica la lógica de negocio de un foro, permitiendo a los usuarios realizar operaciones CRUD (Crear, Leer, Actualizar, Eliminar) sobre tópicos, respuestas y usuarios. Nuestra API REST está implementada utilizando Spring Boot y sigue las mejores prácticas del modelo REST. Además, integramos validaciones de negocio, autenticación y autorización para garantizar una experiencia segura y eficiente.

## Funcionalidades Destacadas

1. **Crear Registros:** Permite a los usuarios agregar nuevos tópicos, respuestas y usuarios a la base de datos.
2. **Listar Registros:** Devuelve una lista completa de todos los registros disponibles.
3. **Ver Detalles:** Muestra información específica sobre un tópico, respuesta o usuario en particular.
4. **Actualizar Información:** Permite a los usuarios modificar datos en registros existentes.
5. **Eliminar Registros:** Permite a los usuarios borrar un registro específico.
6. **Autenticación de Usuarios:** Facilita la autenticación mediante credenciales y la obtención de un token JWT para acceder a rutas protegidas.

## Tecnologías Utilizadas

| Tecnología             | Características                                                                                  |
|------------------------|--------------------------------------------------------------------------------------------------|
| **Java JDK v17**       | La última versión de Java, que ofrece un mejor rendimiento, nuevas funciones y soporte mejorado. |
| **Maven v4**           | Herramienta de gestión de proyectos y automatización de compilación.                             |
| **Spring Boot v3.2.6** | Marco de desarrollo web de Java para aplicaciones robustas y escalables.                         |
| **Spring Data JPA**    | Acceso a datos relacional simplificado para bases de datos SQL.                                  |
| **Spring Security**    | Marco integral de seguridad web para proteger aplicaciones.                                      |
| **Spring Web**         | Módulos para desarrollar aplicaciones web RESTful y tradicionales.                               |
| **SpringDoc-OpenAPI**  | Generación automática de documentación OpenAPI desde anotaciones de Spring.                      |
| **Auth0**              | Plataforma de gestión de identidad y acceso para autenticación y autorización.                   |
| **MySQL v8**           | Sistema de gestión de bases de datos relacional popular y confiable.                             |
| **Flyway Migration**   | Herramienta para gestionar versiones de bases de datos de manera segura.                         |
| **Validation**         | Conjunto de herramientas para validar datos de entrada.                                          |
| **Lombok**             | Procesador de anotaciones para reducir la verbosidad del código.                                 |

## Estructura del Proyecto

El proyecto sigue el patrón **MVC (Modelo-Vista-Controlador)** y se organiza en los siguientes paquetes:

1. **Domain (Modelo):** Contiene las entidades de Tópicos, Respuestas, Cursos y Usuarios, junto con sus servicios que implementan las reglas de negocio.
2. **Controller:** Maneja las solicitudes HTTP a través de controladores REST.
3. **Service:** Lógica de negocio y comunicación con los repositorios.
4. **Repository:** Interacción con la base de datos mediante Spring Data JPA.
5. **Security:** Autenticación y autorización utilizando Spring Security y JWT.
6. **Validation:** Reglas de negocio para validaciones específicas.
7. **Exception Handling:** Gestión de excepciones y errores de la aplicación.

## Validaciones y Tratamiento de Errores

- **Reglas de Negocio:** Validaciones para evitar duplicados y garantizar la integridad de los datos.
- **Validaciones de Integridad:** Excepciones personalizadas para manejar datos no encontrados.
- **Tratamiento de Errores:** Configuración para proteger información sensible y capturar excepciones específicas (por ejemplo, errores 400 o 404).

## Implementación de Base de Datos

Se utiliza MySQL como gestor de base de datos, y Flyway para el control de versiones y migraciones.

<div align="center">
  <img src="https://via.placeholder.com/800x400.png?text=Esquema+de+Base+de+Datos" alt="Esquema de Base de Datos">
</div>

## Servicio de Autenticación/Autorización

Para garantizar la seguridad y el acceso controlado a nuestra API, se implemento un sistema de autenticación y autorización. A continuación, se describen los detalles:

- **Autenticación:** Utilizamos Spring Security para gestionar la autenticación. Los usuarios deben proporcionar su correo electrónico y contraseña para acceder a la API. Además, se ha configurado el sistema en modo Stateless para mantener la eficiencia y escalabilidad.

- **Autorización**: Nuestra API utiliza tokens JWT (JSON Web Tokens) generados por la librería Auth0. Estos tokens se utilizan para autorizar las solicitudes de los usuarios. Cada solicitud API debe incluir el token en el encabezado, excepto en los endpoints específicos de inicio de sesión y registro de usuarios.

### Ejemplo de Uso

Para obtener un token JWT válido, los usuarios deben autenticarse correctamente. Aquí hay un ejemplo de cómo se vería una solicitud de inicio de sesión:

    POST /api/login HTTP/1.1
    Host: tu-servidor.com
    Content-Type: application/json
    
    {
      "email": "usuario@example.com",
      "password": "contraseña-secreta"
    }

La respuesta incluirá un token JWT que se puede utilizar en las solicitudes posteriores:

    {
      "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
    }

### Crear un Tópico

    POST /api/topics HTTP/1.1
    Host: tu-servidor.com
    Content-Type: application/json
    
    {
      "title": "Nuevo Tópico",
      "content": "Contenido del tópico",
      "userId": 1
    }

### Actualizar un Tópico

    PUT /api/topics/1 HTTP/1.1
    Host: tu-servidor.com
    Content-Type: application/json
    
    {
      "title": "Título Actualizado",
      "content": "Contenido actualizado"
    }

### Eliminar un Tópico

    DELETE /api/topics/1 HTTP/1.1
    Host: tu-servidor.com
    Content-Type: application/json

## Configuración

Para ejecutar el proyecto en tu equipo, sigue estos pasos:
1. **Clonar el Repositorio:** Comienza clonando este repositorio en tu máquina local.
2. **Importar el Proyecto:** Abre el proyecto en IntelliJ o cualquier otro IDE compatible con Java.
3. **Configurar la Base de Datos:** Crea una base de datos llamada "foro-api" en MySQL.
4. **Variables de Entorno:** Configura las variables de entorno para la base de datos y JWT en el archivo `application.properties`.
5. **Ejecutar el Proyecto:** Inicia el proyecto.
6. **Prueba las Solicitudes:** Utiliza un cliente REST como Insomnia o Postman para crear y probar las solicitudes.
7. **Documentación con SpringDoc:** También puedes explorar la documentación de la API utilizando la herramienta Swagger proporcionada por SpringDoc.

<div align="center">
  <img src="https://via.placeholder.com/800x400.png?text=Pasos+de+Configuracion+del+Proyecto" alt="Pasos de Configuración del Proyecto">
</div>

## Información de Licencia

Este proyecto está licenciado bajo la Licencia MIT - consulta el archivo [LICENSE](LICENSE) para más detalles.

## Agradecimientos

Agradezco al equipo ONE, Alura Latam y toda la comunidad por la oportunidad de ser parte de esta experiencia y por aprender tanto con sus cursos, retroalimentaciones y conocimientos.

<div align="center">
  <a href="https://www.linkedin.com/in/samanthamunguia/">
    <img src="https://img.shields.io/badge/linkedin-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn">
  </a>
</div>

> [!NOTE]
> Utiliza siempre la última versión de Java y Spring Boot para asegurar compatibilidad y seguridad..

> [!WARNING]
> No expongas tus credenciales de la base de datos ni tus claves secretas JWT en un entorno público..
