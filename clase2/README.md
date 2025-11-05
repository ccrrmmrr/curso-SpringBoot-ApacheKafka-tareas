
## 🎯 Tarea 2 - CRUD Básico de Cursos

### Objetivo
Construir un CRUD completo para la entidad Curso utilizando Spring Data JPA, Docker Compose y pruebas con cURL/Postman.

### Requerimientos Cumplidos ✅

#### Funcionales:
- **POST /api/cursos** - Crea un nuevo curso
- **GET /api/cursos** - Lista todos los cursos
- **GET /api/cursos/{id}** - Obtiene curso por ID
- **PUT /api/cursos/{id}** - Actualiza curso existente
- **DELETE /api/cursos/{id}** - Elimina curso
- **GET /api/cursos/buscar?nombre={nombre}** - Búsqueda por nombre
- **GET /api/cursos/activos** - Filtra cursos activos

#### Técnicos:
- ✅ Repository Spring Data JPA (`CursoRepository`)
- ✅ PostgreSQL con Docker Compose
- ✅ Controlador REST con inyección de dependencias
- ✅ Entidad JPA con validaciones de base de datos

## 📁 Estructura del Proyecto

```
mi-primer-springboot/
├── 📄 README.md
├── ⚙️ docker-compose.yml
├── 📦 pom.xml
├── 📁 src/
│ ├── 📁 main/
│ │ ├── 📁 java/
│ │ │ └── 📁 dev/
│ │ │ └── 📁 cmartinez/
│ │ │ ├── 📁 controller/
│ │ │ │ └── 🎯 CursoController.java
│ │ │ ├── 📁 entity/
│ │ │ │ └── 🏗️ Curso.java
│ │ │ ├── 📁 repository/
│ │ │ │ └── 💾 CursoRepository.java
│ │ │ └── 📁 mi_primer_springboot/
│ │ │ └── 🚀 MiPrimerSpringbootApplication.java
│ │ └── 📁 resources/
│ │ └── ⚙️ application.properties
│ └── 📁 test/
│ └── 📁 java/
│ └── 📁 dev/
│ └── 📁 cmartinez/
│ └── 📁 mi_primer_springboot/
│ └── 🧪 MiPrimerSpringbootApplicationTests.java
```

## Información del Proyecto

- **Nombre:** mi-primer-springboot
- **Desarrollador:** cmartinez
- **Versión de Spring Boot:** 3.5.7
- **Java:** 17
- **Build Tool:** Maven 3.9+
- **Arquitectura:** Docker + Spring Boot + PostgreSQL

## 🚀 Características

- ✅ Entorno de desarrollo con Docker
- ✅ Spring Boot 3.x con Java 17
- ✅ API REST completa para gestión de cursos
- ✅ PostgreSQL integrado y persistente
- ✅ Configuración moderna y reproducible

## 🏃 Cómo Ejecutar

### 1. Iniciar el entorno Docker:
```bash
docker-compose up -d
```
### 2. Verificar contenedores:
```bash
docker ps
```
### 3. Ejecutar la aplicación:
```bash
docker exec -it springboot-dev bash
cd /app
mvn spring-boot:run
```

## 🛠️ Configuración:
### Docker Compose
```yaml
services:
  dev-environment:
    image: maven:3.9-eclipse-temurin-17
    container_name: springboot-dev
    working_dir: /app
    volumes:
      - .:/app
    ports:
      - "8080:8080"
    depends_on:
      - postgres

  postgres:
    image: postgres:15
    container_name: springboot-postgres
    environment:
      POSTGRES_DB: cursos_db
      POSTGRES_USER: cmartinez
      POSTGRES_PASSWORD: password123
    ports:
      - "5432:5432"
    volumes:
      - postgres-data:/var/lib/postgresql/data
```
### Application Proporties:
```properties
spring.datasource.url=jdbc:postgresql://springboot-postgres:5432/cursos_db
spring.datasource.username=cmartinez
spring.datasource.password=password123
spring.jpa.hibernate.ddl-auto=create-drop
spring.jpa.show-sql=true
```

## 📦 Dependencias Principales
```
spring-boot-starter-web
Starter completo para aplicaciones web y RESTful.

spring-boot-starter-data-jpa
Integración con Spring Data JPA y Hibernate.

postgresql
Driver de conexión para PostgreSQL.
```


## 🔧 Pruebas de los EndPoints
### Crear un curso
```bash
curl -X POST http://localhost:8080/api/cursos \
  -H "Content-Type: application/json" \
  -d '{
    "nombre": "Spring Boot Avanzado",
    "profesor": "Carlos Martinez",
    "descripcion": "Curso avanzado de Spring Boot con Docker y PostgreSQL",
    "duracionHoras": 40
  }'
```

### Listar todos los cursos:
```bash
http://localhost:8080/api/cursos
```

### Obtener curso por ID:
```bash
http://localhost:8080/api/cursos
```

### Buscar cursos por nombre:
```bash
curl "http://localhost:8080/api/cursos/buscar?nombre=Spring"
```

### Actualizar curso:
```bash
curl -X PUT http://localhost:8080/api/cursos/1 \
  -H "Content-Type: application/json" \
  -d '{
    "nombre": "Spring Boot PRO",
    "profesor": "cmartinez",
    "descripcion": "Curso PRO actualizado",
    "duracionHoras": 60,
    "activo": true
  }'
```

### Eliminar curso:
```bash
curl -X DELETE http://localhost:8080/api/cursos/1
```

## Screenshots
- [Repositorio Publico](https://github.com/ccrrmmrr/mi-primer-springboot)
- [SpringBoot](https://github.com/ccrrmmrr/curso-SpringBoot-ApacheKafka-tareas/blob/main/clase2/screenshots/log_springBoot01.PNG)
- [Operaciones](https://github.com/ccrrmmrr/curso-SpringBoot-ApacheKafka-tareas/blob/main/clase2/screenshots/operaciones_CRUD.PNG)
- [Docker_Compose](https://github.com/ccrrmmrr/curso-SpringBoot-ApacheKafka-tareas/blob/main/clase2/screenshots/docker_compose_ps.PNG)





