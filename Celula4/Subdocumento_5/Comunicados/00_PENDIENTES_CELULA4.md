# Qué falta para cerrar el Subdocumento 5

**Caso:** 06 Portuaria — TERABYTE · **Célula 4** (V. Guzmán / M. Reyes)
**Versión:** 2.0 · 6 de septiembre de 2026 · reemplaza la lista v1.0
**Estado del subdocumento:** trece apartados cubiertos para diseño I1; 21 decisiones C4 registradas; contratos y pruebas externos condicionados

---

## 1. Dónde estamos

| | v1.0 (mañana) | **v2.0 (ahora)** |
|---|---|---|
| Apartados completados | 5 de 13 | **13 de 13 para diseño I1** |
| Apartados provisionales por Célula 3 | 4 | **0** |
| Pendientes propios de Célula 4 | 8 | **0** |
| Pendientes por otra célula | 1 apartado | **0 apartados; condiciones puntuales trazadas** |
| Decisiones registradas | 0 | **21** |
| Documento LaTeX | esqueleto, 37 páginas | **integrado, 103 páginas, compila sin errores** |

**Los ocho pendientes propios están cerrados para diseño I1.** Modelo conceptual, diccionario, calidad, persistencia, CAP, desempeño, capacidad con cuatro escenarios diferenciados y reparto de trabajo están documentados. Esto no significa contratos, pruebas o aceptación ejecutados.

---

## 2. Lo único que sigue abierto por nuestra parte

| # | Qué falta | Dónde va | Por qué no está cerrado | Prioridad |
|---:|---|---|---|---|
| 1 | **Revisión cruzada final** entre las dos personas de la célula, con acta breve de lo revisado | acuerdo interno | Es procedimiento, no contenido. La regla de la guía es que quien escribe dominio y gobierno no valide persistencia y desempeño | `INDISPENSABLE` |
| 2 | **Compilar en Overleaf** con pdfLaTeX y verificar que las fuentes IBM Plex y el babel español cargan | proyecto LaTeX | Aquí compila con fuentes de respaldo y rótulos en inglés; en Overleaf debe verse correcto | `INDISPENSABLE` |
| 3 | **Subir el control de versiones a 1.0** | `secciones/general/00-control-versiones.tex` | Depende de que 1 y 2 estén hechos | `INDISPENSABLE` |
| 4 | **Integrar con los demás subdocumentos del Informe 1**: descomentar los `\input` de las secciones 1 a 4 y 13 en `main.tex` | `main.tex` | Depende de que las otras células entreguen sus archivos | `INDISPENSABLE` |
| 5 | **Decidir si el Subdocumento 5 se presenta** en la presentación preparatoria 1 | acuerdo de equipo | El Formulario T-22 lo incluye entre los subdocumentos del Informe 1 pero no le dedica viñeta propia en la agenda | `DESEABLE` |
| 6 | **Plan de migración de datos** y **modelo de datos con diccionario** como entregables independientes del Sobre N.º 2 | Sobre N.º 2 | No se exigen en el Informe 1 | `INFORME 2` |
| 7 | **Documentación de interfaces** en OpenAPI 3.1 y AsyncAPI 2.6 de los flujos de datos | Sobre N.º 2 | Depende de los contratos de integración, que son de Célula 3 | `INFORME 2` |

---

## 3. Estado de las dependencias que **no** resuelve Célula 4

Resumen. El detalle, con la pregunta concreta y su fundamento, va en los comunicados por célula.

### 3.1 De **Célula 3** — Subdocumento 4 (arquitectura lógica, física, de integración y de seguridad)

| ID | Estado del cruce | Condición que permanece |
|---|---|---|
| `PEN-01` | `RECIBIDO` | segmentación física exacta de bloques queda parametrizada |
| `PEN-02` | `RECIBIDO` | pruebas de fuga, latencia, rotación y continuidad de los ocho campos |
| `PEN-03` | `CERRADO I1` | alto nivel en SD4; detalle/diccionario en SD5 |
| `PEN-06` | `RECIBIDO` | CDC real del TOS sigue `CONDICIONADO EXTERNO` |
| `PEN-07/07b` | `RECIBIDO` | versión final de productos y pruebas al congelar oferta |
| `PEN-08/10` | `CERRADO I1` | 21,9 GB peak, 32,5 Mbps y WAN ≥35 Mbps; prueba futura |
| `PEN-17` | `CONDICIONADO EXTERNO` | site survey y medición E2E de patio/WAN |
| `PEN-18` | `CONDICIONADO EXTERNO` | política exacta de imagen y alcance del binario en 90 min |
| `PEN-19` | `CONDICIONADO EXTERNO` | matriz exacta de copias y aceptación del CLIENTE |
| `PEN-05` | `RECIBIDO` para diseño | contratos reales siguen `POR LEVANTAR`/`BLOQUEADO EXTERNO` por contraparte |

### 3.2 De **Célula 2** — Subdocumento 3 (esquema de solución, catálogos de requerimientos)

| ID | Materia | Qué condiciona |
|---|---|---|
| `PEN-04` | De qué evento se deriva el movimiento de grúa de muelle | § 5.7 y el alcance del cálculo de emisiones |
| `PEN-05b` | Si crean el requerimiento no funcional de calidad de datos para el T-12 | Trazabilidad, no contenido |
| `PEN-09` | Valores de banda y duración de la desviación de temperatura | § 5.7 |
| `PEN-10b` | Vigencia de `RF-PAT-07` | § 5.2 |
| `PEN-11` | Si el catálogo de campos cifrados pasa a su registro | Trazabilidad de `RNF-SEG-05` |

### 3.3 Del **CLIENTE** y de terceros

| ID | Materia |
|---|---|
| `PEN-12` | Esquema, calidad y tamaño reales de la base del sistema de 2012 |
| `PEN-13` | Fecha exacta de fin de soporte del sistema de 2012 |
| `PEN-14` | Existencia de interfaz por cada autoridad |
| `PEN-15` | Validación de la metodología de emisiones por el verificador externo |
| `PEN-16` | Alcance del plazo de 90 minutos de sincronización |
| `PEN-20` | Volumen real de evidencia documental distinta de las imágenes |

---

## 4. Lo que ya entregamos a otras células

Las tres entregas cruzadas hacia Célula 3 están **cerradas**:

| ID | Qué entregamos | Dónde está |
|---|---|---|
| `E-01` | Capacidad acumulada por familia y horizonte, en dos escenarios, con el reparto borde/nube | A-08 y Anexo de capacidad |
| `E-02` | Necesidad de persistencia por familia, con consistencia y disponibilidad exigidas | A-05 y Anexo de persistencia |
| `E-03` | Atributos que son clave de acceso indexada y cuáles chocan con el cifrado de campo | A-07 y Anexo de desempeño |
| `E-04` | Requisitos de buffer local y de reconciliación para las 72 horas | A-06 |
| `E-05` | Filas del Formulario T-12 correspondientes a los códigos `RT` de datos | pendiente de armar con Célula 2 |
| `E-06` | Criterios de aceptación verificables de calidad, retención y recuperación | A-03, doce pruebas |

---

## 5. Criterio que gobierna esta lista

El Subdocumento 5 pondera **11 % del Informe 1**. Un apartado marcado honestamente como pendiente, con su dependencia trazada y su consulta formulada, se evalúa mejor que un apartado rellenado con contenido inventado. Lo que no se alcance a cerrar queda declarado, no maquillado.
