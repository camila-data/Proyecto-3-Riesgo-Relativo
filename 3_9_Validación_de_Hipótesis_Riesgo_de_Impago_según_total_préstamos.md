# Análisis de Riesgo de Impago en Función del Número de Préstamos Activos

## Objetivo:
Validar la hipótesis de que "Las personas con más cantidad de préstamos activos tienen mayor riesgo de ser malos pagadores".

## Metodología:
1. **Segmentación de los Datos:**
   - Los datos fueron divididos en cuartiles según la cantidad de préstamos activos sacados de la variable creada (`total_prestamos`).
   - Cada cuartil fue analizado para determinar la tasa de impago (`default_flag`) y calcular el riesgo relativo comparando cada cuartil con el cuartil con más préstamos (Q4).

2. **Cálculo del Riesgo Relativo:**
   - El riesgo relativo se calculó comparando la tasa de impago en cada cuartil con la del cuartil con más préstamos (Q4), que se utilizó como referencia.


## Resultados:

### Tasa de Impago por Cuartil de Préstamos:

| Cuartil de Préstamos | Rango de Préstamos | Tasa de Impago (%) | Riesgo Relativo |
|----------------------|--------------------|--------------------|-----------------|
| **Q1**               | 1 a 5 préstamos    | 2.96%              | 2.46            |
| **Q2**               | 5 a 8 préstamos    | 1.70%              | 1.42            |
| **Q3**               | 8 a 11 préstamos   | 1.73%              | 1.44            |
| **Q4**               | 11 a 57 préstamos  | 1.20%              | 1.00 (referencia) |



## Conclusión General:
La hipótesis "Las personas con más cantidad de préstamos activos tienen mayor riesgo de ser malos pagadores" **no se valida**. De hecho, los resultados sugieren lo contrario: a mayor número de préstamos, menor es la probabilidad de impago. 

Este hallazgo está respaldado por:
- Un riesgo relativo de impago más bajo en el cuartil con más préstamos (Q4).
- Resultados consistentes obtenidos en BigQuery.

