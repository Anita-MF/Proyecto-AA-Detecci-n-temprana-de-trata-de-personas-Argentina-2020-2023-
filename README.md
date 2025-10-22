Examen — Detección temprana de trata de personas (Argentina, 2020–2023)

**Objetivo.** Clasificador binario `es_trata` priorizando **Recall**. Entrenado con datos nacionales; análisis de **transferencia a TDF**.

## Reproducibilidad
- Python 3.x · pandas 2.x · scikit-learn 1.x · random_state=42
- Orden de ejecución:
  0–5 (prep/QA) → 6–11 (temporal/espacial/heatmaps) → 12–13 (TDF) → 14 (split/CV)
  → 15 (tuning) → 16–17 (umbral + ROC/PR/CM) → 20 (calibración) → 19 (interpretabilidad)
  → 21 (backtesting) → 22 (χ²) → 23 (interacciones) → 18 (inferencia)

## Umbral y calibración
- Umbral óptimo por curva PR con objetivo de **Recall** (Celda 16).
- Calibración isotónica (Celda 20). Output: `mejor_pipeline_calibrado.pkl` y `best_threshold_calibrado.json`.

## Transferencia a TDF
- Tablas trimestrales y por localidad (Celda 12) + gráficos (Celda 13).
- Evaluación en TDF con el **mismo umbral** del nacional (Celda 23).

## χ² e Interacciones
- Tablas de contingencia y p-values (Celda 22).
- Modelo Logístico con interacciones (mes/temporada, provincia, nacionalidad, anonimato) — Celda 23.

## Inferencia
1. Completar `results/inferencia_template_columns.csv` con casos nuevos o colocar un CSV en `data/infer/nuevos_casos.csv`.
2. Correr Celda 18 → genera `results/inferencia_{…}.csv` con `proba` y `pred_label`.

## Outputs
- `results/`: métricas, umbrales, calibración, χ², interacciones, TDF, backtesting, inferencia.
- `figs/`: gráficos temporales/espaciales, heatmaps, TDF, PR/ROC/CM, calibración, PI/PDP, backtesting.

