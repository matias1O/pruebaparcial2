
## Descripción del Proyecto
Este repositorio contiene la entrega para la evaluación parcial 2. Es una API REST básica hecha con **Spring Boot 3.3.2** y **Java 17** (con conexión a base de datos usando JPA y MySQL). 

El objetivo principal de la entrega no era el código Java en sí, sino montar toda la **infraestructura y automatización DevOps** (CI/CD, pruebas con JaCoCo, seguridad con Dependabot y empaquetado en Docker).

---

## Requerimientos Cumplidos e Integraciones

### 1.Pipeline de CI/CD automatizado (GitHub Actions)
Dentro de la carpeta `.github/workflows/ci.yml` armé el flujo para que cada vez que subo cambios (`git push`), el servidor de GitHub haga lo siguiente de forma automática:
* Descargue el código limpio.
* Instale Java 17 (Temurin).
* Corra el comando de Maven para compilar y testear.
* Valide que el `Dockerfile` arme la imagen correctamente sin errores.

### 2.Reporte de Cobertura con JaCoCo
El plugin está configurado en el `pom.xml` para engancharse en la fase `verify`. 
* Mide qué porcentaje del código está cubierto por pruebas unitarias.
* El archivo de propiedades `sonar-project.properties` está en la raíz configurado con mis credenciales de SonarCloud (`matias10`) para enlazar las rutas del reporte XML.

### 3.Auditoría de Seguridad con Dependabot
Creé el archivo `.github/dependabot.xml` para automatizar la revisión de dependencias. Revisa todos los días el `pom.xml` y abre Pull Requests automáticamente en este repositorio si encuentra librerías viejas o con fallas de seguridad.

### 4.Contenerización con Docker
El proyecto incluye su propio `Dockerfile` en la raíz para empaquetar la aplicación Spring Boot en un contenedor ligero de Linux, asegurando que corre igual en cualquier computador.

---

## Cómo ejecutar y testear de forma local (en Mac)

Como el proyecto usa el wrapper de Maven nativo, para limpiar el historial, correr los tests y volver a generar el reporte HTML de JaCoCo en la máquina local, se debe usar:

```bash
./mvnw clean verify