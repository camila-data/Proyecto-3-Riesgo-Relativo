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
- Los outliers se encuentran en un rango amplio, desde justo por encima del límite de 15,650.0 hasta valores mucho más altos. Asi que el manejo fue imputar los datos por el promedio y la distribución se aprecia así:
- <img width="548" alt="image" src="https://github.com/user-attachments/assets/9894ec9b-6e6f-4df2-a87b-7e71d4924a75">

  
  ## Boxplot de Outliers en Edad

Este boxplot muestra la distribución de los valores atípicos (outliers) en la columna de `edad`.

<img width="517" alt="image" src="https://github.com/user-attachments/assets/cbd49d78-66a3-4509-adef-71730fbc5a2d">

**Observaciones:**
- La mayoría de los datos de edad se encuentran entre aproximadamente 20 y 80 años.
- Los outliers representan edades que están por encima de 96 años.

<img width="610" alt="image" src="https://github.com/user-attachments/assets/3b0c564c-267a-4405-8f36-6e49bec13724">
<img width="548" alt="image" src="https://github.com/user-attachments/assets/495d9f0e-c4a7-462f-b5cf-16932f45cc94">

## Boxplot de Outliers en number_dependents

![output (5)](https://github.com/user-attachments/assets/45cb86e6-427a-47a6-a224-da2a40deae91)
![output (4)](https://github.com/user-attachments/assets/415bd9a2-7119-42a1-8500-4ae9f1f99e30)

**Observaciones:**
- El histograma muestra cómo se distribuye el número de dependientes entre los clientes. La mayoría de los clientes tiene un número bajo de dependientes, con una concentración notable en valores cercanos a 0, 1 y 2.
- Sin embargo, hay algunos valores más altos que, aunque son menos frecuentes, son considerados outliers.

  
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

--  manejo more-90_days reemplaza valores mayores a 90 por un 2 en base a que el promedio de los valores sin contar los 0 es 1,7 aprox y se redondea 
CREATE OR REPLACE TABLE `laboratoria-426416.riesgo_relativo.tabla_real` AS
SELECT 
    user_id,
    CASE 
        WHEN more_90_days_overdue > 20 THEN 2 
        ELSE more_90_days_overdue 
    END AS more_90_days_overdue,
    using_lines_not_secured_personal_assets,
    number_times_delayed_payment_loan_30_59_days,
    debt_ratio,
    number_times_delayed_payment_loan_60_89_days,
    any_delay,
    prestamo_real_estate,
    prestamo_others,
    total_prestamos,
    age,
    last_month_salary,
    number_dependents,
    default_flag
FROM 
    `laboratoria-426416.riesgo_relativo.tabla_real`;

