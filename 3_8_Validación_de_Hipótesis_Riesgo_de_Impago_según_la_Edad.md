# Validación de Hipótesis: Riesgo de Impago según la Edad

## Hipótesis:
Los más jóvenes tienen un mayor riesgo de impago.

## Análisis:

Para validar esta hipótesis, se realizaron cálculos de la tasa de impago (default flag) para cada cuartil de edad, utilizando los datos obtenidos en BigQuery. Se calculó también el riesgo relativo de impago de los demás cuartiles en comparación con el primer cuartil (Q1), que representa a los más jóvenes.

### Resultados:

| Cuartil de Edad | Rango de Edad | Tasa de Impago (%) | Riesgo Relativo |
|-----------------|---------------|--------------------|-----------------|
| **Q1**          | 21 a 41 años  | 3.43%              | 2.46            |
| **Q2**          | 41 a 52 años  | 2.21%              | 1.23            |
| **Q3**          | 52 a 62 años  | 1.39%              | 0.67            |
| **Q4**          | 62 a 83 años  | 0.57%              | 0.24            |

### Interpretación:

- **Q1 (21 a 41 años)**: Los clientes en este cuartil, que son los más jóvenes, presentan la tasa de impago más alta, lo que confirma la hipótesis de que los más jóvenes tienen un mayor riesgo de impago.

- **Q2 (41 a 52 años)**: A medida que la edad aumenta, la tasa de impago disminuye, lo que implica un menor riesgo de impago en comparación con Q1.

- **Q3 (52 a 62 años)**: La tasa de impago continúa disminuyendo, lo que muestra un riesgo aún menor.

- **Q4 (62 a 83 años)**: Los clientes en el cuarto cuartil, los mayores, presentan la tasa de impago más baja, lo que refuerza la idea de que el riesgo de impago disminuye con la edad.

## Conclusión:
Los resultados obtenidos en BigQuery validan la hipótesis de que los más jóvenes tienen un mayor riesgo de impago. La tasa de impago disminuye significativamente a medida que aumenta la edad, y el riesgo relativo es considerablemente menor en los grupos de mayor edad.

```sql
WITH Cuartiles AS (
    SELECT 
        age,
        CAST(default_flag AS INT64) AS default_flag, -- Asegurarse de que default_flag sea un número entero
        NTILE(4) OVER (ORDER BY age) AS cuartil
    FROM 
        `laboratoria-426416.riesgo_relativo.tabla_matriz`
),
ConteoPorCuartil AS (
    SELECT
        cuartil,
        default_flag,
        COUNT(*) AS cantidad,
        MIN(age) AS min_edad,
        MAX(age) AS max_edad
    FROM
        Cuartiles
    GROUP BY
        cuartil,
        default_flag
),
RiskCalculation AS (
    SELECT
        cuartil,
        MIN(min_edad) AS rango_min_edad,
        MAX(max_edad) AS rango_max_edad,
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
    rc.rango_min_edad,
    rc.rango_max_edad,
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
