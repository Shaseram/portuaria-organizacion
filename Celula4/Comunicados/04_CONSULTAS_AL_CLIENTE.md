# Consultas de Célula 4 al CLIENTE y a terceros

**Asunto:** materias del Subdocumento 5 que no se resuelven internamente
**Emite:** Célula 4 — Modelo y gestión de datos
**Vía:** período de consultas del proceso, a través de quien coordine la propuesta
**Fecha:** 6 de septiembre de 2026

---

## Regla que aplicamos

Ninguna de estas seis materias se completó por criterio propio. Cada una tiene declarado el tratamiento provisional que adoptamos mientras no haya respuesta, de modo que el Informe 1 puede entregarse sin ellas. Lo que no se hizo fue rellenarlas con una cifra plausible: `CP, Cap. 17.1` sanciona presentar supuestos como hechos confirmados por el CLIENTE, y `CP, Cap. 14.2` sanciona los valores sin derivación.

---

## 1. `PEN-12` · Esquema, calidad y tamaño reales de la base del sistema de operación de 2012

**Consulta.** ¿Puede el CLIENTE entregar el tamaño real de la base de datos del sistema de 2012, y facilitar el acceso para un perfilado temprano de su esquema y de la calidad de sus datos?

**Por qué.** `CP, Cap. 5` declara que el CLIENTE no dispone de documentación actualizada de sus personalizaciones ni de su modelo de datos. Catorce años de operación y cuatro proveedores sucesivos hacen previsible que existan esquemas heredados, códigos de contenedor no normalizados y maestros duplicados.

**Tratamiento provisional.** El volumen se usa como **orden de magnitud declarado** (≈480 GB, estimado por Célula 2 con la tasa de transacciones de hoy como aproximación de catorce años, lo que probablemente lo sobreestima). El perfilado se adelanta al trabajo de descubrimiento de los meses 1 a 4, en vez de dejarlo para la Etapa 2, y así un fallo de extracción no se descubre cuando ya no queda margen.

---

## 2. `PEN-13` · Fecha exacta de fin de soporte del sistema de 2012

**Consulta.** ¿Cuál es la fecha comprometida por el fabricante para el fin de soporte?

**Por qué.** Condiciona el calendario de la coexistencia y, con él, la ventana en que dos sistemas registran los mismos hechos.

**Tratamiento provisional.** Escenario conservador con holgura declarada, alineado con lo que Célula 3 ya adoptó.

---

## 3. `PEN-14` · Existencia de interfaz por cada autoridad

**Consulta.** ¿Aduana, el servicio agrícola y la autoridad sanitaria disponen de interfaz de intercambio electrónico, y bajo qué condiciones?

**Por qué.** `CP, Cap. 15, RT-05.23` exige identificar cada estándar por su denominación y acreditar la factibilidad de su adopción. No se puede acreditar lo que no se ha verificado.

**Tratamiento provisional.** Canal asistido trazable como alternativa declarada, con acta firmada por el inspector presente y carga posterior con marca de origen. **Ninguna interfaz se presume existente.**

---

## 4. `PEN-16` · Alcance del plazo de 90 minutos de sincronización

**Consulta.** `CP, Cap. 15, RT-03.13` exige que la sincronización tras 72 horas de desconexión no supere 90 minutos, «sin pérdida de ningún movimiento ni de ningún hecho facturable». ¿Ese plazo protege **la integridad de los movimientos y los hechos facturables**, o exige que **todo el volumen generado en 72 horas** haya cruzado el enlace en esos 90 minutos?

**Por qué importa.** El volumen de 72 horas son 13 GB hoy y 39 GB en el escenario de crecimiento exigible, y **el 86 % son imágenes de reconocimiento**, que no bloquean ninguna invariante: la autoridad, los movimientos, las posiciones y los hechos facturables se restablecen mucho antes. Bajo la primera lectura, la reconciliación que importa cabe holgadamente en el plazo. Bajo la segunda, el enlace de reposición debe sostener ≈58 Mbps útiles.

**Tratamiento provisional.** Adoptamos la **primera lectura**, declarada expresamente como **interpretación de Terabyte y no como hecho del caso**. La alternativa conservadora está dimensionada: si el CLIENTE prefiere la segunda, cambia el costo del enlace, no el diseño.

---

## 5. `PEN-15` · Validación de la metodología de emisiones

**Consulta.** ¿Acepta el CLIENTE, y aceptaría un verificador externo, que el consumo energético de los equipos de patio se atribuya a los contenedores **por movimientos ejecutados**?

**Por qué.** El resultado de negocio N.º 16 exige que las emisiones se midan con metodología declarada y **verificable por un tercero**. El criterio de reparto cambia la cifra de emisión que se informa por contenedor, así que conviene acordarlo antes de comprometerla.

**Tratamiento provisional.** Metodología declarada y cerrada (`DEC-C4-01`), con su fundamento: es el único criterio con dato duro del CLIENTE detrás —los movimientos de patio y de muelle son volumetría entregada— y el único que un verificador puede comprobar contra cifras que el terminal ya reporta al concedente. Los dos criterios alternativos se descartaron con argumento: *tiempo de ciclo* se apoyaría en una frecuencia de posicionamiento no validada, y *masa movida* dejaría sin método al flujo de importación, porque la verificación de masa bruta solo es exigible en exportación.

---

## 6. `PEN-20` · Volumen de evidencia documental distinta de las imágenes

**Consulta.** ¿Puede el CLIENTE aportar el volumen actual de actas de inspección, documentos de transporte y evidencia firmada, o una referencia para estimarlo?

**Por qué.** Las dieciocho dimensiones de volumetría del `CP, Cap. 14.2` no incluyen esta categoría —el capítulo no la pide— pero `RT-05.10` obliga a retener esa evidencia seis años, de modo que sí hay que dimensionarla.

**Tratamiento provisional.** Estimación propia con método declarado: ≈223 GB al año, compuesta por actas de inspección, documentos de transporte, evidencia de los cuatro actos con firma electrónica y mensajería de integración. **La incertidumbre de esta cifra no cambia ninguna decisión**: aun en su cota alta representa el 16 % del volumen de imágenes.

---

## Una consulta adicional sobre política de retención

Además de las seis anteriores, la **frontera entre almacenamiento en línea y archivo recuperable** (`DEC-C4-21`) requiere aprobación del CLIENTE cuando apruebe la política de retención. La propuesta aplica el criterio que el propio caso ya usó dos veces —«2 años en línea» para telemetría y «12 + 24 meses» para eventos de seguridad— y la ventana de tres años que el caso trata como operacionalmente relevante al obligar a migrar solo tres años de movimientos.

La única consecuencia visible para el CLIENTE: una objeción de facturación sobre un hecho de más de dos años exigirá restauración desde archivo, con un plazo declarado de 24 horas.
