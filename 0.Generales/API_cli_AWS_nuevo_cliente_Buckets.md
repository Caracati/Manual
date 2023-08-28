# Video 2 *Generacion API cli AWS y nuevo cliente accesos a buckets*
### Importante
- El objetivo de este video es crear una api pero usando la consola, no la interface de AWS
- Dentro de cada carpeta que se encuentra en tandrify sam app hay un yml con la api y las lambdas que se utilizarn, de igual forma hay carpetas con los js que están en node para poder crear la lambda
- En este archivo yml, en la sección de globals esta toda la configuracion de todas las funciones lambda que se creen en ese template

### Creación de api desde consola
- Asignar permiso a usuario desde la interface, creando un access y secret key para poder usar el cli, esto se hace desde IAM, buscando el usuario y en credenciales de seguridad se deben de crear unas claves de acceso esto viene en (4:21)
- Dentro de consola teclear **aws configure** y agregar la información de la llave que se descargó 
- Desde el min (12:00) se explica como crear la api
- Al crear una api nueva tambien hay que declararla en common esto viene en el min (24:45)
- Lo maximo que puede correr una función lambda son 15 minutos
- Revisar todas las propiedades que se les pueden poner a una función lambda https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/sam-resource-function.html
- Es necesario que la veresión de node sea 14, esto al mover una lambda.

### LogsCloudWatch
- Todas las funciones lambda que se corran se van a ir a un log del cloudwatch en gurpo de registros 
- para poder agregar algun registro en log con poner console.log("texto"); se guarda dentro del cloudwatch buscnado poe el nombre de la lambda creada

### Desplegar en DEV
- Existe un pipiline en aws, codepipeline donde se ven los pasos que se realizó en el despligue
- en compilación y proeyctos de compilación hay 2 proyectos uno de pruebas y otro de producción y para que esto corra en dev debe de tener el prefijo dev en la rama que se tiene ejemplo "dev_cambiorealizado".
- Si se está en una rama y se quiere cambiar de rama con los cambios ya hechos hay que usar git checkout -b devCambiosRealizados
- Con esto se puede hacer el commit para que el cambmio se detectue y se suba al ambiente de desarrollo
  
### Progreso de despligue
- En codeBuild en proeycto de compilación se pueden ver todos los estados de cada una de las compilaciones, esto se usa para saber en que estado esta la compilación
- Dentro del código hay archivos yml duildspec_dev y buildspec los cuales tienen las fases que se genera para hacer el despligue en dev o prd segun sea el caso.
- El proceso para hacer la publicación a producción es necesario hacer un merge a la rama master y luego hacer el push para que de igual forma, se suban los cambios automaticamente.

### Amarrar la api creada para verla en el front
- dentro del codigo hay un archivo yml template, el cual tiene todas las apis creadas dentro del codigo, y será necesario agergarla aquí para que se pueda consmir 
- **Para poder encontrar el código en el back end**
  - Desde la aplicación ya corriendo, se puede entrar a red desde el inspector, y buscar las rutas que se utilizan y dentro de esa ruta debería de venir el BasePath que se pone en el yamel, y con esto se puede identificar cual es la lambda que se esta utilizando
  - Con esto se ubica el stack que es el nombre que se le da a la carpeta y en el yaml viene como nombreCarpetaMapping "ExpensesMapping"
  - Para el template de pruebas hay que utilizar otra ruta en el codigo en la carpeta dev en sam app y en dev mappings
  - NOTA: El nombre del stack es el nombre de la carpeta contatendao con mapping como se menciono lineas arriba. esto es por orden ya que puede ir cualquier otro nombre. (min 1:27)
  - NOTA: Las funciones lambda se despliegan directo a aws
  - Los templats de dev y el de prd deben de estar espejeados 
  - Dentro de los archivos app.js vienen las importancies del sdk de tandrify y también del orm en la mayría de estos en donde el sdk trae todas las herrameintas para poder hacer uso del mismo y en el orm trae la funcionalidad para poader hacer uso de la base de datos

### Invalidar usuario
- Dentro de IAM, buscar el usuario, luego en credenciales de seguridad y en claves de acceso se ven todas las claves que se han generado, y solo hay que desactivarla y eliminarla

### Ventajas de serveless
- No hay que mantener el sistema operativo, ni pareches ni segurdiad
- Cada que se ejecuta una funcion AWS toma un servidor disponible, agrega un contendor y en ese contenedor corre la función lambda, lo que hace que muchos usuarios puedan consumir la misma función pero al tener esta distribución la función responde de forma muy rápida
- Todo el conteneido estatico se le quita al servidor, esta en un bucket, la aplicación se encarga del backend y en S3 se mantiene el front end, con esto se permite que se mas escalable

### Cliente nuevo (instancia)
- ## Cognito
- Es un user pool que libera esfuerzo de la aplicación ya que ahí se maneja toda la autentificación 
- En tandrify user pool y en app integration vienen todos los clientes que actualmente trabajan con tandrify
- ## 1 Crear cliente en cognito (2:29)
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
- ## DynamoDB
- Es un servicio de base de datos NoSQL no relacional totalmente administrado ofrecido por Amazon Web Services (AWS). Se utiliza para almacenar y recuperar datos a gran escala con un rendimiento rápido y predecible
- En tablas, y usando la tabla "TandrifyClientConfiguration" y al explorar los elementos "boton naranja" hay que agregar un nuevo registro desde crear elemento, usando el tenant que seróa el nombre de cliente en minusculas
- Agregar un nuevo atributo de tipo string que se llame "userPoolWebClientId" y en el valor debe de ir el id que se agrego en cognito
- ## Base de datos (2:40)
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
- ## Route 53
- Es un servicio de Sistema de Nombres de Dominio (DNS) y Sistema de Nombres de Dominio Seguro (DNSSEC)
- Dentro de hosted zones
- En tandrify.com replicar alguno de los registros, en este caso se usó el de deacero.tandrify.com, copiando el valor/Dirigir el tafico a
- En crear registro agregar el nombre del nuevo cliente que es el tenat, activar la casilla del alias dirigir el trafico a Alias de la distribución de cloudFront
- y pegar el valor que se copio previamente
- Hacer lo mismo con la api que esta en hosted zones copiando el valor de otro cliente
- ## FlushDns
- Desde linea de comandos agregar ipconffig /flushdns para vaciar el cahce de los dns
- ## Clonar BD de prd a dev
- Dentro de tandrify en playground y database darle clic a start cloning
- ## RDS
- (Relational Database Service) es un servicio de bases de datos relacionales completamente administrado ofrecido por Amazon Web Services (AWS). RDS facilita la creación, operación y escalado de bases de datos relacionales en la nube sin la necesidad de administrar la infraestructura subyacente.
- Dentro de base de datos se ve la copia que se hace al hacer la clonación borra y crea
  
 ### Acceso a Bucket (3:04)
- Dentro de consola en S3 buscar el bucket que se desea agregar
- En IAM crear un nuevo rol que sea con cuenta de AWS y en siguiente
- Crear politica y en servicio agregar s3 para darle esos permisos 
- dentro de acciones darle permisos de lectura y escritura
- En recursos en buket agregar el nombre del s3 y en objetc agragrlo de igual forma
- Generar un nombre al bucket, de preferencia poner descripción 
- Seleccionar la politica y agregar el nombre del Rol
- Hay que agregarle los permisos al usuario crando un grupo nuevo y agregarle el acceso del bucket nuevo al usuario
- Para agregar mas persmoso es desde las politicas