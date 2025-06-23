# Guía de Buenas Prácticas de Programación en Java

Esta guía se enfoca en establecer las mejores prácticas para el desarrollo en Java, con el fin de generar código mantenible y reducir errores mediante el uso correcto del lenguaje y evitando malas prácticas.

## Objetivo

El propósito de este documento es guiar a los desarrolladores en el uso de buenas prácticas de programación en Java, asegurando que el código sea más fácil de mantener y cumpla con estándares mínimos de calidad. **No es un manual de entrenamiento en Java**, sino una referencia de buenas prácticas que busca estandarizar el desarrollo de aplicaciones modernas y robustas en Java.

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
  ```

### Clases

Los nombres de las clases deben seguir estas reglas:

- **Sustantivo en Singular**: Los nombres de clases específicas deben ser sustantivos en singular que usualmente representan entidades o actores.

  **Ejemplo**:
  ```java
  BusinessRulesValidator, User
  ```

- **Sufijo Impl para Implementaciones**: Los nombres de clases que implementen una interfaz de tipo deben utilizar el sufijo **Impl** u otro sufijo relacionado con el tipo de la interfaz.

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

## Formato de Codificación

El código de cada programa debe dividirse en las siguientes secciones, en este orden:

- Declaración del paquete.
- Sentencias de importación.
- Comentarios iniciales (describen el propósito del archivo, clase o funcionalidad).
- Declaración de clases e interfaces.

## Estructura de Clases en Java

Esta guía establece las convenciones para la declaración de paquetes, sentencias de importación, comentarios iniciales y la estructura de clases e interfaces en archivos Java, en conformidad con las prácticas recomendadas de desarrollo seguro y buenas prácticas de codificación.

### 1. Declaración del Paquete

La primera línea del código que no sea un comentario debe ser la **declaración del paquete**.

**Ejemplo**:
```java
package mx.com.ejemplo.commons.model;
```

### 2. Sentencias de Importación

Es importante optimizar las importaciones indicando **solo los objetos específicos** que se van a utilizar. **Evitar importar todos los objetos de un paquete** utilizando el comodín (`*`). Asimismo, evitar declarar un objeto indicando repetidamente el paquete al que pertenece.

**Ejemplo**:
```java
import java.util.List;
import mx.com.ejemplo.manager.NotificacionManager;
```

### 3. Comentarios Iniciales

Cada archivo `.java` debe contener comentarios iniciales en el formato **javadoc**, incluyendo al menos los siguientes datos:

#### Formato de Comentario Javadoc

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

### 4. Declaración de Clases e Interfaces

Las declaraciones de clases e interfaces deben estructurarse de manera organizada, incluyendo el uso de comentarios javadoc y una **distribución coherente de métodos y atributos** para facilitar la legibilidad y mantenimiento del código.

### 5. Declaración de Variables

Las variables se deben declarar en el siguiente orden, primero según su **nivel de acceso** y luego según sus **modificadores**:

#### Orden por Nivel de Acceso

1. `public`
2. `protected`
3. `private`
4. `package protected` (sin modificador)

#### Orden por Modificadores

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

## Principios de Clean Code

El código limpio es fundamental para mantener la calidad y legibilidad del software. Los siguientes principios deben aplicarse en todo desarrollo Java:

### Nombres Significativos

- **Usar nombres descriptivos**: Los nombres de variables, métodos y clases deben expresar claramente su propósito.
- **Evitar abreviaciones**: Preferir nombres completos sobre abreviaciones ambiguas.
- **Ser consistente**: Mantener el mismo vocabulario a lo largo del proyecto.

**Ejemplo**:
```java
// ❌ Malo
int d; // días transcurridos
String usr;
List<String> lst;

// ✅ Bueno
int elapsedTimeInDays;
String username;
List<String> activeUsers;
```

### Funciones Pequeñas

- **Principio de Responsabilidad Única**: Cada función debe hacer una sola cosa.
- **Longitud recomendada**: Las funciones no deben exceder 20 líneas de código.
- **Nombres descriptivos**: El nombre de la función debe explicar exactamente lo que hace.

**Ejemplo**:
```java
// ❌ Malo
public void processUser(User user) {
    // Validar usuario
    if (user.getName() == null || user.getName().isEmpty()) {
        throw new IllegalArgumentException("Nombre requerido");
    }
    
    // Guardar en base de datos
    userRepository.save(user);
    
    // Enviar email
    emailService.sendWelcomeEmail(user.getEmail());
    
    // Generar reporte
    reportService.generateUserReport(user);
}

// ✅ Bueno
public void processUser(User user) {
    validateUser(user);
    saveUser(user);
    sendWelcomeEmail(user);
    generateUserReport(user);
}

private void validateUser(User user) {
    if (user.getName() == null || user.getName().isEmpty()) {
        throw new IllegalArgumentException("Nombre requerido");
    }
}
```

### Comentarios Efectivos

- **Código autodocumentado**: El código debe ser tan claro que minimice la necesidad de comentarios.
- **Comentarios útiles**: Solo agregar comentarios que expliquen el "por qué", no el "qué".
- **Mantener comentarios actualizados**: Los comentarios obsoletos son peores que no tener comentarios.

**Ejemplo**:
```java
// ❌ Malo
// Incrementa i en 1
i++;

// ✅ Bueno
// Aplicamos un descuento del 10% para clientes premium
// porque la política comercial lo establece así
if (customer.isPremium()) {
    discount = 0.10;
}
```

### Formateo Consistente

- **Indentación**: Usar siempre la misma cantidad de espacios (recomendado: 4 espacios).
- **Líneas en blanco**: Usar líneas en blanco para separar conceptos relacionados.
- **Longitud de línea**: No exceder 120 caracteres por línea.

## Principios SOLID

Los principios SOLID son fundamentales para crear código mantenible, extensible y testeable:

### S - Principio de Responsabilidad Única (Single Responsibility Principle)

Una clase debe tener solo una razón para cambiar, es decir, solo una responsabilidad.

**Ejemplo**:
```java
// ❌ Malo - Múltiples responsabilidades
public class User {
    private String name;
    private String email;
    
    public void save() {
        // Lógica para guardar en base de datos
    }
    
    public void sendEmail() {
        // Lógica para enviar email
    }
}

// ✅ Bueno - Responsabilidades separadas
public class User {
    private String name;
    private String email;
    // Solo datos y comportamientos relacionados con User
}

public class UserRepository {
    public void save(User user) {
        // Lógica para guardar en base de datos
    }
}

public class EmailService {
    public void sendEmail(String email, String message) {
        // Lógica para enviar email
    }
}
```

### O - Principio Abierto/Cerrado (Open/Closed Principle)

Las clases deben estar abiertas para extensión pero cerradas para modificación.

**Ejemplo**:
```java
// ✅ Usando interfaces para extensibilidad
public interface PaymentProcessor {
    void processPayment(double amount);
}

public class CreditCardProcessor implements PaymentProcessor {
    @Override
    public void processPayment(double amount) {
        // Lógica para procesar pago con tarjeta de crédito
    }
}

public class PayPalProcessor implements PaymentProcessor {
    @Override
    public void processPayment(double amount) {
        // Lógica para procesar pago con PayPal
    }
}
```

### L - Principio de Sustitución de Liskov (Liskov Substitution Principle)

Los objetos de una clase derivada deben poder reemplazar objetos de la clase base sin alterar el funcionamiento del programa.

**Ejemplo**:
```java
public abstract class Bird {
    public abstract void move();
}

public class Sparrow extends Bird {
    @Override
    public void move() {
        fly();
    }
    
    private void fly() {
        // Lógica de vuelo
    }
}

public class Penguin extends Bird {
    @Override
    public void move() {
        swim();
    }
    
    private void swim() {
        // Lógica de nado
    }
}
```

### I - Principio de Segregación de Interfaces (Interface Segregation Principle)

Los clientes no deben ser forzados a depender de interfaces que no usan.

**Ejemplo**:
```java
// ❌ Malo - Interfaz muy amplia
public interface Worker {
    void work();
    void eat();
    void sleep();
}

// ✅ Bueno - Interfaces segregadas
public interface Workable {
    void work();
}

public interface Eater {
    void eat();
}

public interface Sleeper {
    void sleep();
}

public class Human implements Workable, Eater, Sleeper {
    @Override
    public void work() { /* implementación */ }
    
    @Override
    public void eat() { /* implementación */ }
    
    @Override
    public void sleep() { /* implementación */ }
}
```

### D - Principio de Inversión de Dependencias (Dependency Inversion Principle)

Los módulos de alto nivel no deben depender de módulos de bajo nivel. Ambos deben depender de abstracciones.

**Ejemplo**:
```java
// ❌ Malo - Dependencia directa
public class OrderService {
    private MySQLDatabase database = new MySQLDatabase();
    
    public void saveOrder(Order order) {
        database.save(order);
    }
}

// ✅ Bueno - Dependencia de abstracción
public interface Database {
    void save(Order order);
}

public class OrderService {
    private Database database;
    
    public OrderService(Database database) {
        this.database = database;
    }
    
    public void saveOrder(Order order) {
        database.save(order);
    }
}
```

## Integración con SonarLint

SonarLint es una herramienta de análisis estático que ayuda a detectar bugs, vulnerabilidades de seguridad y code smells en tiempo real durante el desarrollo.

### Configuración de SonarLint

#### Instalación en IDE

**Para IntelliJ IDEA:**
1. Ir a `File` → `Settings` → `Plugins`
2. Buscar "SonarLint" e instalar
3. Reiniciar el IDE

**Para Eclipse:**
1. Ir a `Help` → `Eclipse Marketplace`
2. Buscar "SonarLint" e instalar
3. Reiniciar el IDE

**Para Visual Studio Code:**
1. Ir a la vista de Extensiones (`Ctrl+Shift+X`)
2. Buscar "SonarLint" e instalar

#### Configuración del Proyecto

Crear un archivo `sonar-project.properties` en la raíz del proyecto:

```properties
# Información del proyecto
sonar.projectKey=mi-proyecto-java
sonar.projectName=Mi Proyecto Java
sonar.projectVersion=1.0

# Configuración de fuentes
sonar.sources=src/main/java
sonar.tests=src/test/java
sonar.java.binaries=target/classes
sonar.java.test.binaries=target/test-classes

# Configuración de análisis
sonar.java.source=11
sonar.java.target=11

# Exclusiones
sonar.exclusions=**/*Test.java,**/generated/**
```

### Reglas Principales de SonarLint

#### Bugs Críticos

- **Null Pointer Exception**: Verificar objetos nulos antes de usar
- **Resource Leaks**: Cerrar recursos (streams, connections) en bloques try-with-resources
- **Dead Code**: Eliminar código no utilizado

**Ejemplo de corrección**:
```java
// ❌ Malo - Posible NPE
public String getUserName(User user) {
    return user.getName().toUpperCase();
}

// ✅ Bueno - Verificación de null
public String getUserName(User user) {
    return user != null && user.getName() != null 
        ? user.getName().toUpperCase() 
        : "UNKNOWN";
}
```

#### Vulnerabilidades de Seguridad

- **SQL Injection**: Usar PreparedStatement en lugar de concatenación de strings
- **XSS Prevention**: Escapar datos de entrada del usuario
- **Hardcoded Credentials**: No incluir credenciales en el código fuente

**Ejemplo de corrección**:
```java
// ❌ Malo - SQL Injection
public User findUser(String username) {
    String sql = "SELECT * FROM users WHERE username = '" + username + "'";
    // Ejecutar query...
}

// ✅ Bueno - PreparedStatement
public User findUser(String username) {
    String sql = "SELECT * FROM users WHERE username = ?";
    PreparedStatement stmt = connection.prepareStatement(sql);
    stmt.setString(1, username);
    // Ejecutar query...
}
```

#### Code Smells Comunes

- **Métodos muy largos**: Dividir en métodos más pequeños
- **Clases con muchas responsabilidades**: Aplicar principio de responsabilidad única
- **Complejidad ciclomática alta**: Reducir anidamiento y condiciones

### Configuración de Reglas Personalizadas

Crear un archivo `sonar-lint.xml` para personalizar reglas:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
    <rules>
        <!-- Activar reglas específicas -->
        <rule>
            <key>java:S1192</key> <!-- String literals should not be duplicated -->
            <severity>MAJOR</severity>
        </rule>
        
        <!-- Desactivar reglas no aplicables -->
        <rule>
            <key>java:S1118</key> <!-- Utility classes should not have public constructors -->
            <severity>OFF</severity>
        </rule>
    </rules>
</configuration>
```

### Métricas de Calidad

SonarLint proporciona métricas importantes para evaluar la calidad del código:

#### Cobertura de Código
- **Objetivo**: Mínimo 80% de cobertura en pruebas unitarias
- **Herramientas**: JaCoCo integration

#### Complejidad Ciclomática
- **Objetivo**: Máximo 10 por método
- **Acción**: Refactorizar métodos complejos

#### Duplicación de Código
- **Objetivo**: Máximo 3% de duplicación
- **Acción**: Extraer métodos comunes

## Conclusión

La aplicación de estas prácticas de Clean Code, principios SOLID y el uso de SonarLint como herramienta de análisis estático garantiza la creación de código Java de alta calidad, mantenible y seguro. Es responsabilidad de cada desarrollador implementar estas prácticas en su trabajo diario y participar en las revisiones de código para asegurar el cumplimiento de estos estándares.

### Recursos Adicionales

- **Clean Code** - Robert C. Martin
- **Effective Java** - Joshua Bloch
- **SonarQube Documentation**: https://docs.sonarqube.org/
- **Java Code Conventions**: https://www.oracle.com/java/technologies/javase/codeconventions-contents.html
