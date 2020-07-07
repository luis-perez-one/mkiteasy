#SQL - Importar y Exportar Datos

Un csv es..

##Exportar datos a un archivo .csv
```SQL
\COPY ([select_stamement]) TO '[path_completo_archivo_salida]' DELIMITER ',' CSV HEADER ;
```
Ejemplo

```SQL
\COPY 
  ( 
  FROM 
    employee 
   SELECT 
    id, last_name, first_name, department_fk AS department, monthly_salary
   WHERE
    monthly_salary > 1500
   ) 
TO '\home\ljperez\dev\employee_salary_report.csv' DELIMITER ',' CSV HEADER ;
```
