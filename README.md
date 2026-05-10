# 🛒 Backend Ventas - Innovatech Chile

![Java](https://img.shields.io/badge/Java-17-ED8B00?style=for-the-badge&logo=java&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-3.x-6DB33F?style=for-the-badge&logo=spring-boot&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-8.0-4479A1?style=for-the-badge&logo=mysql&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-Ready-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-Cloud-232F3E?style=for-the-badge&logo=amazon-aws&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/CI%2FCD-GitHub_Actions-2088FF?style=for-the-badge&logo=github-actions&logoColor=white)

## 📖 Descripción del Microservicio

Este repositorio contiene el microservicio de **Ventas** para el ecosistema logístico y comercial de Innovatech Chile. Diseñado bajo una arquitectura orientada a microservicios y RESTful, este componente es responsable de la orquestación, validación y persistencia de las operaciones de compra.

A nivel de infraestructura, este servicio opera dentro de la **Capa de Aplicación (App Tier)** en una arquitectura distribuida de 3 capas en AWS, garantizando alta disponibilidad y aislamiento de red (Zero Trust).

---

## 🚀 Stack Tecnológico

### Backend & Datos
* **Lenguaje:** Java 17 (OpenJDK).
* **Framework:** Spring Boot 3.x con Spring Data JPA.
* **Base de Datos:** MySQL 8.0 (Hosteado en capa privada `ec2-gdata`).
* **Documentación API:** Swagger / OpenAPI 3.0.

### Infraestructura & DevOps
* **Contenerización:** Docker (Motor inmutable).
* **CI/CD:** GitHub Actions.
* **Registro de Imágenes:** Amazon Elastic Container Registry (ECR).
* **Orquestación Cloud:** AWS Systems Manager (SSM) sobre EC2.

---

## 🛠️ Arquitectura DevOps & Seguridad (Entregables Técnicos)

Este proyecto fue construido aplicando prácticas modernas de Site Reliability Engineering (SRE):

1. **Inmutabilidad y Seguridad Docker:**
   * **Multi-stage Build:** Compilación optimizada usando Maven en la primera etapa, y un entorno JRE Alpine ultraligero para la ejecución.
   * **Privilegios Non-Root:** El contenedor se ejecuta bajo el usuario restringido `spring`, mitigando vectores de ataque por escalamiento de privilegios.
2. **Pipeline de Despliegue Continuo (CI/CD):**
   * Automatización mediante `.github/workflows/deploy.yml`.
   * El flujo detecta integraciones (Merges) hacia la rama `main`, compila el artefacto `.jar`, construye la imagen Docker, la publica en Amazon ECR y utiliza **AWS SSM** para actualizar el contenedor en la EC2 privada sin necesidad de abrir el puerto SSH (22).
3. **Principios 12-Factor App:**
   * **Configuración Externalizada:** Las credenciales de la base de datos y puertos nunca se escriben en el código, sino que se inyectan dinámicamente mediante variables de entorno en el pipeline.

---

## ⚙️ Variables de Entorno (Configuration)

Para ejecutar este proyecto en cualquier entorno, el sistema espera recibir las siguientes variables de entorno que sobreescriben el `application.properties`:

| Variable de Entorno     | Descripción | Ejemplo |
| :--- | :--- | :--- |
| `SPRING_DATASOURCE_URL` | Cadena de conexión JDBC hacia MySQL | `jdbc:mysql://10.0.x.x:3306/tienda_db?allowPublicKeyRetrieval=true&useSSL=false` |
| `DB_USERNAME`           | Usuario de la base de datos         | `retr0nach` |
| `DB_PASSWORD`           | Contraseña segura del usuario       | `***` |

> **Nota para Producción:** En el entorno de AWS, estas variables se inyectan de forma segura a través de los **Secrets de GitHub Actions**.

---

## 💻 Ejecución en Entorno Local (Desarrollo)

Para levantar este microservicio en una máquina de desarrollo local, se recomienda utilizar el archivo orquestador de la raíz del monorepo original.

1. Asegúrate de tener Docker y Docker Compose instalados.
2. Posiciónate en la carpeta raíz del proyecto (fuera de este repositorio).
3. Ejecuta el entorno completo:
   ```bash
   docker compose up -d