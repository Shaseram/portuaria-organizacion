# Subdocumento 4 — Arquitectura lógica y física de la solución

**Estado:** estructura de integración; solo incorporar contenido con estado `APROBADO`.  
**Caso:** 06 Portuaria — TERABYTE.  
**Fuente de control:** Maestro, Plan y Matriz de Cumplimiento Global.

> Este archivo será el contenido final. No debe convertirse en bitácora, lista de tareas ni depósito de borradores. Las fuentes y demostraciones extensas quedan en las carpetas de trazabilidad; aquí se conservan citas suficientes y narrativa autónoma.

## 4.1 Arquitectura lógica

### 4.1.1 Esquema de solución

**Origen:** A1.  
**Debe contener:** propósito, límite TERABYTE, actores, sistemas conservados y diagrama de contexto.

`PENDIENTE DE INTEGRAR`

### 4.1.2 Principios y estilo arquitectónico

**Origen:** A1 + ADR-001.  
**Debe contener:** modularidad, alternativa comparada, operabilidad por TI=5, resiliencia y límite contra microservicios injustificados.

`PENDIENTE DE INTEGRAR`

### 4.1.3 Capas de la solución

**Origen:** A1.  
**Debe contener:** ocho capas obligatorias, responsabilidades y restricciones.

`PENDIENTE DE INTEGRAR`

### 4.1.4 Módulos y límites de contexto

**Origen:** A1.  
**Debe contener:** catálogo de contextos, dueño, datos/eventos, criticidad e interfaces.

`PENDIENTE DE INTEGRAR`

### 4.1.5 Modelo conceptual del dominio

**Origen:** A1.  
**Debe contener:** entidades, relaciones y eventos portuarios principales.

`PENDIENTE DE INTEGRAR`

### 4.1.6 Arquitectura de integración

**Origen:** A2.  
**Debe contener:** 21+7, servicios/contratos, mensajes, versionado, gobierno, resiliencia y fallback.

`PENDIENTE DE INTEGRAR`

### 4.1.7 Procesos críticos y convivencia con TOS 2012

**Origen:** A3.  
**Debe contener:** secuencias, autoridad dominio×zona×fase, ambas direcciones, conciliación, retorno, 72 h y 2029.

`PENDIENTE DE INTEGRAR`

### 4.1.8 Seguridad lógica

**Origen:** D1.  
**Debe contener:** Zero Trust, exposición, identidad, cifrado, seguridad transversal y confianza.

`PENDIENTE DE INTEGRAR`

## 4.2 Arquitectura física

### 4.2.1 Arquitectura física de la solución

**Origen:** C1.  
**Debe contener:** diagrama híbrido, nodos, zonas, enlaces, protocolos, capacidades, sistemas conservados y límite de oferta.

`PENDIENTE DE INTEGRAR`

### 4.2.2 Emplazamiento y justificación conforme al Artículo 16

**Origen:** C1.  
**Debe contener:** tabla por componente con seis criterios, región/zona, on-premise/edge y alternativa de sala.

`PENDIENTE DE INTEGRAR`

### 4.2.3 Tecnologías de software

**Origen:** C2.  
**Debe contener:** producto/servicio, versión/vigencia, operación, alternativa y lock-in.

`PENDIENTE DE INTEGRAR`

### 4.2.4 Implementos de hardware y software

**Origen:** C2 + C4 + D1.  
**Debe contener:** especificaciones, cantidades, interfaces, consumo, redundancia, seguridad y ambiente.

`PENDIENTE DE INTEGRAR`

### 4.2.5 Data center o sala técnica primaria

**Origen:** C2 + ADR-005.  
**Debe contener:** decisión, distribución, energía, climatización, racks, acceso, incendio, monitoreo y capacidad.

`PENDIENTE DE INTEGRAR`

### 4.2.6 Data center secundario / recuperación

**Origen:** C2 + C3.  
**Debe contener:** ubicación, alcance, replicación, capacidad, RTO/RPO y conmutación.

`PENDIENTE DE INTEGRAR`

### 4.2.7 Ambientes y estrategia de despliegue

**Origen:** C3.  
**Debe contener:** DEV, QA, PREPROD, PROD y DR; IaC, CI/CD, despliegue sin interrupción y retorno.

`PENDIENTE DE INTEGRAR`

### 4.2.8 Redes y comunicaciones

**Origen:** C3 + D1.  
**Debe contener:** segmentación, conductos, patio cargado, handover, enlaces diversos, VMS/ISPS y failover real.

`PENDIENTE DE INTEGRAR`

### 4.2.9 Operación desconectada y sincronización

**Origen:** A3 + C3.  
**Debe contener:** funciones disponibles/no disponibles, 72 h, procedimiento manual, buffer, reconciliación y ≤90 min.

`PENDIENTE DE INTEGRAR`

### 4.2.10 Alta disponibilidad, DR y respaldos

**Origen:** C3.  
**Debe contener:** 99,9 %, RTO/RPO, HA, 3-2-1-1-0, pruebas y SPOF.

`PENDIENTE DE INTEGRAR`

### 4.2.11 Dimensionamiento y plan de capacidad

**Origen:** C4.  
**Debe contener:** fórmulas, normal/peak, concurrencia, almacenamiento, red, crecimiento, holgura y cuello de botella.

`PENDIENTE DE INTEGRAR`

### 4.2.12 Seguridad física y operacional

**Origen:** D1 + D2 + C2/C3.  
**Debe contener:** controles por nodo, administración, hardening, EDR, logging, KMS/HSM, protección marina y evidencia.

`PENDIENTE DE INTEGRAR`

## 4.3 Decisiones de arquitectura

**Origen:** D2 + Registro ADR Global.  
**Debe contener:** tabla ejecutiva de decisiones y ADR relevantes con alternativas, selección, consecuencias y disparadores.

`PENDIENTE DE INTEGRAR`

## 4.4 Supuestos, dependencias y asuntos abiertos

**Origen:** Maestro §18 + decisiones/escalamientos de los tres frentes.  
**Regla:** distinguir lo externo de lo que falta desarrollar internamente.

`PENDIENTE DE INTEGRAR`

## 4.5 Formulario T-11

Se adjunta el contenido de [`02_FORMULARIO_T11_FINAL.md`](02_FORMULARIO_T11_FINAL.md), con las cinco columnas oficiales y sin precios.

`PENDIENTE DE INTEGRAR`

