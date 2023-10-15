# Guía de Colaboración en Git

Esta guía establece las reglas y recomendaciones para trabajar en equipo utilizando Git como sistema de control de versiones en Tandrify. El objetivo es mantener un flujo de trabajo ordenado y eficiente.

## Ramas

Las ramas deben seguir la siguiente nomenclatura: `{tipo}_descripcion-ingles--de-desarrollo`, donde `{tipo}` puede ser:

- `fix`: Para correcciones de errores.
- `feature`: Para nuevas características.
- `hotfix`: Para correcciones críticas que deben implementarse de inmediato.
- `chore`: Para tareas de mantenimiento o tareas no relacionadas con características o correcciones de errores.

Ejemplo de creación de una rama:
```bash
git checkout -b feature_new-functionality
```

## Commits

Los commits deben ser descriptivos y seguir un formato claro. Cada commit debe comenzar con una etiqueta que indique el tipo de cambio y luego una descripción concisa. Las etiquetas comunes son:

- `fix:`: Para correcciones de errores.
- `feat:`: Para nuevas características.
- `docs:`: Para cambios en la documentación.
- `style:`: Para mejoras en el formato o estilo del código.
- `refactor:`: Para refactorizaciones del código.
- `test:`: Para adiciones o modificaciones en pruebas.
- `chore:`: Para tareas de mantenimiento.

Ejemplo de un commit:
```bash
git commit -m "feat: Agregar función de autenticación de usuarios"
```
## Pull Requests (PR) 
>### *Actualmente no se esta utilizando esta opción de PR*
>
>Antes de fusionar una rama en la rama principal (generalmente main o master), se debe abrir un Pull Request (PR) para >revisión. El PR debe incluir:
>
>- Una descripción clara de los cambios.
>- Etiquetas relacionadas (por ejemplo, "Fixes #12" para vincular el PR con un problema de seguimiento).
>- Una lista de verificación de revisión para que los revisores sepan qué aspectos revisar.
>
>Ejemplo de un Pull Request
>- Título del PR: Agregar función de autenticación de usuarios
>- Descripción: Esta solicitud de extracción agrega una nueva función de autenticación de usuarios que permite a los usuarios registrarse y acceder de manera segura al sistema.
>- Etiquetas relacionadas: Fixes #23
>- Lista de verificación de revisión:
>  - Se ha probado la nueva función de autenticación.
>  - La documentación se ha actualizado para reflejar los cambios.
>  - El código sigue los estándares de estilo del proyecto.

## Revisión de Código

Todas las solicitudes de extracción (PR) deben ser revisadas por al menos un miembro del equipo antes de fusionarse. La revisión de código es una oportunidad para:

- Comprobar la calidad del código.
- Asegurarse de que los cambios se adhieran a los estándares del proyecto.
- Identificar problemas potenciales.
- Aunque no se tenga o no se esté implementado el PR, se puede validar el código también para
  - Entender un poco mas el funcionamiento
  - Ver ejemplos de otros desarrolladores y tener mejores ideas


## Resolución de Conflictos
Si surge un conflicto al fusionar una rama, se debe resolver antes de la fusión. 

## Mantenimiento Continuo
El mantenimiento de las ramas y la limpieza de ramas obsoletas es responsabilidad de los desarrolladores. Es buena practica eliminar las ramas una vez fusionadas y resueltas.

## Pasos para hacer merge
- Es necesario trabajar todo de forma local en la rama creada donde se reliazarán los cambios, cuando estos cambios ya estén terminados y con commit se debe de ejecutar 
  - git checkout dev20220809 -- o la rama de dev donde se este trabajando acutalmente de desarrollo
  - git pull -- para garantizar que se tiene la ultima versión de dev
  - git merge {tipo}_descripcion-de-desarrollo
  - git push -- validar con el equipo de desarrollo que no se tenga algun cambio pendiente

### Notas
- Si se quere hacer un cambio de un comentario del ULITMO commit realizado se puede usar
  - git commit --amend -m "Tipo de arreglo: Comentario nuevo"

- Cuando se tiene algun commit que se queire subir a master se puede usar en lugar de hacer un merge
  - git checkout master
  - git pull origin master
  - git cherry-pick 0b5783a
  - git push origin master