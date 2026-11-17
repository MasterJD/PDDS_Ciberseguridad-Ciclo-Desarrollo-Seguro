# ENTREGA — Seguimiento del proyecto final SSDLC (OWASP Juice Shop)

> **Documento de seguimiento del equipo.** Se actualiza al cerrar cada fase. Es el único documento de
> seguimiento versionado; todo lo que se entrega vive en `deliveries/`.
>
> **Guía técnica interna:** `context/guia-implementacion-fases.md` (no se versiona; ver §12).
>
> **Última actualización:** 17-nov-2026
> **Estado global:** base limpia preparada · Fases 0–2 en preparación · Fases 3–8 no iniciadas

---

## 1. Identificación

| Campo | Valor |
|---|---|
| Asignatura | Ciberseguridad — Diseño y proceso de seguridad en el desarrollo de una aplicación |
| Proyecto | Proyecto final (20 puntos) |
| Aplicación | OWASP Juice Shop (Node.js, TypeScript, Angular) |
| Repositorio | `https://github.com/MasterJD/PDDS_Ciberseguridad-Ciclo-Desarrollo-Seguro` |
| Rama base | `main` |
| Integrantes | _(completar: nombre y correo)_ |
| Docente | _(completar)_ |
| Fecha de avance | 18-nov-2026 |
| Fecha de entrega y defensa | 02-dic-2026 |

---

## 2. Resumen ejecutivo del estado

La base del repositorio quedó preparada como fork “limpio” de Juice Shop:

- Se conservó la aplicación funcional y su cadena de build (`frontend/`, `routes/`, `lib/`, `models/`, `data/`, `config/`, `Dockerfile`).
- Se retiró el material ajeno al proyecto: solución de retos, referencias, capturas, monitoreo, Vagrant, IaC intencionalmente insegura, RSN, parches de retos, artefactos FTP/CTF y documentación de la comunidad upstream.
- El catálogo de retos quedó vacío (`data/static/challenges.yml` → `[]`), manteniendo el motor y la UI para no romper la aplicación.
- Se añadieron exclusiones locales a `.gitignore` para secretos, reportes de herramientas y volúmenes de Dependency-Track/DefectDojo.
- El `README.md` se reescribió para el proyecto y el seguimiento oficial vive en `deliveries/ENTREGA.md`.
- El backend compila sin errores (`tsc --noEmit`) y el frontend compila en modo producción.
- La aplicación arranca y responde en `http://localhost:3000` (SPA, `/api/Challenges`, `/rest/admin/application-version`).

**Pendiente inmediato:** cerrar Fases 0–2 (madurez, diseño y amenazas) y preparar el avance del 18-nov.

---

## 3. Hitos y cumplimiento

| Hito | Fecha | Qué se entrega | Estado |
|---|---|---|---|
| Elección de aplicación | 11-nov-2026 | Equipo, aplicación y fork | ✅ Cumplido |
| Avance | 18-nov-2026 | Madurez inicial, diseño y pipeline con SAST y SCA | 🔄 En curso |
| Entrega final | 02-dic-2026 | Repositorio completo + documento técnico PDF (15–25 p.) | ⬜ No iniciado |

---

## 4. Seguimiento por fase

Leyenda: ⬜ No iniciada · 🔄 En curso · ✅ Completada · ⚠️ Con observaciones

| Fase | Entregable | Artefactos | Estado | Evidencia / enlace | Responsable | Fecha |
|---|---|---|---|---|---|---|
| 0 · Madurez inicial | Tabla SAMM actual vs objetivo | `security/madurez/samm-inicial.md` | 🔄 En preparación | — | — | — |
| 1 · Diseño | Arquitectura, DFD, clasificación y ASVS | `security/diseno/` | 🔄 En preparación | — | — | — |
| 2 · Amenazas | Modelo Threat Dragon + tabla + trazabilidad | `security/threat-model/` | 🔄 En preparación | — | — | — |
| 3 · SAST y secretos | Configuración + 5 hallazgos analizados | `.semgrep/`, workflow | ⬜ No iniciada | — | — | — |
| 4 · SCA y SBOM | SBOM, Dependency-Track, priorización, VEX | `security/sbom/`, `security/vex/` | ⬜ No iniciada | — | — | — |
| 5 · IaC | Dockerfile endurecido + IaC + reportes | `infra/` | ⬜ No iniciada | — | — | — |
| 6 · DAST | Reportes ZAP + 5 hallazgos analizados | `.zap/` | ⬜ No iniciada | — | — | — |
| 7 · Guardrails | Política, DefectDojo, 5 PR de corrección | `.github/`, `security/politica-de-bloqueo.md` | ⬜ No iniciada | — | — | — |
| 8 · Pentest y madurez | Plan + comparación antes/después | `security/pentest-plan.md`, `samm-final.md` | ⬜ No iniciada | — | — | — |

---

## 5. Bitácora de cambios del repositorio

### 5.1 Limpieza de la base (17-nov-2026)

| # | Elemento | Acción | Justificación |
|---|---|---|---|
| 1 | `SOLUTIONS.md`, `REFERENCES.md`, `HALL_OF_FAME.md` | Eliminados | Documentación de la comunidad upstream |
| 2 | `CONTRIBUTING.md`, `CODE_OF_CONDUCT.md`, `crowdin.yaml`, `.codeclimate.yml`, `.mailmap` | Eliminados | Procesos/integraciones de upstream |
| 3 | `screenshots/` | Eliminado | Capturas del README original |
| 4 | `monitoring/` | Eliminado | Dashboard Grafana de la demo |
| 5 | `vagrant/` | Eliminado | Aprovisionamiento no usado (proyecto en contenedores) |
| 6 | `infrastructure/`, `terraform/` | Eliminados | IaC intencionalmente insegura de los retos; se reemplazará por `infra/` |
| 7 | `rsn/` | Eliminado | Herramienta exclusiva de los retos de Juice Shop |
| 8 | `data/static/codefixes/` | Eliminado | Parches de retos con código vulnerable deliberado |
| 9 | `data/static/web3-snippets/` | Eliminado | Fragmentos de retos Web3 |
| 10 | `data/static/challenges.yml` | Vaciado a `[]` | Sin catálogo de retos; motor y UI intactos |
| 11 | `ftp/*` y `ftp/quarantine/*` | Eliminados (se conservan `.gitkeep`) | Archivos “filtrados” a propósito para retos |
| 12 | `encryptionkeys/premium.key` | Eliminada | Artefacto del reto de paywall |
| 13 | `ctf.key` | Eliminada | Clave del modo CTF |
| 14 | `app.json` | Eliminado | Descriptor de Heroku |
| 15 | `test/server/rsn.unit.test.ts` | Eliminado | Probaba una herramienta retirada (rompía la compilación) |
| 16 | `test/server/codingChallengeFixes.unit.test.ts` | Eliminado | Validaba parches de retos retirados |
| 17 | `server.ts` | Ajustado | Se retiró la ruta `/infrastructure` y su import |
| 18 | `data/datacreator.ts` | Ajustado | Guarda para arrancar sin `changeProductChallenge` |
| 19 | `lib/codingChallenges.ts` | Ajustado | Se quitaron rutas de snippets eliminadas |
| 20 | `package.json`, `eslint.config.mjs`, `tsconfig.json`, `.dockerignore`, `scripts/package.mjs` | Ajustados | Referencias a `rsn`, `vagrant`, `codefixes`, `ctf.key`, `infrastructure` |
| 21 | `.gitignore` | Ampliado | `.env`, reportes SARIF/ZAP, SBOM raíz, volúmenes de herramientas |
| 22 | `.well-known/csaf/{2017,2021,2024}`, `changes.csv`, `index.txt` | No restaurados | Archivo histórico de avisos CSAF de upstream; no es parte de la aplicación |
| 23 | `.well-known/security.txt`, `.well-known/csaf/provider-metadata.json` | Restaurados desde upstream | `data/datacreator.ts` los lee al arrancar; sin ellos la app no inicia |
| 24 | `README.md` | Reemplazado | El original era material de marketing de upstream; ahora describe el proyecto, su estado y cómo ejecutarlo |
| 25 | `frontend/src/assets/private/*.js` | Des-ignorados en `.gitignore` | Los carga `routes/easterEgg.ts`; con la regla anterior un clon limpio quedaría incompleto |
| 26 | `context/` | Excluido del repositorio | Contiene material del enunciado y notas de trabajo internas; no forma parte de la entrega |
| 27 | `context/entrega-general.md` | Movido a `deliveries/ENTREGA.md` | Los entregables se agrupan en `deliveries/` y el documento pasa a llamarse `ENTREGA.md` |

**Conservado a propósito:** `encryptionkeys/jwt.pub` (se lee al cargar `lib/insecurity.ts`; sin ella la app no
arranca), `threat-model.json` (modelo Threat Dragon base, sin amenazas, útil para la Fase 2), `swagger.yml`
(insumo para ZAP API scan), pruebas y Cypress (red de seguridad; ver deuda conocida).

> **Nota sobre el primer commit.** La rama no tiene commits previos, así que el commit inicial registra los
> 1193 archivos de la aplicación (23.7 MB) y **no muestra eliminaciones**: las rutas retiradas simplemente ya no
> existen. El conteo corresponde a código propio de Juice Shop (`frontend/src` 803, `test/` 160, `routes/` 63,
> `data/static` 53, `models/` y `lib/` 49, `config/` 14), más `deliveries/ENTREGA.md`; queda fuera `context/`
> junto con `node_modules/`, `build/`, `frontend/dist/` y los artefactos de herramientas.

### 5.2 Cambios funcionales

| Fecha | Cambio | Archivo(s) | Motivo | Verificación |
|---|---|---|---|---|
| 17-nov | Catálogo de retos vacío | `data/static/challenges.yml` | Base limpia sin retos | `/api/Challenges` responde `[]` con la app arriba |
| 17-nov | Guarda para producto sin reto | `data/datacreator.ts` | Evitar `TypeError` al no existir `changeProductChallenge` | `tsc` OK; arranque OK |
| 17-nov | Eliminación de ruta `/infrastructure` | `server.ts` | El directorio ya no existe | `tsc` OK; arranque OK |
| 17-nov | Restauración de `.well-known` mínimo | `.well-known/` | Requerido por `prepareFilesystem()` al arrancar | Arranque OK |

---

## 6. Decisiones registradas

| ID | Decisión | Alternativas consideradas | Motivo |
|---|---|---|---|
| D-01 | Limpieza conservadora: mantener motor de retos y UI | Borrar todo el subsistema de retos | El motor está entrelazado en ~52 archivos; borrarlo rompe la app y consume tiempo del proyecto |
| D-02 | Vaciar el catálogo de retos, no el código | Dejar retos activos | Evita ruido de retos/soluciones en el repositorio y en los escaneos |
| D-03 | Conservar pruebas y Cypress | Eliminar pruebas de retos | Sirven de red de seguridad; las que dependen de retos se documentan como deuda |
| D-04 | No editar i18n de retos | Quitar cadenas de 44 archivos | Son inertes; el riesgo de edición supera el beneficio |
| D-05 | Usar `security/diseno/` (sin ñ) | `security/diseño/` | Compatibilidad de rutas en CI, URLs y herramientas |
| D-06 | Mantener `threat-model.json` en la raíz por ahora | Moverlo a `security/threat-model/` | Se importará en Threat Dragon durante la Fase 2 y se versionará allí |
| D-07 | No implementar fases 3–8 en esta iteración | Adelantar pipeline | Instrucción del equipo: primero base limpia y Fases 0–2 |
| D-08 | Restaurar solo el `.well-known` mínimo y descartar el archivo CSAF histórico | Restaurar `.well-known` completo / parchear `datacreator.ts` | El archivo histórico son avisos de vulnerabilidades de upstream (ruido); parchear código propio por un archivo faltante crea deuda evitable |
| D-09 | Reescribir `README.md` para el proyecto | Conservar el README de upstream | El repositorio debe explicar qué se entrega y cómo se ejecuta; el texto original no aporta al curso |
| D-10 | No versionar `context/`; los entregables viven en `deliveries/` | Versionar toda la carpeta `context/` | El material del enunciado no es de nuestra autoría y las notas de trabajo no aportan a la entrega; `deliveries/` concentra lo que sí se evalúa |
| D-11 | Renombrar el seguimiento a `deliveries/ENTREGA.md` | Mantener `entrega-general.md` | Un nombre único, en mayúsculas y visible en la raíz de `deliveries/` |

---

## 7. Deuda conocida y riesgos

| ID | Deuda / riesgo | Impacto | Plan |
|---|---|---|---|
| R-01 | Pruebas de API/E2E que asumen retos concretos fallarán | Medio | Excluirlas de los gates o adaptarlas; registrar en el informe |
| R-02 | `package-lock.json` está ignorado (y `.npmrc` define `package-lock=false`) | Alto (SCA) | Decidir en la Fase 4: quitarlo de `.npmrc`/`.gitignore` para tener `npm ci` reproducible y SCA sobre versiones exactas |
| R-03 | Clave privada RSA embebida en `lib/insecurity.ts` | Crítico | Documentar como amenaza T-02; no reutilizar; rotar en Fase 7 si aplica |
| R-04 | `data/static/i18n/` conserva textos de retos | Bajo | Inertes; se documenta la decisión |
| R-05 | `frontend` requiere `--legacy-peer-deps` y Node ≥ 22.22.3 (Angular 22) | Bajo | Fijar Node 24 LTS en CI; revisar el conflicto de peers al versionar el lockfile |
| R-06 | El catálogo vacío puede confundir al evaluador | Bajo | Explicarlo en README y en este documento |
| R-07 | Falta de tiempo para las 8 fases | Alto | Priorizar Fases 0–2 y pipeline mínimo; plantillas ya listas |
| R-08 | `i18n/*.json` (traducciones del backend) no se versionan, por regla de upstream | Bajo | `routes/languages.ts` degrada con una advertencia y usa la traducción del frontend; se recuperan desde Crowdin si se necesita multilenguaje |
| R-09 | `routes/privacyPolicyProof.ts` sirve `thank-you.jpg`, que no existe en el repositorio | Bajo | Responde con error si se invoca; retirar la ruta o añadir el recurso si algún día se reactiva el reto asociado |

---

## 8. Verificación técnica realizada

| Verificación | Comando | Resultado | Fecha |
|---|---|---|---|
| Instalación backend | `npm install --ignore-scripts` | ✅ 1249 paquetes | 17-nov |
| Compilación TypeScript | `npx tsc --noEmit -p tsconfig.json` | ✅ Sin errores | 17-nov |
| Compilación backend | `npm run build:server` | ✅ `build/` generado | 17-nov |
| Instalación frontend | `npm install --legacy-peer-deps` (en `frontend/`) | ✅ 829 paquetes (solo avisos `EBADENGINE` por Node 22.14) | 17-nov |
| Compilación frontend | `npm run build` (en `frontend/`, Node 24.22.3) | ✅ `frontend/dist/frontend/` + `dist/bom/bom.json` | 17-nov |
| Arranque completo | `node build/app` | ✅ `Server listening on port 3000` (≈24 s) | 17-nov |
| SPA servida | `GET http://localhost:3000/` | ✅ 200 (HTML de Angular) | 17-nov |
| API de retos | `GET /api/Challenges` | ✅ 200 con `data: []` | 17-nov |
| Versión de aplicación | `GET /rest/admin/application-version` | ✅ 200 | 17-nov |
| Archivos a versionar | `git add -A -n` | ✅ 1193 archivos; sin `context/`, `node_modules/`, `build/`, `frontend/dist/` ni artefactos | 17-nov |

> **Requisito de entorno:** Angular 22 exige Node `^22.22.3 || ^24.15.0 || >=26.0.0`. Con Node 22.14 el
> `ng build` se detiene por comprobación de versión; en la verificación se usó Node 24.22.3. El backend
> funciona con Node 22.14 y con 24.x (los módulos nativos se instalan según la versión usada).
>
> **Avisos esperados al arrancar:** faltan `ALCHEMY_API_KEY` y un endpoint LLM en `localhost:11434`; solo
> afectan a retos Web3/chatbot, que están desactivados porque el catálogo está vacío.

---

## 9. Declaración de uso de IA

El enunciado permite asistentes de IA si se declaran y el equipo puede defender lo entregado.

| Herramienta | Uso | Archivos afectados | Revisado por el equipo |
|---|---|---|---|
| Asistente de IA (OpenCode) | Análisis del PDF, limpieza del repositorio, redacción de la guía interna y de `ENTREGA.md` | `deliveries/ENTREGA.md`, `README.md`, limpieza de base | ⬜ Pendiente de revisión |
| — | — | — | — |

> Completar con cualquier otra herramienta usada (Copilot, ChatGPT, etc.). El equipo debe poder explicar
> cada diagrama, requisito y amenaza sin depender del asistente.

---

## 10. Próximos pasos inmediatos

1. ~~Confirmar que la aplicación arranca con frontend compilado~~ ✅ Verificado (ver §8).
2. Completar `security/madurez/samm-inicial.md` con evidencia (capturas de Branch protection y Actions).
3. Crear `security/diseno/` con los cuatro documentos de la Fase 1.
4. Importar `threat-model.json` en Threat Dragon, añadir las 16 amenazas y exportar el modelo.
5. Escribir la matriz de trazabilidad y el borrador de política de excepciones.
6. Preparar el PDF del avance en `deliveries/avance-2026-11-18.pdf` (portada, resumen, Fases 0–2).
7. Recién después, iniciar Fase 3 (secretos + SAST) y Fase 4 (SBOM + SCA).

---

## 11. Correspondencia con la rúbrica

| Criterio | Puntos | Dónde se evidencia | Estado |
|---|---:|---|---|
| Diseño y requisitos | 3 | `security/diseno/` (Fase 1) | 🔄 |
| Modelo de amenazas | 3 | `security/threat-model/` (Fase 2) | 🔄 |
| Pipeline | 6 | `.github/workflows/devsecops.yml` (Fases 3–6) | ⬜ |
| Guardrails y política | 2 | `security/politica-de-bloqueo.md` (Fase 7) | ⬜ |
| Remediación y gestión | 2 | PR de corrección + DefectDojo + VEX (Fase 7) | ⬜ |
| Plan de pentest y madurez | 2 | `security/pentest-plan.md` + `samm-final.md` (Fase 8) | ⬜ |
| Defensa oral | 2 | Demo y explicación | ⬜ |

---

## 12. Entregables (`deliveries/`)

Todo lo que se entrega al docente se versiona en `deliveries/`. La carpeta `context/` (material del enunciado
y notas de trabajo) queda excluida del repositorio mediante `.gitignore`.

| Archivo | Contenido | Estado |
|---|---|---|
| `ENTREGA.md` | Este documento: hitos, fases, decisiones, deuda y verificaciones | ✅ |
| `avance-2026-11-18.pdf` | Informe de avance: madurez inicial, diseño y pipeline con SAST + SCA | ⬜ |
| `entrega-final-2026-12-02.pdf` | Documento técnico final (15–25 p.) | ⬜ |

Convención de nombres: `<tipo>-<fecha>.pdf` en minúsculas y sin tildes, para que el archivo se pueda citar
desde el informe sin problemas de codificación.

---

*Actualizar este documento al cerrar cada fase, con fecha, evidencia y responsable.*
