# Referencias en Norma APA 7.ª edición — Célula 3

**Fecha:** 2026-09-06

**Fuente contractual:** Bases Administrativas `FEP01.26`, **Art. 40.4**: *"Referencias | Norma APA 7.ª edición para toda cita y referencia bibliográfica"*. La exigencia alcanza a toda la propuesta, no solo a los subdocumentos que piden una lista propia.

**Alcance:** este archivo reúne la ficha bibliográfica de **cada estándar, marco y cuerpo normativo que la Célula 3 invoca**. No agrega estándares nuevos ni cambia una sola decisión de arquitectura: solo le pone nombre, año y edición verificable a lo que la célula ya declaró.

**Relación con la matriz del Artículo 4:** este archivo es el **complemento bibliográfico de [`11_MATRIZ_ARTICULO4_MA6.md`](11_MATRIZ_ARTICULO4_MA6.md)**. Esa matriz responde *qué exige cada estándar y cómo lo satisface la solución*; este archivo responde *de qué documento exacto estamos hablando*. Se leen juntos: la matriz manda en el contenido, este archivo manda en la cita. Cada `STD-A4-*` y cada `NORM-A4-*` de la matriz tiene su entrada aquí, y la sección 3 es la tabla de anclaje entre ambos.

---

## 1. Para qué sirve este archivo (en simple)

El Artículo 4.3 de las BA dice que **mencionar un estándar sin evidenciar cómo se satisface obtiene cero**. La matriz MA-6 ya resolvió ese punto. Pero hay una segunda exigencia, distinta y más silenciosa: el Artículo 40.4 obliga a que **toda cita y referencia bibliográfica** esté en APA 7. Hasta ahora la Célula 3 nombraba estándares en texto corrido — "ISO 22301", "WCAG 2.2 AA", "NIST SP 800-207" — sin una lista de referencias que dijera qué edición es, de qué año y quién la publica.

Eso es una brecha formal, y también una brecha de fondo: **"ISO 27017" no es un documento; "ISO/IEC 27017:2026" sí lo es.** Un evaluador que quiera comprobar una afirmación necesita el segundo, no el primero.

Este archivo cierra esa brecha. Su uso previsto es:

1. **Al redactar**, citar en el cuerpo con autor-año: *(International Organization for Standardization, 2019)* o, cuando el estándar es el sujeto de la frase, *ISO 22301:2019*.
2. **Al ensamblar el Informe 1**, el integrador toma esta lista, la funde con la de la Célula 4 (ver sección 2) y produce la lista de referencias única del entregable.

## 2. Regla de no duplicación con la Célula 4

La Célula 4 ya mantiene su propia lista APA en [`../../Célula 4/Subdoc13/B12_REFERENCIAS_APA.md`](../../Célula%204/Subdoc13/B12_REFERENCIAS_APA.md) (responsable: Matías Reyes, estado `APROBADO`), exigida por el Art. 29° de las BA y el `RT-26.03` de las BTT.

**Tres referencias son compartidas entre ambas células** y **no se repiten aquí**, para que el integrador no termine con dos entradas del mismo documento con formato distinto:

| Documento | Dónde vive la ficha | Quién lo usa |
|---|---|---|
| ISO 14083:2023 | `B12` de Célula 4 | `STD-A4-37` (huella de carbono, `CTX-EMIS`) |
| ISO 14064-3:2019 | `B12` de Célula 4 | `STD-A4-37` (verificación independiente) |
| GLEC Framework (Smart Freight Centre, 2023) | `B12` de Célula 4 | `STD-A4-37` (método adoptado) |

ISO 16290:2013 (niveles TRL) también vive en `B12` y la Célula 3 la cita 27 veces; se toma de allí sin duplicar.

**Formato:** este archivo replica exactamente la convención de `B12` — autor institucional completo, año entre paréntesis, título en cursiva, designación del estándar entre paréntesis al final, DOI o URL solo cuando el documento es de acceso público. No se inventó ningún año ni ninguna edición: cada uno se verificó contra la ficha del organismo emisor.

---

## 3. Tabla de anclaje: matriz MA-6 → referencia bibliográfica

Cada fila de `11_MATRIZ_ARTICULO4_MA6.md` queda anclada a la cita autor-año con la que debe aparecer en el texto. La columna **Cita en texto** es literalmente lo que se escribe entre paréntesis al citar.

### 3.1 Estándares y marcos (`STD-A4-*`)

| STD-ID | Documento citable | Cita en texto |
|---|---|---|
| `STD-A4-01` | ISO/IEC 27001:2022 | (ISO & IEC, 2022a) |
| `STD-A4-02` | ISO/IEC 27002:2022 | (ISO & IEC, 2022b) |
| `STD-A4-03` | ISO/IEC 27017:2026 | (ISO & IEC, 2026a) |
| `STD-A4-04` | ISO/IEC 27018:2025 | (ISO & IEC, 2025b) |
| `STD-A4-05` | NIST CSWP 29 — CSF 2.0 | (NIST, 2024) |
| `STD-A4-06` | NIST SP 800-207 | (Rose et al., 2020) |
| `STD-A4-07` | OWASP ASVS 4.0.3 | (OWASP Foundation, 2021) |
| `STD-A4-08` | OWASP Top 10:2025 | (OWASP Foundation, 2025) |
| `STD-A4-09` | OWASP API Security Top 10 — 2023 | (OWASP Foundation, 2023) |
| `STD-A4-10` | OWASP SAMM 2.0 | (OWASP Foundation, 2020) |
| `STD-A4-11` | CIS Benchmarks | (Center for Internet Security, s.f.) |
| `STD-A4-12` | SLSA v1.2 | (The Linux Foundation, 2025) |
| `STD-A4-13` | ECMA-424 (CycloneDX) e ISO/IEC 5962:2021 (SPDX) | (Ecma International, 2024; ISO & IEC, 2021) |
| `STD-A4-14` | sin documento propio; se apoya en `STD-A4-12` y `STD-A4-13` | (The Linux Foundation, 2025) |
| `STD-A4-15` | ISO 22301:2019 | (ISO, 2019) |
| `STD-A4-16` | ISO/IEC 27031:2025 | (ISO & IEC, 2025a) |
| `STD-A4-17` | ISO/IEC 20000-1:2018 | (ISO & IEC, 2018) |
| `STD-A4-18` | ITIL Foundation: ITIL 4 Edition | (AXELOS, 2019) |
| `STD-A4-19` | Site Reliability Engineering (Google) | (Beyer et al., 2016) |
| `STD-A4-20` | ISO/IEC 25010:2023 | (ISO & IEC, 2023b) |
| `STD-A4-21` | ISO/IEC 25012:2008 | (ISO & IEC, 2008) |
| `STD-A4-22` | ISO/IEC/IEEE 29119-1:2022 | (ISO, IEC & IEEE, 2022a) |
| `STD-A4-23` | ISO/IEC/IEEE 42010:2022 | (ISO, IEC & IEEE, 2022b) |
| `STD-A4-24` | The TOGAF Standard, 10.ª ed. | (The Open Group, 2022) |
| `STD-A4-25` | PMBOK Guide, 7.ª ed. | (Project Management Institute, 2021) |
| `STD-A4-26` | Agile Practice Guide | (Project Management Institute & Agile Alliance, 2017) |
| `STD-A4-27` | WCAG 2.2 | (W3C, 2023) |
| `STD-A4-28` | EN 301 549 V3.2.1 | (ETSI, 2021) |
| `STD-A4-29` | OpenAPI Specification 3.1.1 | (OpenAPI Initiative, s.f.) |
| `STD-A4-30` | AsyncAPI Specification 2.6.0 | (AsyncAPI Initiative, 2023) |
| `STD-A4-31` | SMDG Recommendation 06 y directorios UN/EDIFACT | (SMDG, 2020; UNECE, s.f.) |
| `STD-A4-32` | ISO 6346:2022 | (ISO, 2022) |
| `STD-A4-33` | NIST AI 100-1 — AI RMF 1.0 | (NIST, 2023) |
| `STD-A4-34` | ISO/IEC 42001:2023 | (ISO & IEC, 2023a) |
| `STD-A4-35` | ISO 14001:2026 | (ISO, 2026) |
| `STD-A4-36` | ISO/IEC 30134-2:2026 | (ISO & IEC, 2026b) |
| `STD-A4-37` | ISO 14083:2023, ISO 14064-3:2019 y GLEC | fichas en `B12` de Célula 4 |
| `STD-A4-38` | IEC 62443-3-3:2013 | (IEC, 2013) |

### 3.2 Normativa aplicable (`NORM-A4-*`)

| NORM-ID | Documento citable | Cita en texto |
|---|---|---|
| `NORM-A4-01` | Ley N.º 21.719 y Ley N.º 19.628 | (Ley N.º 21.719, 2024; Ley N.º 19.628, 1999) |
| `NORM-A4-02` | Ley N.º 21.663, Ley Marco de Ciberseguridad | (Ley N.º 21.663, 2024) |
| `NORM-A4-03` | Ley N.º 21.459 sobre delitos informáticos | (Ley N.º 21.459, 2022) |
| `NORM-A4-04` | Ley N.º 19.799 sobre firma electrónica | (Ley N.º 19.799, 2002) |
| `NORM-A4-05` | Ley N.º 20.393 y Ley N.º 21.595 | (Ley N.º 20.393, 2009; Ley N.º 21.595, 2023) |
| `NORM-A4-06` | Ley N.º 20.422 sobre inclusión y discapacidad | (Ley N.º 20.422, 2010) |
| `NORM-A4-07` | régimen de zona primaria aduanera | fuente sectorial del CLIENTE; sin referencia bibliográfica propia |
| `NORM-A4-08` | normativa ambiental aplicable | se apoya en `STD-A4-35` y `STD-A4-37` |
| `NORM-A4-09` | Código PBIP/ISPS y SOLAS Cap. XI-2 | (IMO, 1974, 2003) |
| `NORM-A4-10` | SOLAS, Regla VI/2 — VGM | (IMO, 1974) |
| `NORM-A4-11` | Código IMDG, edición 2024 (Enmienda 42-24) | (IMO, 2024) |
| `NORM-A4-12` | normativa fitosanitaria y sanitaria | fuente sectorial del CLIENTE; sin referencia bibliográfica propia |
| `NORM-A4-13` | cadena de frío y programas de exportación | fuente sectorial del CLIENTE; sin referencia bibliográfica propia |
| `NORM-A4-14` | autoridad marítima y concesión portuaria | fuente sectorial del CLIENTE; sin referencia bibliográfica propia |
| `NORM-A4-15` | normativa laboral portuaria y de seguridad y salud | fuente sectorial del CLIENTE; sin referencia bibliográfica propia |

> **Sobre las filas sin referencia bibliográfica.** Cinco `NORM-A4-*` no apuntan a un documento publicado y citable, sino a un régimen administrativo o a instrumentos del propio CLIENTE (resoluciones aduaneras, protocolos fitosanitarios, el contrato de concesión, la normativa laboral y los convenios del terminal). Declararlos "sin referencia bibliográfica propia" **no los deja sin tratamiento**: la matriz MA-6 les asigna control, componente y evidencia futura, y esa evidencia futura es precisamente el documento que el CLIENTE debe aportar durante el levantamiento. Inventar una cita aquí sería peor que no ponerla.

---

## 4. Lista de referencias — estándares, marcos y obras

Orden alfabético por autor, según APA 7. Los sufijos `a`, `b`, `c` distinguen obras del mismo autor y año, tal como exige la norma cuando la cita en texto sería ambigua.

AsyncAPI Initiative. (2023). *AsyncAPI specification 2.6.0*. https://www.asyncapi.com/docs/reference/specification/v2.6.0

AXELOS. (2019). *ITIL foundation: ITIL 4 edition*. TSO.

Beyer, B., Jones, C., Petoff, J., & Murphy, N. R. (Eds.). (2016). *Site reliability engineering: How Google runs production systems*. O'Reilly Media.

Center for Internet Security. (s.f.). *CIS Benchmarks*. Recuperado el 6 de septiembre de 2026, de https://www.cisecurity.org/cis-benchmarks

Ecma International. (2024). *CycloneDX bill of materials specification* (ECMA-424). https://ecma-international.org/publications-and-standards/standards/ecma-424/

European Telecommunications Standards Institute. (2021). *Accessibility requirements for ICT products and services* (EN 301 549 V3.2.1).

Institute of Electrical and Electronics Engineers. (2024). *IEEE standard for information technology — Telecommunications and information exchange between systems — Local and metropolitan area networks — Specific requirements — Part 11: Wireless LAN medium access control (MAC) and physical layer (PHY) specifications* (IEEE Std 802.11-2024).

International Electrotechnical Commission. (2013). *Industrial communication networks — Network and system security — Part 3-3: System security requirements and security levels* (IEC 62443-3-3:2013).

International Maritime Organization. (1974). *International Convention for the Safety of Life at Sea (SOLAS), 1974, as amended*.

International Maritime Organization. (2003). *International Ship and Port Facility Security (ISPS) Code, 2003 edition*.

International Maritime Organization. (2024). *International Maritime Dangerous Goods (IMDG) Code, 2024 edition (incorporating Amendment 42-24)*.

International Organization for Standardization. (2019). *Security and resilience — Business continuity management systems — Requirements* (ISO 22301:2019).

International Organization for Standardization. (2022). *Freight containers — Coding, identification and marking* (ISO 6346:2022).

International Organization for Standardization. (2026). *Environmental management systems — Requirements with guidance for use* (ISO 14001:2026).

International Organization for Standardization & International Electrotechnical Commission. (2008). *Software engineering — Software product Quality Requirements and Evaluation (SQuaRE) — Data quality model* (ISO/IEC 25012:2008).

International Organization for Standardization & International Electrotechnical Commission. (2018). *Information technology — Service management — Part 1: Service management system requirements* (ISO/IEC 20000-1:2018).

International Organization for Standardization & International Electrotechnical Commission. (2021). *Information technology — SPDX specification V2.2.1* (ISO/IEC 5962:2021).

International Organization for Standardization & International Electrotechnical Commission. (2022a). *Information security, cybersecurity and privacy protection — Information security management systems — Requirements* (ISO/IEC 27001:2022).

International Organization for Standardization & International Electrotechnical Commission. (2022b). *Information security, cybersecurity and privacy protection — Information security controls* (ISO/IEC 27002:2022).

International Organization for Standardization & International Electrotechnical Commission. (2023a). *Information technology — Artificial intelligence — Management system* (ISO/IEC 42001:2023).

International Organization for Standardization & International Electrotechnical Commission. (2023b). *Systems and software engineering — Systems and software Quality Requirements and Evaluation (SQuaRE) — Product quality model* (ISO/IEC 25010:2023).

International Organization for Standardization & International Electrotechnical Commission. (2025a). *Cybersecurity — Information and communication technology readiness for business continuity* (ISO/IEC 27031:2025).

International Organization for Standardization & International Electrotechnical Commission. (2025b). *Information security, cybersecurity and privacy protection — Guidelines for protection of personally identifiable information (PII) in public clouds acting as PII processors* (ISO/IEC 27018:2025).

International Organization for Standardization & International Electrotechnical Commission. (2026a). *Information security, cybersecurity and privacy protection — Information security controls based on ISO/IEC 27002 for cloud services* (ISO/IEC 27017:2026).

International Organization for Standardization & International Electrotechnical Commission. (2026b). *Information technology — Data centres key performance indicators — Part 2: Power usage effectiveness (PUE)* (ISO/IEC 30134-2:2026).

International Organization for Standardization, International Electrotechnical Commission, & Institute of Electrical and Electronics Engineers. (2022a). *Software and systems engineering — Software testing — Part 1: General concepts* (ISO/IEC/IEEE 29119-1:2022).

International Organization for Standardization, International Electrotechnical Commission, & Institute of Electrical and Electronics Engineers. (2022b). *Software, systems and enterprise — Architecture description* (ISO/IEC/IEEE 42010:2022).

National Institute of Standards and Technology. (2023). *Artificial intelligence risk management framework (AI RMF 1.0)* (NIST AI 100-1). U.S. Department of Commerce. https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.100-1.pdf

National Institute of Standards and Technology. (2024). *The NIST Cybersecurity Framework (CSF) 2.0* (NIST CSWP 29). U.S. Department of Commerce. https://nvlpubs.nist.gov/nistpubs/CSWP/NIST.CSWP.29.pdf

OpenAPI Initiative. (s.f.). *OpenAPI specification* (Versión 3.1.1). Recuperado el 6 de septiembre de 2026, de https://spec.openapis.org/oas/v3.1.1.html

OWASP Foundation. (2020). *OWASP software assurance maturity model (SAMM) version 2.0*. https://owaspsamm.org/model/

OWASP Foundation. (2021). *OWASP application security verification standard 4.0.3*. https://owasp.org/www-project-application-security-verification-standard/

OWASP Foundation. (2023). *OWASP API security top 10 — 2023*. https://owasp.org/API-Security/editions/2023/en/0x00-header/

OWASP Foundation. (2025). *OWASP top 10:2025*. https://owasp.org/Top10/2025/

Project Management Institute. (2021). *A guide to the project management body of knowledge (PMBOK guide)* (7.ª ed.).

Project Management Institute & Agile Alliance. (2017). *Agile practice guide*.

Rose, S., Borchert, O., Mitchell, S., & Connelly, S. (2020). *Zero trust architecture* (NIST Special Publication 800-207). National Institute of Standards and Technology. https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-207.pdf

SMDG. (2020). *Recommendation 06: SMDG recommended messages between terminal and carrier* (Versión 1.0). https://smdg.org/documents/recommendations/

The Linux Foundation. (2025). *SLSA: Supply-chain levels for software artifacts* (Versión 1.2). https://slsa.dev/spec/v1.2/

The Open Group. (2022). *The TOGAF standard* (10.ª ed.).

United Nations Economic Commission for Europe. (s.f.). *United Nations Trade Data Interchange Directory (UNTDID) — UN/EDIFACT*. Recuperado el 6 de septiembre de 2026, de https://unece.org/trade/uncefact

World Wide Web Consortium. (2023). *Web Content Accessibility Guidelines (WCAG) 2.2* (W3C Recommendation, 5 de octubre de 2023). https://www.w3.org/TR/WCAG22/

---

## 5. Lista de referencias — legislación y normativa chilena

APA 7 admite una lista separada para material legal, porque el formato no es autor-año sino norma-fecha de publicación. Se ordena por número de ley ascendente. La fecha es la de publicación en el Diario Oficial de la República de Chile.

Ley N.º 19.628 de 1999. Sobre protección de la vida privada. 28 de agosto de 1999. Diario Oficial de la República de Chile.

Ley N.º 19.799 de 2002. Sobre documentos electrónicos, firma electrónica y servicios de certificación de dicha firma. 12 de abril de 2002. Diario Oficial de la República de Chile.

Ley N.º 20.393 de 2009. Establece la responsabilidad penal de las personas jurídicas en los delitos que indica. 2 de diciembre de 2009. Diario Oficial de la República de Chile.

Ley N.º 20.422 de 2010. Establece normas sobre igualdad de oportunidades e inclusión social de personas con discapacidad. 10 de febrero de 2010. Diario Oficial de la República de Chile.

Ley N.º 21.459 de 2022. Establece normas sobre delitos informáticos, deroga la ley N.º 19.223 y modifica otros cuerpos legales con el objeto de adecuarlos al Convenio de Budapest. 20 de junio de 2022. Diario Oficial de la República de Chile.

Ley N.º 21.595 de 2023. Sobre delitos económicos y atentados contra el medio ambiente. 17 de agosto de 2023. Diario Oficial de la República de Chile.

Ley N.º 21.663 de 2024. Ley marco de ciberseguridad. 8 de abril de 2024. Diario Oficial de la República de Chile.

Ley N.º 21.719 de 2024. Que regula la protección y el tratamiento de los datos personales y crea la Agencia de Protección de Datos Personales. 13 de diciembre de 2024. Diario Oficial de la República de Chile.

---

## 6. Lista de referencias — fuentes de práctica de ingeniería

Estas cuatro entradas no son estándares del Artículo 4. Existen porque la Célula 3 sostiene afirmaciones técnicas que **no se derivan de las bases ni del caso**, y el Art. 1.3 exige que la solución represente *"el estado del arte de la industria"*. Sin una fuente, esas afirmaciones son opinión del oferente; con ella, son práctica documentada.

| Afirmación de la Célula 3 | Fuente que la respalda |
|---|---|
| el dimensionamiento de radio del patio exige site survey **con patio cargado**, porque los contenedores apilados alteran la propagación | (IEEE, 2024) — capa física y comportamiento del medio |
| el perfil de escritura del núcleo local condiciona la elección de RAID y su penalización de escritura | (Patterson et al., 1988) — trabajo fundacional que define los niveles y su costo |
| operar Kubernetes agrega carga operacional propia, no solo capacidad de cómputo, y por eso pesa en un equipo con TI = 5 | (Burns et al., 2016) — lecciones de una década de gestión de contenedores |
| la brecha de productividad de patio y el comportamiento de grúas y tractocamiones son un problema estudiado, no una intuición | (Steenken et al., 2004) — clasificación y revisión de literatura de operación de terminales |

Burns, B., Grant, B., Oppenheimer, D., Brewer, E., & Wilkes, J. (2016). Borg, Omega, and Kubernetes. *ACM Queue, 14*(1), 70–93.

Institute of Electrical and Electronics Engineers. (2024). *IEEE standard for information technology — … Part 11: Wireless LAN medium access control (MAC) and physical layer (PHY) specifications* (IEEE Std 802.11-2024). [Ficha completa en la sección 4.]

Patterson, D. A., Gibson, G., & Katz, R. H. (1988). A case for redundant arrays of inexpensive disks (RAID). *Proceedings of the 1988 ACM SIGMOD International Conference on Management of Data*, 109–116. https://doi.org/10.1145/50202.50214

Steenken, D., Voß, S., & Stahlbock, R. (2004). Container terminal operation and operations research — A classification and literature review. *OR Spectrum, 26*(1), 3–49. https://doi.org/10.1007/s00291-003-0157-z

> Para afirmaciones sobre patio, citas de camión y emisiones, la Célula 4 ya tiene fichas de Carlo et al. (2014), Ramírez-Nafarrate et al. (2017), Giuliano y O'Brien (2007) y Hakimi et al. (2024) en `B12`. No se duplican aquí: si un frente de Célula 3 necesita una de ellas, la cita desde `B12`.

---

## 7. Observaciones de vigencia detectadas al verificar las ediciones

Al fijar la edición de cada estándar apareció algo que no se veía cuando los nombrábamos sin año: **varios documentos que la Célula 3 invoca tienen una edición más reciente que la que se asume habitualmente.** Esto no rompe nada del baseline —ninguna decisión de arquitectura depende de una cláusula concreta de una edición vieja— pero sí importa para el Art. 4.3, porque citar una edición retirada debilita la evidencia.

Se dejan como **observaciones para el equipo**, no como cambios ejecutados. Ninguna se aplicó sobre la matriz ni sobre los frentes.

| Estándar | Edición vigente | Qué conviene revisar |
|---|---|---|
| ISO/IEC 25010 | **2023** (2.ª ed., nov-2023) retira la de 2011 | el modelo pasó a **nueve características** y el título quedó acotado al modelo de calidad de producto. Si los RNF de Célula 2 se escribieron contra las ocho características de 2011, conviene confirmar que la redacción sigue calzando |
| ISO/IEC 27031 | **2025** (2.ª ed., may-2025) retira la de 2011 | cambió incluso el encabezado: de *"Information technology — Security techniques"* a *"Cybersecurity"*. `C3 §§7–10` lo cita como marco de continuidad TIC; el encuadre se mantiene |
| ISO/IEC 27017 | **2026** (2.ª ed., jul-2026) retira la de 2015 | es reciente. Vale confirmar que `SEC-CLOUD-01` no dependa de una numeración de control de la edición 2015 |
| ISO/IEC 27018 | **2025** (3.ª ed., ago-2025) retira la de 2019 | pasó de *"code of practice"* a *"guidelines"* |
| ISO 14001 | **2026** (4.ª ed., abr-2026) retira la de 2015 | `STD-A4-35` la usa como referencia ambiental, no como certificación; el uso se mantiene |
| ISO/IEC 30134-2 | **2026** (2.ª ed., ene-2026) retira la de 2016 y su enmienda de 2018 | es la definición formal de PUE que respalda el objetivo ≤1,60 de `STD-A4-36` |
| ISO/IEC/IEEE 42010 | **2022** retira la de 2011 | `STD-A4-23` y las cinco vistas se apoyan en el vocabulario de 2022, que es el que usamos |
| EN 301 549 | **V3.2.1 (2021)** es la versión armonizada de referencia; ETSI publicó **V4.1.1 en septiembre de 2026** | se cita V3.2.1 a propósito. La V4.1.1 es de este mes y aún no está consolidada como referencia armonizada |
| OWASP ASVS | la matriz fija **4.0 nivel 2**; OWASP publicó **5.0.0 en 2025** | es una decisión del equipo, no un error: 4.0 L2 sigue siendo verificable. Solo conviene que la oferta diga *4.0.3* y no *"ASVS"* a secas |
| OWASP Top 10 | la versión publicada vigente es **2025** | la matriz lo cita genérico; al redactar conviene nombrar la edición |
| SLSA | la especificación vigente es **v1.2 (nov-2025)**, que agregó el *Source track* | "nivel 3" ya no es inequívoco: conviene escribir **Build L3** |
| AsyncAPI | la matriz fija **2.6 o superior**, que es el piso del Art. 4.3 de las BA y de `RT-05.16`; la AsyncAPI Initiative publicó la **3.0.0 en diciembre de 2023** | se cita la **2.6.0** porque es la versión que la matriz declara. Si un frente adopta una versión superior, debe nombrarla explícitamente: «superior» no es citable |
| ISO 22301 e ISO/IEC 20000-1 | ambas tienen **Enmienda 1:2024** sobre acción climática | no altera los requisitos que usamos; se menciona por completitud |

## 8. Pendientes

1. **Fusión final de listas.** El integrador del Informe 1 debe fundir esta lista con la de `B12` (Célula 4) en una sola lista alfabética antes de la entrega. Las tres referencias compartidas de la sección 2 quedan una sola vez.
2. **Decidir la edición de ASVS y de OWASP Top 10** que la oferta declara, y escribirla completa en el texto.
3. **Escribir "Build L3"** donde hoy dice "SLSA nivel 3", en `STD-A4-12` y en `T11-C3-04`.
4. **Revisar el calce de los RNF de Célula 2 con ISO/IEC 25010:2023.** Es la única observación de la sección 7 que podría tocar contenido y no solo una cita.

> Ninguno de estos cuatro pendientes bloquea el Informe 1. Los tres primeros son de redacción; el cuarto es una comprobación que corresponde coordinar con Célula 2.
