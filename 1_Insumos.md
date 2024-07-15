# Insumos

Este conjunto de datos contiene información sobre préstamos concedidos a un grupo de clientes del banco "Super Caja". Los datos se dividen en cuatro tablas:

1. **user_info**: Datos del usuario/cliente.
2. **loans_outstanding**: Datos del tipo de préstamo.
3. **loans_detail**: Comportamiento de pago de estos préstamos.
4. **default**: Identificación de clientes morosos.

si quieres un vistazo puedes haz aquí  [enlace dataset](https://drive.google.com/file/d/1BbQHMdlIVh_wQrjFp50qa2036ai2CA-W/view). 

A continuación, se presenta la descripción de las variables que componen las tablas de este conjunto de datos:

### user_info
| Archivo   | Variable                  | Descripción                                           |
|-----------|---------------------------|-------------------------------------------------------|
| user_info | user_id                   | Número de identificación del cliente (único para cada cliente) |
|           | age                       | Edad del cliente                                      |
|           | sex                       | Sexo del cliente                                      |
|           | last_month_salary         | Último salario mensual reportado al banco             |
|           | number_dependents         | Número de dependientes                                |

### loans_outstanding
| Archivo           | Variable      | Descripción                                           |
|-------------------|---------------|-------------------------------------------------------|
| loans_outstanding | loan_id       | Número de identificación del préstamo (único para cada préstamo) |
|                   | user_id       | Número de identificación del cliente                  |
|                   | loan_type     | Tipo de préstamo (real estate = inmobiliario, others = otro) |

### loans_detail
| Archivo         | Variable                                      | Descripción                                                                 |
|-----------------|-----------------------------------------------|-----------------------------------------------------------------------------|
| loans_detail    | user_id                                       | Número de identificación del cliente                                        |
|                 | more_90_days_overdue                          | Número de veces que el cliente estuvo más de 90 días vencido                |
|                 | using_lines_not_secured_personal_assets       | Cuánto está utilizando el cliente en relación con su límite de crédito en líneas no garantizadas con bienes personales, como inmuebles y automóviles |
|                 | number_times_delayed_payment_loan_30_59_days  | Número de veces que el cliente se retrasó en el pago de un préstamo (entre 30 y 59 días) |
|                 | debt_ratio                                     | Relación entre las deudas y el patrimonio del prestatario. Ratio de deuda = Deudas / Patrimonio |
|                 | number_times_delayed_payment_loan_60_89_days  | Número de veces que el cliente retrasó el pago de un préstamo (entre 60 y 89 días) |

### default
| Archivo | Variable       | Descripción                                             |
|---------|----------------|---------------------------------------------------------|
| default | user_id        | Número de identificación del cliente                    |
|         | default_flag   | Clasificación de los clientes morosos (1 = clientes que pagan mal, 0 = clientes que pagan bien) |

