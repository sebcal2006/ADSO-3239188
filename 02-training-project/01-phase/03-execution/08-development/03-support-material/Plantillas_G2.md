# Plantillas y ejemplo completo · Guía 2: Planeación de la construcción y base de datos (v2)

**Ficha 3239188 · Análisis y Desarrollo de Software · Competencia 220501096 (Construcción del software) · RAP 593106 y 593107**

Este archivo reúne los formatos que la guía pide (interpretación del diseño, plan de trabajo, selección del stack, entorno local, versionamiento, estándar de codificación, migraciones, pruebas y evidencia) con un ejemplo completo de un servicio pequeño en un dominio **distinto** de los proyectos de la ficha y de las pruebas: el servicio `reservas` de una cancha deportiva de barrio. Las migraciones y las pruebas de este ejemplo **se ejecutaron de verdad** en PostgreSQL 16 y la salida que aparece en la sección 9 es la real.

Es un modelo de **forma**: tus artefactos deben salir del diseño de **tu** servicio (el de la guía 1), con tus tablas, tus reglas y tus roles. Entregar este ejemplo con otros nombres cuenta como artefacto no entregado. Los mínimos exigidos están en **Rubricas_G2.md**.

---

## 0. Diseño del servicio del ejemplo (lo que se interpreta)

Extracto del README, del modelo de datos y del contrato del servicio `03-reservas` (el número es de ejemplo):

- **Responsabilidad:** registrar las reservas de canchas y el alquiler de implementos. Es dueño de los datos de canchas, implementos y reservas. Los clientes son de otro servicio (`clientes`): `reservas` guarda solo `cliente_id`.
- **Tablas del modelo de datos (guía 1):** `cancha`, `implemento`, `reserva`, `reserva_implemento` (N:M entre reserva e implemento).
- **Reglas de negocio:** RN-01 la tarifa por hora es mayor que cero; RN-02 una cancha no se reserva dos veces con la misma hora de inicio el mismo día; RN-03 la hora de fin es posterior a la de inicio; RN-04 el estado es PENDIENTE, CONFIRMADA o CANCELADA; RN-05 el stock de implementos nunca es negativo; RN-06 el código de la cancha es único; RN-07 el deporte es FUTBOL, BALONCESTO, TENIS o VOLEIBOL; RN-08 el valor total de una reserva no es negativo; RN-09 la cantidad alquilada de un implemento es mayor que cero; RN-10 el nombre de un implemento es único.
- **Contrato de API:** `GET /canchas`, `POST /reservas`, `PATCH /reservas/{id}/estado`, `GET /agenda?fecha=`.
- **Eventos:** publica `ReservaConfirmada`; consume `ClienteDesactivado`.
- **Acceso:** la API lee y escribe; el tablero de la portería solo consulta la agenda, sin ver clientes ni valores.

---

## 1. Interpretación del diseño (C1)

En `construction-plan.md`. Una fila por elemento del diseño (≥ 8), con su origen y la tarea que origina.

| # | Elemento del diseño | Documento de origen | Qué implica para la construcción | Tarea |
|---|---|---|---|---|
| E-01 | Tabla `cancha` con código único (RN-06) | `data-model.md` | Tabla con PK y `UNIQUE (codigo)` | T-03, T-04 |
| E-02 | Tabla `reserva` y RN-02, RN-03, RN-04 | `data-model.md` | Tabla con `CHECK` de horas y estado, y `UNIQUE (cancha_id, fecha, hora_inicio)` | T-03, T-04 |
| E-03 | Relación N:M reserva-implemento | `data-model.md` | Tabla intermedia con llave compuesta y dos FK | T-03, T-04 |
| E-04 | `cliente_id` pertenece a otro servicio | README (responsabilidad) | Se guarda el identificador **sin FK** e indexado | T-03, T-04 |
| E-05 | `GET /agenda?fecha=` | Contrato de API | Vista `v_agenda` e índice por fecha | T-04 |
| E-06 | El tablero solo consulta la agenda | README (acceso) | Rol de solo lectura con permiso únicamente sobre la vista | T-05 |
| E-07 | `PATCH /reservas/{id}/estado` | Contrato de API | `updated_at` mantenido por disparador | T-04 |
| E-08 | Evento `ReservaConfirmada` | `events.md` | Confirmar y publicar en la misma transacción (fuera del alcance de G2; queda en el plan) | T-11 |

## 2. Plan de trabajo (C2)

En `construction-plan.md`. ≥ 10 tareas, en orden; la estimación es en horas; «Depende de» define el orden.

| ID | Tarea | Insumo de diseño | Estimación (h) | Depende de | Criterio de terminado |
|---|---|---|---|---|---|
| T-01 | Configurar `docker-compose.yml` y `.env.example` de la base del servicio | `10-devops/local-setup.md` | 0,5 | — | `docker compose up -d` deja el contenedor `healthy` |
| T-02 | Escribir el estándar de codificación | `_stacks/python-fastapi.md`, `06-data/models.md` | 1 | — | `coding-standard.md` con reglas y ejemplos |
| T-03 | V1: esquema y tablas | E-01 a E-04 | 0,5 | T-01, T-02 | V1 corre sin errores en contenedor limpio |
| T-04 | V2: FK, CHECK, UNIQUE, índices, vista y disparador | E-01 a E-05, E-07 | 1 | T-03 | V1 y V2 corren sin errores; `\d` muestra las restricciones |
| T-05 | V3: roles y permisos | E-06 | 0,5 | T-04 | `\dp` muestra solo los permisos definidos |
| T-06 | V4: datos de prueba | Reglas RN-01 a RN-06 | 0,5 | T-04 | ≥ 5 filas por tabla principal |
| T-07 | Pruebas SQL de restricciones, permisos y transacciones | RN-01 a RN-06, E-06 | 1 | T-05, T-06 | Cada prueba muestra el resultado esperado |
| T-08 | Evidencia de ejecución desde cero | — | 0,5 | T-07 | `EVIDENCIA.md` con salida real |
| T-09 | Endpoints `GET /canchas` y `GET /agenda` | Contrato de API | 3 | T-04 | Pruebas de integración en verde |
| T-10 | Endpoints `POST /reservas` y `PATCH /reservas/{id}/estado` | Contrato de API | 4 | T-09 | Pruebas de integración en verde |
| T-11 | Publicación de `ReservaConfirmada` | `events.md` | 3 | T-10 | Evento visible en el broker local |

**Ruta crítica:** T-01 → T-03 → T-04 → T-05 → T-07 → T-08 (G2). Las tareas T-09 a T-11 quedan planeadas para las guías de codificación.

## 3. Selección del stack (C3)

| Decisión | Elegido | Condiciones del servicio o del equipo que lo justifican | Alternativa descartada y razón |
|---|---|---|---|
| Lenguaje y marco | Python 3.12 + FastAPI (`_stacks/python-fastapi.md`) | (1) el equipo ya programó en Python; (2) el servicio es una API REST pequeña; (3) FastAPI documenta el contrato automáticamente | Java + Spring: más configuración de la que necesita un servicio de 4 tablas |
| Motor | PostgreSQL 16 | (1) reglas que exigen restricciones y transacciones; (2) roles y permisos por objeto; (3) imagen oficial liviana | MongoDB: las relaciones fijas y la N:M se modelan mejor en relacional |
| Migraciones | Scripts SQL `V1__` a `V4__` ejecutados por el contenedor (compatibles con Flyway) | (1) el equipo aún no tiene código; (2) se reproducen desde cero con un comando | Alembic: atado al código Python, que todavía no existe |

## 4. Entorno local (C4)

Archivos en la carpeta del servicio. Versión de imagen fijada, `healthcheck`, volumen con nombre, y las migraciones montadas en `/docker-entrypoint-initdb.d` (el contenedor las ejecuta en orden alfabético **solo cuando el volumen está vacío**; por eso se prueba con `down -v`). El servicio de la base se llama `<servicio>-db` y monta `db/tests` en `/tests`: así lo exige D6 y así reproduce el instructor tus pruebas.

`docker-compose.yml`:

```yaml
services:
  reservas-db:
    image: postgres:16-alpine
    container_name: reservas-db
    environment:
      POSTGRES_DB: ${POSTGRES_DB}
      POSTGRES_USER: ${POSTGRES_USER}
      POSTGRES_PASSWORD: ${POSTGRES_PASSWORD}
    ports:
      - "${DB_PORT:-5433}:5432"
    volumes:
      # Las migraciones se ejecutan en orden alfabetico SOLO cuando el volumen esta vacio.
      - ./db/migrations:/docker-entrypoint-initdb.d:ro
      - ./db/tests:/tests:ro
      - reservas-datos:/var/lib/postgresql/data
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U ${POSTGRES_USER} -d ${POSTGRES_DB}"]
      interval: 5s
      timeout: 3s
      retries: 10

volumes:
  reservas-datos:
```

`.env.example` (el `.env` real va en `.gitignore`):

```
# Copiar como .env (el .env NO se versiona). Valores solo para desarrollo local.
POSTGRES_DB=reservas
POSTGRES_USER=reservas_admin
POSTGRES_PASSWORD=cambiar_en_local
DB_PORT=5433
```

Sección «Entorno local» de `construction-plan.md`: cada paso con el comando y la salida esperada.

| Paso | Comando | Salida esperada |
|---|---|---|
| 1 | `docker --version` | `Docker version 24` o superior |
| 2 | `cp .env.example .env` | Sin salida |
| 3 | `docker compose up -d` | `Container reservas-db Started` |
| 4 | `docker compose ps` | Estado `healthy` |
| 5 | `docker compose logs reservas-db` | `running /docker-entrypoint-initdb.d/V1__...` hasta `V4__...`, sin `ERROR` |

## 5. Versionamiento (C5)

Sección «Versionamiento» de `construction-plan.md`:

- **Ramas:** `main` (estable) ← `dev` (integración) ← `g2/reservas-<usuario>` (mi trabajo de la guía). Nadie hace commit directo en `dev` ni en `main`; todo entra por solicitud de cambio con una revisión.
- **Commits convencionales:** `tipo(alcance): descripción en minúscula, en imperativo y sin punto final`.

```
chore(reservas): configurar docker compose de la base del servicio
docs(reservas): definir estandar de codificacion
feat(reservas): crear esquema y tablas en V1
feat(reservas): agregar restricciones, indices y vista en V2
feat(reservas): definir roles de minimo privilegio en V3
test(reservas): agregar pruebas de restricciones y permisos
```

Incorrectos: `cambios`, `avance final`, `Update V2.sql`, `subo todo`.

- **Plantilla de solicitud de cambio** (`.github/pull_request_template.md`, una por equipo):

```markdown
## Qué cambia
## Servicio y archivos
## Cómo se prueba (comandos)
## Lista de verificación
- [ ] Las migraciones corren desde cero (`docker compose down -v` y `up -d`)
- [ ] Sin secretos en el repositorio
- [ ] Cumple coding-standard.md
```

## 6. Estándar de codificación (C6)

En `coding-standard.md`. Cada regla con ejemplo correcto e incorrecto. El ejemplo usa Python; si tu stack es otro, sigue las convenciones de tu guía en `_stacks/` (por ejemplo, `camelCase` para métodos en Java y TypeScript).

| Elemento | Regla | Correcto | Incorrecto |
|---|---|---|---|
| Clase | `PascalCase`, sustantivo en singular | `ReservaService` | `reserva_service`, `Reservas` |
| Método o función | `snake_case`, verbo en infinitivo | `confirmar_reserva()` | `ConfirmarReserva()`, `reserva()` |
| Atributo y variable | `snake_case`, nombre descriptivo | `valor_total` | `vt`, `ValorTotal` |
| Constante | `MAYUSCULAS_CON_GUION` | `ESTADOS_VALIDOS` | `estadosValidos` |
| Tabla | `snake_case`, singular, sin prefijos | `reserva_implemento` | `tblReservas`, `ReservaImplemento` |
| Campo | `snake_case`; FK como `<tabla>_id` | `cancha_id` | `idCancha`, `cancha` |
| Llave primaria y restricciones | `pk_<tabla>`, `fk_<tabla>_<referida>`, `uq_<tabla>_<campos>`, `ck_<tabla>_<regla>` | `ck_reserva_horas` | `reserva_check1` (nombre automático) |
| Índice | `idx_<tabla>_<campos>` | `idx_reserva_fecha` | `indice1` |
| Indentación | 4 espacios, sin tabuladores; líneas de máximo 100 caracteres | (4 espacios) | Mezcla de tabuladores y espacios |
| SQL | Palabras clave en MAYÚSCULAS, una columna por línea en `CREATE TABLE` | `CREATE TABLE reservas.cancha (` | `create table Cancha(id uuid,codigo text)` |
| Documentación del código | Docstring en cada clase y función pública: qué hace, parámetros, retorno y errores | `"""Confirma la reserva. Args: reserva_id. Raises: ReservaNoEncontrada."""` | Sin docstring, o `# funcion` |
| Documentación SQL | Encabezado en cada migración (qué hace) y comentario con la regla de negocio en cada `CHECK` | `-- RN-03: la hora de fin es posterior` | Script sin comentarios |

---

## 7. Migraciones (D1 a D4)

Carpeta `db/migrations/`. Una migración ya aplicada **no se modifica**: un cambio posterior va en `V5__...`. Llaves foráneas **solo dentro del servicio**: `cliente_id` no tiene FK porque `clientes` es otro servicio.

`V1__create_schema.sql`:

```sql
-- V1__create_schema.sql
-- Servicio: reservas (ejemplo de Plantillas_G2, dominio: reserva de canchas deportivas)
-- Crea el esquema del servicio y sus tablas con llave primaria, tipos y NOT NULL.
-- Las llaves foraneas, CHECK, UNIQUE e indices van en V2.

CREATE SCHEMA IF NOT EXISTS reservas;

CREATE TABLE reservas.cancha (
    id            UUID          NOT NULL DEFAULT gen_random_uuid(),
    codigo        VARCHAR(10)   NOT NULL,
    nombre        VARCHAR(80)   NOT NULL,
    deporte       VARCHAR(20)   NOT NULL,
    tarifa_hora   NUMERIC(10,2) NOT NULL,
    activa        BOOLEAN       NOT NULL DEFAULT TRUE,
    created_at    TIMESTAMPTZ   NOT NULL DEFAULT NOW(),
    updated_at    TIMESTAMPTZ   NOT NULL DEFAULT NOW(),
    CONSTRAINT pk_cancha PRIMARY KEY (id)
);

CREATE TABLE reservas.implemento (
    id              UUID          NOT NULL DEFAULT gen_random_uuid(),
    nombre          VARCHAR(60)   NOT NULL,
    stock           INTEGER       NOT NULL,
    valor_alquiler  NUMERIC(10,2) NOT NULL,
    created_at      TIMESTAMPTZ   NOT NULL DEFAULT NOW(),
    updated_at      TIMESTAMPTZ   NOT NULL DEFAULT NOW(),
    CONSTRAINT pk_implemento PRIMARY KEY (id)
);

-- cliente_id pertenece al servicio de clientes: se guarda el identificador,
-- pero NO se declara llave foranea (base de datos por servicio).
CREATE TABLE reservas.reserva (
    id            UUID          NOT NULL DEFAULT gen_random_uuid(),
    cancha_id     UUID          NOT NULL,
    cliente_id    UUID          NOT NULL,
    fecha         DATE          NOT NULL,
    hora_inicio   TIME          NOT NULL,
    hora_fin      TIME          NOT NULL,
    estado        VARCHAR(15)   NOT NULL DEFAULT 'PENDIENTE',
    valor_total   NUMERIC(10,2) NOT NULL,
    created_at    TIMESTAMPTZ   NOT NULL DEFAULT NOW(),
    updated_at    TIMESTAMPTZ   NOT NULL DEFAULT NOW(),
    CONSTRAINT pk_reserva PRIMARY KEY (id)
);

-- Tabla intermedia de la relacion N:M reserva - implemento (llave compuesta).
CREATE TABLE reservas.reserva_implemento (
    reserva_id     UUID     NOT NULL,
    implemento_id  UUID     NOT NULL,
    cantidad       INTEGER  NOT NULL,
    CONSTRAINT pk_reserva_implemento PRIMARY KEY (reserva_id, implemento_id)
);
```

`V2__constraints_indexes.sql`:

```sql
-- V2__constraints_indexes.sql
-- Restricciones con nombre (fk_, uq_, ck_), indices (idx_), vista (v_) y disparador (trg_).

-- Llaves foraneas: solo entre tablas de este servicio.
ALTER TABLE reservas.reserva
    ADD CONSTRAINT fk_reserva_cancha FOREIGN KEY (cancha_id)
        REFERENCES reservas.cancha (id) ON DELETE RESTRICT ON UPDATE CASCADE;

ALTER TABLE reservas.reserva_implemento
    ADD CONSTRAINT fk_reserva_implemento_reserva FOREIGN KEY (reserva_id)
        REFERENCES reservas.reserva (id) ON DELETE CASCADE,
    ADD CONSTRAINT fk_reserva_implemento_implemento FOREIGN KEY (implemento_id)
        REFERENCES reservas.implemento (id) ON DELETE RESTRICT;

-- Reglas de negocio como CHECK.
ALTER TABLE reservas.cancha
    ADD CONSTRAINT ck_cancha_tarifa_positiva CHECK (tarifa_hora > 0),          -- RN-01
    ADD CONSTRAINT ck_cancha_deporte CHECK (deporte IN ('FUTBOL', 'BALONCESTO', 'TENIS', 'VOLEIBOL'));  -- RN-07

ALTER TABLE reservas.implemento
    ADD CONSTRAINT ck_implemento_stock_no_negativo CHECK (stock >= 0);         -- RN-05

ALTER TABLE reservas.reserva
    ADD CONSTRAINT ck_reserva_horas CHECK (hora_fin > hora_inicio),            -- RN-03
    ADD CONSTRAINT ck_reserva_estado CHECK (estado IN ('PENDIENTE', 'CONFIRMADA', 'CANCELADA')),  -- RN-04
    ADD CONSTRAINT ck_reserva_valor CHECK (valor_total >= 0);                  -- RN-08

ALTER TABLE reservas.reserva_implemento
    ADD CONSTRAINT ck_reserva_implemento_cantidad CHECK (cantidad > 0);        -- RN-09

-- Unicidad.
ALTER TABLE reservas.cancha
    ADD CONSTRAINT uq_cancha_codigo UNIQUE (codigo);                           -- RN-06
ALTER TABLE reservas.implemento
    ADD CONSTRAINT uq_implemento_nombre UNIQUE (nombre);                       -- RN-10
-- RN-02: una cancha no se reserva dos veces a la misma hora de inicio el mismo dia.
ALTER TABLE reservas.reserva
    ADD CONSTRAINT uq_reserva_cancha_fecha_hora UNIQUE (cancha_id, fecha, hora_inicio);

-- Indices para las consultas frecuentes (FK y filtros).
CREATE INDEX idx_reserva_cancha_id   ON reservas.reserva (cancha_id);
CREATE INDEX idx_reserva_cliente_id  ON reservas.reserva (cliente_id);
CREATE INDEX idx_reserva_fecha       ON reservas.reserva (fecha);
CREATE INDEX idx_reserva_implemento_implemento_id ON reservas.reserva_implemento (implemento_id);

-- Vista: agenda de reservas vigentes, sin exponer cliente_id ni valores.
CREATE VIEW reservas.v_agenda AS
SELECT c.codigo AS cancha, c.deporte, r.fecha, r.hora_inicio, r.hora_fin, r.estado
FROM reservas.reserva r
JOIN reservas.cancha c ON c.id = r.cancha_id
WHERE r.estado <> 'CANCELADA';

-- Funcion y disparadores: mantienen updated_at sin depender de la aplicacion.
CREATE FUNCTION reservas.fn_actualizar_updated_at() RETURNS trigger
LANGUAGE plpgsql AS $$
BEGIN
    NEW.updated_at := NOW();
    RETURN NEW;
END;
$$;

CREATE TRIGGER trg_cancha_updated_at BEFORE UPDATE ON reservas.cancha
    FOR EACH ROW EXECUTE FUNCTION reservas.fn_actualizar_updated_at();
CREATE TRIGGER trg_implemento_updated_at BEFORE UPDATE ON reservas.implemento
    FOR EACH ROW EXECUTE FUNCTION reservas.fn_actualizar_updated_at();
CREATE TRIGGER trg_reserva_updated_at BEFORE UPDATE ON reservas.reserva
    FOR EACH ROW EXECUTE FUNCTION reservas.fn_actualizar_updated_at();
```

`V3__security_roles.sql`:

```sql
-- V3__security_roles.sql
-- Roles de grupo (NOLOGIN) con minimo privilegio. Las cuentas con inicio de sesion
-- y sus contrasenas NO van en las migraciones: se crean por ambiente con secretos.

CREATE ROLE reservas_app NOLOGIN;       -- la API del servicio: lee y escribe datos, sin DDL
CREATE ROLE reservas_lectura NOLOGIN;   -- reportes: solo consulta la agenda

-- Politica explicita: en un esquema nuevo PUBLIC no tiene acceso; el REVOKE lo deja escrito
-- y corrige cualquier permiso que alguien haya concedido de mas.
REVOKE ALL ON SCHEMA reservas FROM PUBLIC;
GRANT USAGE ON SCHEMA reservas TO reservas_app, reservas_lectura;

-- La aplicacion: SELECT, INSERT y UPDATE; DELETE solo en la tabla intermedia.
GRANT SELECT, INSERT, UPDATE ON reservas.cancha, reservas.implemento, reservas.reserva TO reservas_app;
GRANT SELECT, INSERT, UPDATE, DELETE ON reservas.reserva_implemento TO reservas_app;
GRANT SELECT ON reservas.v_agenda TO reservas_app;

-- Lectura: solo la vista, nunca las tablas base.
GRANT SELECT ON reservas.v_agenda TO reservas_lectura;
REVOKE ALL ON reservas.cancha, reservas.implemento, reservas.reserva, reservas.reserva_implemento FROM reservas_lectura;
```

`V4__seed.sql`:

```sql
-- V4__seed.sql
-- Datos de prueba ficticios (nunca datos reales de personas).

INSERT INTO reservas.cancha (id, codigo, nombre, deporte, tarifa_hora) VALUES
  ('11111111-1111-1111-1111-111111111101', 'F-01', 'Cancha sintetica norte', 'FUTBOL',     80000),
  ('11111111-1111-1111-1111-111111111102', 'F-02', 'Cancha sintetica sur',   'FUTBOL',     75000),
  ('11111111-1111-1111-1111-111111111103', 'B-01', 'Coliseo cubierto',       'BALONCESTO', 60000),
  ('11111111-1111-1111-1111-111111111104', 'T-01', 'Cancha de arcilla',      'TENIS',      50000),
  ('11111111-1111-1111-1111-111111111105', 'V-01', 'Cancha de arena',        'VOLEIBOL',   40000);

INSERT INTO reservas.implemento (id, nombre, stock, valor_alquiler) VALUES
  ('22222222-2222-2222-2222-222222222201', 'Balon de futbol',     10, 5000),
  ('22222222-2222-2222-2222-222222222202', 'Balon de baloncesto',  6, 5000),
  ('22222222-2222-2222-2222-222222222203', 'Raqueta de tenis',     8, 8000),
  ('22222222-2222-2222-2222-222222222204', 'Petos (juego de 10)',  4, 6000),
  ('22222222-2222-2222-2222-222222222205', 'Red de voleibol',      2, 7000);

INSERT INTO reservas.reserva (id, cancha_id, cliente_id, fecha, hora_inicio, hora_fin, estado, valor_total) VALUES
  ('33333333-3333-3333-3333-333333333301', '11111111-1111-1111-1111-111111111101', 'aaaaaaaa-0000-0000-0000-000000000001', '2026-12-10', '18:00', '19:00', 'CONFIRMADA', 85000),
  ('33333333-3333-3333-3333-333333333302', '11111111-1111-1111-1111-111111111101', 'aaaaaaaa-0000-0000-0000-000000000002', '2026-12-10', '19:00', '20:00', 'PENDIENTE',  80000),
  ('33333333-3333-3333-3333-333333333303', '11111111-1111-1111-1111-111111111103', 'aaaaaaaa-0000-0000-0000-000000000003', '2026-12-11', '17:00', '19:00', 'CONFIRMADA', 125000),
  ('33333333-3333-3333-3333-333333333304', '11111111-1111-1111-1111-111111111104', 'aaaaaaaa-0000-0000-0000-000000000001', '2026-12-12', '07:00', '08:00', 'CANCELADA',  50000),
  ('33333333-3333-3333-3333-333333333305', '11111111-1111-1111-1111-111111111105', 'aaaaaaaa-0000-0000-0000-000000000004', '2026-12-12', '16:00', '17:00', 'PENDIENTE',  47000);

INSERT INTO reservas.reserva_implemento (reserva_id, implemento_id, cantidad) VALUES
  ('33333333-3333-3333-3333-333333333301', '22222222-2222-2222-2222-222222222201', 1),
  ('33333333-3333-3333-3333-333333333303', '22222222-2222-2222-2222-222222222202', 1),
  ('33333333-3333-3333-3333-333333333305', '22222222-2222-2222-2222-222222222205', 1);
```

## 8. Pruebas (D5)

`db/tests/pruebas.sql`. Los `ERROR` de P1 a P5 son el **resultado esperado**: demuestran que la restricción o el permiso funciona.

```sql
-- pruebas.sql: demuestra que las restricciones, los permisos y las transacciones funcionan.
-- Se ejecuta con psql SIN detenerse en errores: los errores de P1 a P5 son el resultado esperado.

\echo '== P1 CHECK: tarifa negativa (se espera ERROR ck_cancha_tarifa_positiva)'
INSERT INTO reservas.cancha (codigo, nombre, deporte, tarifa_hora) VALUES ('F-09', 'Prueba', 'FUTBOL', -100);

\echo '== P2 UNIQUE: codigo repetido (se espera ERROR uq_cancha_codigo)'
INSERT INTO reservas.cancha (codigo, nombre, deporte, tarifa_hora) VALUES ('F-01', 'Duplicada', 'FUTBOL', 70000);

\echo '== P3 FK: cancha inexistente (se espera ERROR fk_reserva_cancha)'
INSERT INTO reservas.reserva (cancha_id, cliente_id, fecha, hora_inicio, hora_fin, valor_total)
VALUES ('99999999-9999-9999-9999-999999999999', 'aaaaaaaa-0000-0000-0000-000000000001', '2026-12-20', '10:00', '11:00', 80000);

\echo '== P4 CHECK: hora_fin anterior a hora_inicio (se espera ERROR ck_reserva_horas)'
INSERT INTO reservas.reserva (cancha_id, cliente_id, fecha, hora_inicio, hora_fin, valor_total)
VALUES ('11111111-1111-1111-1111-111111111102', 'aaaaaaaa-0000-0000-0000-000000000001', '2026-12-20', '11:00', '10:00', 80000);

\echo '== P5 Permisos: reservas_lectura intenta escribir y leer la tabla base (se esperan dos ERROR permission denied)'
SET ROLE reservas_lectura;
INSERT INTO reservas.cancha (codigo, nombre, deporte, tarifa_hora) VALUES ('X-01', 'Intrusa', 'TENIS', 1000);
SELECT count(*) FROM reservas.reserva;
\echo '== P5b reservas_lectura si puede leer la vista'
SELECT cancha, fecha, hora_inicio, estado FROM reservas.v_agenda ORDER BY fecha, hora_inicio;
RESET ROLE;

\echo '== P6 Transaccion con ROLLBACK: el stock vuelve a su valor original'
SELECT stock FROM reservas.implemento WHERE nombre = 'Balon de futbol';
BEGIN;
UPDATE reservas.implemento SET stock = stock - 3 WHERE nombre = 'Balon de futbol';
SELECT stock FROM reservas.implemento WHERE nombre = 'Balon de futbol';
ROLLBACK;
SELECT stock FROM reservas.implemento WHERE nombre = 'Balon de futbol';

\echo '== P7 Transaccion con COMMIT: reserva + implemento + descuento de stock, todo o nada'
BEGIN;
INSERT INTO reservas.reserva (id, cancha_id, cliente_id, fecha, hora_inicio, hora_fin, valor_total)
VALUES ('33333333-3333-3333-3333-333333333306', '11111111-1111-1111-1111-111111111102', 'aaaaaaaa-0000-0000-0000-000000000005', '2026-12-13', '09:00', '10:00', 81000);
INSERT INTO reservas.reserva_implemento (reserva_id, implemento_id, cantidad)
VALUES ('33333333-3333-3333-3333-333333333306', '22222222-2222-2222-2222-222222222204', 1);
UPDATE reservas.implemento SET stock = stock - 1 WHERE nombre = 'Petos (juego de 10)';
COMMIT;
SELECT nombre, stock FROM reservas.implemento WHERE nombre = 'Petos (juego de 10)';

\echo '== P8 Disparador: updated_at cambia al actualizar'
SELECT updated_at = created_at AS sin_cambios FROM reservas.cancha WHERE codigo = 'T-01';
UPDATE reservas.cancha SET tarifa_hora = 55000 WHERE codigo = 'T-01';
SELECT updated_at > created_at AS actualizado FROM reservas.cancha WHERE codigo = 'T-01';
```

## 9. Evidencia de ejecución (D6 y D7)

`db/EVIDENCIA.md`: comandos y **salida real** copiada de la terminal. Esta es la salida real del ejemplo.

**1. Desde cero:**

```
$ docker compose down -v
$ docker compose up -d
 Container reservas-db Started
$ docker compose logs reservas-db | grep -E "initdb.d|ERROR"
reservas-db  | /usr/local/bin/docker-entrypoint.sh: running /docker-entrypoint-initdb.d/V1__create_schema.sql
reservas-db  | /usr/local/bin/docker-entrypoint.sh: running /docker-entrypoint-initdb.d/V2__constraints_indexes.sql
reservas-db  | /usr/local/bin/docker-entrypoint.sh: running /docker-entrypoint-initdb.d/V3__security_roles.sql
reservas-db  | /usr/local/bin/docker-entrypoint.sh: running /docker-entrypoint-initdb.d/V4__seed.sql
```

**2. Objetos creados** (`docker compose exec reservas-db psql -U reservas_admin -d reservas`):

```
reservas=# \dt reservas.*
                   List of relations
  Schema  |        Name        | Type  |     Owner      
----------+--------------------+-------+----------------
 reservas | cancha             | table | reservas_admin
 reservas | implemento         | table | reservas_admin
 reservas | reserva            | table | reservas_admin
 reservas | reserva_implemento | table | reservas_admin
(4 rows)
```

```
reservas=# \d reservas.reserva
                                    Table "reservas.reserva"
   Column    |           Type           | Collation | Nullable |            Default             
-------------+--------------------------+-----------+----------+--------------------------------
 id          | uuid                     |           | not null | gen_random_uuid()
 cancha_id   | uuid                     |           | not null | 
 cliente_id  | uuid                     |           | not null | 
 fecha       | date                     |           | not null | 
 hora_inicio | time without time zone   |           | not null | 
 hora_fin    | time without time zone   |           | not null | 
 estado      | character varying(15)    |           | not null | 'PENDIENTE'::character varying
 valor_total | numeric(10,2)            |           | not null | 
 created_at  | timestamp with time zone |           | not null | now()
 updated_at  | timestamp with time zone |           | not null | now()
Indexes:
    "pk_reserva" PRIMARY KEY, btree (id)
    "idx_reserva_cancha_id" btree (cancha_id)
    "idx_reserva_cliente_id" btree (cliente_id)
    "idx_reserva_fecha" btree (fecha)
    "uq_reserva_cancha_fecha_hora" UNIQUE CONSTRAINT, btree (cancha_id, fecha, hora_inicio)
Check constraints:
    "ck_reserva_estado" CHECK (estado::text = ANY (ARRAY['PENDIENTE'::character varying, 'CONFIRMADA'::character varying, 'CANCELADA'::character varying]::text[]))
    "ck_reserva_horas" CHECK (hora_fin > hora_inicio)
    "ck_reserva_valor" CHECK (valor_total >= 0::numeric)
Foreign-key constraints:
    "fk_reserva_cancha" FOREIGN KEY (cancha_id) REFERENCES reservas.cancha(id) ON UPDATE CASCADE ON DELETE RESTRICT
Referenced by:
    TABLE "reservas.reserva_implemento" CONSTRAINT "fk_reserva_implemento_reserva" FOREIGN KEY (reserva_id) REFERENCES reservas.reserva(id) ON DELETE CASCADE
Triggers:
    trg_reserva_updated_at BEFORE UPDATE ON reservas.reserva FOR EACH ROW EXECUTE FUNCTION reservas.fn_actualizar_updated_at()
```

```
reservas=# \dv reservas.*
              List of relations
  Schema  |   Name   | Type |     Owner      
----------+----------+------+----------------
 reservas | v_agenda | view | reservas_admin
(1 row)

reservas=# \df reservas.*
                                  List of functions
  Schema  |           Name           | Result data type | Argument data types | Type 
----------+--------------------------+------------------+---------------------+------
 reservas | fn_actualizar_updated_at | trigger          |                     | func
(1 row)
```

```
reservas=# \dp reservas.*
                                              Access privileges
  Schema  |        Name        | Type  |           Access privileges           | Column privileges | Policies 
----------+--------------------+-------+---------------------------------------+-------------------+----------
 reservas | cancha             | table | reservas_admin=arwdDxt/reservas_admin+|                   | 
          |                    |       | reservas_app=arw/reservas_admin       |                   | 
 reservas | implemento         | table | reservas_admin=arwdDxt/reservas_admin+|                   | 
          |                    |       | reservas_app=arw/reservas_admin       |                   | 
 reservas | reserva            | table | reservas_admin=arwdDxt/reservas_admin+|                   | 
          |                    |       | reservas_app=arw/reservas_admin       |                   | 
 reservas | reserva_implemento | table | reservas_admin=arwdDxt/reservas_admin+|                   | 
          |                    |       | reservas_app=arwd/reservas_admin      |                   | 
 reservas | v_agenda           | view  | reservas_admin=arwdDxt/reservas_admin+|                   | 
          |                    |       | reservas_app=r/reservas_admin        +|                   | 
          |                    |       | reservas_lectura=r/reservas_admin     |                   | 
(5 rows)
```

**3. Pruebas** (`docker compose exec reservas-db sh -c "psql -U reservas_admin -d reservas -f /tests/pruebas.sql 2>&1"`):

```
== P1 CHECK: tarifa negativa (se espera ERROR ck_cancha_tarifa_positiva)
psql:/tests/pruebas.sql:5: ERROR:  new row for relation "cancha" violates check constraint "ck_cancha_tarifa_positiva"
DETAIL:  Failing row contains (a44f1b67-d878-4c5d-b77f-2eec81595c27, F-09, Prueba, FUTBOL, -100.00, t, 2026-11-27 00:55:36.345157+00, 2026-11-27 00:55:36.345157+00).
== P2 UNIQUE: codigo repetido (se espera ERROR uq_cancha_codigo)
psql:/tests/pruebas.sql:8: ERROR:  duplicate key value violates unique constraint "uq_cancha_codigo"
DETAIL:  Key (codigo)=(F-01) already exists.
== P3 FK: cancha inexistente (se espera ERROR fk_reserva_cancha)
psql:/tests/pruebas.sql:12: ERROR:  insert or update on table "reserva" violates foreign key constraint "fk_reserva_cancha"
DETAIL:  Key (cancha_id)=(99999999-9999-9999-9999-999999999999) is not present in table "cancha".
== P4 CHECK: hora_fin anterior a hora_inicio (se espera ERROR ck_reserva_horas)
psql:/tests/pruebas.sql:16: ERROR:  new row for relation "reserva" violates check constraint "ck_reserva_horas"
DETAIL:  Failing row contains (f4292003-06b7-4b46-a2ec-27a3927bb511, 11111111-1111-1111-1111-111111111102, aaaaaaaa-0000-0000-0000-000000000001, 2026-12-20, 11:00:00, 10:00:00, PENDIENTE, 80000.00, 2026-11-27 00:55:36.449323+00, 2026-11-27 00:55:36.449323+00).
== P5 Permisos: reservas_lectura intenta escribir y leer la tabla base (se esperan dos ERROR permission denied)
SET
psql:/tests/pruebas.sql:20: ERROR:  permission denied for table cancha
psql:/tests/pruebas.sql:21: ERROR:  permission denied for table reserva
== P5b reservas_lectura si puede leer la vista
 cancha |   fecha    | hora_inicio |   estado   
--------+------------+-------------+------------
 F-01   | 2026-12-10 | 18:00:00    | CONFIRMADA
 F-01   | 2026-12-10 | 19:00:00    | PENDIENTE
 B-01   | 2026-12-11 | 17:00:00    | CONFIRMADA
 V-01   | 2026-12-12 | 16:00:00    | PENDIENTE
(4 rows)

RESET
== P6 Transaccion con ROLLBACK: el stock vuelve a su valor original
 stock 
-------
    10
(1 row)

BEGIN
UPDATE 1
 stock 
-------
     7
(1 row)

ROLLBACK
 stock 
-------
    10
(1 row)

== P7 Transaccion con COMMIT: reserva + implemento + descuento de stock, todo o nada
BEGIN
INSERT 0 1
INSERT 0 1
UPDATE 1
COMMIT
       nombre        | stock 
---------------------+-------
 Petos (juego de 10) |     3
(1 row)

== P8 Disparador: updated_at cambia al actualizar
 sin_cambios 
-------------
 t
(1 row)

UPDATE 1
 actualizado 
-------------
 t
(1 row)
```

## 10. Sección «Schema migration» de data-model.md (D8)

```markdown
## Schema migration

**Herramienta:** scripts SQL versionados, ejecutados por el contenedor de PostgreSQL al crear el volumen (compatibles con Flyway).
**Ubicación:** `db/migrations/`
**Convención de nombres:** `V<n>__<descripcion_en_snake_case>.sql` (V1 esquema, V2 restricciones, V3 seguridad, V4 datos de prueba).
**Reglas:** una migración aplicada no se modifica; cada cambio nuevo es una migración nueva (`V5__...`).
**Reversión:** en local, `docker compose down -v` y volver a levantar. En un ambiente con datos, una migración nueva que deshace el cambio, previa copia de seguridad (`pg_dump`) y prueba de restauración.
```

---

## 11. Entrega de la prueba de desempeño (en computador y en Moodle)

**Antes del jueves 3 de diciembre** (no habrá internet en la prueba): comprueba que Docker funciona y descarga la imagen con `docker pull postgres:16-alpine`.

Durante la prueba trabajas en una carpeta con estos archivos (el paquete trae el enunciado y el archivo `ejecutar.sh`):

```
G2-desempeno-<variante>/
  01-esquema.sql
  02-restricciones.sql
  03-seguridad.sql
  04-pruebas.sql
  ejecutar.sh        (lo trae el paquete; no lo modifiques)
  salida.txt         (lo genera ejecutar.sh)
```

Comandos (funcionan igual en PowerShell, CMD y Git Bash), desde la carpeta de trabajo:

```
docker run -d --name g2-prueba -e POSTGRES_PASSWORD=prueba -e POSTGRES_DB=prueba postgres:16-alpine
docker cp . g2-prueba:/trabajo
docker exec g2-prueba sh /trabajo/ejecutar.sh
docker cp g2-prueba:/trabajo/salida.txt .
```

Para repetir desde cero después de corregir un script: `docker rm -f g2-prueba` y vuelve a ejecutar los cuatro comandos. Al terminar, comprime la carpeta como `G2-desempeno-<variante>.zip` y súbela a la tarea de Moodle (la plataforma registra quién la sube; no pongas tu nombre en los archivos).
