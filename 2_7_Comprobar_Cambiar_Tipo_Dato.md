## Cambiar Tipo de Dato 

Cambio del tipo de dato de la columnas creadas (que se detallan en el siguiente punto). 


### 1. Creación de una tabla con el esquema deseado

Convertir columnas específicas de tipo FLOAT a INT64 de la tabla. Las columnas convertidas son prestamo_real_estate, prestamo_others y total_prestamos.

-- Crear una nueva tabla con las columnas convertidas a enteros
CREATE OR REPLACE TABLE `laboratoria-426416.riesgo_relativo.tabla_matriz` AS
SELECT
  CAST(prestamo_real_estate AS INT64) AS prestamo_real_estate,
  CAST(prestamo_others AS INT64) AS prestamo_others,
  CAST(total_prestamos AS INT64) AS total_prestamos,
  -- Incluye todas las demás columnas sin cambios
  more_90_days_overdue,
  using_lines_not_secured_personal_assets,
  number_times_delayed_payment_loan_30_59_days,
  debt_ratio,
  number_times_delayed_payment_loan_60_89_days,
  any_delay,
  age,
  last_month_salary,
  number_dependents,
  default_flag
FROM
  `laboratoria-426416.riesgo_relativo.tabla_matriz`;
