## Pasos para generar una nueva instancia

- ### Cognito
  - Es un user pool que libera esfuerzo de la aplicación ya que ahí se maneja toda la autentificación 
  - En tandrify user pool y en app integration vienen todos los clientes que actualmente trabajan con tandrify
- ### 1 Crear cliente en cognito (2:29)
  - En el botón "Create app client"
  - Agregar el nombre del cliente
  - no se genera secreto del cliente
  - se dejan los flujos de autentificación costum auth y srp auth
  - La demas información se deja de la misma forma
- ### Configuración 
  - Es conveniente copiar de otro cliente la configuración que se tiene
  - Urls de llamadas apermitidas copiar el de la configuración existente y reemplazar el nombre por el cliente nuevo tanto para llamadas como esiones permitidas
  - En proveedores de identidad agregar congnito y microsoft
  - Tipos de concesion de oaut son el de codigo de autorización y concesión implicita
  - Amitos de OpenId Connect es email openid y profile 
  - Permisos de escritura y lectura se qeudan como en el ejemplo
  - Después de crear el cliente se debe de identficar el id del mismo
- ### DynamoDB
  - Es un servicio de base de datos NoSQL no relacional totalmente administrado ofrecido por Amazon Web Services (AWS). Se utiliza para almacenar y recuperar datos a gran escala con un rendimiento rápido y predecible
  - En tablas, y usando la tabla "TandrifyClientConfiguration" y al explorar los elementos "boton naranja" hay que agregar un nuevo registro desde crear elemento, usando el tenant que seróa el nombre de cliente en minusculas
  - Agregar un nuevo atributo de tipo string que se llame "userPoolWebClientId" y en el valor debe de ir el id que se agrego en cognito
- ## Base de datos (Querys mas abajo en el documento) (2:40)
  - Crear un rol y agregar rutas y asiganar ese rol
  - Los roles se clasifican por tenant y rol
  - La tabla frontendRoute tiene todos los roles por tenant
  - en la tabla **Role** se creo un nuevo rol llamado Developer con el tenant que es el nombre del cliente y se genera un nuevo id y ese se utilizara en el **frontendroute** utlizando el tenant también y en el roleid va el id que se genero en la tabla de role
  - En el campo name van las rutas a los modulos que se desean accesar con ese rol, si se pone ^/* se tiene permiso para todos
  - Posteriormente en la tabla **user** hay que agregar un usuario por tenant junto al correo e identificar el id que se genero 
  - Y para finalizar hay que enlazar en la tabla **userRole** el modelID que es el id que se genero en la tabla de user con el id que se genero en la tabla de role
  - 1- Agregar en role
  - 2- Agregar en frontendroute
  - 3- Agregar en user 
  - 4- Agregar en userRole
- ### Route 53
  - Es un servicio de Sistema de Nombres de Dominio (DNS) y Sistema de Nombres de Dominio Seguro (DNSSEC)
  - Dentro de hosted zones
  - En tandrify.com replicar alguno de los registros, en este caso se usó el de deacero.tandrify.com, copiando el valor/Dirigir el tafico a
  - En crear registro agregar el nombre del nuevo cliente que es el tenat, activar la casilla del alias dirigir el trafico a Alias de la distribución de cloudFront
  - y pegar el valor que se copio previamente
  - Hacer lo mismo con la api que esta en hosted zones copiando el valor de otro cliente
- ### FlushDns
  - Desde linea de comandos agregar ipconffig /flushdns para vaciar el cahce de los dns
- ### Clonar BD de prd a dev
  - Dentro de tandrify en playground y database darle clic a start cloning
- ## RDS
  - (Relational Database Service) es un servicio de bases de datos relacionales completamente administrado ofrecido por Amazon Web Services (AWS). RDS facilita la creación, operación y escalado de bases de datos relacionales en la nube sin la necesidad de administrar la infraestructura subyacente.
  - Dentro de base de datos se ve la copia que se hace al hacer la clonación borra y crea

## Registros en base de datos (usando adosa)

- Para crear los roles especifos de la instancia
```sql
select *
from tandrify.role -- 70, 71

INSERT INTO tandrify.role
(tenantId, name)
VALUES('adosa', 'Admin'),  -- 70 --REF 68
	  ('adosa', 'Planner');-- 71 --REF 65
```
- Para asignar las rutas de los roles creados
```sql
Select *
from tandrify.frontendRoute

INSERT INTO tandrify.frontendRoute
(tenantId, name, discriminator, roleId)
VALUES('adosa', '^/*', 'roleFrontendRoute', 70),
	  ('adosa', '^/demand/*', 'roleFrontendRoute', 71);
```
- Para crear los usuarios que van a utilizar la nueva interface
```sql
select *
from tandrify.user u 
where email in ('rtello@caracati.com', 'jsalinas@caracati.com','rvaldes@delphuscg.com', 'dguajardo@delphuscg.com', 'dherrera@delphuscg.com')
and tenantId = 'adosa'

INSERT INTO tandrify.user
(tenantId, email)
VALUES('adosa', 'rvaldes@delphuscg.com'), 273
('adosa', 'dguajardo@delphuscg.com'),274
('adosa', 'dherrera@delphuscg.com'),275
('adosa', 'jsalinas@caracati.com'),276
('adosa', 'rtello@caracati.com');277
```
- Para enlazar el o los usuarios creados con el rol en especifico
```sql
select *
from tandrify.userRole ur 

  - INSERT INTO tandrify.userRole
(modelId, propertyId)
VALUES(273, 70),
(274, 70),
(275, 70),
(276, 70),
(277, 70);
```


