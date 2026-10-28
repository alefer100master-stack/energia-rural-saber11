# Protocolo de evaluación (fijado en el ACA 1, antes de cualquier prueba formal)

Enfoque descriptivo/diagnóstico. Cualquier cambio se justifica en `bitacora_decisiones.csv`.

| Elemento | Definición / fórmula | Referencia o regla |
|---|---|---|
| KPI 1. Puntaje global rural | PG(m,t) = promedio de punt_global de estudiantes rurales del municipio m en el año t | Media nacional rural del año; línea base 2019 |
| KPI 2. Brecha urbano–rural | BUR(m,t) = PG urbano − PG rural | Brecha nacional 2019 |
| KPI 3. ICEE rural | VCS rural / VT rural × 100 | ICEE rural nacional del año; bandas <70 %, 70–95 %, ≥95 % |
| KPI 4. Diferencia por cobertura | PG medio (Alta) − PG medio (Baja) | Grupo de control: banda Alta |
| KPI 5. Asociación | ρ de Spearman con IC 95 % bootstrap (B = 2.000, semilla 42) | ρ = 0 |
| KPI 6. Varianza asociada | ΔR² del ICEE sobre controles socioeconómicos + efectos fijos de año | ΔR² = 0 |
| Pruebas (ACA 3) | H1 Spearman por año/región; H2 Kruskal–Wallis + Dunn; H3 Mann–Whitney + delta de Cliff; H4 panel con efectos fijos y errores agrupados por municipio; H5 interacción ICEE × año | α = 0,05; corrección de Holm |
| Validación | Robustez por año, región, umbral de estudiantes, ICEE con/sin transferencias, áreas | Mismo signo e IC sin cero en ≥2 de 3 años |
| Criterio de éxito | \|ρ\| ≥ 0,10 con IC 95 % sin cero en ≥2 de 3 años y ΔR² ≥ 0,02 con p < 0,05 tras Holm | Cohen (1988) |
