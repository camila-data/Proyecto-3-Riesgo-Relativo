# Identificación y Manejo de Valores Duplicados

## Resumen de Duplicados por Tabla

### default_data
0 duplicados.

### loans_detail
0 duplicados.

### loans_outstanding
0 duplicados.

### user_info
0 duplicados.

## Consulta en BigQuery para Identificar Duplicados

Para identificar registros duplicados en la tabla `default` basados en el `user_id`, se utilizó la siguiente consulta en BigQuery:

```sql
-- Identificar registros duplicados en la tabla default basados en user_id
SELECT
    user_id,
    COUNT(*) AS count_duplicates
FROM
    `laboratoria-426416.riesgo_relativo.default`
GROUP BY
    user_id
HAVING
    COUNT(*) > 1;
