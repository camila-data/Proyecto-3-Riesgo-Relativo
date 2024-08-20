# Score Crediticio

Este documento describe el proceso de creación de un score crediticio para clasificar a los clientes como "buen pagador" o "mal pagador". El score se ha desarrollado utilizando varias variables relevantes en un entorno BigQuery, y se ha optimizado para identificar con precisión el riesgo de incumplimiento.

## 2. Variables Utilizadas

Se seleccionaron y utilizaron las siguientes variables clave para construir el score crediticio:

- **`any_delay`**: Indica si el cliente ha tenido algún retraso en sus pagos. Esta variable recibió un peso doble debido a su importancia en la predicción del riesgo.
- **`age` (Edad)**: Clasificada en cuartiles para reflejar el riesgo asociado con la edad. Los clientes más jóvenes (Q1 y Q2) recibieron un valor de 1, indicando mayor riesgo.
- **`last_month_salary` (Salario del último mes)**: Se evaluó el salario mensual, asignando un valor de 1 solo a los clientes en el cuartil más alto (Q4), indicando menor riesgo.
- **`total_prestamos` (Número total de préstamos activos)**: Clasificada en cuartiles, con los clientes con menos préstamos (Q1 y Q2) recibiendo un valor de 1, indicando mayor riesgo.

## 3. Cálculo del Score Total

El **Score Total** se calculó sumando las variables dummies ajustadas para cada cliente, con un peso adicional en `any_delay`.

## 4. Clasificación de Clientes

Basado en el **Score Total**, los clientes fueron clasificados como "buen pagador" o "mal pagador" usando un umbral específico.

## 5. Optimización del Modelo

Se realizaron ajustes para mejorar la **sensibilidad** del modelo, aumentando el peso de la variable `any_delay`. Este ajuste resultó en una mejor identificación de los clientes con alto riesgo de incumplimiento, aunque con una ligera disminución en la especificidad.

## 6. Resultados y Conclusiones

### Matriz de Confusión (Modelo Final)

La matriz de confusión para el modelo final, que da mayor peso a `any_delay`, se muestra a continuación:

|                       | **Predicción: No Incumple** | **Predicción: Incumple** |
|-----------------------|----------------------------|--------------------------|
| **Real: No Incumple** | 27,958                     | 7,359                    |
| **Real: Incumple**    | 49                         | 634                      |

### Métricas del Modelo

- **Precisión (Accuracy)**: 79.4%
- **Sensibilidad (Recall o Tasa de Verdaderos Positivos)**: 92.8%
- **Especificidad (Tasa de Verdaderos Negativos)**: 79.2%
- **F1-Score**: 0.146

  
![matriz de confusion](https://github.com/user-attachments/assets/7c323a0c-dac1-4768-bccb-e2f5b8c1dcaf)

# Resultado

![descarga (1)](https://github.com/user-attachments/assets/274b6d51-e887-4e5a-8f6d-652a96282cfd)

  

## 7. Implementación en BigQuery

Las consultas SQL han sido implementadas en BigQuery para automatizar el cálculo del score y la clasificación de clientes en la tabla `laboratoria-426416.riesgo_relativo.tabla_real`. 

## 8. Evaluación del Modelo con Python

El siguiente código en Python fue utilizado para calcular y visualizar la matriz de confusión y las métricas clave:

```python
import numpy as np
import pandas as pd
from sklearn.metrics import confusion_matrix, accuracy_score, recall_score, precision_score, f1_score
import matplotlib.pyplot as plt
import seaborn as sns

# Verifica si las columnas necesarias están presentes
if 'Clasificacion' not in data.columns:
    raise ValueError("La columna 'Clasificacion' no se encuentra en el DataFrame.")

# Convertir la columna 'Clasificacion' a un formato numérico
# 'Mal Pagador' -> 1, 'Buen Pagador' -> 0
data['prediccion'] = data['Clasificacion'].map({'Mal Pagador': 1, 'Buen Pagador': 0})

# Asegúrate de que la columna 'default_flag' existe y es numérica
if 'default_flag' not in data.columns:
    raise ValueError("La columna 'default_flag' no se encuentra en el DataFrame.")

# Convertir ambas columnas a enteros para asegurar consistencia
data['default_flag'] = data['default_flag'].astype(int)
data['prediccion'] = data['prediccion'].astype(int)

# Calcular la matriz de confusión
matriz_confusion = confusion_matrix(data['default_flag'], data['prediccion'])

# Calcular las métricas
precision = accuracy_score(data['default_flag'], data['prediccion'])
sensibilidad = recall_score(data['default_flag'], data['prediccion'])
especificidad = recall_score(data['default_flag'], data['prediccion'], pos_label=0)
f1 = f1_score(data['default_flag'], data['prediccion'])

# Imprimir las métricas
print(f"Precisión: {precision:.4f}")
print(f"Sensibilidad (Recall): {sensibilidad:.4f}")
print(f"Especificidad: {especificidad:.4f}")
print(f"F1-Score: {f1:.4f}")

# Visualizar la matriz de confusión
plt.figure(figsize=(8, 6))
sns.heatmap(matriz_confusion, annot=True, fmt='d', cmap='Blues', cbar=False,
            xticklabels=['No Incumple', 'Incumple'], yticklabels=['No Incumple', 'Incumple'])
plt.xlabel('Predicción')
plt.ylabel('Real')
plt.title('Matriz de Confusión')
plt.show()

```
#Cálculo del Score Total:
```sql

UPDATE `laboratoria-426416.riesgo_relativo.tabla_matriz`
SET Score_Total = 
    2 * CAST(any_delay AS INT64) +  -- Doble peso para `any_delay`
    CASE 
        WHEN age BETWEEN 21 AND 41 THEN 1
        WHEN age BETWEEN 42 AND 52 THEN 1
        ELSE 0
    END +
    CASE 
        WHEN last_month_salary > 6845 THEN 1
        ELSE 0
    END +
    CASE 
        WHEN total_prestamos BETWEEN 1 AND 5 THEN 1
        WHEN total_prestamos BETWEEN 6 AND 8 THEN 1
        ELSE 0
    END;
```
# Clasificación de clientes.

```SQL 
SELECT
    *,
    CASE
        WHEN Score_Total >= 3 THEN 'Mal Pagador'
        ELSE 'Buen Pagador'
    END AS Clasificacion
FROM
    `laboratoria-426416.riesgo_relativo.tabla_matriz`;
