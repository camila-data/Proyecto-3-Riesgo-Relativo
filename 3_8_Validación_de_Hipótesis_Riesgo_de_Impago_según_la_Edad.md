# Validación de Hipótesis: Riesgo de Impago según la Edad

## Hipótesis:
Los más jóvenes tienen un mayor riesgo de impago.

## Análisis:

Para validar esta hipótesis, se realizaron cálculos de la tasa de impago (default flag) para cada cuartil de edad, utilizando los datos obtenidos en BigQuery. Se calculó también el riesgo relativo de impago de los demás cuartiles en comparación con el primer cuartil (Q1), que representa a los más jóvenes.

### Resultados:

| Cuartil de Edad | Rango de Edad | Tasa de Impago (%) | Riesgo Relativo |
|-----------------|---------------|--------------------|-----------------|
| **Q1**          | 21 a 41 años  |                    | 2.46            |
| **Q2**          | 41 a 52 años  | 2.18%              | 0.63            |
| **Q3**          | 52 a 62 años  | 1.39%              | 0.40            |
| **Q4**          | 62 a 83 años  | 0.57%              | 0.16            |

### Interpretación:

- **Q1 (21 a 41 años)**: Los clientes en este cuartil, que son los más jóvenes, presentan la tasa de impago más alta, lo que confirma la hipótesis de que los más jóvenes tienen un mayor riesgo de impago.

- **Q2 (41 a 52 años)**: A medida que la edad aumenta, la tasa de impago disminuye, lo que implica un menor riesgo de impago en comparación con Q1.

- **Q3 (52 a 62 años)**: La tasa de impago continúa disminuyendo, lo que muestra un riesgo aún menor.

- **Q4 (62 a 83 años)**: Los clientes en el cuarto cuartil, los mayores, presentan la tasa de impago más baja, lo que refuerza la idea de que el riesgo de impago disminuye con la edad.

### Conclusión:

Los resultados obtenidos en BigQuery validan la hipótesis de que los más jóvenes tienen un mayor riesgo de impago. La tasa de impago disminuye significativamente a medida que aumenta la edad, y el riesgo relativo es considerablemente menor en los grupos de mayor edad.

