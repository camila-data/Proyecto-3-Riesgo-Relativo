## Identificar y Manejar Datos Fuera del Alcance del Análisis

### Resultados de las Correlaciones

- **Correlación entre more_90_days_overdue y number_times_delayed_payment_loan_30_59_days:** 0.9829
- **Correlación entre more_90_days_overdue y using_lines_not_secured_personal_assets:** -0.0014
- **Correlación entre more_90_days_overdue y debt_ratio:** -0.0082
- **Correlación entre more_90_days_overdue y number_times_delayed_payment_loan_60_89_days:** 0.9922
- **Correlación entre number_times_delayed_payment_loan_30_59_days y debt_ratio:** -0.0052
- **Correlación entre number_times_delayed_payment_loan_30_59_days y number_times_delayed_payment_loan_60_89_days:** 0.9866

### Interpretación

#### Correlación muy alta:
- **more_90_days_overdue y number_times_delayed_payment_loan_30_59_days (0.9829):**
  - Estas correlaciones indican una relación muy fuerte entre estas variables. Esto sugiere que estas variables están capturando información similar sobre los retrasos en el pago de los préstamos. Podrías considerar eliminar una o más de estas variables para evitar redundancias en tu análisis.
  
- **more_90_days_overdue y number_times_delayed_payment_loan_60_89_days (0.9922)**
- **number_times_delayed_payment_loan_30_59_days y number_times_delayed_payment_loan_60_89_days (0.9866)**

#### Correlación muy baja:
- **more_90_days_overdue y using_lines_not_secured_personal_assets (-0.0014):**
  - Estas correlaciones indican que no hay una relación lineal significativa entre estas variables, por lo que pueden considerarse independientes en el contexto de este análisis.
  
- **more_90_days_overdue y debt_ratio (-0.0082)**
- **number_times_delayed_payment_loan_30_59_days y debt_ratio (-0.0052)**

#### Justificación para Retener Todas las Variables
- **more_90_days_overdue:**
  - Esta variable indica si un cliente ha estado más de 90 días vencido, lo cual es crítico para identificar posibles fondos perdidos.
  - La retención de esta variable ayuda a entender casos graves de incumplimiento.
  
- **number_times_delayed_payment_loan_30_59_days y number_times_delayed_payment_loan_60_89_days:**
  - Estas variables ayudan a identificar patrones de comportamiento de pago menos graves pero aún importantes.
  - Podrían ser útiles para segmentar clientes en diferentes niveles de riesgo y ajustar las políticas de crédito en consecuencia.

Aunque hay una alta correlación entre estas variables, es importante retenerlas todas en el análisis de crédito debido a la naturaleza crítica de la información que proporcionan sobre los retrasos en los pagos. Cada variable aporta un aspecto diferente del comportamiento de pago del cliente y puede ser vital para construir un modelo predictivo robusto.

### Consultas SQL para BigQuery

#### Correlación entre more_90_days_overdue y number_times_delayed_payment_loan_30_59_days:
```sql
SELECT 
  CORR(more_90_days_overdue, number_times_delayed_payment_loan_30_59_days) AS correlation
FROM 
  `laboratoria-426416.riesgo_relativo.loans_detail`
