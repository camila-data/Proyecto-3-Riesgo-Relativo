# Validación de Hipótesis: Riesgo de Impago según la Edad

## Hipótesis:
Los más jóvenes tienen un mayor riesgo de impago.

## Análisis:

Para validar esta hipótesis, se realizó un análisis en el que se dividieron los clientes en cuartiles según su edad. Posteriormente, se calculó la tasa de impago (default flag) para cada cuartil y se comparó con la tasa de impago del primer cuartil (los más jóvenes) para obtener el riesgo relativo.

### Resultados:

| Cuartil de Edad | Rango de Edad | Tasa de Impago (%) | Riesgo Relativo |
|-----------------|---------------|--------------------|-----------------|
| **Q1**          | 21 a 41 años  | 3.43%              | 1.00            |
| **Q2**          | 41 a 52 años  | 2.08%              | 0.61            |
| **Q3**          | 52 a 62 años  | 1.33%              | 0.39            |
| **Q4**          | 62 a 83 años  | 0.58%              | 0.17            |

### Interpretación:

- **Q1 (21 a 41 años)**: Los clientes en este cuartil, que son los más jóvenes, presentan la tasa de impago más alta, con un 3.43%. Este grupo sirve como base de comparación para los otros cuartiles, con un riesgo relativo de 1.00.

- **Q2 (41 a 52 años)**: A medida que la edad aumenta, la tasa de impago disminuye al 2.08%, lo que equivale a un riesgo relativo de 0.61 en comparación con Q1.

- **Q3 (52 a 62 años)**: La tasa de impago continúa disminuyendo a 1.33%, lo que representa un riesgo relativo de 0.39 en comparación con los más jóvenes.

- **Q4 (62 a 83 años)**: Los clientes en el cuarto cuartil, los mayores, presentan la tasa de impago más baja, con solo un 0.58%. Esto da un riesgo relativo de 0.17, lo que indica que tienen un 83.02% menos de riesgo de impago en comparación con los más jóvenes.

### Conclusión:

Los resultados confirman la hipótesis de que los más jóvenes (Q1: 21 a 41 años) tienen un mayor riesgo de impago en comparación con los clientes de mayor edad. A medida que la edad aumenta, el riesgo de impago disminuye significativamente.
