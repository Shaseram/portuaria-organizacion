# Registro global de decisiones de arquitectura

**Uso:** índice de ADR aprobados y candidatos de los tres frentes. Las decisiones heredadas de Célula 2 se citan; no se reabren sin evidencia nueva o contradicción con una fuente superior.

## 1. Estados

`CANDIDATO` · `EN ANÁLISIS` · `PROPUESTO` · `APROBADO` · `SUPERADO` · `BLOQUEADO EXTERNO`

## 2. Índice inicial

| ADR | Decisión | Autor primario | Insumos | Estado | Destino |
|---|---|---|---|---|---|
| `ADR-001` | estilo: núcleo modular vs. servicios distribuidos | A1 | volumen, 72 h, TI=5 | PROPUESTO | lógica/físico |
| `ADR-002` | frontera del runtime local y sincronización | A3/C1 | cinco funciones críticas; A3 §7/§10; conciliación pendiente de la observación A1↔C1 sobre `CTX-VESSEL` | PROPUESTO | lógico/físico |
| `ADR-003` | mecanismo de integración/eventos | A2 | 21+7, desconexión; A2 §7 | PROPUESTO | integración |
| `ADR-004` | convivencia/autoridad del TOS | A3 | Decisión 1, RF-CON-13/14; A3 §10 | PROPUESTO | procesos |
| `ADR-005` | habilitar sala actual vs. reemplazarla; variante dimensional de sala nueva con núcleo local acotado+nube | C1/C2 | Decisión 20, Art. 16; rutas físicas por validar | CANDIDATO | físico/T-11 |
| `ADR-006` | red de patio y conectividad redundante | C3 | Decisión 9/19, site survey | CANDIDATO | despliegue/T-11 |
| `ADR-007` | almacenamiento/RAID/HA/DR | C2/C3/C4 | RNF-DIS-13/14/15; RNF-DES-09..12; volumetría estacional | CANDIDATO | físico/T-11 |
| `ADR-008` | identidad y acceso Zero Trust; gobierno común con capacidad local delegada como línea base condicionada | D1 | eventuales/PAM; RF-POR-02/09; operación 72 h; aprobación condicionada a F3-ESC-001/002 | PROPUESTO | seguridad |
| `ADR-009` | llaves, secretos y cifrado: gobierno común con capacidades criptográficas separadas por ámbito y servicio local protegido | D1 | nube/on-prem/edge; alternativas y consecuencias en D1 B4.8 | PROPUESTO | seguridad/T-11 |
| `ADR-010` | detección híbrida federada, evidencia inmutable y SOC gestionado 24x7 | D1/D2 | autonomía 72 h, retenciones/incidentes y FEP02 RT-11.14..21; alternativas en D1 B5.8 | PROPUESTO | seguridad/T-11 |
| `ADR-011` | proveedor y regiones primaria/secundaria de nube | C2; decisión transversal | `RT-03.01`, `RT-15.04/05`, latencia, residencia, intensidad de carbono y reversibilidad; `F2-ESC-009`; `THR-073`/`SPOF-22` | CANDIDATO | físico/seguridad/T-11 |

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
