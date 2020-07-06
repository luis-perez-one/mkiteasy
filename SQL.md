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
   
  
