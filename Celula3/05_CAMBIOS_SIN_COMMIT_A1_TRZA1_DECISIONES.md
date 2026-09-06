# Cambios sin commit — A1, TRZ_A1 y Decisiones/Escalamientos de Frente 1

**Estado:** estos cambios están **solo en el árbol de trabajo local** de `frente_1`, no comiteados. Este documento existe para que el resto del equipo pueda ver exactamente qué se modificó sin necesidad de comparar archivos manualmente, mientras se decide si se comitean.

**Fecha del corte:** 2026-09-06.
**Origen de los cambios:** corrección de la contradicción `CTX-VESSEL` (A1 vs. C1) detectada en la auditoría cruzada de Frente 3 (`D2_AMENAZAS_ADR_Y_PUNTOS_DE_FALLA.md`, hallazgos `B6-F03`/`B6-F04a`), más la reconstrucción de un cruce de SPOF con D2 que se había perdido por un `git reset` accidental de una rama.
**Archivos afectados:** `A1_CONTEXTO_Y_ARQUITECTURA_LOGICA.md`, `trazabilidad/TRZ_A1.md`, `trazabilidad/DECISIONES_Y_ESCALAMIENTOS.md`. Ningún otro archivo del frente ni de otro frente fue tocado.

---

## 1. `A1_CONTEXTO_Y_ARQUITECTURA_LOGICA.md` — 6 cambios puntuales

### 1.1 Descripción de `CTX-VESSEL` (§2.2, catálogo de componentes)

**Antes:** una sola frase — *"Nave y mensajería: gestión de planes de carga/descarga, órdenes, confirmaciones, ventanas de atraque (≥72 h para alianza), cálculo de productividad por grúa/hora y procesamiento de mensajería marítima EDIFACT (BAPLIE, COPRAR, COARRI, CODECO)."*

**Ahora:** se divide explícitamente en dos subconjuntos:
- **(1) Subconjunto operacional de muelle** — local, Crítica, requerido en `EDGE-RUN`; se aclara que su emplazamiento físico (`PHY-OPS-01`) **todavía no está asignado por C1** (remite a `F1-CONFLICTO-002`). Incluye recaladas en ejecución, secuencias STS, confirmación de movimientos contenedor a contenedor, ventana de atraque activa y productividad en tiempo real (`RF-NAV-12`).
- **(2) Subconjunto de mensajería e integración externa** — nube, Alta, `PHY-CLD-03`. Incluye anuncios de recaladas futuras y mensajería EDIFACT (BAPLIE/COPRAR/COARRI/CODECO) vía `INT-HUB`. Se aclara que durante un corte de enlace la mensajería entrante espera y la saliente se acumula en el buffer local de `EDGE-RUN`.

**Por qué:** A1 marcaba todo `CTX-VESSEL` como un bloque único "Crítica", lo que chocaba con C1 (que ubica todo el componente en nube). Separar los dos subconjuntos deja claro que solo la parte de muelle necesita sobrevivir localmente — la mensajería, por definición, no puede operar sin el enlace exterior.

### 1.2 Bullet de `SRV-IAM` (Capa 7 — Seguridad)

**Se agregó** un párrafo nuevo al final de la descripción existente, explicando la continuidad de `SRV-IAM` durante las 72 h sin enlace: `EDGE-RUN` cachea localmente sesiones y credenciales **activas** para validación offline (no el directorio completo ni la emisión de credenciales nuevas). Se deja constancia de que este mecanismo coincide con lo que C1 ya asume físicamente (`PHY-OPS-01`, caché de sesión), pero que C1 etiqueta el componente "crítica" y A1 lo etiqueta "Alta" — se aclara que es una diferencia de **eje de medición** (comportamiento vs. infraestructura física), no un error, y que queda pendiente de conciliar en Puerta 2.

### 1.3 Bullet de `EDGE-RUN` (componente transversal)

**Cambio mínimo de una frase:** en la lista de componentes que `EDGE-RUN` replica, `CTX-VESSEL` ahora dice explícitamente *"(subconjunto de muelle local; ver descripción en §2.2 y `F1-CONFLICTO-002`)"* — antes solo decía `CTX-VESSEL` a secas, sin distinguir subconjunto.

### 1.4 Tabla "Cinco funciones críticas" (§2.2), fila 1

**Antes:** *"Atención de nave y movimientos | `CTX-OPS`, `CTX-VESSEL` | Registro de movimientos de carga/descarga, confirmaciones, ventana de atraque en curso | Nueva mensajería EDIFACT con navieras (INT-HUB) queda en buffer hasta reconectar"*

**Ahora:** *"`CTX-VESSEL` (subconjunto muelle)"* en la columna de componentes; la columna "qué sigue funcionando" se precisa a *"Órdenes de carga/descarga STS, confirmaciones de contenedor, ventana de atraque en curso, productividad en tiempo real"*; la columna de degradación pasa de *"Nueva mensajería EDIFACT... queda en buffer"* a *"Mensajería EDIFACT... se encola en buffer local; anuncios de naves futuras diferidos"* (más preciso: incluye explícitamente los anuncios de naves futuras como parte de lo que se degrada).

### 1.5 Tabla de SPOF lógicos (§2.5)

**Se agregó una columna nueva**, "ID en D2 (Frente 3)", que cruza cada SPOF lógico de A1 con su ID correspondiente en el catálogo consolidado de Frente 3 (`SPOF-01`, `SPOF-07`, `SPOF-08`, `SPOF-10`, `SPOF-14`).

**Se agregó una fila nueva:** `INT-HUB` como bus único de intercambio (`SPOF-08` en D2), que antes no estaba en la tabla de A1 aunque sí es un SPOF real (21 contrapartes y 7 familias convergen en un único punto de integración).

La tabla pasó de 4 filas a 5 filas.

> **Nota de esta misma auditoría, todavía no corregida:** al verificar contra el D2 real, el ID `SPOF-08`/`SPOF-10` que esta fila le asigna a `GW-API` no es correcto — en el catálogo de D2, `SPOF-08` es `INT-HUB` y `SPOF-10` es `SRV-IAM`, no `GW-API`. D2 no tiene un SPOF propio dedicado a `GW-API`. Esto quedó señalado como hallazgo `X-2`... **(corrección: el hallazgo correspondiente en el documento de auditoría cruzada es el que trata la cita `RT-11.27`; el error de `GW-API`/SPOF se documentó dentro del mismo bloque de "colisión SPOF-NN", hallazgo `X-1`, en `04_AUDITORIA_CRUZADA_A_C_D.md`)**. Se deja constancia aquí porque la fila de A1 todavía no se ha corregido.

### 1.6 Tabla de catálogo de componentes (§3.1), fila `CTX-VESSEL`

**Antes:** *"Nave y mensajería | 4-Negocio | Planes, órdenes, confirmaciones, ventana y productividad | Crítica"*

**Ahora:** la columna de responsabilidad pasa a *"Partición dual: (a) subconjunto operacional de muelle local (órdenes STS, movimientos, ventana activa, productividad); (b) mensajería externa EDIFACT y anuncios futuros"*, y la columna de criticidad pasa de un valor único ("Crítica") a *"Crítica (subconjunto muelle local) / Alta (mensajería EDIFACT nube)"*.

### 1.7 Nota nueva bajo "Escala de criticidad" (§3.1)

**Se agregó un párrafo** aclarando que la escala de criticidad de A1 es **lógica/de comportamiento** (¿la función debe seguir sin enlace?), no física, y que Frente 3 detectó que no coincide exactamente con la escala física de C1 para siete componentes: `CTX-VESSEL`, `GW-EDGE`, `GW-API`, `CTX-INSP`, `CTX-EMIS`, `DATA-DOC` (A1 "Alta"/C1 "media") y `SRV-IAM` (A1 "Alta"/C1 "crítica"). Se deja explícito que ninguna escala está mal, que miden ejes distintos, y que no existe hoy una tabla de correspondencia entre ambas.

### 1.8 Tabla de dependencias/continuidad (§4.1), fila `CTX-VESSEL`

**Antes:** *"Planes de carga/descarga, ventanas, productividad | CTX-OPS, INT-HUB (EDIFACT), CTX-PLAN | Sí — operación de nave incluida en EDGE-RUN"*

**Ahora:** *"Recalada activa, órdenes de carga/descarga, ventana activa, productividad"* en la primera columna; la columna de continuidad se precisa a *"Sí — subconjunto de muelle opera 72 h en EDGE-RUN; mensajería externa EDIFACT se encola en buffer local persistente sin detener la atención física de nave"*.

---

## 2. `trazabilidad/TRZ_A1.md` — 2 cambios

### 2.1 Fila `TRZ-A1-033` (declaración de SPOF lógicos)

**Antes:** citaba *"5 puntos únicos de falla lógicos (GW-API, INT-TOS, SRV-IAM, EDGE-RUN, CTX-PLAN)"*, sin cruce con D2.

**Ahora:** pasa a *"6 puntos únicos de falla lógicos (GW-API, INT-TOS, SRV-IAM, EDGE-RUN, INT-HUB, CTX-PLAN)"* — se agrega `INT-HUB` a la lista — y la columna de fuente primaria ahora incluye *"cruzado con Frente 3 `D2_AMENAZAS_ADR_Y_PUNTOS_DE_FALLA.md` (`SPOF-01/07/08/10/14`)"*. La afirmación también se amplía para mencionar que cada SPOF lleva su "ID cruzado con el SPOF físico/de amenazas correspondiente de D2".

### 2.2 Fila nueva `TRZ-A1-039`

Se agrega después de `TRZ-A1-038`. Documenta el hallazgo de `CTX-VESSEL` con su fuente exacta: `D2_AMENAZAS_ADR_Y_PUNTOS_DE_FALLA.md` bloque `B6.7`/`ADR-002` (cita textual del hallazgo de Frente 3) más la fila de C1 (`PHY-CLD-03`, "operación de muelle sí; mensajería no"). Columna "MC/decisión": `ADR-002`. Estado: `CONFLICTO ABIERTO (ver F1-CONFLICTO-002)`. Sección A1: `§2.2 (EDGE-RUN)`. Salida a otro frente: `C1/C3/D2`.

La tabla principal de `TRZ_A1.md` pasa de 41 a 42 filas.

---

## 3. `trazabilidad/DECISIONES_Y_ESCALAMIENTOS.md` — 1 fila nueva

Se agrega `F1-CONFLICTO-002` al final de la tabla de decisiones/escalamientos (después de `F1-OBS-003`):

| Campo | Contenido |
|---|---|
| Fecha | 2026-09-06 |
| Entregable | A1 |
| Tipo | CONFLICTO |
| Tema | Emplazamiento físico de `CTX-VESSEL` (A1 lo declara Crítica/replicada en `EDGE-RUN`; C1 lo ubica solo en nube) + seis diferencias adicionales de etiqueta de criticidad entre A1 y C1 |
| Alternativas/impacto | Detalla la contradicción con C1 y cita el hallazgo independiente de Frente 3 (`B6.3`/`B6.7`/`ADR-002` de D2), listando las seis diferencias de criticidad (`GW-EDGE`, `GW-API`, `CTX-INSP`, `CTX-EMIS`, `DATA-DOC`, `SRV-IAM`) |
| Recomendación | Separa lo sustantivo (dónde vive físicamente la operación de muelle de `CTX-VESSEL` — pendiente de `ADR-002` en Puerta 2) de lo menor (las seis diferencias de etiqueta, que no se fuerzan a una equivalencia unilateral) |
| Afecta a | A1, C1, C3, D2 |
| Estado | CONFLICTO ABIERTO (para Puerta 2) |

---

## 4. Resumen para decidir el commit

- Los tres archivos quedan **consistentes entre sí**: la fila nueva de `DECISIONES_Y_ESCALAMIENTOS.md` referencia `TRZ-A1-039`, que a su vez referencia las secciones editadas de `A1_CONTEXTO_Y_ARQUITECTURA_LOGICA.md`.
- Se verificó la integridad estructural de las tablas modificadas (conteo de columnas uniforme) y el conteo de fences `mermaid` de A1 (6, sin cambios) después de cada edición.
- **Pendiente, detectado en esta misma revisión y no corregido todavía:** la fila de SPOF de A1 le asigna a `GW-API` los IDs `SPOF-08`/`SPOF-10` de D2, pero en el catálogo real de D2 esos IDs corresponden a `INT-HUB` y `SRV-IAM` respectivamente — `GW-API` no tiene SPOF propio declarado en D2. Ver sección 1.5 de este documento y el hallazgo `X-1`/`X-2` de `04_AUDITORIA_CRUZADA_A_C_D.md`.
