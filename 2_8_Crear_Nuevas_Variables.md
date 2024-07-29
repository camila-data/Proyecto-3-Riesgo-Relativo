# Análisis de Préstamos y Creación de Nuevas Variables

En la tabla `loans_outstanding_standar`, tenemos: `loan_id` (ID único de préstamo), `user_id` (ID de cliente, puede repetirse), y `loan_type` ('real estate' o 'others'), esto supone un problema al unir tablas por lo que conviene Crear una nueva tabla agrupando totales por user _id : `user_id`, `prestamo_realestate`, `prestamo_others`, `total_prestamos`.

## Consulta SQL en BigQuery:

```sql
CREATE OR REPLACE TABLE `laboratoria-426416.riesgo_relativo.loan_summary` AS
SELECT
  user_id,
  COUNTIF(loan_type = 'real estate') AS prestamo_realestate,
  COUNTIF(loan_type = 'others') AS prestamo_others,
  COUNT(*) AS total_prestamos
FROM
  `laboratoria-426416.riesgo_relativo.loans_outstanding_standar`
GROUP BY
  user_id;
```

## Explicación
- Crea nueva tabla `loan_summary`
- Cuenta préstamos 'real estate' y 'others' por usuario
- Calcula total de préstamos por usuario
- Agrupa resultados por `user_id`
