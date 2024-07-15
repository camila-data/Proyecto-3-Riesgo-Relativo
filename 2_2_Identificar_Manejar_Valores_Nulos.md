# Identificación y Manejo de Valores Nulos

## Resumen de Valores Nulos por Tabla

### default_data
No tiene valores nulos.

### loans_detail
No tiene valores nulos.

### loans_outstanding
No tiene valores nulos.

### user_info
- **last_month_salary**: 7,199 valores nulos.
- **number_dependents**: 943 valores nulos.
- Otros campos no tienen valores nulos.

## Consulta en BigQuery para Encontrar Valores Nulos

Para contar los valores nulos en cada campo de la tabla `user_info`, se utilizó la siguiente consulta en BigQuery:

```sql
-- Contar valores nulos para cada campo en user_info dentro del proyecto riesgo relativo
SELECT
    COUNTIF(user_id IS NULL) AS null_user_id,
    COUNTIF(age IS NULL) AS null_age,
    COUNTIF(sex IS NULL) AS null_sex,
    COUNTIF(last_month_salary IS NULL) AS null_last_month_salary,
    COUNTIF(number_dependents IS NULL) AS null_number_dependents
FROM
    `laboratoria-426416.riesgo_relativo.user_info`;
