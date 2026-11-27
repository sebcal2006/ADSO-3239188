# README de entrega · Guía 1: Modelo de datos del software

> Este archivo se copia **una sola vez por equipo** como `06-data/G1-README-entrega.md` en el repositorio de documentación del equipo: lo crea, con la tabla vacía, el integrante designado como parte de la base común que se fusiona en la rama de integración el 26 de noviembre, antes de que los demás creen sus ramas. La tabla de la sección 2 tiene **una fila por aprendiz**, y la sección 4 tiene **una subsección por aprendiz**. Cada aprendiz edita **solo su fila y su subsección**, desde su propia rama `g1/<NN-servicio>-<usuario>`. Borra las instrucciones entre `>` cuando lo llenes.
>
> Una fila de propiedad o una subsección ausente o incompleta limita la nota a 70 (Rubricas_G1.md, sección 1.5). Los formatos de cada artefacto están en **Plantillas_G1.md**.

> No escribas nombres completos, números de documento, teléfonos ni correos. Identifícate **solo con tu usuario de GitHub**.

## 1. Datos del equipo

| Campo | Valor |
|---|---|
| Ficha | 3239188 |
| Repositorio | `code-sena/<abreviatura>-docs` |
| Proyecto | |
| Rama de integración (destino de las solicitudes de integración) | `dev` / `main` (deja una) |
| Catálogo de servicios acordado | `09-microservices/service-catalog.md` (fecha del commit del acuerdo: ) |
| Estándar de nombrado y modelado del equipo | `06-data/modeling-conventions.md` |
| Tipo de identificador del equipo | UUID / BIGINT / otro (deja uno y justifícalo en `modeling-conventions.md`) |

## 2. Tabla de propiedad (una fila por aprendiz, registrada el 26 de noviembre)

> Cada servicio o conjunto de tablas tiene **un solo dueño**. `01-api-gateway` no sirve como único servicio. Si tu servicio tiene menos de 4 entidades propias, agrega un segundo servicio o un conjunto acotado de tablas.

| Usuario de GitHub | Servicio(s) a cargo | Tablas a cargo | Motor | Rama | Solicitud de integración |
|---|---|---|---|---|---|
| `usuario-ejemplo` | `03-pedidos` | `pedidos`, `items_pedido`, `estados_pedido`, `direcciones_entrega`, `pedidos_promociones` | PostgreSQL | `g1/03-pedidos-usuario-ejemplo` | #12 |
| | | | | | |
| | | | | | |

## 3. Archivos compartidos

| Archivo | Qué escribe cada aprendiz |
|---|---|
| `09-microservices/service-catalog.md` | El equipo acuerda el catálogo; cada aprendiz completa la ficha de su servicio |
| `06-data/models.md` | `## Servicio: NN-<servicio>` con el motor, el usuario responsable y el enlace a su `data-model.md` |
| `06-data/data-dictionary.md` | `## Servicio: NN-<servicio> (@usuario)` con el diccionario de sus tablas |
| `06-data/modeling-conventions.md` | El equipo declara ≥ 6 reglas; cada aprendiz las verifica en su `data-model.md` |
| `09-microservices/data-ownership-matrix.md` | Las filas de las entidades de su servicio, con su usuario en la última columna |

## 4. Sección individual de cada aprendiz

> Copia este bloque una vez por aprendiz y diligéncialo.

### Aprendiz `@usuario`

**Servicio(s):** `NN-<servicio>` · **Rama:** `g1/NN-<servicio>-<usuario>` · **Solicitud de integración:** #

#### 4.1 Archivos de mi entrega

| Artefacto | Archivo | Origen («nuevo» o commit mío anterior, con su enlace) | Qué ajusté o agregué |
|---|---|---|---|
| M1 Modelo conceptual | `09-microservices/services/NN-<servicio>/data-model.md` | | |
| M2 Modelo lógico y cuadro de reglas | `09-microservices/services/NN-<servicio>/data-model.md` | | |
| M3 Normalización | `09-microservices/services/NN-<servicio>/normalization.md` | | |
| Sección del índice | `06-data/models.md` | | |
| D1 Diccionario | `06-data/data-dictionary.md` | | |
| D2 Verificación del estándar | `09-microservices/services/NN-<servicio>/data-model.md` | | |
| D3 Motor | `09-microservices/services/NN-<servicio>/data-model.md` | | |
| D4 Políticas | `09-microservices/services/NN-<servicio>/data-security.md` | | |
| D5 Roles y datos personales | `09-microservices/services/NN-<servicio>/data-security.md` | | |
| D6 Propiedad | `09-microservices/data-ownership-matrix.md` | | |

> Solo puedes declarar como origen un contenido que **tú** escribiste antes (se verifica con el historial). Lo que escribió un compañero, las plantillas del marco sin diligenciar y los ejemplos de Plantillas_G1 no cuentan como tuyos.

**Qué reutilicé (2 a 4 líneas):**

**Qué ajusté para llegar al estándar de la rúbrica (2 a 4 líneas):**

**Qué hice nuevo (2 a 4 líneas):**

#### 4.2 Autoverificación de mínimos

> Marca con `x` solo lo que de verdad cumples. El instructor lo contrasta con los archivos.

Producto 1:
- [ ] M1 ≥ 4 entidades propias, ≥ 3 relaciones con cardinalidad mínima y máxima, ≥ 1 1:N, ≥ 1 N:M (o multivaluado declarado), externas marcadas, traza a requisitos
- [ ] M2 ≥ 5 tablas con PK; FK solo internas; referencias externas sin FK; auditoría y borrado lógico; ≥ 2 índices; cuadro de ≥ 4 reglas; `erDiagram` con tipos
- [ ] M3 ≥ 2 tablas de 0FN a 3FN con dependencias funcionales (una con llave compuesta y una con transitiva)
- [ ] Sección de mi servicio en `06-data/models.md`

Producto 2:
- [ ] D1 diccionario del 100 % de mis columnas, idéntico a mi modelo lógico
- [ ] D2 ≥ 6 reglas del estándar verificadas sobre todas mis tablas
- [ ] D3 motor con ≥ 3 condiciones y 1 alternativa descartada
- [ ] D4 ≥ 6 políticas (2 por principio), con hash y sal, TLS, respaldo y prueba de restauración
- [ ] D5 matriz de ≥ 3 roles contra todas mis tablas y tratamiento de datos personales
- [ ] D6 filas de mis entidades en la matriz de propiedad

#### 4.3 Días de trabajo

> Al menos **2 días distintos** con commits propios sustantivos entre el jueves 26 de noviembre y el domingo 6 de diciembre de 2026 (11:59 p. m.).

| Día | Qué avancé (mensaje del commit) |
|---|---|
| | |
| | |

#### 4.4 Uso de inteligencia artificial (obligatorio)

> Si no usaste IA, escribe «No usé IA». Si la usaste, di para qué, con qué herramienta y qué verificaste o cambiaste después. Lo que no puedas explicar en la verificación oral cuenta como no propio.

| Herramienta | Para qué la usé | Qué verifiqué o cambié después |
|---|---|---|
| | | |

#### 4.5 Declaración de autoría

Declaro que el contenido de mis archivos y de mis secciones es de mi autoría, que lo que reutilicé está indicado en 4.1, que no entregué como propio material del instructor, plantillas sin diligenciar ni contenido de otros aprendices, y que puedo explicar cada artefacto en la verificación oral.

Usuario de GitHub: ______________________  Fecha: ______________
