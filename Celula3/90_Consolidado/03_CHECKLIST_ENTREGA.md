# Checklist final — Subdocumento 4

## 1. Cobertura contractual

| Control | Evidencia | Estado |
|---|---|---|
| 4.1 a) Esquema de solución | contexto aprobado | PENDIENTE |
| 4.1 b) Arquitectura lógica | ocho capas + catálogo | PENDIENTE |
| 4.2 a) Arquitectura física | híbrido + nodos/zonas | PENDIENTE |
| 4.2 b) Tecnologías software | catálogo/vigencia | PENDIENTE |
| 4.2 c) Implementos HW/SW | especificaciones/cantidad | PENDIENTE |
| 4.2 d) Data center primario | decisión/especificación | PENDIENTE |
| 4.2 e) Data center secundario | DR/especificación | PENDIENTE |
| T-11 | cinco columnas, completo | PENDIENTE |
| SD4-01..08 | matriz global | PENDIENTE |

## 2. Arquitectura lógica e integración

- [ ] Ocho capas obligatorias visibles.
- [ ] Actores y sistemas externos fuera del límite.
- [ ] Módulos, bounded contexts y responsabilidades explícitos.
- [ ] UI no accede a datos directamente.
- [ ] Modelo conceptual y eventos portuarios.
- [ ] 21 contrapartes + 7 familias técnicas.
- [ ] Contratos, mensajes, versiones y gobierno.
- [ ] Idempotencia, timeout, retry, DLQ, breaker, bulkhead y fallback.
- [ ] TOS bidireccional, autoridad dominio×zona×fase y retorno.
- [ ] App offline, portal seguro, cabina y notificaciones compartidas.

## 3. Arquitectura física y despliegue

- [ ] Híbrida, región primaria/secundaria y multi-AZ.
- [ ] Emplazamiento Art. 16 por componente.
- [ ] Sala/edge/nube/DR y sistemas conservados visibles.
- [ ] Sala decidida por ADR y sin eliminar 72 h.
- [ ] Ambiente marino especificado por clase/ubicación.
- [ ] Redes operacional, administrativa y protección segregadas.
- [ ] Site survey con patio cargado y prueba real de failover.
- [ ] Cinco ambientes aislados; PREPROD equivalente.
- [ ] HA, RTO≤4 h, RPO≤15 min, DR semestral.
- [ ] Respaldo 3-2-1-1-0 y restauración mensual.
- [ ] Operación local 72 h y sincronización ≤90 min.
- [ ] Funciones no disponibles y procedimiento manual declarados.
- [ ] Retorno de toda intervención y congelamiento respetado.

## 4. Seguridad

- [ ] Zero Trust transversal y STRIDE por componente/integración.
- [ ] CDN/WAF/DDoS/TLS 1.3/HSTS/certificados/bots.
- [ ] SSO/MFA/RBAC/ABAC/SoD/PAM.
- [ ] Eventuales y terminal compartida resueltos.
- [ ] Cifrado en tránsito/reposo, KMS/HSM y secretos.
- [ ] Logs inalterables, SIEM y EDR híbridos.
- [ ] Plazos de incidentes y vulnerabilidades.
- [ ] SAST/SCA/DAST, SBOM, firma/SLSA y anonimización.
- [ ] SPOF residuales declarados y justificados.

## 5. Capacidad y T-11

- [ ] Valores normal, peak, concurrencia y crecimiento.
- [ ] Dos naves + gate y telemetría local/central.
- [ ] Almacenamiento/retenciones, 72 h y red.
- [ ] Fórmulas, unidades, supuestos y sensibilidad reproducibles.
- [ ] Holgura, ampliación y primer cuello de botella.
- [ ] Cada cantidad vuelve a un cálculo.
- [ ] Cada caja física ofertada tiene fila T-11 o inclusión justificada.
- [ ] Cada fila T-11 aparece en físico.
- [ ] T-11 conserva cinco columnas oficiales.
- [ ] No hay precios ni montos económicos.

## 6. Caso específico, trazabilidad y forma

- [ ] Se ven terminal, gate, patio, reefer, muelle, TOS, ERP, VMS, autoridades, ferrocarril y concedente.
- [ ] Programa 2029 tratado como indivisible.
- [ ] Retención/migración coherentes con Célula 2.
- [ ] Pendientes externos están etiquetados y tienen fallback.
- [ ] Decisiones, supuestos y hechos no están mezclados.
- [ ] Cada cifra tiene fuente o etiqueta de supuesto.
- [ ] Cada ADR tiene alternativas y consecuencias.
- [ ] Diagramas tienen leyenda, dirección de lectura y nombres consistentes.
- [ ] No hay diagramas genéricos ni productos en la vista lógica.
- [ ] Matriz global y auditorías locales completas.

## 7. Veredicto

| Resultado | Valor |
|---|---|
| Controles cumplidos | POR CONTAR |
| Controles parciales | POR CONTAR |
| No cumple | POR CONTAR |
| Bloqueos externos tratados | POR CONTAR |
| Veredicto final | PENDIENTE |

No emitir `APROBADO` si existe un `NO CUMPLE`, una contradicción silenciosa, un componente físico sin justificación, una fila T-11 sin respaldo o un precio en la oferta técnica.

