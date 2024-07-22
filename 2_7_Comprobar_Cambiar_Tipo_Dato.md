## Cambiar Tipo de Dato 

Cambio del tipo de dato de la columna `default_flag` de `INTEGER` a `BOOLEAN` en la tabla `default`.


### 1. Creación de una nueva tabla con el esquema deseado
Se creó una nueva tabla `default_update` con el mismo esquema que la tabla original `default`, pero con la columna `default_flag` definida como `BOOLEAN`.

```sql
CREATE TABLE laboratoria-426416.riesgo_relativo.default_new AS
SELECT
  user_id,
  CAST(default_flag AS BOOLEAN) AS default_flag
FROM
  laboratoria-426416.riesgo_relativo.default;
