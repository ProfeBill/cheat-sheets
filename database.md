# Usando PostgreSQL con Python

## Prerrequisitos

- *Fundamental* haber leído el tutorial de SQL en https://thedataschools.com/sql.html 

- Debe tener disponible un servidor de PostgreSQL, recuerde que puede crear una cuenta gratuita en :  https://render.com/  o  https://neon.tech/ (entre muchos otros)
- Tome nota del nombre de los datos de conexión a su base de datos. en neon.tech los encontrará en el Dashboard
- En su proyecto, instale el paquete psycho2 con el siguiente comando:  

    pip install psycopg2-binary

## Creación de las tablas de municipios

1. [Crear la tabla de departamentos](https://github.com/ProfeBill/database-01/blob/90fc7003a28e0dd84a6865fd47549f721229d8d3/sql/crear-departamentos.sql)
2. [Insertar las filas para cada departamento](https://github.com/ProfeBill/database-01/blob/90fc7003a28e0dd84a6865fd47549f721229d8d3/sql/datos-departamentos.sql)
3. [Crear la tabla de municipios](https://github.com/ProfeBill/database-01/blob/90fc7003a28e0dd84a6865fd47549f721229d8d3/sql/crear-municipios.sql)
4. [Insertar los municipios en la tabla](https://github.com/ProfeBill/database-01/blob/90fc7003a28e0dd84a6865fd47549f721229d8d3/sql/datos-municipios.sql)

## Conexión

Reemplace los datos de conexion con los datos tomados de su servidor

    connection = psycopg2.connect(database="#######", user="########", password="########", host="########", port=5432)


## Para saber más

* Documentación de psycopg2
https://www.psycopg.org/docs/