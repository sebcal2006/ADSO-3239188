# Rúbricas y condiciones de evaluación · Guía 2: Planeación de la construcción y base de datos (v2)

**Ficha 3239188 · Análisis y Desarrollo de Software (228118) · Proyecto formativo 3271213 · Fase Ejecución**  
**Competencia 220501096 (Construcción del software).** RAP de la guía: **593106** (01) Planear actividades de construcción del software de acuerdo con el diseño establecido · **593107** (02) Construir la base de datos para el software a partir del modelo de datos. Los demás RAP de la competencia no se desarrollan en esta guía.

| RAP | Actividad del proyecto formativo | Carpeta de la actividad en el repositorio de la ficha |
|---|---|---|
| 593106 | Codificar los módulos del software, con base en los estándares del mercado | `03-execution/08-development` |
| 593107 | Desarrollar la estructura de datos y la interfaz de usuario del software | `03-execution/09-database-ui` |

Este documento es público: lo puedes leer desde el primer día. Los criterios de evaluación están tomados **literalmente** del programa de formación; los niveles están redactados para que se puedan comprobar con el archivo en la mano o ejecutando tus scripts.

---

## 1. Reglas generales

### 1.1 Las cuatro evidencias y a qué RAP pertenece cada una

| # | Evidencia | RAP | Peso en la guía | Fecha | Forma |
|---|---|---|---|---|---|
| 1 | Prueba de conocimiento | 593106 (10 preguntas) y 593107 (10 preguntas) | 25 % | Jueves 3 de diciembre de 2026 | Presencial, individual, 40 min, cuestionario de 20 preguntas en la plataforma Moodle (Zajuna), con calificación automática |
| 2 | Producto 1: plan de construcción del servicio | **593106** | 25 % | Hasta el domingo 6 de diciembre de 2026, 11:59 p. m. | Rama `g2/<servicio>-<usuario>` con solicitud de cambio (pull request) en el repositorio del equipo |
| 3 | Producto 2: base de datos construida | **593107** | 25 % | Hasta el domingo 6 de diciembre de 2026, 11:59 p. m. | La misma rama y la misma solicitud de cambio |
| 4 | Prueba de desempeño | **593107** | 25 % | Jueves 3 de diciembre de 2026 | Presencial, individual, en computador, 90 min, con PostgreSQL en contenedor; los archivos se entregan en una tarea de Moodle |

### 1.2 Cómo se aprueba cada RAP (regla de aprobación por resultado)

Cada RAP se juzga **por separado**, con sus propias evidencias. Puedes aprobar uno y quedar pendiente en el otro.

**Subpuntaje de conocimiento por RAP.** De las 20 preguntas, 10 son del RAP 593106 y 10 del RAP 593107. Para cada RAP: `conocimiento RAP = aciertos en sus 10 preguntas × 10` (de 0 a 100).

**Nota de cada RAP** (las evidencias conservan su peso de 25 %, y la prueba de conocimiento aporta la mitad de su peso a cada RAP):

- **RAP 593106** = (conocimiento 593106 + 2 × Producto 1) / 3
- **RAP 593107** = (conocimiento 593107 + 2 × Producto 2 + 2 × Prueba de desempeño) / 5

**Condiciones de aprobación:**

| RAP | Se aprueba si se cumplen todas |
|---|---|
| 593106 | (a) Nota RAP 593106 ≥ 70 · (b) Producto 1 ≥ 70 |
| 593107 | (a) Nota RAP 593107 ≥ 70 · (b) Producto 2 ≥ 70 · (c) tus migraciones se ejecutan **sin errores desde cero en un contenedor limpio** cuando el instructor las reproduce (sección 3.3) |

La condición (c) es una **compuerta**: la documentación sola no demuestra que la base de datos esté construida. Sin migraciones que se ejecuten, el RAP 593107 no se aprueba, sea cual sea el promedio.

**Ejemplo.** Conocimiento: 8 aciertos de 593106 (80) y 5 de 593107 (50). Producto 1 = 85, Producto 2 = 76, desempeño = 70. RAP 593106 = (80 + 170) / 3 = 83,3 → aprobado. RAP 593107 = (50 + 152 + 140) / 5 = 68,4 → no llega a 70: queda por evaluar con plan de mejoramiento.

**Nota de la guía (informativa, libro de calificaciones de Moodle)** = promedio de las cuatro evidencias. El juicio que se registra es el de cada RAP, no el promedio de la guía.

**Si un RAP no cumple**, el resultado **no se registra como «No aprobado»** en la plataforma de gestión académica: queda por evaluar y se acuerda un plan de mejoramiento con fecha. El instructor lo comunica por la plataforma de formación.

Aclaraciones de diseño de la evaluación:

- **La escala por saltos (100, 70, 40, 0) es deliberada**: se califica con el archivo en la mano y sin valores intermedios discutibles. Un producto con todos los criterios en nivel 70 obtiene 70, el mínimo exigido; cualquier tope por debajo de 70 (secciones 1.5 y 1.6) hace que ese producto, y por tanto su RAP, no se apruebe.
- **Relación con la guía 1.** El modelo de datos del servicio se califica en la guía 1 (RAP 593101). Aquí no se califica el modelo, sino lo que haces con él: planear su construcción (P1) y construirlo en el motor (P2). Si al construir corriges el modelo, actualiza `data-model.md` y decláralo en el archivo de entrega.

### 1.3 Cómo se calcula un producto

Cada rúbrica tiene criterios ponderados que suman 100. En cada criterio se ubica el trabajo en uno de cuatro niveles: **100**, **70**, **40** o **0**. La nota del producto es la suma de `peso × nivel / 100`. Después se aplican los topes de las secciones 1.5 y 1.6, si corresponden.

**Regla de resolución cuando el trabajo cumple solo una parte de un nivel:**

1. El nivel 100 exige **todas** las condiciones de su celda. Si no las cumples todas, bajas a 70.
2. En los niveles 70 y 40, las condiciones unidas por «o» son **defectos que ubican el trabajo en ese nivel**: basta uno de ellos.
3. Si tienes defectos de dos niveles distintos, **rige el nivel más bajo**. Si el trabajo no cumple ni una condición del 40, es 0.
4. Los porcentajes se cuentan sobre lo que **debía** existir (por ejemplo, sobre todas las tablas de tu modelo de datos).

### 1.4 Dónde y cómo se entrega

Trabajas en el **repositorio de tu equipo** (`code-sena/<equipo>-docs`), sobre el **servicio propio** que asumiste en la guía 1:

1. Desde la rama de integración del equipo (`dev` si existe; si no, `main`) creas tu rama individual: `g2/<servicio>-<usuario>` (por ejemplo, `g2/reservas-usuario123`).
2. Trabajas solo en la carpeta de tu servicio: `09-microservices/services/NN-<servicio>/`.
3. Antes del corte abres una **solicitud de cambio (pull request)** de tu rama hacia la rama de integración. No es necesario que se fusione antes del corte.
4. En la carpeta del servicio va el archivo `ENTREGA-G2.md`, hecho con **Plantilla_README_Entrega_G2.md**.

```
09-microservices/services/NN-<servicio>/
├── ENTREGA-G2.md            ← archivo de entrega (tabla de propiedad, autoría, IA)
├── construction-plan.md     ← P1: C1, C2, C3, C5
├── coding-standard.md       ← P1: C6
├── docker-compose.yml       ← P1: C4 (configuración) y P2: D6 (ejecución desde cero)
├── .env.example             ← P1: C4 (sin secretos)
├── data-model.md            ← de la guía 1; en P2 actualizas «Schema migration»
└── db/
    ├── migrations/
    │   ├── V1__create_schema.sql
    │   ├── V2__constraints_indexes.sql
    │   ├── V3__security_roles.sql
    │   └── V4__seed.sql
    ├── tests/
    │   └── pruebas.sql
    └── EVIDENCIA.md
```

Cuando esta guía difiera del marco de trabajo del repositorio (que propone ramas `feat/*`, carpeta `src/migrations/` y nombres `V001__`), **prevalece esta guía**: rama `g2/<servicio>-<usuario>`, carpeta `db/migrations/` y nombres `V1__` a `V4__`.

**Corte:** domingo 6 de diciembre de 2026 a las 11:59 p. m. (hora de Colombia). El instructor toma una **copia de tu rama a esa hora** y evalúa lo que contenga. Lo que se suba después, o por otro medio (correo, mensajería, USB), no se evalúa. No reescribas el historial (sin `git push --force` sobre tu rama de entrega).

**Si tu servicio quedó con un motor no relacional** en la guía 1 (por ejemplo, solo Redis o MongoDB), avísalo el jueves 26 de noviembre: con el instructor se elige la parte relacional que construirás o un servicio del equipo con datos relacionales. **Si dos aprendices tienen el mismo servicio**, avísenlo ese mismo día: se reparten las tablas y cada uno declara las suyas en la tabla de propiedad.

### 1.5 Requisitos mínimos de aceptación (RMA) y tope de 60

Cada producto tiene una lista de **artefactos obligatorios** con una cantidad mínima (secciones 2 y 3). **Si falta un artefacto obligatorio, el producto tiene un tope de 60 puntos.** Un artefacto cuenta como entregado solo si es tuyo, corresponde a tu servicio y se puede abrir o ejecutar. Quedarse corto en la cantidad mínima de un artefacto que sí entregaste **no activa el tope**: se refleja en el nivel del criterio.

Además, en el Producto 2: **si las migraciones no se ejecutan desde cero sin errores** en la reproducción del instructor, el producto tiene **tope 40** y el RAP 593107 queda por evaluar (sección 1.2, condición c).

### 1.6 Control de autoría (individual y verificable)

El insumo (el diseño del servicio) viene de la guía 1; **los dos productos son individuales**. Se verifican así:

| Control | Qué se revisa | Si no se cumple |
|---|---|---|
| Historial de commits | Commits hechos con **tu cuenta de GitHub** (autor del commit) en al menos **2 días distintos** entre el jueves 26 de noviembre de 2026 y el domingo 6 de diciembre de 2026 a las 11:59 p. m., con mensajes en formato de commits convencionales. El día se verifica con la fecha en que se **publicó** (push) en GitHub. Cada día debe traer **cambios sustantivos** en archivos de tu servicio (no cuentan espacios, saltos de línea ni renombrados sin contenido). Solo cuentan los commits sobre los archivos de **tu** servicio | 1 solo día: tope 70 · ningún día con cambios sustantivos propios: tope 60 |
| Solicitud de cambio | Pull request de `g2/<servicio>-<usuario>` hacia `dev` (o `main`) abierta antes del corte, con la plantilla del equipo | Rama sin solicitud de cambio: tope 70 · sin rama: no entregado |
| Archivo de entrega | `ENTREGA-G2.md` completo: tabla de propiedad (servicio, archivos, usuario de GitHub), origen del insumo, qué se hizo, uso de IA declarado y declaración de autoría | Ausente o incompleto: tope 70 |
| Verificación oral de autoría (fecha posterior a la entrega que el instructor comunica por la plataforma de formación) | **Una pregunta por producto** sobre **tus** archivos, con tu entrega abierta: por qué una tarea va antes que otra, qué hace una regla de tu estándar, qué impide una restricción, por qué un rol no tiene cierto permiso, qué pasa si se ejecuta de nuevo una migración. Apruebas si **explicas con tus palabras** qué hiciste y por qué. Si hay duda, se hace una tercera pregunta sobre ese producto | Si no sabes explicar **tu propio** producto: ese producto queda con **tope 50**. Puedes pedir una segunda oportunidad el mismo día |
| Contenido idéntico a otro aprendiz | Scripts, planes o estándares iguales o casi iguales entre aprendices (mismo texto, mismos nombres, mismos errores) **sin declararlo** | Tope 40 en el producto de cada uno, **después de una aclaración con derecho a réplica** (el instructor te muestra la coincidencia y puedes explicar tu proceso con tu historial) |
| Material ajeno como propio | El ejemplo «reservas» de Plantillas_G2 con otros nombres, las plantillas del marco de trabajo sin diligenciar (`_template/`, `models.md` de ejemplo) o el trabajo de otro integrante | Ese artefacto se cuenta como **no entregado** (activa el tope 60) |
| Commits masivos | Un commit que agrega decenas de archivos que no son tuyos (por ejemplo, el marco de trabajo completo o la carpeta de otro servicio) | No cuenta como aporte propio; se revisa el resto del historial |

Si se aplican varios topes, **rige el más bajo** (no se suman). El uso de IA está permitido **solo si lo declaras** en `ENTREGA-G2.md` (para qué la usaste y qué cambiaste después); lo que no puedas explicar en la verificación oral cuenta como no propio.

### 1.7 Presupuesto de tiempo (cada producto está dimensionado para unas 3 horas)

El presupuesto supone que tu modelo de datos de la guía 1 está terminado. Si no lo está, termínalo primero: sin él no hay insumo. La guía 1 vence el mismo 6 de diciembre: planifica las dos.

| Producto 1 | Min | Producto 2 | Min |
|---|---|---|---|
| C1 interpretación del diseño | 25 | D1 V1 esquema y tablas | 30 |
| C2 plan de trabajo estimado | 30 | D2 V2 restricciones, índices, vista y disparador | 40 |
| C3 stack justificado | 15 | D3 V3 roles y permisos | 20 |
| C4 Docker Compose, `.env.example` y pasos verificados | 35 | D4 V4 datos de prueba | 15 |
| C5 ramas, commits y solicitud de cambio | 25 | D5 pruebas SQL | 25 |
| C6 estándar de codificación | 40 | D6 y D7 ejecución desde cero y evidencia | 30 |
| `ENTREGA-G2.md` | 10 | «Schema migration» en `data-model.md` | 10 |
| **Total** | **180** | **Total** | **170** |

---

## 2. Producto 1: plan de construcción del servicio (RAP 593106 · 25 %)

### 2.1 Artefactos obligatorios y mínimos

| Artefacto | Dónde | Mínimo exigible |
|---|---|---|
| C1. Interpretación del diseño | `construction-plan.md` | Tabla con ≥ 8 elementos del diseño de tu servicio (tablas, endpoints, eventos o reglas de negocio), cada uno con el documento de origen (README, `data-model.md`, contrato de API, `events.md`) y la tarea que origina |
| C2. Plan de trabajo | `construction-plan.md` | ≥ 10 tareas con ID, descripción, insumo de diseño, estimación en horas, orden o dependencia y criterio de terminado; incluye las tareas de base de datos (V1 a V4) y la ruta crítica |
| C3. Selección del stack | `construction-plan.md` | Lenguaje, marco de trabajo, motor de base de datos y herramienta de migraciones, tomados de las guías de `_stacks/`, justificados con ≥ 3 condiciones del servicio o del equipo; ≥ 1 alternativa descartada con su razón |
| C4. Herramientas de desarrollo configuradas | `docker-compose.yml`, `.env.example`, sección «Entorno local» de `construction-plan.md` | El contenedor de la base de datos del servicio se levanta con un solo comando; versiones fijadas (no `latest`); variables en `.env.example` sin secretos reales; `.env` excluido del repositorio; pasos de instalación con el comando y la salida esperada de cada uno |
| C5. Versionamiento configurado | Sección «Versionamiento» de `construction-plan.md`, historial y solicitud de cambio | Estrategia de ramas escrita (tu rama, la de integración y la principal, y cómo se promueve); ≥ 4 commits propios con formato `tipo(alcance): descripción`; solicitud de cambio abierta con la plantilla del equipo (`.github/pull_request_template.md`; si el equipo no la tiene, la agregas en tu rama) |
| C6. Estándar de codificación | `coding-standard.md` | Reglas de nombrado de clases, métodos, atributos, variables, constantes, tablas, campos, llaves, restricciones e índices; reglas de indentación y longitud de línea; regla de documentación del código (formato del comentario de clase o función, según el lenguaje); cada regla con un ejemplo correcto y uno incorrecto; coherente con el lenguaje elegido en C3 |

Recomendado y **no calificado**: proteger la rama de integración (exigir revisión antes de fusionar) y agregar una verificación automática (por ejemplo, una acción que ejecute las migraciones en un contenedor). Si lo haces, descríbelo en «Versionamiento».

### 2.2 Rúbrica

| # | Criterio del programa (texto literal) | Artefactos | Peso |
|---|---|---|---|
| 1 | Interpreta el informe de diseño para definir el plan de trabajo en la construcción del software. | C1 y C2 | 35 |
| 2 | Selecciona y configura herramientas de desarrollo de acuerdo con las condiciones del software a construir. | C3 y C4 | 25 |
| 3 | Selecciona y configura herramientas de versionamiento para el control de cambios en el código. | C5 | 20 |
| 4 | Define estándares de codificación de acuerdo con las reglas de la plataforma de desarrollo seleccionada. | C6 | 20 |

| Criterio | 100 | 70 | 40 | 0 |
|---|---|---|---|---|
| **1. Interpretación del diseño y plan de trabajo** | ≥ 8 elementos del diseño, cada uno con su documento de origen y la tarea que origina; ≥ 10 tareas con ID, insumo, estimación, dependencia y criterio de terminado; el orden respeta las dependencias (por ejemplo, V1 antes de V2, esquema antes de seguridad); ruta crítica identificada; toda tabla de `data-model.md` tiene al menos una tarea | 6 o 7 elementos, u 8 o 9 tareas, o faltan estimación o criterio de terminado en hasta el 30 % de las tareas, o una dependencia en orden incorrecto | Lista de tareas sin relación con el diseño del servicio, o sin estimaciones, o menos de 6 tareas | Ausente o corresponde a otro servicio |
| **2. Herramientas de desarrollo** | Stack con ≥ 3 condiciones concretas y una alternativa descartada; `docker-compose.yml` que levanta la base con un comando, versión de imagen fijada, `healthcheck` y volumen; `.env.example` sin secretos reales y `.env` ignorado; pasos verificados con comando y salida esperada | Stack con 1 o 2 condiciones, o compose funcional sin versión fijada o sin `healthcheck`, o un paso sin salida esperada | Stack sin justificar, o compose que no levanta, o secretos reales en el repositorio | Ausente |
| **3. Versionamiento** | Estrategia de ramas escrita y aplicada; ≥ 4 commits propios en formato convencional con alcance; solicitud de cambio abierta desde `g2/<servicio>-<usuario>` con la plantilla diligenciada (qué cambia, cómo se prueba) | 2 o 3 commits convencionales, o plantilla sin diligenciar, o estrategia escrita pero no aplicada | Commits sin formato, o trabajo directo en la rama de integración | Sin control de versiones verificable |
| **4. Estándar de codificación** | Reglas para clases, métodos, atributos, variables, constantes, tablas, campos, llaves, restricciones e índices; indentación y longitud de línea; documentación del código con su formato; ejemplo correcto e incorrecto por regla; coherente con el lenguaje de C3 y **aplicado** en tus scripts de P2 | Falta 1 o 2 de las categorías de nombrado, o faltan ejemplos en hasta el 30 % de las reglas, o hasta 3 incumplimientos del propio estándar en P2 | Estándar genérico copiado sin relación con el lenguaje elegido, o sin reglas de base de datos | Ausente |

---

## 3. Producto 2: base de datos construida (RAP 593107 · 25 %)

### 3.1 Artefactos obligatorios y mínimos

| Artefacto | Dónde | Mínimo exigible |
|---|---|---|
| D1. Esquema y tablas | `db/migrations/V1__create_schema.sql` | `CREATE SCHEMA` del servicio; ≥ 4 tablas de tu modelo de datos con PK con nombre, tipos adecuados, `NOT NULL` donde el modelo lo exige y campos de auditoría (`created_at`, `updated_at`) en las tablas principales (las tablas intermedias de una relación N:M pueden omitirlos) |
| D2. Restricciones, índices y objetos | `db/migrations/V2__constraints_indexes.sql` | FK con nombre **solo entre tablas de tu servicio**, con `ON DELETE` declarado en todas; ≥ 3 `CHECK` y ≥ 2 `UNIQUE` que respondan a reglas del diseño; ≥ 3 índices (al menos uno sobre una FK); ≥ 1 vista; ≥ 1 función o procedimiento, o ≥ 1 disparador (por ejemplo, `updated_at` o auditoría) |
| D3. Seguridad | `db/migrations/V3__security_roles.sql` | ≥ 2 roles con mínimo privilegio (por ejemplo, aplicación y solo lectura); permisos concedidos con `GRANT` por objeto y `GRANT USAGE` sobre el esquema; al menos un `REVOKE` explícito que documente la política (por ejemplo, `REVOKE ALL ON SCHEMA ... FROM PUBLIC`); sin contraseñas reales en el script |
| D4. Datos de prueba | `db/migrations/V4__seed.sql` | ≥ 5 filas en cada tabla principal y filas en las tablas intermedias; datos ficticios |
| D5. Pruebas | `db/tests/pruebas.sql` | ≥ 4 pruebas de violación de restricciones (al menos un `CHECK`, un `UNIQUE` y una FK); ≥ 2 pruebas de permisos (una operación negada y una permitida con `SET ROLE`); 1 transacción con `ROLLBACK` que muestre el dato antes y después; 1 transacción con `COMMIT` de varias operaciones |
| D6. Ejecución desde cero | `docker-compose.yml` (el mismo de C4) | Servicio de base de datos llamado `<servicio>-db`, con `./db/migrations` montado en `/docker-entrypoint-initdb.d` y `./db/tests` montado en `/tests` (como en Plantillas_G2, sección 4); `docker compose down -v` seguido de `docker compose up -d` ejecuta V1 a V4 en orden y sin errores |
| D7. Evidencia | `db/EVIDENCIA.md` | Comandos ejecutados y **salida real copiada de la terminal** (no capturas editadas ni texto escrito a mano): registro de las migraciones, `\dt`, `\d` de ≥ 2 tablas, `\dv`, `\df` o lista de disparadores, `\dp` y la salida completa de `pruebas.sql` |
| D8. Estrategia de migración | Sección «Schema migration» de `data-model.md` | Herramienta, ubicación, convención de nombres, regla de no modificar una migración aplicada y cómo se revierte un cambio |

**Base de datos por servicio.** Tu servicio guarda el identificador de una entidad de otro servicio (por ejemplo, `cliente_id`), pero **no declara FK hacia tablas de otro servicio**. Una FK entre servicios es un error de diseño y se descuenta en el criterio 2.

**Motor.** PostgreSQL 16 por defecto. Se acepta MySQL 8 si tu equipo ya lo eligió en el stack (C3), con los equivalentes de cada objeto; el ejemplo y la prueba de desempeño usan PostgreSQL.

### 3.2 Rúbrica

| # | Criterio del programa (texto literal) | Artefactos | Peso |
|---|---|---|---|
| 1 | Crea la base de datos integrando los objetos de acuerdo con la funcionalidad del software. | D1, D4, vista y función o disparador de D2, D6, D7 y D8 | 40 |
| 2 | Implementa restricciones en la base de datos de acuerdo con las reglas de diseño. | Restricciones e índices de D2 y pruebas de violación de D5 | 30 |
| 3 | Define esquemas de seguridad en la base de datos para mantener la integridad de la información. | D3, pruebas de permisos y transacciones de D5 | 30 |

| Criterio | 100 | 70 | 40 | 0 |
|---|---|---|---|---|
| **1. Creación de la base de datos y sus objetos** | V1 a V4 se ejecutan desde cero sin errores; el 100 % de las tablas del modelo de datos del servicio existe con PK, tipos coherentes con el diccionario y `NOT NULL`; ≥ 1 vista y ≥ 1 función o disparador que **responden a una funcionalidad del servicio** (no de relleno); datos de prueba que permiten ejercitar las consultas; `EVIDENCIA.md` con salida real completa; «Schema migration» actualizada | Se ejecuta, pero faltan hasta 2 tablas del modelo o hasta 3 diferencias de tipo o nombre con el modelo, o la vista o la función no se relaciona con el servicio, o la evidencia está incompleta | Scripts que solo se ejecutan con correcciones manuales, o menos de 4 tablas, o sin evidencia de ejecución | No se ejecuta o solo hay documentación |
| **2. Restricciones** | Toda FK del servicio con nombre y `ON DELETE` justificado por la regla del diseño; ≥ 3 `CHECK` y ≥ 2 `UNIQUE` que corresponden a reglas escritas en el diseño (cada una citada en un comentario); ≥ 3 índices justificados; ninguna FK entre servicios; ≥ 4 pruebas de violación cuya salida muestra el `ERROR` con el nombre de la restricción | 2 `CHECK` o 1 `UNIQUE`, o restricciones sin nombre, o 2 o 3 pruebas de violación, o índices sin justificar | Restricciones que no corresponden a ninguna regla del diseño, o sin pruebas de violación, o una FK hacia otro servicio | Sin restricciones además de las PK |
| **3. Esquema de seguridad e integridad** | ≥ 2 roles de grupo con mínimo privilegio, permisos concedidos por objeto (no `ALL PRIVILEGES` al rol de la aplicación); `GRANT USAGE` sobre el esquema y `REVOKE` explícito; ningún rol de la aplicación con permisos de DDL; pruebas que muestran una operación negada (`permission denied`) y una permitida; transacción con `ROLLBACK` que deja el dato igual y transacción con `COMMIT` de varias operaciones; sin contraseñas reales en el repositorio | 2 roles pero uno con más permisos de los necesarios, o solo una prueba de permisos, o falta la transacción con `COMMIT` | Un solo rol, o `GRANT ALL` a todos, o sin pruebas de permisos ni transacciones | Sin roles ni permisos |

### 3.3 Cómo reproduce el instructor tus migraciones

En la copia de tu rama tomada a la hora del corte, en la carpeta de tu servicio:

```bash
cp .env.example .env
docker compose down -v
docker compose up -d
docker compose logs          # V1 a V4 ejecutados, sin ERROR
docker compose exec <servicio>-db psql -U <usuario> -d <base> -f /tests/pruebas.sql
```

Si un paso falla por algo que no está en tu repositorio (un archivo que solo existe en tu equipo, una variable sin documentar, un puerto fijo distinto del documentado), cuenta como que **no se ejecuta**. Prueba tú mismo esta secuencia antes del corte, con el volumen borrado.

La compuerta del RAP 593107 depende solo de que **las migraciones se ejecuten desde cero sin errores**. Si el nombre del servicio o el montaje de `db/tests` no siguen D6 pero las migraciones sí corren, el instructor adapta el comando de las pruebas y lo descuenta en el criterio 1, no en la compuerta.

---

## 4. Prueba de desempeño (RAP 593107 · 25 %)

**Qué es.** El jueves 3 de diciembre de 2026, después de la prueba de conocimiento, de forma presencial e individual y **en computador** (el del ambiente o tu portátil), recibes por Moodle el paquete de un caso corto que no conoces: un modelo de datos de cuatro tablas con sus reglas de negocio y sus reglas de acceso. Hay dos versiones del caso, repartidas por turno. Tienes **90 minutos** para escribir y ejecutar en un contenedor de PostgreSQL:

1. `01-esquema.sql`: esquema y tablas con PK, tipos y `NOT NULL`.
2. `02-restricciones.sql`: FK, `CHECK`, `UNIQUE`, índices y una vista, según las reglas del caso.
3. `03-seguridad.sql`: los roles y permisos que piden las reglas de acceso, con `GRANT` y `REVOKE`.
4. `04-pruebas.sql`: datos mínimos y pruebas de violación, de permisos y una transacción con `ROLLBACK`.
5. `salida.txt`: la salida completa de la ejecución de los cuatro scripts, tal como la produce la terminal.

**Preparación obligatoria antes de la sesión** (no hay internet durante la prueba): tener Docker funcionando y la imagen descargada con `docker pull postgres:16-alpine`. El paquete trae el comando exacto para iniciar el contenedor. Si tu equipo no tiene Docker, avisa al instructor a más tardar el martes 1 de diciembre de 2026 para usar un equipo del ambiente.

**Recursos permitidos:** apuntes, esta guía, el banco de preguntas y Plantillas_G2 sin conexión. Solo se permite la conexión a Moodle (Zajuna) para descargar el paquete y subir el archivo. No se permite otro uso de internet, mensajería, asistentes de IA ni ayuda de otras personas. Una infracción anula la prueba (0).

**Cómo entregas.** Al terminar subes **un solo archivo comprimido** (`G2-desempeno-<variante>.zip`) con los cinco archivos a la tarea de Moodle de la prueba. Plantillas_G2, sección 11, da el detalle. Lo que no esté en la tarea al cierre no se evalúa.

**Topes:** sin `salida.txt`, tope 60. Scripts que no se ejecutan en ningún punto (por ejemplo, `01-esquema.sql` falla en la primera tabla), tope 40. El instructor reproduce tus scripts en un contenedor limpio y **califica sobre la salida reproducida**. Si la salida que entregas difiere en lo sustancial de la reproducida (por ejemplo, muestra objetos o pruebas que tus scripts no producen), el instructor conversa contigo antes de calificar. Los errores «already exists» por haber ejecutado dos veces sin `docker rm -f` no cuentan en contra.

| # | Criterio del programa (texto literal) | Aspecto que se observa | Peso |
|---|---|---|---|
| 1 | Crea la base de datos integrando los objetos de acuerdo con la funcionalidad del software. | Esquema, tablas, llaves, tipos y vista del caso; ejecución sin errores | 35 |
| 2 | Implementa restricciones en la base de datos de acuerdo con las reglas de diseño. | Cada regla de negocio del caso convertida en la restricción correcta y probada | 35 |
| 3 | Define esquemas de seguridad en la base de datos para mantener la integridad de la información. | Roles y permisos según las reglas de acceso, pruebas de permisos y transacción | 30 |

| Criterio | 100 | 70 | 40 | 0 |
|---|---|---|---|---|
| **1. Objetos** | Las 4 tablas con PK, tipos adecuados y `NOT NULL` según el caso; FK correctas (incluida la tabla intermedia con llave compuesta); la vista pedida devuelve lo que el caso exige; los scripts se ejecutan en orden sin errores | 1 error de tipo, de llave o de la vista, o un script con un error que no impide el resto | 2 o más errores de llaves, o la vista falta | No crea las tablas |
| **2. Restricciones** | Todas las reglas de negocio del caso implementadas con la restricción correcta y con nombre; ≥ 3 pruebas de violación con el `ERROR` visible en `salida.txt` | Falta 1 regla, o 1 o 2 pruebas de violación | Faltan 2 o más reglas, o sin pruebas | Sin restricciones además de las PK |
| **3. Seguridad e integridad** | Los roles pedidos con exactamente los permisos de las reglas de acceso (ni más ni menos) y `GRANT USAGE` sobre el esquema; prueba de una operación negada y una permitida; transacción con `ROLLBACK` que deja el dato igual | Un rol con un permiso de más o de menos, o falta la prueba de permisos o la transacción | Roles creados sin permisos correctos, o `GRANT ALL` | Sin roles |

El instructor califica con una **solución de referencia privada** de cada versión del caso.

---

## 5. Prueba de conocimiento (RAP 593106 y 593107 · 25 %)

Se presenta como **cuestionario en la plataforma Moodle (Zajuna)**, de forma presencial en el ambiente de formación y con **calificación automática**: la nota sobre 100 que calcula Moodle es la nota de la evidencia de conocimiento. 20 preguntas de selección múltiple (una sola respuesta correcta), 5 puntos cada una, 40 minutos, sin recursos. **10 preguntas son variantes de preguntas del banco** (el mismo concepto con otro caso, otros datos u otra redacción; memorizar la letra o el texto del banco no sirve) **y 10 son inéditas**. El examen y su clave no se publican; el banco público (Banco_Preguntas_G2_v2) es un documento de estudio sin respuestas.

**Tabla de especificaciones:**

| RAP | Preguntas del examen (20) | Preguntas del banco (60) | Qué se verifica (criterios del programa, resumidos) |
|---|---|---|---|
| 593106 (01) Planear la construcción | 10 (5 variantes del banco y 5 inéditas) | 30 | Interpretar el informe de diseño para el plan de trabajo; estimación y dependencias; seleccionar y configurar herramientas de desarrollo (contenedores, variables de entorno, stack); herramientas de versionamiento, control de cambios e integración continua; estándares de codificación (documentación, nombrado de variables, métodos, atributos, clases, tablas y campos, indentación) |
| 593107 (02) Construir la base de datos | 10 (5 variantes del banco y 5 inéditas) | 30 | Motores relacionales (SMBD, instancias, configuración, objetos, seguridad, permisos, copias de seguridad y restauración); conceptos NoSQL (Redis, MongoDB); SQL DDL, DML y DCL; restricciones; transacciones; procedimientos, funciones y disparadores; base de datos por servicio y migraciones |

Los aciertos de cada RAP se cuentan por separado para la nota de cada resultado (sección 1.2).

---

## 6. Resumen de topes

| Situación | Tope |
|---|---|
| Falta un artefacto obligatorio (por producto); no alcanzar la cantidad mínima solo baja el nivel del criterio | 60 |
| Las migraciones no se ejecutan desde cero sin errores (Producto 2) — además, el RAP 593107 no se aprueba | 40 |
| Sin ningún día con commits sustantivos propios en el periodo (por fecha de push) | 60 |
| Commits sustantivos en un solo día del periodo | 70 |
| Rama sin solicitud de cambio abierta antes del corte | 70 |
| `ENTREGA-G2.md` ausente o incompleto | 70 |
| Contenido idéntico a otro aprendiz sin declarar (tras la aclaración con réplica) | 40 |
| No explicas tu propio producto en la verificación oral | 50 (ese producto) |
| Prueba de desempeño sin `salida.txt` | 60 |
| Prueba de desempeño con scripts que no se ejecutan en ningún punto | 40 |
| Infracción de los recursos en la prueba de desempeño o de conocimiento | 0 en esa prueba |
