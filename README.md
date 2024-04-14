# MEAN Color App

## Objetivo
El objetivo de este proyecto es demostrar una aplicación completa usando el stack MEAN (MongoDB, Express.js, Angular, Node.js), implementada con Docker y gestionada como microservicios.

## Tecnologías Utilizadas
- MongoDB
- Express.js
- Angular
- Node.js
- Docker
- Docker Compose

## Estructura del Proyecto
Este proyecto está dividido en tres submódulos:
- Backend: Contiene toda la lógica del servidor, API y conexión a la base de datos.
- Frontend: Una aplicación Angular que consume la API del backend.
- MongoDB: Una base de datos para almacenar los datos de colores.

## Cómo Ejecutar
Para ejecutar toda la aplicación:
1. Clona este repositorio:
```
git clone --recurse-submodules https://github.com/your-username/mean-color-app.git
```
2. Navega al directorio del repositorio y ejecuta Docker Compose:
```
cd mean-color-app
docker-compose up --build
```
Esto construirá y levantará todos los servicios necesarios.

## Licencia
Especifica aquí tu tipo de licencia.

