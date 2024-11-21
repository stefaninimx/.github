# Guía de Buenas Prácticas de Programación en Java
Esta guía se enfoca en establecer las mejores prácticas para el desarrollo en Java, con el fin de generar código mantenible y reducir errores mediante el uso correcto del lenguaje y evitando malas prácticas.

## Objetivo
El propósito de este documento es guiar a los desarrolladores en el uso de buenas prácticas de programación en Java, asegurando que el código sea más fácil de mantener y cumpla con estándares mínimos de calidad. **No es un manual de entrenamiento en Java**, sino una referencia de buenas prácticas que busca estandarizar el desarrollo de aplicaciones SOA en Java.

## Audiencia
Esta guía está dirigida a desarrolladores de todos los niveles, especialistas técnicos y arquitectos.

## Marco Normativo
- **IS-05-0059** - Norma del sistema para prácticas de codificación segura.

## Estándares de Codificación en Java

### Lenguaje del Código
El **idioma inglés** será utilizado en el código (nombres de variables, clases, métodos, etc.) por las siguientes razones:
- Simplifica los nombres mediante el uso de género neutro.
- Reduce la ambigüedad en el uso de tiempos verbales.
- Facilita la integración con bibliotecas estándar y de terceros.

### Lenguaje para Comentarios y Registros
El **idioma español** se utilizará en comentarios y mensajes de registro, debido a que:
- Es el idioma común de usuarios, administradores y desarrolladores.
- Facilita el diagnóstico de errores por parte del equipo de soporte técnico.

## Elementos del Programa

A continuación se definen las normas de nomenclatura para paquetes, interfaces, clases, atributos, métodos y variables en el código Java.

### Paquetes
- Los nombres deben escribirse en **minúsculas**.
- Deben comenzar con el nombre del dominio de forma inversa, y continuar libremente según la funcionalidad o la organización del equipo.
  
  **Ejemplo**:
  ```java
  package com.stefanini.marketing.commons;

### Clases
Los nombres de las clases deben seguir estas reglas:

- Sustantivo en Singular: Los nombres de clases específicas deben ser sustantivos en singular que usualmente representan entidades o actores.

  **Ejemplo**:
  ```java
  BusinessRulesValidator, User

Sufijo **Impl** para Implementaciones: Los nombres de clases que implementen una interfaz de tipo deben utilizar el sufijo **Impl** u otro sufijo relacionado con el tipo de la interfaz.

  **Ejemplo**:
  ```java
  class SaleProductImpl implements SaleProduct;
  class RegisterSaleCmd implements RegisterSale;
  ```

### Constantes
Los nombres de las constantes deben seguir las mismas reglas de nomenclatura que las variables, pero deben escribirse completamente en mayúsculas, con palabras separadas por guiones bajos si es necesario.

  **Ejemplo**:
  
  ```java
  public static final int FALSE = 0;
  public static final int TRUE = 1;
  ```

### Métodos
Los nombres de los métodos deben ser verbos en inglés en su forma base, y deben seguir la notación camelCase (primera letra en minúscula y cada palabra interna con mayúscula).

  **Ejemplo**:
  
  ```java
  public void run();
  public int jumpHigh();
  ```

### Formato de Codificación
El código de cada programa debe dividirse en las siguientes secciones, en este orden:

- Declaración del paquete.
- Sentencias de importación.
- Comentarios iniciales (describen el propósito del archivo, clase o funcionalidad).
- Declaración de clases e interfaces.

### Estructura de Clases en Java

Esta guía establece las convenciones para la declaración de paquetes, sentencias de importación, comentarios iniciales y la estructura de clases e interfaces en archivos Java, en conformidad con las prácticas recomendadas de desarrollo seguro y buenas prácticas de codificación.

  ## 1. Declaración del Paquete
  La primera línea del código que no sea un comentario debe ser la **declaración del paquete**.
  
  **Ejemplo**:
  ```java
  package mx.com.ejemplo.commons.model;
  ```
  
  ## 2. Sentencias de Importación
  Es importante optimizar las importaciones indicando **solo los objetos específicos** que se van a utilizar. **Evitar importar todos los objetos de un paquete** utilizando el comodín (`*`). Asimismo, evitar declarar un objeto indicando repetidamente el paquete al que pertenece.
  
  **Ejemplo**:
  ```java
  import java.util.List;
  import mx.com.ejemplo.manager.NotificacionManager;
  ```
  
  ## 3. Comentarios Iniciales
  Cada archivo `.java` debe contener comentarios iniciales en el formato **javadoc**, incluyendo al menos los siguientes datos:
  
  ### Formato de Comentario Javadoc
  - **Descripción**: Breve descripción de la clase pública en una línea de un máximo de 80 caracteres.
    - Pueden incluirse varias líneas para una descripción completa.
    - Se permite HTML básico conforme a las pautas de javadoc.
  
  - **Autor**: Nombre del autor original del archivo.
  
  **Ejemplo**:
  ```java
  /**
   * Implementa la comunicación con la base de datos.<br>
   *
   * @author Juan Perez
   */
  public class MiObjeto {
      // Implementación de la clase
  }
  ```
  
  ## 4. Declaración de Clases e Interfaces
  Las declaraciones de clases e interfaces deben estructurarse de manera organizada, incluyendo el uso de comentarios javadoc y una **distribución coherente de métodos y atributos** para facilitar la legibilidad y mantenimiento del código.
  
  ## 5. Declaración de Variables
  Las variables se deben declarar en el siguiente orden, primero según su **nivel de acceso** y luego según sus **modificadores**:

### Orden por Nivel de Acceso
1. `public`
2. `protected`
3. `private`
4. `package protected` (sin modificador)

### Orden por Modificadores
1. `static`
2. `final`
3. `transient`
4. `volatile`

**Ejemplo de Declaración de Variables**:
```java
public class EjemploClase {
    
    // Variables públicas
    public static final int CONSTANTE = 10;
    public transient String variableTransitoria;

    // Variables protegidas
    protected static List<String> listaProtegida;

    // Variables privadas
    private int contador;
    private final String nombre = "EjemploClase";

    // Métodos y otros elementos de la clase...
}
```

