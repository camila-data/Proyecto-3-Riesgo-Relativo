# Identificación y Manejo de Valores Nulos

## Resumen de Valores Nulos por Tabla

### default_data
No tiene valores nulos.

### loans_detail
No tiene valores nulos.


### user_info
- **last_month_salary**: 7,199 valores nulos.
- **number_dependents**: 943 valores nulos.

# Manejo de nulos en BigQuery

La finalidad de esta consulta es limpiar los datos en la tabla `laboratoria-426416.riesgo_relativo.user_info` sustituyendo los valores nulos en dos columnas específicas:
- `last_month_salary`: se sustituirán los valores nulos con el promedio de los salarios existentes.
- `number_dependents`: se sustituirán los valores nulos con el valor 0.


## Consultas de SQL Utilizadas 

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

### Consulta en BigQuery para sustituir Valores Nulos

CREATE OR REPLACE VIEW `laboratoria-426416.riesgo_relativo.user_info_updated` AS
-- Calcular el promedio de last_month_salary, excluyendo los valores nulos
WITH salary_avg AS (
    SELECT AVG(last_month_salary) AS avg_salary
    FROM `laboratoria-426416.riesgo_relativo.user_info`
    WHERE last_month_salary IS NOT NULL
)
-- Seleccionar todos los datos y sustituir los valores nulos en ambas columnas
SELECT 
    user_id,
    age,
    sex,
    IFNULL(last_month_salary, (SELECT avg_salary FROM salary_avg)) AS last_month_salary,
    IFNULL(number_dependents, 0) AS number_dependents
FROM 
    `laboratoria-426416.riesgo_relativo.user_info`;


