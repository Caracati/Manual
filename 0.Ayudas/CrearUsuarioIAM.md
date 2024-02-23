# Crear usuario en AWS con IAM
## Politicas
- Antes de generar el usuario es necesario generar una politica la cual tendrá los permisos para el usuario, en este ejemplo se agrega los permisos necesarios para que el usuario tenga permisos a un bucket de s3
- Entrar a IAM
- En el panel de navegación izquierdo, selecciona "Policies" y luego "Create policy". 
- En la página "Elegir un servicio", seleccionar "JSON" para crear una política personalizada mediante JSON.
```
  {
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "s3:GetObject",
                "s3:ListBucket"
            ],
            "Resource": [
                "arn:aws:s3:::tfy-interfaces-inboundbucket",
                "arn:aws:s3:::tfy-interfaces-inboundbucket/adosa/*"
            ]
        }
    ]
}
```
## Crear usuario
- Entrar a IAM
- En el panel de navegación izquierdo, selecciona "Users" y luego "Create users". 
- Agregar nombre de usuario que sería el correo y seleccionar Next
- Seleccionar provide user acces to the aws y que se autogenere la contraseña 
- Desde Attach policies directly agregar la politica creada, o en su defecto copiar alguna ya existente
- ### Crear archivo CSV
  - Para crear el archivo CSV con las credenciales buscar el usuario e ingresar 
  - Buscar el Create acces key en la parte superior 
  - Elegir Command Line Intefaces (cli)
  - Agregar descripción y crear el archivo

