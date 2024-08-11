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

## Resultados
| Cuartil Expuesto | Tasa de Impago (%) | Riesgo Expuesto | Riesgo No Expuesto | Riesgo Relativo | Rango Mínimo de Préstamos | Rango Máximo de Préstamos | Cantidad Default (flag=1) | Cantidad No Default (flag=0) |
|------------------|-------------------|-----------------|--------------------|-----------------|---------------------------|---------------------------|----------------------------|-----------------------------|
| **Q1**           | 2.96%             | 0.0296          | 0.0154             | 1.9137          | 1                         | 5                         | 266                        | 8734                        |
| **Q2**           | 1.70%             | 0.0170          | 0.0196             | 0.8660          | 5                         | 8                         | 153                        | 8847                        |
| **Q3**           | 1.73%             | 0.0173          | 0.0195             | 0.8880          | 8                         | 11                        | 156                        | 8844                        |
| **Q4**           | 1.20%             | 0.0120          | 0.0213             | 0.5635          | 11                        | 57                        | 108                        | 8892                        |


## Conclusión General:
La hipótesis "Las personas con más cantidad de préstamos activos tienen mayor riesgo de ser malos pagadores" **no se valida**. De hecho, los resultados sugieren lo contrario: a mayor número de préstamos, menor es la probabilidad de impago. 

Este hallazgo está respaldado por:
- Un riesgo relativo de impago más bajo en el cuartil con más préstamos (Q4).
- Resultados consistentes obtenidos en BigQuery con la siguiente consulta.
  
  ##sql
  
 ```sql
WITH Cuartiles AS (
    SELECT 
        total_prestamos,
        CAST(default_flag AS INT64) AS default_flag,
        NTILE(4) OVER (ORDER BY total_prestamos) AS cuartil
    FROM 
        `laboratoria-426416.riesgo_relativo.tabla_real`
),
ConteoPorCuartil AS (
    SELECT
        cuartil,
        default_flag,
        COUNT(*) AS cantidad,
        MIN(total_prestamos) AS min_prestamos,
        MAX(total_prestamos) AS max_prestamos
    FROM
        Cuartiles
    GROUP BY
        cuartil,
        default_flag
),
RiskCalculation AS (
    SELECT
        cuartil,
        MIN(min_prestamos) AS rango_min_prestamos,
        MAX(max_prestamos) AS rango_max_prestamos,
        SUM(CASE WHEN default_flag = 1 THEN cantidad ELSE 0 END) AS default_count,
        SUM(CASE WHEN default_flag = 0 THEN cantidad ELSE 0 END) AS non_default_count,
        SUM(cantidad) AS total_count,
        SUM(CASE WHEN default_flag = 1 THEN cantidad ELSE 0 END) * 1.0 / SUM(cantidad) AS risk
    FROM 
        ConteoPorCuartil
    GROUP BY 
        cuartil
),
CombinedRisk AS (
    SELECT
        rc.cuartil AS cuartil_expuesto,
        SUM(CASE WHEN rc2.cuartil != rc.cuartil THEN rc2.risk * rc2.total_count ELSE 0 END) / 
        SUM(CASE WHEN rc2.cuartil != rc.cuartil THEN rc2.total_count ELSE 0 END) AS combined_non_exposed_risk
    FROM 
        RiskCalculation rc
    JOIN 
        RiskCalculation rc2
    ON 
        rc.cuartil != rc2.cuartil
    GROUP BY 
        rc.cuartil
)
SELECT
    rc.cuartil AS cuartil_expuesto,
    rc.risk AS exposed_risk,
    cr.combined_non_exposed_risk AS non_exposed_risk,
    rc.risk / cr.combined_non_exposed_risk AS risk_relative,
    rc.rango_min_prestamos,
    rc.rango_max_prestamos,
    rc.default_count AS cantidad_default_flag_1,
    rc.non_default_count AS cantidad_default_flag_0
FROM
    RiskCalculation rc
JOIN
    CombinedRisk cr
ON
    rc.cuartil = cr.cuartil_expuesto
ORDER BY 
    cuartil_expuesto;

