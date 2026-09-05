# Célula 3 — Subdocumento 4: Arquitectura lógica y física

Este directorio es el espacio de trabajo trazable para construir el Subdocumento 4 del Caso 06 Portuaria. La distribución está definida por **frentes**, no por nombres personales.

## Orden de lectura obligatorio

1. [`00_Gobierno/00_MAESTRO_CONTEXTO_ARQUITECTURA.md`](00_Gobierno/00_MAESTRO_CONTEXTO_ARQUITECTURA.md): verdades, restricciones y decisiones heredadas.
2. [`00_Gobierno/01_PLAN_ENTREGABLES_Y_DEPENDENCIAS.md`](00_Gobierno/01_PLAN_ENTREGABLES_Y_DEPENDENCIAS.md): qué debe producir cada frente, dependencias y puertas de integración.
3. Índice del frente asignado: entregables, orden de trabajo y estado.
4. Archivo del entregable: contrato concreto, productos y definición de terminado.
5. Archivo `TRZ_*` asociado: demostración de origen y destino de cada afirmación.

## Regla de autoridad

El Maestro de Célula 3 deriva del Caso 06, las Bases Técnicas Transversales, las Bases Administrativas y la versión corregida de Célula 2. Si se detecta una contradicción, **no se resuelve silenciosamente**: se aplica la jerarquía indicada en el Maestro y se registra el conflicto en `DECISIONES_Y_ESCALAMIENTOS.md`.

## Estructura mínima esperada del repositorio

Los enlaces son relativos y no dependen del nombre de usuario, disco o carpeta local. Para conservar toda la trazabilidad de trabajo solo se requieren estas carpetas hermanas:

```text
raiz-del-repositorio/
├── Celula2/
└── Celula3/
```

`Celula3/` puede moverse junto con esa raíz completa. Si se copia de forma aislada, las referencias de evidencia hacia Célula 2 quedarán sin destino. No cambiar los enlaces por rutas absolutas personales.

Las Bases Administrativas, las Bases Técnicas Transversales y el PDF oficial del Caso 06 deben permanecer disponibles para el equipo en Drive u otro medio común para contrastes excepcionales. No son una dependencia de enlaces del repositorio: el Maestro cita documento, capítulo, código y materia, y contiene el contexto necesario para trabajar. Las carpetas auxiliares personales `Bases_caso/` y `continuacion_correccion/` no son requeridas.

## Regla de edición

- Cada frente edita sus entregables, diagramas y trazabilidad.
- El integrador designado actualiza los archivos globales en las puertas de integración.
- Nadie inventa interfaces, protocolos, cifras, productos, certificaciones ni decisiones del CLIENTE.
- Los archivos de `90_Consolidado/` reciben únicamente contenido aprobado para entrega.
- El Formulario T-11 final contiene especificaciones y cantidades técnicas, **nunca precios**.

## Estado inicial

La estructura y los contratos de trabajo quedaron preparados el 2026-09-04. Los nombres de responsables deben asignarse en la tabla de control del Plan sin renombrar carpetas ni archivos.
