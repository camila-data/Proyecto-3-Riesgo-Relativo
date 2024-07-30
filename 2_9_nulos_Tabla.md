# Identificar valores nulos en la nueva tabla 

- Se encontraron los siguientes valores nulos en la tabla `tabla_matriz`:

| Columna                                          | Nulos |
|--------------------------------------------------|-------|
| user_id                                          | 0     |
| more_90_days_overdue                             | 0     |
| using_lines_not_secured_personal_assets          | 0     |
| number_times_delayed_payment_loan_30_59_days     | 0     |
| debt_ratio                                       | 0     |
| number_times_delayed_payment_loan_60_89_days     | 0     |
| any_delay                                        | 1     |
| prestamo_real_estate                             | 425   |
| prestamo_others                                  | 425   |
| total_prestamos                                  | 425   |
| age                                              | 760   |
| last_month_salary                                | 760   |
| number_dependents                                | 760   |
| default_flag                                     | 0     |


### fórmula utilizada:


```sql
SELECT
  'user_id' AS columna, COUNTIF(user_id IS NULL) AS nulos FROM `laboratoria-426416.riesgo_relativo.tabla_matriz`
UNION ALL
SELECT
  'more_90_days_overdue' AS columna, COUNTIF(more_90_days_overdue IS NULL) AS nulos FROM `laboratoria-426416.riesgo_relativo.tabla_matriz`
UNION ALL
SELECT
  'using_lines_not_secured_personal_assets' AS columna, COUNTIF(using_lines_not_secured_personal_assets IS NULL) AS nulos FROM `laboratoria-426416.riesgo_relativo.tabla_matriz`
UNION ALL
SELECT
  'number_times_delayed_payment_loan_30_59_days' AS columna, COUNTIF(number_times_delayed_payment_loan_30_59_days IS NULL) AS nulos FROM `laboratoria-426416.riesgo_relativo.tabla_matriz`
UNION ALL
SELECT
  'debt_ratio' AS columna, COUNTIF(debt_ratio IS NULL) AS nulos FROM `laboratoria-426416.riesgo_relativo.tabla_matriz`
UNION ALL
SELECT
  'number_times_delayed_payment_loan_60_89_days' AS columna, COUNTIF(number_times_delayed_payment_loan_60_89_days IS NULL) AS nulos FROM `laboratoria-426416.riesgo_relativo.tabla_matriz`
UNION ALL
SELECT
  'any_delay' AS columna, COUNTIF(any_delay IS NULL) AS nulos FROM `laboratoria-426416.riesgo_relativo.tabla_matriz`
UNION ALL
SELECT
  'prestamo_real_estate' AS columna, COUNTIF(prestamo_real_estate IS NULL) AS nulos FROM `laboratoria-426416.riesgo_relativo.tabla_matriz`
UNION ALL
SELECT
  'prestamo_others' AS columna, COUNTIF(prestamo_others IS NULL) AS nulos FROM `laboratoria-426416.riesgo_relativo.tabla_matriz`
UNION ALL
SELECT
  'total_prestamos' AS columna, COUNTIF(total_prestamos IS NULL) AS nulos FROM `laboratoria-426416.riesgo_relativo.tabla_matriz`
UNION ALL
SELECT
  'age' AS columna, COUNTIF(age IS NULL) AS nulos FROM `laboratoria-426416.riesgo_relativo.tabla_matriz`
UNION ALL
SELECT
  'last_month_salary' AS columna, COUNTIF(last_month_salary IS NULL) AS nulos FROM `laboratoria-426416.riesgo_relativo.tabla_matriz`
UNION ALL
SELECT
  'number_dependents' AS columna, COUNTIF(number_dependents IS NULL) AS nulos FROM `laboratoria-426416.riesgo_relativo.tabla_matriz`
UNION ALL
SELECT
  'default_flag' AS columna, COUNTIF(default_flag IS NULL) AS nulos FROM `laboratoria-426416.riesgo_relativo.tabla_matriz`


