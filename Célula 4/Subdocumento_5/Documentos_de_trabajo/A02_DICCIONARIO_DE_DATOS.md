# A-02 — Diccionario de datos

**Caso:** 06 Portuaria — TERABYTE
**Subdocumento:** 5 — Modelo y gestion de datos
**Celula:** 4 (V. Guzman / M. Reyes)
**Destino en el documento:** Anexo A.2 y § 5.14
**Version:** 1.0 · 6 de septiembre de 2026
**Modelo de origen:** diagramas del modelo conceptual, version 2.1

---

## 0. Alcance

Este documento cumple `BTT, Cap. 5, RT-05.01`, que exige entregar el modelo de datos documentado **y un diccionario de datos con el nombre, el tipo, el dominio de valores, la obligatoriedad, el propietario y la sensibilidad de cada atributo**, y `BA, Art. 23`, que anade el linaje y el propietario por dominio de informacion.

Cubre **las 80 entidades y los 451 atributos** del modelo conceptual version 2.1, sin excepcion. Cada entidad aparece con su ficha de gobierno y la tabla completa de sus atributos.

El diccionario **no** define tablas, indices, claves foraneas fisicas ni motor: eso pertenece al § 5.4 y depende de decisiones de arquitectura fisica que Celula 3 aun no ha cerrado. Tampoco redefine el modelo: si un atributo no esta en los diagramas, no esta aqui.

### Relacion con la version 2.1 del modelo

Antes de escribir este diccionario se revisaron los catorce diagramas de la version 2.0 y se corrigieron cinco defectos de consistencia, documentados en la adenda del informe de revision. Tres afectan directamente a lo que se escribe aqui:

- `CONDUCTOR` ya no duplica el documento de identidad: el dato personal vive una sola vez en `PERSONA` y el conductor lo referencia. Sin esa correccion, el diccionario habria declarado el mismo dato personal dos veces, con dos plazos de retencion y dos cifrados.
- `ALARMA` ya no guarda el origen en dos campos que podian discrepar.
- `PESAJE_VGM` admite el repesaje que `RF-GAT-09` contempla.

---

## 1. Convenciones del diccionario

### 1.1 Los ocho campos por atributo

`RT-05.01` exige seis campos. Se agregan dos que este caso hace necesarios, y que se declaran como decision propia de Terabyte.

| Campo | Origen | Contenido |
|---|---|---|
| Nombre | `RT-05.01` | identificador del atributo, sin tilde, igual al del diagrama |
| Tipo | `RT-05.01` | tipo conceptual, no tipo de motor |
| Dominio de valores | `RT-05.01` | rango, enumeracion o referencia |
| Obligatoriedad | `RT-05.01` | obligatorio, condicional o derivado |
| Propietario | `RT-05.01` | rol organizacional del CLIENTE, nunca un sistema |
| Sensibilidad | `RT-05.01` | clase de proteccion aplicable |
| **Clase de retencion** | propio | la clase del § 5.12 que gobierna su ciclo de vida |
| **Fuente de verdad** | propio | quien puede escribirlo, incluida la coexistencia con el TOS 2012 |

El propietario y la fuente de verdad se declaran a nivel de entidad, porque son propiedad del objeto y no de cada campo; los demas se declaran por atributo.

### 1.2 Tipos conceptuales

`string` · `int` · `decimal` · `boolean` · `date` · `enum` · `timestamptz`

`timestamptz` se usa en **todo** instante: el terminal opera 24x7x365 y la evidencia debe ser comparable entre husos horarios. No hay ningun instante sin zona en el modelo.

### 1.3 Como se decide la obligatoriedad

Regla aplicada sin excepcion, para que el criterio sea verificable y no quede al gusto de quien escribe:

| Valor | Cuando se aplica |
|---|---|
| **Obligatorio** | el atributo forma parte de la clave primaria, o su ausencia impide persistir el hecho |
| **Condicional** | el modelo declara explicitamente una condicion de nulidad: *nulo mientras*, *nulo si*, *solo cuando*, *puede no* |
| **Derivado** | el atributo se calcula a partir de otros y se audita; **no se captura como dato de entrada** |

La distincion entre obligatorio y derivado no es formal. `RT-05.03` exige poder reconstruir los valores anteriores y posteriores de cualquier registro, y `RT-05.04` exige validacion en el punto de captura: un atributo derivado no se valida en captura, se recalcula y se contrasta.

### 1.4 Clases de sensibilidad

| Clase | Definicion | Consecuencia |
|---|---|---|
| `interna` | uso interno del terminal | control de acceso por rol |
| `personal` | dato de persona natural | cifrado de campo y registro de consulta, `RT-11.10` y `RT-16.09` |
| `comercial sensible` | tarifas negociadas, volumenes y documentacion del cliente | cifrado de campo y segregacion por contraparte |
| `sensible por seguridad de la carga` | ubicacion y contenido declarado del contenedor | cifrado de campo y registro de consulta; el caso lo califica expresamente |
| `evidencia` | respalda un hecho con consecuencia externa | inmutabilidad y sello de integridad, `RT-16.07` |
| `telemetria` | serie temporal de instrumentacion | retencion diferenciada en linea y agregada |
| `auditoria` | registro de lo que hicieron las personas | inalterable para todo perfil, incluido el administrador |
| `maestro` | entidad compartida entre modulos | gestion de datos maestros sin duplicacion, `RT-05.09` |

### 1.5 Clases de retencion

Las ocho clases del § 5.12, mas cuatro categorias de gobierno que el propio diccionario necesita.

| Clase | Plazo y tratamiento | Origen |
|---|---|---|
| Movimientos y registros de operacion | 10 anos, eliminacion controlada | `CP, Cap. 15, RT-05.10` |
| Series de temperatura reefer | 5 anos | `CP, Cap. 15, RT-05.10`; `RNF-CUM-08` |
| Evidencia de hechos facturables | 6 anos | `CP, Cap. 15, RT-05.10` |
| Verificacion de masa bruta | 5 anos | `CP, Cap. 15, RT-05.10` |
| Imagenes de reconocimiento | 12 meses, eliminacion o anonimizacion | `CP, Cap. 15, RT-05.10` |
| Registros de acceso de personas | 5 anos | `CP, Cap. 15, RT-05.10` |
| Telemetria de equipos | 2 anos en linea, agregacion posterior | `CP, Cap. 15, RT-05.10` |
| Auditoria | el plazo de la clase auditada | `RT-05.03`, `RT-16.07` |
| Maestro | mientras la entidad opere, mas el plazo del dato que referencia | decision propia |
| Permanente | parametro de gobierno, no caduca | decision propia |
| Vigencia del contrato + 6 meses | preaviso de obsolescencia | `RT-05.17` |
| La de la clase que transporta | el mensaje hereda el plazo de su contenido | decision propia |

`RNF-CUM-14` prohibe expresamente aplicar un plazo uniforme a toda la informacion. La seccion 6 verifica que ninguna entidad quedo sin clase asignada.

### 1.6 Regla de no invencion

Tres atributos aparecen con la marca **VACIO DECLARADO** en su dominio de valores. No es un descuido: son los tres valores que el caso deliberadamente no entrega y que ninguna celula ha cerrado. Poblarlos con una cifra plausible seria inventar un dato del CLIENTE.

---

## 2. Resumen por dominio

| Dominio | Entidades | Atributos |
|---|---:|---:|
| DOM-OPS · Contenedor y operacion | 5 | 40 |
| DOM-PAT · Patio y posicion | 9 | 48 |
| DOM-GAT · Gate y transporte | 11 | 57 |
| DOM-REF · Reefer y cadena de frio | 7 | 46 |
| DOM-NAV · Nave y planificacion | 10 | 52 |
| DOM-INS · Inspecciones | 6 | 32 |
| DOM-FAC · Evidencia y facturacion | 7 | 38 |
| DOM-ACC · Acceso e identidad | 10 | 46 |
| DOM-EMI · Energia y emisiones | 4 | 27 |
| DOM-INT · Integracion, autoridad y auditoria | 11 | 65 |
| **Total** | **80** | **451** |

---

# 3. Diccionario de datos

## D-02 · DOM-OPS y DOM-PAT — Contenedor, operacion, patio y posicion

### CONTENEDOR

| | |
|---|---|
| **Dominio** | DOM-OPS |
| **Propietario del dato** | Operaciones |
| **Clase de dato** | maestro |
| **Sensibilidad** | interna |
| **Clase de retencion** | Maestro — mientras la entidad opere, mas el plazo del dato que referencia |
| **Fuente de verdad** | Naviera para los datos del equipo; la solucion para su estado en el terminal |
| **Diagrama** | D-02 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `codigo_iso6346` | string | PK | Codigo ISO 6346: cuatro letras de propietario, seis digitos y digito verificador | Obligatorio | identificador normalizado, RF-INT-08 |
| `tipo` | enum | — | {dry, reefer, tanque, open top} | Obligatorio | dry, reefer, tanque, open top |
| `tamano` | enum | — | {20 pies, 40 pies} | Obligatorio | 20 pies, 40 pies |
| `tara` | decimal | — | kg | Obligatorio | kg |
| `clase_imdg` | enum | — | {clases 1 a 9 del Codigo IMDG} | Condicional | nulo si no es carga peligrosa, RN-02 |
| `requiere_frio` | boolean | — | {verdadero, falso} | Obligatorio | — |
| `dimension_especial` | boolean | — | {verdadero, falso} | Obligatorio | — |
| `id_naviera` | string | FK | Identificador de la entidad referenciada | Obligatorio | ref. D-05.NAVIERA |

### VISITA — nombre de negocio: `VisitaContenedor`

| | |
|---|---|
| **Dominio** | DOM-OPS |
| **Propietario del dato** | Operaciones |
| **Clase de dato** | operacional |
| **Sensibilidad** | sensible por seguridad de la carga |
| **Clase de retencion** | Movimientos y registros de operacion — 10 anos |
| **Fuente de verdad** | Solucion tras el corte de la zona; TOS 2012 antes del corte |
| **Diagrama** | D-02 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_visita` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `codigo_iso6346` | string | FK | Identificador de la entidad referenciada | Obligatorio | — |
| `flujo` | enum | — | {importacion, exportacion, transbordo} | Obligatorio | importacion, exportacion, transbordo |
| `instante_ingreso` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |
| `instante_salida` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Condicional | nulo mientras la visita esta abierta |
| `estado_visita` | enum | — | {anunciada, descargada, ingresada, posicionada, removida, en inspeccion, retenida, liberable, embarcada, retirada, anulada} | Obligatorio | ciclo de vida en D-09 |
| `id_recalada` | string | FK | Identificador de la entidad referenciada | Condicional | ref. D-05.RECALADA, nulo hasta la asignacion |
| `id_cliente` | string | FK | Identificador de la entidad referenciada | Obligatorio | ref. D-06.CLIENTE |

### MOVIMIENTO

| | |
|---|---|
| **Dominio** | DOM-OPS |
| **Propietario del dato** | Operaciones |
| **Clase de dato** | operacional |
| **Sensibilidad** | sensible por seguridad de la carga |
| **Clase de retencion** | Movimientos y registros de operacion — 10 anos |
| **Fuente de verdad** | Solucion tras el corte de la zona; TOS 2012 antes del corte |
| **Diagrama** | D-02 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_movimiento` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `id_visita` | string | FK | Identificador de la entidad referenciada | Obligatorio | — |
| `tipo` | enum | — | {descarga, carga, remocion, reubicacion, ingreso, salida} | Obligatorio | descarga, carga, remocion, reubicacion, ingreso, salida |
| `instante` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | instante real del hecho, no de digitacion |
| `id_equipo` | string | FK | Identificador de la entidad referenciada | Obligatorio | — |
| `celda_origen` | string | FK | Identificador de la entidad referenciada | Condicional | nulo en ingreso |
| `celda_destino` | string | FK | Identificador de la entidad referenciada | Condicional | nulo en salida |
| `fuente_registro` | enum | — | {telemetria, optica, manual excepcional} | Obligatorio | telemetria, optica, manual excepcional |
| `id_correlacion` | string | — | Identificador de correlacion comun de extremo a extremo | Obligatorio | RT-05.19 |
| `id_recalada` | string | FK | Identificador de la entidad referenciada | Obligatorio | ref. D-05.RECALADA, solo carga y descarga |

### POSICION_VIGENTE

| | |
|---|---|
| **Dominio** | DOM-PAT |
| **Propietario del dato** | Operaciones |
| **Clase de dato** | operacional |
| **Sensibilidad** | sensible por seguridad de la carga |
| **Clase de retencion** | Movimientos y registros de operacion — 10 anos |
| **Fuente de verdad** | Solucion tras el corte de la zona; TOS 2012 antes del corte |
| **Diagrama** | D-02 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_visita` | string | PK,FK | Identificador de la entidad referenciada | Obligatorio | — |
| `id_celda` | string | FK | Identificador de la entidad referenciada | Obligatorio | — |
| `vigente_desde` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |
| `estado_confianza` | enum | — | {conocida, por verificar (D-10), RF-PAT-03} | Obligatorio | conocida, por verificar (D-10), RF-PAT-03 |
| `instante_ultima_verificacion` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |

### ASIGNACION_POSICION

| | |
|---|---|
| **Dominio** | DOM-PAT |
| **Propietario del dato** | Operaciones |
| **Clase de dato** | operacional |
| **Sensibilidad** | interna |
| **Clase de retencion** | Movimientos y registros de operacion — 10 anos |
| **Fuente de verdad** | Solucion |
| **Diagrama** | D-02 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_asignacion` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `id_visita` | string | FK | Identificador de la entidad referenciada | Obligatorio | — |
| `celda_propuesta` | string | FK | Identificador de la entidad referenciada | Obligatorio | — |
| `nivel_rn01_determinante` | int | — | 1 a 4 | Obligatorio | 1 a 4, RN-01 |
| `restriccion_cedida` | string | — | Texto acotado | Condicional | declarada solo cuando hay conflicto |
| `motivo` | string | — | Explicacion de la asignacion, ligada al nivel de RN-01 aplicado | Obligatorio | — |
| `instante` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |
| `version_algoritmo` | string | — | Version semantica del algoritmo de asignacion | Obligatorio | obligatoria para reproducir la decision |

### CONDICION_DINAMICA

| | |
|---|---|
| **Dominio** | DOM-PAT |
| **Propietario del dato** | Jefatura de operaciones |
| **Clase de dato** | operacional |
| **Sensibilidad** | interna |
| **Clase de retencion** | Movimientos y registros de operacion — 10 anos |
| **Fuente de verdad** | Solucion |
| **Diagrama** | D-02 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_condicion` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `tipo` | enum | — | {equipo no disponible, bloque restringido, cliente} | Obligatorio | equipo no disponible, bloque restringido, cliente |
| `alcance` | string | — | Bloque, zona o equipo sobre el que rige la condicion | Obligatorio | — |
| `id_autor` | string | FK | Identificador de la entidad referenciada | Obligatorio | ref. D-07.PERSONA |
| `motivo` | string | — | Motivo declarado por quien crea la condicion | Obligatorio | — |
| `vigencia_desde` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |
| `vigencia_hasta` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |

### TAREA_VERIFICACION

| | |
|---|---|
| **Dominio** | DOM-PAT |
| **Propietario del dato** | Jefatura de patio |
| **Clase de dato** | operacional |
| **Sensibilidad** | interna |
| **Clase de retencion** | Movimientos y registros de operacion — 10 anos |
| **Fuente de verdad** | Solucion |
| **Diagrama** | D-02 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_tarea` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `id_visita` | string | FK | Identificador de la entidad referenciada | Obligatorio | — |
| `posicion_candidata` | string | — | Identificador de celda donde se presume el contenedor | Obligatorio | — |
| `id_asignado_a` | string | FK | Identificador de la entidad referenciada | Obligatorio | ref. D-07.PERSONA |
| `estado` | enum | — | {abierta, en curso, cerrada} | Obligatorio | abierta, en curso, cerrada |
| `instante_creacion` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |
| `instante_cierre` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |

### CUSTODIA

| | |
|---|---|
| **Dominio** | DOM-OPS |
| **Propietario del dato** | Operaciones |
| **Clase de dato** | evidencia |
| **Sensibilidad** | evidencia |
| **Clase de retencion** | Evidencia de hechos facturables — 6 anos |
| **Fuente de verdad** | Solucion, con firma electronica de la contraparte |
| **Diagrama** | D-02 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_custodia` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `id_visita` | string | FK | Identificador de la entidad referenciada | Obligatorio | — |
| `responsable` | enum | — | {terminal, transportista, naviera} | Obligatorio | terminal, transportista, naviera |
| `desde` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |
| `hasta` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |
| `id_firma` | string | FK | Identificador de la entidad referenciada | Obligatorio | conformidad de recepcion o entrega, RT-16.14 |

### CONDICION_LIBERACION

| | |
|---|---|
| **Dominio** | DOM-OPS |
| **Propietario del dato** | Operaciones y comercial |
| **Clase de dato** | operacional |
| **Sensibilidad** | interna |
| **Clase de retencion** | Movimientos y registros de operacion — 10 anos |
| **Fuente de verdad** | Solucion, por conjuncion de fuentes externas (aduana, SAG, comercial) |
| **Diagrama** | D-02 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_visita` | string | PK,FK | Identificador de la entidad referenciada | Obligatorio | — |
| `documentacion_validada` | boolean | — | {verdadero, falso} | Obligatorio | — |
| `autorizacion_aduanera` | boolean | — | {verdadero, falso} | Obligatorio | — |
| `sin_retencion_fitosanitaria` | boolean | — | {verdadero, falso} | Obligatorio | — |
| `sin_deuda_asociada` | boolean | — | {verdadero, falso} | Obligatorio | — |
| `vgm_dentro_de_tolerancia` | boolean | — | {verdadero, falso} | Obligatorio | — |
| `liberado` | boolean | — | {verdadero, falso} | Derivado | derivado: conjuncion de las cinco, RN-06 |
| `instante_ultima_evaluacion` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |

### BLOQUE

| | |
|---|---|
| **Dominio** | DOM-PAT |
| **Propietario del dato** | Jefatura de patio |
| **Clase de dato** | maestro |
| **Sensibilidad** | interna |
| **Clase de retencion** | Maestro — mientras la entidad opere, mas el plazo del dato que referencia |
| **Fuente de verdad** | Solucion |
| **Diagrama** | D-02 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_bloque` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `id_zona_operativa` | string | FK | Identificador de la entidad referenciada | Obligatorio | ref. D-08.ZONA_OPERATIVA |
| `habilitado_imdg` | boolean | — | {verdadero, falso} | Obligatorio | — |

### CELDA

| | |
|---|---|
| **Dominio** | DOM-PAT |
| **Propietario del dato** | Jefatura de patio |
| **Clase de dato** | maestro |
| **Sensibilidad** | interna |
| **Clase de retencion** | Maestro — mientras la entidad opere, mas el plazo del dato que referencia |
| **Fuente de verdad** | Solucion |
| **Diagrama** | D-02 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_celda` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `id_bloque` | string | FK | Identificador de la entidad referenciada | Obligatorio | — |
| `bahia` | int | — | Numerico no negativo | Obligatorio | — |
| `fila` | int | — | Numerico no negativo | Obligatorio | — |
| `altura` | int | — | Numerico no negativo | Obligatorio | — |
| `tiene_toma_reefer` | boolean | — | {verdadero, falso} | Obligatorio | — |

### EQUIPO_PATIO

| | |
|---|---|
| **Dominio** | DOM-PAT |
| **Propietario del dato** | Mantenimiento |
| **Clase de dato** | maestro |
| **Sensibilidad** | interna |
| **Clase de retencion** | Maestro — mientras la entidad opere, mas el plazo del dato que referencia |
| **Fuente de verdad** | Solucion |
| **Diagrama** | D-02 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_equipo` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `tipo` | enum | — | {grua de patio, tractocamion, equipo pesado} | Obligatorio | grua de patio, tractocamion, equipo pesado |
| `fuente_energia` | enum | — | {diesel, electrico} | Obligatorio | diesel, electrico |
| `instrumentado` | boolean | — | {verdadero, falso} | Obligatorio | condiciona D-06.CONSUMO_EQUIPO |

### PUNTO_DE_PASO

| | |
|---|---|
| **Dominio** | DOM-PAT |
| **Propietario del dato** | Tecnologias de informacion |
| **Clase de dato** | maestro |
| **Sensibilidad** | interna |
| **Clase de retencion** | Maestro — mientras la entidad opere, mas el plazo del dato que referencia |
| **Fuente de verdad** | Solucion |
| **Diagrama** | D-02 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_punto` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `ubicacion` | string | — | Ubicacion fisica del portico o lector en el recinto | Obligatorio | — |

### LECTURA_OPTICA

| | |
|---|---|
| **Dominio** | DOM-PAT |
| **Propietario del dato** | Tecnologias de informacion |
| **Clase de dato** | evidencia · imagen |
| **Sensibilidad** | sensible por seguridad de la carga |
| **Clase de retencion** | Imagenes de reconocimiento — 12 meses |
| **Fuente de verdad** | Dispositivo de reconocimiento optico |
| **Diagrama** | D-02 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_lectura` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `id_punto` | string | FK | Identificador de la entidad referenciada | Obligatorio | — |
| `instante` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |
| `codigo_leido` | string | — | Codigo ISO 6346 o patente, segun el punto de paso | Condicional | puede no coincidir con ninguna visita abierta |
| `confianza_lectura` | decimal | — | 0 a 1 | Obligatorio | 0 a 1 |
| `id_visita` | string | FK | Identificador de la entidad referenciada | Condicional | nulo mientras la lectura no se concilia |


## D-03 · DOM-GAT — Gate y transporte terrestre

### TRANSPORTISTA

| | |
|---|---|
| **Dominio** | DOM-GAT |
| **Propietario del dato** | Comercial |
| **Clase de dato** | maestro |
| **Sensibilidad** | interna |
| **Clase de retencion** | Maestro — mientras la entidad opere, mas el plazo del dato que referencia |
| **Fuente de verdad** | Solucion, con dato declarado por la empresa |
| **Diagrama** | D-03 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_transportista` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `razon_social` | string | — | Razon social registrada | Obligatorio | — |
| `rol_unico_tributario` | string | UK | Identificador tributario nacional | Obligatorio | — |

### CAMION

| | |
|---|---|
| **Dominio** | DOM-GAT |
| **Propietario del dato** | Comercial |
| **Clase de dato** | maestro |
| **Sensibilidad** | interna |
| **Clase de retencion** | Maestro — mientras la entidad opere, mas el plazo del dato que referencia |
| **Fuente de verdad** | Transportista, validado por la solucion |
| **Diagrama** | D-03 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `patente` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `id_transportista` | string | FK | Identificador de la entidad referenciada | Obligatorio | — |

### CONDUCTOR

| | |
|---|---|
| **Dominio** | DOM-GAT |
| **Propietario del dato** | Comercial y proteccion portuaria |
| **Clase de dato** | maestro |
| **Sensibilidad** | personal |
| **Clase de retencion** | Registros de acceso de personas — 5 anos |
| **Fuente de verdad** | Transportista para el vinculo laboral; D-07.PERSONA para el dato personal |
| **Diagrama** | D-03 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_conductor` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `id_persona` | string | FK,UK | Identificador de la entidad referenciada | Obligatorio | ref. D-07.PERSONA, el dato personal vive alli, RT-05.09 |
| `id_transportista` | string | FK | Identificador de la entidad referenciada | Obligatorio | — |
| `habilitacion_vigente` | boolean | — | {verdadero, falso} | Derivado | derivado de D-07.HABILITACION |

### CITA

| | |
|---|---|
| **Dominio** | DOM-GAT |
| **Propietario del dato** | Jefatura de gate |
| **Clase de dato** | operacional |
| **Sensibilidad** | interna |
| **Clase de retencion** | Movimientos y registros de operacion — 10 anos |
| **Fuente de verdad** | Solucion |
| **Diagrama** | D-03 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_cita` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `id_transportista` | string | FK | Identificador de la entidad referenciada | Obligatorio | — |
| `id_visita` | string | FK | Identificador de la entidad referenciada | Obligatorio | ref. D-02.VISITA |
| `franja_desde` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |
| `franja_hasta` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |
| `estado` | enum | — | {confirmada, cumplida, fuera de ventana, no show} | Obligatorio | confirmada, cumplida, fuera de ventana, no show |
| `instante_solicitud` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |

### TURNO_CAMION

| | |
|---|---|
| **Dominio** | DOM-GAT |
| **Propietario del dato** | Jefatura de gate |
| **Clase de dato** | operacional |
| **Sensibilidad** | interna |
| **Clase de retencion** | Movimientos y registros de operacion — 10 anos |
| **Fuente de verdad** | Solucion, derivado de eventos de barrera |
| **Diagrama** | D-03 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_turno_camion` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `patente` | string | FK | Identificador de la entidad referenciada | Obligatorio | — |
| `id_conductor` | string | FK | Identificador de la entidad referenciada | Obligatorio | — |
| `id_cita` | string | FK | Identificador de la entidad referenciada | Condicional | nulo si el camion llega sin cita |
| `instante_arribo_barrera` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |
| `instante_instruccion_emitida` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |
| `instante_salida` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |
| `estadia_minutos` | int | — | Minutos, entero no negativo | Derivado | derivado de EVENTO_GATE, RF-GAT-12 |

### EVENTO_GATE

| | |
|---|---|
| **Dominio** | DOM-GAT |
| **Propietario del dato** | Jefatura de gate |
| **Clase de dato** | operacional |
| **Sensibilidad** | interna |
| **Clase de retencion** | Movimientos y registros de operacion — 10 anos |
| **Fuente de verdad** | Barrera fisica del puesto de gate |
| **Diagrama** | D-03 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_evento` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `id_turno_camion` | string | FK | Identificador de la entidad referenciada | Obligatorio | — |
| `tipo` | enum | — | {entrada, salida} | Obligatorio | entrada, salida |
| `puesto` | string | — | Identificador del puesto de gate: 8 de entrada y 6 de salida | Obligatorio | — |
| `instante` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |
| `id_correlacion` | string | — | Identificador de correlacion comun de extremo a extremo | Obligatorio | RT-05.19 |

### MOVIMIENTO_TERRESTRE

| | |
|---|---|
| **Dominio** | DOM-GAT |
| **Propietario del dato** | Jefatura de gate |
| **Clase de dato** | operacional |
| **Sensibilidad** | sensible por seguridad de la carga |
| **Clase de retencion** | Movimientos y registros de operacion — 10 anos |
| **Fuente de verdad** | Solucion |
| **Diagrama** | D-03 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_turno_camion` | string | PK,FK | Identificador de la entidad referenciada | Obligatorio | — |
| `id_visita` | string | PK,FK | Identificador de la entidad referenciada | Obligatorio | — |
| `sentido` | enum | — | {entrega, retiro} | Obligatorio | entrega, retiro |
| `instante` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |

### DOCUMENTO_TRANSPORTE

| | |
|---|---|
| **Dominio** | DOM-GAT |
| **Propietario del dato** | Comercial |
| **Clase de dato** | operacional |
| **Sensibilidad** | comercial sensible |
| **Clase de retencion** | Evidencia de hechos facturables — 6 anos |
| **Fuente de verdad** | Cliente o agencia que lo presenta; la solucion valida |
| **Diagrama** | D-03 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_documento` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `id_visita` | string | FK | Identificador de la entidad referenciada | Obligatorio | ref. D-02.VISITA |
| `tipo` | string | — | {catalogo de documentos de transporte, a cerrar con el CLIENTE} | Obligatorio | — |
| `estado_validacion` | enum | — | {validado, con discrepancia, pendiente} | Obligatorio | validado, con discrepancia, pendiente |
| `instante_validacion` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | validacion anticipada, RF-GAT-03 |

### PESAJE_VGM

| | |
|---|---|
| **Dominio** | DOM-GAT |
| **Propietario del dato** | Jefatura de gate |
| **Clase de dato** | evidencia |
| **Sensibilidad** | evidencia |
| **Clase de retencion** | Verificacion de masa bruta — 5 anos |
| **Fuente de verdad** | Bascula certificada del terminal |
| **Diagrama** | D-03 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_pesaje` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `id_visita` | string | FK | Identificador de la entidad referenciada | Obligatorio | ref. D-02.VISITA |
| `secuencia_pesaje` | int | — | Numerico no negativo | Obligatorio | 1 pesaje inicial, mayor a 1 repesaje tras discrepancia, RF-GAT-09 |
| `masa_declarada` | decimal | — | kg | Obligatorio | kg |
| `masa_verificada` | decimal | — | kg | Obligatorio | kg |
| `desviacion` | decimal | — | kg | Derivado | derivado, kg |
| `dentro_de_tolerancia` | boolean | — | {verdadero, falso} | Obligatorio | RN-05 |
| `instante` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |
| `id_bascula` | string | — | Identificador de la bascula certificada | Obligatorio | — |

### INSTRUCCION_DESTINO

| | |
|---|---|
| **Dominio** | DOM-GAT |
| **Propietario del dato** | Jefatura de gate |
| **Clase de dato** | operacional |
| **Sensibilidad** | interna |
| **Clase de retencion** | Movimientos y registros de operacion — 10 anos |
| **Fuente de verdad** | Solucion |
| **Diagrama** | D-03 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_instruccion` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `id_turno_camion` | string | FK | Identificador de la entidad referenciada | Obligatorio | — |
| `celda_destino` | string | FK | Identificador de la entidad referenciada | Obligatorio | ref. D-02.CELDA |
| `instante_emision` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |

### EXCEPCION_GATE

| | |
|---|---|
| **Dominio** | DOM-GAT |
| **Propietario del dato** | Jefatura de gate |
| **Clase de dato** | operacional |
| **Sensibilidad** | interna |
| **Clase de retencion** | Movimientos y registros de operacion — 10 anos |
| **Fuente de verdad** | Solucion |
| **Diagrama** | D-03 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_excepcion` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `id_turno_camion` | string | FK | Identificador de la entidad referenciada | Obligatorio | — |
| `motivo` | enum | — | {documental, VGM, habilitacion, sin cita, otro} | Obligatorio | documental, VGM, habilitacion, sin cita, otro |
| `estado` | enum | — | {abierta, resuelta, derivada} | Obligatorio | abierta, resuelta, derivada |
| `instante` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |


## D-04 · DOM-REF — Reefer y cadena de frio

### TABLERO

| | |
|---|---|
| **Dominio** | DOM-REF |
| **Propietario del dato** | Mantenimiento electrico |
| **Clase de dato** | maestro |
| **Sensibilidad** | interna |
| **Clase de retencion** | Maestro — mientras la entidad opere, mas el plazo del dato que referencia |
| **Fuente de verdad** | Solucion |
| **Diagrama** | D-04 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_tablero` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `id_bloque` | string | FK | Identificador de la entidad referenciada | Obligatorio | ref. D-02.BLOQUE |
| `estado` | enum | — | {operativo, en falla, sin comunicacion} | Obligatorio | operativo, en falla, sin comunicacion |
| `tomas_nominales` | int | — | Numerico no negativo | Obligatorio | — |

### TOMA_REEFER

| | |
|---|---|
| **Dominio** | DOM-REF |
| **Propietario del dato** | Mantenimiento electrico |
| **Clase de dato** | maestro |
| **Sensibilidad** | interna |
| **Clase de retencion** | Maestro — mientras la entidad opere, mas el plazo del dato que referencia |
| **Fuente de verdad** | Solucion |
| **Diagrama** | D-04 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_toma` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `id_tablero` | string | FK | Identificador de la entidad referenciada | Obligatorio | — |
| `id_celda` | string | FK | Identificador de la entidad referenciada | Obligatorio | ref. D-02.CELDA |
| `estado` | enum | — | {libre, ocupada, fuera de servicio} | Obligatorio | libre, ocupada, fuera de servicio |
| `instrumentada` | boolean | — | {verdadero, falso} | Condicional | si es falsa, la serie proviene de agregado reportado |

### CONEXION_REEFER

| | |
|---|---|
| **Dominio** | DOM-REF |
| **Propietario del dato** | Operaciones patio refrigerado |
| **Clase de dato** | operacional |
| **Sensibilidad** | comercial sensible |
| **Clase de retencion** | Evidencia de hechos facturables — 6 anos |
| **Fuente de verdad** | Solucion |
| **Diagrama** | D-04 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_conexion` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `id_visita` | string | FK | Identificador de la entidad referenciada | Obligatorio | ref. D-02.VISITA |
| `id_toma` | string | FK | Identificador de la entidad referenciada | Obligatorio | — |
| `instante_conexion` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |
| `instante_desconexion` | timestamptz | — | Instante con zona horaria; nulo mientras la conexion esta vigente | Condicional | nulo mientras la conexion esta vigente |
| `consigna_temperatura` | decimal | — | grados Celsius | Obligatorio | grados Celsius |
| `minutos_desconectado_acumulados` | int | — | Minutos, entero no negativo | Derivado | derivado, umbral en RN-10 |

### MUESTRA_TEMPERATURA

| | |
|---|---|
| **Dominio** | DOM-REF |
| **Propietario del dato** | Operaciones patio refrigerado |
| **Clase de dato** | telemetria |
| **Sensibilidad** | evidencia |
| **Clase de retencion** | Series de temperatura reefer — 5 anos |
| **Fuente de verdad** | Instrumentacion de la toma; agregada en el concentrador de patio |
| **Diagrama** | D-04 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_conexion` | string | PK,FK | Identificador de la entidad referenciada | Obligatorio | — |
| `instante` | timestamptz | PK | Instante con zona horaria; operacion 24x7 | Obligatorio | — |
| `temperatura` | decimal | — | grados Celsius | Obligatorio | grados Celsius |
| `estado_conexion` | boolean | — | {verdadero, falso} | Obligatorio | — |
| `consumo_kwh` | decimal | — | Numerico no negativo | Obligatorio | — |
| `origen` | enum | — | {borde local, agregado reportado} | Obligatorio | borde local, agregado reportado |
| `calidad_dato` | enum | — | {valida, interpolada, ausente} | Obligatorio | valida, interpolada, ausente |

### PARAMETRO_DESVIACION

| | |
|---|---|
| **Dominio** | DOM-REF |
| **Propietario del dato** | Jefatura de operaciones |
| **Clase de dato** | operacional versionado |
| **Sensibilidad** | interna |
| **Clase de retencion** | Series de temperatura reefer — 5 anos |
| **Fuente de verdad** | Terabyte, parametrizado y validado con el CLIENTE |
| **Diagrama** | D-04 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_parametro` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `version` | int | PK | Entero correlativo, empieza en 1 | Obligatorio | el parametro se versiona, nunca se sobrescribe |
| `banda_superior` | decimal | — | VACIO DECLARADO: grados Celsius, sin valor fijado por el caso (RN-11) | Obligatorio | sin valor fijado por el caso, RN-11 |
| `banda_inferior` | decimal | — | VACIO DECLARADO: grados Celsius, sin valor fijado por el caso (RN-11) | Obligatorio | sin valor fijado por el caso, RN-11 |
| `duracion_minima_minutos` | int | — | Minutos; acotada para no exceder los 5 min de RT-05.29 | Obligatorio | acotada para no exceder los 5 min de RF-REF |
| `vigencia_desde` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |
| `vigencia_hasta` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |
| `id_autor` | string | FK | Identificador de la entidad referenciada | Obligatorio | ref. D-07.PERSONA |

### ALARMA

| | |
|---|---|
| **Dominio** | DOM-REF |
| **Propietario del dato** | Operaciones patio refrigerado |
| **Clase de dato** | operacional |
| **Sensibilidad** | evidencia |
| **Clase de retencion** | Series de temperatura reefer — 5 anos |
| **Fuente de verdad** | Solucion, evaluada en el borde |
| **Diagrama** | D-04 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_alarma` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `tipo` | enum | — | {desviacion, desconexion, falla de tablero, ausencia de dato} | Obligatorio | desviacion, desconexion, falla de tablero, ausencia de dato |
| `severidad` | enum | — | {baja, media, alta, critica} | Obligatorio | baja, media, alta, critica |
| `tipo_objeto_origen` | enum | — | {conexion, toma, tablero} | Obligatorio | conexion, toma, tablero |
| `id_objeto_origen` | string | FK | Identificador de la entidad referenciada | Obligatorio | polimorfico, unica referencia al origen |
| `instante_evento_fisico` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |
| `instante_generacion` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | diferencia menor o igual a 5 min |
| `id_parametro_aplicado` | string | FK | Identificador de la entidad referenciada | Obligatorio | — |
| `version_parametro_aplicado` | int | FK | Entero correlativo, empieza en 1 | Obligatorio | — |
| `estado` | enum | — | {abierta, confirmada, escalada, cerrada} | Obligatorio | abierta, confirmada, escalada, cerrada |

### CONFIRMACION_ALARMA

| | |
|---|---|
| **Dominio** | DOM-REF |
| **Propietario del dato** | Operaciones patio refrigerado |
| **Clase de dato** | evidencia |
| **Sensibilidad** | personal |
| **Clase de retencion** | Series de temperatura reefer — 5 anos |
| **Fuente de verdad** | Persona identificada que confirma |
| **Diagrama** | D-04 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_alarma` | string | PK,FK | Identificador de la entidad referenciada | Obligatorio | — |
| `nivel_escalamiento` | int | PK | Numerico no negativo | Obligatorio | RN-08 |
| `id_persona` | string | FK | Identificador de la entidad referenciada | Obligatorio | ref. D-07.PERSONA |
| `instante` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |
| `canal` | enum | — | {consola, movil, mensajeria} | Obligatorio | consola, movil, mensajeria |


## D-05 · DOM-NAV — Nave y planificacion

### NAVIERA

| | |
|---|---|
| **Dominio** | DOM-NAV |
| **Propietario del dato** | Comercial |
| **Clase de dato** | maestro |
| **Sensibilidad** | interna |
| **Clase de retencion** | Maestro — mientras la entidad opere, mas el plazo del dato que referencia |
| **Fuente de verdad** | Naviera; la solucion mantiene el registro maestro |
| **Diagrama** | D-05 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_naviera` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `nombre` | string | — | Nombre comercial de la linea naviera | Obligatorio | — |
| `codigo_scac` | string | UK | Codigo de transportista de cuatro caracteres | Obligatorio | identificador de intercambio |

### NAVE

| | |
|---|---|
| **Dominio** | DOM-NAV |
| **Propietario del dato** | Planificacion |
| **Clase de dato** | maestro |
| **Sensibilidad** | interna |
| **Clase de retencion** | Maestro — mientras la entidad opere, mas el plazo del dato que referencia |
| **Fuente de verdad** | Naviera |
| **Diagrama** | D-05 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_nave` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `nombre` | string | — | Nombre de la nave | Obligatorio | — |
| `numero_imo` | string | UK | Numero de la Organizacion Maritima Internacional, siete digitos | Obligatorio | — |
| `id_naviera` | string | FK | Identificador de la entidad referenciada | Obligatorio | — |

### RECALADA

| | |
|---|---|
| **Dominio** | DOM-NAV |
| **Propietario del dato** | Planificacion |
| **Clase de dato** | operacional |
| **Sensibilidad** | interna |
| **Clase de retencion** | Movimientos y registros de operacion — 10 anos |
| **Fuente de verdad** | Solucion para la ejecucion; naviera para el anuncio |
| **Diagrama** | D-05 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_recalada` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `id_nave` | string | FK | Identificador de la entidad referenciada | Obligatorio | — |
| `ventana_confirmada` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | confirmacion con 72 h de antelacion, RF-NAV-03 |
| `instante_atraque_real` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |
| `instante_zarpe_real` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |
| `sitio_asignado` | string | — | {sitio 1, sitio 2, sitio 3; ampliable a un cuarto sitio por parametrizacion} | Obligatorio | — |
| `productividad_mov_hora` | decimal | — | Numerico no negativo | Derivado | derivado, RF-NAV-12 |

### PLAN_ESTIBA

| | |
|---|---|
| **Dominio** | DOM-NAV |
| **Propietario del dato** | Planificacion |
| **Clase de dato** | operacional versionado |
| **Sensibilidad** | comercial sensible |
| **Clase de retencion** | Movimientos y registros de operacion — 10 anos |
| **Fuente de verdad** | Naviera para el plano de estiba; la solucion para el plan de patio |
| **Diagrama** | D-05 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_plan` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `version` | int | PK | Entero correlativo, empieza en 1 | Obligatorio | el plan se versiona, nunca se sobrescribe |
| `id_recalada` | string | FK | Identificador de la entidad referenciada | Obligatorio | — |
| `estado` | enum | — | {propuesto, aprobado, corregido} | Obligatorio | propuesto, aprobado, corregido |
| `instante` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |
| `origen` | enum | — | {algoritmo, planificador} | Obligatorio | algoritmo, planificador |

### CORRECCION_PLAN

| | |
|---|---|
| **Dominio** | DOM-NAV |
| **Propietario del dato** | Planificacion |
| **Clase de dato** | operacional |
| **Sensibilidad** | interna |
| **Clase de retencion** | Movimientos y registros de operacion — 10 anos |
| **Fuente de verdad** | Planificador del terminal |
| **Diagrama** | D-05 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_correccion` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `id_plan` | string | FK | Identificador de la entidad referenciada | Obligatorio | — |
| `version_plan` | int | FK | Entero correlativo, empieza en 1 | Obligatorio | — |
| `motivo_estructurado` | enum | — | {catalogo cerrado, RF-NAV-08} | Obligatorio | catalogo cerrado, RF-NAV-08, no texto libre |
| `id_autor` | string | FK | Identificador de la entidad referenciada | Obligatorio | ref. D-07.PERSONA |
| `instante` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |

### REGLA_PLANIFICADOR

| | |
|---|---|
| **Dominio** | DOM-NAV |
| **Propietario del dato** | Planificacion |
| **Clase de dato** | conocimiento capturado |
| **Sensibilidad** | interna |
| **Clase de retencion** | Permanente — parametro de gobierno, no caduca |
| **Fuente de verdad** | Terabyte, derivada de las correcciones del planificador |
| **Diagrama** | D-05 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_regla` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `enunciado` | string | — | Enunciado de la regla en lenguaje de negocio | Obligatorio | — |
| `id_correccion_origen` | string | FK | Identificador de la entidad referenciada | Obligatorio | — |
| `vigencia_desde` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |
| `estado` | enum | — | {candidata, vigente, retirada} | Obligatorio | candidata, vigente, retirada |

### ASIGNACION_EQUIPO

| | |
|---|---|
| **Dominio** | DOM-NAV |
| **Propietario del dato** | Planificacion |
| **Clase de dato** | operacional |
| **Sensibilidad** | interna |
| **Clase de retencion** | Movimientos y registros de operacion — 10 anos |
| **Fuente de verdad** | Solucion |
| **Diagrama** | D-05 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_asignacion` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `id_recalada` | string | FK | Identificador de la entidad referenciada | Obligatorio | — |
| `id_equipo` | string | FK | Identificador de la entidad referenciada | Obligatorio | ref. D-02.EQUIPO_PATIO |
| `id_turno_operacional` | string | FK | Identificador de la entidad referenciada | Obligatorio | ref. D-07.TURNO_OPERACIONAL |
| `desde` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |
| `hasta` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |

### ORDEN_EMBARQUE

| | |
|---|---|
| **Dominio** | DOM-NAV |
| **Propietario del dato** | Comercial |
| **Clase de dato** | operacional |
| **Sensibilidad** | comercial sensible |
| **Clase de retencion** | Evidencia de hechos facturables — 6 anos |
| **Fuente de verdad** | Naviera |
| **Diagrama** | D-05 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_orden` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `id_recalada` | string | FK | Identificador de la entidad referenciada | Obligatorio | — |
| `id_naviera` | string | FK | Identificador de la entidad referenciada | Obligatorio | — |
| `estandar_mensaje` | string | — | Denominacion del mensaje sectorial de orden de embarque | Obligatorio | orden de embarque, RF-INT-02 |
| `version_contrato` | string | — | Version semantica del contrato de interfaz vigente | Obligatorio | ref. D-08.CONTRATO_INTERFAZ |
| `instante_recepcion` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |
| `id_correlacion` | string | — | Identificador de correlacion comun de extremo a extremo | Obligatorio | RT-05.19 |

### EMBARCADOR

| | |
|---|---|
| **Dominio** | DOM-NAV |
| **Propietario del dato** | Comercial |
| **Clase de dato** | maestro |
| **Sensibilidad** | interna |
| **Clase de retencion** | Maestro — mientras la entidad opere, mas el plazo del dato que referencia |
| **Fuente de verdad** | Solucion, con dato declarado por el embarcador |
| **Diagrama** | D-05 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_embarcador` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `razon_social` | string | — | Razon social registrada | Obligatorio | — |

### INSTRUCCION_EMBARQUE

| | |
|---|---|
| **Dominio** | DOM-NAV |
| **Propietario del dato** | Comercial |
| **Clase de dato** | operacional |
| **Sensibilidad** | comercial sensible |
| **Clase de retencion** | Evidencia de hechos facturables — 6 anos |
| **Fuente de verdad** | Embarcador o su agencia |
| **Diagrama** | D-05 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_instruccion` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `id_recalada` | string | FK | Identificador de la entidad referenciada | Obligatorio | — |
| `id_embarcador` | string | FK | Identificador de la entidad referenciada | Obligatorio | — |
| `canal` | enum | — | {portal estructurado, RF-POR-09} | Obligatorio | portal estructurado, RF-POR-09 |
| `estado_validacion` | enum | — | {aceptada, con discrepancia, rechazada} | Obligatorio | aceptada, con discrepancia, rechazada |
| `instante_presentacion` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |


## D-06a · DOM-FAC — Evidencia y facturacion

### CLIENTE

| | |
|---|---|
| **Dominio** | DOM-FAC |
| **Propietario del dato** | Comercial |
| **Clase de dato** | maestro |
| **Sensibilidad** | comercial sensible |
| **Clase de retencion** | Maestro — mientras la entidad opere, mas el plazo del dato que referencia |
| **Fuente de verdad** | Solucion; el ERP mantiene el maestro contable |
| **Diagrama** | D-06a |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_cliente` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `razon_social` | string | — | Razon social registrada | Obligatorio | — |
| `tipo` | enum | — | {exportador, importador, agencia, transportista, naviera} | Obligatorio | exportador, importador, agencia, transportista, naviera |

### HECHO_FACTURABLE

| | |
|---|---|
| **Dominio** | DOM-FAC |
| **Propietario del dato** | Comercial |
| **Clase de dato** | comercial sensible |
| **Sensibilidad** | comercial sensible |
| **Clase de retencion** | Evidencia de hechos facturables — 6 anos |
| **Fuente de verdad** | Solucion; el ERP emite el documento tributario |
| **Diagrama** | D-06a |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_hecho` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `id_visita` | string | FK | Identificador de la entidad referenciada | Obligatorio | ref. D-02.VISITA |
| `tipo` | enum | — | {transferencia, almacenaje, conexion, movimiento adicional, pesaje, inspeccion, zona peligrosa, servicio especial} | Obligatorio | transferencia, almacenaje, conexion, movimiento adicional, pesaje, inspeccion, zona peligrosa, servicio especial |
| `instante_ocurrencia` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | instante propio del hecho, RF-FAC-01 |
| `id_regla_aplicada` | string | FK | Identificador de la entidad referenciada | Obligatorio | — |
| `version_regla_aplicada` | int | FK | Entero correlativo, empieza en 1 | Obligatorio | FK compuesta, RF-FAC-02 |
| `monto_calculado` | decimal | — | Numerico no negativo | Obligatorio | — |
| `estado` | enum | — | {generado, entregado, objetado, compensado} | Obligatorio | generado, entregado, objetado, compensado |

### REGLA_TARIFARIA

| | |
|---|---|
| **Dominio** | DOM-FAC |
| **Propietario del dato** | Comercial |
| **Clase de dato** | comercial sensible versionado |
| **Sensibilidad** | comercial sensible |
| **Clase de retencion** | Evidencia de hechos facturables — 6 anos |
| **Fuente de verdad** | CLIENTE aprueba el tarifario; la solucion lo versiona |
| **Diagrama** | D-06a |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_regla` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `version` | int | PK | Entero correlativo, empieza en 1 | Obligatorio | la regla se versiona, nunca se sobrescribe |
| `tipo_hecho` | enum | — | {transferencia, almacenaje, conexion, movimiento adicional, pesaje, inspeccion, zona peligrosa, servicio especial} | Obligatorio | — |
| `vigencia_desde` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |
| `vigencia_hasta` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Condicional | — |
| `id_autor_cambio` | string | FK | Identificador de la entidad referenciada | Obligatorio | ref. D-07.PERSONA |

### EVIDENCIA

| | |
|---|---|
| **Dominio** | DOM-FAC |
| **Propietario del dato** | Comercial |
| **Clase de dato** | evidencia inmutable |
| **Sensibilidad** | evidencia |
| **Clase de retencion** | Evidencia de hechos facturables — 6 anos |
| **Fuente de verdad** | Objeto de origen en D-02, D-03 o D-04 |
| **Diagrama** | D-06a |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_evidencia` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `id_hecho` | string | FK | Identificador de la entidad referenciada | Obligatorio | — |
| `tipo` | enum | — | {evento, medicion, serie, lectura optica, firma} | Obligatorio | evento, medicion, serie, lectura optica, firma |
| `referencia_objeto_origen` | string | — | Puntero al objeto de origen en D-02, D-03 o D-04 | Obligatorio | puntero al objeto de D-02, D-03 o D-04 |
| `sello_integridad` | string | — | Resumen criptografico del contenido, inalterable | Obligatorio | inalterable, RT-16.07 |
| `instante_creacion` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |

### OBJECION

| | |
|---|---|
| **Dominio** | DOM-FAC |
| **Propietario del dato** | Comercial |
| **Clase de dato** | comercial sensible |
| **Sensibilidad** | comercial sensible |
| **Clase de retencion** | Evidencia de hechos facturables — 6 anos |
| **Fuente de verdad** | Cliente que la presenta |
| **Diagrama** | D-06a |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_objecion` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `id_hecho` | string | FK | Identificador de la entidad referenciada | Obligatorio | — |
| `id_cliente` | string | FK | Identificador de la entidad referenciada | Obligatorio | — |
| `motivo` | string | — | Motivo declarado por el cliente | Obligatorio | — |
| `estado` | enum | — | {abierta, en analisis, aceptada, rechazada} | Obligatorio | abierta, en analisis, aceptada, rechazada |
| `instante_presentacion` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |

### RESOLUCION_OBJECION

| | |
|---|---|
| **Dominio** | DOM-FAC |
| **Propietario del dato** | Comercial |
| **Clase de dato** | comercial sensible |
| **Sensibilidad** | comercial sensible |
| **Clase de retencion** | Evidencia de hechos facturables — 6 anos |
| **Fuente de verdad** | Terminal, con la evidencia invocada |
| **Diagrama** | D-06a |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_objecion` | string | PK,FK | Identificador de la entidad referenciada | Obligatorio | — |
| `resultado` | enum | — | {acogida, acogida parcial, rechazada} | Obligatorio | acogida, acogida parcial, rechazada |
| `id_evidencia_invocada` | string | FK | Identificador de la entidad referenciada | Obligatorio | — |
| `id_responsable` | string | FK | Identificador de la entidad referenciada | Obligatorio | ref. D-07.PERSONA |
| `instante` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |

### ENTREGA_ERP

| | |
|---|---|
| **Dominio** | DOM-FAC |
| **Propietario del dato** | Comercial y contabilidad |
| **Clase de dato** | comercial sensible |
| **Sensibilidad** | comercial sensible |
| **Clase de retencion** | Evidencia de hechos facturables — 6 anos |
| **Fuente de verdad** | ERP para el documento tributario; la solucion para el hecho |
| **Diagrama** | D-06a |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_hecho` | string | PK,FK | Identificador de la entidad referenciada | Obligatorio | — |
| `id_documento_tributario` | string | — | Folio del documento emitido por el ERP | Condicional | emitido por el ERP, nunca por la solucion |
| `instante_entrega` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |
| `estado_conciliacion` | enum | — | {pendiente, conciliada, con diferencia} | Obligatorio | pendiente, conciliada, con diferencia |


## D-06b · DOM-INS — Inspecciones de autoridad

### AUTORIDAD

| | |
|---|---|
| **Dominio** | DOM-INS |
| **Propietario del dato** | Cumplimiento normativo |
| **Clase de dato** | maestro |
| **Sensibilidad** | interna |
| **Clase de retencion** | Maestro — mientras la entidad opere, mas el plazo del dato que referencia |
| **Fuente de verdad** | Autoridad; la solucion mantiene el registro |
| **Diagrama** | D-06b |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_autoridad` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `tipo` | enum | — | {aduana, SAG, sanitaria, maritima} | Obligatorio | aduana, SAG, sanitaria, maritima |
| `nombre` | string | — | Denominacion oficial del organismo | Obligatorio | — |
| `id_contraparte` | string | FK | Identificador de la entidad referenciada | Obligatorio | ref. D-08.CONTRAPARTE |

### SOLICITUD_INSPECCION

| | |
|---|---|
| **Dominio** | DOM-INS |
| **Propietario del dato** | Cumplimiento normativo |
| **Clase de dato** | operacional |
| **Sensibilidad** | interna |
| **Clase de retencion** | Evidencia de hechos facturables — 6 anos |
| **Fuente de verdad** | Autoridad que emite la seleccion |
| **Diagrama** | D-06b |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_solicitud` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `id_visita` | string | FK | Identificador de la entidad referenciada | Obligatorio | ref. D-02.VISITA |
| `id_autoridad` | string | FK | Identificador de la entidad referenciada | Obligatorio | — |
| `instante_recepcion` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |
| `canal` | enum | — | {interfaz, canal asistido trazable} | Obligatorio | interfaz, canal asistido trazable |
| `id_correlacion` | string | — | Identificador de correlacion comun de extremo a extremo | Obligatorio | RT-05.19 |

### CITA_INSPECCION

| | |
|---|---|
| **Dominio** | DOM-INS |
| **Propietario del dato** | Cumplimiento normativo |
| **Clase de dato** | operacional |
| **Sensibilidad** | interna |
| **Clase de retencion** | Evidencia de hechos facturables — 6 anos |
| **Fuente de verdad** | Solucion, acordada con la autoridad |
| **Diagrama** | D-06b |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_cita` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `id_solicitud` | string | FK | Identificador de la entidad referenciada | Obligatorio | — |
| `hora_acordada` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |
| `hora_real_atencion` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |
| `cumplida_en_hora` | boolean | — | {verdadero, falso} | Derivado | derivado de las dos anteriores, RF-INS-07 |

### REMOCION_PROGRAMADA

| | |
|---|---|
| **Dominio** | DOM-INS |
| **Propietario del dato** | Jefatura de patio |
| **Clase de dato** | operacional |
| **Sensibilidad** | interna |
| **Clase de retencion** | Movimientos y registros de operacion — 10 anos |
| **Fuente de verdad** | Solucion |
| **Diagrama** | D-06b |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_remocion` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `id_cita` | string | FK | Identificador de la entidad referenciada | Obligatorio | — |
| `instante_programado` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |
| `id_movimiento` | string | FK | Identificador de la entidad referenciada | Obligatorio | ref. D-02.MOVIMIENTO, al ejecutarse |
| `estado` | enum | — | {programada, ejecutada, anulada} | Obligatorio | programada, ejecutada, anulada |

### ACTA_INSPECCION

| | |
|---|---|
| **Dominio** | DOM-INS |
| **Propietario del dato** | Cumplimiento normativo |
| **Clase de dato** | evidencia firmada |
| **Sensibilidad** | evidencia |
| **Clase de retencion** | Evidencia de hechos facturables — 6 anos |
| **Fuente de verdad** | Autoridad y terminal, con firma electronica |
| **Diagrama** | D-06b |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_acta` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `id_cita` | string | FK | Identificador de la entidad referenciada | Obligatorio | — |
| `resultado` | enum | — | {conforme, con observaciones, con retencion} | Obligatorio | conforme, con observaciones, con retencion |
| `id_firma` | string | FK | Identificador de la entidad referenciada | Obligatorio | firma electronica, RT-16.14 |
| `instante` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |

### RETENCION

| | |
|---|---|
| **Dominio** | DOM-INS |
| **Propietario del dato** | Cumplimiento normativo |
| **Clase de dato** | operacional |
| **Sensibilidad** | interna |
| **Clase de retencion** | Evidencia de hechos facturables — 6 anos |
| **Fuente de verdad** | Autoridad que la impone |
| **Diagrama** | D-06b |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_retencion` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `id_acta` | string | FK | Identificador de la entidad referenciada | Condicional | nulo si la retencion no proviene de un acta |
| `id_visita` | string | FK | Identificador de la entidad referenciada | Obligatorio | ref. D-02.VISITA |
| `id_autoridad` | string | FK | Identificador de la entidad referenciada | Obligatorio | — |
| `motivo` | string | — | Motivo declarado por la autoridad | Obligatorio | — |
| `vigencia_desde` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |
| `vigencia_hasta` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Condicional | nulo mientras la retencion sigue vigente |


## D-06c · DOM-EMI — Energia y emisiones

### CONSUMO_EQUIPO

| | |
|---|---|
| **Dominio** | DOM-EMI |
| **Propietario del dato** | Mantenimiento y sostenibilidad |
| **Clase de dato** | telemetria |
| **Sensibilidad** | interna |
| **Clase de retencion** | Telemetria de equipos — 2 anos en linea y agregacion posterior |
| **Fuente de verdad** | Instrumentacion del equipo |
| **Diagrama** | D-06c |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_consumo` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `id_equipo` | string | FK | Identificador de la entidad referenciada | Obligatorio | ref. D-02.EQUIPO_PATIO |
| `unidad` | enum | — | {litros de diesel, kWh} | Obligatorio | litros de diesel, kWh |
| `valor` | decimal | — | Numerico no negativo | Obligatorio | — |
| `instante_desde` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |
| `instante_hasta` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |
| `origen_medicion` | enum | — | {instrumentacion por equipo, estimacion declarada} | Obligatorio | instrumentacion por equipo, estimacion declarada |

### ATRIBUCION_CONSUMO

| | |
|---|---|
| **Dominio** | DOM-EMI |
| **Propietario del dato** | Sostenibilidad |
| **Clase de dato** | operacional |
| **Sensibilidad** | interna |
| **Clase de retencion** | Movimientos y registros de operacion — 10 anos |
| **Fuente de verdad** | Solucion, con criterio y version de algoritmo declarados |
| **Diagrama** | D-06c |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_consumo` | string | PK,FK | Identificador de la entidad referenciada | Obligatorio | — |
| `id_emision` | string | PK,FK | Identificador de la entidad referenciada | Obligatorio | — |
| `fraccion_atribuida` | decimal | — | 0 a 1 | Obligatorio | 0 a 1, suma 1 por consumo |
| `criterio` | enum | — | {movimientos ejecutados, tiempo de ciclo, masa movida}; valor adoptado: movimientos ejecutados (DEC-C4-01) | Obligatorio | movimientos ejecutados, tiempo de ciclo, masa movida |
| `version_algoritmo` | string | — | Version semantica del algoritmo de reparto | Obligatorio | obligatoria para reproducir el reparto |

### FACTOR_EMISION

| | |
|---|---|
| **Dominio** | DOM-EMI |
| **Propietario del dato** | Sostenibilidad |
| **Clase de dato** | maestro versionado |
| **Sensibilidad** | interna |
| **Clase de retencion** | Permanente — parametro de gobierno, no caduca |
| **Fuente de verdad** | Fuente metodologica externa (GLEC); la solucion la versiona |
| **Diagrama** | D-06c |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_factor` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `version` | int | PK | Entero correlativo, empieza en 1 | Obligatorio | — |
| `fuente` | string | — | Denominacion y version de la fuente metodologica | Obligatorio | GLEC v3.2 |
| `alcance` | enum | — | {1, 2, 3} | Obligatorio | 1, 2, 3 |
| `valor` | decimal | — | Numerico no negativo | Obligatorio | — |
| `unidad` | string | — | kg CO2e por unidad de consumo | Obligatorio | kg CO2e por unidad de consumo |
| `vigencia_desde` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |

### EMISION_CONTENEDOR

| | |
|---|---|
| **Dominio** | DOM-EMI |
| **Propietario del dato** | Sostenibilidad |
| **Clase de dato** | operacional |
| **Sensibilidad** | interna |
| **Clase de retencion** | Movimientos y registros de operacion — 10 anos |
| **Fuente de verdad** | Solucion, verificable por tercero |
| **Diagrama** | D-06c |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_emision` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `id_visita` | string | FK | Identificador de la entidad referenciada | Obligatorio | ref. D-02.VISITA |
| `consumo_atribuido` | decimal | — | Numerico no negativo | Derivado | derivado de ATRIBUCION_CONSUMO |
| `id_factor` | string | FK | Identificador de la entidad referenciada | Obligatorio | — |
| `version_factor` | int | FK | Entero correlativo, empieza en 1 | Obligatorio | FK compuesta |
| `valor_emision` | decimal | — | kg | Obligatorio | kg CO2e |
| `metodologia` | string | — | Denominacion de la norma y de la guia aplicadas | Obligatorio | ISO 14083 via GLEC v3.2 |
| `instante_calculo` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |


## D-07 · DOM-ACC — Acceso e identidad

### PERSONA

| | |
|---|---|
| **Dominio** | DOM-ACC |
| **Propietario del dato** | Personas y proteccion portuaria |
| **Clase de dato** | personal |
| **Sensibilidad** | personal |
| **Clase de retencion** | Registros de acceso de personas — 5 anos |
| **Fuente de verdad** | Solucion, con dato acreditado por la organizacion de origen |
| **Diagrama** | D-07 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_persona` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `tipo` | enum | — | {propio, eventual, conductor, visita, inspector} | Obligatorio | propio, eventual, conductor, visita, inspector |
| `documento_identidad` | string | UK | Documento nacional de identidad o pasaporte; cifrado a nivel de campo | Obligatorio | dato personal, cifrado de campo, unico registro del dato, RT-11.10 y RT-05.09 |
| `organizacion` | string | — | Texto acotado | Obligatorio | — |

### HABILITACION

| | |
|---|---|
| **Dominio** | DOM-ACC |
| **Propietario del dato** | Personas |
| **Clase de dato** | personal |
| **Sensibilidad** | personal |
| **Clase de retencion** | Registros de acceso de personas — 5 anos |
| **Fuente de verdad** | Organismo acreditador; la solucion registra la vigencia |
| **Diagrama** | D-07 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_habilitacion` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `id_persona` | string | FK | Identificador de la entidad referenciada | Obligatorio | — |
| `tipo` | string | — | {catalogo de habilitaciones del plan de proteccion portuaria} | Obligatorio | — |
| `vigencia_desde` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |
| `vigencia_hasta` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |
| `vigente` | boolean | — | {verdadero, falso} | Derivado | derivado, verificado al ingreso, RF-ACC-05 |

### TURNO_OPERACIONAL

| | |
|---|---|
| **Dominio** | DOM-ACC |
| **Propietario del dato** | Jefatura de operaciones |
| **Clase de dato** | operacional |
| **Sensibilidad** | interna |
| **Clase de retencion** | Movimientos y registros de operacion — 10 anos |
| **Fuente de verdad** | Solucion |
| **Diagrama** | D-07 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_turno_operacional` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `fecha` | date | — | Fecha calendario | Obligatorio | — |
| `jornada` | enum | — | {tres turnos, operacion 24x7} | Obligatorio | tres turnos, operacion 24x7 |
| `instante_cierre` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | corte para la conciliacion de D-08 |

### NOMBRADA

| | |
|---|---|
| **Dominio** | DOM-ACC |
| **Propietario del dato** | Jefatura de operaciones |
| **Clase de dato** | personal |
| **Sensibilidad** | personal |
| **Clase de retencion** | Registros de acceso de personas — 5 anos |
| **Fuente de verdad** | Solucion, publicada por la jefatura de turno |
| **Diagrama** | D-07 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_nombrada` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `id_turno_operacional` | string | FK | Identificador de la entidad referenciada | Obligatorio | — |
| `instante_publicacion` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |
| `personas_asignadas` | int | — | Numerico no negativo | Derivado | derivado, hasta 380 eventuales por turno |

### ASIGNACION_NOMBRADA

| | |
|---|---|
| **Dominio** | DOM-ACC |
| **Propietario del dato** | Jefatura de operaciones |
| **Clase de dato** | personal |
| **Sensibilidad** | personal |
| **Clase de retencion** | Registros de acceso de personas — 5 anos |
| **Fuente de verdad** | Solucion |
| **Diagrama** | D-07 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_nombrada` | string | PK,FK | Identificador de la entidad referenciada | Obligatorio | — |
| `id_persona` | string | PK,FK | Identificador de la entidad referenciada | Obligatorio | — |
| `funcion` | string | — | {catalogo de funciones operacionales del turno} | Obligatorio | — |

### CREDENCIAL_TEMPORAL

| | |
|---|---|
| **Dominio** | DOM-ACC |
| **Propietario del dato** | Proteccion portuaria |
| **Clase de dato** | personal |
| **Sensibilidad** | personal |
| **Clase de retencion** | Registros de acceso de personas — 5 anos |
| **Fuente de verdad** | Solucion |
| **Diagrama** | D-07 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_credencial` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `id_nombrada` | string | FK | Identificador de la entidad referenciada | Obligatorio | FK compuesta hacia ASIGNACION_NOMBRADA |
| `id_persona` | string | FK | Identificador de la entidad referenciada | Obligatorio | — |
| `vigencia_desde` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |
| `vigencia_hasta` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | expiracion automatica, RF-ACC-02 |
| `medio` | enum | — | {tarjeta de proximidad, codigo temporal, aplicacion movil} | Obligatorio | sin biometria obligatoria, RF-ACC-04 |

### ZONA_RECINTO

| | |
|---|---|
| **Dominio** | DOM-ACC |
| **Propietario del dato** | Proteccion portuaria |
| **Clase de dato** | maestro |
| **Sensibilidad** | interna |
| **Clase de retencion** | Maestro — mientras la entidad opere, mas el plazo del dato que referencia |
| **Fuente de verdad** | Plan de proteccion de la instalacion portuaria |
| **Diagrama** | D-07 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_zona` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `nombre` | string | — | Denominacion de la zona en el plan de proteccion | Obligatorio | — |
| `nivel_proteccion` | enum | — | {niveles 1, 2 y 3 del plan de proteccion de la instalacion portuaria} | Obligatorio | segun el plan de proteccion de la instalacion |

### ZONA_HABILITADA

| | |
|---|---|
| **Dominio** | DOM-ACC |
| **Propietario del dato** | Proteccion portuaria |
| **Clase de dato** | personal |
| **Sensibilidad** | personal |
| **Clase de retencion** | Registros de acceso de personas — 5 anos |
| **Fuente de verdad** | Solucion |
| **Diagrama** | D-07 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_credencial` | string | PK,FK | Identificador de la entidad referenciada | Obligatorio | — |
| `id_zona` | string | PK,FK | Identificador de la entidad referenciada | Obligatorio | — |

### EVENTO_ACCESO

| | |
|---|---|
| **Dominio** | DOM-ACC |
| **Propietario del dato** | Proteccion portuaria |
| **Clase de dato** | personal |
| **Sensibilidad** | personal |
| **Clase de retencion** | Registros de acceso de personas — 5 anos |
| **Fuente de verdad** | Control de acceso en el borde |
| **Diagrama** | D-07 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_evento` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `id_persona` | string | FK | Identificador de la entidad referenciada | Obligatorio | — |
| `id_zona` | string | FK | Identificador de la entidad referenciada | Obligatorio | — |
| `tipo` | enum | — | {ingreso, egreso} | Obligatorio | ingreso, egreso |
| `instante` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | instante del hecho en el borde |
| `instante_sincronizacion` | timestamptz | — | Instante con zona horaria; posterior al hecho si hubo operacion sin conectividad | Condicional | posterior si se registro sin conectividad |
| `medio_verificacion` | string | — | {credencial de proximidad, codigo temporal, verificacion manual} | Obligatorio | — |
| `registrado_sin_conectividad` | boolean | — | {verdadero, falso} | Obligatorio | RF-ACC-08 |

### CONSULTA_SENSIBLE

| | |
|---|---|
| **Dominio** | DOM-ACC |
| **Propietario del dato** | Seguridad de la informacion |
| **Clase de dato** | auditoria |
| **Sensibilidad** | auditoria |
| **Clase de retencion** | Auditoria — el plazo de la clase auditada |
| **Fuente de verdad** | Solucion, registro automatico no editable |
| **Diagrama** | D-07 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_consulta` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `id_persona` | string | FK | Identificador de la entidad referenciada | Obligatorio | — |
| `tipo_dato` | enum | — | {ubicacion de contenedor, informacion comercial, dato personal} | Obligatorio | ubicacion de contenedor, informacion comercial, dato personal |
| `objeto_consultado` | string | — | Identificador del objeto sobre el que se consulto | Obligatorio | — |
| `instante` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |
| `dispositivo` | string | — | Identificador del dispositivo desde el que se consulto | Obligatorio | RT-16.09 y RT-05.03 |


## D-08 · DOM-INT — Integracion, autoridad y auditoria

### CONTRAPARTE

| | |
|---|---|
| **Dominio** | DOM-INT |
| **Propietario del dato** | Tecnologias de informacion |
| **Clase de dato** | maestro |
| **Sensibilidad** | interna |
| **Clase de retencion** | Maestro — mientras la entidad opere, mas el plazo del dato que referencia |
| **Fuente de verdad** | Solucion |
| **Diagrama** | D-08 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_contraparte` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `tipo` | enum | — | {naviera, autoridad, ferroviario, concedente, TOS, ERP, periferia} | Obligatorio | naviera, autoridad, ferroviario, concedente, TOS, ERP, periferia |
| `nombre` | string | — | Denominacion de la contraparte | Obligatorio | — |
| `estado_contrato` | enum | — | {confirmado, POR LEVANTAR} | Obligatorio | confirmado, POR LEVANTAR |

### CONTRATO_INTERFAZ

| | |
|---|---|
| **Dominio** | DOM-INT |
| **Propietario del dato** | Tecnologias de informacion |
| **Clase de dato** | maestro versionado |
| **Sensibilidad** | interna |
| **Clase de retencion** | Vigencia del contrato mas el preaviso de obsolescencia de 6 meses |
| **Fuente de verdad** | Acuerdo con la contraparte; la solucion lo versiona |
| **Diagrama** | D-08 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_contrato` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `version_semantica` | string | PK | Identificador unico asignado por la solucion | Obligatorio | RT-05.17, el contrato se versiona |
| `id_contraparte` | string | FK | Identificador de la entidad referenciada | Obligatorio | — |
| `estandar` | string | — | Denominacion del estandar sectorial de intercambio | Obligatorio | — |
| `modo` | enum | — | {sincrono, asincrono} | Obligatorio | sincrono, asincrono |
| `vigencia_desde` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |
| `obsolescencia_anunciada` | timestamptz | — | Instante con zona horaria; preaviso minimo de 6 meses | Condicional | preaviso minimo de 6 meses |

### MENSAJE

| | |
|---|---|
| **Dominio** | DOM-INT |
| **Propietario del dato** | Tecnologias de informacion |
| **Clase de dato** | operacional |
| **Sensibilidad** | segun la clase que transporta |
| **Clase de retencion** | La de la clase de informacion que transporta |
| **Fuente de verdad** | Contraparte emisora, segun direccion |
| **Diagrama** | D-08 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_mensaje` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `id_contrato` | string | FK | Identificador de la entidad referenciada | Obligatorio | — |
| `version_contrato` | string | FK | Identificador de la entidad referenciada | Obligatorio | FK compuesta |
| `direccion` | enum | — | {entrada, salida} | Obligatorio | entrada, salida |
| `instante` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |
| `id_correlacion` | string | — | Identificador de correlacion comun de extremo a extremo | Obligatorio | comun de extremo a extremo, RT-05.19 |
| `clave_idempotencia` | string | UK | Clave unica que descarta el reproceso de un mismo mensaje | Obligatorio | descarta el reproceso de un mismo mensaje |
| `estado` | enum | — | {recibido, procesado, en cola, en DLQ} | Obligatorio | recibido, procesado, en cola, en DLQ |
| `reintentos` | int | — | Numerico no negativo | Obligatorio | — |

### DOMINIO_INFORMACION

| | |
|---|---|
| **Dominio** | DOM-INT |
| **Propietario del dato** | Gobierno del dato |
| **Clase de dato** | maestro |
| **Sensibilidad** | interna |
| **Clase de retencion** | Permanente — parametro de gobierno, no caduca |
| **Fuente de verdad** | Terabyte |
| **Diagrama** | D-08 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_dominio` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `nombre` | string | — | {DOM-OPS, DOM-PAT, DOM-GAT, DOM-REF, DOM-NAV, DOM-INS, DOM-FAC, DOM-ACC, DOM-EMI, DOM-INT} | Obligatorio | los diez dominios de D-01 |

### ZONA_OPERATIVA

| | |
|---|---|
| **Dominio** | DOM-INT |
| **Propietario del dato** | Gobierno del dato |
| **Clase de dato** | maestro |
| **Sensibilidad** | interna |
| **Clase de retencion** | Permanente — parametro de gobierno, no caduca |
| **Fuente de verdad** | Terabyte y Celula 3, POR NOMBRAR |
| **Diagrama** | D-08 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_zona` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `nombre` | string | — | VACIO DECLARADO: por nombrar en conjunto con la Celula 3 | Obligatorio | POR NOMBRAR en conjunto con la Celula 3 |

### FASE_TRANSICION

| | |
|---|---|
| **Dominio** | DOM-INT |
| **Propietario del dato** | Gobierno del dato |
| **Clase de dato** | maestro |
| **Sensibilidad** | interna |
| **Clase de retencion** | Permanente — parametro de gobierno, no caduca |
| **Fuente de verdad** | Terabyte |
| **Diagrama** | D-08 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_fase` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `nombre` | enum | — | {previo al corte, validacion paralela, posterior al corte} | Obligatorio | previo al corte, validacion paralela, posterior al corte |

### ASIGNACION_AUTORIDAD

| | |
|---|---|
| **Dominio** | DOM-INT |
| **Propietario del dato** | Gobierno del dato |
| **Clase de dato** | gobierno del dato |
| **Sensibilidad** | interna |
| **Clase de retencion** | Permanente — parametro de gobierno, no caduca |
| **Fuente de verdad** | Terabyte, aprobada por el CLIENTE |
| **Diagrama** | D-08 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_asignacion` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `id_dominio` | string | FK,UK | Identificador de la entidad referenciada | Obligatorio | — |
| `id_zona` | string | FK,UK | Identificador de la entidad referenciada | Obligatorio | — |
| `id_fase` | string | FK,UK | Identificador de la entidad referenciada | Obligatorio | — |
| `vigencia_desde` | timestamptz | UK | Instante con zona horaria; operacion 24x7 | Obligatorio | la terna es unica en cada instante |
| `sistema_autoritativo` | enum | — | {TOS 2012, solucion} | Obligatorio | TOS 2012, solucion |
| `vigencia_hasta` | timestamptz | — | Instante con zona horaria; nulo mientras la asignacion rige | Condicional | — |

### TRANSFERENCIA_AUTORIDAD

| | |
|---|---|
| **Dominio** | DOM-INT |
| **Propietario del dato** | Gobierno del dato |
| **Clase de dato** | operacional |
| **Sensibilidad** | interna |
| **Clase de retencion** | Movimientos y registros de operacion — 10 anos |
| **Fuente de verdad** | Sistema con autoridad en la zona de origen |
| **Diagrama** | D-08 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_transferencia` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `id_visita` | string | FK | Identificador de la entidad referenciada | Obligatorio | ref. D-02.VISITA |
| `id_asignacion` | string | FK | Identificador de la entidad referenciada | Obligatorio | — |
| `zona_origen` | string | FK | Identificador de la entidad referenciada | Obligatorio | — |
| `zona_destino` | string | FK | Identificador de la entidad referenciada | Obligatorio | — |
| `clave_idempotencia` | string | UK | Clave unica que impide aplicar dos veces la misma transferencia | Obligatorio | — |
| `numero_secuencia` | int | — | Numerico no negativo | Obligatorio | ordena las transferencias de una misma visita |
| `estado` | enum | — | {emitido, confirmado, fallido} | Obligatorio | emitido, confirmado, fallido |
| `instante` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |

### DIVERGENCIA_CONCILIACION

| | |
|---|---|
| **Dominio** | DOM-INT |
| **Propietario del dato** | Gobierno del dato |
| **Clase de dato** | operacional |
| **Sensibilidad** | interna |
| **Clase de retencion** | Movimientos y registros de operacion — 10 anos |
| **Fuente de verdad** | Solucion, por comparacion de ambos registros |
| **Diagrama** | D-08 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_divergencia` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `universo` | enum | — | {inventario, movimientos, gate, hechos} | Obligatorio | inventario, movimientos, gate, hechos |
| `id_turno_operacional` | string | FK | Identificador de la entidad referenciada | Obligatorio | ref. D-07.TURNO_OPERACIONAL |
| `clasificacion` | enum | — | {desfase, nuevo correcto, nuevo incorrecto, no explicada} | Obligatorio | desfase, nuevo correcto, nuevo incorrecto, no explicada |
| `ventana_horas` | int | — | Horas, entero no negativo | Obligatorio | 48 para posicion, 24 para gate |
| `estado` | enum | — | {abierta, explicada, cerrada} | Obligatorio | abierta, explicada, cerrada |
| `instante_deteccion` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |

### VERIFICACION_FISICA

| | |
|---|---|
| **Dominio** | DOM-INT |
| **Propietario del dato** | Jefatura de patio |
| **Clase de dato** | evidencia |
| **Sensibilidad** | evidencia |
| **Clase de retencion** | Movimientos y registros de operacion — 10 anos |
| **Fuente de verdad** | Persona que ejecuta el barrido fisico |
| **Diagrama** | D-08 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_verificacion` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `id_divergencia` | string | FK | Identificador de la entidad referenciada | Obligatorio | — |
| `id_bloque` | string | FK | Identificador de la entidad referenciada | Obligatorio | ref. D-02.BLOQUE |
| `id_turno_operacional` | string | FK | Identificador de la entidad referenciada | Obligatorio | ref. D-07.TURNO_OPERACIONAL |
| `resultado` | enum | — | {confirma, corrige, no concluyente} | Obligatorio | confirma, corrige, no concluyente |
| `instante` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |

### REGISTRO_AUDITORIA

| | |
|---|---|
| **Dominio** | DOM-INT |
| **Propietario del dato** | Seguridad de la informacion |
| **Clase de dato** | auditoria inalterable |
| **Sensibilidad** | auditoria |
| **Clase de retencion** | Auditoria — el plazo de la clase auditada |
| **Fuente de verdad** | Solucion, registro automatico no editable |
| **Diagrama** | D-08 |


| Atributo | Tipo | Clave | Dominio de valores | Obligatoriedad | Origen y nota |
|---|---|---|---|---|---|
| `id_registro` | string | PK | Identificador unico asignado por la solucion | Obligatorio | — |
| `entidad_afectada` | string | — | Nombre de la entidad del modelo conceptual | Obligatorio | — |
| `id_objeto_afectado` | string | — | Identificador del objeto alterado | Obligatorio | — |
| `operacion` | enum | — | {alta, modificacion, baja, consulta} | Obligatorio | alta, modificacion, baja, consulta |
| `id_persona` | string | FK | Identificador de la entidad referenciada | Obligatorio | ref. D-07.PERSONA |
| `instante` | timestamptz | — | Instante con zona horaria; operacion 24x7 | Obligatorio | — |
| `dispositivo` | string | — | Identificador del dispositivo de origen de la operacion | Obligatorio | — |
| `valores_anteriores` | string | — | Documento estructurado con el estado previo | Condicional | — |
| `valores_posteriores` | string | — | Documento estructurado con el estado resultante | Condicional | — |
| `sello_inalterabilidad` | string | — | Resumen criptografico encadenado al registro previo | Obligatorio | encadenado al registro previo, RT-16.07 |

---

# 4. Catalogo de campos sujetos a cifrado a nivel de campo

`CP, Cap. 15, RT-11.10` exige cifrado a nivel de campo para tres familias: los datos personales de trabajadores propios, eventuales, conductores y visitantes; la informacion comercial sensible de clientes, incluidas tarifas negociadas y volumenes; y los datos que permitan inferir el contenido de valor de un contenedor o su ruta. `RNF-SEG-05` compromete el 100 % de los campos identificados como sensibles.

Este catalogo es esa lista. **Cierra el pendiente A-12 y responde la consulta C-02 dirigida a Celula 2**: si el catalogo no existia en el catalogo de requerimientos, existe ahora derivado del diccionario.

## 4.1 Datos personales

| Atributo | Entidad | Por que |
|---|---|---|
| `documento_identidad` | `PERSONA` | dato identificatorio de persona natural; unico registro del dato en el modelo |
| `organizacion` | `PERSONA` | permite reidentificar a un eventual por su empleador |
| `tipo` | `PERSONA` | distingue propio, eventual, conductor, visita e inspector |
| `id_persona` | `CONDUCTOR` | vincula a la persona natural con su rol de conductor |
| `id_persona` | `ASIGNACION_NOMBRADA` | revela quien trabajo en cada turno |
| `id_persona` | `CREDENCIAL_TEMPORAL` | asocia credencial y persona |
| `id_persona`, `id_zona`, `instante` | `EVENTO_ACCESO` | reconstruye el movimiento de una persona dentro del recinto |
| `id_persona`, `objeto_consultado`, `dispositivo` | `CONSULTA_SENSIBLE` | revela que consulto cada persona |
| `id_persona`, `dispositivo` | `REGISTRO_AUDITORIA` | atribuye cada operacion a una persona identificada |
| `tipo`, `vigencia_desde`, `vigencia_hasta` | `HABILITACION` | acredita condiciones personales |

## 4.2 Informacion comercial sensible

| Atributo | Entidad | Por que |
|---|---|---|
| `monto_calculado` | `HECHO_FACTURABLE` | valor cobrado a un cliente identificable |
| `id_regla_aplicada`, `version_regla_aplicada` | `HECHO_FACTURABLE` | permite inferir la tarifa negociada |
| todos los atributos | `REGLA_TARIFARIA` | es el tarifario, incluidas vigencias y excepciones |
| `razon_social`, `tipo` | `CLIENTE` | asocia volumen operado a un cliente |
| `motivo` | `OBJECION` | contiene la posicion comercial del cliente |
| `id_cliente` | `VISITA` | asocia carga y cliente |
| `consigna_temperatura` | `CONEXION_REEFER` | revela la naturaleza de la carga |
| `estandar_mensaje`, `id_naviera` | `ORDEN_EMBARQUE` | revela el vinculo comercial naviera-cliente |
| `id_embarcador` | `INSTRUCCION_EMBARQUE` | idem |
| todos los atributos | `PLAN_ESTIBA` | revela la composicion de la carga de la nave |

## 4.3 Datos que permiten inferir el contenido de valor o la ruta

| Atributo | Entidad | Por que |
|---|---|---|
| `id_celda`, `vigente_desde` | `POSICION_VIGENTE` | **es la ubicacion del contenedor**; el caso la califica expresamente como sensible por seguridad de la carga |
| `celda_origen`, `celda_destino` | `MOVIMIENTO` | reconstruye la trayectoria dentro del recinto |
| `celda_propuesta` | `ASIGNACION_POSICION` | anticipa la ubicacion futura |
| `celda_destino` | `INSTRUCCION_DESTINO` | idem, en el gate |
| `clase_imdg` | `CONTENEDOR` | declara mercancia peligrosa |
| `codigo_leido` | `LECTURA_OPTICA` | asocia contenedor y punto de paso con instante |
| `id_visita`, `sentido` | `MOVIMIENTO_TERRESTRE` | revela quien retira que carga y cuando |
| `posicion_candidata` | `TAREA_VERIFICACION` | revela ubicacion presunta |

## 4.4 Consecuencia para el § 5.10

Ocho de estos atributos son, a la vez, **clave de acceso indexada** en el catalogo de operaciones criticas: `POSICION_VIGENTE.id_celda`, `MOVIMIENTO.celda_origen` y `celda_destino`, `CONTENEDOR.clase_imdg`, `LECTURA_OPTICA.codigo_leido`, `CONDUCTOR.id_persona`, `EVENTO_ACCESO.id_persona` y `HECHO_FACTURABLE.id_regla_aplicada`.

Un cifrado que impida la busqueda por igualdad sobre esos campos hace inalcanzables los umbrales de `RT-09.01`. **Célula 3 respondió para I1 en D1 B4.3:** valor cifrado aleatoriamente más token de igualdad con clave y contexto separados para celdas, clase IMDG y lectura óptica; identificador sustituto opaco para persona y regla tarifaria; o consulta confinada al servicio propietario si la prueba de fuga falla. Los ocho casos conservan propietario, prueba y estado condicionado; no se adopta cifrado determinista directo ni una copia en claro.

---

# 5. Atributos derivados

`RT-05.04` exige validacion en el punto de captura. Un atributo derivado no se valida en captura: se recalcula y se contrasta con su formula. Distinguirlos es lo que impide que alguien los edite a mano y rompa la trazabilidad que exige `RT-05.03`.

| Atributo | Se calcula a partir de | Origen |
|---|---|---|
| `CONDICION_LIBERACION.liberado` | la conjuncion de las cinco condiciones | `RN-06` |
| `CONDUCTOR.habilitacion_vigente` | la habilitacion vigente de la persona | `RF-ACC-05` |
| `TURNO_CAMION.estadia_minutos` | los eventos de barrera de entrada y salida | `RF-GAT-12` |
| `PESAJE_VGM.desviacion` | masa declarada y masa verificada | `RN-05` |
| `CONEXION_REEFER.minutos_desconectado_acumulados` | la serie de estado de conexion | `RN-10` |
| `RECALADA.productividad_mov_hora` | los movimientos de muelle y el tiempo de operacion | `RF-NAV-12` |
| `CITA_INSPECCION.cumplida_en_hora` | hora acordada y hora real de atencion | `RF-INS-07` |
| `EMISION_CONTENEDOR.consumo_atribuido` | la suma de las atribuciones de consumo | `RF-EMI-03` |
| `HABILITACION.vigente` | las fechas de vigencia contra el instante de consulta | `RF-ACC-05` |
| `NOMBRADA.personas_asignadas` | el recuento de asignaciones de la nombrada | `RF-ACC-01` |

Los cuatro primeros sostienen indicadores comprometidos: estadia del camion, cumplimiento de la hora de inspeccion, productividad de grua y cadena de frio. Ninguno se captura, todos se producen — que es la exigencia de `CP, Cap. 10, restriccion 14`.

---

# 6. Verificacion de la retencion

`RNF-CUM-14` prohibe el plazo uniforme. Esta tabla verifica que las 80 entidades tienen clase asignada y que ninguna clase quedo vacia.

| Clase de retencion | Entidades | Cuales |
|---|---:|---|
| Movimientos y operacion — 10 anos | 24 | ASIGNACION_EQUIPO, ASIGNACION_POSICION, ATRIBUCION_CONSUMO, CITA, CONDICION_DINAMICA, CONDICION_LIBERACION, CORRECCION_PLAN, DIVERGENCIA_CONCILIACION, EMISION_CONTENEDOR, EVENTO_GATE, EXCEPCION_GATE, INSTRUCCION_DESTINO, MOVIMIENTO, MOVIMIENTO_TERRESTRE, PLAN_ESTIBA, POSICION_VIGENTE, RECALADA, REMOCION_PROGRAMADA, TAREA_VERIFICACION, TRANSFERENCIA_AUTORIDAD, TURNO_CAMION, TURNO_OPERACIONAL, VERIFICACION_FISICA, VISITA |
| Evidencia facturable — 6 anos | 15 | ACTA_INSPECCION, CITA_INSPECCION, CONEXION_REEFER, CUSTODIA, DOCUMENTO_TRANSPORTE, ENTREGA_ERP, EVIDENCIA, HECHO_FACTURABLE, INSTRUCCION_EMBARQUE, OBJECION, ORDEN_EMBARQUE, REGLA_TARIFARIA, RESOLUCION_OBJECION, RETENCION, SOLICITUD_INSPECCION |
| Temperatura reefer — 5 anos | 4 | ALARMA, CONFIRMACION_ALARMA, MUESTRA_TEMPERATURA, PARAMETRO_DESVIACION |
| Verificacion de masa bruta — 5 anos | 1 | PESAJE_VGM |
| Imagenes de reconocimiento — 12 meses | 1 | LECTURA_OPTICA |
| Accesos de personas — 5 anos | 8 | ASIGNACION_NOMBRADA, CONDUCTOR, CREDENCIAL_TEMPORAL, EVENTO_ACCESO, HABILITACION, NOMBRADA, PERSONA, ZONA_HABILITADA |
| Telemetria de equipos — 2 anos en linea | 1 | CONSUMO_EQUIPO |
| Auditoria — plazo de la clase auditada | 2 | CONSULTA_SENSIBLE, REGISTRO_AUDITORIA |
| Maestro | 16 | AUTORIDAD, BLOQUE, CAMION, CELDA, CLIENTE, CONTENEDOR, CONTRAPARTE, EMBARCADOR, EQUIPO_PATIO, NAVE, NAVIERA, PUNTO_DE_PASO, TABLERO, TOMA_REEFER, TRANSPORTISTA, ZONA_RECINTO |
| Permanente | 6 | ASIGNACION_AUTORIDAD, DOMINIO_INFORMACION, FACTOR_EMISION, FASE_TRANSICION, REGLA_PLANIFICADOR, ZONA_OPERATIVA |
| Vigencia del contrato + 6 meses | 1 | CONTRATO_INTERFAZ |
| La de la clase que transporta | 1 | MENSAJE |
| **Total** | **80** | — |

**Dos observaciones que conviene declarar en el texto del § 5.12.**

La primera: `MUESTRA_TEMPERATURA` cae en dos plazos a la vez. La serie que respalda la cadena de frio se retiene 5 anos (`RNF-CUM-08`), pero la telemetria granular solo vive 2 anos en linea antes de agregarse. La entidad se retiene por el plazo mas exigente y la agregacion opera sobre la resolucion, no sobre la existencia del dato.

La segunda: la retencion de `CONDUCTOR` y de `PERSONA` es la misma —5 anos desde el ultimo acceso— precisamente porque ahora el dato personal esta una sola vez. Antes de la correccion de la version 2.1 eran dos plazos independientes sobre el mismo dato, que es la clase de incoherencia que una auditoria de proteccion de datos encuentra primero.

---

# 7. Vacios declarados

| Marca | Atributo | Que falta | Responsable |
|---|---|---|---|
| `VACIO DECLARADO` | `PARAMETRO_DESVIACION.banda_superior` y `banda_inferior` | los valores en grados Celsius de la banda de desviacion de temperatura. El caso no los entrega y `RN-11` los deja parametrizables | Celula 2 y CLIENTE — consulta C-03 |
| `VACIO DECLARADO` | `ZONA_OPERATIVA.nombre` | los nombres de las zonas que estructuran la autoridad del dato | Celula 3 — consulta B-01 |
| — *cerrado* | `ATRIBUCION_CONSUMO.criterio` | **Resuelto por `DEC-C4-01`**: se adopta el reparto por movimientos ejecutados. Es el unico criterio con dato duro del CLIENTE detras, no exige instrumentacion adicional y es el unico que un verificador externo puede comprobar contra cifras que el terminal ya reporta al concedente | Celula 4 — cerrado |

Con `DEC-C4-01` cerrado y A3 recibido, la estructura de zonas/fases queda definida y la segmentación física exacta permanece parametrizada. El vacío sustantivo del diccionario es el valor de la banda de desviación (`PEN-09`, Célula 2 y CLIENTE); no se inventa.

Dos entidades quedan ademas **sujetas a confirmacion** sin bloquear el diccionario: `CONDICION_DINAMICA`, porque `RF-PAT-07` sigue declarado pendiente de validacion interna en Celula 2, y `MOVIMIENTO` en su atributo `id_recalada`, porque el evento del que se deriva el movimiento de muelle sigue sin declararse — las seis gruas de muelle no estan en el universo instrumentable.

---

# 8. Integracion en el documento LaTeX

El diccionario completo va al **Anexo A.2**. Por su extension —80 fichas— conviene componerlo con la misma disciplina que los diagramas:

1. Las fichas de gobierno de cada entidad y sus tablas de atributos se generan desde este archivo, no se transcriben a mano.
2. Las tablas de atributos son de seis columnas y algunas superan la pagina: se componen con `longtable` y encabezado repetido, como las del Anexo F, no con `tabularx`.
3. Las secciones 4, 5, 6 y 7 de este documento van al cuerpo del Subdocumento 5 y no al anexo: la seccion 4 al § 5.12 y al § 5.10, la 5 al § 5.11, la 6 al § 5.12 y la 7 al § 5.15.
4. El § 5.14 deja de estar marcado `PENDIENTE — DECISION PROPIA DE CELULA 4` y pasa a `COMPLETADO`, con la salvedad de los tres vacios declarados.

---

# 9. Trazabilidad

| Exigencia | Fuente | Donde se cumple |
|---|---|---|
| Diccionario con nombre, tipo, dominio, obligatoriedad, propietario y sensibilidad de cada atributo | `BTT, Cap. 5, RT-05.01` | seccion 3, las 80 fichas |
| Modelo documentado con linaje y propietario por dominio | `BA, Art. 23` | ficha de gobierno de cada entidad |
| Gestion de datos maestros sin duplicacion de entidades compartidas | `BTT, Cap. 5, RT-05.09` | 16 entidades marcadas `maestro`; correccion de `CONDUCTOR` y `PERSONA` |
| Trazabilidad de toda operacion con valores anteriores y posteriores | `BTT, Cap. 5, RT-05.03` | `REGISTRO_AUDITORIA` y la seccion 5 de atributos derivados |
| Validacion en el punto de captura | `BTT, Cap. 5, RT-05.04` | columna de obligatoriedad y dominio de valores de cada atributo |
| Cifrado a nivel de campo de las categorias que el caso identifica | `CP, Cap. 15, RT-11.10`; `RNF-SEG-05` | seccion 4 |
| Retencion diferenciada por clase, sin plazo uniforme | `CP, Cap. 15, RT-05.10`; `RNF-CUM-14` | seccion 6 |
| Registro de consultas a informacion sensible | `CP, Cap. 15, RT-16.09` | `CONSULTA_SENSIBLE` y seccion 4.3 |

---

**Cierre.** 80 entidades, 451 atributos, cada uno con sus ocho campos. Dos vacios declarados y ninguno rellenado; el tercero, que era el unico de Celula 4, quedo cerrado en `DEC-C4-01`. El catalogo de campos cifrados que faltaba en el catalogo de requerimientos existe ahora, y la consulta a Celula 3 sobre cifrado e indexacion queda acotada a ocho atributos concretos.
