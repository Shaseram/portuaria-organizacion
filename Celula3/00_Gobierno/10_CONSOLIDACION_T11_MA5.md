# Consolidación del catálogo y Formulario T-11 — MA-5

**Fecha:** 2026-09-06

**Estado histórico del bloque:** `MA-5 COMPLETADA — P3 SUPERADA`; el estado operativo vigente está en `Celula3/README.md`.
**Entradas:** C1–C4, D1 `SEC-PHYS`, D2, A1–A3, Art. 16, Art. 84 y Formulario T-11.

## 1. Resultado

MA-5 convirtió los candidatos dispersos en dos fuentes canónicas:

- `90_Consolidado/01_T11_TRABAJO_TRAZABLE.md`: matriz interna de 12 columnas, con ID, nodo, fuente, cantidad, control y estado.
- `90_Consolidado/02_FORMULARIO_T11_FINAL.md`: tabla contractual con exactamente las cinco columnas oficiales.

El resultado contiene **32 filas ofertadas/especificadas**, cero precios, cero `POR COMPLETAR` y cantidades expresadas como cálculo, suscripción/servicio o rango con mecanismo de cierre.

## 2. Decisión cloud incorporada

El usuario seleccionó AWS como proveedor. La baseline de Informe 1 queda:

| Función | Selección | Regla |
|---|---|---|
| primaria | AWS São Paulo `sa-east-1` | producción en al menos dos zonas de disponibilidad |
| secundaria | AWS Norte de Virginia `us-east-1` | activo-pasivo, réplica caliente de datos y cómputo reducido reproducible por IaC |
| región AWS Chile anunciada | no usada como dependencia | revisar tras disponibilidad general y solo si supera catálogo, multi-AZ, latencia, residencia y carbono |
| dominio común AWS | riesgo residual `SPOF-22` | copia inmutable y autoridad de borrado separada; portabilidad por componente |

Fuentes de vigencia consultadas: [regiones AWS](https://docs.aws.amazon.com/global-infrastructure/latest/regions/aws-regions.html), [zonas de disponibilidad](https://docs.aws.amazon.com/global-infrastructure/latest/regions/aws-availability-zones.html), [anuncio de región Chile](https://aws.amazon.com/blogs/aws/coming-soon-aws-south-america-chile-region/) y [estrategias de DR](https://docs.aws.amazon.com/wellarchitected/latest/framework/rel_planning_for_recovery_disaster_recovery.html).

`ADR-011` pasa de `CANDIDATO` a `PROPUESTO`. No pasa a `APROBADO`: siguen pendientes medición de latencia, tratamiento/residencia contractual, catálogo/certificaciones al congelar oferta, métrica regional de carbono y pruebas de DR/salida.

## 3. Cambios que cerraron brechas

| Brecha | Resolución |
|---|---|
| T-11 era una fila ficticia | sustituido por 32 filas concretas |
| nube sin proveedor ni lugar | AWS `sa-east-1` / `us-east-1` |
| racks sin fila propia | `T11-C2-21`: 2 racks 42U con PDUs A/B |
| escrow semestral omitido | `T11-SVC-01`: 1 servicio, 2 depósitos/año, BA Art. 84.6 |
| equipos de terreno “más repuestos” | 88 operativos + 9 repuestos; supuesto propio 10 %, validable por MTTR/lead time |
| gabinetes sin total | 59–61: 18 gate + 32 reefer + 3 muelle + 6–8 patio |
| puestos sin cantidad | baseline 3; AHT real es condición de validación |
| SIEM duplicable | `T11-SEC-04` absorbido por `T11-C2-19` |
| controles convertidos en compras repetidas | cifrado, red, backup, IaC/SBOM y frameworks se incluyen en su plataforma dueña |

## 4. Condiciones legítimas conservadas

Las siguientes condiciones no son campos vacíos ni bloquean el Informe 1:

- site survey para cerrar estaciones/gabinetes de patio;
- AHT para revalidar puestos;
- medición de enlaces y de la ingesta de logs;
- inventario final de nodos Linux y cargas EDR;
- congelamiento de fabricante/modelo/licencia y productos IAM/SOC en H2;
- pruebas futuras de 72 h, restauración, conmutación y retorno.

## 5. Control de alcance

- Los sistemas existentes del CLIENTE —TOS, ERP, VMS, básculas, barreras y control de grúas— no son provisión nueva.
- Los marcos incorporados al desarrollo —React, Spring Boot, React Native, SQLite, OpenAPI/AsyncAPI— no generan licencias separadas.
- La obra civil y canalizaciones ejecutadas por el CLIENTE permanecen especificadas en C2, pero no se fingen como suministro de TERABYTE.
- El hardware de terreno que TERABYTE debe especificar sigue visible aunque la compra corresponda al CLIENTE.

## 6. Puerta P3

**Cierre histórico:** MA-5 quedó lista para revisión y P3 fue superada. MA-6, MA-7 y MA-8 ya fueron completadas; la continuación vigente es la producción final descrita en `Celula3/README.md`.
