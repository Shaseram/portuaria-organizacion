# Plan de corrección — seis incoherencias de contenido en Célula 3

**Fecha:** 2026-09-06
**Rama y commit sobre el que se verificó:** `main` · posterior a `399e915` (baseline MA-8)
**Autor:** Frente 2, en rol de integrador.

## Qué es este documento y qué no es

Es una lista de **seis incoherencias de sustancia** entre lo que afirman distintos documentos de Célula 3, y entre Célula 3 y los catálogos de Célula 2. Cada una viene con la cita literal de los dos lados, para que puedan comprobarla sin creerme.

**No es una auditoría más.** La auditoría semántica y contractual de `06_AUDITORIA_FINAL_SEMANTICA_CONTRACTUAL_INFORME1.md` ya cubrió dieciocho hallazgos y sus correcciones MA-3 a MA-8 están aplicadas y verificadas. Esto es **complementario**: revisa una dimensión que esa auditoría no tocó —la historia de la convivencia con el TOS y el traspaso— y la trazabilidad hacia los catálogos de Célula 2. Se comprobó una por una que ninguna de las seis está en sus dieciocho.

**No hay que rediseñar nada.** Las seis son declaraciones que hay que precisar, citas que faltan o una decisión de calendario. Ninguna exige cambiar la arquitectura.

## Cómo comprobarlo ustedes mismos

Cada cita lleva `archivo:línea`. Para verla:

```bash
cd portuaria-organizacion
sed -n '295p' Celula3/01_Frente_Logica_Integracion/A3_PROCESOS_CRITICOS_Y_TOS.md
```

## Resumen

| # | Incoherencia | Severidad | Dueño |
|---|---|---|---|
| 1 | La Etapa 1 pasa a producción **sin marcha blanca**; C3 llama marcha blanca a la sombra del congelamiento | **ALTO** | A3 + C3, con decisión de equipo |
| 2 | Seis requisitos de tractocamiones —cuatro Críticos— no los cita nadie, y son la causa declarada de la brecha de productividad | **ALTO** | A1 + A2 |
| 3 | A3 es el documento de convivencia y cita 3 de los 14 requisitos de convivencia | **ALTO** | A3 |
| 4 | El TOS está en la sala, pero tres documentos postergan su conciliación «a la reconexión» | **ALTO** | A1 + C3 (C1 es el que está bien) |
| 5 | La unidad del traspaso no es la misma en A3 y en C3 | **ALTO** | A3 + C3 |
| 6 | El Maestro cuenta 80 equipos a instrumentar donde el caso cuenta 74 | **MEDIO** | Maestro (integrador) |

---

## Hallazgo 1 · La Etapa 1 entra a producción sin marcha blanca

**Severidad: ALTO.** Es el más importante de los seis.

### En simple

Hay tres cosas distintas que se están confundiendo:

- **Congelamiento** — del 15 de diciembre al 30 de abril es la temporada de fruta. El caso prohíbe *intervenir sistemas* y prohíbe *pasar a producción*. No se puede tocar nada.
- **Marcha blanca** — es hacer funcionar el sistema nuevo **en paralelo con la operación real**, escribiendo datos de verdad, conciliando los dos registros y pudiendo volver atrás. El caso la exige antes de cualquier paso a producción.
- **Sombra** — es mirar sin tocar: el sistema nuevo lee y compara, pero no escribe ni decide nada.

La diferencia importa: para conciliar «ambos registros» tiene que haber **dos registros**, o sea el sistema nuevo tiene que estar escribiendo. Y para «volver atrás» tiene que tener **autoridad** sobre algo. Una sombra no escribe y no tiene autoridad, así que no hay nada que conciliar ni nada que revertir. **Marcha blanca y sombra no son lo mismo.**

Nuestro calendario pone tres meses de sombra dentro del congelamiento y luego pasa a producción. C3 llama a esos tres meses «marcha blanca». Con eso, la Etapa 1 —que es la sustitución del registro de todos los contenedores, lo que el caso llama el mayor riesgo del proyecto— **entraría a producción sin haber escrito nunca un dato real en convivencia**.

### Lo que dice cada lado

**El caso, Cap. 13.3, condición 1:**
> *«Nada entra en producción sin haber convivido con la forma actual de trabajar durante la marcha blanca correspondiente, **con conciliación entre ambas** y **con la posibilidad de volver atrás**.»*

**El caso, Cap. 13.3, condición 5**, específica para el TOS:
> *«La sustitución o el envolvimiento del sistema de operación de 2012 es el punto de mayor riesgo del proyecto: por él pasa todo el registro de la operación. **Su marcha blanca debe contemplar convivencia real, conciliación de ambos registros y un procedimiento de retorno probado.**»*

**El caso, Cap. 13.3, condición 3:**
> *«El paso a producción no puede ocurrir entre el 15 de diciembre y el 30 de abril.»*

**Nuestro Maestro, regla negativa 15** — `Celula3/00_Gobierno/00_MAESTRO_CONTEXTO_ARQUITECTURA.md:736`:
> *«No llamar marcha blanca a una intervención durante el congelamiento.»*

**A3, calendario ejecutable** — `Celula3/01_Frente_Logica_Integracion/A3_PROCESOS_CRITICOS_Y_TOS.md`:
> `:354` — *«Versión candidata Etapa 1 lista, instalada, con retorno probado | ≤12 | **14-dic-2027**»*
> `:355` — *«Validación paralela no invasiva, **solo lectura/sombra, sin autoridad** | 13-15 | 15-dic-2027 a 30-abr-2028»*
> `:356` — *«Producción Etapa 1 | 16 | **mayo 2028**»*
> `:358` — *«**Marcha blanca Etapa 2** | 19-20 | ago-sep 2028 | No [dentro del congelamiento]»*

**C3, calendario** — `Celula3/02_Frente_Fisica_Despliegue/C3_DESPLIEGUE_RED_Y_CONTINUIDAD.md:367`:
> *«Producción Etapa 1 | 16 | **tras tres meses de marcha blanca con plan de reversión activo**»*

### Por qué es una incoherencia real

Los «tres meses» previos al mes 16 son los meses 13, 14 y 15: exactamente el congelamiento. A3 dice que ahí solo cabe sombra **sin autoridad**; C3 los llama marcha blanca **con plan de reversión activo**. Una sombra sin autoridad no tiene plan de reversión porque no hay nada que revertir.

Y lo que revela la contradicción es más serio que el nombre: **A3 tiene una fila explícita de «Marcha blanca Etapa 2» en los meses 19-20, y ninguna fila de marcha blanca para la Etapa 1.** A3 sabe cómo se ve una marcha blanca en su tabla; simplemente la Etapa 1 no tiene. Entre la versión instalada (mes 12) y producción (mes 16) solo existe la sombra.

No es un detalle de redacción. El caso cierra ese capítulo diciendo: *«La estrategia de puesta en producción pesa, en la evaluación de este caso, tanto como la arquitectura.»*

### Qué proponemos

Es una **decisión de equipo**, no una corrección de texto. Hay dos salidas y ambas son defendibles:

**Opción A — correr la producción de Etapa 1.** A3 dice que mayo 2028 es lo más **temprano** posible, no lo obligatorio. Se abre una ventana real de marcha blanca en mayo-junio 2028, apenas termina el congelamiento, y producción pasa al mes 18 o 19. Coste: comprime la Etapa 2, que debe estar en producción antes de 2029 por la alianza naviera.

**Opción B — marcha blanca antes del congelamiento.** Se adelanta la versión candidata y la marcha blanca ocurre entre septiembre y el 14 de diciembre de 2027, solapada con el final de la instalación. Coste: menos margen de desarrollo, y hay que declarar el riesgo de solapar instalación con convivencia.

En cualquiera de las dos, **`C3:367` debe dejar de llamar marcha blanca a los meses 13-15**, y A3 debe tener una fila de marcha blanca de Etapa 1 tan explícita como la que ya tiene para la Etapa 2.

---

## Hallazgo 2 · Seis requisitos de tractocamiones que no cita nadie

**Severidad: ALTO.**

### En simple

El caso dice que la brecha de productividad del terminal —24,8 movimientos por hora de grúa frente a los 30 que la alianza naviera exigirá desde 2029— **no es culpa de la grúa**: es el tiempo que la grúa pasa detenida esperando que llegue el tractocamión que se lleva el contenedor.

Célula 2 lo tradujo en seis requisitos, `RF-TRA-01` a `RF-TRA-06`, cuatro de ellos de prioridad **Crítica**: posicionar los tractocamiones, asignarlos a cada movimiento de grúa, estimar su llegada, **registrar cada detención de grúa por espera de equipo**, reasignar ante indisponibilidad y registrar sus movimientos.

**Ninguno de los seis se cita en ningún documento de Célula 3.** Y mientras tanto A1 declara que `CTX-VESSEL` calcula «productividad». Estamos prometiendo el resultado sin decir quién produce el dato que lo hace calculable.

### Lo que dice cada lado

**El caso, línea 213:**
> *«La productividad efectiva promedio es de veinticuatro coma ocho movimientos por hora de grúa. La alianza naviera exige treinta a partir de 2029. **La diferencia entre esos dos números no es solo la grúa: es el tiempo en que la grúa está detenida esperando que llegue el tractocamión.**»*

**El caso, línea 215:**
> *«Los tractocamiones no tienen posicionamiento satelital. El supervisor los asigna por radio y su ubicación exacta en cada momento es conocimiento del supervisor, no del sistema.»*

**Célula 2** — `Celula2/01_Requerimientos/Catalogo rf definitivo parte2.md:250-257`, `RF-TRA-04`, Crítica:
> *«La solución **deberá registrar como evento propio cada detención de grúa de muelle atribuible a espera de tractocamión**, con su inicio, su término y el equipo involucrado.»*
> *«**Resultado esperado:** la primera causa de la brecha de productividad queda cuantificada, no supuesta.»*
> *«**Criterio de aceptación:** para una recalada cerrada, la suma de las detenciones registradas por causa reconcilia con la diferencia entre el tiempo total de atención y el tiempo de operación efectiva, sin residuo no clasificado.»*

**Célula 3 — lo único que existe.** Una mención indirecta, en `Celula3/01_Frente_Logica_Integracion/A2_ARQUITECTURA_DE_INTEGRACION.md:169`:
> *«`PER-EQPOS` | Equipos de patio y tractocamiones (18 grúas de patio, 42 tractocamiones) sin posicionamiento hoy | `CTX-YARD`…»*

**Y la promesa sin el insumo**, en `Celula3/01_Frente_Logica_Integracion/A1_CONTEXTO_Y_ARQUITECTURA_LOGICA.md:470`:
> *«`CTX-VESSEL` | Nave y mensajería | … órdenes STS, movimientos, ventana activa **y productividad**»*

### Por qué es una incoherencia real

El Maestro no exige citar los 139 RF —dice expresamente, en su línea 98, que *«la arquitectura no reproduce las 230 fichas»*—, pero sí exige *«citar los IDs que respalden componentes, controles, interfaces, capacidad y criterios de aceptación»*. `RF-TRA-04` es literalmente un criterio de aceptación medible sobre el indicador que la alianza naviera exigirá en 2029, y no está respaldado por ningún componente nombrado.

La consecuencia práctica: si un evaluador pregunta *«¿cómo van a subir de 24,8 a 30 movimientos por hora?»*, hoy la respuesta está en el catálogo de Célula 2 y no en la arquitectura.

### Qué proponemos

1. **A1** asigna el dominio a un componente y lo cita. La ubicación natural es `CTX-YARD` para posición y asignación de tractocamiones —A2 ya los mapea ahí— y `CTX-OPS` para el evento de detención, que es un hecho operacional. Basta una línea en la responsabilidad de cada uno y las citas `RF-TRA-01..06`.
2. **A1 o A3** declara de dónde sale el evento de `RF-TRA-04`: es un hecho derivado de cruzar el estado de la grúa con la disponibilidad del tractocamión asignado, no un sensor nuevo.
3. **C4** verifica si los 42 tractocamiones instrumentados ya están dentro de los 74 equipos que dimensiona. Según el caso, línea 750, sí lo están (18+42+14 = 74). No debería cambiar el dimensionamiento, pero conviene dejarlo verificado y escrito.

---

## Hallazgo 3 · A3 es el documento de convivencia y cita 3 de 14 requisitos de convivencia

**Severidad: ALTO.**

### En simple

Célula 2 escribió catorce requisitos de convivencia (`RF-CON-01` a `RF-CON-14`): cómo conviven el sistema nuevo y el TOS de 2012, cómo se escriben los datos en los dos, cómo se apaga esa doble escritura y cómo se vuelve atrás.

A3 es *el* documento de la convivencia, y cita tres: `RF-CON-01`, `RF-CON-13` y `RF-CON-14`. Los otros once no aparecen. Y lo llamativo es que A3 **describe los mecanismos** de dos de los que no cita, con sus mismas palabras, pero sin su identificador y —esto es lo que importa— **sin el número medible que los hace verificables**.

### Lo que dice cada lado

**Célula 2** — `Celula2/01_Requerimientos/Catalogo rf definitivo parte1.md:100-110`, `RF-CON-03`, Crítica:
> *«Mientras un dominio esté en convivencia, la solución deberá escribir cada hecho operacional **simultáneamente** en su propio registro y en el sistema de operación de 2012…»*
> *«**Resultado esperado:** ambos registros contienen el mismo hecho **en no más de 60 segundos**; toda diferencia mayor computa como divergencia.»*
> *«**Criterio de aceptación:** sobre una muestra de un turno completo, el **100 %** de los hechos registrados en la solución tiene su correspondiente en el sistema de 2012 dentro de los 60 segundos.»*
> *«Valor provisional. La ventana de desfase definitiva se fija en la puerta de decisión del mes 4, al medirse la latencia real de escritura hacia el sistema de 2012.»*

**Célula 2** — `Celula2/02_Decisiones_Reglas_Supuestos/Registro_supuestos_v3.md:289`, Supuesto T:
> *«La ventana de desfase tolerada entre el registro propio y el sistema de 2012 es de **60 segundos**, valor provisional.»*

**A3, describiendo ese mismo mecanismo sin citarlo** — `Celula3/01_Frente_Logica_Integracion/A3_PROCESOS_CRITICOS_Y_TOS.md:295`:
> *«revertir sin necesidad cuesta poco (**el TOS sigue al día mientras la escritura dual esté activa**)»*

**A3, describiendo `RF-CON-04` sin citarlo** — `:297`:
> *«el apagado es un hito **bajo doble control y aprobación explícita del CLIENTE**, nunca automático»*

### Por qué es una incoherencia real

«El TOS sigue al día» es una afirmación sin unidad de medida. Célula 2 ya le puso una: **60 segundos, con criterio de aceptación del 100 % sobre un turno, y marcada como provisional hasta la puerta del mes 4**. Sin ese número, la reversión de ≤15 minutos que A3 compromete no tiene cómo demostrarse: no se sabe cuánto puede ir atrasado el TOS en el momento de revertir.

Es exactamente el tipo de rotura de cadena que la Matriz Global intenta evitar: `fuente → RF/RNF → componente → control → evidencia`. Si el ID no está, la cadena no se puede recorrer.

### Qué proponemos

1. **A3** cita `RF-CON-03` donde afirma que el TOS sigue al día, e incorpora la ventana de **60 segundos** y su carácter provisional, atada a la puerta del mes 4 que A3 ya tiene en su calendario (`:353`).
2. **A3** cita `RF-CON-04` en el párrafo del apagado bajo doble control.
3. **A3** revisa los once `RF-CON` no citados y, para cada uno, o lo cita donde corresponda o declara por qué queda fuera del alcance de este entregable. No hace falta citarlos todos: hace falta que ninguno quede sin respuesta.

---

## Hallazgo 4 · El TOS está en la sala, pero su conciliación «espera al enlace»

**Severidad: ALTO.**

### En simple

El escenario del corte de 72 horas es este: **se cae el enlace hacia afuera**, hacia la nube, pero el terminal sigue funcionando con todo lo que tiene en su sala técnica.

El TOS de 2012 está físicamente en el terminal. La pieza que traduce entre el sistema nuevo y el TOS —`INT-TOS`— también la pusimos en la sala, y C1 explica muy bien por qué: hacerlo pasar por el enlace sería agregar un punto de falla a la integración más frágil del proyecto.

Pero A1 y C3 dicen que, durante el corte, «la conciliación fina con el TOS se posterga a la reconexión». Si el TOS, `INT-TOS` y el núcleo local están los tres en la misma sala, **esa conciliación no cruza el enlace caído**. No hay razón para postergarla.

O falta nombrar un componente en nube del que sí dependa —y entonces la función crítica 2, «posición e inventario y cruce de zonas», no sobrevive las 72 horas como prometemos—, o estamos declarando como degradado algo que en realidad funciona.

### Lo que dice cada lado

**C1, y es el que está bien** — `Celula3/02_Frente_Fisica_Despliegue/C1_ARQUITECTURA_FISICA_Y_EMPLAZAMIENTO.md:136`:
> *«`PHY-OPS-03` | `INT-TOS` | on-premise, sala | ≤1 s | **debe seguir durante el corte** | … | El TOS 2012 está en el terminal. **Traducir y conciliar a través del enlace agregaría un punto de falla** a una integración que ya es la más frágil del proyecto.»*

**A1** — `Celula3/01_Frente_Logica_Integracion/A1_CONTEXTO_Y_ARQUITECTURA_LOGICA.md:426`, tabla de las cinco funciones críticas, fila 2:
> *«Posición/inventario y cruce de zonas | `CTX-YARD`, `CTX-OPS`, `INT-TOS` | … | **Conciliación fina con el TOS se posterga a la reconexión** (ventana de investigación 48 h)»*

**C3, matriz de continuidad §7** — `Celula3/02_Frente_Fisica_Despliegue/C3_DESPLIEGUE_RED_Y_CONTINUIDAD.md:253`:
> *«Posición e inventario | crítica | … | **ninguno**: la posición sigue con DGPS/RTLS y lectura óptica local. **Lo que se posterga es la conciliación fina con el TOS** *(A3 §7)*.»*

**C3, §7.1** — `:273`, en la columna «lo que sí espera al enlace»:
> *«Posición y cruce de zonas | posición con DGPS/RTLS y lectura óptica | **la conciliación fina con el TOS**»*

### Por qué es una incoherencia real

C1 argumenta explícitamente que conciliar por el enlace sería un error de diseño, y por eso pone `INT-TOS` en la sala. A1 y C3 ponen esa misma conciliación en la lista de lo que espera al enlace. Las dos no pueden ser verdad con la misma topología.

Hay un agravante que conviene mirar: A3 establece que *«un fallo parcial mantiene la autoridad anterior, deja el evento en cola y bloquea una segunda transferencia hasta conciliarlo»*. Si la conciliación queda postergada hasta 72 horas, un solo fallo parcial congelaría los cruces de zona de ese contenedor durante todo el corte.

### Qué proponemos

Decidir cuál de las dos es cierta y alinear las tres:

- **Si la conciliación es local** —que es lo que sostiene C1 y lo que la topología sugiere—: se retira la postergación de `A1:426` y de `C3:253/273`, y se declara que la conciliación con el TOS continúa durante el corte porque ambos sistemas están en la sala. Lo que espera al enlace es otra cosa: el reporte agregado hacia la nube.
- **Si alguna parte necesita nube** —por ejemplo un servicio de reglas o un almacén de referencia—: hay que nombrar ese componente, y entonces C1 debe reflejarlo y D2 debe tratarlo como dependencia del corte.

Dueño: **A1 y C3** hacen el cambio; **C1** ya está correcto y sirve de referencia.

---

## Hallazgo 5 · La unidad del traspaso no es la misma en A3 y en C3

**Severidad: ALTO.**

### En simple

El caso exige que el despliegue se pueda hacer «por proceso o por zona», y da ejemplos: gate, patio, patio refrigerado, muelle, planificación, facturación, portal.

A3 dice que el núcleo de registro —gate, posición, movimientos y salida— es **una sola pieza que se sustituye completa**, y que separarla por función está prohibido, porque dejar la posición en el TOS mientras el gate ya migró crearía **dos fuentes de verdad sobre el mismo contenedor**. Lo que sí se puede es desplegarlo **bloque de patio por bloque de patio**.

C3 toma la lista del caso —donde gate y facturación aparecen como procesos separables— y declara que su estrategia cumple esa condición. Pero para el núcleo no puede cumplirla: gate y posición van juntos o no van.

### Lo que dice cada lado

**A3** — `Celula3/01_Frente_Logica_Integracion/A3_PROCESOS_CRITICOS_Y_TOS.md:239`:
> *«el núcleo de registro es **un solo contexto acotado** (gate+posición+movimientos+salida) que se sustituye completo, pero se despliega por zona del patio, **nunca por función** — dejar la posición en el TOS mientras el gate ya migró generaría dos fuentes de verdad sobre el mismo objeto.»*

**C3** — `Celula3/02_Frente_Fisica_Despliegue/C3_DESPLIEGUE_RED_Y_CONTINUIDAD.md:153`:
> *«El `CP, Cap. 13.3`, condición 4, exige que «el despliegue debe poder hacerse **por proceso o por zona** —gate, patio, patio refrigerado, muelle, planificación, facturación, portal de clientes—…». Azul-verde conmuta todo el tráfico a la vez y no respeta esa partición. **El progresivo por zona sí**.»*

### Por qué es una incoherencia real

C3 usa la lista del caso para dar por cumplida la condición 4, y esa lista incluye separaciones que A3 prohíbe expresamente para el núcleo. No es un matiz de palabras: el caso pide poder desplegar «gate» como unidad, y nuestra arquitectura no puede hacerlo para el registro. Eso hay que **declararlo y justificarlo**, no darlo por cumplido.

Lo bueno es que la justificación de A3 es sólida —evitar dos fuentes de verdad sobre el mismo contenedor es exactamente lo que el caso quiere evitar— y un evaluador la aceptaría. Lo que no se sostiene es afirmar que se cumple la condición tal como está escrita.

### Qué proponemos

1. **C3 §4** declara abiertamente que, para el núcleo de registro, la condición 4 se satisface **por bloque de patio y por etapa**, no por proceso, y cita la razón de A3.
2. Fijar un vocabulario único entre los dos documentos: **«zona de despliegue»** para el artefacto de software y **«zona de autoridad»** para el bloque de patio. Hoy la palabra «zona» significa dos cosas distintas.
3. Nota: C3 ya reconoce esto en su §7.2 —*«se sustituye como un solo contexto acotado pero se despliega bloque por bloque del patio»*—, o sea que el propio documento se contradice entre su §4 y su §7.2. Alinear los dos.

---

## Hallazgo 6 · El Maestro cuenta 80 equipos donde el caso cuenta 74

**Severidad: MEDIO.** Es el más simple de arreglar.

### En simple

El caso lista qué equipos móviles hay que instrumentar. El Maestro reprodujo esa lista y le agregó una categoría de más: las seis grúas de muelle. La suma pasa de 74 a 80. C4 dimensionó con 74, que es lo correcto.

No cambia ningún cálculo hoy, porque C4 usó el número bueno. Pero si alguien toma el Maestro como fuente —que es lo que el Maestro pide que se haga— llegaría a un número distinto.

### Lo que dice cada lado

**El caso, línea 750:**
> *«**Equipos móviles a instrumentar** | 18 grúas de patio, 42 tractocamiones, 14 equipos pesados | hasta 88 equipos»*

18 + 42 + 14 = **74**.

**El Maestro** — `Celula3/00_Gobierno/00_MAESTRO_CONTEXTO_ARQUITECTURA.md:156`:
> *«Equipos | **6 grúas muelle**, 18 patio, 42 tractocamiones, 14 pesados | hasta 88 equipos instrumentables»*

6 + 18 + 42 + 14 = **80**.

**C4, que usa el número correcto** — `Celula3/02_Frente_Fisica_Despliegue/C4_DIMENSIONAMIENTO_Y_T11.md:136`:
> *«Posicionamiento de **74 equipos** móviles cada 2 s | 37,0 | 51 %»*

### Por qué es una incoherencia real

El caso no incluye las grúas de muelle entre los equipos a instrumentar, y tiene sentido: el control de las grúas es un sistema conservado que la restricción 3 y el Capítulo 11 del caso prohíben intervenir. C1 lo refleja bien al declarar el borde de muelle como *«solo lectura, autorización del fabricante»*.

### Qué proponemos

Corregir `Maestro:156` para que la lista sea la del caso —18 patio, 42 tractocamiones, 14 pesados, 74 equipos— y, si se quiere conservar la mención de las 6 grúas de muelle, ponerla en una columna aparte marcada como **lectura de telemetría, no instrumentación**. Dueño: integrador.

---

## Lo que corrijo de una versión anterior de este análisis

Por transparencia, dos afirmaciones que hice antes y que la verificación desmintió:

1. Dije que **«ningún documento declara un RPO del retorno»**. Es falso: Célula 2 lo declara en `RF-CON-03` y en el Supuesto T, en 60 segundos provisionales. El hallazgo correcto es que Célula 3 no lo llevó, y así quedó redactado arriba.
2. Dije que la escritura dual era **«un compromiso sin respaldo»** porque A2 declara la interfaz del TOS «por levantar». Queda matizado: `RF-CON-03` ya trae la nota *«Valor provisional… se fija en la puerta de decisión del mes 4»*, y A3 sí tiene esa puerta en su calendario. La condición existe en los dos extremos; lo único que falta es que A3 la ate explícitamente a la frase «el TOS sigue al día». Va incluido en el hallazgo 3 y no se levanta como hallazgo aparte.

## Cifras de contexto, por si sirven

De los catálogos de Célula 2, Célula 3 cita hoy 44 de 139 RF (32 %), 47 de 91 RNF (52 %) y 10 de 11 reglas de negocio (91 %). **Esto no es un defecto en sí mismo** —el Maestro dice expresamente que la arquitectura no reproduce las fichas—, y la mayoría de los umbrales están cubiertos citando el código `RT` del caso en vez del RNF. Se incluye solo como referencia. Las dos familias que sí merecen mirada son `RF-TRA` (6 definidos, 0 citados; hallazgo 2) y `RF-CON` (14 definidos, 3 citados; hallazgo 3).
