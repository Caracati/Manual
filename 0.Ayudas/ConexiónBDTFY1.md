## Para tandrify 1

- En RDS buscar la base de datos caracatisqlserver
- En la sección de Securit grup seleccionar alguna
- En inbound rules -> Edit inboun rules
- Agregar una nueva regla con la ip de la máquina que se desea conectar


## Conexión
- Data Source={Solicitar data soruce}
- Catalog=tandrify;
- User ID={Solicitar Usuario};
- Password={Solicitar contrseña}
- La base de datos es tandrify
- Con el siguiente query se puede saber si se ejecutó la interface, par esto debe de haber mas de 300,000 registros si el siguiente query muestre resultados menores despues de las 8.00 se debe de ejecutar el get, la fecha debe de ser la fecha actual
  - SELECT count(*)  FROM [tandrify].[dbo].[AX_ib_inventory]
where transaction_date = '2023-08-01';
