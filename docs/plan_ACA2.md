# Plan del ACA 2 — Estado (v0.2): ejecutado, salvo el paso 6 (I de Moran con vecindad geográfica), que pasa al ACA 3 porque requiere coordenadas municipales

<!-- -->
# Plan del ACA 2 (etapa 3 de la ruta) con la retroalimentación del Avance 1

Punto de partida: panel municipal rural de 2.627 filas (v0.2), protocolo de la sección 7.9 y bitácora de decisiones.

| # | Qué se hará | De dónde sale | Cómo se hará |
|---|---|---|---|
| 1 | Pipeline de preprocesamiento | Retroalimentación; sección 8.7 | `Pipeline` de scikit-learn con `StandardScaler` + `KNNImputer(5)`. Se ajusta **dentro de cada iteración** del bootstrap, solo con los datos de esa iteración. |
| 2 | Modelo dimensional | Cronograma (Tabla 2) | Hechos: puntajes. Dimensiones: municipio, año, región y banda de cobertura. |
| 3 | KPIs del protocolo | Tabla 4 | KPI 1 a 6 calculados sobre el modelo dimensional, con su línea base. |
| 4 | Pruebas H1 a H3 por año y región | Tabla 4 | Spearman con IC 95 % por bootstrap; Kruskal–Wallis + Dunn; Mann–Whitney + delta de Cliff; corrección de Holm, α = 0,05. |
| 5 | Sensibilidad mediana frente a KNN | Retroalimentación; Anexo D.2 | Repetir los pasos 3 y 4 con cada método y comparar el tamaño del efecto (ρ, diferencia entre bandas, ΔR²). |
| 6 | I de Moran con vecindad geográfica real | Retroalimentación; Anexo D.1 | Agregar coordenadas o límites municipales del DANE; vecinos por contigüidad o por los k más cercanos; I de Moran de puntajes y de residuos; mapa. |
| 7 | Dejar lista la interacción ICEE × región (H6) | Retroalimentación; Anexo D.3 | Variables de región e interacción en el modelo dimensional; la estimación formal va en el panel del ACA 3. |
| 8 | Documentación | Retroalimentación | Cada ajuste se registra en `docs/bitacora_decisiones.csv` con fecha, alternativas y evidencia. |

Pendiente para poder hacer el paso 6: un archivo con las coordenadas o los límites de los municipios (por ejemplo, el Marco Geoestadístico Nacional del DANE o el conjunto DIVIPOLA de datos.gov.co con latitud y longitud).
