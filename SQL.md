# SQL 

Motor de BDD: [PostgreSQL](https://www.postgresql.org/)

## SELECT statements
### Estructura general
```SQL
SELECT
 column1_name,
 column2_name AS my new_defined_name,
  -- las columnas pueden ser re-nombradas de manera opcional
  -- no afecta a la tabla solo en el resultdo del SELECT
 column4_name,
 column7_name,
 column9_name AS city
 column11_name AS neighbourhood
 column17_name
 column18_name
 column20_name*column21_name AS total_con_impuestos
 columnN_name
 
 FROM
  table_or_view_name
  
  -- A partir de aquí todo es OPCIONAL 
  -- menos cerrar el statement con ';'
  
  -- que condiciones deben de cumplir los datos seleccionados
  WHERE
   column4_name == 'some string' AND
   column20_name IS NOT NULL AND   
   (
    column2_name <= 87.34 OR
    column7_name == True
   )
  
   -- se desea hacer la agrupación de acuerdo a
   -- alguna variable categórica?
   -- pueden existir sub-agrupaciones
   GROUP BY
    city,
    neighbourhood
   
   -- ordenar de acuerdo a una o varias columns
   ORDER BY
    column18_name,
    column17_name[DESC]
   
   ;
   ```
   
### Distintos valores de una columna
Si tuvieramos un tabla con datos de varios motores `engine` y queremos conocer los distintos valores de desplazamiento (aka_cilindrada) `displacement_cm3` que existen en la tabla, haríamos el siguiente query:
  
 ```SQL
 SELECT 
  DISTINC (displacement_cm3)
 FROM
  engine;
 ```
 ## Contar filas de una tabla
 ### Filas en general
 Opción 1, no recomendada por desempeño:
 ```SQL
 SELECT 
  COUNT (*)
 FROM
  table_or_view_name;
 ```
  
 Opción 2, contar considerando una columna que estamos seguros que contiene datos, por ejemplo la llave primaria:
 ```SQL
 SELECT
  COUNT(id)
 FROM
  table_name;
  ```
  :bulb: Puedes ampliar el statement con clausulas WHERE y ORDER BY
   
  ### Distintos valores de una o varias columna
 ```SQL
  SELECT
   COUNT(DISTINCT column3_name, column4_name)
  FROM
   table_or_view_name;
```
   :bulb: Puedes ampliar el statement con clausulas WHERE y ORDER BY

 
 ### COUNT para promedios agrupados
 ```SQL
  SELECT
   SUM(sale_import) AS total_sales
   COUNT(order_id) AS orders_qty
   SUM(sale_import) / COUNT(order_id) AS order_avg_import
   
  FROM
   sale;
   
  GROUP BY
   customer_id
  
  -- HAVING se usa para especificar una condicion que a diferencia de WHERE 
  -- aplica a *el resultado de la agrupación de filas* , no a las filas de manera individual
  
  HAVING 
    order_avg_import > 1000
    
   ;
 ```
## JOINS
`JOIN` es de los comandos más utilizados cuando trabajamos con SQL, nos permite encontrar distintos tipos de relaciones entre varias tablas de la BDD. Existen 4 tipos de `JOIN` que pueden utilizarse hasta de 6 maneras distintas:
  - `ÌNNER JOIN` es el `JOIN` más común y devuelve solo aquellas filas cuando haya una coincidencia. Sería el equivalente a usar `BUSCARV`o `VLOOUKUP` en Excel.
  
 ![PostgreSQL JOINS](https://sp.postgresqltutorial.com/wp-content/uploads/2018/12/PostgreSQL-Joins.png)
 
 Consulta [esta liga](https://www.postgresqltutorial.com/postgresql-joins/) para una explicación más profunda.
 
 ## VIEWS
 * Una vista o `VIEW` es un subconjunto de la infromación que existe en una tabla. En consecuencia pueden como una herramienta para:
    * Ayudar a concentrarnos solo en aquellas columnas (variables) de interés. 
    * Restringir el acceso a datos a cierto perfil de usuarios.
 * Pueden actuar como tablas agregadas, donde el motor de la BDD agrega la información a travres de funciones cómo (`SUM`, `AVERAGE`, `MAX`, `MIN`, etc) y presenta los resultados calculados como parte de la información. 
 * Haciendo uso de [`JOIN`](https://github.com/ljperez001/mkiteasy/blob/master/SQL.md#joins) las vistas pueden unir y simplificar tablas en una sola tabla virtual.
 * Reducir la complejidad de la información, por ejemplo una vista para `venta2001` y otra para `venta2002`particiona de manera transparente los datos subyacentes. 
  
  :point_up: [referencia](https://en.wikipedia.org/wiki/View_(SQL))
  
  *Ejemplo de un query statement para crear un VIEW*
  Considerando el siquiente esquema:
  
```SQL
CREATE VIEW v_articulo_fotografia AS

SELECT
    t4.nombre AS marca,
    t3.nombre AS sub_marca,
    t6.nombre AS solucion,
    t5.nombre AS sub_solucion,
    t1.pk AS articulo_k,
    t1.codigo_fabricante AS codigo_fabricante,
    t1.descripcion AS descripcion,
    t2.durl AS durl

FROM 
    articulo as t1
    LEFT JOIN articulo_fotografia as t2 ON t1.pk = articulo_fk
    INNER JOIN sub_marca AS t3 ON t1.sub_marca_fk = t3.pk
    INNER JOIN marca AS t4 ON t3.marca_fk = t4.pk
    INNER JOIN sub_solucion AS t5 ON t1.sub_solucion_fk = t5.pk
    INNER JOIN solucion AS t6 ON t5.solucion_fk = t6.pk


WHERE
    t1.activo = True AND
    t1.oculto_b2b = False

;
```
 
