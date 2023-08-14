## Como agregar una nueva linea de demanda
- Las linas de demanda son ...

### Para agregar una linea de demanda es necesario agregarla en la base de datos en la tabla tandrify.demandSetting
- select * from tandrify.demandSetting where tenantId = 'amparts'
- el orden 

Base de datos
En la tabla demandSettings se da de alta con el nuevo nombre, ya se hizo el ejemplo para amparts con el id 41 y 45


## Codigo
- En sam app tentants generic inteface sale en app, dentro de la funcion de getModel, aquí se determina lo de las lineas de demanda utilizando el switch se puede tomar el ejemplo de farmacias del ahorro o de amparts, en esto código se determina como debe de finalizar el archivo para hacer la carga con la linea de demanda correcta.


