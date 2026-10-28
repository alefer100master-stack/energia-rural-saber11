# Cobertura eléctrica rural y rendimiento en Saber 11 (Colombia, 2019–2022)

Proyecto de grado de la Especialización en Analítica de Datos (CUN).
Autores: Diego Alejandro Prada, Leidy Adriana Motta Molina y Cristian Stiven Quitian Rojas. Director: Juan Pablo Morales Arias.

| Entrega | Versión (etiqueta) | Cuaderno |
|---|---|---|
| ACA 1 — etapas 1 y 2 de la ruta (CRISP-DM: negocio, datos y preparación) | v0.1 | `notebooks/ACA1_etapas_1_y_2.ipynb` |
| ACA 2 | v0.2 | (pendiente) |
| ACA 3 | v1.0 | (pendiente) |

## Objetivo
Evaluar la relación entre la cobertura de energía eléctrica rural de los municipios y el rendimiento en Saber 11 de los estudiantes de sedes rurales de Colombia en 2019, 2020 y 2022, integrando datos abiertos del ICFES y de la UPME.

## Datos
| Fuente | Conjunto | Enlace | Licencia |
|---|---|---|---|
| ICFES | Resultados únicos Saber 11 (`kgxf-xxbe`), periodos 20194 y 20224 | https://www.datos.gov.co/d/kgxf-xxbe | CC BY-SA 4.0 |
| ICFES | Saber 11° 2020-2 (`rnvb-vnyh`) | https://www.datos.gov.co/d/rnvb-vnyh | CC BY-SA 4.0 |
| UPME | Índice de Cobertura de Energía Eléctrica (ICEE) municipal 2019–2022, 2023 y 2024 | https://www.upme.gov.co/indice-de-cobertura-de-energia-electrica-icee/ | Información pública (Ley 1712 de 2014), con citación |

- `data/raw/`: copias descargadas el 2026-10-15 (la fecha va en el nombre de cada archivo) y `manifiesto_descargas.csv` con la huella SHA-256 de cada una. Todos los archivos pesan menos de 25 MB.
- `data/processed/`: `panel_municipal_rural_2019_2022.csv` (panel analítico) e `icee_municipal_2019_2024.csv`.
- Los datos del ICFES están anonimizados por la entidad; solo se descargaron 23 columnas (sin fecha de nacimiento ni documento). Los datos derivados se comparten bajo CC BY-SA 4.0, como exige la licencia de origen.

## Cómo reproducir
1. Abra `notebooks/ACA1_etapas_1_y_2.ipynb` en Google Colab (Archivo › Subir cuaderno, o desde GitHub).
2. En la primera celda de código reemplace `USUARIO` en `REPO_URL` por la cuenta de GitHub del repositorio: el cuaderno clona el repositorio para tener los datos.
3. Entorno de ejecución › Ejecutar todas. Corre de principio a fin, sin errores y con semilla fija (`SEED = 42`).
   - Modo por defecto `congelado`: usa las copias de `data/raw/` y comprueba su SHA-256 contra el manifiesto.
   - `MODO_ADQUISICION=api`: vuelve a descargar de datos.gov.co (API SODA) y de la UPME.
4. Salidas: `results/tables/` (CSV y `cifras.json`), `results/figures/` (PNG a 300 dpi y SVG) y una fila nueva en `results/experiments.csv`. En Colab también se genera `requirements.txt` con `pip freeze`.

Ninguna cifra del documento de grado se escribe a mano: todas salen de `results/tables/`.

## Resultados principales (ACA 1)
- ETL: 2.667.284 registros crudos del ICFES; se eliminaron 1.083.409 filas duplicadas exactas. Panel final: 2.627 observaciones municipio–año de 926 municipios (242.126 estudiantes rurales).
- Asociación ICEE rural – puntaje global rural: ρ de Spearman = 0,30 (IC 95 %: 0,27–0,34). La relación sigue siendo positiva dentro de grupos de municipios con nivel educativo parecido (ρ de 0,27 a 0,34).
- Los municipios con cobertura rural alta (≥95 %) superan en 16,1 puntos a los de cobertura baja (<70 %).
- La asociación se repite en 2019, 2020 y 2022 y es heterogénea por región (ver `results/tables/T18_robustez_spearman.csv`).

## Entorno de cómputo
- Máquina: Linux x86_64 (CPU); sin GPU. Tiempo de ejecución completo del cuaderno: 93 s. No hay entrenamiento de modelos en el ACA 1.
- Python 3.13.16; pandas 3.0.5, NumPy 2.5.3, SciPy 1.18.1, scikit-learn 1.9.1, Matplotlib 3.11.2, seaborn 0.13.2. Versiones exactas en `requirements.txt` (reemplácelo por el generado en Colab).

## Estructura
```
energia-rural-saber11/
├── README.md
├── notebooks/            ACA1_etapas_1_y_2.ipynb 
├── data/
│   ├── raw/              copias descargadas con fecha + manifiesto SHA-256
│   └── processed/        panel limpio listo para modelar
├── results/
│   ├── tables/           tablas CSV y cifras.json
│   ├── figures/          PNG 300 dpi y SVG
│   └── experiments.csv   una fila por corrida
├── models/               model_card.md (sin modelo en v0.1)
├── docs/                 bitácora de decisiones, protocolo de evaluación y diagrama de la ruta
├── requirements.txt
└── LICENSE               MIT
```
