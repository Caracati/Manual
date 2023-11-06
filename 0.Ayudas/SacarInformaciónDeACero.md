# Obtener información de deacero
  
- Es necesario entrar a la instancia de EC2 DeAcero Interface Windows 
- Dentro de C:\scripts\interface_extract.py hay ejemplos de como usar la función para exportar el inventario con la fecha actual
- y en C:\scripts\exports se encuentran los archivos exportados mas no se pasan a S3
- Para ejecutar dichos querys hay que usar el siguiente comando desde C:/scripts py interface_extract.py

Dentro de esta misma ruta de scripts, se encuentra la inforamción necesaria para obtener las interfaces que es como trabaja deacero para subir todo a S3