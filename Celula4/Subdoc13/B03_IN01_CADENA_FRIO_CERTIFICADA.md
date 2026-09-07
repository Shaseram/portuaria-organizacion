# B03 · IN-01 · Innovación de producto o servicio

> **Caso:** 06 Portuaria — TERABYTE · **Célula 4** · **Subdocumento 13 — Innovaciones**
> **Responsable:** Matías Reyes · **Corte:** 2026-09-06 · **Estado:** APROBADO — texto de entrega
> **Origen:** Numeral correspondiente del Subdocumento 13. Cubre los cinco ejes del Formulario T-22: idea, tecnología, alcance, forma de implementación y resultado esperado, más la declaración de investigación adicional.

---

#### 13.2 Innovación de producto o servicio — Cadena de frío certificada Aconcagua

**Idea.** Hoy, cuando una toma refrigerada falla, el terminal se avisa a sí mismo. El exportador cuya fruta está en esa toma no se entera. Y cuando la carga llega a destino, el terminal no puede entregar el registro continuo de temperatura que los mercados exigen como evidencia de cadena de frío: hoy ese registro sencillamente no existe. La innovación convierte la instrumentación que el proyecto instalará de todos modos en **un servicio con dos caras nuevas**: el aviso llega al dueño de la carga en el momento en que ocurre la desviación, y la serie de temperatura se entrega como un certificado sellado que un tercero puede verificar por su cuenta, sin pedirle nada al terminal.

**Tecnología que la sustenta.** Tres piezas, ninguna experimental. La cadena de eventos de temperatura por contenedor se **sella mediante registro encadenado por hash**, se firma electrónicamente y recibe **sello de tiempo conforme a RFC 3161**, de modo que la fecha y la integridad son demostrables sin acceso a los sistemas del terminal. La pertenencia de un registro individual a la serie sellada se demuestra mediante **estructura de árbol de Merkle**, siguiendo el patrón de registro auditable de RFC 6962, sin exponer el resto de la serie. El aviso externo viaja por los adaptadores de canal por audiencia que la solución ya contempla, con confirmación de recepción registrada. La firma reutiliza el servicio transversal de firma electrónica que la solución ya construye para los cuatro actos obligatorios: **no se agrega ninguna plataforma criptográfica nueva.**

**Alcance.** Cubre los contenedores refrigerados conectados a tomas instrumentadas. Se despliega en dos fases: primero el aviso proactivo por canal directo, y después el certificado descargable con usuario autenticado, porque el registro y la verificación de identidad de clientes externos pertenecen a la Etapa 2 del alcance definido en el Subdocumento 3. **No cubre** la carga seca, ni la temperatura durante el transporte marítimo, ni sustituye el registro del propio equipo refrigerado del contenedor.

**Forma de implementación.** Se apoya íntegramente en componentes que el alcance obligatorio ya construye: el contexto de reefer y telemetría genera el evento; el servicio de evidencia y firma lo sella; el servicio de notificaciones lo emite por el adaptador que corresponda a cada audiencia; el portal y la puerta de enlace de servicios entregan el certificado y exponen el punto público de verificación. Al abrir una nueva superficie de exposición externa, requiere modelado de amenazas propio conforme al `RT-26.07` de las Bases Técnicas Transversales, que se desarrolla en el Subdocumento 4.

**Resultado esperado.** Que una desviación de temperatura llegue a alguien que tenga interés propio en que se resuelva, en cualquiera de los tres turnos —que es exactamente lo que faltó la madrugada del 18 de febrero de 2026, cuando la pérdida fue de US$ 620.000 en 38 contenedores durante nueve horas—, y que el terminal pueda ofrecer evidencia de cadena de frío como atributo de su servicio, en una operación donde entre enero y marzo se concentra el 62 % del volumen refrigerado del año. El Caso registra la consecuencia comercial de no tenerla en cuatro palabras: tras la pérdida del 18 de febrero, **«el exportador no volvió»**.

**Investigación adicional declarada.** Requiere levantar con al menos un exportador y una autoridad qué formato de certificado es efectivamente aceptado en los mercados de destino de la fruta chilena; sin esa validación, el certificado puede ser técnicamente correcto y comercialmente inútil. La meta del indicador se fijará una vez conocido ese formato.

