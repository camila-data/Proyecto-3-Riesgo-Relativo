### Unión de tablas 
- Se utilizó la siguiente consulta en SQL para la unión de las 3 tablas originales.

```sql
  CREATE OR REPLACE TABLE laboratoria-426416.riesgo_relativo.tabla_real AS
SELECT 
    ldu.user_id,
    ldu.more_90_days_overdue,
    ldu.using_lines_not_secured_personal_assets,
    ldu.number_times_delayed_payment_loan_30_59_days,
    ldu.debt_ratio,
    ldu.number_times_delayed_payment_loan_60_89_days,
    ldu.any_delay,
    ls.prestamo_real_estate,
    ls.prestamo_others,
    ls.total_prestamos,
    uio.age,
    uio.last_month_salary,
    uio.number_dependents,
    du.default_flag
FROM 
    laboratoria-426416.riesgo_relativo.loans_detail_update ldu
LEFT JOIN 
    laboratoria-426416.riesgo_relativo.loan_summary ls
ON 
    ldu.user_id = ls.user_id
LEFT JOIN 
    laboratoria-426416.riesgo_relativo.user_info_outliers uio
ON 
    ldu.user_id = uio.user_id
LEFT JOIN 
    laboratoria-426416.riesgo_relativo.default_update du
ON 
    ldu.user_id = du.user_id;
