# SQL 

## Query example

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
 columnx_name
 
 FROM
  table
  
  -- A partir de aquí todo es OPCIONAL 
  -- menos cerrar el statement con ';'
  
  -- que condiciones deben de cumplir los datos seleccionados
  WHERE
   column4_name == 'some string' AND
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
