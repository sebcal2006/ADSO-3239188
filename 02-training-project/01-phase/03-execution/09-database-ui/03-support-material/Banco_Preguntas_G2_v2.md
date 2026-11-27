# Banco de preguntas · Guía 2: Planeación de la construcción y base de datos (v2)

**Ficha 3239188 · Análisis y Desarrollo de Software · Competencia 220501096 (Construcción del software)**  
**Fase Ejecución · RAP 593106 (actividad: Codificar los módulos del software, con base en los estándares del mercado) y RAP 593107 (actividad: Desarrollar la estructura de datos y la interfaz de usuario del software)**

## Cómo se usa este banco

- Son **60 preguntas de selección múltiple** (opciones A, B, C y D, una sola respuesta correcta): **15 básicas, 25 intermedias y 20 avanzadas**, con la etiqueta del resultado de aprendizaje (RAP) y del nivel. Más de 20 se plantean como caso.
- Reparto por RAP: **30 de planeación de la construcción (RAP 593106)** y **30 de construcción de la base de datos (RAP 593107)**.
- **Este archivo no trae las respuestas.** Es para estudiar: resuelve cada pregunta, justifica por qué descartas las otras tres opciones y compruébalo en tu contenedor cuando la pregunta sea de SQL. Las opciones tienen longitud parecida a propósito: no se acierta por el tamaño del texto ni por la posición de la letra.
- **La prueba de conocimiento** (jueves **3 de diciembre de 2026**, presencial e individual, 40 minutos, **cuestionario en la plataforma Moodle (Zajuna)** con calificación automática) tiene **20 preguntas: 10 de cada RAP**. De ellas, **10 son variantes** de preguntas de este banco (el mismo concepto con otro caso, otros datos u otra redacción) y **10 son inéditas**. Memorizar la letra o el texto no sirve; hay que entender el porqué.
- La prueba pesa el **25 %** de la guía, y los aciertos de cada RAP cuentan por separado en la nota de ese resultado (Rubricas_G2.md, sección 1.2).

## Fechas

| Evidencia | Fecha |
|---|---|
| Prueba de conocimiento (Moodle) y prueba de desempeño (en computador, con PostgreSQL en contenedor) | Jueves 3 de diciembre de 2026 (presencial) |
| Producto 1 (plan de construcción) y Producto 2 (base de datos construida) | Hasta el domingo 6 de diciembre de 2026, 11:59 p. m. |

Las condiciones de cada producto, los mínimos y las rúbricas están en **Rubricas_G2.md**; los formatos y el ejemplo completo, en **Plantillas_G2.md**.

---

## Parte 1. Planeación de la construcción del software (RAP 593106: Planear actividades de construcción del software de acuerdo con el diseño establecido)

**1.** ¿Qué contiene el informe de diseño que se usa como entrada para planear la construcción de un servicio? *(RAP 593106 · Básica)*

- A) Los artefactos de diseño y sus decisiones: responsabilidades, modelo de datos, contratos y eventos.
- B) Los requisitos tal como los redactó el cliente, sin ningún análisis ni decisión técnica.
- C) El código fuente de los módulos ya construidos, con sus pruebas unitarias y de integración.
- D) El acta de inicio del proyecto, con el presupuesto, el cronograma general, los interesados y los riesgos.


**2.** En un plan de trabajo, ¿para qué sirve el criterio de terminado de cada tarea? *(RAP 593106 · Básica)*

- A) Para registrar cuántas horas se estimó que tomaría la tarea completa.
- B) Para señalar cuál tarea del plan debe hacerse antes que ella.
- C) Para asignar la tarea a la persona con más experiencia del equipo.
- D) Para comprobar de forma verificable cuándo la tarea está completa.


**3.** ¿Qué es Git? *(RAP 593106 · Básica)*

- A) Un servicio en la nube para alojar repositorios y revisar el código de un equipo.
- B) Un sistema de control de versiones distribuido que registra el historial de cambios.
- C) Un motor de integración continua que ejecuta pruebas automáticas en cada cambio.
- D) Un gestor de paquetes que descarga las dependencias que necesita el proyecto.


**4.** ¿Por qué el archivo `.env` de un servicio no se sube al repositorio? *(RAP 593106 · Básica)*

- A) Porque Git no puede versionar archivos cuyo nombre empieza con un punto.
- B) Porque Docker Compose lo genera solo cada vez que se levanta el contenedor.
- C) Porque ocupa demasiado espacio y vuelve muy lenta la clonación del repositorio.
- D) Porque contiene valores sensibles, como contraseñas, propios de cada entorno.


**5.** Según la convención más común de los lenguajes orientados a objetos, ¿cómo se nombra una clase? *(RAP 593106 · Básica)*

- A) En snake_case y con un verbo, por ejemplo `crear_factura_service`.
- B) En mayúsculas con guion bajo, por ejemplo `FACTURA_SERVICE`.
- C) En camelCase y con un verbo, por ejemplo `crearFacturaService`.
- D) En PascalCase y con un sustantivo, por ejemplo `FacturaService`.


**6.** ¿Qué es una solicitud de cambio (pull request)? *(RAP 593106 · Básica)*

- A) Una petición para revisar e integrar los cambios de una rama en otra.
- B) Una copia completa del repositorio, con todo su historial, en la cuenta de otra persona.
- C) Una etiqueta que marca una versión publicada del software.
- D) Un comando que trae los cambios remotos a la rama local actual.


**7.** ¿Qué hace Docker Compose en el entorno de desarrollo de un servicio? *(RAP 593106 · Básica)*

- A) Define en un archivo los contenedores del entorno y los levanta con un comando.
- B) Compila el código fuente del servicio y genera su archivo ejecutable final.
- C) Publica la imagen del servicio en un registro público para que otros la usen.
- D) Reemplaza a la base de datos real durante las pruebas automáticas del servicio.


**8.** ¿Qué es la integración continua? *(RAP 593106 · Básica)*

- A) Desplegar cada cambio directamente en producción, sin ninguna revisión ni prueba previa.
- B) Integrar cambios con frecuencia y verificar cada uno con compilación y pruebas automáticas.
- C) Fusionar todas las ramas del equipo una sola vez, al final del proyecto, en una única entrega.
- D) Mantener dos versiones completas del sistema funcionando en paralelo durante todo el año.


**9.** Un plan tiene estas tareas de base de datos: T1 crear las tablas (V1), T2 crear los roles y permisos (V3), T3 crear las restricciones e índices (V2) y T4 cargar los datos de prueba (V4). ¿En qué orden deben ejecutarse? *(RAP 593106 · Intermedia · Caso)*

- A) T2, T1, T3 y T4: primero los permisos, para que nadie toque las tablas al crearlas.
- B) T4, T1, T3 y T2: primero los datos, para probar las tablas apenas existan.
- C) T1, T4, T3 y T2: los datos antes de las restricciones, para que no fallen.
- D) T1, T3, T2 y T4: tablas, restricciones, permisos y al final los datos de prueba.


**10.** ¿Qué práctica mejora la estimación de una tarea grande del plan de construcción? *(RAP 593106 · Intermedia)*

- A) Dividirla en tareas pequeñas y estimar cada una por separado.
- B) Estimarla una sola vez al final, cuando ya se terminó la tarea.
- C) Usar la misma cantidad de horas para todas las tareas del plan.
- D) Pedir que la estime una persona que no va a hacer la tarea.


**11.** El contrato de API de un servicio define `GET /pedidos?estado=` como la consulta más usada. ¿Qué tarea de base de datos se desprende de ese elemento del diseño? *(RAP 593106 · Intermedia · Caso)*

- A) Crear una tabla nueva llamada `estado` con una fila por cada pedido.
- B) Conceder permiso DELETE sobre pedidos al rol de solo lectura.
- C) Crear un índice sobre la columna `estado` de la tabla de pedidos.
- D) Quitar el CHECK de `estado` para aceptar cualquier valor en el filtro.


**12.** Un equipo debe justificar el lenguaje de su servicio. ¿Cuál de estas razones es una condición del software o del equipo que sí justifica la selección? *(RAP 593106 · Intermedia · Caso)*

- A) Es el lenguaje que aparece primero en la lista de guías de la carpeta `_stacks`.
- B) Es el lenguaje con el logotipo más reconocido entre los aprendices de la ficha.
- C) El equipo ya domina el lenguaje y existe una guía del stack con su estructura de carpetas.
- D) Es el lenguaje que usó otro equipo de la ficha, así se pueden copiar sus archivos sin ningún cambio.


**13.** ¿Por qué en `docker-compose.yml` se fija la versión de la imagen (por ejemplo, `postgres:16-alpine`) en lugar de usar `latest`? *(RAP 593106 · Intermedia)*

- A) Porque la etiqueta `latest` no existe en el registro oficial de imágenes.
- B) Porque las imágenes con versión fijada se descargan sin conexión a internet.
- C) Porque `latest` solo funciona en servidores y no en computadores personales.
- D) Para que todos los integrantes y ambientes usen exactamente la misma versión.


**14.** ¿Cuál de estos mensajes cumple el formato de commits convencionales? *(RAP 593106 · Intermedia)*

- A) `Agregué la validación del monto minimo en pagos`
- B) `FEAT: PAGOS VALIDACION DE MONTO MINIMO.`
- C) `feat(pagos): agregar validacion de monto minimo`
- D) `pagos(feat) agregar validacion de monto minimo`


**15.** En un equipo, un integrante hace commits directos en `dev` y varias veces ha roto el trabajo de los demás. ¿Qué configuración de versionamiento lo evita? *(RAP 593106 · Intermedia · Caso)*

- A) Borrar la rama `dev` y trabajar todos directamente sobre la rama `main`.
- B) Pedir que cada integrante trabaje en un repositorio aparte, sin integrar nunca su trabajo.
- C) Hacer `git push --force` sobre `dev` cada vez que algo deje de funcionar.
- D) Proteger `dev` para que solo reciba cambios por solicitud de cambio revisada.


**16.** ¿Qué archivo evita que `.env` y las carpetas de dependencias se suban al repositorio? *(RAP 593106 · Intermedia)*

- A) `.env.example`, porque reemplaza al archivo que trae los valores reales.
- B) `.gitignore`, con las rutas o patrones que Git debe ignorar.
- C) `docker-compose.yml`, porque declara los archivos que usa el contenedor.
- D) `.editorconfig`, porque define cómo se guarda cada archivo del proyecto.


**17.** El estándar del equipo dice: tablas en snake_case y en singular, y llaves foráneas como `<tabla>_id`. ¿Cuál instrucción lo cumple? *(RAP 593106 · Intermedia · Caso)*

- A) `CREATE TABLE detalle_pedido (pedido_id UUID NOT NULL, ...)`
- B) `CREATE TABLE DetallePedidos (IdPedido UUID NOT NULL, ...)`
- C) `CREATE TABLE tbl_detalle (pedido UUID NOT NULL, ...)`
- D) `CREATE TABLE detalles_pedidos (pedidoId UUID NOT NULL, ...)`


**18.** Según un estándar de codificación, ¿qué debe incluir la documentación de una función pública? *(RAP 593106 · Intermedia)*

- A) Qué hace, sus parámetros, lo que retorna y los errores que puede lanzar.
- B) El nombre de quien la escribió y la fecha de cada una de sus modificaciones.
- C) Una copia del código de la función explicado línea por línea en español.
- D) Solo el nombre de la función repetido en una frase corta al comienzo.


**19.** ¿Por qué un estándar de codificación fija la indentación, por ejemplo 4 espacios y sin tabuladores? *(RAP 593106 · Intermedia)*

- A) Porque el compilador de todos los lenguajes de programación rechaza los tabuladores.
- B) Porque así el programa se ejecuta más rápido cuando se despliega en producción.
- C) Para que el código se lea igual en todo editor y los cambios no sean solo de formato.
- D) Porque Git no puede guardar en su historial los archivos que tienen tabuladores.


**20.** Tareas: T1 configurar compose (1 h); T2 escribir V1 (2 h, depende de T1); T3 escribir V2 (2 h, depende de T2); T4 escribir el estándar (1 h, sin dependencias); T5 escribir V3 (1 h, depende de T3). Si las tareas sin dependencia pueden hacerse en paralelo, ¿cuál es la duración mínima? *(RAP 593106 · Intermedia · Caso)*

- A) 6 horas, por la ruta T1, T2, T3 y T5.
- B) 7 horas, la suma de todas las tareas del plan.
- C) 2 horas, la duración de la tarea más larga.
- D) 5 horas, por la ruta T4, T2, T3 y T5.


**21.** Un aprendiz abre una sola solicitud de cambio de 2 000 líneas que mezcla el compose, el estándar, las migraciones y código de la API. La política del equipo pide máximo 400 líneas y una tarea por rama. ¿Qué corresponde? *(RAP 593106 · Avanzada · Caso)*

- A) Aprobarla sin revisar, porque revisar tantas líneas de una sola vez tomaría demasiado tiempo.
- B) Comprimir los archivos en un .zip para que cuente como un solo cambio pequeño.
- C) Hacer squash de todos los commits para que parezca un cambio de pocas líneas.
- D) Dividirla en solicitudes de cambio más pequeñas, una por tarea, revisadas por separado.


**22.** ¿Qué verificación automática en la integración continua protege mejor la construcción de la base de datos de un servicio? *(RAP 593106 · Avanzada)*

- A) Revisar que los nombres de los archivos de migración estén escritos en minúscula.
- B) Contar las líneas de cada migración y rechazar las que superen las cien líneas.
- C) Levantar un contenedor limpio y ejecutar todas las migraciones en cada solicitud de cambio.
- D) Ejecutar solo la última migración, directamente sobre la base de datos de producción, cada viernes.


**23.** Un aprendiz subió por error el archivo `.env` con la contraseña de la base de datos a la rama compartida del equipo. ¿Qué es lo correcto? *(RAP 593106 · Avanzada · Caso)*

- A) Borrar el archivo en un commit nuevo; así la contraseña sale por completo del historial del repositorio.
- B) Renombrar el archivo a `.env.old` para que nadie lo reconozca después.
- C) Volver privado el repositorio durante un día y luego dejarlo como estaba.
- D) Cambiar la contraseña expuesta, agregar `.env` a `.gitignore` y retirar el archivo.


**24.** La guía de instalación local de un equipo dice solo «instalar PostgreSQL», sin versión. Las migraciones funcionan en tres equipos y fallan en el cuarto. ¿Qué configuración ataca la causa? *(RAP 593106 · Avanzada · Caso)*

- A) Pedir a quien tiene el fallo que reinstale el sistema operativo de su equipo.
- B) Quitar de las migraciones las instrucciones que fallan solo en ese equipo y dejar las demás iguales.
- C) Un `docker-compose.yml` con la imagen y la versión fijadas, usado por todo el equipo.
- D) Ejecutar las migraciones solo en uno de los computadores que no fallan.


**25.** Un equipo con stack Java escribe en su estándar: «los métodos van en snake_case, porque las tablas van en snake_case». ¿Qué está mal? *(RAP 593106 · Avanzada · Caso)*

- A) Nada: usar snake_case en todo el proyecto, incluidos los métodos, es obligatorio en el lenguaje Java.
- B) Las tablas también deberían ir en camelCase para coincidir con los métodos.
- C) Los métodos deberían ir en mayúsculas para distinguirlos bien de las tablas.
- D) Mezcla reglas: los métodos siguen la convención de Java y las tablas la de la base.


**26.** Un plan tenía 10 tareas de 1 hora cada una. Después de terminar 3 tareas, el aprendiz lleva 6 horas. ¿Cuál es la mejor decisión? *(RAP 593106 · Avanzada · Caso)*

- A) Mantener el plan sin cambios, porque cambiarlo demostraría que estaba mal hecho.
- B) Dejar de registrar las horas para que el retraso del plan no quede a la vista.
- C) Reestimar las tareas que faltan con lo aprendido y ajustar el plan o el alcance.
- D) Saltar las pruebas de las tareas restantes para recuperar el tiempo perdido.


**27.** Dos aprendices modificaron en sus ramas la misma plantilla de solicitud de cambio del equipo. Al integrar la segunda rama aparece un conflicto. ¿Qué corresponde? *(RAP 593106 · Avanzada · Caso)*

- A) Forzar el push sobre la rama de integración para que quede únicamente su propia versión del archivo.
- B) Actualizar la rama con la de integración, resolver conservando lo de ambos y volver a probar.
- C) Cerrar la solicitud de cambio y crear de nuevo el repositorio desde el principio.
- D) Borrar el archivo en conflicto para que la fusión pase sin ningún error.


**28.** El modelo de datos de un servicio tiene 6 tablas, pero el plan de construcción solo tiene tareas para 4 de ellas. ¿Cómo se interpreta? *(RAP 593106 · Avanzada · Caso)*

- A) El plan está completo porque tiene más de cuatro tareas registradas.
- B) Las dos tablas sin tarea deben borrarse del modelo de datos.
- C) El plan no cubre el diseño: faltan tareas para dos tablas del modelo.
- D) Las tablas sin tarea se crean solas al ejecutar las migraciones.


**29.** El plan del servicio `reservas` incluye la tarea «crear la FK de `reserva.cliente_id` hacia la tabla `cliente` del servicio `clientes`». ¿Cómo se interpreta frente al diseño de microservicios? *(RAP 593106 · Avanzada · Caso)*

- A) Es correcta: toda columna que termina en `_id` debe tener su llave foránea declarada.
- B) Contradice el diseño: entre servicios se guarda el identificador y se consulta por API o eventos.
- C) Es correcta si las dos bases de datos se ejecutan en el mismo servidor físico.
- D) Debe cambiarse por copiar completa la tabla de clientes, con todas sus columnas, dentro del servicio de reservas.


**30.** ¿Cuál es la diferencia entre integración continua y entrega continua? *(RAP 593106 · Avanzada)*

- A) Son el mismo proceso con dos nombres distintos según el proveedor de la herramienta.
- B) La primera despliega directamente en producción y la segunda solo compila el código fuente del servicio.
- C) La entrega continua reemplaza las pruebas automáticas por una revisión manual final.
- D) La primera verifica cada cambio; la segunda deja cada versión verificada lista para desplegar.


## Parte 2. Construcción de la base de datos (RAP 593107: Construir la base de datos para el software a partir del modelo de datos)

**31.** ¿Qué instrucciones pertenecen al lenguaje de definición de datos (DDL)? *(RAP 593107 · Básica)*

- A) SELECT, INSERT y UPDATE.
- B) GRANT, REVOKE y DENY.
- C) CREATE, ALTER y DROP.
- D) BEGIN, COMMIT y ROLLBACK.


**32.** ¿Para qué sirven GRANT y REVOKE? *(RAP 593107 · Básica)*

- A) Para conceder y retirar permisos sobre los objetos de la base de datos.
- B) Para confirmar y deshacer los cambios de una transacción en curso.
- C) Para crear y eliminar las tablas, vistas e índices de un esquema.
- D) Para insertar y borrar varias filas de una tabla en una sola orden de manipulación de datos.


**33.** ¿Qué es un sistema manejador de bases de datos (SMBD)? *(RAP 593107 · Básica)*

- A) El software que crea, administra y controla el acceso a las bases de datos.
- B) El archivo donde se guardan, una tras otra, todas las tablas de una sola aplicación.
- C) El lenguaje de consulta que se usa para leer y escribir los datos.
- D) El diagrama que muestra las entidades del negocio y sus relaciones.


**34.** ¿Qué garantiza una llave primaria? *(RAP 593107 · Básica)*

- A) Que la columna se relacione con una tabla que pertenece a otro servicio.
- B) Que cada fila se identifique de forma única y que ese valor no sea nulo.
- C) Que las consultas por cualquier columna de la tabla sean siempre rápidas.
- D) Que los valores de la columna se ingresen siempre en orden ascendente.


**35.** ¿Para qué se usa típicamente Redis en un sistema de microservicios? *(RAP 593107 · Básica)*

- A) Como fuente principal de datos financieros con transacciones complejas.
- B) Como motor relacional para reportes con muchas uniones entre tablas.
- C) Como almacén clave-valor en memoria para caché, sesiones o contadores.
- D) Como herramienta para versionar y aplicar las migraciones del esquema.


**36.** ¿Qué es una vista en una base de datos relacional? *(RAP 593107 · Básica)*

- A) Una copia física de una tabla que el motor actualiza de forma automática todas las noches.
- B) Una consulta almacenada con nombre que se usa como si fuera una tabla.
- C) Un índice que ordena las filas de la tabla por una de sus columnas.
- D) Un rol que solo tiene permiso de lectura sobre todo el esquema.


**37.** ¿Qué herramienta de PostgreSQL genera una copia de seguridad lógica de una base de datos? *(RAP 593107 · Básica)*

- A) `pg_isready`, que exporta las tablas que cambiaron en el último día.
- B) `\dt`, que guarda la lista de tablas del esquema en un archivo.
- C) `VACUUM`, que copia la base de datos completa hacia otro servidor.
- D) `pg_dump`, que exporta la estructura y los datos a un archivo.


**38.** Una regla de negocio dice: «el porcentaje de descuento está entre 0 y 50». ¿Qué restricción la implementa? *(RAP 593107 · Intermedia · Caso)*

- A) `CONSTRAINT uq_venta_descuento UNIQUE (descuento, total_venta)`
- B) `descuento NUMERIC(5,2) NOT NULL DEFAULT 50 CHECK (descuento > 0)`
- C) `CONSTRAINT ck_venta_descuento CHECK (descuento BETWEEN 0 AND 50)`
- D) `CONSTRAINT fk_venta_descuento FOREIGN KEY (descuento) REFERENCES tope`


**39.** Regla: «un mismo cliente no puede calificar dos veces el mismo producto». ¿Qué restricción la implementa en la tabla `calificacion`? *(RAP 593107 · Intermedia · Caso)*

- A) `UNIQUE (cliente_id)`
- B) `UNIQUE (producto_id)`
- C) `CHECK (cliente_id <> producto_id)`
- D) `UNIQUE (cliente_id, producto_id)`


**40.** Al borrar un pedido deben borrarse también sus líneas de detalle. ¿Qué declaración lo implementa? *(RAP 593107 · Intermedia · Caso)*

- A) `ON DELETE CASCADE` en la FK de `detalle_pedido` hacia `pedido`.
- B) `ON DELETE CASCADE` en la FK de `pedido` hacia `cliente`.
- C) `ON DELETE RESTRICT` en la FK de `detalle_pedido` hacia `pedido`.
- D) `ON DELETE SET NULL` en la FK de `detalle_pedido` hacia `producto`.


**41.** Se ejecuta: `BEGIN;` luego `UPDATE cuenta SET saldo = saldo - 100 WHERE id = 1;` luego un segundo UPDATE sobre la cuenta 2 que falla, y por último `ROLLBACK;`. ¿Cuál es el resultado? *(RAP 593107 · Intermedia · Caso)*

- A) Queda guardado el primer cambio, porque se ejecutó antes del error.
- B) Ninguno de los cambios queda guardado; la cuenta 1 conserva su saldo inicial.
- C) Quedan guardados los dos cambios, porque ROLLBACK solo cancela la última orden ejecutada.
- D) La tabla queda bloqueada hasta que un administrador la desbloquee.


**42.** ¿Qué objeto mantiene actualizada la columna `updated_at` en cada modificación, sin depender de la aplicación? *(RAP 593107 · Intermedia)*

- A) Una vista que muestra la hora actual junto a cada fila de la tabla.
- B) Un disparador BEFORE UPDATE que asigna la hora actual a la fila nueva.
- C) Un índice sobre `updated_at` que se recalcula en cada nueva consulta.
- D) Un valor `DEFAULT NOW()`, que se vuelve a aplicar en cada UPDATE.


**43.** En PostgreSQL, ¿cuál es una diferencia correcta entre una función y un procedimiento? *(RAP 593107 · Intermedia)*

- A) Son iguales; PostgreSQL solo cambia la palabra con que se crean y se borran.
- B) El procedimiento retorna una tabla y la función nunca puede retornar nada.
- C) La función retorna un valor y se usa en consultas; el procedimiento se invoca con CALL.
- D) La función solo se puede escribir en SQL puro y el procedimiento solo en el lenguaje de programación C.


**44.** En una tabla de 2 millones de filas, la consulta `SELECT ... WHERE cliente_id = $1` es lenta. ¿Qué objeto la mejora? *(RAP 593107 · Intermedia · Caso)*

- A) Una restricción CHECK sobre la columna `cliente_id`.
- B) Convertir `cliente_id` en la llave primaria de la tabla.
- C) Un índice sobre la columna `cliente_id` de esa tabla.
- D) Una vista que filtre las filas por `cliente_id`.


**45.** El rol de reportes solo necesita consultar las ventas por mes. ¿Qué configuración aplica el mínimo privilegio? *(RAP 593107 · Intermedia · Caso)*

- A) Conceder ALL PRIVILEGES sobre el esquema para evitar errores de permisos.
- B) Conceder SELECT sobre una vista de ventas por mes y nada sobre las tablas base.
- C) Usar el mismo usuario administrador de la aplicación para generar los reportes.
- D) Conceder SELECT, INSERT y UPDATE, por si luego necesita corregir algún dato.


**46.** En PostgreSQL 16, un rol recién creado y sin permisos ejecuta `SELECT * FROM ventas.pedido`, en un esquema `ventas` que otro usuario acaba de crear. ¿Qué ocurre? *(RAP 593107 · Intermedia · Caso)*

- A) Recibe `permission denied for schema ventas`: un esquema nuevo no da acceso a PUBLIC.
- B) Lee la tabla, porque todo rol hereda de PUBLIC el acceso a los esquemas nuevos.
- C) Lee la tabla, pero no puede modificarla hasta que se le conceda UPDATE.
- D) Recibe un error de sintaxis, porque debe anteponer el nombre del dueño.


**47.** Un aprendiz corrige su `V2__constraints_indexes.sql` y ejecuta `docker compose up -d`, pero el cambio no aparece en la base. ¿Por qué? *(RAP 593107 · Intermedia · Caso)*

- A) Los scripts de `/docker-entrypoint-initdb.d` corren solo con el volumen vacío; se usa `down -v`.
- B) Docker Compose solo ejecuta el primer archivo de la carpeta de migraciones montada en el contenedor de la base.
- C) PostgreSQL ignora los archivos SQL que contienen comentarios escritos en español.
- D) El contenedor necesita que se reinicie el computador para leer los cambios nuevos.


**48.** El servicio `pedidos` necesita mostrar el nombre del cliente, que pertenece al servicio `clientes`. ¿Qué es lo correcto? *(RAP 593107 · Intermedia · Caso)*

- A) Hacer un JOIN directo con la tabla de clientes de la base de datos del otro servicio.
- B) Declarar una FK desde pedidos hacia la tabla de clientes que tiene el otro servicio.
- C) Dar al servicio de pedidos el usuario administrador de la base de datos de clientes.
- D) Pedirlo al servicio de clientes por su API, o mantener una copia actualizada por eventos.


**49.** ¿Cuándo conviene MongoDB sobre un motor relacional? *(RAP 593107 · Intermedia)*

- A) Cuando se necesitan transacciones entre muchas tablas relacionadas a la vez.
- B) Cuando los datos son documentos de estructura variable que se leen completos.
- C) Cuando las reglas exigen llaves foráneas y restricciones estrictas en todo.
- D) Cuando el sistema solo guarda sesiones temporales que expiran en minutos.


**50.** ¿Qué hace la instrucción `UPDATE producto SET precio = 0;`? *(RAP 593107 · Intermedia · Caso)*

- A) No hace nada, porque le falta la cláusula WHERE que indica qué filas cambiar.
- B) Lanza un error de sintaxis por no tener WHERE.
- C) Pone en cero el precio de todos los productos de la tabla.
- D) Actualiza solo la primera fila de la tabla.


**51.** `V2__constraints_indexes.sql` ya se aplicó en el ambiente de pruebas del equipo y se descubre un CHECK mal escrito. ¿Qué es lo correcto? *(RAP 593107 · Avanzada · Caso)*

- A) Editar V2 y volver a ejecutarla, porque así el historial queda más ordenado.
- B) Crear `V5__corregir_check.sql`, que elimine la restricción y la vuelva a crear.
- C) Borrar V2 del repositorio y escribir la corrección completa dentro de V1.
- D) Corregir la restricción a mano en la base de pruebas, sin dejar ningún script.


**52.** En local, las bases de dos servicios están en el mismo servidor, y V2 incluye `FOREIGN KEY (cliente_id) REFERENCES clientes.cliente (id)`, tabla del servicio `clientes`. El script se ejecuta sin errores. ¿Cómo se evalúa? *(RAP 593107 · Avanzada · Caso)*

- A) Es correcto, porque la base de datos aceptó la instrucción sin mostrar ningún error.
- B) Es un error de diseño: acopla los servicios aunque hoy ejecute; se deja solo el identificador.
- C) Es correcto si además se agrega ON DELETE CASCADE, para que la integridad entre los dos servicios sea completa.
- D) Es un error solo de nombre: la restricción debería llamarse `fk_cliente`.


**53.** Se ejecutó `GRANT SELECT ON ventas.pedido TO reportes;`, pero al consultar, el rol recibe `permission denied for schema ventas`. ¿Qué falta? *(RAP 593107 · Avanzada · Caso)*

- A) `GRANT CREATE ON SCHEMA ventas TO reportes;`
- B) `GRANT ALL PRIVILEGES ON ventas.pedido TO reportes;`
- C) `GRANT USAGE ON SCHEMA ventas TO reportes;`
- D) `GRANT INSERT ON ventas.pedido TO reportes;`


**54.** La tabla tiene `CHECK (fecha_fin >= fecha_inicio)` y `fecha_fin` admite nulos. Se inserta una fila con `fecha_fin` NULL. ¿Qué ocurre? *(RAP 593107 · Avanzada · Caso)*

- A) Se rechaza, porque toda comparación con NULL viola la restricción CHECK.
- B) Se acepta solo si la columna tiene definido un valor por defecto.
- C) Se rechaza, porque NULL se convierte en la fecha mínima del motor.
- D) Se acepta: un CHECK que da desconocido (NULL) no se considera violado.


**55.** En el servicio de reservas, registrar una reserva y descontar el stock del implemento alquilado deben ocurrir juntos o no ocurrir. ¿Qué diseño lo garantiza? *(RAP 593107 · Avanzada · Caso)*

- A) Ejecutar ambas operaciones en una transacción y confirmar con COMMIT si las dos funcionan.
- B) Ejecutarlas en dos peticiones separadas y descontar el stock al día siguiente con un proceso programado.
- C) Descontar primero el stock, porque es la operación más importante de las dos.
- D) Desactivar el CHECK del stock mientras se insertan las reservas del día.


**56.** Una tabla de eventos recibe 5 000 inserciones por minuto y casi nunca se consulta. Alguien propone crear un índice por cada columna. ¿Cómo se evalúa? *(RAP 593107 · Avanzada · Caso)*

- A) Es mala idea: cada índice encarece cada inserción y ocupa espacio sin beneficio.
- B) Es buena idea: los índices aceleran las inserciones porque ordenan los datos.
- C) Es indiferente: los índices no afectan las inserciones ni el espacio en disco.
- D) Es obligatorio: toda columna necesita un índice para poder tener restricciones.


**57.** Un equipo ejecuta `pg_dump` cada noche desde hace meses, pero nunca ha restaurado una copia. ¿Qué riesgo tiene? *(RAP 593107 · Avanzada · Caso)*

- A) Ninguno: si el archivo de la copia existe y tiene tamaño, la restauración queda garantizada siempre.
- B) No sabe si la copia sirve: sin prueba de restauración no hay garantía de recuperar los datos.
- C) Que las copias ocupan espacio en disco; lo correcto es borrarlas cada semana.
- D) Que `pg_dump` borra los datos originales de la base al terminar cada copia.


**58.** El rol con el que se conecta la API es dueño de las tablas y tiene `CREATE` sobre el esquema. ¿Qué riesgo de seguridad implica? *(RAP 593107 · Avanzada · Caso)*

- A) Si la API es comprometida, puede borrar o alterar tablas; ese rol no debe tener DDL.
- B) Ninguno, porque la API necesita crear tablas nuevas en cada una de sus peticiones.
- C) Que las consultas de la API serán más lentas por tener demasiados permisos.
- D) Que el rol no podrá insertar filas mientras conserve el permiso de CREATE.


**59.** La carpeta montada en `/docker-entrypoint-initdb.d` tiene `V1__create_schema.sql`, `V2__constraints.sql` y `V10__add_column.sql`. ¿En qué orden los ejecuta el contenedor de PostgreSQL? *(RAP 593107 · Avanzada · Caso)*

- A) `V1__`, `V2__` y `V10__`, porque el contenedor ordena por el número de versión.
- B) Solo `V10__`, porque el contenedor ejecuta el archivo con la versión más alta.
- C) En el orden en que se crearon los archivos en el disco del equipo anfitrión.
- D) `V10__` primero, luego `V1__` y `V2__`: el orden es alfabético y no numérico.


**60.** Se necesita registrar en `auditoria_precio` el precio anterior y el nuevo cada vez que cambie un precio, incluso si el cambio se hace directamente desde psql. ¿Qué objeto lo logra? *(RAP 593107 · Avanzada · Caso)*

- A) Una vista que compare el precio actual con el precio que tenía la semana anterior.
- B) Un disparador AFTER UPDATE OF precio que inserte los valores OLD y NEW en la auditoría.
- C) Un índice sobre la columna `precio` que guarde de forma automática sus valores anteriores.
- D) Una regla en el código de la API que registre los cambios que se hacen por la API.
