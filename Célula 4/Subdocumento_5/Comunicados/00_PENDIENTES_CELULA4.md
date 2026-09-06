# Qué falta para cerrar el Subdocumento 5

**Caso:** 06 Portuaria — TERABYTE · **Célula 4** (V. Guzmán / M. Reyes)
**Versión:** 2.0 · 6 de septiembre de 2026 · reemplaza la lista v1.0
**Estado del subdocumento:** doce apartados completados de trece; 21 decisiones cerradas; 20 dependencias trazadas

---

## 1. Dónde estamos

| | v1.0 (mañana) | **v2.0 (ahora)** |
|---|---|---|
| Apartados completados | 5 de 13 | **12 de 13** |
| Apartados provisionales por Célula 3 | 4 | **0** |
| Pendientes propios de Célula 4 | 8 | **0** |
| Pendientes por otra célula | 1 apartado | 1 apartado (integración) |
| Decisiones registradas | 0 | **21** |
| Documento LaTeX | esqueleto, 37 páginas | **integrado, 103 páginas, compila sin errores** |

**Los ocho pendientes propios están cerrados.** Modelo conceptual (14 diagramas), diccionario de datos (80 entidades, 451 atributos), matriz de calidad ISO/IEC 25012 (54 reglas), comparación de alternativas de persistencia (13 alternativas), matriz CAP por operación (25 operaciones), estrategia de desempeño (21 índices), capacidad acumulada (2 escenarios) y el reparto de trabajo con revisión cruzada.

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

## 3. Lo que falta y **no** depende de nosotras

Resumen. El detalle, con la pregunta concreta y su fundamento, va en los comunicados por célula.

### 3.1 De **Célula 3** — Subdocumento 4 (arquitectura lógica, física, de integración y de seguridad)

| ID | Materia | Qué apartado nuestro condiciona |
|---|---|---|
| `PEN-01` | Zonas y fases nombradas de la matriz de autoridad del dato | § 5.3, § 5.9 y el nivel 1 de la cascada de resolución de conflictos |
| `PEN-02` | Mecanismo de cifrado de campo y su efecto sobre la indexación de ocho atributos | § 5.10, umbrales de 1 segundo |
| `PEN-03` | Quién publica el modelo conceptual: su sección 4.1.5 o nuestro § 5.14 | § 5.2 y § 5.14 |
| `PEN-06` | Mecanismo de integración: eventos, réplica o captura de cambios | § 5.6, § 5.8 y § 5.10 |
| `PEN-07` | Producto y versión de motor por familia | § 5.4 |
| `PEN-07b` | Emplazamiento: qué almacén en borde, cuál en nube | § 5.4, § 5.5 y § 5.13 |
| `PEN-08` | Revalidación de la volumetría con el factor estacional | § 5.10, § 5.12 y § 5.13 |
| `PEN-10` | Frontera del runtime local y tamaño de buffer del borde | § 5.5 y § 5.13 |
| `PEN-17` | Latencia real de la red de patio y ancho de banda del enlace de reposición | § 5.10 |
| `PEN-18` | Política de captura de imágenes (conjunta con Célula 4) | § 5.10 y § 5.13 |
| `PEN-19` | Esquema de copias que satisface el respaldo 3-2-1-1-0 sobre objetos | § 5.13 |
| **`PEN-05`** | **Contratos de integración por contraparte** — es el que mantiene abierto el § 5.8 | **§ 5.8 completo** |

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
