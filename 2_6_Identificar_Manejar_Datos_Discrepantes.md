#  Outliers en los Datos

- Se encontraron los siguientes outliers con el método del Rango Intercuartílico (IQR)

## loans_detail.csv

- **more_90_days_overdue**: 1946 outliers
  - Porcentaje de outliers: 5.41%
- **using_lines_not_secured_personal_assets**: 177 outliers
  - Porcentaje de outliers: 0.49%
- **number_times_delayed_payment_loan_30_59_days**: 5812 outliers
  - Porcentaje de outliers: 16.14%
- **debt_ratio**: 7579 outliers
  - Porcentaje de outliers: 21.05%
- **number_times_delayed_payment_loan_60_89_days**: 1865 outliers
  - Porcentaje de outliers: 5.18%

## user_info.csv

- **age**: 10 outliers
  - Porcentaje de outliers: 0.03%
 - manejo de estos outliers: eliminar los clientes mayores a 96 años.
- **last_month_salary**: 1170 outliers
  - Porcentaje de outliers: 3.25%
  - manejo de estos outliers: imputar por el promedio los valores más altos.
- **number_dependents**: 3230 outliers
  - Porcentaje de outliers: 8.97%
 


# Detalles de Outliers en los Datos
## Boxplot de Outliers en Último Salario del Mes

Este boxplot muestra la distribución de los valores atípicos (outliers) en la columna de last month salary.

<img width="603" alt="image" src="https://github.com/user-attachments/assets/03c2b291-c696-4a8b-ab4c-b78f8e21853e">


**Observaciones:**
- Los outliers se encuentran en un rango amplio, desde justo por encima del límite de 15,650.0 hasta valores mucho más altos.
  
  ## Boxplot de Outliers en Edad

Este boxplot muestra la distribución de los valores atípicos (outliers) en la columna de `edad`.

<img width="517" alt="image" src="https://github.com/user-attachments/assets/cbd49d78-66a3-4509-adef-71730fbc5a2d">

**Observaciones:**
- La mayoría de los datos de edad se encuentran entre aproximadamente 20 y 80 años.
- Los outliers representan edades que están porn encima de 96 años.

<img width="610" alt="image" src="https://github.com/user-attachments/assets/3b0c564c-267a-4405-8f36-6e49bec13724">
<img width="548" alt="image" src="https://github.com/user-attachments/assets/495d9f0e-c4a7-462f-b5cf-16932f45cc94">

  
# Cálculo de Outliers utilizando Google Colab
Para calcular los outliers en las diferentes columnas de tus archivos CSV, se utilizó este código en Google Colab  :

```python
# Función para calcular outliers
def calcular_outliers(df, columna):
    Q1 = df[columna].quantile(0.25)
    Q3 = df[columna].quantile(0.75)
    IQR = Q3 - Q1
    lower_bound = Q1 - 1.5 * IQR
    upper_bound = Q3 + 1.5 * IQR
    outliers = df[(df[columna] < lower_bound) | (df[columna] > upper_bound)]
    return outliers


