# D1 — Arquitectura de seguridad

## Contrato del entregable

### Objetivo y destino

Definir Zero Trust, exposición, identidad, cifrado, detección y DevSecOps, y entregar requisitos utilizables por Física desde `v0.1`. Alimenta las secciones 4.1.8 y 4.2.12.

### Cumplimientos asignados

- `SD4-04`, apoyo a `SD4-02`, `SD4-05` y `SD4-08`.
- T7-4.4; BTT Cap. 11/12; Art. 21/22.
- RNF-SEG, RNF-CUM, RNF-OPE, RNF-DIS-14, RF-POR-02/09 y `MC-04`; obligación directa SOC 24x7 de FEP02 Cap. 11 RT-11.17.
- Corte y consecuencias: Maestro §2.3 y matriz global §3; controles y decisiones siguen pendientes.

### Entradas obligatorias

- Maestro §§5–6, 9–12, 16, 18–19.
- RNF vigente, actores/eventuales y sistemas conservados.
- A1/C1 `v0.1` para refinamiento; no son requisito para iniciar.

### Trabajo requerido

- [ ] Definir principios Zero Trust y flujos de confianza.
- [ ] Definir zonas/conductos para nube, on-premise, borde y terceros.
- [ ] Diseñar CDN/WAF/DDoS/TLS/HSTS/certificados/bots.
- [ ] Diseñar SSO, MFA, RBAC/ABAC, SoD y PAM.
- [ ] Resolver eventuales por nombrada y terminal compartida.
- [ ] Definir cifrado, KMS/HSM, rotación y secretos.
- [ ] Definir logs inalterables, SIEM, EDR y alertas portuarias, con SOC 24x7 (ubicación, dotación y procedimientos).
- [ ] Definir respuesta, plazos de vulnerabilidad e incidentes.
- [ ] Definir SAST/SCA/DAST, imágenes, SBOM, firma/SLSA y datos no productivos.
- [ ] Mapear control→capa→tipo de componente→evidencia.
- [ ] Preparar componentes/licencias/servicios candidatos a T-11.

### Entrega temprana `SEC-PHYS-v0.1`

| ID control | Capacidad requerida | Componente/servicio candidato | Ubicación/restricción | HA/continuidad | Evidencia | Entrada para T-11 |
|---|---|---|---|---|---|---|
| `SEC-EDGE-01` | WAF + DDoS + TLS 1.3 | servicio gestionado | borde público nube | multi-AZ | configuración/prueba | sí |
| `SEC-IAM-01` | SSO/MFA/RBAC/ABAC | IAM | nube/híbrido; acceso local crítico definido | según criticidad | matriz/prueba | sí |
| `SEC-LOG-01` | log inalterable/SIEM | plataforma de seguridad | nube + colectores locales | buffer 72 h | caso de uso | sí |
| `SEC-END-01` | EDR/cifrado/gestión | licencias endpoint | on-prem/puestos | continuidad local | consola/evidencia | sí |
| `SEC-KEY-01` | llaves/secretos | KMS/HSM/vault | híbrido según operación | rotación/recuperación | prueba | sí |

### Matriz de controles obligatoria

| Control | Fuente | Actor/dato | Capa | Comp. lógico | Nodo físico | Amenaza | Implementación | Evidencia | Responsable operativo | Estado |
|---|---|---|---|---|---|---|---|---|---|---|
| POR COMPLETAR | — | — | — | — | — | — | — | — | — | PENDIENTE |

### Productos obligatorios

1. Vista lógica de seguridad y fronteras de confianza.
2. `SEC-PHYS-v0.1` entregado en Puerta 1.
3. Matriz de controles completa.
4. Matriz de identidad/roles/sesiones.
5. Candidatos de T-11 y `ADR-008/009/010`.

### Decisiones permitidas y escalamiento

Puede definir patrones y controles mínimos. Debe escalar identidad federada no confirmada, restricciones de autoridad/VMS, productos sin compatibilidad demostrada y controles que impidan operar 72 h.

### Salidas hacia otros frentes

- Frente 1: políticas de exposición, identidad y datos por interfaz.
- Frente 2: zonas, controles físicos, productos/licencias y requisitos de continuidad.

### Definición de terminado

- [ ] Seguridad aparece en todas las capas, no solo perímetro.
- [ ] Actores internos, externos, eventuales y privilegiados están resueltos.
- [ ] Cada dato sensible tiene protección en tránsito/reposo y manejo de llaves.
- [ ] Logging/detección cubren nube, on-premise y borde sin puntos ciegos.
- [ ] Controles tienen evidencia y componente físico cuando corresponde.
- [ ] No se rompe operación desconectada.
- [ ] `TRZ_D1.md` completo.

## Contenido listo para integrar

> Incorporar aquí la versión aprobada.

## Trazabilidad

Ver [`trazabilidad/TRZ_D1.md`](trazabilidad/TRZ_D1.md).

