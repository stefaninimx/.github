# Roles

### 1. **Arquitecto / Admin Repositorio**
   - **Crea y define la rama `main` y `develop`**: El arquitecto establece los lineamientos generales del proyecto, la estructura del repositorio y crea las ramas principales (`main` para la versión estable y `develop` para el desarrollo).
   - **Supervisa los merges finales a `main`**: Revisa las versiones y aprueba los cambios importantes para integrarse en la versión estable, asegurando que cumplan con los requisitos del proyecto.

### 2. **Líder Técnico**
   - **Gestión de ramas de release y hotfixes**:
      - **Rama `release`**: El líder técnico crea ramas de `release` a partir de `develop` en preparación para lanzamientos; aquí se realizan ajustes finales y pruebas antes de fusionarlas a `main`.
      - **Rama `hotfix`**: En caso de problemas en producción, el líder técnico crea ramas `hotfix` a partir de `main` para corregir errores críticos. Estas se fusionan tanto a `main` como a `develop`.
   - **Revisión de pull requests (PR)**: Valida y aprueba los PR de los desarrolladores, verificando que el código cumpla con los estándares y es compatible con la arquitectura.

### 3. **Desarrollador**
   - **Trabajo en ramas `feature`**:
      - Cada desarrollador crea una rama `feature` desde `develop` para trabajar en nuevas funcionalidades o mejoras. Estas ramas deben tener nombres descriptivos (`feature/nueva-funcionalidad`) y enfocarse en un cambio específico.
   - **Envío de pull requests a `develop`**: Al terminar una `feature`, el desarrollador abre un PR hacia `develop` para revisión y aprobación por parte del líder técnico.

### Resumen del Flujo
1. **El arquitecto define** el entorno principal (`main` y `develop`).
2. **El líder técnico administra** las ramas de **`release` y `hotfix`**, y revisa los Pull Request de `feature`.
3. **Los desarrolladores crean** ramas de **`feature`** para su trabajo y envían PR para integrarlas en `develop`.


# Manejo de ramas

En este apartado se explica como se realiza el manejo de las ramas para los proyectos en los repositorios de código.


## Ramas

Las ramas para todos los proyectos son:

* master
* release
* develop
* hotfix
* feature
  
## Flujo de Trabajo

### Ramas Principales

- **`main`**: Contiene el código de producción. Solo el arquitecto puede realizar cambios directos aquí.
- **`develop`**: Rama base para el desarrollo continuo. Contiene el código preparado para la siguiente versión de lanzamiento.

### Ramas de Soporte

- **`feature`**: Utilizadas para desarrollar nuevas funcionalidades. Se crean a partir de `develop`.
  - **Convención de nombres**: `feature/nombre-descriptivo`.
  - Se integran de nuevo en `develop` a través de un PR, que debe ser revisado y aprobado por el líder técnico.

- **`release`**: Preparadas para la próxima versión de producción. Se crean a partir de `develop`.
  - **Convención de nombres**: `release/vX.Y.Z`.
  - Permiten realizar ajustes menores y pruebas finales. Después de ser revisadas, se integran en `main` y `develop`.

- **`hotfix`**: Utilizadas para corregir errores críticos en producción. Se crean a partir de `main`.
  - **Convención de nombres**: `hotfix/nombre-descriptivo`.
  - Al finalizar, se integran tanto en `main` como en `develop`.

## Flujo de Trabajo Detallado

### Desarrollo de Funcionalidades (Feature)

1. El desarrollador crea una rama `feature` desde `develop`.
2. Desarrolla la nueva funcionalidad.
3. Envía un Pull Request a `develop`.
4. El líder técnico revisa y aprueba el Pull Request.
5. La funcionalidad es integrada en `develop`.

### Preparación de Lanzamientos (Release)

1. El líder técnico crea una rama `release` desde `develop`.
2. Se realizan pruebas y se corrigen errores menores.
3. Una vez estable, la rama `release` se fusiona en `main` y `develop`.
4. Se etiqueta la nueva versión en `main`.

### Corrección de Errores Críticos (Hotfix)

1. El líder técnico crea una rama `hotfix` desde `main`.
2. Se corrige el error y se realizan pruebas.
3. Se fusiona la rama `hotfix` en `main` y `develop`.
4. Se etiqueta la nueva versión en `main`.

## Buenas Prácticas

- Mantener las ramas `feature` pequeñas y específicas para facilitar la revisión.
- Commits Pequeños y Frecuentes: Realiza commits pequeños que aborden cambios específicos. Esto facilita la revisión y el seguimiento de cambios.
-	Mensajes de Commit Claros y Descriptivos: Escribe mensajes de commit que expliquen claramente el propósito del cambio. Comienza con un verbo en tiempo presente, por ejemplo: "Corrige error de validación en formulario".
-	Revisiones de Código (Code Reviews): Utiliza Pull Requests para revisar el código antes de fusionarlo en las ramas principales. Esto mejora la calidad del código y permite compartir conocimiento entre el equipo.
-	Mantén el Repositorio Limpio: Elimina ramas que ya no sean necesarias después de que se hayan fusionado. Esto ayuda a mantener el repositorio organizado.
-	Sincroniza Frecuentemente con la Rama Principal: Actualiza regularmente tu rama de trabajo con los cambios de develop o master. Esto minimiza conflictos de fusión y mantiene tu trabajo alineado con las últimas actualizaciones.
-	Evita el Uso de force push: A menos que sea absolutamente necesario, evita usar force push, ya que puede sobrescribir el historial compartido y causar problemas para otros colaboradores.

Este estándar tiene como objetivo optimizar el flujo de trabajo y asegurar una integración continua y ordenada de las nuevas funcionalidades y correcciones, respetando las responsabilidades de cada rol.
