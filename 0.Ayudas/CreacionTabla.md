## Crear un tabla en Tandrify
- Todos los cambios de la base de datos se van quedando en el repositorio
- Estos cambios están en data-models y models
- La forma de crear la clase es en base a entity framework
- Ventajas de EntityFramework
  - Te puedes regresar a una versión anterior
  - Se puede volver a recrear de forma mas sencilla, al tener toda la definición Single sorce of true, ultimo punto de verdad
- Casi todas las clases heredan de ciertos modelos
- La clase de tentan model, deben de estar con tenant id

## Creación de tabla
- Se deben de crear una carpeta en donde se debe de agregar la información que se desea agregar
- Las propiedades se deben de poner con minusculas, ya que las clases se conviernten a JS
- Las clases no deben de ser abstractas
- Dentr de la carpta de **Data** en el archivo **TandrifyContext** se debe de declarar 
- ## Terminal
  - Hay que tener putty ejecutandose
  - y hay que tener el archivo Program.cs
  - Se puede tener un servicio de AWS que se llama secret manager par poder tener las contraseñas en dicho servicio
  - El archivo Program.cs debe de ir en la carpta de Data-models - Tandrify 
  - Para ejecutar dichos comandos hay que estár en data-modles/Tandrify
  - Ejecutar el comando **dotnet ef migration add "nombre de tabla"** para crear el archivo de migración para poder crear la tabla
  - Al ejecutar el comando de forma correcta se crean 2 metodos UP y DOWN para poder regresar en el tiempo 
  - Para agregar la tabla a la base de datos se debe de ejecutar el comando **dotnet ef database update**
  - Es necesario validar el puerto al que apunta la conexión de la base de datos
  - El puerto 3308 ya que si se tiene instalado el mySql ya tiene este puerto, por loq ue se pasa al 3307 para que no se ocupe el puerto 3308
  - ## modificar tabla
    - No es recomendable utilizar booleanos, ya que al convertirlo a JS que lo pone como decimal por lo que es mejor usar int para que sea 0 o 1.
    - se debe de agregar a la migración con **dotnet ef migration add "nombre de tabla + Descripcion"** ej **dotnet ef megration add CatVidas** este nombre es el que se guarda en la carpeta de migraciones
    - Para actualizar usar **dotnet ef database update**
## Resumen de creación de tabla
- Crear la carpeta contenedora
- Crear la clase con las propiedades necesarias
- Crear los indices en data-models\Tandrify\Data\TandrifyContext.cs
- ejecutar **dotnet ef migrations add {nombre}** para agregar en la migración
- Ejecutar **dotnet ef migrations script {{MigraciónPreviaALaAtual}}** para generar el script en cuestión hay que modificar la migarción por la migración previa a la que se hizo actualmente, desde data-models/Tandrify esto generará un script parecido a esto, Validar que el script cumpla con lo que se realizó, deberá de ser el nombre de la clase antes de la migración de alrchivo cs
  - ALTER TABLE `aliasRule` ADD `expirationDate` datetime(6) NULL;

    INSERT INTO `__EFMigrationsHistory` (`MigrationId`, `ProductVersion`)
    VALUES ('20231114210412_AliasRuleExpirationDateAdd', '3.1.5');
- En caso de que se quiera hacer en automatico desde el comando ejecutar la siguiente linea (NO HACERLO)
  - Ejecutar **dotnet ef database update {nombreoajuste}** para que el ajuste se vea reflejado en la base de datos
- Para finalizar es necesario ejecutar el comando **gulp** desde data-models/model-exporter para que se haga la transaforamcion a typescript y posterior a js para luego pasarlos a la carpeta correspondiente validar puerto correcto para dev o prd ejemplo secret.port = '3308' se puede valildar desde putty o desde DBeaver o Workbeanch
- Desde layers de sam app ejecutar el npm run publish-dev para subir los cambios en especifico
- Posterior a la publicación validar que en Lambda - function - tfy-dev-basicCrud-Crud....(en prd se omite dev) - edit layers y que TandrifyEntitesLayerDev tenga la ultima version del layer (hay otras layers que modificar para que esto pueda funcionar, como la carga masiva tfy-dev-enginesettingsreceived-DataReceived )
- Al terminar es necesario dentro de sam app y layers abrir una terminar y ejecutar npm run publish-dev

## Gulp
- Es necesario tener python
- Es necesario tener el archivo de configuración de gulp
- Este archivo se ignora dentor del git ignore
- Crea 2 carptas, models y exports
  - en models primero los convierte a TS
  - en exports a JS
  - Los cambia de carpeta

## Eliminar migración
- Es posible eliminar una migración con el comando dotnet ef migrations remove esto desde data-models/Tandrify
  - Esto eliminará la ultima migración tender en cuenta que si la migración ya fue aplicada en la bd se deberá de borrar de la tabla 
    - select * from __EFMigrationsHistory
  - Posterior eliminar loq ue se haya realizado en la tabla correspondiente