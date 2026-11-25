# Licencias y autorización de uso de los datos

Este proyecto usa únicamente datos abiertos publicados por entidades del Estado colombiano. No se requirió autorización adicional.

| Fuente | Conjunto | Enlace | Licencia o autorización |
|---|---|---|---|
| ICFES | Resultados únicos Saber 11 (`kgxf-xxbe`), periodos 20194 y 20224 | https://www.datos.gov.co/d/kgxf-xxbe | Creative Commons Atribución-CompartirIgual 4.0 Internacional (CC BY-SA 4.0) |
| ICFES | Saber 11° 2020-2 (`rnvb-vnyh`), periodo 20204 | https://www.datos.gov.co/d/rnvb-vnyh | CC BY-SA 4.0 |
| UPME | Índice de Cobertura de Energía Eléctrica (ICEE), anexos municipales 2019–2022, 2023 y 2024 | https://www.upme.gov.co/indice-de-cobertura-de-energia-electrica-icee/ | Información pública (Ley 1712 de 2014), uso con citación de la fuente |

## Condiciones que cumple el proyecto

- **Atribución:** cada fuente se cita en el documento de grado (APA 7) y en el `README.md`.
- **Compartir igual:** los datos derivados del ICFES (`data/processed/`) se comparten bajo la misma licencia CC BY-SA 4.0. El código del repositorio usa la licencia MIT (`LICENSE`).
- **Copias fechadas:** `data/raw/` guarda las copias descargadas el 2026-10-15 con su huella SHA-256 en `data/raw/manifiesto_descargas.csv`.

## Datos personales

- Los microdatos del ICFES están anonimizados por la entidad. El campo `estu_consecutivo` es un código seudonimizado asignado por el ICFES; por sí solo no identifica a la persona y no se publica en los resultados.
- Por minimización (Ley 1581 de 2012) solo se descargaron 23 columnas; no se descargaron fecha de nacimiento, tipo ni número de documento.
- Los resultados se publican agregados por municipio y año; el panel analítico no contiene registros individuales.
- Los anexos de la UPME no contienen datos personales.
