# Plan maestro quirúrgico — Alineación Célula 3 y Célula 4

**Propósito:** alinear las fuentes de arquitectura y datos para habilitar la redacción inmediata del Subdocumento 4 sin duplicar el Subdocumento 5.

**Commit base auditado:** `9b460ad9faf6876b677564bcbd884ec1fc22e58e` (`main`).

**Auditoría de respaldo:** [`AUDITORIA_ALINEACION_CELULA3_CELULA4.md`](AUDITORIA_ALINEACION_CELULA3_CELULA4.md).

**Estado vigente:** `ALINEACIÓN C3–C4 EJECUTADA`; base técnica y estructura editorial preparadas para la redacción conjunta.
**Regla de entrega:** no hacer commit ni push hasta revisión y autorización del usuario.

---

## 1. Resultado que debe producir este plan

Al terminar deben existir:

1. Una sola arquitectura normal/corte/retorno en C3 y C4.
2. Una sola baseline de capacidad para Informe 1, con escenarios futuros separados.
3. Un vocabulario compartido de datos, sin dos modelos conceptuales competidores.
4. Dependencias C4 actualizadas contra MA8.
5. Seguridad y datos enlazados mediante el catálogo de 28 campos y el tratamiento de 8 búsquedas.
6. Innovaciones claramente separadas de la baseline arquitectónica.
7. `Celula3/90_Consolidado/04_BASE_OBLIGATORIA_SUBDOCUMENTO_4.md` como punto de entrada editorial: estructura contractual, mínimos, fuentes y bosquejos abiertos; el consolidado conserva el inventario técnico pendiente de redacción conjunta.
8. Los bocetos F1–F5 separados del consolidado y archivados como referencia; los diagramas definitivos quedan a cargo del equipo. D3 se ejecuta solamente sobre el ensamblado final.

### 1.1 Estado de relevo

| Ámbito | Estado vigente | Qué significa para quien continúe |
|---|---|---|
| Decisiones compartidas `ALN-01..11` | **Aplicadas** | No reabrirlas sin evidencia oficial nueva o instrucción expresa del usuario. |
| Correcciones C3 `C3-01..07` | **Completadas** | Arquitectura, capacidad, datos, seguridad, integración, innovación y gobierno están alineados. |
| Correcciones C4 `C4-01..09` | **Completadas** | C4 consume la baseline C3 y conserva como propios el detalle de datos, calidad, retención y capacidad acumulada. |
| `GATE-01..04` | **Superados** | La redacción puede comenzar sin esperar nuevas decisiones arquitectónicas. |
| `C3-08` | **Habilitado** | El equipo debe convertir la base técnica en prosa natural y autónoma. |
| `C3-09` | **Pendiente del equipo** | Diagramas definitivos, ensamblado y D3 se realizan después de estabilizar la redacción. |
| `C4-10` | **Pendiente deliberado** | Regenerar PDF/LaTeX es una tarea editorial posterior de C4 y no bloquea la escritura de C3. |

**Conclusión operativa:** la alineación entre Célula 3 y Célula 4 está suficientemente cerrada para comenzar la escritura. Los pendientes restantes son editoriales, visuales o de validación externa; no constituyen contradicciones abiertas entre ambas células.

---

## 2. Contrato de decisiones compartidas

Estas decisiones ya están fijadas para ejecutar la alineación. Un agente no debe reabrirlas salvo evidencia oficial nueva o instrucción expresa del usuario.

| ID | Decisión de alineación | Consecuencia directa |
|---|---|---|
| `ALN-01` | C3 gobierna arquitectura lógica/física, emplazamiento, continuidad, integración, seguridad, productos de referencia y T-11. | C4 consume esas decisiones; una alternativa distinta se marca como propuesta, no como hecho. |
| `ALN-02` | La carga principal y el registro consolidado viven normalmente en AWS `sa-east-1`; el núcleo local mantiene estado crítico sincronizado y asume autoridad durante el corte. | El nodo local **no es solo puente** ni copia pasiva: ejecuta la ruta operacional crítica durante 72 h. Tampoco es una copia completa de toda la nube. |
| `ALN-03` | DR activo-pasivo en AWS `us-east-1`, RTO ≤4 h y RPO ≤15 min. | No confundir desastre del sitio con pérdida de WAN; `EDGE-RUN` resuelve el segundo escenario. |
| `ALN-04` | Baseline I1: 13,7 GB promedio/20,3 Mbps; 21,9 GB peak estacional/32,5 Mbps; cada WAN ≥35 Mbps disponibles. | 39 GB/57,8 Mbps es escenario de crecimiento 3×. ≈40 GB/≈58 Mbps es sensibilidad de imagen de 1 MB; no mezclar ambos motivos. |
| `ALN-05` | `Contenedor` es el activo/maestro de negocio; `VisitaContenedor` es el agregado de una estadía; `Recalada` o `VisitaNave` identifica la visita de una nave. | C3 publica la vista de alto nivel; C4 mantiene el modelo detallado y el diccionario. |
| `ALN-06` | Cuatro capacidades lógicas: `DATA-CORE`, `DATA-TS`, `DATA-DOC`, `DATA-AN`; dos familias principales de motor: PostgreSQL/temporal y objetos. | “Tres almacenamientos” de C4 se explica como separación funcional mínima, no como eliminación de evidencia/objetos. |
| `ALN-07` | El catálogo C4 de 28 campos sensibles se incorpora por referencia; Seguridad C3 gobierna el mecanismo y C3+C4 resuelven los 8 campos indexados. | No duplicar el catálogo completo en Subdoc 4. |
| `ALN-08` | Los patrones de integración de C3 bastan para I1; contratos, versiones y capacidades reales de terceros pueden quedar condicionados. | C4 completa §5.8 como propuesta y no inventa interfaces. |
| `ALN-09` | `CTX-SIM` e IN-05 son innovaciones condicionadas, no componentes implementados, aprobados ni filas obligatorias del T-11. | Solo entran a la baseline mediante ratificación A1/C1 y dimensionamiento C4. |
| `ALN-10` | Los 11 ADR permanecen `PROPUESTO`; hay 0 `APROBADO`. | “Aprobado” en C4 debe calificarse como editorial o interno. |
| `ALN-11` | Dos enlaces WAN de proveedores y rutas físicas diferentes constituyen la baseline. | No agregar un tercer enlace al catálogo o T-11 sin una decisión posterior ajena a este plan. |

---

## 3. Reglas de ejecución para cualquier agente

### 3.1 Antes de editar

1. Ejecutar `git status --short --branch` y registrar cualquier cambio ajeno.
2. No descartar, ocultar, mover ni reescribir cambios existentes de otras células.
3. Confirmar que el commit base sigue siendo ancestro de `HEAD`. Si `main` avanzó, revisar el diff antes de aplicar este plan.
4. Reclamar un solo bloque de trabajo y limitar el diff a sus archivos.
5. Leer la auditoría y las fuentes indicadas en la tarea; no releer todos los PDF.

### 3.2 Reglas de fuentes

- C3 se edita desde las rutas definidas por `Celula3/README.md`.
- Para C4 se adopta como ruta operativa recomendada:
  - entregable: `Célula 4/Subdocumento_5/CONTENIDO_SUBDOCUMENTO_5.md`;
  - respaldo: `Célula 4/Subdocumento_5/Documentos_de_trabajo/A00..A08`;
  - comunicaciones: `Célula 4/Subdocumento_5/Comunicados/`;
  - innovaciones: `Célula 4/Subdoc13/B*.md`.
- Los A00–A08 de la raíz, `Célula 4/Documentos_de_trabajo/` y comunicados/diagramas duplicados no se editan hasta que `C4-01` los marque expresamente como históricos o espejos.
- Los `.tex` no se editan ni se consultan salvo que el Markdown canónico no permita resolver una contradicción. Los PDF se regeneran solo al final.

### 3.3 Límites

- No aprobar ADR.
- No convertir propuesta, supuesto o validación futura en hecho.
- No inventar productos, versiones, capacidades de carrier, resultados de site survey ni pruebas.
- No hacer correcciones masivas o de estilo fuera del bloque asignado.
- No reincorporar los bocetos archivados al entregable. Los diagramas definitivos serán preparados y aprobados por el equipo después de estabilizar la redacción.
- No duplicar en Subdoc 4 las 80 entidades, 451 atributos ni matrices completas de C4.

### 3.4 Registro mínimo de cada bloque

Al terminar una tarea, el agente debe dejar en su respuesta:

- ID de tarea;
- archivos tocados;
- decisión aplicada (`ALN-*`);
- cambio semántico realizado;
- pendientes conservados y su responsable;
- validación ejecutada;
- confirmación de que no hizo commit/push.

---

## 4. Carril Célula 3 — correcciones propias

### `C3-01` — Ratificar la topología normal/corte/retorno

- **Prioridad:** P0.
- **Archivos:**
  - `Celula3/02_Frente_Fisica_Despliegue/C1_ARQUITECTURA_FISICA_Y_EMPLAZAMIENTO.md`
  - `Celula3/01_Frente_Logica_Integracion/A1_CONTEXTO_Y_ARQUITECTURA_LOGICA.md`
  - `Celula3/02_Frente_Fisica_Despliegue/C2_TECNOLOGIAS_HARDWARE_Y_DATA_CENTERS.md`
- **Aplicar:** `ALN-01..03`.
- **Cambio:** verificar y, solo donde sea ambiguo, declarar los tres estados:
  1. normal: AWS es registro consolidado; local mantiene réplica/estado crítico caliente;
  2. corte: `EDGE-RUN` asume autoridad de las cinco funciones críticas durante 72 h;
  3. retorno: reconciliación determinista ≤90 min y devolución controlada de autoridad.
- **No cambiar:** AWS, regiones, RTO/RPO ni estado de ADR.
- **Cierre:** ninguna fuente C3 describe el local como simple gateway, réplica pasiva o primario permanente.
- **Estado:** [x] Completado por verificación — C1, A1 y C2 ya contienen los tres estados y no requieren cambio semántico.

### `C3-02` — Congelar la baseline de capacidad I1

- **Prioridad:** P0.
- **Archivos:**
  - `Celula3/02_Frente_Fisica_Despliegue/C4_DIMENSIONAMIENTO_Y_T11.md`
  - `Celula3/90_Consolidado/01_T11_TRABAJO_TRAZABLE.md`
  - `Celula3/90_Consolidado/02_FORMULARIO_T11_FINAL.md`
- **Aplicar:** `ALN-04`.
- **Cambio:** añadir una tabla breve de escenarios si todavía no queda inequívoca; conservar ≥35 Mbps como baseline I1 y declarar ≥58 Mbps como disparador de crecimiento/sensibilidad, no como capacidad ya contratada.
- **Condición:** si la política final exige que objetos de 1 MB o el escenario 3× completen íntegramente en 90 min, actualizar T-11 mediante decisión trazable; no hacerlo por inferencia.
- **Cierre:** toda cifra indica escenario y fórmula; T-11 no mezcla actual, peak y futuro.
- **Estado:** [x] Completado — escenarios compartidos añadidos; T-11 conserva ≥35 Mbps para el peak I1.

### `C3-03` — Alinear el modelo de alto nivel y `V-DATA-01`

- **Prioridad:** P1.
- **Dependencia:** `C4-04` y `C4-05` pueden ejecutarse en paralelo, pero deben converger antes del cierre.
- **Archivos:**
  - `Celula3/01_Frente_Logica_Integracion/A1_CONTEXTO_Y_ARQUITECTURA_LOGICA.md`
  - `Celula3/00_Gobierno/12_PROYECCION_EDITORIAL_Y_PLAN_DIAGRAMAS_MA7.md`
  - posteriormente `Celula3/90_Consolidado/00_BASE_TECNICA_SUBDOCUMENTO_4.md`
- **Aplicar:** `ALN-05/06`.
- **Cambio:** reemplazar la lectura “Contenedor único centro operacional” por la distinción maestro/visita; separar `VisitaContenedor` de `Recalada/VisitaNave`; mantener cuatro capacidades lógicas y enlazar el detalle a C4.
- **Entregable:** `V-DATA-01` con dominio, autoridad, flujo, almacén, protección, retención y dueño del detalle.
- **Cierre:** cada dominio C4 tiene correspondencia C3 y no se copian entidades/atributos completos.
- **Estado:** [x] Completado — convención semántica compartida y `V-DATA-01` ampliada a los diez dominios C4.

### `C3-04` — Incorporar el catálogo de protección de C4

- **Prioridad:** P1.
- **Archivos:**
  - `Celula3/03_Frente_Seguridad_Consolidacion/D1_ARQUITECTURA_DE_SEGURIDAD.md`
  - trazas D1 estrictamente afectadas
- **Aplicar:** `ALN-07`.
- **Cambio:** sustituir “Subdoc 5 entregará el catálogo” por “catálogo de 28 campos recibido, pendiente de contraste”; enlazar C4 y conservar el patrón de identificadores sustitutos, índices derivados o servicio autorizado.
- **Salida conjunta:** tabla de 8 campos con necesidad de igualdad, mecanismo, fuga aceptable, propietario de clave, prueba y estado.
- **Cierre:** 28/28 campos referenciados y 8/8 búsquedas resueltas o condicionadas con responsable.
- **Estado:** [x] Completado para diseño I1 — 28/28 campos referenciados y 8/8 búsquedas dispuestas; aceptación y pruebas quedan condicionadas.

### `C3-05` — Entregar a C4 el estado real de integración

- **Prioridad:** P1.
- **Archivos:**
  - `Celula3/01_Frente_Logica_Integracion/A2_ARQUITECTURA_DE_INTEGRACION.md`
  - trazas A2 solo si el estado está obsoleto
- **Aplicar:** `ALN-08`.
- **Cambio:** no rediseñar. Confirmar catálogo de 21 contrapartes/7 familias, eventos, idempotencia, DLQ y contrato tipo; enumerar qué interfaz sigue `POR LEVANTAR` o `BLOQUEADO EXTERNO`.
- **Cierre:** C4 puede completar §5.8 sin inventar contratos ni presentar todo como ausente.
- **Estado:** [x] Completado — A2 entrega explícitamente inventario, contrato tipo, resiliencia y lista de condiciones externas.

### `C3-06` — Blindar innovación y estados

- **Prioridad:** P2.
- **Archivos:**
  - `Celula3/00_Gobierno/06_RESPUESTA_COORDINACION_SUBDOC5_INNOVACIONES.md`
  - registro ADR y T-11 solo para verificar, no para promover/agregar
- **Aplicar:** `ALN-09/10`.
- **Cambio:** no es necesario modificar si ya dice “provisional”. Confirmar que `CTX-SIM` no ingresa a catálogo, figura o T-11 sin ratificación/dimensionamiento.
- **Cierre:** búsqueda C3 conserva 11 ADR `PROPUESTO`, 0 aprobados y `CTX-SIM` condicionado.
- **Estado:** [x] Completado — 11 ADR `PROPUESTO`, 0 aprobados; `CTX-SIM` queda fuera de catálogo/figuras/T-11 salvo ratificación.

### `C3-07` — Actualizar gobierno después del cruce

- **Prioridad:** P2.
- **Dependencias:** `C3-01..06`, `C4-01..09`.
- **Archivos:**
  - `Celula3/README.md`
  - `Celula3/00_Gobierno/13_PREPARACION_D3_Y_MAPA_ENSAMBLADO_MA8.md`
  - `Celula3/90_Consolidado/03_CHECKLIST_ENTREGA.md`
- **Cambio:** marcar el cruce C3–C4 como completado con pendientes externos tratados; no declarar redacción, figuras ni D3 terminados.
- **Cierre:** README indica exactamente qué falta para producción, sin mencionar Subdoc 5 como ausente.
- **Estado:** [x] Completado — README, MA8 y checklist registran el cruce C3–C4 cerrado como base técnica, sin declarar redacción final, diagramas entregables ni D3 terminados.

### `C3-08` — Redacción editorial conjunta del Subdocumento 4

- **Prioridad:** P0 después de los gates.
- **Dependencia obligatoria:** `GATE-01..04` aprobados.
- **Guía de entrada:** `Celula3/90_Consolidado/04_BASE_OBLIGATORIA_SUBDOCUMENTO_4.md`.
- **Destino de redacción:** `Celula3/90_Consolidado/00_BASE_TECNICA_SUBDOCUMENTO_4.md`.
- **Fuentes:** orden canónico de `Celula3/README.md`; este plan no sustituye ese mapa editorial.
- **Secuencia de redacción:** respetar los apartados contractuales `4.1 a/b` y `4.2 a–e + T-11`; usar las trece subsecciones existentes solo como desglose interno de contenidos.
- **Reglas:** explicar en lenguaje natural antes de usar códigos; describir zonas, responsabilidades y comportamiento; conclusiones primero; cifras con escenario; estados explícitos; trazabilidad interna fuera del cuerpo principal; datos detallados por referencia a C4; T-11 se incorpora sin reescribirlo.
- **Cierre:** trece subsecciones comprensibles para un evaluador, sin marcadores vacíos, sin dependencia de referencias internas para entender la propuesta y con las fuentes originales preservadas en el expediente.
- **Estado:** [ ] Habilitado para trabajo conjunto — existe una guía obligatoria, una base técnica alineada y un mapa de fuentes; la redacción editorial definitiva no se declara realizada.

### `C3-09` — Diagramas del equipo, ensamblado y D3

- **Prioridad:** P1 posterior a `C3-08`.
- **Archivos:** consolidado redactado por el equipo, diagramas definitivos del equipo, T-11 y D3. Los bocetos previos viven únicamente en `Celula3/90_Consolidado/diagramas_archivados/`.
- **Cambio:** incorporar únicamente los diagramas que el equipo decida preparar y aprobar; deben usar los mismos nombres, ubicaciones y cifras del texto definitivo. Los bocetos archivados no son insumos obligatorios ni evidencia de cierre.
- **Cierre:** ensamblar texto, diagramas aprobados y T-11; ejecutar `TRZ-D3-001..013`, corregir fuentes y emitir P5. No marcar D3 ejecutado antes del ensamblado.
- **Estado:** [ ] Pendiente — los diagramas definitivos quedan a cargo del equipo; los cinco bocetos anteriores fueron archivados y excluidos del entregable.

### Base de secciones para la escritura conjunta

Este desglose está listo para que el equipo redacte sin reabrir la alineación. No reemplaza la estructura contractual `4.1 a/b` y `4.2 a–e + T-11`; la guía obligatoria indica cómo agruparlo. Los títulos internos pueden pulirse editorialmente, pero deben conservar la cobertura indicada.

| Sección | Pregunta que debe responder en lenguaje natural |
|---|---|
| `4.1.1 Esquema de solución` | Quiénes usan la solución, qué canales existen, qué pertenece a TERABYTE y qué sistemas externos se integran. |
| `4.1.2 Arquitectura lógica` | Qué grandes áreas funcionales componen la plataforma y cómo se relacionan sin exponer códigos internos innecesarios. |
| `4.1.3 Integración y procesos críticos` | Cómo se intercambian datos con TOS, ERP, navieras, autoridades, ferrocarril, concesionaria y dispositivos; qué ocurre durante corte y retorno. |
| `4.1.4 Datos y seguridad` | Qué tipos de datos maneja la solución, quién conserva autoridad y cómo se protegen identidad, permisos, evidencia y telemetría. |
| `4.1.5 Decisiones y cumplimiento` | Cuáles son las decisiones propuestas, por qué son razonables y qué validaciones permanecen pendientes. |
| `4.2.1 Arquitectura física y emplazamiento` | Qué vive en la nube, en la sala técnica y en gate, patio, reefers y muelle; por qué esa distribución cumple el modelo híbrido. |
| `4.2.2 Tecnologías de software` | Qué familias tecnológicas se proponen, para qué sirven y dónde se ejecutan. |
| `4.2.3 Implementos de hardware y software` | Qué equipamiento y licencias o servicios requiere la solución, con sus cantidades justificadas. |
| `4.2.4 Data center primario` | Cómo se acondiciona y utiliza la infraestructura local, qué supuestos dependen del levantamiento y cuál es su rol durante una desconexión. |
| `4.2.5 Data center secundario` | Cómo funciona la recuperación activo-pasiva en otra región y cómo se diferencia de la continuidad local. |
| `4.2.6 Despliegue, redes y continuidad` | Cómo se despliega, conecta, monitorea y mantiene la solución; cómo operan los dos enlaces WAN, LTE/5G, las 72 horas y la reconciliación. |
| `4.2.7 Dimensionamiento y capacidad` | Qué demanda se espera, qué escenario gobierna el Informe 1 y qué condiciones disparan una ampliación. |
| `4.2.8 Formulario T-11` | Qué productos o servicios componen la propuesta y cómo cada cantidad vuelve a una necesidad técnica. |

**Regla editorial:** el lector debe comprender cada sección sin abrir A1–D3. Los códigos, enlaces y matrices permanecen como trazabilidad interna y solo se llevan al cuerpo cuando sean indispensables para evitar ambigüedad.

---

## 5. Carril Célula 4 — correcciones solicitadas

### `C4-01` — Fijar fuentes canónicas dentro del repositorio

- **Prioridad:** P0 administrativa; ejecutar antes de todo otro cambio C4.
- **Archivos:**
  - `Célula 4/00_INDICE.md`
  - `Célula 4/Subdocumento_5/00_INDICE.md`
- **Cambio recomendado:** declarar como editables las rutas de §3.2; marcar las copias raíz y duplicadas como espejo/histórico/no editar. Explicar que el PDF/LaTeX se regenera desde la fuente editorial disponible, pero no declarar como fuente de verdad un proyecto ausente de `main`.
- **No hacer:** borrar, mover o sincronizar masivamente duplicados.
- **Cierre:** un agente puede identificar una única ruta editable para entregable, respaldo y comunicados.
- **Estado:** [x] Completado — rutas canónicas fijadas en ambos índices; no se movieron ni borraron copias.

### `C4-02` — Adoptar la topología arquitectónica C3

- **Prioridad:** P0.
- **Dependencia:** `C4-01`; contrato `ALN-01..03`.
- **Archivos canónicos:**
  - `Subdocumento_5/Documentos_de_trabajo/A05_ALTERNATIVAS_PERSISTENCIA.md`
  - `Subdocumento_5/Documentos_de_trabajo/A06_MATRIZ_CAP_POR_OPERACION.md`
  - `Subdocumento_5/CONTENIDO_SUBDOCUMENTO_5.md`
- **Cambiar:**
  - “primario permanente en borde” → “registro consolidado normal en AWS con estado crítico local caliente y autoridad local durante el corte”;
  - “primario cloud incumple” → “primario cloud es admisible si la ruta local autoritativa completa no depende de WAN”;
  - dirección y estados de réplica/failover conforme a `ALN-02`.
- **Conservar:** relacional, ACID, escritor único, PostgreSQL/temporal, objetos, RPO y reconciliación.
- **Cierre:** ninguna fuente canónica C4 presenta edge-primary permanente como requisito de las Bases.
- **Estado:** [x] Completado — A05, A06 y el contenido canónico adoptan AWS normal y autoridad local durante corte.

### `C4-03` — Separar capacidad actual, peak y crecimiento

- **Prioridad:** P0.
- **Dependencia:** `C4-01`; contrato `ALN-04`.
- **Archivos canónicos:**
  - `Subdocumento_5/Documentos_de_trabajo/A08_ALMACENAMIENTO_ACUMULADO.md`
  - `Subdocumento_5/CONTENIDO_SUBDOCUMENTO_5.md`
  - comunicado de decisiones/capacidad si repite cifras
- **Cambio:** publicar la misma tabla de escenarios de C3. Etiquetar 39/57,8 como 3× futuro y ≈40/≈58 como sensibilidad de imagen a 1 MB. No afirmar que imágenes pueden terminar después de 90 min como interpretación contractual confirmada.
- **Conservar:** cálculos de 3,6/9,9 TB de dato y 6,4/18,1 TB aprovisionados como horizonte de C4, separados de la capacidad online I1 de C3.
- **Cierre:** ≥35 Mbps y ≥58 Mbps no aparecen aplicados al mismo escenario.
- **Estado:** [x] Completado — A08 y el contenido canónico separan promedio, peak, 3× y sensibilidad de imagen.

### `C4-04` — Normalizar entidades centrales

- **Prioridad:** P1.
- **Archivos canónicos:** A00, A01, A02 y `CONTENIDO...`.
- **Aplicar:** `ALN-05`.
- **Cambio:** renombrar o definir inequívocamente `VISITA` como `VisitaContenedor`; reservar `Recalada/VisitaNave` para nave. Mantener claves y relaciones del modelo detallado.
- **Cierre:** el lector entiende por qué Contenedor es maestro y VisitaContenedor es agregado operacional, sin contradicción con A1 C3.
- **Estado:** [x] Completado — `VISITA` se conserva como identificador físico de `VisitaContenedor`; `Recalada/VisitaNave` queda inequívoca.

### `C4-05` — Normalizar almacenamientos y motores

- **Prioridad:** P1.
- **Archivos canónicos:** A00, A05 y `CONTENIDO...` §§5.4–5.6.
- **Aplicar:** `ALN-06`.
- **Cambio:** declarar explícitamente:
  - cuatro capacidades lógicas: operacional, temporal, evidencia/objetos y analítica;
  - cinco familias solo si histórico se cuenta aparte;
  - dos familias de motor: PostgreSQL/temporal y objetos.
- **Cierre:** no hay tablas que aparenten eliminar `DATA-DOC` ni crear cinco productos independientes.
- **Estado:** [x] Completado — cuatro capacidades lógicas alineadas sobre dos familias de motor.

### `C4-06` — Entregar el cruce de cifrado a C3

- **Prioridad:** P1.
- **Archivos canónicos:** A00, A02, A03 y `CONTENIDO...` §5.10.
- **Aplicar:** `ALN-07`.
- **Cambio:** conservar 28 campos; para los 8 indexados indicar necesidad de búsqueda por igualdad y aceptar el patrón de decisión C3. No escoger cifrado determinista por defecto.
- **Cierre:** tabla conjunta de 8 filas completa o cada fila condicionada con propietario/prueba.
- **Estado:** [x] Completado para diseño I1 — C4 conserva el catálogo y referencia la disposición C3 por campo sin aprobar cifrado determinista.

### `C4-07` — Actualizar dependencias contra MA8 y completar §5.8

- **Prioridad:** P1.
- **Archivos canónicos:**
  - `Subdocumento_5/Comunicados/00_PENDIENTES_CELULA4.md`
  - `Subdocumento_5/Comunicados/02_SOLICITUD_A_CELULA_3.md`
  - A00 y `CONTENIDO...`, incluidos Anexos F/G
- **Aplicar:** `ALN-08`.
- **Cambio de estado:** usar únicamente `RECIBIDO`, `RECIBIDO CON CONFLICTO`, `CONDICIONADO EXTERNO` o `CERRADO I1` para solicitudes C3.
- **Cerrar como recibido:** propiedad del modelo, zonas/fases, runtime local, productos de referencia, 18 dimensiones, red propuesta y patrón 3-2-1-1-0.
- **Mantener condicionado:** 8 búsquedas cifradas, contratos/protocolos reales, CDC TOS, latencia/site survey, política de imagen y matriz exacta de copias.
- **§5.8:** redactar diseño propuesto desde A2; no inventar contratos externos.
- **Cierre:** §5.8 deja de figurar entero como pendiente de C3.
- **Estado:** [x] Completado en contenido/A00 — §5.8 cerrado como diseño I1; contratos reales conservan condición externa. Comunicados actualizados en el mismo bloque.

### `C4-08` — Corregir trazas y recuentos internos

- **Prioridad:** P2.
- **Dependencia:** `C4-02..07`.
- **Archivos:** fuente canónica definida en `C4-01`.
- **Cambio:**
  - 80 entidades totales y 78 relacionales, solo si ese es el reparto verificado;
  - sincronización como cuello vigente; ingesta como riesgo secundario;
  - calidad/diccionario con el mismo estado del resumen;
  - corregir `PendienteTres`, encabezados repetidos y tablas duplicadas.
- **Cierre:** una búsqueda no encuentra estados o cifras históricas sin etiqueta.
- **Estado:** [x] Completado — 80/78+2 coherente, sincronización como cuello vigente, estados actualizados y 164 encabezados duplicados eliminados.

### `C4-09` — Condicionar innovaciones y calificar “aprobado”

- **Prioridad:** P2.
- **Archivos:**
  - `Célula 4/Subdoc13/B05_IN03_GEMELO_DE_OPERACION.md`
  - `Célula 4/Subdoc13/B11_PENDIENTES_POR_CELULA.md`
  - `Célula 4/Subdoc13/00_INDICE_SUBDOCUMENTO_13.md`
- **Aplicar:** `ALN-09/10`.
- **Cambio:** “se incorpora”/“cerrado” → “candidato condicionado a ratificación A1/C1”; `APROBADO` → `APROBADO PARA INTEGRACIÓN EDITORIAL C4` en la leyenda, sin necesidad de repetirlo en cada archivo si el índice gobierna.
- **Cierre:** `CTX-SIM` no aparece implementado, contratado, aprobado por arquitectura ni cuantificado en T-11.
- **Estado:** [x] Completado — aprobación calificada como editorial C4 y `CTX-SIM` condicionado a ratificación, capacidad y amenazas.

### `C4-10` — Regenerar entregables solo después del cierre

- **Prioridad:** P3.
- **Dependencia:** `C4-01..09` y `GATE-01..04`.
- **Acción:** propagar desde la fuente canónica a PDF/LaTeX únicamente si C4 dispone del proyecto real; revisar visualmente y verificar que el Markdown siga representando el contenido.
- **No hacer:** editar a mano tres copias o corregir solo el PDF.
- **Cierre:** PDF, Markdown e índice declaran la misma versión y estado.
- **Estado:** [ ] Pendiente deliberado — dependencias de alineación cumplidas; no regenerar PDF/LaTeX sin solicitud de C4 y sin su proyecto editorial canónico.

---

## 6. Orden coordinado de ejecución

| Orden | Tareas | Responsable | Puede ejecutarse en paralelo con | Salida |
|---:|---|---|---|---|
| 1 | `C4-01` | C4 | revisión sin cambios de `C3-01/02` | Fuentes editables inequívocas |
| 2 | `C3-01`, `C3-02`, `C4-02`, `C4-03` | Ambas | por carril, usando `ALN-01..04` | Arquitectura y capacidad alineadas |
| 3 | `C3-03/04`, `C4-04/05/06` | Ambas | sí, con tabla común | Vocabulario, almacenes y cifrado alineados |
| 4 | `C3-05/06`, `C4-07/08/09` | Ambas | sí | Estados, integración e innovación corregidos |
| 5 | `GATE-01..04` | Agente auditor | ninguno | Autorización de redacción |
| 6 | `C3-07`, luego `C3-08` | C3 + equipo redactor | C4-10 puede esperar | Gobierno actualizado y Subdoc 4 redactado en lenguaje natural |
| 7 | `C3-09`, luego `C4-10` | Equipo / cada célula | coordinación de nombres/cifras | Diagramas aprobados, D3 y entregables regenerados |

No es necesario esperar validaciones externas para iniciar `C3-08` si están etiquetadas como condicionadas y tienen responsable, método y hito de cierre.

---

## 7. Gates para iniciar la redacción del Subdocumento 4

### `GATE-01` — Topología

- [x] AWS figura como carga principal/registro consolidado normal.
- [x] Local figura como núcleo operacional autónomo, con autoridad temporal durante corte.
- [x] No queda “primario en borde obligatorio” ni “cloud primary incumple” como afirmación vigente.
- [x] DR y corte WAN se explican como escenarios distintos.

**Resultado:** APROBADO PARA REDACCIÓN — baseline común en C1/C3 C3 y A05/A06/Contenido C4.

### `GATE-02` — Capacidad

- [x] 13,7/20,3 está etiquetado como promedio actual.
- [x] 21,9/32,5 y WAN ≥35 está etiquetado como peak/baseline I1.
- [x] 39/57,8 está etiquetado como crecimiento 3×.
- [x] ≈40/≈58 está etiquetado como sensibilidad a imagen 1 MB.
- [x] El alcance de ≤90 min está declarado o condicionado, no inventado.

**Resultado:** APROBADO PARA REDACCIÓN — tabla compartida en C4 C3, A08 y Contenido C4.

### `GATE-03` — Datos y seguridad

- [x] Contenedor/VisitaContenedor/Recalada tienen significados únicos.
- [x] Cuatro capacidades lógicas y dos familias de motor están conciliadas.
- [x] `V-DATA-01` tiene dueño y estructura acordados.
- [x] Los 28 campos y las 8 búsquedas están recibidos y resueltos/condicionados.

**Resultado:** APROBADO PARA REDACCIÓN — detalle en SD5; vista y protección arquitectónicas en SD4.

### `GATE-04` — Estados y alcance

- [x] C4 ya no presenta MA8 como ausente.
- [x] §5.8 diferencia diseño propuesto de contratos externos.
- [x] `CTX-SIM` e IN-05 siguen condicionados.
- [x] Los 11 ADR siguen `PROPUESTO`; 0 `APROBADO`.
- [x] La baseline y el T-11 contienen únicamente los dos enlaces WAN exigidos.

**Resultado:** APROBADO PARA REDACCIÓN — estados editoriales y arquitectónicos separados.

**Decisión de paso:** los cuatro gates cumplen. `C3-08` queda **HABILITADO PARA TRABAJO CONJUNTO** y `C3-09` **PENDIENTE**; `C4-10` no es requisito para iniciar la redacción del Subdocumento 4.

---

## 8. Verificación mecánica mínima

Ejecutar estas búsquedas sobre las fuentes canónicas y leer cada resultado en contexto:

```bash
rg -n "primario.*borde|primario.*nube|cloud.*incumple|autoridad.*corte|réplica.*local" Celula3 'Célula 4' -g '*.md'
rg -n "13 GB|13,7 GB|21,9 GB|39 GB|19,3 Mbps|20,3 Mbps|32,5 Mbps|35 Mbps|57,8 Mbps|58 Mbps" Celula3 'Célula 4' -g '*.md'
rg -n "78 entidades|80 entidades|PendienteTres|ingesta de series|ventana de sincronización" 'Célula 4' -g '*.md'
rg -n "CTX-SIM|APROBADO|PROPUESTO|tercer enlace" Celula3 'Célula 4' -g '*.md'
rg -n "Subdocumento 5 entrega|pendiente — C3|pendiente.*Célula 3|PEN-0" Celula3 'Célula 4' -g '*.md'
```

Luego ejecutar:

```bash
git diff --check
git status --short --branch
```

Una coincidencia no es automáticamente un error: puede ser historia o alternativa descartada, pero debe estar rotulada como tal.

---

## 9. Matriz de cierre y relevo

| Bloque | Responsable | Estado | Evidencia de cierre | Bloquea |
|---|---|---|---|---|
| `C3-01` | C3 | Completado | tres estados coherentes | `GATE-01` superado |
| `C3-02` | C3 | Completado | T-11 y escenarios coherentes | `GATE-02` superado |
| `C3-03` | C3 | Completado | `V-DATA-01` alineada | `GATE-03` superado |
| `C3-04` | C3 | Completado I1 | 28/8 tratados; prueba condicionada | `GATE-03` superado |
| `C3-05` | C3 | Completado | estado de 21+7 e interfaces | `GATE-04` superado |
| `C3-06` | C3 | Completado | innovación/ADR sin promoción | `GATE-04` superado |
| `C3-07` | C3 | Completado | gobierno actualizado | `C3-08` habilitado |
| `C3-08` | C3 + equipo redactor | Habilitado | base técnica con trece subsecciones; redacción natural pendiente | habilita diagramas definitivos cuando el texto se estabilice |
| `C3-09` | Equipo / C3 | Pendiente | diagramas aprobados + D3/P5 | cierre Subdoc 4 |
| `C4-01` | C4 | Completado | índice con una ruta editable | — |
| `C4-02` | C4 | Completado | topología C3 adoptada | `GATE-01` superado |
| `C4-03` | C4 | Completado | escenarios separados | `GATE-02` superado |
| `C4-04/05/06` | C4 | Completado I1 | modelo/almacenes/cifrado | `GATE-03` superado |
| `C4-07/08/09` | C4 | Completado | estados/trazas/innovación | `GATE-04` superado |
| `C4-10` | C4 | Pendiente deliberado | entregables regenerados | cierre Subdoc 5/13; no bloquea la redacción |

### Plantilla de relevo entre agentes

```md
## Relevo — <ID de tarea>
- Commit/HEAD revisado:
- Archivos modificados:
- Decisiones ALN aplicadas:
- Cambio realizado:
- Pendientes conservados:
- Validación ejecutada:
- Resultado del gate afectado:
- Commit/push: NO
```

---

## 10. Criterio final de éxito

Este plan termina cuando:

1. `GATE-01..04` están cumplidos con evidencia en archivos canónicos;
2. C3 y C4 describen la misma arquitectura y los mismos escenarios;
3. los pendientes externos están condicionados, no inventados;
4. el Subdocumento 4 está redactado en lenguaje natural, los diagramas que apruebe el equipo coinciden con el texto y D3 emite veredicto;
5. el usuario revisa el diff y decide si autoriza commit/push.
