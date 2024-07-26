## Identificar y Manejar Datos Fuera del Alcance del Análisis

### Resultados de las Correlaciones

| Variables                                                                  | Correlación    |
|----------------------------------------------------------------------------|----------------|
| more_90_days_overdue y number_times_delayed_payment_loan_30_59_days         | 0.9829         |
| more_90_days_overdue y using_lines_not_secured_personal_assets              | -0.0014        |
| more_90_days_overdue y debt_ratio                                           | -0.0082        |
| more_90_days_overdue y number_times_delayed_payment_loan_60_89_days         | 0.9922         |
| number_times_delayed_payment_loan_30_59_days y debt_ratio                   | -0.0052        |
| number_times_delayed_payment_loan_30_59_days y number_times_delayed_payment_loan_60_89_days | 0.9866    

<img width="664" alt="image" src="https://github.com/user-attachments/assets/0b7c2e57-ecbb-47ad-a414-899c79ec4f98">

### Interpretación

#### Correlación muy alta:
- **more_90_days_overdue y number_times_delayed_payment_loan_30_59_days (0.9829):**
- **more_90_days_overdue y number_times_delayed_payment_loan_60_89_days (0.9922)**
- **number_times_delayed_payment_loan_30_59_days y number_times_delayed_payment_loan_60_89_days (0.9866)**

#### Correlación muy baja:
- **more_90_days_overdue y using_lines_not_secured_personal_assets (-0.0014):**
  - Estas correlaciones indican que no hay una relación lineal significativa entre estas variables, por lo que pueden considerarse independientes en el contexto de este análisis.
  
- **more_90_days_overdue y debt_ratio (-0.0082)**
- **number_times_delayed_payment_loan_30_59_days y debt_ratio (-0.0052)**

#### En este se deben retener Todas las Variables
- **more_90_days_overdue:**
  - Esta variable indica si un cliente ha estado más de 90 días vencido, lo cual es crítico para identificar posibles fondos perdidos.
  - La retención de esta variable ayuda a entender casos graves de incumplimiento.
 

### Eliminación de la Columna `sex` 

Eliminar la columna `sex` de la tabla `user_info_updated` ya que el sexo de los clientes no es relevante para este análisis. 

**Proceso:**
1. **Eliminación de la Columna `sex`**:
    - Se utiliza la instrucción `CREATE OR REPLACE TABLE` para crear una nueva tabla sin la columna `sex`.


### Consulta SQL Utilizada

**Eliminación de la Columna `sex`**:
```sql
CREATE OR REPLACE TABLE `laboratoria-426416.riesgo_relativo.user_info_updated_no_sex` AS
SELECT
  user_id,
  age,
  last_month_salary,
  number_dependents
FROM
  `laboratoria-426416.riesgo_relativo.user_info_updated`;
