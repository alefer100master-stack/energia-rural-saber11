# Tarjeta del modelo (versión v0.2, ACA 2)

**Propósito.** Diagnóstico, no predicción: medir cuánta variación del puntaje global rural de Saber 11 (promedio municipal, 2019, 2020 y 2022) se asocia a
la cobertura eléctrica rural (ICEE de la UPME), después de tener en cuenta el contexto socioeconómico, territorial y escolar (objetivo específico 3).

**Datos.** Panel municipal rural de 2,627 municipio–año (926 municipios). Prueba: 20 % de los municipios, separados antes de
cualquier transformación. Variables: 17 seleccionadas con LASSO (estabilidad ≥ 80 % en 15 particiones) e información mutua.

**Modelos comparados.** Línea base (promedio), Regresión lineal, Ridge, Lasso, KNN, SVR, Árbol de decisión, Random Forest, HistGradientBoosting, XGBoost, LightGBM, Red neuronal (MLP); además stacking y votación de los tres mejores. Validación: 5 pliegues × 3 repeticiones, agrupados por
municipio y estratificados por banda de cobertura; búsqueda aleatoria de 20 combinaciones por modelo.

**Mejor modelo: Red neuronal (MLP).** RMSE de validación 15.74 ± 0.88 puntos (línea base 23.67);
R² 0.554 ± 0.050; en la prueba RMSE 15.15 y R² 0.658. Sin las variables de energía
el RMSE sube 0.07 ± 0.45 puntos.

**Modelo inferencial.** Panel con efectos fijos de municipio y año y errores agrupados por municipio (H4–H6); ver `results/tables/A2_T18_modelos_panel.csv`.

**Limitaciones.** Asociación, no causalidad. Unidad municipal (no se concluye sobre estudiantes). El ICEE mide cobertura, no calidad del servicio.
Pocos años por municipio (máximo 3). Usos no recomendados: asignar recursos a un municipio solo con la predicción del modelo.
