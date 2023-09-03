# Como resetear una instancia ya creada
- Tomar en cuenta que al borrar demandResult hay que hacerlo por lotes esto para evitar que al ser muchos registros que borrar, genere algun probelma y no borre al intentar hacerlo dentro de una transacción 

- DemandResult es la tabla donde vienen los consumos, venta y demandas

- el orden para hacer el borrado de la información sería 
  - DemandResult
  - Product
  - Location

Para obtener el model id se debe de utilizar el query

```sql
select *
from demandSetting 
where tenantid = '{nombre del tenent}'
```

### Querys para hacer el borrado

```sql 
delete from demandResult where modelid = {modelid} limit 10000

delete from product where tenantid = '{nombre del tenant}' limit 10000

delete from location where tenantid = '{nombre del tenant}'
```

Validar si se desea quitar por completo la información, de ser asi validar las siguientes tablas

```sql
select *
from productAttributeField paf 
where tenantId = '{nombre del tenant}';

select *
from abcSetting as2
where tenantId = '{nombre del tenant}'

select *
from historySetting as2
where tenantId = '{nombre del tenant}'

select *
from filterSetting as2
where tenantId = '{nombre del tenant}'

select *
from demandSetting
where tenantid = '{nombre del tenant}'
```