# Fundamentos de Java aplicados a Big Data

Este documento recopila los conceptos esenciales de Java, orientados a su uso en proyectos y frameworks de Big Data. Incluye ejemplos de código, enlaces a documentación oficial y recomendaciones prácticas.

## 1. Introducción

**Java** es un lenguaje de programación de propósito general, **orientado a objetos, robusto y multiplataforma**. Gran parte del ecosistema Big Data (por ejemplo, Hadoop y muchos componentes de Spark) está escrito en Java o se ejecuta sobre la **JVM** _(Java Virtual Machine)_. Por ello, dominar sus fundamentos es crucial para desarrollar y mantener soluciones eficientes de procesamiento masivo de datos.

## 2. JDK vs. JRE

- **JDK (Java Development Kit)**:

  - Contiene el compilador (`javac`), la JVM, bibliotecas estándar y herramientas (javadoc, jdb, jar).
  - Necesario para **compilar y empaquetar** código Java.
  - 🔗 [Documentación oficial](https://docs.oracle.com/en/java/javase/24/)

- **JRE (Java Runtime Environment)**:
  - Incluye la JVM y las bibliotecas estándar necesarias para ejecutar aplicaciones Java, pero **no el compilador**.
  - Se utiliza cuando sólo se necesita ejecutar aplicaciones existentes.

Para desarrollar, siempre se requiere el JDK. La instalación de cualquier JDK (Oracle, OpenJDK o Temurin) provee también el JRE.

## 3. Estructura de un programa Java

Un programa Java básico consta de:

1. **Declaración de paquete (opcional)**
   ```java
   package com.miempresa.proyecto;
   ```
2. **Importaciones (opcional)**

   ```java
   import java.util.List;
   import java.io.IOException;
   ```

3. **Definición de clase pública**
   ```java
   public class MiClase {
       public static void main(String[] args) {
           // Punto de entrada
       }
   }
   ```
4. **Método `main`**

   Firma obligatoria:

   ```java
   public static void main(String[] args)
   ```

   JVM busca este método como punto de inicio.

5. **Compilación y ejecución**

   Compilar:

   ```sh
   javac MiClase.java
   ```

   Ejecutar:

   ```sh
   java MiClase
   ```

   <img src="./img/editing-compiling-executing.png" width="500">

## 4. Tipos de datos y variables

Java es un lenguaje **fuertemente tipado**. Cada variable debe declararse con su tipo:

- **Primitivos**:

  - Enteros: `byte` (8 bits), `short` (16 bits), `int` (32 bits), `long` (64 bits)
  - Punto flotante: `float` (32 bits), `double` (64 bits)
  - Caracteres: `char` (16 bits, UTF-16)
  - Booleano: `boolean` (true/false)

- **Referencias**:

  - Clases (`String`, `Integer`, `List<String>`, etc.)
  - Interfaces y arrays (`int[]`, `String[]`)

<br>

```java
int contador = 0;
long timestamp = System.currentTimeMillis();
double promedio = 12.5;
boolean activo = true;
String mensaje = "Hola, Big Data";
```

## 5. Operadores y expresiones

- **Aritméticos**: `+`, `-`, `*`, `/`, `%`
- **Relacionales**: `==`, `!=`, `<`, `>`, `<=`, `>=`
- **Lógicos**: `&&`, `||`, `!`
- **Asignación**: `=`, `+=`, `-=`, `*=`, `/=`, `%=`
- **Incremento/Decremento**: `++`, `--`

<br>

```java
int a = 5, b = 3;
int suma = a + b;        // 8
boolean esMayor = a > b; // true
b += 2;                  // b = 5
```

## 6. Estructuras de control

### Condicional `if–else`

```java
if (condicion) {
    // bloque si es verdadero
} else if (otraCondicion) {
    // bloque alternativo
} else {
    // bloque final
}
```

### Switch

```java
switch (opcion) {
    case 1:
        // ...
        break;
    case 2:
        // ...
        break;
    default:
        // ...
}
```

### Bucles

**`for` clásico**

```java
for (int i = 0; i < 10; i++) {
    System.out.println(i);
}
```

**`for-each` (para arrays y colecciones)**

```java
List<String> nombres = List.of("Alice", "Bob", "Carol");
for (String nombre : nombres) {
    System.out.println(nombre);
}
```

**`while`**

```java
int x = 0;
while (x < 5) {
    System.out.println(x);
    x++;
}
```

**`do-while`**

```java
int y = 0;
do {
    System.out.println(y);
    y++;
} while (y < 5);
```

## 7. Programación orientada a objetos (POO)

Java está diseñado para trabajar con objetos. Los pilares principales son:

1. **Clases y objetos**

   - **Clase**: molde que define atributos (campos) y comportamiento (métodos).
   - **Objeto**: instancia de una clase en memoria.

   ```java
   public class Usuario {
       private String nombre;
       private int edad;

       public Usuario(String nombre, int edad) {
           this.nombre = nombre;
           this.edad = edad;
       }

       public void saludar() {
           System.out.println("Hola, soy " + nombre);
       }
   }

   // En otro sitio:
   Usuario u = new Usuario("Ana", 30);
   u.saludar(); // Imprime: Hola, soy Ana
   ```

2. **Encapsulación**

   - Campos privados (`private`) y acceso mediante getters/setters públicos.
   - Protege datos y mantiene integridad.

3. **Herencia**

   - Permite que una clase (subclase) extienda de otra (superclase).
   - Sintaxis: `public class Vehiculo { ... }`
     `public class Coche extends Vehiculo { ... }`

4. **Polimorfismo**

   - Un objeto puede comportarse como instancia de su clase o de cualquier superclase.
   - Permite métodos sobrecargados (mismo nombre, distintas firmas) y sobrescritos (`@Override`).

5. **Clases abstractas e interfaces**

   - **Abstractas**: pueden tener métodos con implementación o sin ella (`abstract class Servicio { ... }`).
   - **Interfaces** (a partir de Java 8 pueden tener métodos `default` y `static`).

## 8. Paquetes y organización de código

Para proyectos grandes es esencial organizar las clases en paquetes:

```text
src/
 └─ main/
     └─ java/
         └─ com/
             └─ miempresa/
                 └─ proyecto/
                     ├─ App.java
                     └─ servicios/
                         └─ ServicioProcesamiento.java
```

Cada carpeta correlaciona con un `package`.

En `ServicioProcesamiento.java`, la primera línea sería:

```java
package com.miempresa.proyecto.servicios;
```

Para compilar todo el proyecto desde la raíz (`src/main/java`):

```sh
javac -d ../out $(find . -name "*.java")
```

Para ejecutar (suponiendo que `App.class` está en `out/com/miempresa/proyecto/`):

```sh
java -cp out com.miempresa.proyecto.App
```

## 9. Herramientas de compilación y gestión de dependencias

En proyectos Big Data es común usar **Maven** o **Gradle** para manejar dependencias (por ejemplo, el cliente de Hadoop, Spark, etc.) y automatizar compilaciones.

### 9.1. Maven

- **`pom.xml`** básico:

  ```xml
  <project xmlns="http://maven.apache.org/POM/4.0.0"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
                               http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.miempresa</groupId>
    <artifactId>mi-proyecto-bigdata</artifactId>
    <version>1.0-SNAPSHOT</version>
    <properties>
      <maven.compiler.source>17</maven.compiler.source>
      <maven.compiler.target>17</maven.compiler.target>
    </properties>
    <dependencies>
      <!-- Ejemplo: dependencia de Hadoop Common -->
      <dependency>
        <groupId>org.apache.hadoop</groupId>
        <artifactId>hadoop-common</artifactId>
        <version>3.3.4</version>
      </dependency>
      <!-- Dependencia de Spark Core -->
      <dependency>
        <groupId>org.apache.spark</groupId>
        <artifactId>spark-core_2.12</artifactId>
        <version>3.4.1</version>
      </dependency>
    </dependencies>
  </project>
  ```

- Comandos frecuentes:

  ```sh
  mvn clean compile      # Compila el proyecto
  mvn package            # Empaqueta en JAR
  mvn dependency:tree    # Muestra árbol de dependencias
  ```

### 9.2. Gradle

- **`build.gradle`** mínimo:

  ```groovy
  plugins {
      id 'java'
  }

  group = 'com.miempresa'
  version = '1.0-SNAPSHOT'
  sourceCompatibility = '17'

  repositories {
      mavenCentral()
  }

  dependencies {
      implementation 'org.apache.hadoop:hadoop-common:3.3.4'
      implementation 'org.apache.spark:spark-core_2.12:3.4.1'
  }
  ```

- Comandos frecuentes:

  ```sh
  gradle clean build     # Compila y empaqueta
  gradle dependencies    # Lista dependencias
  ```

## 10. Ejemplo de MapReduce en Java

A modo de ilustración, este fragmento muestra un job MapReduce muy básico (Word Count), útil para entender cómo Java interactúa con Hadoop:

```java
package com.miempresa.bigdata.hadoop;

import java.io.IOException;
import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.IntWritable;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Job;
import org.apache.hadoop.mapreduce.Mapper;
import org.apache.hadoop.mapreduce.Reducer;
import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;

public class WordCount {

    public static class TokenizerMapper
         extends Mapper<Object, Text, Text, IntWritable> {

        private final static IntWritable uno = new IntWritable(1);
        private Text palabra = new Text();

        @Override
        public void map(Object key, Text value, Context context)
                throws IOException, InterruptedException {
            String[] tokens = value.toString().split("\\s+");
            for (String t : tokens) {
                palabra.set(t.replaceAll("[^a-zA-Z0-9]", "").toLowerCase());
                if (!palabra.toString().isEmpty()) {
                    context.write(palabra, uno);
                }
            }
        }
    }

    public static class SumaReducer
         extends Reducer<Text, IntWritable, Text, IntWritable> {
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

    public static void main(String[] args) throws Exception {
        if (args.length != 2) {
            System.err.println("Uso: WordCount <directorio_entrada> <directorio_salida>");
            System.exit(2);
        }
        Configuration conf = new Configuration();
        Job job = Job.getInstance(conf, "Word Count");
        job.setJarByClass(WordCount.class);
        job.setMapperClass(TokenizerMapper.class);
        job.setCombinerClass(SumaReducer.class);
        job.setReducerClass(SumaReducer.class);
        job.setOutputKeyClass(Text.class);
        job.setOutputValueClass(IntWritable.class);
        FileInputFormat.addInputPath(job, new Path(args[0]));
        FileOutputFormat.setOutputPath(job, new Path(args[1]));
        System.exit(job.waitForCompletion(true) ? 0 : 1);
    }
}
```

**Cómo usar este ejemplo**:

1. Empaqueta el proyecto en un JAR (por ejemplo, `wordcount.jar`).

2. Copia a HDFS algún texto de prueba:

   ```sh
   hdfs dfs -mkdir -p /user/tu_usuario/wordcount/input
   hdfs dfs -put textos/*.txt /user/tu_usuario/wordcount/input/
   ```

3. Ejecuta el job:

   ```sh
   hadoop jar wordcount.jar com.miempresa.bigdata.hadoop.WordCount \
     /user/tu_usuario/wordcount/input /user/tu_usuario/wordcount/output
   ```

4. Visualiza resultados:

   ```sh
   hdfs dfs -cat /user/tu_usuario/wordcount/output/part-*
   ```

## 11. Gestión de compilación para entornos Big Data

Cuando desarrollas jobs de Hadoop o aplicaciones de Spark, debes:

1. Incluir dependencias _“provided”_ para componentes de cluster:

   - Hadoop (`hadoop-common`, `hadoop-mapreduce-client-core`, etc.)
   - Spark (`spark-core`, `spark-sql`, etc.)
     En Maven:

   ```xml
   <dependency>
     <groupId>org.apache.hadoop</groupId>
     <artifactId>hadoop-common</artifactId>
     <version>3.3.4</version>
     <scope>provided</scope>
   </dependency>
   ```

   Esto evita que el JAR final incluya las bibliotecas que ya están en el cluster.

2. Empaquetar todo en un JAR “**fat/uber**” en caso de aplicaciones Spark standalone o Yarn.

   - Con Maven: usar el plugin [maven-shade-plugin](https://maven.apache.org/plugins/maven-shade-plugin/).
   - Con Gradle: configurar la tarea `shadowJar` (plugin “com.github.johnrengelman.shadow”).

3. Probar localmente con un entorno simulado (por ejemplo, Hadoop en modo pseudo-distribuido o Spark local) antes de desplegar al cluster.

## 12. Buenas prácticas y recomendaciones

1. **Versiones de Java y Big Data**:

   - Verifica la compatibilidad de la versión de Java con la versión de Hadoop/Spark que uses. A menudo, Hadoop 3.x funciona bien con Java 8 o Java 11, mientras que Spark 3.4.x es compatible con Java 8–11–17.
   - Para producción, elige la versión LTS (por ejemplo, Java 17).

2. **Gestión de memoria de la JVM**:

   - Configura opciones como `-Xms`, `-Xmx` y `-XX:+UseG1GC` para controlar el heap, especialmente en nodos de datos o ejecutores de Spark.
   - Ejemplo de configuración en Spark:

     ```sh
     spark-submit \
       --conf "spark.executor.memory=4g" \
       --conf "spark.driver.memory=2g" \
       --class com.miempresa.bigdata.App \
       mi-aplicacion-spark.jar
     ```

3. **Estructura modular**:

   - Separa el código de negocio (lógica de procesamiento) de la configuración (lectura de parámetros, rutas HDFS/DB).
   - Usa clases y métodos bien definidas para facilitar pruebas unitarias.

4. **Documentación y comentarios**:

   - Agrega JavaDocs en clases y métodos públicos para describir su funcionalidad.
   - Mantén ejemplos de uso en comentarios o en un archivo **USAGE.md**.

## 13. Enlaces oficiales y recursos adicionales

- **Tutorial oficial de Java (Oracle)**:
  [https://docs.oracle.com/javase/tutorial/](https://docs.oracle.com/javase/tutorial/)
- **Referencias de API de Java SE 17/21**:
  [https://docs.oracle.com/en/java/javase/](https://docs.oracle.com/en/java/javase/)
- **Guía de programación MapReduce (Apache Hadoop)**:
  [https://hadoop.apache.org/docs/r3.3.4/hadoop-mapreduce-client/hadoop-mapreduce-client-core/MapReduceTutorial.html](https://hadoop.apache.org/docs/r3.3.4/hadoop-mapreduce-client/hadoop-mapreduce-client-core/MapReduceTutorial.html)
- **API de Spark en Java**:
  [https://spark.apache.org/docs/latest/api/java/](https://spark.apache.org/docs/latest/api/java/)
- **Java Code Conventions** (Guía de estilo oficial):
  [https://www.oracle.com/java/technologies/javase/codeconventions-introduction.html](https://www.oracle.com/java/technologies/javase/codeconventions-introduction.html)

#### Enlaces de interés

- **Aprendiendo Java**

  - [Learn Java Dev](https://dev.java/learn/)
  - [Learn Java Online](https://www.learnjavaonline.org/)
  - [Java Tutorials Oracle](https://docs.oracle.com/javase/tutorial/java/index.html)
  - [Learn Java Programming](https://www.programiz.com/java-programming)

- **Cursos Online**
  - [Edx Online Courses and Programs](https://www.edx.org/learn/java)
  - [Codecademy: Learn Java](https://www.codecademy.com/enrolled/courses/learn-java)
  - [FreeCodeCamp: Learn Java Courses for Beginners](https://www.freecodecamp.org/news/learn-java-free-java-courses-for-beginners/)
  - [Coursera - Cursos de Java](https://www.coursera.org/courses?query=java)
