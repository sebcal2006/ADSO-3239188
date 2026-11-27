# Rúbricas y condiciones de evaluación · Guía 1: Modelo de datos del software (v2)

**Ficha 3239188 · Análisis y Desarrollo de Software · Competencia 220501095 (Modelado de los artefactos del software)**  
**RAP de la guía:** 593101 (02) Estructurar el modelo de datos del software de acuerdo con las especificaciones del análisis. Esta guía no evalúa los RAP 593103, 593100 ni 593102, ni las competencias de inglés e investigación.

Este documento es público y se publica con la guía en el repositorio de la ficha, carpeta `02-training-project/01-phase/02-planning/06-architecture`: lo puedes leer desde el primer día. Los criterios de evaluación están tomados **literalmente** del programa de formación; los niveles están redactados para que se puedan comprobar con el archivo en la mano.

---

## 1. Reglas generales

### 1.1 Los cuatro entregables

| # | Entregable | Peso | Fecha | Forma |
|---|---|---|---|---|
| 1 | Prueba de conocimiento | 25 % | Jueves 3 de diciembre de 2026, en la sesión | Presencial, individual, 40 min, cuestionario de 20 preguntas (10 variantes del banco y 10 inéditas) en Moodle (Zajuna), con calificación automática |
| 2 | Producto 1: modelo conceptual, modelo lógico y normalización | 25 % | Hasta el domingo 6 de diciembre de 2026, 11:59 p. m. | Tu rama `g1/<servicio>-<usuario>` y tu solicitud de integración (pull request) en el repositorio de documentación de tu equipo |
| 3 | Producto 2: diccionario, estándar, motor y seguridad | 25 % | Hasta el domingo 6 de diciembre de 2026, 11:59 p. m. | La misma rama y la misma solicitud de integración |
| 4 | Prueba de desempeño | 25 % | Jueves 3 de diciembre de 2026, en la sesión | Presencial, individual, en computador, 90 min; archivos entregados en una tarea de Moodle (Zajuna) |

**Nota de la guía = promedio de los cuatro entregables. Se aprueba con 70/100 o más.** No hay más entregables ni puntos extra.

- **No hay nota mínima por entregable**: cuenta el promedio. La excepción es la infracción de recursos en una prueba (0 en esa prueba).
- **La escala por saltos (100, 70, 40, 0) es deliberada**: se califica con el archivo en la mano, sin valores intermedios discutibles. Un producto con todos los criterios en nivel 70 obtiene 70, la nota mínima de aprobación.
- **Si el promedio no llega a 70**, el resultado de aprendizaje no se registra como «No aprobado»: queda por evaluar y se acuerda un plan de mejoramiento con fecha, que el instructor comunica por la plataforma de formación.

### 1.2 Cómo se calcula un producto

Cada rúbrica tiene criterios ponderados que suman 100. En cada criterio el trabajo se ubica en uno de cuatro niveles: **100**, **70**, **40** o **0**. La nota del producto es la suma de `peso × nivel / 100`. Después se aplican los topes de las secciones 1.4 y 1.5.

**Regla de resolución (aplica a todas las tablas de niveles):**

1. El nivel 100 exige **todas** las condiciones de su celda. Si no las cumples todas, bajas a 70.
2. En los niveles 70 y 40, las condiciones unidas por «o» son **defectos que ubican el trabajo en ese nivel**: basta uno.
3. Si tienes defectos de dos niveles distintos, **rige el más bajo**. Si no cumples ni una condición del 40, es 0.
4. Los porcentajes se cuentan sobre lo que **debía** existir (por ejemplo, todas las columnas de **todas** tus tablas).

### 1.3 Dónde y cómo se entrega

Trabajas en el **repositorio de documentación de tu equipo** (`code-sena/<abreviatura>-docs`), sembrado con el marco de gobierno de microservicios:

0. **Base común del equipo (sesión del 26 de noviembre).** Un integrante designado publica en la rama de integración, con una solicitud de integración que se fusiona en la misma sesión, el catálogo acordado (`09-microservices/service-catalog.md`), el estándar (`06-data/modeling-conventions.md`) y los archivos compartidos con su estructura vacía (`06-data/G1-README-entrega.md`, `06-data/data-dictionary.md`, `09-microservices/data-ownership-matrix.md`). Así todas las ramas parten de la misma base y nadie crea dos veces el mismo archivo.
1. Creas tu rama, **después** de esa fusión, desde la rama de integración del equipo (`dev` si existe; si no, `main`): `g1/<NN-servicio>-<usuario>`, por ejemplo `g1/03-pedidos-usuario-ejemplo`.
2. Haces commit y push de tus archivos en esa rama, con tu propia cuenta de GitHub.
3. Abres una **solicitud de integración (pull request)** hacia `dev` (o `main`) titulada `G1 593101: <servicio> (<usuario>)`, **antes del corte**.

Archivos de cada aprendiz (contenido individual):

```
09-microservices/services/NN-<servicio>/data-model.md      ← P1 (modelo conceptual y lógico) y P2 (motor, verificación del estándar)
09-microservices/services/NN-<servicio>/normalization.md   ← P1 (normalización)
09-microservices/services/NN-<servicio>/data-security.md   ← P2 (políticas, roles, datos personales)
```

Archivos compartidos del equipo (cada aprendiz escribe **solo su sección o sus filas**, encabezadas con su usuario de GitHub):

```
09-microservices/service-catalog.md        ← catálogo acordado por el equipo (26 de noviembre)
06-data/G1-README-entrega.md               ← README de entrega: tabla de propiedad + sección de cada aprendiz
06-data/models.md                          ← una sección por servicio: motor, responsable y enlace a data-model.md
06-data/data-dictionary.md                 ← una sección por servicio (P2, D1)
06-data/modeling-conventions.md            ← estándar de nombrado y de modelado del equipo
09-microservices/data-ownership-matrix.md  ← filas de las entidades de cada servicio (P2, D6)
```

**Corte:** domingo 6 de diciembre de 2026 a las 11:59 p. m. El instructor toma una copia del repositorio a esa hora y evalúa **la cabeza de tu rama en tu solicitud de integración**, esté o no fusionada. El catálogo y el estándar del equipo se leen en la rama de integración; tus secciones y filas, en tu rama. Si tu rama tiene conflictos con la de un compañero en un archivo compartido, no los resuelves borrando lo de otro: cada uno conserva solo su sección o sus filas. Lo que se suba después o por otro medio (correo, mensajería, USB) no se evalúa. Está prohibido reescribir el historial (`git push --force`) sobre la rama de la entrega y fusionar o modificar las ramas de tus compañeros. Todos los diagramas van en **Mermaid** dentro de los archivos Markdown (GitHub los muestra como diagrama); no se piden imágenes exportadas ni script ejecutado.

### 1.4 Requisitos mínimos de aceptación (RMA) y tope de 60

Cada producto tiene una lista de **artefactos obligatorios** con cantidades mínimas **por aprendiz** (secciones 2.1 y 3.1). **Si falta un artefacto obligatorio, el producto tiene un tope de 60.** Un artefacto cuenta como entregado solo si es tuyo, corresponde a tu servicio y se puede abrir. Quedarse corto en una cantidad mínima de un artefacto que sí entregaste **no activa el tope**: baja el nivel del criterio.

### 1.5 Atribución individual y control de autoría

Los repositorios son de equipo; **el juicio es individual**. Se atribuye a cada aprendiz solo lo que se puede verificar como suyo:

| Control | Qué se revisa | Si no se cumple |
|---|---|---|
| Propiedad registrada | Tu fila en la tabla de propiedad de `06-data/G1-README-entrega.md`: usuario de GitHub, servicio(s) y tablas a tu cargo, rama y número de la solicitud de integración. Debe quedar publicada en tu rama al terminar la sesión del 26 de noviembre (quien no asista a esa sesión la registra a más tardar el viernes 27 de noviembre, en un servicio libre acordado con su equipo) | Sin fila, sin rama y sin solicitud de integración: producto **no entregado** (0). Sin fila pero con rama y solicitud de integración: tope 70 |
| Solicitud de integración | Abierta desde tu rama hacia `dev` (o `main`) antes del corte | Rama publicada sin solicitud de integración: tope 60 |
| Autoría de los commits | Solo cuentan los commits cuyo **autor es tu cuenta** y que modifican **tus archivos** o **tus secciones** de los compartidos. Lo que un compañero escriba en tus archivos no cuenta para ti; lo que tú escribas en archivos de otro servicio no cuenta para ti | Lo no atribuible se tiene por no entregado |
| Días de trabajo | Commits propios con cambios sustantivos en **al menos 2 días distintos** entre el jueves 26 de noviembre y el domingo 6 de diciembre de 2026 (11:59 p. m.), verificados por la fecha de publicación (push). No cuentan espacios, saltos de línea ni renombrados | 1 solo día: tope 70 · ningún día: tope 60 |
| README de entrega | Tu sección individual completa (plantilla Plantilla_README_Entrega_G1): qué reutilizaste y de dónde, qué ajustaste, qué hiciste nuevo, uso de IA declarado y declaración de autoría | Ausente o incompleta: tope 70 |
| Verificación oral de autoría | En la fecha que el instructor comunique por la plataforma de formación, **una pregunta por producto** sobre tus archivos, con tu rama abierta: por qué una tabla quedó así, qué dependencia eliminaste para llegar a 3FN, por qué ese motor, quién puede leer una columna personal. Apruebas si lo explicas con tus palabras, sin leer un texto preparado; si hay duda, se hace una tercera pregunta | Si no explicas **tu propio** producto: ese producto queda con tope 50 |
| Contenido idéntico a otro aprendiz | Tablas, textos o errores iguales o casi iguales a los de otro aprendiz, de tu equipo o de otro equipo, sin declararlo | Tope 40 en el producto de cada uno, **después de una aclaración con derecho a réplica** con tu historial de commits |
| Contenido que no es tuyo | Plantillas del marco de gobierno sin diligenciar (por ejemplo, las tablas `orders` y `order_items`, los campos `[field]` o el texto entre corchetes), los ejemplos de Plantillas_G1, el material del instructor o el contenido escrito por otro aprendiz | Ese artefacto se cuenta como **no entregado** (activa el tope 60) |
| Commits masivos | Un commit que agrega decenas de archivos que no son tuyos (por ejemplo, volver a copiar el marco de gobierno) | No cuenta como aporte propio |

Si se aplican varios topes, **rige el más bajo**. El uso de inteligencia artificial está permitido **solo si lo declaras** (para qué, con qué herramienta y qué cambiaste después); lo que no puedas explicar en la verificación oral cuenta como no propio.

### 1.6 Reparto de servicios y punto de partida

- **Paso de arranque (sesión del 26 de noviembre).** Si tu equipo solo tiene los dos servicios de la plantilla (`01-api-gateway` y `02-auth-service`), primero acuerda el catálogo en `09-microservices/service-catalog.md` a partir de `02-domain`, `04-requirements` y `05-architecture`: número, nombre, responsabilidad, motor previsto y estado de cada servicio.
- **Un dueño por servicio.** Cada integrante es responsable de **al menos un servicio de dominio** con datos relacionales propios; dos aprendices no comparten el mismo servicio. Si tu equipo tiene más integrantes que servicios con datos, el equipo descompone mejor el dominio o asigna a cada aprendiz un **conjunto acotado de tablas** que no se cruce con el de otro, y lo deja escrito en la tabla de propiedad.
- **Servicio pequeño.** Si tu servicio tiene menos de 4 entidades propias, sumas un segundo servicio o un conjunto acotado de tablas hasta cumplir los mínimos, y lo registras. `01-api-gateway` (solo caché) **no sirve** como único servicio; `02-auth-service` sí, si alguien lo toma completo.
- **Conjunto relacional.** El conjunto que se califica debe ser **relacional**: sin tablas relacionales no hay forma de evidenciar la normalización. Si tu servicio usa otro tipo de motor, tomas además un servicio o un conjunto de tablas relacional.
- **Identificadores.** Se acepta el tipo de identificador que tu equipo declare en `06-data/modeling-conventions.md` (UUID, BIGINT u otro), siempre que sea uno solo en todo el equipo y esté justificado.
- **Lo que ya existe.** Si en tu repositorio ya hay contenido en `06-data/models.md` o en la carpeta de tu servicio, cuenta **solo si lo escribiste tú** (se verifica con el historial) y lo declaras en el README; lo escrito por un compañero no cuenta para ti. Lo que exista en otra rama del equipo se trae a tu rama con un commit tuyo que lo declare.

### 1.7 Presupuesto de tiempo (6 horas de trabajo independiente)

| Producto 1 | Min | Producto 2 | Min |
|---|---|---|---|
| M1 modelo conceptual en Mermaid con trazas | 40 | D1 diccionario de tus tablas | 45 |
| M2 modelo lógico, cuadro de reglas e índices | 50 | D2 verificación del estándar | 15 |
| M3 normalización de 2 tablas | 60 | D3 selección del motor | 15 |
| Sección en `06-data/models.md` | 10 | D4 políticas de seguridad | 40 |
| README, rama y solicitud de integración | 20 | D5 matriz de roles y datos personales | 35 |
| | | D6 filas de la matriz de propiedad | 15 |
| | | README | 15 |
| **Total** | **180** | **Total** | **180** |

Haz primero un commit el mismo 26 de noviembre (tu fila de propiedad) y otro a mitad de semana: sirven también para el control de días de trabajo.

---

## 2. Producto 1: modelo conceptual, modelo lógico y normalización (25 %)

### 2.1 Artefactos obligatorios y mínimos por aprendiz

| Artefacto | Dónde | Mínimo exigible |
|---|---|---|
| M1. Modelo conceptual | `data-model.md` de tu servicio | Diagrama Mermaid con ≥ 4 entidades propias con atributos e identificador; ≥ 3 relaciones con cardinalidad mínima y máxima; ≥ 1 relación 1:N y ≥ 1 N:M (si tu servicio no tiene una N:M real, la sustituye un atributo multivaluado resuelto en tabla aparte, declarado); entidades de otros servicios marcadas como referencia externa; tipo de base de datos seleccionado; traza de cada entidad a un requisito o historia de usuario con su identificador |
| M2. Modelo lógico relacional | `data-model.md` de tu servicio | Diagrama Mermaid `erDiagram` con tipos y tablas en el formato del marco (campo, tipo, nulo, descripción, restricciones); ≥ 5 tablas propias contando las intermedias; PK en todas; FK solo entre tablas de tu servicio, con acción referencial; referencias a otros servicios como columna `<entidad>_id` sin FK, con el servicio dueño indicado; campos de auditoría y de borrado lógico; ≥ 2 índices justificados; cuadro de ≥ 4 reglas de transformación aplicadas a tu caso |
| M3. Normalización | `normalization.md` de tu servicio | ≥ 2 tablas de tu propio servicio llevadas paso a paso de 0FN a 1FN, 2FN y 3FN, con las dependencias funcionales escritas y el estado antes y después; una con **llave compuesta** (dependencia parcial) y otra con **dependencia transitiva** |
| Sección en el índice | `06-data/models.md` | `## Servicio: NN-<servicio>` con el motor, tu usuario de GitHub y el enlace a tu `data-model.md` |

Los formatos y un ejemplo pequeño de otro dominio están en **Plantillas_G1.md**.

### 2.2 Rúbrica

| # | Criterio del programa (texto literal) | Aspecto que se observa | Peso |
|---|---|---|---|
| 1 | Genera el modelo conceptual de acuerdo con el tipo de base de datos seleccionada y las especificaciones del análisis. | Modelo conceptual (M1) | 25 |
| 2 | Genera el modelo lógico de acuerdo con la técnica seleccionada. | Modelo lógico relacional y reglas de transformación (M2) | 25 |
| 3 | Genera el modelo lógico de acuerdo con la técnica seleccionada. | Principios de datos por servicio en el modelo lógico (M2 y sección del índice) | 15 |
| 4 | Normaliza el modelo lógico de acuerdo con el tipo de base de datos. | Evidencia de normalización (M3) | 35 |

| Criterio | 100 | 70 | 40 | 0 |
|---|---|---|---|---|
| **1. Modelo conceptual** | ≥ 4 entidades propias con atributos e identificador; ≥ 3 relaciones con cardinalidad mínima y máxima y verbo; ≥ 1 1:N y ≥ 1 N:M (o multivaluado declarado); entidades externas marcadas como referencia; tipo de base de datos declarado y coherente con el servicio; cada entidad traza a un requisito con su ID; el diagrama se muestra en GitHub | 4 entidades con cardinalidad incompleta en 1 relación, o 1 entidad sin traza, o entidades externas sin marcar | 3 entidades, o sin cardinalidades, o entidades de otros servicios modeladas como propias | Ausente, menos de 3 entidades, plantilla sin diligenciar o contenido de otro |
| **2. Modelo lógico** | Todas las entidades transformadas; ≥ 5 tablas; PK en todas; FK internas con acción referencial; cada N:M con tabla intermedia; cuadro de ≥ 4 reglas aplicadas a tus entidades; diagrama `erDiagram` con tipos; ≥ 2 índices justificados por una consulta concreta | 1 o 2 errores (una FK ausente, una N:M sin resolver, un índice sin justificar), o 4 tablas | 3 o más errores, o tablas sin llaves, o sin cuadro de reglas | Ausente |
| **3. Datos por servicio** | Ninguna FK hacia tablas de otro servicio; cada referencia externa como `<entidad>_id` con el servicio dueño y el mecanismo (API o evento); campos de auditoría y borrado lógico en el 100 % de las tablas; identificador según la convención del equipo; sección del índice en `06-data/models.md` | Falta auditoría o borrado lógico en 1 tabla, o una referencia externa sin mecanismo, o falta la sección del índice | Una FK hacia otro servicio, o tablas compartidas con otro servicio, o sin auditoría en la mayoría de las tablas | El modelo es una base compartida entre servicios |
| **4. Normalización** | ≥ 2 tablas propias (una con llave compuesta y una con transitiva) con los pasos 0FN → 1FN → 2FN → 3FN, dependencias funcionales escritas y estado antes y después; el modelo lógico final coincide con el resultado; toda desnormalización está justificada | Solo 1 tabla con los tres pasos, o pasos sin dependencias funcionales, o ninguna tabla con llave compuesta | Afirma «está en 3FN» sin evidencia, o solo aplica 1FN, o normaliza tablas que no son de su servicio | Ausente |

**Sobre el criterio 3.** El programa no trae un criterio específico para la arquitectura de datos por servicio. Se usa la oración literal más cercana (el modelo lógico de acuerdo con la técnica seleccionada: base de datos por servicio) y se declara como **evidencia derivada**: se observa cómo tu modelo lógico aplica la técnica, no una competencia nueva.

---

## 3. Producto 2: diccionario, estándar, motor y seguridad (25 %)

### 3.1 Artefactos obligatorios y mínimos por aprendiz

| Artefacto | Dónde | Mínimo exigible |
|---|---|---|
| D1. Diccionario de datos | `06-data/data-dictionary.md`, sección `## Servicio: NN-<servicio> (@usuario)` | 100 % de las tablas y columnas de tu servicio: tabla, columna, tipo, tamaño o precisión, nulo, restricciones, dominio o valores permitidos, descripción y marca de dato personal (sí/no) |
| D2. Estándar de nombrado y modelado | `06-data/modeling-conventions.md` (del equipo) y tu `data-model.md` | El equipo declara ≥ 6 reglas (tablas, columnas, FK, índices, tipo de identificador, fechas, borrado lógico, auditoría); tú verificas ≥ 6 reglas sobre **todas** tus tablas, con resultado y corrección |
| D3. Selección del motor | `data-model.md` de tu servicio | Motor y versión; ≥ 3 condiciones concretas de tu servicio que lo justifican; 1 alternativa descartada con su razón |
| D4. Políticas de seguridad | `data-security.md` de tu servicio | ≥ 6 políticas: ≥ 2 de integridad, ≥ 2 de confidencialidad y ≥ 2 de disponibilidad, cada una con una medida concreta sobre tus tablas o columnas; credenciales con **hash y sal** (no «cifradas») si tu servicio las guarda; tráfico por TLS; respaldo con frecuencia y prueba de restauración |
| D5. Roles y datos personales | `data-security.md` de tu servicio | Matriz de ≥ 3 roles contra el 100 % de tus tablas con los permisos de cada rol; tratamiento de los datos personales de tu servicio: columna, finalidad, autorización, conservación, quién accede y medida de protección |
| D6. Propiedad de los datos | `09-microservices/data-ownership-matrix.md` | Una fila por cada entidad de tu servicio: servicio dueño, quién guarda copia y cómo se sincroniza |

### 3.2 Rúbrica

| # | Criterio del programa (texto literal) | Aspecto que se observa | Peso |
|---|---|---|---|
| 1 | Crea el diccionario de datos de acuerdo con el modelo lógico. | Diccionario de datos (D1) | 25 |
| 2 | Crea el diccionario de datos de acuerdo con el modelo lógico. | Estándar de nombrado y modelado verificado (D2) | 10 |
| 3 | Genera el modelo conceptual de acuerdo con el tipo de base de datos seleccionada y las especificaciones del análisis. | Selección del motor (D3) | 10 |
| 4 | Define políticas de seguridad para garantizar integridad, confidencialidad y disponibilidad de los datos. | Políticas por principio (D4) | 25 |
| 5 | Define políticas de seguridad para garantizar integridad, confidencialidad y disponibilidad de los datos. | Matriz de roles y tratamiento de datos personales (D5) | 20 |
| 6 | Define políticas de seguridad para garantizar integridad, confidencialidad y disponibilidad de los datos. | Propiedad de los datos (D6) | 10 |

| Criterio | 100 | 70 | 40 | 0 |
|---|---|---|---|---|
| **1. Diccionario** | 100 % de las columnas de tus tablas con los nueve campos; coincide al 100 % con tu modelo lógico (mismos nombres, tipos y restricciones) | ≥ 80 % de las columnas completas, o hasta 3 diferencias con el modelo lógico | ≥ 50 % de las columnas, o sin dominio | < 50 % o ausente |
| **2. Estándar** | ≥ 6 reglas del estándar del equipo verificadas sobre todas tus tablas; ningún incumplimiento sin corregir | 4 o 5 reglas verificadas, o 1 o 2 incumplimientos sin corregir | < 4 reglas verificadas | Ausente |

Si al corte la rama de integración no tiene `06-data/modeling-conventions.md` con ≥ 6 reglas, cada aprendiz verifica sus tablas contra las convenciones de `06-data/models.md` del marco (sección «Naming conventions» y campos de auditoría) y lo declara; la falta del equipo no se descuenta a quien sí verificó.
| **3. Motor** | Motor y versión; ≥ 3 condiciones concretas del servicio (estructura de los datos, transacciones, patrón de consulta, volumen); 1 alternativa descartada con razón; coherente con `05-architecture` y con la guía de motores de `06-data/models.md` | 1 o 2 condiciones, o sin alternativa descartada | Motor nombrado con justificación genérica | Ausente |
| **4. Políticas** | ≥ 2 por principio (≥ 6), cada una con medida concreta sobre tus tablas o columnas (qué `CHECK`, qué columna se cifra, qué frecuencia de respaldo); hash y sal en credenciales si aplica; TLS; respaldo con frecuencia y prueba de restauración | ≥ 1 por principio con medida concreta, o falta respaldo o prueba de restauración | Políticas genéricas copiadas de una definición, sin vínculo con tus tablas | Ausente |
| **5. Roles y datos personales** | ≥ 3 roles contra el 100 % de tus tablas con permisos (`SELECT`, `INSERT`, `UPDATE`, borrado lógico); mínimo privilegio; usuario de la aplicación distinto del de migraciones; cada columna personal con finalidad, autorización, conservación, quién accede y medida, de acuerdo con la normativa colombiana de protección de datos personales | Matriz completa y datos personales parciales, o falta 1 tabla en la matriz | < 3 roles, o sin tratamiento de datos personales | Ausente |
| **6. Propiedad** | Una fila por cada entidad de tu servicio; un solo dueño por entidad, sin choque con las filas de tus compañeros; copias y mecanismo de sincronización coherentes con tu `data-model.md` | Falta 1 entidad o 1 mecanismo | Entidades con dos dueños, o filas sin mecanismo | Ausente |

**Sobre los criterios 2, 3 y 6.** Son evidencia derivada de oraciones literales del programa: el estándar de nombrado forma parte del diccionario; la selección del motor es «el tipo de base de datos seleccionada»; la propiedad única de cada dato es una política de integridad. No se califica dos veces el mismo hecho.

---

## 4. Prueba de desempeño (25 %)

**Qué es.** El jueves 3 de diciembre de 2026, en la sesión, de forma presencial e individual y **en computador**, recibes como archivos digitales el extracto del análisis de un caso que no conoces, una tabla plana no normalizada con datos de ejemplo y los dos servicios en que se divide el caso. Hay dos versiones del caso, repartidas por turno. Tienes **90 minutos**.

**Qué entregas (los cinco archivos son obligatorios):**

1. `01-propiedad-y-conceptual.md`: qué dato pertenece a qué servicio y el modelo conceptual de cada servicio (Mermaid o tabla de entidades y relaciones con cardinalidad).
2. `02-normalizacion.md`: la tabla llevada de 0FN a 3FN con las dependencias funcionales escritas.
3. `03-modelo-logico.md` (o `.sql`): las tablas de cada servicio con PK, FK internas, tipos y referencias externas sin FK.
4. `04-diccionario.md`: el diccionario completo de la tabla que indique el enunciado.
5. `05-seguridad.md`: una política por cada principio (integridad, confidencialidad y disponibilidad) y la matriz de roles de la tabla con datos personales que indique el enunciado.

**Cómo entregas.** Al terminar subes **un solo archivo** `G1-desempeno-<variante>.zip` a la tarea de Moodle de la prueba. Moodle registra quién lo sube; no escribas tu nombre en los archivos. Lo que no esté en la tarea al cierre no se evalúa.

**Recursos permitidos:** computador con editor de texto (con vista de Markdown), ofimática y, si quieres, un motor SQL; apuntes digitales, esta guía, el banco de preguntas y Plantillas_G1.md sin conexión. Solo se permite la conexión a Moodle para descargar el paquete y subir el archivo. No se permite otra navegación, mensajería, asistentes de IA, abrir el repositorio de tu equipo ni ayuda de otras personas. Una infracción anula la prueba (0).

**Tope:** si falta uno de los cinco archivos, la prueba tiene tope de 60.

| # | Criterio del programa (texto literal) | Aspecto que se observa | Peso |
|---|---|---|---|
| 1 | Genera el modelo conceptual de acuerdo con el tipo de base de datos seleccionada y las especificaciones del análisis. | Propiedad de los datos y modelo conceptual de los dos servicios | 15 |
| 2 | Genera el modelo lógico de acuerdo con la técnica seleccionada. | Modelo lógico de los dos servicios | 20 |
| 3 | Normaliza el modelo lógico de acuerdo con el tipo de base de datos. | Normalización con dependencias funcionales | 30 |
| 4 | Crea el diccionario de datos de acuerdo con el modelo lógico. | Diccionario de la tabla indicada | 15 |
| 5 | Define políticas de seguridad para garantizar integridad, confidencialidad y disponibilidad de los datos. | Políticas y matriz de roles | 20 |

| Criterio | 100 | 70 | 40 | 0 |
|---|---|---|---|---|
| **1. Propiedad y conceptual** | Cada dato asignado a un único servicio dueño, de acuerdo con el análisis; entidades con identificador y relaciones con cardinalidad mínima y máxima; las relaciones entre servicios se marcan como referencia externa | 1 o 2 datos mal asignados, o cardinalidades incompletas | 3 o más datos mal asignados, o sin cardinalidades | No entrega |
| **2. Modelo lógico** | Todas las tablas de los dos servicios con PK, tipos correctos, FK internas, tablas intermedias donde corresponde y **ninguna FK entre servicios** (referencia por identificador) | 1 error de llaves o de tipos, o una referencia externa con FK | 2 o 3 errores, o tablas sin llaves | No entrega o más de 3 errores |
| **3. Normalización** | Identifica todas las violaciones de 1FN, 2FN y 3FN de la tabla; escribe las dependencias funcionales; el resultado queda en 3FN | Identifica dos de las tres categorías, o el resultado tiene una dependencia sin resolver | Identifica una categoría | No normaliza |
| **4. Diccionario** | 100 % de las columnas de la tabla indicada con tipo, tamaño, nulo, restricciones, dominio y marca de dato personal; coincide con el modelo lógico; corrige los tipos inadecuados de la tabla original | ≥ 80 % de las columnas completas, o 1 tipo inadecuado sin corregir | ≥ 50 % de las columnas, o sin dominio | < 50 % o no entrega |
| **5. Seguridad** | Una política concreta por cada principio sobre las tablas del caso; credenciales con hash y sal; matriz de ≥ 3 roles con mínimo privilegio sobre la tabla indicada; columnas personales identificadas con su medida | Falta un principio, o la matriz no aplica mínimo privilegio | Políticas genéricas sin relación con el caso | No entrega |

El instructor califica con una **solución de referencia privada** de cada versión. Si encuentras otra solución válida y la justificas, se acepta.

---

## 5. Prueba de conocimiento (25 %)

Cuestionario en **Moodle (Zajuna)**, presencial, con **calificación automática**: la nota sobre 100 es la nota de la evidencia de conocimiento. 20 preguntas de selección múltiple con única respuesta, 5 puntos cada una, 40 minutos, sin recursos. **10 son variantes** de preguntas del banco (el mismo concepto con otros datos o con otro caso) y **10 son inéditas**. El examen y su clave no se publican; el banco público (Banco_Preguntas_G1.md, 40 preguntas) es un documento de estudio sin respuestas.

| Criterio del programa (593101) | Preguntas del examen (aprox.) | Temas |
|---|---|---|
| Genera el modelo conceptual de acuerdo con el tipo de base de datos seleccionada y las especificaciones del análisis. | 4 | Tipos de bases de datos y motores, entidades, cardinalidad, big data |
| Genera el modelo lógico de acuerdo con la técnica seleccionada. | 6 | Reglas de transformación, restricciones, notación, datos por servicio |
| Normaliza el modelo lógico de acuerdo con el tipo de base de datos. | 4 | 1FN, 2FN, 3FN, dependencias funcionales, desnormalización |
| Crea el diccionario de datos de acuerdo con el modelo lógico. | 2 | Tipos, tamaños, dominio, estándar de nombrado |
| Define políticas de seguridad para garantizar integridad, confidencialidad y disponibilidad de los datos. | 4 | Principios, hash y sal, cifrado, niveles de acceso, datos personales, respaldo |

---

## 6. Resumen de topes

| Situación | Tope |
|---|---|
| Sin fila de propiedad, sin rama y sin solicitud de integración | 0 (no entregado) |
| Falta un artefacto obligatorio (por producto) | 60 |
| Rama publicada sin solicitud de integración al corte | 60 |
| Ningún día con commits sustantivos propios en el periodo | 60 |
| Commits sustantivos en un solo día del periodo | 70 |
| README individual ausente o incompleto, o sin fila de propiedad | 70 |
| No explicas tu propio producto en la verificación oral | 50 (ese producto) |
| Contenido idéntico a otro aprendiz sin declarar (tras la aclaración con réplica) | 40 |
| Falta uno de los cinco archivos de la prueba de desempeño | 60 |
| Infracción de los recursos en una prueba | 0 en esa prueba |
