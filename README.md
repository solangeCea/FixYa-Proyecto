# FixYa Proyecto

FixYa es una plataforma web para la gestión de servicios técnicos, desarrollada con React, TypeScript, Vite, Tailwind CSS, FastAPI, SQLAlchemy, PostgreSQL y Docker.

## Requisitos

Antes de ejecutar el proyecto se debe tener instalado:

- Git
- Docker
- Docker Compose

## Instalación

Clonar el repositorio principal:

```bash
git clone https://github.com/solangeCea/FixYa-Proyecto.git
cd FixYa-Proyecto
Clonar el backend dentro de la carpeta del proyecto:

git clone https://github.com/vanneglezn/FixYa.git

Clonar el frontend dentro de la carpeta del proyecto:

git clone https://github.com/solangeCea/fixya-frontend.git

docker compose up -d --build

docker exec -i db psql -U postgres -d fixya_db < FixYa/database/seed.sql