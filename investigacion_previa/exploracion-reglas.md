# Exploración Inicial de los Datos (`transacciones.csv`) con Pandas

## _Tipos de datos_

#### Analizando los tipos que posee cada campo, podemos observar que la mayoría de campos son de tipo `str`, esto podría suponer un problema por las siguientes razones:

- Un campo como `monto` debería ser de tipo númerico.
- Un campo como `fecha_hora` debería ser de tipo fecha (date).

#### Una posible solución para esto sería convertir los valores de estas columnas a sus correctos tipos, respectivamente.

---

## _Formato de Texto_

#### Analizando los valores únicos de los campos, podemos observar las siguientes inconsistencias:

- `moneda`:
  - Mismos valores repetidos, en mayúsculas y minúsculas.
  - Ejemplo: `ars` y `ARS`.
- `tipo`:
  - Mismos valores repetidos, en mayúsculas y minúsculas.
  - Espacios en blanco, al principio y al final de los valores.
  - Ejemplo: ` EXTRACCION` y `extraccion`

#### Una solución para esto sería sanitizar y estandarizar el formato de los textos en las columnas, eliminando espacios en blanco y eligiendo que los valores estén escritos o todos en mayúsculas o todos en minúsculas.

---

## _Duplicados_

#### Analizando el campo `id_transaccion`, podemos detectar la cantidad de _75_ valores duplicados. Esto es un problema ya que los datos de esta columna deben ser _identificadores únicos_ para cada registro que representa una transacción.

#### Una posible solución en este caso sería tratar identificar y salvaguardar los registros con IDs repetidos, asignandoles IDs únicos.

---

## _Valores nulos_

#### No se detectaron valores nulos existentes en los campos.

---

## _Formato de Fecha_

#### Analizando la cantidad de valores por formato de fecha en el campo `fecha_hora`, podemos observar los siguientes resultados:

- Existen _2316_ valores que utilizan un tipo de formato de fecha _YYYY-mm-dd_.
- Existen _259_ valores que utilizan un tipo de formato de fecha _dd/mm/YYYY_.

#### Esto supone un problema ya que no es ideal para un campo como `fecha_hora` que sus valores difieran en formato.

#### En este caso, la solución sería estandarizar el formato para todos los valores de la columna al tipo correspondiente indicado por la empresa (_YYYY-MM-DD hh:mm:ss_).

---

## _Rango de Valores Númericos_

#### Realizando la evaluación de valores mínimos, máximos y menores a cero, se llegó a estos resultados con respecto a los siguientes campos:

- `monto`:
  - Se halló que el valor mínimo dentro de este campo es de _-898513.02_. Esto supone un problema, ya que un campo númerico que contiene _montos_ de transacciones no puede contener valores númericos negativos. La empresa especifica que los valores del campo `monto` deben ser mayores a 0.

- `id_cuenta`: No se encontraron valores númericos negativos.
- `id_sucursal`: No se encontraron valores númericos negativos.
- `id_transaccion`: No se encontraron valores númericos negativos.

#### La solución en este caso sería identificar los registros del campo `monto` con valores menores a cero y descartarlos hacia una tabla de rechazados, donde se tratará de limpiar los datos posibles.

## _Conclusión_

### En este archivo markdown se remarcó, a raiz de una investigación previa de la fuente de datos, inconsistencias específicas por campos y las posibles soluciones/validaciones a implementar posteriormente en nuestro proceso ETL.
