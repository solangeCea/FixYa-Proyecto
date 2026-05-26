# FixYa Proyecto

FixYa es una plataforma web para conectar clientes con tecnicos de servicios del hogar. El proyecto usa React, TypeScript, Vite, Tailwind CSS, FastAPI, SQLAlchemy, PostgreSQL, JWT y Docker.

## Requisitos

Antes de ejecutar el proyecto instala:

- Git
- Docker Desktop
- Docker Compose

No es necesario instalar Node.js, npm, Python ni PostgreSQL localmente si se ejecuta con Docker.

## Pasos obligatorios para ejecutar el proyecto

Este repositorio maestro no incluye directamente el codigo del backend ni del frontend. Despues de clonar `FixYa-Proyecto`, es obligatorio clonar tambien los repositorios `FixYa` y `fixya-frontend` dentro de la carpeta principal.

Ejecuta estos comandos en orden:

```bash
git clone https://github.com/solangeCea/FixYa-Proyecto.git
cd FixYa-Proyecto

git clone https://github.com/vanneglezn/FixYa.git
git clone https://github.com/solangeCea/fixya-frontend.git

docker compose up -d --build

docker exec -i db psql -U postgres -d fixya_db < FixYa/database/seed.sql
```

Luego abre la web en:

```txt
http://localhost:5173
```

## Estructura esperada

El proyecto principal debe contener dos repositorios internos:

```txt
FixYa-Proyecto/
|-- FixYa/             # Backend FastAPI
|-- fixya-frontend/    # Frontend React + Vite
|-- docker-compose.yml
`-- README.md
```

Los nombres de carpetas deben quedar exactamente como `FixYa` y `fixya-frontend`, porque `docker-compose.yml` usa esas rutas.

## Instalacion desde cero

Clonar el repositorio principal:

```bash
git clone https://github.com/solangeCea/FixYa-Proyecto.git
cd FixYa-Proyecto
```

Clonar el backend dentro de la carpeta del proyecto:

```bash
git clone https://github.com/vanneglezn/FixYa.git
```

Clonar el frontend dentro de la carpeta del proyecto:

```bash
git clone https://github.com/solangeCea/fixya-frontend.git
```

## Levantar el sistema

Construir y levantar los contenedores:

```bash
docker compose up -d --build
```

Verificar que los contenedores esten corriendo:

```bash
docker compose ps
```

Deberian aparecer estos servicios:

- `db`
- `fixya_backend`
- `fixya_frontend`

## Cargar datos iniciales

Cuando los contenedores ya esten arriba, cargar el seed de la base de datos:

```bash
docker exec -i db psql -U postgres -d fixya_db < FixYa/database/seed.sql
```

Si es la primera vez que levantas el proyecto, espera unos segundos despues de `docker compose up -d --build` antes de ejecutar el seed. El backend crea las tablas automaticamente al iniciar.

## Accesos

Frontend:

```txt
http://localhost:5173
```

Backend API:

```txt
http://localhost:8000
```

Swagger / documentacion API:

```txt
http://localhost:8000/docs
```

PostgreSQL:

```txt
Host: localhost
Port: 5432
Database: fixya_db
User: postgres
Password: postgres
```

## Comandos utiles

Ver logs de todos los servicios:

```bash
docker compose logs -f
```

Ver logs solo del backend:

```bash
docker compose logs -f backend
```

Ver logs solo del frontend:

```bash
docker compose logs -f frontend
```

Detener contenedores:

```bash
docker compose down
```

Reconstruir todo desde cero:

```bash
docker compose up -d --build
```

Resetear la base de datos y volver a cargar seed:

```bash
docker compose down -v
docker compose up -d --build
docker exec -i db psql -U postgres -d fixya_db < FixYa/database/seed.sql
```

> Importante: `docker compose down -v` elimina el volumen de PostgreSQL y borra los datos locales.

## Variables de entorno

Para ejecucion con Docker, `docker-compose.yml` ya define la conexion a PostgreSQL:

```txt
DATABASE_URL=postgresql://postgres:postgres@db:5432/fixya_db
```

El archivo `FixYa/.env.example` sirve como referencia si se quiere ejecutar el backend fuera de Docker.

## Solucion de problemas

Si Docker muestra errores de montaje en Windows, reinicia Docker Desktop y vuelve a ejecutar:

```bash
docker compose down
docker compose up -d --build
```

Si el frontend no refleja cambios recientes, reconstruye sin cache:

```bash
docker compose build --no-cache frontend
docker compose up -d frontend
```

Si el backend no responde, revisar logs:

```bash
docker compose logs -f backend
```

Si el seed falla porque ya existen datos, puedes usar el reinicio limpio de base de datos:

```bash
docker compose down -v
docker compose up -d --build
docker exec -i db psql -U postgres -d fixya_db < FixYa/database/seed.sql
```

## Flujo recomendado para ejecutar

```bash
git clone https://github.com/solangeCea/FixYa-Proyecto.git
cd FixYa-Proyecto
git clone https://github.com/vanneglezn/FixYa.git
git clone https://github.com/solangeCea/fixya-frontend.git
docker compose up -d --build
docker compose ps
docker exec -i db psql -U postgres -d fixya_db < FixYa/database/seed.sql
```

Luego abrir:

```txt
http://localhost:5173
```
