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
- **last_month_salary**: 1170 outliers
  - Porcentaje de outliers: 3.25%
- **number_dependents**: 3230 outliers
  - Porcentaje de outliers: 8.97%


# Detalles de Outliers en los Datos
## Boxplot de Outliers en Último Salario del Mes

Este boxplot muestra la distribución de los valores atípicos (outliers) en la columna de last month salary.

<img width="603" alt="image" src="https://github.com/user-attachments/assets/408e1769-8b06-4b8a-88c8-e8ab9971ebb3">


**Observaciones:**
- Los outliers se encuentran en un rango amplio, desde justo por encima del límite de 15,650.0 hasta valores mucho más altos.

  
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


