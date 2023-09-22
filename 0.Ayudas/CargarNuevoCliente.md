# Carga de nuevo cliente ejemplo con adosa
- Crear linea o lineas de demanda en la siguiente tabla
```sql
select * from tandrify.demandSetting where tenantId = 'adosa' -- da 46 la cual se usrará para el count y validar que se haya cargado bien la demanda
```

- Validar los archivos que se mandan para ver los nombres y agregarlos en lo catálogos
### Ejemplo de productos

![Alt text](Assets/image.png)

### Ejemplo de ubicaciones
- En este cliente se mandaron solo code y description por los que todos los atributos van apagados, si se llegan a enviar otros atributos estos se deben de crear como el ejemplo de productos

## Ajustes en codigo
- Se hicieron ajustes en esta parte del codigo para agergar los diccionarios y también la parte de la carga de consumo

 - .../interface/common/dictionaries/demand.js  
 - .../interface/common/dictionaries/locations.js    
 - .../interface/common/dictionaries/products.js     
 - .../tenants/generic/interface/sale/app.js  
  
- Al tener esta información capturada en los catálogos y los ajustes en el codigo, se deben de subir los archivos en el directorio del bucket de s3 correspondiente en este caso tfy-interfaces-inboundbucket/adosa/ tanto para ubicaciones como productos y consumo

## Carga de consumos
- En este caso en la carga inicial se cargan todos los archivos de golpe
- Para validar la carga 

```sql
  select count(*) from demandResult dr where modelId = 46
```

