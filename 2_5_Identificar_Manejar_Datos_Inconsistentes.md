# Análisis de Datos Inconsistentes en Variables Categóricas

## Análisis de la Variable `loan_type` en `loans_outstanding`

### Resultados

| Fila | loan_type   | count  |
|------|-------------|--------|
| 1    | other       | 268770 |
| 2    | real estate | 36560  |
| 3    | REAL ESTATE | 1      |
| 4    | Real Estate | 1      |
| 5    | OTHER       | 1      |
| 6    | Other       | 1      |
| 7    | others      | 1      |

### Resultados

| Fila | loan_type   | count  |
|------|-------------|--------|
| 1    | others      | 268773 |
| 2    | real estate | 36562  |

## Para identificar valores inconsistentes en la variable `loan_type`, se utilizó la siguiente consulta SQL en BigQuery:

```sql
SELECT
  loan_type,
  COUNT(*) as count
FROM
  `laboratoria-426416.riesgo_relativo.loans_outstanding`
GROUP BY
  loan_type
ORDER BY
  count DESC;

```sql
--para cambiar los valores inconsistentes en la variable loan_type y dejarlos en una nueva tabla
CREATE OR REPLACE TABLE `laboratoria-426416.riesgo_relativo.loans_outstanding_standar` AS
SELECT
  loan_id,
  user_id,
  CASE 
    WHEN LOWER(loan_type) = 'real estate' THEN 'real estate'
    WHEN LOWER(loan_type) IN ('other', 'others') THEN 'others'
    ELSE LOWER(loan_type)
  END AS loan_type
FROM 
  `laboratoria-426416.riesgo_relativo.loans_outstanding`;
