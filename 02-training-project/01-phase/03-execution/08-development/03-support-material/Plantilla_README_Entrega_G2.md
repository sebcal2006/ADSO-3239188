# ENTREGA-G2 · Guía 2: Planeación de la construcción y base de datos

> Los formatos de cada artefacto y un ejemplo completo están en **Plantillas_G2.md**; los mínimos y niveles, en **Rubricas_G2.md**.
>
> Copia este archivo como `ENTREGA-G2.md` dentro de la carpeta de **tu** servicio (`09-microservices/services/NN-<servicio>/`), en tu rama `g2/<servicio>-<usuario>`, y diligéncialo. Borra las instrucciones entre `>` cuando lo llenes. Un archivo de entrega ausente o incompleto limita la nota a 70 (Rubricas_G2.md, sección 1.6).

> No escribas tu nombre completo, tu número de documento, teléfonos ni correos, ni datos reales de terceros. Identifícate solo con tu usuario de GitHub.

## 1. Datos de la entrega

| Campo | Valor |
|---|---|
| Ficha | 3239188 |
| Repositorio del equipo | `code-sena/<equipo>-docs` |
| Servicio propio (número y nombre de la carpeta) | `NN-<servicio>` |
| Usuario de GitHub del autor (el mismo de los commits) | |
| Rama de entrega | `g2/<servicio>-<usuario>` |
| Rama de integración destino | `dev` / `main` (deja una) |
| Enlace a la solicitud de cambio (pull request) | |
| Motor de base de datos y versión | PostgreSQL 16 / MySQL 8 (deja uno) |

## 2. Tabla de propiedad

> Una fila por archivo o grupo de archivos de esta entrega. Si compartes el servicio con otro aprendiz (acordado con el instructor el 26 de noviembre), lista solo **tus** tablas y archivos, y escribe en «Observación» qué tablas son del otro usuario.

| Producto | Archivo o carpeta | Tablas u objetos que cubre | Usuario de GitHub del autor | Observación |
|---|---|---|---|---|
| P1 | `construction-plan.md` | | | |
| P1 | `coding-standard.md` | | | |
| P1 | `docker-compose.yml`, `.env.example` | | | |
| P2 | `db/migrations/V1__create_schema.sql` | | | |
| P2 | `db/migrations/V2__constraints_indexes.sql` | | | |
| P2 | `db/migrations/V3__security_roles.sql` | | | |
| P2 | `db/migrations/V4__seed.sql` | | | |
| P2 | `db/tests/pruebas.sql` | | | |
| P2 | `db/EVIDENCIA.md` | | | |
| P2 | `data-model.md` (sección «Schema migration») | | | |

## 3. Origen del insumo

| Pregunta | Respuesta |
|---|---|
| Ruta del modelo de datos de la guía 1 que usaste como insumo | `09-microservices/services/NN-<servicio>/data-model.md` |
| Otros documentos de diseño usados (contrato de API, `events.md`, README del servicio, `06-data/`) | |
| ¿Corregiste el modelo de datos al construir la base? ¿Qué y por qué? | |
| ¿Algún archivo de esta entrega lo hizo otra persona? | Sí / No (si es Sí, explica: los productos son individuales) |

## 4. Qué hice y qué decidí

**Producto 1 (RAP 593106), en 3 a 5 líneas:** decisión principal del plan, stack elegido y por qué, y la regla de tu estándar que más te costó definir.

**Producto 2 (RAP 593107), en 3 a 5 líneas:** qué restricción protege la regla de negocio más importante de tu servicio, qué puede y qué no puede hacer cada rol, y qué prueba lo demuestra.

## 5. Autoverificación de mínimos

> Marca con `x` solo lo que de verdad cumples. El instructor lo contrasta con los archivos y ejecuta tus migraciones.

**Producto 1:**
- [ ] C1 Interpretación: ≥ 8 elementos del diseño con su origen y su tarea
- [ ] C2 Plan: ≥ 10 tareas con ID, insumo, estimación, dependencia y criterio de terminado
- [ ] C3 Stack justificado con ≥ 3 condiciones y una alternativa descartada
- [ ] C4 `docker-compose.yml` con versión fijada y `healthcheck`, `.env.example` sin secretos, `.env` ignorado, pasos con salida esperada
- [ ] C5 Estrategia de ramas, ≥ 4 commits convencionales propios, solicitud de cambio con plantilla
- [ ] C6 Estándar de codificación con nombrado (código y base de datos), indentación, documentación y ejemplos

**Producto 2:**
- [ ] D1 V1: esquema y ≥ 4 tablas con PK, tipos, `NOT NULL` y auditoría en las tablas principales
- [ ] D2 V2: FK con `ON DELETE` (ninguna hacia otro servicio), ≥ 3 `CHECK`, ≥ 2 `UNIQUE`, ≥ 3 índices, ≥ 1 vista, ≥ 1 función o disparador
- [ ] D3 V3: ≥ 2 roles con mínimo privilegio, `GRANT` y `REVOKE`, sin contraseñas reales
- [ ] D4 V4: ≥ 5 filas por tabla principal, datos ficticios
- [ ] D5 Pruebas: ≥ 4 violaciones, ≥ 2 de permisos, transacción con `ROLLBACK` y con `COMMIT`
- [ ] D6 El servicio de base se llama `<servicio>-db`, monta `db/migrations` y `db/tests`, y probé `docker compose down -v` y `docker compose up -d`: V1 a V4 corren sin errores
- [ ] D7 `EVIDENCIA.md` con la salida real de la terminal
- [ ] D8 Sección «Schema migration» de `data-model.md` actualizada

## 6. Historial de commits

> Debes tener commits tuyos con cambios sustantivos en archivos de tu servicio en **al menos 2 días distintos** entre el jueves 26 de noviembre de 2026 y el domingo 6 de diciembre de 2026 a las 11:59 p. m. Anota los días y un mensaje de ejemplo de cada uno.

| Día | Mensaje del commit (formato `tipo(alcance): descripción`) |
|---|---|
| | |
| | |

## 7. Uso de inteligencia artificial (declaración obligatoria)

> Si no usaste IA, escribe «No usé IA». Si la usaste, di para qué, con qué herramienta y qué cambiaste después. Lo que no puedas explicar en la verificación oral cuenta como no propio.

| Herramienta | Para qué la usé | Qué verifiqué o cambié después |
|---|---|---|
| | | |

## 8. Declaración de autoría

Declaro que los archivos listados en la tabla de propiedad son de mi autoría, que los hice sobre el servicio que asumí en la guía 1, que no entregué como propio material del instructor, del marco de trabajo sin diligenciar ni de otros aprendices, que las migraciones se ejecutan desde cero como lo muestra mi evidencia y que puedo explicar cada archivo en la verificación oral.

Usuario de GitHub: ______________________  Fecha: ______________
