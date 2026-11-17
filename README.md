# PDDS Ciberseguridad — Ciclo de Desarrollo Seguro sobre OWASP Juice Shop

Repositorio del proyecto final de **Ciberseguridad**. Se toma [OWASP Juice Shop](https://owasp.org/www-project-juice-shop/)
como aplicación base y se le aplica un **ciclo de vida de desarrollo seguro (SSDLC)**: medición de madurez,
diseño seguro, modelo de amenazas, SAST/SCA/DAST automatizados, guardrails en el pipeline y un plan de pentest.

| Campo | Valor |
|---|---|
| Repositorio | `https://github.com/MasterJD/PDDS_Ciberseguridad-Ciclo-Desarrollo-Seguro` |
| Rama de trabajo | `main` |
| Entrega final | 02-dic-2026 |

## Estado de la base

Esta copia es un **fork depurado** de Juice Shop, preparado como línea base del proyecto:

- La aplicación funciona: backend (Express + TypeScript), frontend (Angular 22), SQLite/Sequelize y MarsDB.
- El **catálogo de retos está vacío** (`data/static/challenges.yml` → `[]`). El motor de retos, las rutas y la
  interfaz de *Score Board* se conservan para no romper la aplicación, pero no hay retos activos.
- Se retiró el material ajeno al proyecto: soluciones y referencias de retos, capturas, monitoreo, Vagrant,
  infraestructura intencionalmente insegura de los retos, RSN, parches de retos y artefactos FTP/CTF.
- El detalle de cada eliminación, decisión y deuda conocida está en [`context/entrega-general.md`](context/entrega-general.md).

> ⚠️ **Juice Shop es intencionalmente inseguro.** No lo despliegues en producción ni expongas la instancia a
> Internet. Cualquier IaC de los retos originales fue eliminada; el `Dockerfile` de la raíz es solo para uso local.

## Documentación del proyecto

| Documento | Contenido |
|---|---|
| [`context/entrega-general.md`](context/entrega-general.md) | Seguimiento de hitos, fases, decisiones, deuda y verificaciones |
| [`context/guia-implementacion-fases.md`](context/guia-implementacion-fases.md) | Guía técnica de las fases 0–2 (madurez, diseño y modelo de amenazas) |
| [`AGENTS.md`](AGENTS.md) | Convenciones del repositorio y reglas para asistentes de IA |

## Requisitos

- **Node.js 24 LTS** (o `^22.22.3`). El backend admite Node 22–26, pero Angular 22 rechaza versiones menores
  a `22.22.3` al compilar el frontend.
- npm 11 o superior.
- Docker (opcional, para ejecutar en contenedor).

## Instalación y ejecución local

```bash
npm install                 # instala backend y compila frontend + servidor (postinstall)
npm start                   # sirve la aplicación en http://localhost:3000
```

Si prefieres controlar cada paso (recomendado en Windows o en redes con proxy):

```bash
npm install --ignore-scripts
cd frontend && npm install --legacy-peer-deps && cd ..
npm run build               # frontend (ng build) + servidor (tsc)
npm start
```

El frontend se sirve desde `frontend/dist/frontend`, por lo que **debes compilarlo antes de arrancar** el
servidor; de lo contrario el arranque falla en la verificación de precondiciones.

Para desarrollo con recarga en caliente:

```bash
npm run serve               # backend con tsx + frontend con ng serve
```

Con Docker:

```bash
docker build -t juice-shop-ssdlc .
docker run --rm -p 3000:3000 juice-shop-ssdlc
```

## Pruebas y calidad

```bash
npm run test:server         # pruebas unitarias del backend
npm run test:api            # pruebas de integración de la API
npm run test:frontend       # pruebas unitarias del frontend (Vitest)
npm start & npm run test:e2e  # pruebas E2E (Cypress)
npm run lint                # ESLint + Stylelint
```

Algunas pruebas E2E y de API asumen retos concretos y fallarán mientras el catálogo esté vacío; están
registradas como deuda conocida en `context/entrega-general.md`.

## Estructura del repositorio

```
app.ts, server.ts      Punto de entrada y configuración de Express
routes/                Endpoints de la API
lib/                   Utilidades (seguridad, validación, logger)
models/                Modelos Sequelize (SQLite)
data/                  Creación de datos y catálogos estáticos
frontend/              Aplicación Angular
config/                Configuración por entorno (YAML)
test/                  Pruebas unitarias y de integración
cypress/               Pruebas E2E
context/               Documentación del proyecto
threat-model.json      Modelo Threat Dragon base (Fase 2)
```

## Atribución y licencia

Proyecto derivado de **OWASP Juice Shop**, © Bjoern Kimminich & the OWASP Juice Shop contributors,
distribuido bajo licencia [MIT](LICENSE). El código original conserva sus avisos de copyright y su licencia.
