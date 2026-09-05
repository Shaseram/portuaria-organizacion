# Registro global de decisiones de arquitectura

**Uso:** índice de ADR aprobados y candidatos de los tres frentes. Las decisiones heredadas de Célula 2 se citan; no se reabren sin evidencia nueva o contradicción con una fuente superior.

## 1. Estados

`CANDIDATO` · `EN ANÁLISIS` · `PROPUESTO` · `APROBADO` · `SUPERADO` · `BLOQUEADO EXTERNO`

## 2. Índice inicial

| ADR | Decisión | Autor primario | Insumos | Estado | Destino |
|---|---|---|---|---|---|
| `ADR-001` | estilo: núcleo modular vs. servicios distribuidos | A1 | volumen, 72 h, TI=5 | PROPUESTO | lógica/físico |
| `ADR-002` | frontera del runtime local y sincronización | A3/C1 | cinco funciones críticas | CANDIDATO | lógico/físico |
| `ADR-003` | mecanismo de integración/eventos | A2 | 21+7, desconexión | CANDIDATO | integración |
| `ADR-004` | convivencia/autoridad del TOS | A3 | Decisión 1, RF-CON-13/14 | CANDIDATO | procesos |
| `ADR-005` | sala actual vs. nueva vs. edge mínimo+nube | C1/C2 | Decisión 20, Art. 16 | CANDIDATO | físico/T-11 |
| `ADR-006` | red de patio y conectividad redundante | C3 | Decisión 9/19, site survey | CANDIDATO | despliegue/T-11 |
| `ADR-007` | almacenamiento/RAID/HA/DR | C2/C3/C4 | RPO/RTO/capacidad | CANDIDATO | físico/T-11 |
| `ADR-008` | identidad y acceso Zero Trust | D1 | eventuales/externos/PAM | CANDIDATO | seguridad |
| `ADR-009` | llaves, secretos y cifrado | D1 | nube/on-prem/edge | CANDIDATO | seguridad/T-11 |
| `ADR-010` | observabilidad/SIEM y evidencia inmutable | D1/D2 | retenciones/incidentes | CANDIDATO | seguridad/T-11 |

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

