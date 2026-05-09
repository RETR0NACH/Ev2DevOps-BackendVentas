# /back-Ventas_SpringBoot/README.md

# Backend Ventas - Innovatech Chile

Este microservicio es responsable de la orquestación y persistencia de las operaciones de venta del ecosistema Innovatech. Está construido bajo una arquitectura de API REST utilizando el ecosistema de Spring Boot.

## 🚀 Tecnologías Utilizadas
- **Lenguaje:** Java 17 (OpenJDK).
- **Framework:** Spring Boot 3.x con Spring Data JPA.
- **Base de Datos:** MySQL 8.0 (conectado vía AWS RDS/EC2).
- **Documentación:** Swagger / OpenAPI UI.

## 📦 Componentes Creados (Entregables Técnicos)
1. **Dockerfile Optimizado:** - Implementación de **Multi-stage build** (Maven para construcción y JRE Alpine para ejecución).
   - Seguridad **Non-root**: Ejecución bajo el usuario `spring` para mitigar riesgos de escalada de privilegios.
2. **Pipeline CI/CD (.github/workflows/deploy.yml):**
   - Automatización total en la rama `deploy`.
   - Flujo: Build -> Push a Amazon ECR -> Deploy en EC2 mediante AWS SSM.
3. **Externalización de Configuración:** Uso de variables de entorno para endpoints de BD (`DB_ENDPOINT`, `DB_PORT`), cumpliendo con los estándares de *12-Factor App*.

## 🛠️ Instalación y Uso Local
Se recomienda el uso del `docker-compose.yml` ubicado en la raíz del proyecto para levantar este servicio junto a su base de datos dependiente.