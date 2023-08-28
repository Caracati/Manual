# Estándar de Programación: Aplicación con Angular, Entity Framework y Lambdas

## Frontend: Angular

### Estructura del Proyecto
..........

### Mejores Prácticas

- Utilizar rutas y lazy loading para cargar módulos y componentes de manera eficiente.
- Emplear componentes reutilizables para mantener la coherencia en la interfaz de usuario.
- Aplicar el patrón "Smart and Dumb Components" para separar la lógica de presentación y la lógica de negocio.

## Backend: Entity Framework y Lambdas

### Estructura del Proyecto
.............

### Entity Framework

- Utilizar migraciones para gestionar la estructura de la base de datos.
- Configurar Data Annotations o Fluent API para definir relaciones, validaciones y propiedades de las entidades.

### Lambda Expressions

- Usar Lambda Expressions para realizar consultas eficientes en colecciones y bases de datos.
- Emplear métodos como `Where`, `OrderBy`, `Select`, etc., para filtrar y transformar datos.
- Priorizar la legibilidad al combinar operaciones Lambda en cadenas largas.
- Documentar todas las lambdas creadas con una descripción que sea entendible

### Manejo de Valores Nulos

- Utilizar tipos nullable (`int?`, `DateTime?`, etc.) en lugar de valores por defecto para representar campos opcionales en la base de datos.
- En las consultas Lambda, considerar el uso de operadores de coalescencia nula (`??`) para proporcionar valores alternativos en caso de que un campo sea nulo.

## Control de Versiones

- Utilizar un sistema de control de versiones como Git para rastrear y colaborar en el código.
- Aplicar branching y merging de manera adecuada para mantener un flujo de trabajo organizado.

## Pruebas y Calidad del Código

- Implementar pruebas unitarias y de integración para validar el funcionamiento del backend.
- Utilizar herramientas de análisis estático de código para identificar problemas potenciales.
- Aplicar patrones de diseño SOLID para mantener un código modular y mantenible.

## Documentación

- Documentar los endpoints de la API utilizando herramientas como Swagger.
- Incluir comentarios descriptivos en el código para mejorar la comprensión tanto en funciones y clases.
- Mantener una documentación actualizada para futuros desarrolladores y colaboradores.
