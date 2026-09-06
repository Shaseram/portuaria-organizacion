# Registro global de decisiones de arquitectura

**Uso:** índice de ADR aprobados y candidatos de los tres frentes. Las decisiones heredadas de Célula 2 se citan; no se reabren sin evidencia nueva o contradicción con una fuente superior.

## 1. Estados

`CANDIDATO` · `EN ANÁLISIS` · `PROPUESTO` · `APROBADO` · `SUPERADO` · `BLOQUEADO EXTERNO`

## 2. Índice vigente tras MA-4

| ADR | Decisión | Autor primario | Insumos | Estado | Destino |
|---|---|---|---|---|---|
| `ADR-001` | estilo: núcleo modular vs. servicios distribuidos | A1 | volumen, 72 h, TI=5 | PROPUESTO | lógica/físico |
| `ADR-002` | frontera del runtime local y sincronización | A3/C1 | funciones críticas y apoyos parciales del inventario canónico `EDGE-RUN`; A3 §7/§10; emplazamiento de `CTX-VESSEL` y gateway local conciliado en MA-3; capacidad/prueba pendientes | PROPUESTO | lógico/físico |
| `ADR-003` | mecanismo de integración/eventos | A2 | 21+7, desconexión; A2 §7 | PROPUESTO | integración |
| `ADR-004` | convivencia/autoridad del TOS | A3 | Decisión 1, RF-CON-13/14; A3 §10 | PROPUESTO | procesos |
| `ADR-005` | sala principal: rehabilitar 34 m² si supera puertas normativas; reemplazo compacto obligatorio si alguna falla | C1/C2 | Decisión 20, Art. 16; `RT-06.01..34`; baseline C4; condicionado a accesos, espacio separado, rutas físicas y plano | PROPUESTO | físico/T-11 |
| `ADR-006` | LTE/5G privada como baseline de red del patio; esquema mixto si el site survey invalida cobertura/handover/independencia | C3 | Decisión 9/19; 18 ha; autonomía 8 h; rango inicial 6–8; `F2-ESC-001` | PROPUESTO | despliegue/T-11 |
| `ADR-007` | 3 nodos, almacenamiento local RAID 10, DR activo-pasivo y respaldo 3-2-1-1-0 | C2/C3/C4 | RNF-DIS-13/14/15; RNF-DES-09..12; 4×480 GB; RTO 4 h/RPO 15 min; pruebas pendientes | PROPUESTO | físico/T-11 |
| `ADR-008` | identidad y acceso Zero Trust; gobierno común con capacidad local crítica | D1 | eventuales/PAM; RF-POR-02/09; operación 72 h; `SRV-IAM` crítico con autenticación/autorización local de identidades vigentes; producto, directorio/federación y revocación aislada condicionados a F3-ESC-001/002 | PROPUESTO | seguridad |
| `ADR-009` | llaves, secretos y cifrado: gobierno común con capacidades criptográficas separadas por ámbito y servicio local protegido | D1 | nube/on-prem/edge; alternativas y consecuencias en D1 B4.8 | PROPUESTO | seguridad/T-11 |
| `ADR-010` | detección híbrida federada, evidencia inmutable y SOC gestionado 24x7 | D1/D2 | autonomía 72 h, retenciones/incidentes y FEP02 RT-11.14..21; alternativas en D1 B5.8 | PROPUESTO | seguridad/T-11 |
| `ADR-011` | AWS; primaria São Paulo `sa-east-1` multi-AZ y secundaria Norte de Virginia `us-east-1` | C2; decisión transversal | `RT-03.01`, `RT-15.04/05`, catálogo regional vigente, residencia, carbono y reversibilidad; `F2-ESC-009`; `THR-073`/`SPOF-22` | PROPUESTO | físico/seguridad/T-11 |

**Corte MA-5:** los 11 ADR quedan `PROPUESTO` como baseline de Informe 1 y hay **0 ADR `APROBADO`**. `ADR-011` fue promovido al seleccionar AWS y declarar ubicaciones concretas: producción en `sa-east-1`, distribuida en al menos dos zonas de disponibilidad, y DR activo-pasivo en `us-east-1`. La región AWS anunciada para Chile se revisará solo cuando esté disponible y supere las puertas de catálogo, multi-AZ, latencia, residencia y carbono; no es dependencia de esta oferta. El estado propuesto permite completar T-11 sin confundir selección de arquitectura con contratación, prueba o aceptación del CLIENTE.

## 3. Plantilla obligatoria de ADR

```md
# ADR-XXX — Título

- Fecha:
- Estado:
- Propietario:
- Fuentes y requisitos:

## Contexto y fuerza de decisión
## Alternativas evaluadas
## Criterios ponderados
## Decisión
## Consecuencias positivas
## Consecuencias negativas y riesgos residuales
## Impacto lógico, físico, seguridad, capacidad y T-11
## Validación y evidencia
## Condición de revisión/sustitución
```

## 4. Regla de aprobación

Un ADR no se aprueba si no presenta al menos dos alternativas reales, criterios vinculados al caso, consecuencias negativas, trazabilidad y efecto en las demás vistas. Nombrar un producto sin comparar el problema que resuelve no es una decisión arquitectónica suficiente.
