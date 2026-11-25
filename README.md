# Cobertura eléctrica rural y rendimiento en Saber 11 (Colombia, 2019–2022)

Proyecto de grado de la Especialización en Analítica de Datos (CUN).
Integrantes: Diego Alejandro Prada Fernández, Juan David Sierra Laborde y Jhan Carlos Guerrero Silva. Director: Juan Pablo Morales Arias.

| Entrega | Versión (etiqueta) | Cuaderno |
|---|---|---|
| ACA 1 — etapas 1 y 2 de la ruta (CRISP-DM: negocio, datos y preparación) | v0.1 (con los ajustes de la retroalimentación en v0.2) | `notebooks/ACA1_etapas_1_y_2.ipynb` |
| ACA 2 — etapas 2 y 3: ingeniería de características, modelo dimensional, KPIs, tablero, pruebas de hipótesis y batería de modelos | **v0.2** | `notebooks/ACA2_etapas_2_y_3.ipynb` |
| ACA 3 | v1.0 | (pendiente) |

## Objetivo
Evaluar la relación entre la cobertura de energía eléctrica rural de los municipios y el rendimiento en Saber 11 de los estudiantes de sedes rurales de Colombia en 2019, 2020 y 2022, integrando datos abiertos del ICFES y de la UPME.

## Datos
| Fuente | Conjunto | Enlace | Licencia |
|---|---|---|---|
| ICFES | Resultados únicos Saber 11 (`kgxf-xxbe`), periodos 20194 y 20224 | https://www.datos.gov.co/d/kgxf-xxbe | CC BY-SA 4.0 |
| ICFES | Saber 11° 2020-2 (`rnvb-vnyh`) | https://www.datos.gov.co/d/rnvb-vnyh | CC BY-SA 4.0 |
| UPME | Índice de Cobertura de Energía Eléctrica (ICEE) municipal 2019–2022, 2023 y 2024 | https://www.upme.gov.co/indice-de-cobertura-de-energia-electrica-icee/ | Información pública (Ley 1712 de 2014), con citación |

- `data/raw/`: copias descargadas el 2026-10-15 y `manifiesto_descargas.csv` con la huella SHA-256 de cada una.
- `data/processed/`: panel analítico (`panel_municipal_rural_2019_2022.csv`), ICEE municipal y `modelo_dimensional/` (dimensiones, hechos de cobertura y vista del panel en CSV). La base SQLite completa (`modelo_dimensional.sqlite`, unos 160 MB) no se sube: la regenera el cuaderno ACA2.
- Los datos del ICFES están anonimizados por la entidad. Los datos derivados se comparten bajo CC BY-SA 4.0, como exige la licencia de origen.

## Cómo reproducir
1. Abra en Google Colab el cuaderno ACA1 y luego el ACA2 (en ese orden: el ACA2 usa el panel que produce el ACA1):
   - https://colab.research.google.com/github/alefer100master-stack/energia-rural-saber11/blob/v0.2/notebooks/ACA1_etapas_1_y_2.ipynb
   - https://colab.research.google.com/github/alefer100master-stack/energia-rural-saber11/blob/v0.2/notebooks/ACA2_etapas_2_y_3.ipynb
2. La primera celda de código clona este repositorio en la etiqueta `v0.2`.
3. Entorno de ejecución › Ejecutar todas. Corren de principio a fin con semilla fija (`SEED = 42`). El ACA2 tarda unos 6 minutos en CPU.
4. Salidas del ACA2: `results/tables/` (prefijo `A2_`, `cifras_aca2.json` y `metricas_por_particion.csv`), `results/figures/` (prefijo `A2_`), `results/dashboard/tablero_aca2.html` (tablero: se abre con doble clic), `models/model_card.md` y filas nuevas en `results/experiments.csv`.

Ninguna cifra del documento de grado se escribe a mano: todas salen de `results/tables/`.

## Resultados principales (ACA 2)
- Modelo dimensional (esquema estrella en SQLite): 22 de 25 controles de totales dan diferencia cero contra la fuente; los demás son las diferencias que explica el ETL.
- Objetivo 2: asociación ICEE rural – puntaje significativa en los tres años (ρ de 0,281 a 0,325, Holm p < 0,001); clara en Orinoquía, Caribe y Amazonía y nula en Andina y Pacífica.
- Objetivo 3: entre municipios, +10 puntos porcentuales de ICEE ↔ +2,47 puntos de puntaje; ΔR² = 0,073. Dentro del mismo municipio no es significativa (H4: p = 0,23). La interacción ICEE × región es significativa (H6).
- Batería de 10 modelos (validación 5 × 3 agrupada por municipio): mejor modelo Red neuronal (MLP), RMSE 15,71 ± 0,64 frente a 24,72 de la línea base; MAE 12,1 puntos.

## Entorno de cómputo
- Google Colab, CPU estándar (sin GPU). XGBoost y LightGBM se entrenan si están instalados (vienen en Colab).
- Ejecución que generó `results/`: Python 3.13.18, pandas 3.0.5, scikit-learn 1.9.1, SciPy 1.18.1, Matplotlib 3.11.2; XGBoost no y LightGBM no disponibles; tiempo 353 s. Versiones de Colab en `requirements.txt`.

## Estructura
```
energia-rural-saber11/
├── README.md
├── notebooks/            ACA1_etapas_1_y_2.ipynb · ACA2_etapas_2_y_3.ipynb
├── data/
│   ├── raw/              copias descargadas con fecha + manifiesto SHA-256
│   └── processed/        panel, ICEE y modelo_dimensional/ (CSV)
├── results/
│   ├── tables/           tablas CSV, cifras.json, cifras_aca2.json, metricas_por_particion.csv
│   ├── figures/          PNG 300 dpi y SVG
│   ├── dashboard/        tablero_aca2.html
│   └── experiments.csv   una fila por modelo y corrida
├── models/               model_card.md
├── docs/                 bitácora de decisiones, protocolo de evaluación, licencias y diagramas
├── requirements.txt
├── LICENSE               MIT (código)
└── .github/workflows/    flujo auxiliar que descomprime archivos subidos por partes
```

Licencias y uso de los datos: ver `docs/licencia_datos.md`.
