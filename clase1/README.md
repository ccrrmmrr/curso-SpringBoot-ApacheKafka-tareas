# Tarea1. Mi Primer Proyecto Spring Boot Moderno

## Información del Proyecto

- **Nombre:** mi-primer-springboot
- **Desarrollador:** Carlos Martinez
- **Versión de Spring Boot:** 3.5.7
- **Java:** 17
- **Build Tool:** Maven 3.9+
- **Arquitectura:** Docker + Spring Boot

## 🚀 Características

- ✅ Entorno de desarrollo con Docker
- ✅ Spring Boot 3.x con Java 17
- ✅ Controller REST personalizado
- ✅ Configuración moderna y reproducible

## 📁 Estructura del Proyecto
```
mi-primer-springboot/
├── 📄 README.md
├── ⚙️ docker-compose.yml
├── 📦 pom.xml
├── 🛠️ mvnw
├── 🖥️ mvnw.cmd
├── 📖 HELP.md
├── 🔧 .gitignore
├── 🔒 .gitattributes
├── 📁 .mvn/
│   └── 📁 wrapper/
│       └── 📄 maven-wrapper.properties
├── 📁 src/
│   ├── 📁 main/
│   │   ├── 📁 java/
│   │   │   └── 📁 dev/
│   │   │       └── 📁 cmartinez/
│   │   │           ├── 📁 controller/
│   │   │           │   └── 🎯 HolaController.java
│   │   │           └── 📁 mi_primer_springboot/
│   │   │               └── 🚀 MiPrimerSpringbootApplication.java
│   │   └── 📁 resources/
│   │       ├── ⚙️ application.properties
│   │       ├── 📁 static/
│   │       └── 📁 templates/
│   └── 📁 test/
│       └── 📁 java/
│           └── 📁 dev/
│               └── 📁 cmartinez/ (✅ ACTUALIZADO)
│                   └── 📁 mi_primer_springboot/
│                       └── 🧪 MiPrimerSpringbootApplicationTests.java
└── 📁 target/ (🚫 ignorado por Git)
```

### `src/main/java/dev/cmartinez/mi_primer_springboot/`
- `MiPrimerSpringbootApplication.java`: Clase principal que inicia la aplicación Spring Boot con la anotación `@SpringBootApplication`

### `src/main/java/dev/cmartinez/controller/`
- `HolaController.java`: Controlador REST con endpoints personalizados para demostrar el funcionamiento

### `src/main/resources/`
- `application.properties`: Archivo de configuración de Spring Boot (propiedades, puertos, etc.)

### `src/test/`
- Directorio para pruebas unitarias y de integración con JUnit y Spring Test
- `MiPrimerSpringbootApplicationTests.java`: Test básico de la aplicación

### `pom.xml`
- Archivo de configuración de Maven que define dependencias, plugins y configuración del proyecto

### `target/`
- Directorio generado por Maven que contiene los archivos compilados, JAR final y recursos de build

### `docker-compose.yml`
- Configuración de Docker para el entorno de desarrollo con JDK 17 y mapeo de puertos

## 🏃 Cómo Ejecutar

### Opción 1: Con Docker (Recomendado)
```bash
# Iniciar entorno de desarrollo
docker-compose up -d dev-environment

# Entrar al contenedor
docker exec -it springboot-dev bash

# Ejecutar la aplicación
mvn spring-boot:run
```
## Dependencias Principales

Lista las dependencias en `pom.xml` y explica brevemente cada una:
- spring-boot-starter-web: 
  Starter completo para aplicaciones web y RESTful.
Incluye:
       Spring MVC - Framework para aplicaciones web
       Tomcat embebido - Servidor web integrado (no necesita instalación externa)
       Jackson - Librería para procesar JSON (requests/responses automáticos)
       Spring Boot Auto-configuration - Configuración automática basada en classpath
       Validación - Anotaciones para validar datos (@NotNull, @Size, etc.)
¿Para qué sirve?
       Crea controladores REST, maneja peticiones HTTP, serializa/deserializa JSON automáticamente.

- spring-boot-starter-test: [Tu explicación]
  Starter para testing de aplicaciones Spring Boot.
Incluye:
       JUnit 5 - Framework principal para pruebas unitarias
       Spring Test & Spring Boot Test - Utilidades para testing de Spring
       AssertJ - Librería de aserciones fluidas y legibles
       Hamcrest - Matchers para pruebas más expresivas
       Mockito - Framework para crear mocks y stubs
       JSONassert - Librería para assertions de JSON
       JsonPath - XPath para JSON
¿Para qué sirve?
       Escribir tests unitarios, de integración, mockear dependencias y probar endpoints REST.

## Conceptos Aprendidos

#### ¿Qué es Spring Boot?
     Framework que simplifica radicalmente el desarrollo de aplicaciones Spring mediante:
     - Auto-configuración: Analiza el classpath y configura automáticamente los beans necesarios
     - Servidores embebidos: Incluye Tomcat, Jetty o Undertow dentro del JAR
     - Convención sobre configuración: Configuraciones sensibles por defecto
     - Starter dependencies: Dependencias preempaquetadas para casos de uso comunes
     - Producción lista: Health checks, métricas, externalización de configuración
       Ventaja: De "cero a producción" en minutos, sin XML de configuración.

#### ¿Qué es Maven?
     Herramienta de construcción y gestión de dependencias que:
     - Gestión de dependencias: Descarga automáticamente librerías de repositorios centrales
     - Ciclo de vida de build: Compilación, testing, empaquetado en fases estandarizadas
     - Configuración declarativa: Define QUÉ hacer, no CÓMO (a diferencia de Ant)
     - Sistema de plugins: Extensible para cualquier tarea (deploy, análisis, etc.)
     - Build reproducible: Mismo resultado en cualquier máquina
       Ejemplo: mvn spring-boot:run compila, resuelve dependencias y ejecuta.

#### ¿Qué significa "Tomcat started on port 8080"?
     Indica que:
     - Tomcat: Servidor web/servlet container está integrado en tu aplicación
     - Puerto 8080: Escucha peticiones HTTP en ese puerto
     - Embebido: No necesitas instalar Tomcat por separado
     - Listo para producción: El mismo servidor que usarías en producción
       Ventaja: Desarrollas y despliegas con el mismo entorno.


#### ¿Para qué sirve la anotación @SpringBootApplication?
      Es una anotación compuesta que combina tres anotaciones esenciales:
      1. @Configuration - Marca la clase como fuente de definiciones de beans
      2. @EnableAutoConfiguration - Habilita la magia de auto-configuración de Spring Boot
      3. @ComponentScan - Escanea el package actual y sub-packages en busca de componentes

## Screenshot
- [Versiones](https://github.com/ccrrmmrr/mi-primer-springboot/tree/main/screenshots/01_versiones.PNG)
- [Spring-boot](https://github.com/ccrrmmrr/mi-primer-springboot/tree/main/screenshots/02_spring.PNG)
- [Primer Proyecto](https://github.com/ccrrmmrr/mi-primer-springboot/tree/main/screenshots/03_primerproyecto.PNG)

## Autor
Carlos Roberto Martinez Rivadeneira - Curso Spring Boot & Kafka
