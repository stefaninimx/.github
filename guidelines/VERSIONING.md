# Manejo de ramas
En este capítulo se explica como se realiza el manejo de las ramas para los proyectos en los repositorios de código.

## Roles en el repositorio

* Developer
* Tester
* Deployer
* Mantainer
* Líder funcional

### Developer
Encargado del desarrollo de código al igual que las pruebas unitarias. Es responsable de aplicar **buenas prácticas de desarrollo**, desarrollar **pruebas unitarias** y garantizar que su código pueda ser integrado con el desarrollo de los demás miembros del equipo.

### Tester
Encargado de validar que el desarrollo cumple con las funcionalidades solicitadas por el cliente. Su principal responsabilidad es ejecutar **pruebas de sistema** para validar y verificar que un desarrollo puede pasar a **pruebas de aceptación** de cliente. Tiene la potestad de detener el flujo del desarrollo cuando no se cumplen con ciertos estándares o funcionalidades.

### Deployer
Encargado del despliegue del código en fase de staging (pre-productivo) y producción. Su responsabilidad es el despliegue correcto de los cambios realizados en desarrollo, posterior a la aprobación del tester. Dependiendo del proceso de integración y despliegue continuo este rol puede ser manejado automáticamente y no requiere de una persona.

### Mantainer
Administrador y principal responsable del repositorio. En su función como líder técnico en el proyecto tiene la responsabilidad de garatizar que el gitflow se está siguiendo correctamente. Además es el usuario que da la aprobación para el paso de cambios a la rama master del desarrollo.

### Líder funcionalidad
Usuario dueño de la aplicación, es la persona que solicita el desarrollo o mejoras, y quien realiza la validación del desarrollo por medio de **pruebas de aceptación**.

---

## Ramas

Las ramas para todos los proyectos son:

* master
* staging
* develop
* hotfix
* feature
* issue
![Ramas](../assets/img/branches.PNG "Ramas")


### master
La rama master es la rama principal del repositorio. Esta es la rama que alberga el código que será desplegado en producción y sobre el que se maneja el versionamiento de la aplicación. Esta rama tiene las siguientes reglas:
* El código no debe tener problemas de integración, compilación ni ejecución
* El código debe haber sido probado por el tester y líder funcional (usuario que solicitó la solución)
* Solo el mantainer puede mezclar cambios a esta rama
* El versionamiento se realiza haciendo uso de [versionamiento semántico](VERSIONING.md)
* La mezcla de cambios está limitada por la función de Pull request, no se permiten merge. Para la creación de pull request revise [nuestras normas de estilo](../style/PULL_REQUESTS.md)

Para asegurar que los cambios solo sean mezclados haciendo uso de pull request, el mantainer puede agregar reglas las cuales se crean en el repositorio por medio del menú settings.

**_Paso 1_**
![Reglas](../assets/img/rules_1.PNG "Agregando reglas paso 1")
**_Paso 2_**
![Reglas](../assets/img/rules_2.PNG "Agregando reglas paso 2")
