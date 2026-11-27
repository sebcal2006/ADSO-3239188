# Banco de preguntas · Guía 1: Modelo de datos del software (v2)

**Ficha 3239188 · Análisis y Desarrollo de Software · Competencia 220501095 (Modelado de los artefactos del software)**  
**RAP 593101: Estructurar el modelo de datos del software de acuerdo con las especificaciones del análisis**  
**Fase Planeación · Actividad: Determinar la estructura lógica y tecnológica del software**

## Cómo se usa este banco

- Son **40 preguntas de selección múltiple** (opciones A, B, C y D, una sola respuesta correcta): **10 básicas, 16 intermedias y 14 avanzadas**, con la etiqueta del nivel. 31 se plantean como caso o escenario.
- Cubren todo el temario del resultado de aprendizaje: tipos de bases de datos y motores, modelo conceptual, modelo lógico relacional y sus reglas de transformación, normalización, diccionario de datos y estándar de nombrado, seguridad de los datos y tratamiento de datos personales, big data y los principios de datos de los microservicios del marco de gobierno.
- **Este archivo no trae las respuestas.** Es para estudiar: resuelve cada pregunta, justifica por qué descartas las otras tres opciones y contrasta con tus apuntes, la guía y lo que construyes en los productos. Las opciones tienen longitud parecida a propósito: no se acierta por el tamaño del texto ni por la posición de la letra.
- **La prueba de conocimiento** (jueves **3 de diciembre de 2026**, presencial e individual, 40 minutos, como **cuestionario en la plataforma Moodle (Zajuna)** con calificación automática) tiene **20 preguntas: 10 son variantes de preguntas de este banco (el mismo concepto con otros datos o con otro caso) y 10 son inéditas**. Memorizar la letra o el texto no sirve: hay que entender el porqué.
- La prueba de conocimiento pesa el **25 %** de la guía. La guía se aprueba con un promedio de **70 o más** entre los cuatro entregables (prueba de conocimiento, producto 1, producto 2 y prueba de desempeño).

## Fechas

| Entregable | Fecha |
|---|---|
| Prueba de conocimiento (cuestionario en Moodle) y prueba de desempeño (en computador, archivos en Moodle) | Jueves 3 de diciembre de 2026, en la sesión |
| Producto 1 (modelo conceptual, lógico y normalización) y Producto 2 (diccionario, motor y seguridad) | Hasta el domingo 6 de diciembre de 2026 a las 11:59 p. m., en tu rama y tu solicitud de integración |

Las condiciones, los mínimos por aprendiz y las rúbricas están en **Rubricas_G1.md**; los formatos, en **Plantillas_G1.md**; la plantilla del README de entrega, en **Plantilla_README_Entrega_G1.md**.

---

## Parte 1. Tipos de bases de datos, motores y big data

**1.** ¿Qué tipo de base de datos guarda cada registro como un documento de estructura flexible, por ejemplo en formato JSON? *(RAP 593101 · Básica)*

- A) Una base de datos documental, orientada a documentos JSON o similares.
- B) Una base de datos relacional, que organiza los datos en tablas de esquema fijo.
- C) Una base de datos de grafos, que guarda nodos y las aristas que los unen.
- D) Una base de datos de series de tiempo, que indexa medidas por su fecha.

**2.** Un servicio guarda sesiones de usuario que expiran a los 30 minutos y se leen miles de veces por segundo. ¿Qué tipo de almacenamiento encaja mejor? *(RAP 593101 · Básica · Caso)*

- A) Una base relacional con una tabla de sesiones y un índice por fecha de inicio.
- B) Una base de grafos que relacione cada sesión con sus usuarios y dispositivos.
- C) Un archivo plano compartido en el servidor que cada instancia lee al iniciar.
- D) Un almacén clave-valor en memoria con expiración automática de las claves.

**3.** ¿Qué características se usan con frecuencia para describir un escenario de big data? *(RAP 593101 · Básica)*

- A) Atomicidad, consistencia, aislamiento y durabilidad de cada transacción.
- B) Integridad, confidencialidad y disponibilidad de toda la información.
- C) Volumen, velocidad y variedad de los datos que se deben procesar.
- D) Primera, segunda y tercera forma normal de todo el modelo de datos.

**4.** El servicio de catálogo de una tienda guarda productos cuyos atributos cambian por categoría (una nevera tiene capacidad; una camiseta, talla y color) y casi no requiere transacciones entre productos. ¿Qué motor se justifica mejor? *(RAP 593101 · Intermedia · Caso)*

- A) Un motor relacional con una columna fija para cada atributo posible de todas las categorías.
- B) Un motor documental, que admite estructuras distintas por producto sin alterar el esquema.
- C) Un almacén clave-valor, que guarda cualquier atributo sin necesidad de consultarlo.
- D) Un motor de series de tiempo, porque cada producto tiene una fecha de creación.

**5.** El servicio de pagos registra cobros, abonos y reversos que deben quedar completos o no quedar, y se consultan por cliente y por fecha. ¿Qué decisión de motor es la más coherente? *(RAP 593101 · Intermedia · Caso)*

- A) Un motor relacional con transacciones ACID y restricciones de integridad.
- B) Un motor documental sin esquema, para registrar cualquier forma de pago futura.
- C) Un almacén clave-valor en memoria, por su velocidad al escribir cada cobro.
- D) Un índice de búsqueda de texto completo como única fuente de los pagos.

**6.** Un servicio usa un motor documental y guarda dentro de cada pedido una copia del nombre y la dirección de entrega del cliente. ¿Cómo se evalúa esa decisión frente a la normalización? *(RAP 593101 · Avanzada · Caso)*

- A) Es inválida, porque todo motor debe cumplir la 3FN exactamente igual que una base relacional.
- B) Es válida sin justificación, porque en un motor documental la normalización no tiene ningún sentido práctico.
- C) Es válida si se justifica: se embebe lo que se lee junto y la copia es una foto del momento de la compra.
- D) Es inválida, porque los motores documentales no permiten guardar textos dentro de otros documentos.

**7.** Un servicio recibe millones de eventos de clic por día para análisis de comportamiento, que se consultan por lotes y en agregados. ¿Qué decisión es más coherente? *(RAP 593101 · Avanzada · Caso)*

- A) Llevar los eventos a un almacenamiento distribuido para análisis, separado de la base transaccional.
- B) Guardar cada clic en la base relacional del servicio de pedidos, en una tabla normalizada hasta la 3FN.
- C) Descartar los eventos después de mostrarlos en pantalla para no ocupar espacio en disco.
- D) Guardar los clics en la caché clave-valor como única copia permanente de los datos.

## Parte 2. Modelo conceptual y modelo lógico relacional

**8.** En el modelo conceptual, ¿qué es una entidad? *(RAP 593101 · Básica)*

- A) Una columna de una tabla física con su tipo de dato y su tamaño máximo permitido.
- B) Un objeto del negocio, concreto o abstracto, del que interesa guardar datos.
- C) Una regla que restringe los valores que acepta un atributo del modelo.
- D) Una consulta que combina datos de varias tablas que están relacionadas.

**9.** ¿Qué función cumple el identificador de una entidad en el modelo conceptual? *(RAP 593101 · Básica)*

- A) Indicar con qué otras entidades se relaciona la entidad y en qué cantidad lo hace.
- B) Definir el tipo de dato y el tamaño máximo de cada uno de los atributos.
- C) Ordenar las ocurrencias de la entidad según la fecha de su registro.
- D) Distinguir de manera única cada ocurrencia de la entidad frente a las demás.

**10.** Dentro de una misma base de datos, ¿qué garantiza una llave foránea? *(RAP 593101 · Básica)*

- A) Que el valor referenciado exista como llave primaria en la tabla relacionada.
- B) Que el valor de la columna no se repita en ninguna otra fila de la misma tabla.
- C) Que la columna se cifre antes de guardarse en el disco del servidor.
- D) Que las consultas por esa columna sean más rápidas que por las demás.

**11.** El análisis dice: «toda reserva pertenece a exactamente un huésped; un huésped registrado puede no tener reservas todavía». ¿Qué cardinalidades (mínima y máxima) corresponden? *(RAP 593101 · Intermedia · Caso)*

- A) Cada reserva, con mínimo 0 y máximo 1 huésped; cada huésped, con mínimo 1 y máximo N reservas.
- B) Cada reserva, con mínimo 1 y máximo N huéspedes; cada huésped, con mínimo 1 y máximo 1 reserva.
- C) Cada reserva, con mínimo 0 y máximo N huéspedes; cada huésped, con mínimo 0 y máximo N reservas.
- D) Cada reserva, con mínimo 1 y máximo 1 huésped; cada huésped, con mínimo 0 y máximo N reservas.

**12.** Un proveedor puede registrar varios correos de contacto; en el modelo conceptual aparece como atributo multivaluado de `proveedor`. ¿Cómo se transforma al modelo lógico? *(RAP 593101 · Intermedia · Caso)*

- A) Una tabla `correos_proveedor` con su propia llave y una FK hacia `proveedores`.
- B) Una columna `correos` en `proveedores` con los valores separados por punto y coma.
- C) Tres columnas `correo1`, `correo2` y `correo3` en la tabla `proveedores`.
- D) Un objeto JSON con los correos guardado en una columna de texto de `proveedores`.

**13.** En un servicio de personal, cada empleado puede tener un jefe que también es empleado, y un jefe tiene varios subordinados. ¿Cómo se representa en el modelo lógico? *(RAP 593101 · Intermedia · Caso)*

- A) Una tabla `jefes` separada que copia todas las columnas de la tabla `empleados`.
- B) Una columna `subordinados` en `empleados` con los identificadores separados por comas.
- C) Una columna `jefe_id` en `empleados` con FK hacia la misma tabla y que admite nulo.
- D) Una columna `jefe_id` en `empleados`, obligatoria y sin FK para evitar los ciclos.

**14.** Las entidades `ClientePersona` y `ClienteEmpresa` comparten documento, correo y dirección, y cada una tiene dos atributos propios. ¿Qué transformación al modelo lógico es válida si se justifica? *(RAP 593101 · Intermedia · Caso)*

- A) Una tabla `clientes` con lo común y una tabla por subtipo que comparte su llave primaria.
- B) Una tabla por cada atributo común, unida a los subtipos mediante llaves foráneas.
- C) Una tabla `clientes` con lo común y los atributos propios en una sola columna de texto libre.
- D) Una tabla por subtipo, cada una en un servicio distinto, unidas por FK entre servicios.

**15.** La regla de negocio dice que la cantidad de un ítem de pedido debe estar entre 1 y 99. ¿Qué restricción del modelo lógico la garantiza en la base de datos? *(RAP 593101 · Intermedia · Caso)*

- A) Una restricción UNIQUE sobre la columna para que no se repitan cantidades.
- B) Un índice sobre la columna para que las cantidades se validen más rápido.
- C) Un valor por defecto de 1 en la columna para evitar valores fuera del rango.
- D) Una restricción CHECK sobre la columna que limite el valor a ese rango.

**16.** El servicio de agenda consulta con mucha frecuencia `citas` por `profesional_id` y rango de `fecha_hora`, y casi nunca por `observacion`. ¿Qué índice se justifica? *(RAP 593101 · Avanzada · Caso)*

- A) Un índice sobre `observacion` para acelerar todas las búsquedas.
- B) Un índice compuesto sobre (`profesional_id`, `fecha_hora`).
- C) Un índice sobre cada columna, para cubrir cualquier consulta posible.
- D) Ningún índice, porque la llave primaria acelera cualquier consulta.

**17.** Cada vehículo de una flota tiene a lo sumo un dispositivo GPS instalado, y cada dispositivo está en a lo sumo un vehículo. ¿Cómo se transforma al modelo lógico dentro del mismo servicio? *(RAP 593101 · Avanzada · Caso)*

- A) Una FK `vehiculo_id` en `dispositivos_gps`, con UNIQUE y que admite nulo.
- B) Una tabla intermedia con llave compuesta, como en toda relación entre dos entidades.
- C) Una FK en cada tabla apuntando a la otra, ambas obligatorias y sin UNIQUE.
- D) Una FK `vehiculo_id` en `dispositivos_gps` sin UNIQUE, que admite varios por vehículo.

## Parte 3. Normalización

**18.** ¿Qué exige la Segunda Forma Normal (2FN) a una tabla que ya está en 1FN? *(RAP 593101 · Básica)*

- A) Que ningún atributo no clave dependa solo de una parte de la llave compuesta.
- B) Que ningún atributo no clave dependa de otro atributo que tampoco forma parte de la llave.
- C) Que cada celda guarde un único valor y que no existan grupos repetidos.
- D) Que la tabla tenga una llave primaria simple y nunca una llave compuesta.

**19.** La tabla `cursos(id_curso, nombre, horarios)` guarda en `horarios` textos como «lun 8-10; mié 8-10». ¿Qué forma normal incumple y cuál es la corrección? *(RAP 593101 · Intermedia · Caso)*

- A) Incumple 2FN; se divide la llave primaria de `cursos` en dos columnas para separar los horarios.
- B) Incumple 1FN; los horarios pasan a una tabla propia con una fila por horario y FK al curso.
- C) Incumple 3FN; el nombre del curso pasa a una tabla aparte con su propio identificador.
- D) No incumple ninguna; el texto es un único valor porque está en una sola columna.

**20.** La tabla `turnos_mesero(id_mesero, id_turno, propinas, nombre_mesero, telefono_mesero)` tiene llave (`id_mesero`, `id_turno`). ¿Qué problema tiene y cómo se corrige? *(RAP 593101 · Intermedia · Caso)*

- A) Dependencia transitiva: las propinas dependen del teléfono y pasan a una tabla `telefonos`.
- B) Atributo multivaluado: las propinas se separan en una tabla distinta por cada turno.
- C) Dependencia parcial: los datos del mesero dependen solo de `id_mesero` y pasan a `meseros`.
- D) Ninguno: todas las columnas dependen de la llave porque están en la misma tabla.

**21.** En `sedes(id_sede, nombre, id_municipio, nombre_municipio, departamento)`, con llave `id_sede`, el municipio determina el departamento. ¿Qué corrección deja la tabla en 3FN? *(RAP 593101 · Intermedia · Caso)*

- A) Separar `nombre` en una tabla propia porque depende directamente de `id_sede`.
- B) Crear la llave compuesta (`id_sede`, `id_municipio`) para que todo dependa de la llave completa.
- C) Quitar `id_municipio` y conservar el nombre del municipio y el departamento en la sede.
- D) Llevar municipio y departamento a `municipios` y dejar `id_municipio` como FK en `sedes`.

**22.** `facturas(num_factura, fecha, nit_cliente, razon_social, cod_producto, descripcion, unidad_medida, cantidad)` tiene llave (`num_factura`, `cod_producto`); `num_factura → fecha, nit_cliente`, `nit_cliente → razon_social` y `cod_producto → descripcion, unidad_medida`. ¿Qué esquema queda en 3FN? *(RAP 593101 · Avanzada · Caso)*

- A) `facturas(num_factura, fecha, nit_cliente, razon_social)` y `detalles(num_factura, cod_producto, descripcion, unidad_medida, cantidad)`.
- B) `clientes(nit, razon_social)`, `facturas(num_factura, fecha, nit_cliente)`, `productos(cod_producto, descripcion, unidad_medida)` y `detalles(num_factura, cod_producto, cantidad)`.
- C) `clientes(nit, razon_social)`, `facturas(num_factura, fecha, nit_cliente)` y `detalles(num_factura, cod_producto, descripcion, unidad_medida, cantidad)` con llave (`num_factura`, `cod_producto`).
- D) `facturas(num_factura, fecha)`, `clientes(nit, razon_social, num_factura)` y `detalles(num_factura, cod_producto, cantidad)`.

**23.** Un tablero muestra el total de cada pedido miles de veces por hora y calcularlo exige sumar los ítems cada vez. El equipo propone guardar `total` en `pedidos`. ¿Cuál es la decisión correcta? *(RAP 593101 · Avanzada · Caso)*

- A) Aceptarlo como desnormalización documentada, con una regla que recalcule el total al cambiar los ítems.
- B) Rechazarlo siempre, porque cualquier columna calculada rompe la primera forma normal del modelo lógico relacional.
- C) Aceptarlo sin documentarlo, porque el rendimiento justifica cualquier redundancia en el modelo.
- D) Eliminar la tabla de ítems y guardar solo el total, para que no exista ninguna redundancia.

## Parte 4. Diccionario de datos y estándar de nombrado

**24.** En un diccionario de datos, ¿qué describe el dominio de una columna? *(RAP 593101 · Básica)*

- A) El conjunto de valores válidos que puede tomar, como un rango o una lista.
- B) La tabla de otro servicio desde la cual se copia el valor de la columna.
- C) El rol que creó la columna en la base de datos y la fecha exacta en que la creó.
- D) El índice que acelera las búsquedas que se hacen sobre esa columna.

**25.** En el diccionario, la columna `fecha_hora_cita` de un servicio que atiende usuarios de varias zonas horarias aparece como VARCHAR(20). ¿Qué ajuste corresponde? *(RAP 593101 · Intermedia · Caso)*

- A) Mantener VARCHAR y ampliar el tamaño a 50 caracteres para admitir cualquier formato de fecha.
- B) Usar INTEGER con el año, el mes y el día concatenados en un solo número entero.
- C) Usar DATE, porque la hora de la cita no hace falta para ordenar la agenda.
- D) Usar un tipo de fecha y hora con zona horaria, como TIMESTAMPTZ, según la convención.

**26.** Un diccionario trae las tablas `Clientes`, `tbl_pedido` y `DetallePedidos`, y las columnas `IdCli` y `fechaPed`. La convención del equipo es snake_case, tablas en plural y FK como `<singular>_id`. ¿Qué nombres la cumplen? *(RAP 593101 · Intermedia · Caso)*

- A) `Clientes`, `Pedidos`, `DetallesPedido`, `ClienteId` y `FechaPedido`.
- B) `tbl_clientes`, `tbl_pedidos`, `tbl_detalles`, `id_cli` y `fec_ped`.
- C) `clientes`, `pedidos`, `detalles_pedido`, `cliente_id` y `fecha_pedido`.
- D) `cliente`, `pedido`, `detalle`, `idCliente` y `fechapedido`.

**27.** El diccionario dice que `estado` de `ordenes` es VARCHAR(20) con valores PENDIENTE, PAGADA y ANULADA; el modelo lógico la declara INTEGER sin CHECK. ¿Qué procede? *(RAP 593101 · Avanzada · Caso)*

- A) Dejar ambos documentos así, porque cada uno describe una vista distinta del mismo dato del servicio.
- B) Corregir solo el diccionario para que diga INTEGER, sin restringir los valores posibles.
- C) Eliminar la columna `estado` y deducir el estado de la orden a partir de su fecha.
- D) Unificar diccionario y modelo, y declarar la restricción CHECK con los valores del dominio.

## Parte 5. Seguridad de los datos y tratamiento de datos personales

**28.** ¿Qué principio de seguridad se protege al impedir que un dato se modifique sin autorización o quede inconsistente? *(RAP 593101 · Básica)*

- A) La disponibilidad de los datos.
- B) La integridad de los datos.
- C) La confidencialidad de los datos.
- D) La escalabilidad de los datos.

**29.** El servicio de afiliados guarda número de documento, teléfono y contraseña. ¿Qué medida es correcta para cada dato? *(RAP 593101 · Intermedia · Caso)*

- A) Los tres datos cifrados con la misma llave reversible para descifrarlos cuando se necesite.
- B) Contraseña cifrada de forma reversible; documento y teléfono en texto plano.
- C) Contraseña con hash y sal; documento y teléfono cifrados o enmascarados según el rol.
- D) Los tres datos con hash y sal, de modo que nadie pueda volver a leerlos.

**30.** Un servicio de inscripciones debe recuperarse de la pérdida de su servidor sin perder más de una hora de datos. ¿Qué política de disponibilidad responde a esa exigencia? *(RAP 593101 · Intermedia · Caso)*

- A) Un respaldo completo semanal guardado en el mismo disco del servidor de la base.
- B) Permisos de solo lectura para todos los roles durante el horario de inscripciones.
- C) Respaldos al menos cada hora, copia en otra ubicación y pruebas de restauración.
- D) Cifrado de las columnas personales de la tabla de inscripciones con una llave.

**31.** El usuario de base de datos con que se conecta el servicio de facturación tiene permisos de administrador sobre todo el motor «para facilitar las migraciones». ¿Qué política corrige el riesgo? *(RAP 593101 · Avanzada · Caso)*

- A) Mantener el permiso de administrador y cambiar la contraseña del usuario de base de datos cada semana.
- B) Dar el mismo permiso de administrador a todos los servicios para que sean iguales.
- C) Mantener el permiso y cifrar las tablas para que los datos no se puedan leer.
- D) Mínimo privilegio: un usuario de la aplicación solo con DML en su esquema y otro para migraciones.

**32.** El servicio de afiliaciones pide fecha de nacimiento, dirección y un dato de salud para un descuento. ¿Qué conjunto de medidas trata correctamente esos datos personales? *(RAP 593101 · Avanzada · Caso)*

- A) Guardar todos los datos cifrados y usarlos para cualquier fin futuro que defina la empresa.
- B) Finalidad informada, autorización previa, solo los datos necesarios, acceso por rol y plazo de conservación.
- C) Pedir la autorización solo si el titular la solicita expresamente y guardar los datos sin ningún plazo definido.
- D) Publicar los datos de forma anónima en reportes abiertos sin consultar antes al titular.

**33.** Un servicio cifra en la base las columnas de documento y teléfono, pero la API y la conexión a la base viajan sin cifrar. ¿Qué evaluación es correcta? *(RAP 593101 · Avanzada · Caso)*

- A) Es suficiente, porque los datos ya están cifrados cuando quedan guardados en la base.
- B) Es suficiente si la contraseña de la base de datos tiene al menos doce caracteres.
- C) Falta proteger los datos en tránsito con TLS; el cifrado en reposo no cubre ese riesgo.
- D) Sobra cifrar en reposo; basta con cifrar en tránsito para cubrir los dos riesgos.

## Parte 6. Datos en una arquitectura de microservicios

**34.** Según el principio de base de datos por servicio, ¿cómo obtiene un servicio un dato que pertenece a otro? *(RAP 593101 · Básica)*

- A) Con una consulta SQL que une sus propias tablas con las tablas del otro servicio.
- B) Por la API del servicio dueño o por los eventos que ese servicio publica.
- C) Leyendo la base del otro servicio con un usuario de solo lectura.
- D) Copiando cada noche toda la base del otro servicio a su propia base.

**35.** Las tablas del marco de gobierno traen `created_at`, `updated_at`, `created_by`, `updated_by` y `deleted_at`. ¿Para qué sirve ese conjunto? *(RAP 593101 · Intermedia · Caso)*

- A) Llevar el control de versiones del esquema de la tabla en cada una de las migraciones aplicadas.
- B) Particionar la tabla por fecha para que las consultas históricas sean más rápidas.
- C) Registrar quién y cuándo creó o modificó cada fila, y marcar las eliminadas sin borrarlas.
- D) Reemplazar la llave primaria por una combinación de usuario y fecha de creación.

**36.** El servicio de pedidos necesita saber qué cliente hizo cada pedido; los clientes pertenecen al servicio de clientes. ¿Cómo se modela en la base del servicio de pedidos? *(RAP 593101 · Intermedia · Caso)*

- A) Una columna `cliente_id` con FK hacia la tabla `clientes` de la otra base.
- B) Una copia completa de la tabla `clientes` dentro de la base de pedidos.
- C) Una vista que une en tiempo real la tabla `pedidos` con la tabla `clientes` del otro servicio.
- D) Una columna `cliente_id` sin FK; los datos del cliente se obtienen por API o eventos.

**37.** En `data-model.md` del servicio de reservas aparece `huesped_id UUID REFERENCES huespedes(id)`, y `huespedes` está en el servicio de identidad. ¿Qué hallazgo procede? *(RAP 593101 · Avanzada · Caso)*

- A) Ninguno: la FK garantiza integridad y es la práctica recomendada también entre servicios.
- B) Se corrige moviendo la tabla `huespedes` al servicio de reservas para conservar la FK.
- C) Viola la base de datos por servicio: se quita la FK y el dato se valida por API o eventos.
- D) Se corrige con una FK `ON DELETE CASCADE` para propagar el borrado al otro servicio.

**38.** Los servicios de ventas y de despachos guardan la dirección de entrega del cliente, y ambos la actualizan. ¿Qué corrige la matriz de propiedad de los datos? *(RAP 593101 · Avanzada · Caso)*

- A) Dejar que ambos actualicen y conservar el valor con la fecha de cambio más reciente.
- B) Crear un tercer servicio que lea las dos bases y corrija las diferencias cada noche.
- C) Mover la dirección a una tabla compartida en una base común, con acceso de escritura para ambos servicios.
- D) Definir un único servicio dueño de la dirección; el otro guarda copia y se sincroniza por evento.

**39.** La tabla `usuarios` usa borrado lógico con `deleted_at` y tiene UNIQUE sobre `correo`. Un usuario borrado lógicamente quiere registrarse de nuevo con el mismo correo y la base lo rechaza. ¿Qué ajuste es el más adecuado? *(RAP 593101 · Avanzada · Caso)*

- A) Quitar la restricción UNIQUE de `correo` y validar duplicados solo en la interfaz.
- B) Un índice único parcial sobre `correo` solo para las filas con `deleted_at` nulo.
- C) Borrar físicamente la fila anterior para liberar el correo antes del nuevo registro.
- D) Agregar la fecha actual al final del correo nuevo para que no se repita en la tabla.

**40.** Al confirmar un pedido, el servicio de pedidos debe descontar inventario en el servicio de inventario; no hay base compartida. ¿Qué mecanismo mantiene la consistencia? *(RAP 593101 · Avanzada · Caso)*

- A) Una transacción única que bloquee las tablas de ambas bases de datos hasta que termine el pedido.
- B) Consistencia eventual con eventos y acciones compensatorias, como en el patrón saga.
- C) Un disparador en la base de pedidos que escriba en la tabla de inventario.
- D) Una vista materializada compartida que ambos servicios actualicen a la vez.

