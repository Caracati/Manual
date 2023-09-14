## Reinicio pasa

### Situación
- Actualmente se cuenta con el cliente pasa el cual esta utilizando la versión 1 de tandrify, se ha detectado que por alguna razón la aplicación deja de funcionar y no es posible utilizar la aplicación, actualmente esta situación se detectaba hasta que el cliente de pasa se daba cuenta y notificaba vía correo.
- Para corroborar la desconexión se puede ingresar a [Tandrify1](https://pasa.tandrify.com/auth.html) en donde se mostrará un error en la pagina

### Solución
- Para dar soporte a esto se debe de realizar el reinicio del servidor de pasa que se encuentra en **EC2** y la instancia de pasa que esta en **Elastic Beanstalk**
- Se encontró una forma de estar monitoreando mediante peticiones el estatus de la aplicación y se está registrando en un log las respuetas de dichas peticiones, con esto se prentende que de forma manual, se haga el reinicio el cual se explica a continuación, de igual forma se piensa automatizar dicha tarea, acutualmente se hace a las 6:00 am de forma manual

### Pasos de reinicio
- ### EC2 (Paso uno)
  - Entrar a Instancies (running)
  - Dar click en la instancia de PASA (Instancie ID)
  - En Instance state - Reboot instance
  - Esprar unos segundos en lo que se reinicia

- ### Elastic Beanstalk (Paso dos)
  - Ingreasr a la instancia de PASA que deberá de estar en rojo en el campo de Health
  - En Actions - Restart app server(s)
  - Esperar de 10 a 20 minutos en lo que se reinicia
  - Para corroborar el reinicio correcto Ingresar de nuevo a [Tandrify1](https://pasa.tandrify.com/auth.html) donde se deberá de mostrar el login de la aplicación

- ### Carga de inventario (Paso tres opcional)
  - Es necesario corroborar que la carga del inventario se hizo de forma correcta
  - Esta carga se tiene planeada se ejecute de 6:30 am  a 7:00 am
  - Por lo que es necesario validar dentro de la base de datos dicha carga de forma correcta para poder realizar esto es necesario realizar la consulta en la base de datos de Tandrify1 la cual se encuentra en este mismo documento en la sección de **Conexión**
  - Si al realizar la consulta con la fecha actual el valor del conunt es mucho menor a los 300,000 se puede entender que la carga no fue exitosa y se debe de ejecutar una petición a las siguientes URLS
    - pasa.tandrify.com/api/CronJob/{Solicitarid}
    - pasa.tandrify.com/api/CronJob/{Solciitarid}
  - Para obtener el valor de dicho get 
    - Desde cloud watch se saca el id del cient desde las reglas (Rules)
    - En IntefacePasaMx - Targets - Input (Constant) el valor de compantyId es el valor que corresponde a la url
    - La lambda se llama TandrifyInterface
  
## Conexión
- Data Source={SolicitarCadena};
- User ID={SolicitarUsuario};
- Password={SolicitarContraseña}
- La base de datos es tandrify
- Con el siguiente query se puede saber si se ejecutó la interface, par esto debe de haber mas de 300,000 registros si el siguiente query muestre resultados menores despues de las 8.00 se debe de ejecutar el get, la fecha debe de ser la fecha actual
```sql
SELECT count(*)  FROM [tandrify].[dbo].[AX_ib_inventory]
WHERE CONVERT(DATE, transaction_date) = CONVERT(DATE, GETDATE());
```
- en caso de haaber menos de 300 ejecutar 
```sql
-- DELETE FROM [tandrify].[dbo].[AX_ib_inventory]
WHERE CONVERT(DATE, transaction_date) = CONVERT(DATE, GETDATE());
```