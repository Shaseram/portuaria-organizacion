# Complemento de auditoría — cierre del catálogo tecnológico del Subdocumento 4

**Fecha:** 2026-09-06  
**Estado:** entrada para el contraste de auditorías y el cierre previo a diagramación.  
**Relación:** complementa la auditoría global; no reemplaza ni duplica sus correcciones.

## 1. Propósito

El Subdocumento 4 exige describir las **tecnologías de software a utilizar** y los **implementos de hardware y software a proveer**. Célula 3 ya define la mayor parte de las capacidades de plataforma, pero todavía debe cerrar el stack principal de construcción de la solución y distinguir entre:

1. componente lógico;
2. tecnología que lo materializa;
3. producto, licencia o servicio efectivamente ofertado;
4. elemento que corresponde registrar en T-11.

Este cierre debe ejecutarse después de corregir las inconsistencias del contraste final de auditorías y antes de producir los diagramas definitivos, B8, D3 y el Subdocumento 4.

## 2. Estado actual

| Ámbito | Definición disponible | Estado de cierre |
|---|---|---|
| Ejecución | contenedores; plataforma gestionada en nube y runtime local liviano | patrón definido; producto por decidir |
| Datos transaccionales | PostgreSQL gestionado y capacidad local | candidato definido |
| Series temporales | extensión sobre PostgreSQL o motor dedicado | alternativa por seleccionar |
| Objetos/documentos | almacenamiento de objetos con ciclo de vida e inmutabilidad | capacidad definida; proveedor por decidir |
| Integración | `INT-HUB`, broker persistente, colas durables y DLQ; servicio gestionado o Kafka/RabbitMQ | arquitectura definida; producto por decidir |
| Observabilidad | OpenTelemetry con recolector y buffer local | estándar definido; plataforma por decidir |
| Infraestructura como código | Terraform u OpenTofu | alternativa por seleccionar |
| Sistema operativo | Linux empresarial endurecido y con soporte vigente | familia definida; distribución por decidir |
| Seguridad | IAM/MFA/PAM, KMS/HSM, secretos, SIEM, EDR, SOC y respaldo | capacidades definidas; productos/licencias pendientes |
| CI/CD y cadena de suministro | SAST, SCA, DAST, SBOM, firma, procedencia y registro de artefactos | controles definidos; herramientas pendientes |
| Nube | operación primaria/secundaria y DR | AWS; `sa-east-1` primaria multi-AZ y `us-east-1` secundaria, `ADR-011 PROPUESTO` |
| Aplicaciones | canales y componentes lógicos definidos en A1–A3 | **stack de frontend, backend/API y aplicación de terreno pendiente** |

## 3. Decisiones mínimas que faltan

No es necesario seleccionar cada biblioteca. Sí deben quedar definidos y justificados estos elementos principales:

| Decisión | Contenido mínimo | Efecto directo |
|---|---|---|
| Canal web/frontend | tecnología o framework, compatibilidad, despliegue y política LTS | 4.2.3 y diagrama de despliegue |
| Backend y APIs | lenguaje, framework/runtime, estilo de API, autenticación y ejecución nube/local | 4.1.3, 4.2.2 y nodos de cómputo |
| Aplicación móvil/terminal | PWA, multiplataforma o nativa; operación offline, sincronización, gestión y compatibilidad con equipo robusto | 4.2.3, 4.2.4 y continuidad de 8 h |
| Contenedores/orquestación | Kubernetes gestionado o alternativa más simple; límite del runtime local | 4.2.1, 4.2.3, capacidad y operación con TI=5 |
| Persistencia y mensajería | selección entre candidatos ya documentados y reglas de portabilidad | 4.2.3, `ADR-003` y T-11 cuando corresponda |
| Plataforma de ingeniería | repositorio, CI/CD, registro de artefactos, IaC y herramientas DevSecOps | 4.2.3, 4.2.7 y licencias/servicios |
| Seguridad y observabilidad | productos o servicios compatibles con operación híbrida y aislamiento de 72 h | 4.1.4, 4.2.2, 4.2.3, 4.2.6 y T-11 |
| Ciclo de vida | versión de referencia, soporte vigente, actualización, reversibilidad y fin de soporte | catálogo, ADR y condiciones de operación |

La selección debe preferir la alternativa más simple que cumpla continuidad, seguridad, portabilidad y operación por un equipo TI de cinco personas. Solo se abre o amplía un ADR cuando la elección tenga alternativas reales y consecuencias arquitectónicas relevantes.

## 4. Regla de publicación y T-11

- **4.1 Arquitectura lógica:** muestra capas, responsabilidades, contratos e interfaces usando IDs canónicos; evita marcas.
- **4.2.3 Tecnologías de software:** declara tecnología, producto de referencia o servicio, alternativa, modalidad gestionada/autogestionada, ubicación y vigencia.
- **4.2.4 Implementos:** especifica lo que debe suministrarse, sus interfaces, redundancia, seguridad y condiciones ambientales.
- **T-11:** recibe solo hardware, plataforma, licencia o servicio efectivamente ofertado, con ubicación, cantidad y justificación.
- Un framework open source incluido en el desarrollo no genera por sí solo una fila T-11. Sí la genera el soporte, licencia, plataforma gestionada o servicio separado que se oferte.
- Mientras falte una decisión externa, se conserva el requisito vinculante, las alternativas y el criterio de selección; no se inventa una marca ni una cantidad.

## 5. Trazabilidad mínima de cierre

Cada tecnología publicada debe permitir seguir esta cadena:

`fuente/requisito → componente A1/A2 → tecnología C2 → nodo C1 → capacidad C4 → control D1/D2 → T-11 si aplica → diagrama → evidencia prevista`

El catálogo tecnológico final debe contener, como mínimo:

| Campo | Regla |
|---|---|
| Componente lógico | ID canónico existente |
| Función | responsabilidad concreta |
| Tecnología seleccionada | no dejar vacía en el stack principal |
| Producto o referencia | con “o equivalente” cuando corresponda |
| Alternativa evaluada | breve y real |
| Ubicación | nube, sala técnica, edge o servicio |
| Modalidad | gestionada o autogestionada |
| Vigencia | versión de referencia y política de soporte |
| ADR/requisito | enlace o identificador estable |
| T-11 | ID o `NO APLICA JUSTIFICADO` |

## 6. Criterio para comenzar los diagramas

Se puede diagramar cuando:

- las correcciones críticas y altas del contraste final tengan tratamiento acordado;
- frontend, backend/API y aplicación de terreno tengan una línea tecnológica seleccionada;
- `ADR-008` y `ADR-011` estén decididos o formalmente condicionados sin contradicciones;
- cada plataforma principal tenga ubicación y modalidad coherentes con las 72 h de aislamiento;
- no exista doble conteo entre observabilidad, SIEM, CI/CD y otros servicios en T-11;
- las dependencias realmente externas estén identificadas como tales.

Cumplidas estas condiciones, los diagramas podrán construirse desde un único catálogo y no será necesario corregir nombres, cajas y emplazamientos durante la redacción del Subdocumento 4.
