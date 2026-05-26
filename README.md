# Sistema de Gestión de Horarios (SIGH)

Sistema web para la generación y gestión automática de horarios hospitalarios con cobertura 24h, manejo de recargos, novedades y optimización mediante inteligencia artificial.

## Arquitectura

```
├── frontend/        # React 18 + TypeScript + Vite + Tailwind CSS
├── backend/         # Node.js + Express + TypeScript + Prisma (PostgreSQL embebido)
├── ia-service/      # Python – solver de optimización (CP-SAT)
└── docker-compose.yml
```

### Servicios

| Servicio     | Tecnología                          | Puerto |
|--------------|-------------------------------------|--------|
| Frontend     | React 18, Vite, Tailwind, Shadcn/UI | 80     |
| Backend      | Express, TypeScript, Prisma         | 5000   |
| IA Service   | Python, CP-SAT                      | 8000   |
| Fuseki       | Apache Jena (SPARQL/RDF)            | 3030   |

## Funcionalidades

- Generación automática de programaciones mensuales con cobertura 24h
- Optimización de horarios por área mediante solver CP-SAT (aprox. 73s para 30 días)
- Gestión de 15 áreas hospitalarias (1 área por empleado)
- Módulo de recargos con cálculo automático
- Gestión de novedades (ausencias, permisos, incapacidades)
- Dark mode
- Exportación a Excel
- Autenticación JWT

## Requisitos

- [Docker](https://www.docker.com/) y Docker Compose
- Node.js 18+ (solo para desarrollo local)
- Python 3.10+ (solo para desarrollo local del ia-service)

## Instalación con Docker

```bash
# Clonar el repositorio
git clone https://github.com/Erickcod/GeneradorHorarios.git
cd GeneradorHorarios

# Levantar todos los servicios
docker-compose up -d
```

Accede a la app en `http://localhost`

## Desarrollo local

### Backend

```bash
cd backend
npm install
npm run dev
```

### Frontend

```bash
cd frontend
npm install
npm run dev
```

Disponible en `http://localhost:5173`

### IA Service

```bash
cd ia-service
pip install -r requirements.txt
python main.py
```

## Variables de entorno

Crea un archivo `.env` en `backend/`:

```env
JWT_SECRET=tu_secreto_jwt
IA_SERVICE_URL=http://localhost:8000
FUSEKI_ENDPOINT=http://localhost:3030/nomina
FUSEKI_QUERY=http://localhost:3030/nomina/query
FUSEKI_UPDATE=http://localhost:3030/nomina/update
FUSEKI_DATA=http://localhost:3030/nomina/data
```

Crea un archivo `.env` en `frontend/`:

```env
VITE_API_URL=http://localhost:5000/api
```

## Stack tecnológico

**Frontend:** React 18, TypeScript, Vite, Tailwind CSS, Shadcn/UI, React Query, Zustand, React Router, Recharts, Axios

**Backend:** Node.js, Express, TypeScript, Prisma ORM, PostgreSQL, JWT, bcrypt, Helmet

**IA Service:** Python, CP-SAT (OR-Tools), HTTP Server nativo

**Infraestructura:** Docker, Docker Compose, Nginx, Apache Jena Fuseki
