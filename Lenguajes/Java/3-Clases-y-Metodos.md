# Clases y Métodos en Java

Este documento funciona como una guía de referencia rápida para todo lo relacionado con **definición de clases**, **constructores**, **atributos**, **métodos** y **elementos avanzados** (herencia, clases internas, etc.).

## Índice de contenidos

- [Definición de clases](#definición-de-clases)
- [Paquetes (package)](#paquetes-package)
- [Constructores](#constructores)
- [Atributos (campos)](#atributos-campos)
- [Métodos](#métodos)
- [Modificadores Avanzados](#modificadores-avanzados)
- [Clases Internas (Inner/Anidadas)](#clases-internas-inneranidadas)
- [Herencia y Jerarquía de Clases](#herencia-y-jerarquía-de-clases)
- [Ejemplos Prácticos](#ejemplos-prácticos)
- [Aplicación a Big Data (ejemplos específicos)](#aplicación-a-big-data-ejemplos-específicos)
- [Buenas Prácticas y Recomendaciones](#buenas-prácticas-y-recomendaciones)
- [Enlaces y Documentación Oficial](#enlaces-y-documentación-oficial)

## Definición de Clases

**Declaración básica**

```java
[modificadores] class NombreClase [extends SuperClase] [implements Interfaz1, Interfaz2] {
    // campos, constructores, métodos, clases internas
}
```

**Modificadores de acceso**:

- `public`: accesible desde cualquier paquete.
- `protected`: accesible desde el mismo paquete y subclases.
- `private`: accesible solo dentro de la misma clase.
- _default_ (sin modificador): accesible solamente en el mismo paquete.

**Convención de nombres**

- Clases y interfaces: **PascalCase** (p.ej. `UsuarioAdmin`, `FileProcessor`).
- Los nombres de carpeta deben corresponder con el `package` (minúsculas, sin espacios, p.ej. `com/miempresa/util`).

**Ejemplo mínimo:**

```java
package com.miempresa.util;

public class Usuario {
    // ...
}
```

## Paquetes (package)

**Sintaxis**: la primera línea de un archivo `.java`:

```java
package com.miempresa.proyecto.modulo;
```

**Relación con carpetas**: Si declaras `package com.miempresa.proyecto.modulo;`, el archivo debe estar en `…/com/miempresa/proyecto/modulo/NombreClase.java`.

**Importaciones**:

```java
import java.util.List;
import com.miempresa.otromodulo.Servicio;
```

## Constructores

#### **Constructor por defecto**

Si no se declara ningún constructor, el compilador genera uno sin parámetros:

```java
public Usuario() { }
```

#### **Constructor con parámetros**

```java
public class Usuario {
    private String nombre;
    private int edad;

    // Constructor parametrizado
    public Usuario(String nombre, int edad) {
        this.nombre = nombre;
        this.edad = edad;
    }
}
```

#### **Sobrecarga de constructores**

```java
public Usuario() {
    this("SinNombre", 0); // Llama al constructor parametrizado
}

public Usuario(String nombre) {
    this(nombre, 0);
}
```

#### **Llamada a superconstructor**

Si se extiende otra clase:

```java
public class Empleado extends Usuario {
    private String departamento;

    public Empleado(String nombre, int edad, String depto) {
        super(nombre, edad);       // Invoca al constructor de Usuario
        this.departamento = depto;
    }
}
```

## Atributos (Campos)

#### **Sintaxis**:

```java
[modificador] [static] [final] Tipo nombreCampo [= valorInicial];
```

**Tipos de campos**:

1. **Variables de instancia** (no `static`): una por cada objeto.

   ```java
   private String nombre;
   private int edad;
   ```

2. **Variables estáticas** (`static`): compartidas por todas las instancias.

   ```java
   public static final int MAX_USUARIOS = 100;
   ```

#### **Inmutabilidad**:

`final` en un campo hace que solo pueda asignarse una vez:

```java
private final String idUnico;
```

#### **Encapsulación**:

Normalmente se declara `private` y se expone mediante getters/setters:

```java
public class Usuario {
    private String nombre;
    private int edad;

    public String getNombre() {
        return nombre;
    }

    public void setNombre(String nombre) {
        this.nombre = nombre;
    }

    public int getEdad() {
        return edad;
    }

    public void setEdad(int edad) {
        if (edad >= 0) {
            this.edad = edad;
        }
    }
}
```

#### **Campos finales y de clase**:

- `public static final double PI = 3.14159;`
- Constante compartida, no puede modificarse.

## Métodos

### 1. Sintaxis y componentes

```java
[modificadores] [<T>] [<T extends ...>] [tipoDeRetorno|void] nombreMetodo([Tipo1 arg1, Tipo2 arg2, ...]) [throws Excepcion1, Excepcion2] {
    // cuerpo del método
}
```

#### **Modificadores comunes**:

- `public`, `protected`, `private`, _default_.
- `static`: método de clase, invocable sin instanciar.
- `final`: no puede sobreescribirse en subclases.
- `abstract`: se declara en clase abstracta; sin implementación.
- `synchronized`: controla acceso concurrente.

#### **Tipo de retorno**:

- Un tipo (p.ej. `int`, `String`, `List<Usuario>`) o `void` si no devuelve nada.

#### **Generics** (opcionales):

```java
public <T> void imprimir(T elemento) { … }
public <K, V> Map<K, V> crearMapa(List<K> claves, List<V> valores) { … }
```

#### **Throws**:

Si el método lanza excepciones comprobadas:

```java
public void leerArchivo(String ruta) throws IOException { … }
```

### 2. Métodos de instancia vs. estáticos

**Instancia**:

```java
public int sumar(int a, int b) {
    return a + b;
}
```

Requiere: `MiClase obj = new MiClase(); obj.sumar(2, 3);`

**Estático**:

```java
public static int multiplicar(int a, int b) {
    return a * b;
}
```

Invocable como: `MiClase.multiplicar(2, 3);` sin instanciar.

### 3. Sobrecarga de métodos

- **Mismo nombre**, distinta **firma** (número/tipo de parámetros):

  ```java
  public double calcularArea(double radio) {
      return Math.PI * radio * radio;
  }

  public int calcularArea(int lado) {
      return lado * lado;
  }
  ```

### 4 Sobrescritura (Override) y Polimorfismo

#### **Sobrescribir** un método de la superclase:

```java
public class Animal {
    public void hacerSonido() {
        System.out.println("Sonido genérico");
    }
}

public class Perro extends Animal {
    @Override
    public void hacerSonido() {
        System.out.println("Guau");
    }
}
```

#### **Polimorfismo**:

```java
Animal a = new Perro();
a.hacerSonido(); // Imprime “Guau” (binding dinámico)
```

### 5 Métodos `final` y `abstract`

**`final`**: evita que una subclase sobrescriba el método.

```java
public class Util {
    public final void metodoCritico() { … }
}
```

**`abstract`**: solo en clases abstractas.

```java
public abstract class Figura {
    public abstract double calcularArea();
}
```

## Modificadores Avanzados

### **`abstract`**

- En clases: `public abstract class Servicio { … }`
- En métodos: `public abstract void ejecutar();`
- Una clase abstracta no puede instanciarse directamente.

### **`final`**

**Clase final**: no puede heredarse.

```java
public final class Constantes { … }
```

**Método final**: no puede sobrescribirse en subclases.

**Campo final**: valor inmutable tras la inicialización.

### **`synchronized`** (concurrencia)

Método bloqueado en acceso:

```java
public synchronized void agregarElemento(T elemento) {
    lista.add(elemento);
}
```

Se usa para evitar condiciones de carrera en entornos multihilo.

### **`transient`** (serialización)

Campo no serializable:

```java
private transient ConexionBD conexion;
```

### **`volatile`** (concurrencia)

Garantiza visibilidad inmediata en distintos hilos:

```java
private volatile boolean activo;
```

## Clases Internas (Inner/Anidadas)

Java permite definir clases dentro de otras clases. Sirve para organizar código relacionado y controlar el alcance.

### 1. Clases Anidadas Estáticas (Static Nested Classes)

```java
public class Externa {
    public static class NestedEstatica {
        public void metodo() {
            System.out.println("Dentro de nested estática");
        }
    }
}

// Invocación:
Externa.NestedEstatica obj = new Externa.NestedEstatica();
obj.metodo();
```

- **No** tienen referencia implícita a una instancia de la clase externa.
- Útiles para agrupar clases auxiliares.

### 2. Clases Internas No Estáticas (Inner Classes)

```java
public class Externa {
    private int dato = 10;

    public class Interna {
        public void mostrarDato() {
            System.out.println("Dato: " + dato);
            // Puede acceder a campos de la instancia de Externa
        }
    }
}

// Invocación:
Externa ext = new Externa();
Externa.Interna in = ext.new Interna();
in.mostrarDato();
```

- **Poseen referencia** a la instancia que las creó (`Externa.this`).

### 3. Clases Locales (dentro de un método)

```java
public void metodoEjemplo() {
    class Local {
        void saludar() {
            System.out.println("Hola desde clase local");
        }
    }
    Local l = new Local();
    l.saludar();
}
```

- Solo visibles dentro del bloque o método donde se definen.

### 4. Clases Anónimas y Lambdas

- **Clase anónima**: implementación “al vuelo” de una interfaz o clase abstracta:

  ```java
  Runnable tarea = new Runnable() {
      @Override
      public void run() {
          System.out.println("Ejecutando tarea");
      }
  };
  new Thread(tarea).start();
  ```

- **Lambda (Java 8+)**: sintaxis reducida para interfaces funcionales:

  ```java
  Runnable tareaLambda = () -> System.out.println("Tarea con lambda");
  new Thread(tareaLambda).start();
  ```

## Herencia y Jerarquía de Clases

- **Extender una clase**:

  ```java
  public class Vehiculo {
      public void arrancar() { … }
  }

  public class Coche extends Vehiculo {
      @Override
      public void arrancar() {
          System.out.println("Arranca el coche");
      }
  }
  ```

- **Implementar interfaces** (Java 8+ permite métodos `default` y `static`):

  ```java
  public interface Volador {
      void volar();

      default void aterrizar() {
          System.out.println("Aterrizando");
      }
  }

  public class Avion implements Volador {
      @Override
      public void volar() {
          System.out.println("El avión vuela");
      }
  }
  ```

- **Casting e `instanceof`**:

  ```java
  Vehiculo v = new Coche();
  v.arrancar(); // “Arranca el coche”

  if (v instanceof Coche) {
      Coche c = (Coche) v;
      // ahora c tiene métodos específicos de Coche
  }
  ```

- **Clases abstractas vs. interfaces**:

  - **Abstracta**: puede tener implementación parcial, campos, constructores.
  - **Interfaz**: solo constantes (`public static final`) y métodos abstractos (antes de Java 8). Con Java 8+, pueden tener `default` y `static`.

## Ejemplos Prácticos

### 1. Clase simple con atributos, constructor y getters/setters

```java
package com.miempresa.modelo;

public class Persona {
    private String nombre;
    private int edad;

    public Persona() {
        this("Desconocido", 0);
    }

    public Persona(String nombre, int edad) {
        this.nombre = nombre;
        this.edad = edad;
    }

    public String getNombre() {
        return nombre;
    }

    public void setNombre(String nombre) {
        if (nombre != null && !nombre.isEmpty()) {
            this.nombre = nombre;
        }
    }

    public int getEdad() {
        return edad;
    }

    public void setEdad(int edad) {
        if (edad >= 0) {
            this.edad = edad;
        }
    }

    @Override
    public String toString() {
        return "Persona[nombre=" + nombre + ", edad=" + edad + "]";
    }
}
```

### 2. Sobrecarga y sobrescritura de métodos

```java
public class Calculadora {
    // Sobrecarga (overload)
    public int sumar(int a, int b) {
        return a + b;
    }

    public double sumar(double a, double b) {
        return a + b;
    }

    // Sobrescritura (override)
    @Override
    public String toString() {
        return "Calculadora básica";
    }
}
```

### 3. Ejemplo de herencia y polimorfismo

```java
public class Animal {
    public void sonido() {
        System.out.println("Sonido genérico");
    }
}

public class Gato extends Animal {
    @Override
    public void sonido() {
        System.out.println("Miau");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal a1 = new Animal();
        Animal a2 = new Gato();    // Polimorfismo

        a1.sonido(); // “Sonido genérico”
        a2.sonido(); // “Miau”
    }
}
```

### 4. Clase interna (Inner) y anónima

```java
public class Externa {
    private long timestamp = System.currentTimeMillis();

    public void iniciarReloj() {
        // Clase interna local
        class Reloj {
            public void mostrarHora() {
                System.out.println("Timestamp: " + timestamp);
            }
        }
        Reloj r = new Reloj();
        r.mostrarHora();
    }

    public Runnable obtenerTarea() {
        // Clase anónima implementando Runnable
        return new Runnable() {
            @Override
            public void run() {
                System.out.println("Hilo ejecutado en: " + System.currentTimeMillis());
            }
        };
    }
}
```

## Aplicación a Big Data (ejemplos específicos)

### 1. Clase que implementa `Writable` (Hadoop)

```java
package com.miempresa.hadoop;

import java.io.DataInput;
import java.io.DataOutput;
import java.io.IOException;
import org.apache.hadoop.io.Writable;

public class ParTextoInt implements Writable {
    private String clave;
    private int valor;

    // Constructor vacío (requerido por Hadoop)
    public ParTextoInt() { }

    public ParTextoInt(String clave, int valor) {
        this.clave = clave;
        this.valor = valor;
    }

    @Override
    public void write(DataOutput out) throws IOException {
        out.writeUTF(clave);
        out.writeInt(valor);
    }

    @Override
    public void readFields(DataInput in) throws IOException {
        clave = in.readUTF();
        valor = in.readInt();
    }

    // Getters y setters...
}
```

### 2. Extender `Mapper` / `Reducer` (Hadoop MapReduce)

```java
public class WordCountMapper extends Mapper<Object, Text, Text, IntWritable> {
    private final static IntWritable uno = new IntWritable(1);
    private Text palabra = new Text();

    @Override
    public void map(Object key, Text value, Context context)
            throws IOException, InterruptedException {
        String[] tokens = value.toString().split("\\s+");
        for (String t : tokens) {
            palabra.set(t.toLowerCase().replaceAll("[^a-zA-Z0-9]", ""));
            if (!palabra.toString().isEmpty()) {
                context.write(palabra, uno);
            }
        }
    }
}
```

```java
public class WordCountReducer extends Reducer<Text, IntWritable, Text, IntWritable> {
    private IntWritable resultado = new IntWritable();

    @Override
    public void reduce(Text key, Iterable<IntWritable> valores, Context context)
            throws IOException, InterruptedException {
        int suma = 0;
        for (IntWritable val : valores) {
            suma += val.get();
        }
        resultado.set(suma);
        context.write(key, resultado);
    }
}
```

### 3. Helper para `SparkSession` (Spark Java API)

```java
package com.miempresa.spark;

import org.apache.spark.SparkConf;
import org.apache.spark.sql.SparkSession;

public class SparkUtil {
    public static SparkSession crearSparkSession(String appName, String master) {
        // master puede ser "local[*]" o URL de cluster
        SparkConf conf = new SparkConf()
                .setAppName(appName)
                .setMaster(master);

        return SparkSession.builder()
                .config(conf)
                .getOrCreate();
    }
}
```

## Buenas Prácticas y Recomendaciones

1. **Visibilidad acorde a la responsabilidad**

   - Usa `private` para campos internos, `public` solo si es parte de la API de la clase.
   - Evita `public static` a menos que sea una constante (por ejemplo, `public static final String VERSION = "1.0";`).

2. **Separación de responsabilidades**

   - Cada clase debe tener una única responsabilidad (Single Responsibility Principle).
   - Si la clase crece demasiado, extrae funcionalidades a una nueva clase.

3. **JavaDoc y Comentarios**

   - Documenta métodos públicos con `/** … */`.
   - Mantén comentarios breves y enfocados en el “por qué”, no en el “qué” (el “qué” debería leerse del código).

4. **Evitar clases anónimas largas**

   - Si la implementación anónima supera unas pocas líneas, conviene crear una clase interna nombrada.

5. **Uso de patrones de diseño cuando corresponda**

   - Factory, Singleton (con enum en Java 8+), Builder, Strategy, etc.

6. **Versión mínima de Java**

   - Para proyectos Big Data:

     - Hadoop 3.x → Java 8 o Java 11.
     - Spark 3.4.x → Java 8, Java 11 o Java 17.

## Enlaces y Documentación Oficial

- **Java Language Specification (JLS)**
  [https://docs.oracle.com/javase/specs/](https://docs.oracle.com/javase/specs/)
- **Tutorial oficial de Oracle (Clases y Objetos)**
  [https://docs.oracle.com/javase/tutorial/java/javaOO/index.html](https://docs.oracle.com/javase/tutorial/java/javaOO/index.html)
- **API de Java SE 17/21**
  [https://docs.oracle.com/en/java/javase/](https://docs.oracle.com/en/java/javase/)
- **Guía de buenas prácticas de Oracle**
  [https://www.oracle.com/java/technologies/javase/codeconventions.html](https://www.oracle.com/java/technologies/javase/codeconventions.html)
- **Documentación de Hadoop Writable**
  [https://hadoop.apache.org/docs/stable/api/org/apache/hadoop/io/Writable.html](https://hadoop.apache.org/docs/stable/api/org/apache/hadoop/io/Writable.html)
- **Spark Java API**
  [https://spark.apache.org/docs/latest/api/java/](https://spark.apache.org/docs/latest/api/java/)
