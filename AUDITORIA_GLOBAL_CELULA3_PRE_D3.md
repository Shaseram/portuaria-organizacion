# Auditoría global independiente de Célula 3 — corte previo a D3

**Fecha del corte:** 2026-09-06  
**Rama auditada:** `frente_3`  
**Commit de referencia:** `bb3da8a`  
**Objeto:** revisar Célula 3 completa antes de corregir, producir diagramas, ejecutar B8/D3 y consolidar el Subdocumento 4.  
**Resultado:** `NO APTO PARA D3 TODAVÍA; APTO PARA OLA DE CORRECCIÓN CONTROLADA`.

## 1. Alcance y criterio

Esta auditoría es deliberadamente más amplia que la auditoría interna de D3. D3 es la puerta formal de integración y cierre; este documento es una revisión independiente previa que busca impedir que D3 consolide contradicciones ya conocidas.

Se contrastaron:

- gobierno de Célula 3: Maestro, Plan, Matriz de Cumplimiento Global y Registro ADR;
- paquetes A1–A3, C1–C4 y D1–D2, incluidos sus índices, trazas, decisiones y auditorías locales;
- esqueletos de D3, Subdocumento 4, T-11 de trabajo, T-11 final y checklist de entrega;
- catálogos vigentes de Célula 2 cuando una afirmación dependía de RF/RNF/RN;
- PDF oficiales solo para asuntos de alto impacto dudoso: precedencia contractual, baja de identidad, plazos de incidentes, propiedad/licencias/datos/IA y alcance BTT.

La jerarquía correcta es la de FEP01 Art. 5.1–5.4: Bases Administrativas y anexos; Bases Técnicas del caso y anexos; aclaraciones/respuestas/modificaciones formales; luego los demás documentos allí enumerados. FEP02 complementa y fija pisos transversales que el caso puede endurecer, nunca rebajar. Los catálogos y Markdown son instrumentos de trabajo, no sustitutos de los PDF.

### Escala

- `CRÍTICO`: contradicción que puede producir incumplimiento contractual o una arquitectura internamente imposible.
- `ALTO`: impide aprobar un paquete, cerrar una vista o demostrar trazabilidad 1:1.
- `MEDIO`: defecto de gobierno o evidencia que puede inducir una lectura incorrecta, pero tiene corrección directa.
- `BLOQUEANTE PLANIFICADO`: ausencia deliberada y conocida; no es un error de autor, pero debe cerrarse antes de D3/entrega.

## 2. Veredicto ejecutivo

Se registran **22 hallazgos**:

| Clase | Cantidad | Lectura |
|---|---:|---|
| Críticos | 3 | deben corregirse antes de aprobar D1/D2 o producir diagramas definitivos |
| Altos | 11 | deben cerrarse o convertirse en dependencia externa formalmente tratada |
| Medios | 5 | saneamiento rápido de gobierno y trazabilidad |
| Bloqueantes planificados | 3 | diagramas, decisiones/aceptaciones y consolidación D3/T-11 |

No se recomienda reiniciar los entregables. La base útil es amplia:

- A1 declara 16 actores y 24 componentes; A2, 21 contrapartes y 7 familias técnicas; A3 desarrolla las secuencias críticas y la convivencia TOS;
- C1 declara 21 nodos; C2/C3 especifican plataforma, recinto, red, ambientes y continuidad; C4 aporta cálculos reproducibles y candidatos T-11;
- D1 define 31 controles y una política explícita de admisión de eventos; D2 cruza 24/24 componentes, 11/11 sistemas canónicos y 21/21 nodos, con 73 amenazas y 22 SPOF;
- D1–D2 distinguen correctamente diseño documental, evidencia futura, aceptación de riesgo y aprobación.

La brecha no es falta de trabajo técnico general, sino que **las vistas no forman todavía una única arquitectura aprobable y la trazabilidad global quedó por detrás de los paquetes**.

## 3. Resumen de hallazgos y dueño

| ID | Sev. | Hallazgo | Dueño primario | Tipo de cierre |
|---|---|---|---|---|
| `AGC3-001` | CRÍTICO | jerarquía contractual incorrecta en Frente 2 | Gobierno/F2 | corrección interna inmediata |
| `AGC3-002` | CRÍTICO | baja IAM medida desde reconexión en A1 | A1/D1 | corrección interna + dependencia externa |
| `AGC3-003` | CRÍTICO | `CTX-VESSEL` crítico/local en A1–A3 pero solo nube en C1 | A1/A3/C1 | decisión y corrección cruzada |
| `AGC3-004` | ALTO | alcance BTT incompleto en gobierno: RT-06, Cap. 7 y checklist C | Gobierno/F2 | corrección interna |
| `AGC3-005` | ALTO | matriz global no refleja el desarrollo real | Integrador/D3 | consolidación interna |
| `AGC3-006` | ALTO | seis criticidades A1↔C1 sin resolver | A1/C1 | corrección cruzada |
| `AGC3-007` | ALTO | `CH-CAB` reducido al muelle en C1 | A1/C1/C3 | corrección cruzada |
| `AGC3-008` | ALTO | `ACT-TI` sin canal y actores sin consumo transversal suficiente | A1/D1/D3 | corrección interna |
| `AGC3-009` | ALTO | SIEM posiblemente duplicado y capacidad local no demostrada | C2/C4/D1 | corrección y recálculo |
| `AGC3-010` | ALTO | `ADR-011` incompleto y estados ADR desfasados | C2/integrador | completar y sincronizar |
| `AGC3-011` | ALTO | Célula 2 intercambia RT-11.18 y RT-11.19 | Célula 2/integrador | corrección de fuente derivada |
| `AGC3-012` | ALTO | obligaciones BA Art. 77 y 84–86 sin traza arquitectónica | Gobierno/A1–D1 | incorporar controles |
| `AGC3-013` | ALTO | auditorías locales F1/F2 vacías | revisores F1/F2 | revisión independiente |
| `AGC3-014` | ALTO | trazas de paquetes siguen sin cierre/revisión | autores/revisores | revisar y promover estados |
| `AGC3-015` | MEDIO | estado vigente de D2 anuncia B7 como futuro | D2 | corrección editorial de estado |
| `AGC3-016` | MEDIO | `RNF-ARQ` se cita aunque esa categoría no existe | C1 | corrección de traza |
| `AGC3-017` | MEDIO | tres enlaces Markdown rotos o mal resueltos | Gobierno/A2/C4 | corrección mecánica |
| `AGC3-018` | MEDIO | referencias a ramas/archivos históricos no disponibles | F1/integrador | normalizar evidencia local |
| `AGC3-019` | MEDIO | doble DoD y estados históricos/vigentes ambiguos | F2/D2 | unificar lectura canónica |
| `AGC3-020` | PLANIFICADO | fuentes/exportaciones de diagramas pendientes | todos/B8 | ejecutar después de corrección |
| `AGC3-021` | PLANIFICADO | 0 ADR aprobados y 0 SPOF aceptados/cerrados | autores/CLIENTE | decisión o escalamiento formal |
| `AGC3-022` | PLANIFICADO | D3, consolidado y T-11 siguen como esqueletos | D3/integrador | ejecutar puerta final |

## 4. Hallazgos críticos

### `AGC3-001` — La jerarquía contractual de Frente 2 está invertida

**Evidencia.** [`DECISIONES_Y_ESCALAMIENTOS.md`](../../02_Frente_Fisica_Despliegue/trazabilidad/DECISIONES_Y_ESCALAMIENTOS.md) §inicio afirma `FEP03 > FEP02 > FEP01`. El [Maestro](../../00_Gobierno/00_MAESTRO_CONTEXTO_ARQUITECTURA.md) §1 conserva correctamente FEP01 Art. 5.1–5.4.

**Problema.** FEP01 ubica las Bases Administrativas primero. Además, las obligaciones de los documentos se complementan; no corresponde usar una jerarquía técnica simplificada para descartar un requisito transversal o administrativo.

**Impacto.** Una contradicción futura podría resolverse contra una fuente de menor precedencia, debilitando alcance, seguridad, continuidad o una condición de oferta.

**Corrección.** Sustituir la fórmula por la regla completa del Maestro y enlazarla, sin inventar una jerarquía alternativa entre FEP02 y FEP03. Toda ambigüedad real se registra y consulta; mientras tanto se conserva la lectura acumulativa/más exigente.

**Cierre verificable.** No queda ninguna ocurrencia de `FEP03 > FEP02 > FEP01`; todos los registros de decisión remiten a Maestro §1/FEP01 Art. 5.

### `AGC3-002` — A1 desplaza ilegalmente el reloj de baja de identidad a la reconexión

**Evidencia.** [A1](../../01_Frente_Logica_Integracion/A1_CONTEXTO_Y_ARQUITECTURA_LOGICA.md) §2.5 y §3.2 afirma dos veces que la baja efectiva ≤24 h se cuenta desde la reconexión. FEP02 `RT-12.10` exige baja no superior a 24 h **desde la desvinculación**. [D1](../D1_ARQUITECTURA_DE_SEGURIDAD.md) B2.4 y [TRZ_D1](TRZ_D1.md) conservan el reloj correcto y declaran la revocación durante aislamiento como `F3-ESC-002`.

**Problema.** Un corte exterior puede durar 72 h. Contar desde la reconexión permitiría que una identidad desvinculada siga siendo válida hasta 96 h o más, contradiciendo el requisito obligatorio.

**Impacto.** Invalida el supuesto de `SRV-IAM` como autoridad única con simples sesiones cacheadas y afecta `ADR-008`, `SPOF-10`, relevo de turno, terminales compartidos y acceso de emergencia.

**Corrección.** En A1, eliminar el desplazamiento del reloj; declarar que el diseño debe permitir revocación/bloqueo local o un mecanismo alternativo efectivo dentro de 24 h desde la desvinculación. Mantener como externo el directorio, canal de aviso y producto real, pero no el cumplimiento del reloj.

**Cierre verificable.** A1, D1, ADR-008 y pruebas previstas dicen lo mismo; existe escenario de baja durante corte de 72 h y criterio de aceptación ≤24 h desde la desvinculación.

### `AGC3-003` — `CTX-VESSEL` hace imposible la continuidad declarada

**Evidencia.** [A1](../../01_Frente_Logica_Integracion/A1_CONTEXTO_Y_ARQUITECTURA_LOGICA.md) incluye `CTX-VESSEL` como crítico dentro de `EDGE-RUN`; [A3](../../01_Frente_Logica_Integracion/A3_PROCESOS_CRITICOS_Y_TOS.md) dice que la operación de nave continúa localmente. [C1](../../02_Frente_Fisica_Despliegue/C1_ARQUITECTURA_FISICA_Y_EMPLAZAMIENTO.md) lo emplaza solo en `PHY-CLD-03`, con criticidad alta, aunque su tabla reconoce “operación de muelle sí; mensajería no”. D2 lo registra como `B6-F03`.

**Problema.** No existe nodo local que ejecute la parte de operación de nave que A1/A3 declaran disponible durante el corte. Separar operación local de mensajería diferida es válido, pero C1 no modela esa partición.

**Impacto.** `ADR-002` no puede aprobarse; `EDGE-RUN` carece de frontera física estable; capacidad local, amenazas, T-11 y diagramas quedarían construidos sobre universos distintos.

**Corrección.** Definir una única partición: núcleo funcional de operación de nave local en `PHY-OPS-01` y adaptadores/mensajería externa diferidos o bufferizados; o cambiar A1/A3 mediante decisión fundada. Actualizar criticidad, emplazamiento, capacidad, amenazas y traza en conjunto.

**Cierre verificable.** Una fila única permite seguir `CTX-VESSEL → EDGE-RUN → PHY-OPS/CLD → cálculo → T-11 → prueba 72 h` sin contradicción.

## 5. Hallazgos altos

### `AGC3-004` — El gobierno aún trunca el alcance BTT

Hay tres defectos relacionados:

1. [Maestro](../../00_Gobierno/00_MAESTRO_CONTEXTO_ARQUITECTURA.md) §10.3 todavía dice `RT-06.01..24`; FEP02 §3.2 exige aplicar íntegramente `RT-06.01..34` a la sala principal sustantiva.
2. Maestro §9.2 resume algunos umbrales del Cap. 7, pero no controla los catorce requisitos de site secundario/DR; C2/C3 sí absorbieron gran parte, dejando al gobierno por detrás.
3. La [Matriz Global](../../00_Gobierno/02_MATRIZ_CUMPLIMIENTO_GLOBAL.md) no incorpora el checklist de 28 entregables del Capítulo C del BTT, pese a `F2-ESC-005`.

Esto puede ocultar custodia/inventario de medios, espacio de operación separado, rutas físicas distintas, análisis de amenazas comunes, replicación observable, retorno al principal y evidencia formal de oferta.

**Corrección.** Corregir el rango; crear cobertura explícita `RT-07.01..14`; agregar una matriz de los 28 entregables con dueño, Sobre, artefacto, evidencia y estado. No duplicar narrativa: el gobierno controla y enlaza, los paquetes desarrollan.

### `AGC3-005` — La Matriz Global no representa el avance de los paquetes

**Evidencia.** En [Matriz Global](../../00_Gobierno/02_MATRIZ_CUMPLIMIENTO_GLOBAL.md) §3, `GTR-001..016` conserva numerosas celdas `POR DEFINIR`, aunque A1–C4 ya tienen componentes, nodos, controles y cálculos. Solo `GTR-017..019` refleja el cruce reciente de D1/D2. La sección 5 físico–T-11 mantiene una única fila `POR DEFINIR`.

**Impacto.** No se puede demostrar la cadena principal exigida por el equipo: `fuente → MC/RF/RNF → componente → nodo → control → diagrama → T-11 → evidencia`. La cobertura local existe, pero no hay vista global auditable.

**Corrección.** Actualizar `GTR-001..019` desde las trazas vigentes; descomponer filas heterogéneas cuando una sola no permita verificar afirmaciones distintas; completar el control físico–T-11 desde C1/C2/C3/C4/D1. La matriz debe apuntar a evidencia, no declarar cumplimiento por mera existencia de texto.

### `AGC3-006` — Seis criticidades adicionales no tienen autoridad canónica

D2 B6.3 identifica:

| Componente | A1 | C1 |
|---|---|---|
| `CTX-EMIS` | alta | media |
| `CTX-INSP` | alta | media |
| `DATA-DOC` | alta | media |
| `GW-API` | alta | media |
| `GW-EDGE` | alta | media |
| `SRV-IAM` | alta | crítica |

La criticidad gobierna HA, ubicación, capacidad, continuidad, pruebas y T-11; no es solo una etiqueta editorial.

**Corrección.** Definir criterio común —impacto contractual, continuidad, pérdida de datos, exposición y dependencia— y resolver cada fila. Actualizar A1, C1, D2, C4 y matriz global en el mismo cambio.

### `AGC3-007` — `CH-CAB` quedó físicamente reducido al muelle

**Evidencia.** A1 usa `CH-CAB` para cabina y terreno: grúas, equipos de patio, gate/terminal compartido y sombra de radio de 8 h. C1 lo mapea únicamente a `PHY-EDG-04` muelle.

**Impacto.** Distorsiona cobertura radio, inventario de dispositivos, amenazas `THR-025/067`, escenario `SCN-11` y cantidades T-11.

**Corrección.** Modelar `CH-CAB` como canal desplegado en las clases de equipo/emplazamientos que realmente lo usan, sin crear un componente lógico por ubicación. C1/C3/C4 deben compartir la misma matriz de instancias y cantidades.

### `AGC3-008` — Administración y actores no cierran de extremo a extremo

**Evidencia.** A1 declara `ACT-TI` con “consola de administración”, pero no existe un componente de canal que la materialice. `F1-OBS-002` lo reconoce. La traza de actores agrupa los 16 en solo dos filas y la mayoría no reaparece nominalmente en A2/A3/C1–C4/D1; `F1-OBS-003` ya advertía consumo downstream insuficiente.

**Impacto.** PAM, grabación de sesión, break-glass, operación con TI=5, responsabilidades de `THR-034/062` y aceptación de `SPOF-13` quedan sin actor/canal estable.

**Corrección.** Resolver si existe un cuarto canal administrativo o una especialización explícita de uno existente; crear matriz `ACT-* → canal → rol/perfil → operación → componente → control → evidencia`. No inventar personas nominales; usar roles y dejar nombres como dependencia del CLIENTE.

### `AGC3-009` — SIEM/T-11 puede duplicarse y el buffer se declaró cerrado prematuramente

**Evidencia.** [C2](../../02_Frente_Fisica_Despliegue/C2_TECNOLOGIAS_HARDWARE_Y_DATA_CENTERS.md) crea `T11-C2-19` para “observabilidad y SIEM”. [C4](../../02_Frente_Fisica_Despliegue/C4_DIMENSIONAMIENTO_Y_T11.md) crea además `T11-SEC-04` para plataforma SIEM/registro. C4 §9.ter calcula ≈8 GB/año y ≈0,07 GB/72 h como **piso**, reconoce que faltan logs de plataforma/red/borde —posible término dominante—, pero afirma que no hay que reabrir los ≈50 GB locales. D1 B5.2.1, ya disponible, exige dimensionar por clase con EPS, bytes, peak, indexación, réplica y compresión medidos, y no duplicar telemetría cruda.

**Problema.** El piso promedio no demuestra el buffer al peak ni el total de la plataforma. Además, C4 cuenta todas las transacciones de negocio como eventos de seguridad, mientras D1 solo exige éxitos cuando hay auditoría/no repudio y prioriza fallos/anomalías.

**Corrección.** Reservar una sola fila comercial para SIEM/logging o separar explícitamente “observabilidad operacional” de “SIEM de seguridad”, sin solape de licencias/ingesta. Recalcular `T11-SEC-04` desde la política D1 y conservar el tamaño como rango/medición pendiente hasta disponer de productos y fuentes reales. Retirar la conclusión categórica sobre 50 GB hasta demostrar peak de 72 h más margen.

### `AGC3-010` — `ADR-011` existe, pero todavía no es una decisión

**Evidencia.** El [Registro ADR](../../00_Gobierno/03_REGISTRO_ADR_GLOBAL.md) lo declara `CANDIDATO`. C2 todavía dice “no existe”, “propuesto, no abierto”; `TRZ_C2` pide abrirlo; F1 dice que aún no existe. D2 lo revisa correctamente como candidato, pero solo hay criterios: no compara proveedores/regiones concretos ni selecciona alternativa.

**Impacto.** Proveedor, regiones, residencia, fallo común, carbono, servicios, reversibilidad, DR y T-11 siguen condicionados. No puede aprobarse `SPOF-22` ni la topología cloud.

**Corrección.** Primero sincronizar toda mención a `CANDIDATO`. Luego documentar al menos dos alternativas reales con proveedor/regiones disponibles, latencia, dominios de fallo, residencia, intensidad de carbono, catálogo, costo cualitativo y salida. Si el dato de mercado/CLIENTE aún falta, dejar criterios y consulta, sin promoverlo a `PROPUESTO`.

### `AGC3-011` — Célula 2 intercambia las referencias RT de incidentes y brechas

**Evidencia.** [`RNF.md`](../../../Celula2/01_Requerimientos/RNF.md) asigna `RNF-SEG-07` (brecha ≤24 h) a `RT-11.18` y `RNF-SEG-11` (incidente crítico ≤2 h) a `RT-11.19`. FEP02 §11.3 establece lo contrario: `RT-11.18` = incidente crítico comunicado ≤2 h; `RT-11.19` = brecha ≤24 h y causa raíz ≤5 días hábiles. D1/TRZ_D1 usan correctamente los plazos sustantivos y registran el cruce.

**Corrección.** Célula 2 debe intercambiar solo las referencias de fuente, sin cambiar IDs RNF ni plazos. Después se actualiza el corte consumido por Célula 3. Mientras tanto, toda traza debe mantener la salvedad explícita de TRZ_D1 §4.

### `AGC3-012` — Faltan obligaciones administrativas con efecto arquitectónico directo

La Célula 3 menciona reversibilidad técnica, repositorio del CLIENTE, privacidad e IA condicional, pero no existe una cadena explícita a FEP01:

| Fuente | Exigencia con efecto en Subdocumento 4 | Brecha actual |
|---|---|---|
| Art. 77 | plan de reversibilidad dentro de 90 días, actualización anual, formatos abiertos y acompañamiento ≥90 días | se trata vendor lock-in, no el plan/criterio contractual completo |
| Art. 84 | propiedad del CLIENTE desde creación; licencias de terceros a su nombre; preexistentes declarados; control OSS; código en repo CLIENTE; escrow semestral | IaC/repo y SCA aparecen, pero no la cadena completa ni el escrow/T-11 |
| Art. 85 | acuerdo de tratamiento, subencargados autorizados, derechos, eliminación certificada, transferencia internacional autorizada | D1 cubre controles técnicos, pero no todos los actos/aceptaciones contractuales |
| Art. 86 | modelo/proveedor/versión/ubicación, no entrenamiento, validación humana, riesgos, auditoría y desactivación sin afectar el resto | `STD-18` solo pide declarar uso/controles o `NO APLICA` |

**Impacto.** Selección cloud, licencias, DevSecOps, arquitectura de datos, IA/innovaciones, salida y T-11 podrían cumplir técnicamente y aun así incumplir contrato.

**Corrección.** Agregar filas GTR/controles específicos, asignar paquete y evidencia, y reflejar su efecto en ADR-011, D1, C2/C3 y Subdocumento 5. Si no se incorpora IA, emitir `NO APLICA JUSTIFICADO` en lugar de dejar `PENDIENTE` indefinido.

### `AGC3-013` — Las auditorías locales obligatorias de F1 y F2 están vacías

**Evidencia.** [`F1/AUDITORIA_CIERRE.md`](../../01_Frente_Logica_Integracion/trazabilidad/AUDITORIA_CIERRE.md) y [`F2/AUDITORIA_CIERRE.md`](../../02_Frente_Fisica_Despliegue/trazabilidad/AUDITORIA_CIERRE.md) conservan todas las casillas en `PENDIENTE`, brechas `POR COMPLETAR` y revisor `POR ASIGNAR`. D3 declara estas auditorías como entradas obligatorias.

**Corrección.** Cada frente debe ejecutar una revisión independiente, nombrar revisor, registrar evidencia por control y emitir veredicto. El autor puede corregir después, pero no autoaprobar sin revisión cruzada.

### `AGC3-014` — Las trazas no permiten promover los paquetes

Los paquetes contienen material técnico desarrollado, pero C1–C4 siguen declarando `TRZ_C*.md completo — en curso`; A1 mantiene revisión cruzada pendiente; gran parte de las filas `TRZ-A*` y `TRZ-C*` están `PARA REVISIÓN`. D1/D2 continúan `EN CURSO` y no tienen contenido aprobado para el consolidado.

**Problema.** “Contenido listo para integrar” describe ubicación editorial, no aprobación. La regla global permite consolidar solo `APROBADO`.

**Corrección.** Tras resolver los hallazgos semánticos, revisar cada traza, promover solo las filas comprobadas y dejar externas/condicionadas con dueño, fallback y evidencia de cierre. No cambiar todo masivamente a `APROBADO`.

## 6. Hallazgos medios

### `AGC3-015` — El encabezado vigente de D2 está desfasado

[D2](../D2_AMENAZAS_ADR_Y_PUNTOS_DE_FALLA.md) §“Plan de desarrollo acordado” dice que B7 es el siguiente bloque, mientras su tabla y punto de continuación afirman correctamente que B7/B7-R/B7-C ya se ejecutaron.

**Corrección.** Actualizar solo el estado vigente del encabezado; conservar los cortes históricos identificados como tales.

### `AGC3-016` — `TRZ_C1` usa una categoría RNF inexistente

[`TRZ_C1.md`](../../02_Frente_Fisica_Despliegue/trazabilidad/TRZ_C1.md) fila `TRZ-C1-001` cita “RNF-ARQ aplicables”. La propia Matriz Global `GTR-002` aclara que Célula 2 no posee categoría `RNF-ARQ`.

**Corrección.** Citar directamente `FEP02 RT-02.01` y, si aplica, los RNF reales asociados; no fabricar una familia de identificadores.

### `AGC3-017` — Hay enlaces Markdown que no llevan a evidencia

1. [Registro de alineación](../../00_Gobierno/05_REGISTRO_ALINEACION_CELULA2.md) línea de `C2-HIS`: el paréntesis del nombre no está escapado y rompe el destino Markdown.
2. [A2](../../01_Frente_Logica_Integracion/A2_ARQUITECTURA_DE_INTEGRACION.md) §1.1 enlaza un `.md` de FEP03 que no existe.
3. [C4](../../02_Frente_Fisica_Despliegue/C4_DIMENSIONAMIENTO_Y_T11.md) §10 usa `../../90_Consolidado/...`; desde su carpeta resuelve fuera de `Celula3`. El destino correcto comienza con `../90_Consolidado/...`.

**Corrección.** Reparar destinos y repetir el barrido global, no solo el paquete D1/D2.

### `AGC3-018` — Algunas evidencias siguen atadas a una rama o archivo inexistente

F1 conserva referencias a `git show origin/frente_2` aunque F2 ya está integrado, y cita `Celula2/RECORDATORIO_ANTES_DE_ENTREGA.md`, archivo que no existe en el árbol actual. Eso impide que otro auditor reproduzca la evidencia desde el corte compartido.

**Corrección.** Apuntar al archivo integrado y sección estable; si un antecedente no se conserva, absorber su conclusión en el registro vigente con fuente oficial/catálogo verificable.

### `AGC3-019` — El estado se expresa en dos DoD incompatibles

C1–C4 mantienen el contrato inicial con casillas sin marcar y, más abajo, una “Definición de terminado — estado” con varias casillas cerradas. D2 mezcla cortes históricos y estado vigente; F1/F2 no marcan siempre cuál tabla es canónica.

**Impacto.** Lectores y automatizaciones pueden concluir simultáneamente que un control está pendiente y cumplido.

**Corrección.** Mantener el contrato como lista normativa sin estado o rotularlo `plantilla histórica`; conservar una sola tabla de estado vigente por paquete, fechada, y enlazar los cortes anteriores.

## 7. Bloqueantes planificados, no defectos inesperados

### `AGC3-020` — Diagramas diferidos

Las carpetas `diagramas/` de los tres frentes están vacías. A1–A3 incluyen Mermaid en línea, pero faltan las vistas físicas, despliegue/red, fronteras de seguridad, leyendas, exportaciones y versión citada. La decisión de dibujar después de auditar es razonable; sigue siendo condición obligatoria de B8/D3.

**Puerta de inicio.** No dibujar hasta cerrar `AGC3-001..010`, especialmente `CTX-VESSEL`, criticidades, `CH-CAB`, IAM y SIEM. De otro modo los diagramas cristalizan contradicciones.

### `AGC3-021` — Decisiones, riesgos y evidencia externa aún no están aprobados

Estado vigente: 11 ADR registrados —7 `PROPUESTO`, 4 `CANDIDATO`, 0 `APROBADO`—; 22 SPOF —11 `POR ACEPTAR`, 11 `ESCALADO`, 0 aceptados/cerrados—. Además faltan productos/contratos, responsables nominales, site survey, capacidad real de enlaces, directorio/federación, pruebas y aceptaciones.

Esto no exige inventar respuestas. Cada externo debe quedar con dueño, fecha/hito, fallback conservador, efecto si no se obtiene y evidencia de aceptación. Los ADR que puedan decidirse con información interna deben cerrarse antes de etiquetarlos como externos.

### `AGC3-022` — D3 y el consolidado todavía son esqueletos

[`D3`](../D3_AUDITORIA_Y_CONSOLIDACION.md) está pendiente; [`00_CONTENIDO_FINAL_SUBDOCUMENTO_4.md`](../../90_Consolidado/00_CONTENIDO_FINAL_SUBDOCUMENTO_4.md) conserva todas las secciones por integrar; [`01_T11_TRABAJO_TRAZABLE.md`](../../90_Consolidado/01_T11_TRABAJO_TRAZABLE.md) tiene una fila ficticia; el formulario final y checklist siguen vacíos.

Esto es correcto para el corte pre-D3. Se convierte en incumplimiento si se intenta declarar cierre antes de ejecutar las olas siguientes.

## 8. Pendientes externos que sí pueden preservarse

Estos asuntos no deben inventarse para cerrar el documento. Pueden quedar abiertos si el diseño conserva un rango/fallback y la traza registra dueño, hito y evidencia:

| Dependencia | Dueño externo o coordinador | Tratamiento conservador actual | Evidencia para cerrar |
|---|---|---|---|
| capacidad y conmutación real de fibra/radioenlace | CLIENTE/proveedores; C3/C4 | diseñar operación normal y reposición por separado; no prometer ≤90 min sobre un enlace no medido | capacidad sostenida, prueba de corte y recuperación |
| site survey con patio cargado, sombras y handover | CLIENTE/proveedor de red; C3 | cantidades por rango y ubicación condicionada | informe de cobertura/carga y failover |
| dos ingresos físicos independientes al edificio | CLIENTE; C1/C2/C3 | no aprobar alternativa de sala actual si no se demuestra cumplimiento | plano/inspección y diseño de rutas |
| aprobación para intervenir/segregar la red de protección | autoridad de protección/CLIENTE | no intervenir VMS/ISPS; conductos controlados propuestos | autorización y prueba de no degradación |
| tamaño real de imágenes OCR/patente/contenedor | CLIENTE/fabricante; C4 | mantener sensibilidad y margen declarado, sin fijar cantidad final | muestras representativas y percentiles |
| directorio, federación y aviso de desvinculación durante aislamiento | CLIENTE; A1/D1 | requisito de baja ≤24 h intacto; producto/mecanismo por validar | contrato IAM, prueba offline y cronología |
| contratos, versiones, SLA y capacidades de TOS/periféricos/terceros | CLIENTE/fabricantes; A2/A3 | adaptadores, timeouts y fallbacks sin inventar protocolo | contrato técnico y prueba por interfaz |
| catálogo campo→propietario→sensibilidad→retención→custodia | Subdocumento 5/CLIENTE; D1 | clasificación mínima y cifrado conservadores | catálogo aprobado y cruce completo |
| responsables nominales, custodios, aceptadores y contactos | CLIENTE/adjudicatario | roles propuestos, nunca nombres inventados | RACI y acta de aceptación |
| proveedor/regiones/productos y cotización técnica final | adjudicatario/CLIENTE; ADR-011/C2 | criterios y candidatos sin selección ficticia | comparación, decisión y ficha vigente |

No son externos: corregir textos, resolver criticidades entre A1/C1, delimitar `CH-CAB`, reparar enlaces, actualizar trazas, evitar doble conteo y completar auditorías locales.

## 9. Plan de corrección por olas

### Ola 1 — Correcciones que no dependen de terceros

1. Corregir jerarquía contractual y rango `RT-06.01..34`.
2. Corregir el reloj IAM en A1 y sincronizarlo con D1/ADR-008.
3. Corregir referencias RT-11.18/19 en Célula 2 o registrar el commit pendiente de su dueño.
4. Reparar enlaces, `RNF-ARQ`, estado vigente de D2 y menciones ADR desfasadas.
5. Incorporar a gobierno Cap. 7, checklist C y BA Art. 77/84–86.

**Salida:** ninguna contradicción contractual o referencia inválida conocida.

### Ola 2 — Consistencia semántica entre frentes

1. Resolver `CTX-VESSEL` y `ADR-002`.
2. Resolver las seis criticidades.
3. Resolver despliegue de `CH-CAB`.
4. Resolver canal administrativo `ACT-TI` y matriz de actores/roles.
5. Delimitar observabilidad operacional versus SIEM y recalcular el buffer/rango de ingesta.

**Salida:** catálogo lógico, físico, seguridad y capacidad cuentan una sola solución.

### Ola 3 — Trazabilidad, decisiones y revisión independiente

1. Completar auditorías locales F1/F2 y contraste con esta auditoría y las de los demás agentes.
2. Completar/revisar `TRZ_A*`, `TRZ_C*`, `TRZ_D*` y matriz global.
3. Completar `ADR-011`; resolver/promover los ADR con información suficiente.
4. Construir T-11 de trabajo y control 1:1; mantener externos como rango o condición.
5. Formalizar SPOF/residuales: aceptación, escalamiento o mitigación, nunca “cerrado” por descripción.

**Salida:** paquetes elegibles para promoción individual a `APROBADO` o `BLOQUEADO EXTERNO TRATADO`.

### Ola 4 — Representación y cierre

1. Producir y revisar los diagramas con IDs ya estabilizados.
2. Ejecutar B8 de D1/D2.
3. Ejecutar D3 sobre auditorías locales, matriz global, ADR y T-11.
4. Integrar únicamente contenido aprobado al Subdocumento 4.
5. Emitir T-11 final de cinco columnas y checklist/acta de brechas.

## 10. Criterios mínimos para autorizar D3

- [ ] `AGC3-001..003` cerrados.
- [ ] No quedan discrepancias A1↔C1 sin decisión registrada.
- [ ] Matriz global actualizada hasta componente, nodo, control, T-11 y evidencia.
- [ ] F1 y F2 tienen auditoría local con revisor y veredicto.
- [ ] Cada traza pendiente distingue trabajo interno de dato/autoridad externa.
- [ ] `ADR-011` tiene estado coherente y alternativas reales, o bloqueo externo preciso.
- [ ] SIEM/observabilidad tiene frontera comercial y cálculo no duplicado.
- [ ] T-11 de trabajo existe y el control físico↔cantidad es bidireccional.
- [ ] Los pendientes externos tienen dueño, fallback, efecto, hito y evidencia requerida.
- [ ] Se conserva la decisión de no dibujar hasta estabilizar estas materias.

## 11. Regla para comparar las auditorías del equipo

No se debe votar por cantidad de hallazgos. Para cada hallazgo aportado por otro auditor:

1. identificar fuente oficial o identificador estable;
2. comprobar si es contradicción, omisión, dato externo o trabajo deliberadamente diferido;
3. localizar el dueño del texto y los consumidores afectados;
4. acordar una corrección única y su criterio de cierre;
5. actualizar trazas y matriz global en el mismo cambio;
6. conservar en el acta los desacuerdos no resueltos, sin corregirlos silenciosamente.

## 12. Conclusión

Célula 3 está **mucho más cerca de una corrección integrada que de una reescritura**. D1 y D2 cumplieron su función de descubrir dependencias cruzadas, pero no pueden cerrarse todavía como entregables: A1/C1 discrepan sobre continuidad e identidad, la gobernanza contractual tiene rezagos y la traza global/T-11 no materializa aún el trabajo local.

La secuencia segura es: **corregir contradicciones → contrastar auditorías → actualizar trazabilidad/ADR/T-11 → diagramar → B8 → D3 → Subdocumento 4**. Los datos realmente externos pueden permanecer pendientes si están tratados de forma conservadora y verificable; las inconsistencias internas no deben disfrazarse como dependencias externas.
