# TRZ-D1 — Arquitectura de seguridad

| ID | Fuente | RNF/MC | Control | Actor/dato | Capa/componente | Nodo/servicio | Evidencia | T-11 | Estado |
|---|---|---|---|---|---|---|---|---|---|
| `TRZ-D1-001` | BTT Cap. 11 | RNF-SEG | Zero Trust/STRIDE | todos | transversal | POR DEFINIR | modelo/prueba | candidatos | PENDIENTE |
| `TRZ-D1-002` | BTT Cap. 12 + Caso 06 | MC-04 | IAM terminal/eventual | ACT-EVT/externos | SRV-IAM | POR DEFINIR | matriz/sesión | sí | PENDIENTE |
| `TRZ-D1-003` | BTT Cap. 11 | RNF-SEG | WAF/DDoS/TLS | públicos | GW-EDGE | nube multi-AZ | prueba/config | sí | PENDIENTE |
| `TRZ-D1-004` | BTT Cap. 11 | RNF-SEG/OPE | log/SIEM/EDR | operación | transversal | híbrido | caso portuario | sí | PENDIENTE |
| `TRZ-D1-005` | FEP02 Cap. 7 RT-07.09..12; C2 B1 | RNF-DIS-14 | respaldo cifrado/inmutable | datos y claves | POR DEFINIR | POR DEFINIR | restauración mensual; resistencia al borrado | POR DEFINIR | PENDIENTE |
| `TRZ-D1-006` | Caso 06 Anexo A; FEP02 Cap. 12; C2 B2/C3 | RF-POR-02; RF-POR-09 | identidad/autorización y evidencia de carga | ACT-AGE | CH-PORTAL/SRV-IAM | POR DEFINIR | validación, permisos y trazabilidad por registro | POR DEFINIR | PENDIENTE |
| `TRZ-D1-007` | FEP02 Cap. 11 RT-11.17; Caso 06 Cap. 10 restricción 11 | obligación directa BTT; sin RNF equivalente declarado | SOC 24x7 | TI=5 | POR DEFINIR | POR DEFINIR | ubicación, dotación y procedimientos | POR DEFINIR | PENDIENTE |
