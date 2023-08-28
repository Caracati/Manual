# Conectar AWS s3 con Knime
## Objetivo
- Conectar la herramienta knime con los buckets de S3 de AWS.
## Requisitos
- Tener instalado knime en su ultima version
- Dentro de kinme es necesario tener extensiones para poder utilizar los nodos de AWS

## Configuracion Knime
- Dentro de la herramienta KNIME 
  - File
    - Install KINME extension (dentro del buscar teclear amazon o AWS)
    - Seleccionar las opciones como **KNIME Amazon Cloud Connector**

## Como utilizar los conectores
- Es necesario tener las credenciales de acceso que se utilizan en AWS
- Dentro de los nodos a utilizar es posible buscar amazon y el primer nodo a utiliar para autenticar es el nodo
  - Amazon Authenticator
    - Seleccionar el Acces Key Id and Secrete Key
      - Agregar las credenciales (Realizar pureba de conexión) 
  - Amazon S3 Connector
    - En este nodo se debe de especificar el directorio del cual se requiere obtener los archivios /nombre_del_directorio/carpeta (*Este directorio debe de pertenecer a la llave y secreto creado con aterioridad*)
  - File Reader (Solo se usa para la explicación)
    - Al tener la configuración realizada dentro de este nodo ya será posible obtener todos los archivos que se cuentan en el bucket para poder hacer el uso que se necesite.
