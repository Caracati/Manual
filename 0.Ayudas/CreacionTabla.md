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
- ejecutar **dotnet ef migration add {nombre}** para agregar en la migración
- Ejecutar **dotnet ef database update {nombreoajuste}** para que el ajuste se vea reflejado en la base de datos

## Gulp
- Es necesario tener python
- Es necesario tener el archivo de configuración de gulp
- Este archivo se ignora dentor del git ignore
- Crea 2 carptas, models y exports
  - en models primero los convierte a TS
  - en exports a JS
  - Los cambia de carpeta
  - 