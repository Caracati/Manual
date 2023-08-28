# Video 1*Levantar proyecto de forma local*
### Importante
- La versión actual de tandrify es **14.16.0**
- Al usar una versión mas nueva se muestra un error al ejecutar **ng serve** el error se muetra en el video (17:54)
  - opensslErrorStack: [error:03000006]
  - library: 'digital envelope routimes'
- Para dar solución al probelma hay que usar la ultima versión mencionada en este documento y para eso hay que utilizara nvm
- Para instalar las dependendias hay que usar npm install o npm i en la lina de comandos del proyecto
- Todos los días en la noche hay una respaldo de la base de datos, la cual va de la base de datos de producción a la base de datos de desarrollo, esto para poder tener una replica identica en dev y poder hacer las pruebas necesarias.

#### NVM
- Usando el nvm (node version manager) se puden manejar las diferentes versiones
- Hay que instalar localmente desde el enlace que se muestra en el video (32:00) que es en github la ultima version 
- Corriendo el comando en constola *nvm list* se muestran todas las versiones
- Para instalar una nueva versión desde NVM usar *nvm install +version - nvm install 14.16.0*
- Para cambiar la versión se usa el comando nvm use 14.16.0 se pude usar nvm list para revisar las que se tengan instaladas

#### CLI AWS
- La liga para descargar viene en el video en el minuto (49:52) es un enlace a AWS para poder hacer la instalación
- La principal función de este CLI es poder interactuar con los servicos de AWS mediante comandos en lugar de utilziar la interfaz gráfica de usuario
- Se puede crear cualquier recurso desde la terminal

#### CLI SAM
- SAM = Servelees Aplication Model
- Se utliza para subir solo el backend directo a AWS entre otras funciones.

#### Saber a que instancia se esta apuntando en DEV
- En angular-app - src - app - enviroments - enviroments.ts se modifica el prefijo a la instancia que quieres apuntar ya sea TIASA, CT, DEACERO



