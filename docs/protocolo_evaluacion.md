# Protocolo de evaluación (fijado en el ACA 1, antes de cualquier prueba formal; ajustado en la v0.2 tras la retroalimentación)

Enfoque descriptivo/diagnóstico. Cualquier cambio se justifica en `bitacora_decisiones.csv`.

| Elemento | Definición / fórmula | Referencia o regla |
|---|---|---|
| KPI 1. Puntaje global rural | PG(m,t) = promedio de punt_global de estudiantes rurales del municipio m en el año t | Media nacional rural del año; línea base 2019 |
| KPI 2. Brecha urbano–rural | BUR(m,t) = PG urbano − PG rural | Brecha nacional 2019 |
| KPI 3. ICEE rural | VCS rural / VT rural × 100 | ICEE rural nacional del año; bandas <70 %, 70–95 %, ≥95 % |
| KPI 4. Diferencia por cobertura | PG medio (Alta) − PG medio (Baja) | Grupo de control: banda Alta |
| KPI 5. Asociación | ρ de Spearman con IC 95 % bootstrap (B = 2.000, semilla 42) | ρ = 0 |
| KPI 6. Varianza asociada | ΔR² del ICEE sobre controles socioeconómicos + efectos fijos de año | ΔR² = 0 |
| Métrica principal | KPI 5: ρ de Spearman ICEE rural–puntaje con IC 95 % | Decide si la asociación es relevante |
| Métricas secundarias | KPI 4 (Alta − Baja) y KPI 6 (ΔR²); KPI 1–3 de seguimiento | Se reportan junto a la principal |
| Línea base | ρ = 0 y ΔR² = 0 (sin asociación); año 2019 para KPI 1–3 | Referencia de comparación |
| Pruebas (H1–H6, ejecutadas en el ACA 2) | H1 Spearman por año/región; H2 Kruskal–Wallis + Dunn; H3 Mann–Whitney + delta de Cliff; H4 panel con efectos fijos y errores agrupados por municipio; H5 interacción ICEE × año; H6 interacción ICEE × región | α = 0,05; corrección de Holm |
| Sensibilidad y diagnóstico espacial (v0.2) | Repetir las estimaciones con imputación por mediana y por KNN; la imputación se ajusta dentro de cada remuestreo, solo con los datos de esa iteración; I de Moran de puntajes y residuos | La conclusión no debe depender del método de imputación; si hay patrón territorial se reporta y se usan errores agrupados |
| Partición y validación (ACA 2) | Pruebas H1–H6 sobre todo el panel. Batería de modelos: prueba = 20 % de los municipios separada antes de toda transformación; validación 5 × 3 agrupada por municipio y estratificada por banda; Pipeline (KNN + escalado); búsqueda aleatoria de 20 combinaciones por modelo. Robustez: año, región, umbral de estudiantes, ICEE con/sin transferencias, grupos comparables, semillas y validación temporal | RMSE, MAE, MAPE y R² (media ± d.e.); mismo signo e IC sin cero en ≥2 de 3 años |
| Criterio de éxito | \|ρ\| ≥ 0,10 con IC 95 % sin cero en ≥2 de 3 años y ΔR² ≥ 0,02 con p < 0,05 tras Holm | Cohen (1988) |


**Resultado (ACA 2):** criterio de éxito cumplido — 3 de 3 años con |ρ| ≥ 0,10 e IC sin cero; ΔR² = 0,073 con p ajustado < 0,05 (`results/tables/A2_T21_criterio_exito.csv`).
