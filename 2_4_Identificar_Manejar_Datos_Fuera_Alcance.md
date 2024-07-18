## Identificar y Manejar Datos Fuera del Alcance del Análisis

### Resultados de las Correlaciones

| Variables                                                                  | Correlación    |
|----------------------------------------------------------------------------|----------------|
| more_90_days_overdue y number_times_delayed_payment_loan_30_59_days         | 0.9829         |
| more_90_days_overdue y using_lines_not_secured_personal_assets              | -0.0014        |
| more_90_days_overdue y debt_ratio                                           | -0.0082        |
| more_90_days_overdue y number_times_delayed_payment_loan_60_89_days         | 0.9922         |
| number_times_delayed_payment_loan_30_59_days y debt_ratio                   | -0.0052        |
| number_times_delayed_payment_loan_30_59_days y number_times_delayed_payment_loan_60_89_days | 0.9866         |

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
  
- **number_times_delayed_payment_loan_30_59_days y number_times_delayed_payment_loan_60_89_days:**
  - Estas variables ayudan a identificar patrones de comportamiento de pago menos graves pero aún importantes.
  - Podrían ser útiles para segmentar clientes en diferentes niveles de riesgo y ajustar las políticas de crédito en consecuencia.

