## 🎯 Tarea 3. Refuerzo de arquitectura, validaciones y relación 1:N

### 📊 Información del Proyecto
- **Desarrollador:** cmartinez
- **Stack:** Spring Boot 3.5.7 + Java 17 + PostgreSQL + Docker
- **Arquitectura:** Microservicios Modernos
- **Entorno:** DevOps Native (Linux + Docker + Terminal)

## 🚀 Características Técnicas Implementadas

### ✅ Arquitectura en Capas Empresarial
- Controller Layer (REST) → Service Layer (Business) → Repository Layer (Data) → Database

### ✅ Validaciones Robustas con Bean Validation
- Validaciones de campo (`@NotBlank`, `@Size`, `@Min`)
- Mensajes personalizados en `application.properties`
- Validación de reglas de negocio (categorías únicas)

### ✅ Manejo Global de Errores
- `@RestControllerAdvice` para manejo centralizado
- Respuestas JSON uniformes (timestamp, status, message, path)
- Códigos HTTP específicos (400, 404, 409)

### ✅ Relación 1:N Cursos ↔ Categorías
- Entidades JPA con relaciones `@OneToMany`/`@ManyToOne`
- Endpoints específicos para relaciones (`/api/categorias/{id}/cursos`)
- Validación de integridad referencial


## 🏗️ Estructura del Proyecto

```
modern-springboot-project/
├── 🐳 docker-compose.yml
├── 📦 pom.xml
├── 📁 src/
│ └── 📁 main/
│ ├── 📁 java/
│ │ └── 📁 dev/
│ │ └── 📁 cmartinez/
│ │ ├── 🎯 controller/ (REST APIs)
│ │ ├── 🏗️ entity/ (JPA Entities)
│ │ ├── 💾 repository/ (Spring Data)
│ │ ├── 🔧 service/ (Business Logic)
│ │ ├── 📋 dto/ (Data Transfer Objects)
│ │ ├── ⚠️ exception/ (Error Handling)
│ │ └── 🚀 mi_primer_springboot/ (Main App)
│ └── 📁 resources/
│ └── ⚙️ application.properties
└── 📄 README.md

```


## 🐳 Ejecución con Docker (Enfoque DevOps)

### 1. Iniciar Infraestructura
```bash
# Levantar todos los servicios
docker-compose up -d

# Verificar estado
docker-compose ps
```

### 2. Verificar Servicios
```bash
# Aplicación Spring Boot
curl http://localhost:8080/actuator/health

# Base de datos PostgreSQL
docker exec -it springboot-postgres psql -U cmartinez -d cursos_db -c "\dt"
```

### 3. Ejecutar Aplicación
```bash
# Acceder al contenedor de desarrollo
docker exec -it springboot-dev bash

# Compilar y ejecutar
mvn clean compile
mvn spring-boot:run
```

## 📡 Endpoints Implementados
### 🎯 Gestión de Cursos
```
Método	Endpoint	Descripción
GET	/api/cursos	Listar todos los cursos
GET	/api/cursos/{id}	Obtener curso por ID
POST	/api/cursos	Crear nuevo curso
PUT	/api/cursos/{id}	Actualizar curso existente
DELETE	/api/cursos/{id}	Eliminar curso
GET	/api/cursos/buscar?nombre={nombre}	Buscar cursos por nombre
GET	/api/cursos/activos	Obtener cursos activos
```

### 🗂️ Gestión de Categorías
```
Método	Endpoint	Descripción
GET	/api/categorias	Listar todas las categorías
GET	/api/categorias/{id}	Obtener categoría por ID
POST	/api/categorias	Crear nueva categoría
PUT	/api/categorias/{id}	Actualizar categoría existente
DELETE	/api/categorias/{id}	Eliminar categoría
GET	/api/categorias/buscar?nombre={nombre}	Buscar categorías por nombre
GET	/api/categorias/activas	Obtener categorías activas
GET	/api/categorias/{id}/cursos	Obtener cursos por categoría
```

## 🧪 Pruebas y Validaciones
### Validaciones de Entrada (HTTP 400)
```bash
# Curso con datos inválidos
curl -X POST http://localhost:8080/api/cursos \
  -H "Content-Type: application/json" \
  -d '{"nombre": "", "profesor": "", "duracionHoras": 0}'

# Respuesta esperada:
{
  "status": 400,
  "error": "Bad Request",
  "message": "Errores de validación: {duracionHoras=La duración debe ser al menos 1 hora, profesor=El profesor es obligatorio, nombre=El nombre del curso es obligatorio}",
  "path": "/api/cursos",
  "timestamp": "2025-11-05T01:41:07.358914416"
}
```
### Conflictos de Negocio (HTTP 409)
```bash
# Categoría duplicada
curl -X POST http://localhost:8080/api/categorias \
  -H "Content-Type: application/json" \
  -d '{"nombre": "Programación", "descripcion": "Duplicado"}'

# Eliminar categoría con cursos
curl -X DELETE http://localhost:8080/api/categorias/1
```

### Recursos No Encontrados (HTTP 404)
```bash
# Curso inexistente
curl http://localhost:8080/api/cursos/999
```

## Modelo de Datos
###  Entidad Curso
```java
@Entity
@Table(name = "cursos")
public class Curso {
    private Long id;
    private String nombre;          // @NotBlank, @Size(max=100)
    private String profesor;        // @NotBlank, @Size(max=100)
    private String descripcion;     // @Size(max=500)
    private Integer duracionHoras;  // @Min(1)
    private LocalDateTime fechaCreacion;
    private Boolean activo;
    private Categoria categoria;    // @ManyToOne
}
```
###  Entidad Categoría
```java
@Entity
@Table(name = "categorias")
public class Categoria {
    private Long id;
    private String nombre;          // @NotBlank, @Size(max=100), Unique
    private String descripcion;     // @Size(max=500)
    private LocalDateTime fechaCreacion;
    private Boolean activo;
    private List<Curso> cursos;     // @OneToMany
}
```
## 🔧 Configuración
### Docker Compose
```yaml
services:
  dev-environment:
    image: maven:3.9-eclipse-temurin-17
    container_name: springboot-dev
    working_dir: /app
    ports: ["8080:8080"]
    depends_on: [postgres]

  postgres:
    image: postgres:15
    container_name: springboot-postgres
    environment:
      POSTGRES_DB: cursos_db
      POSTGRES_USER: cmartinez
      POSTGRES_PASSWORD: password123
    ports: ["5432:5432"]
```

### Application Properties
```properties
# Database
spring.datasource.url=jdbc:postgresql://springboot-postgres:5432/cursos_db
spring.datasource.username=cmartinez
spring.datasource.password=password123

# JPA
spring.jpa.hibernate.ddl-auto=create-drop
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.format_sql=true

# Validation Messages
curso.nombre.notblank=El nombre del curso es obligatorio
curso.nombre.size=El nombre no puede exceder los 100 caracteres
# ... más mensajes personalizados
```

## Screenshots
- [Estado Contenedor](https://github.com/ccrrmmrr/curso-SpringBoot-ApacheKafka-tareas/blob/main/clase3/screenshots/docker_compose_ps.PNG)
- [Health Check PostgreSQL](https://github.com/ccrrmmrr/curso-SpringBoot-ApacheKafka-tareas/blob/main/clase3/screenshots/health_check_postgres.PNG)
- [Health Check Aplicacion](https://github.com/ccrrmmrr/curso-SpringBoot-ApacheKafka-tareas/blob/main/clase3/screenshots/aplicacion.PNG)
- [Validacion 400 Bad Request](https://github.com/ccrrmmrr/curso-SpringBoot-ApacheKafka-tareas/blob/main/clase3/screenshots/validacion.PNG)
- [Conflicto 409](https://github.com/ccrrmmrr/curso-SpringBoot-ApacheKafka-tareas/blob/main/clase3/screenshots/conflicto.PNG)
- [Prueba de Relacion](https://github.com/ccrrmmrr/curso-SpringBoot-ApacheKafka-tareas/blob/main/clase3/screenshots/relacion.PNG)







