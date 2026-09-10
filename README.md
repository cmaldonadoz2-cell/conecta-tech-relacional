# ConectaTech - Modelo Relacional Avanzado

## Descripción

Este proyecto desarrolla el modelo entidad-relación y el esquema relacional de ConectaTech, una organización de congresos profesionales presenciales, virtuales e híbridos.

## Objetivo

Analizar una narrativa de negocio, construir un modelo entidad-relación avanzado y transformarlo en un esquema relacional ejecutable en PostgreSQL.

## Tecnologías utilizadas

- PostgreSQL 18
- Docker
- Docker Compose
- Mermaid
- SQL
- Git y GitHub

## Estructura del proyecto

- `narrativa-y-reglas.md`: análisis de la narrativa y reglas de negocio.
- `diccionario-datos.md`: diccionario de datos.
- `compose.yaml`: configuración de PostgreSQL con Docker Compose.
- `.env.example`: ejemplo de variables de entorno.
- `modelo-conceptual.mmd`: modelo entidad-relación conceptual.
- `modelo-logico.mmd`: modelo lógico.
- `sql/01_schema.sql`: creación de tablas y restricciones.
- `sql/02_seed.sql`: datos iniciales.
- `sql/03_queries.sql`: consultas de demostración.
- `sql/04_invalid_tests.sql`: pruebas de operaciones inválidas.

## Ejecución

El proyecto utiliza Docker Compose para ejecutar PostgreSQL y permitir reconstruir la base de datos desde una base vacía.

## Autor

Nombre: [cristel maldonado]