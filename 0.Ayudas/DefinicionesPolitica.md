## Definiciones de los encabezados en politicas

- El objetivo de esta sección es dar a conocer los campos que se tienen en los encabezados al generar un politica y explicar su definición para tener un mejor entendimineto y conceptos de las mismas

- En análisis de la demanda al terminar de ejecutar y correr todas las policitas es posible descargar el archivo final de como quedó la policita del inventario el cual se desglosa en la tabla siguiente
- Actualmente son 39 headers los que se tienen al 23 de febrero del 2024

| Campo             | Descripción                     |
|-------------------|---------------------------------|
| locationCode      | Código de ubicación de donde se encuentra el producto             |
| locationName      | Nombre de la ubicación de donde se encuentra el producto          |
| productCode       | Código del producto o SKU del producto            |
| productName       | Nombre del producto              |
| supplierName      | Nombre del proveedor             |
| start             | Primera venta del producto dentro de la ventana de tiempo seleccionada|
| end               | Fecha de fin de la ventana de tiempo                    |
| periods           | Son los días de venta que tuvo el producto en la ventana de tiempo, este campo va de la mano con minDays ya que este se toma en cuenta si el producto tiene menos ventas de las establecidas esto se calculo desde el día de su primer compra a mas date         |
| average           | Valor promedio del volumen (piezas vendidas) sobre el los periodo.  volumen / periodo                |
| sigma             | Desviación estándar del producto              |
| cv                | Coeficiente de variación, es para determinar que tan regular o irregular fue la venta, entre mas se acerque al cero es mas estable  (sigma / average)       |
| volume            | Son las piezs que se vendieron en la ventana de tiempo establecida            |
| cost              | Costo total de la venta del producto de la ventan de tiempo, para obtener el costo individual es costo / volumen           |
| revenue           | Ingresos generados totales de la venta del producto en la ventana de tiempo, para calcular la ganancia por porducto es revenue / volumen              |
| minDate           | fecha inicial en la Ventana de tiempo real - todo esto se parametriza desde ventnas de tiempo                     |
| maxDate           | fecha final en la Ventana de tiempo real - todo esto se parametriza desde ventnas de tiempo                     |
| minDays           | Son los días minimos que puede tener un producto como venta       |
| daysWithDemand    | Son los días en los que ese producto tuvo venta                 |
| lastDemandDate    | Última fecha de demanda en la que el producto tuvo venta         |
| zAverage          | Valor Z del promedio             |
| zMargin           | Valor Z del margen (Para obtener el margen se usa la formula de revenue - cost)              |
| zCv               | Valor Z del coeficiente de variación |
| zCost             | Valor Z del costo                 |
| abc               | Clasificación ABC - es la clasificación que se le asigna al producto              |
| volumeWeight      | Peso del volumen que se le asigna al volumen para sacar el ABC                |
| marginWeight      | Peso del margen que se le asigna al margen para sacar el ABC                 |
| variabilityWeight | Peso de la variabilidad que se le asigna a la variabilidad para sacar el ABC         |
| costWeight        | Peso del costo que se le asigna al costo para sacar el ABC                  |
| AsPercentage      | Porcentaje de As es la cantidad en % del los productos que se quieren que sean de clasificación A                |
| BsPercentage      | Porcentaje de Bs es la cantidad en % del los productos que se quieren que sean de clasificación B  (el % sobrante se va para C y los D son los que no tienen consumo)                |
| serviceLevel      | Nivel de servicio que se le quiere dar a ese producto, esto va dependiendo también de la clasificación ABC que se le haya asignado, esto quiero decir la probabilidad de poder cubrir la demanda en ese momento               |
| strategy          | Es la estrategía que se le dará al producto ya sea meta, punto de reorden o seguridad       |
| orderType         | Tipo de orden                    |
| lotSize           | Tamaño total del lote si en este campo hay 10 significa que el lote tiene un total de 10 productos                  |
| reorderingDelay   | Cuándo se hará la revisión para realizar el pedido             |
| leadtime          | Tiempo de espera en la entrega del producto                 |
| target            | Objetivo es el inventario meta                        |
| reorder           | Punto de reorden                        |
| safety            | Inventario de seguridad    |
