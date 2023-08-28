# Conectar AWS s3 con PowerBi
## Objetivo
- Conectar la herramienta de power bi con los buckets de S3 de AWS.
## Requisitos
- Tener instalado [python](https://www.python.org/downloads/) en su ultima version
- Ejecutar el siguiente comando en en CMD o powershell para instalar las dependencias necesarias
  - pip install boto3 pandas matplotlib
- Validar versión instalada de python
  - python -- version 
- Tener instalado PowerBi en su versión de escritorio.

## Configuracion PowerBi
- Dentro de la misma consola de comandas CMD o powerShell escribir
  - **where python** y tomar la primer ruta que se muestra omitiendo el python.exe
    - ej. C:\Users\Microsoft\python\python.exe
    - solo copiar C:\Users\Microsoft\python\

- Dentro de PowerBi de escritorio en File - Optiones and settings - Optiones
  - en Global seleccionar *Python scripting*
  - En **Set a Python home direcotry** pegar el resultado del **where python** y presionar ok

- Al tener la cofiguración lista para python buscar la opcion de **Get data** y en la ventan que se muestra presionar **more** y dentro del cuadro de busqueda escribir **Pyhton** y seleccionar Pyhon script

## Codigo y ejemplo
- Para finalizar es necesario agregar el código de pytHon donde se tienen las credenciales y conexiones necesarias para poader obtener los archivos de algun bucket
- **NOTA:** Al tener nombres diferntes en los archiVos de textos por cada bucket, es necesario que el script en cuestión tenga las adecuaciones necesarias

## Ejemplo de codigo
```python
import boto3
import os
import io
import pandas as pd
from datetime import datetime, timedelta

my_key = '{LLAVE SOLIICTADA}'
my_secret = '{SECRETO DEL USUARIO}'

my_bucket_name = '{NOMBRE DEL BUCKET}'

def generate_date_range_strings(start_date_str, end_date_str, output_date_format):
    start_date = datetime.strptime(start_date_str, "%Y-%m-%d")
    end_date = datetime.strptime(end_date_str, "%Y-%m-%d")
    
    date_list = []
    current_date = start_date
    
    while current_date <= end_date:
        date_list.append(current_date.strftime(output_date_format))
        current_date += timedelta(days=1)
    
    return date_list

def run():
    end_date = datetime.now().strftime("%Y-%m-%d")
    dates = generate_date_range_strings('2023-08-10', end_date, "%Y%m%d")

    my_file_paths = [f"ordenesdecompra/OrdenCompra_{date}.txt" for date in dates]

    session = boto3.Session(aws_access_key_id=my_key,
                            aws_secret_access_key=my_secret)
    s3_client = session.client('s3')

    dataframes = []

    for file_path in my_file_paths:
        response = None
        try:
            response = s3_client.get_object(Bucket=my_bucket_name, Key=file_path)
        except:
            continue

        file_data = io.BytesIO(response['Body'].read())
        csv_df = pd.read_csv(file_data, header=0, sep="|", encoding='unicode_escape')
        dataframes.append(csv_df)

    return pd.concat(dataframes)

output = run()

print(output)
