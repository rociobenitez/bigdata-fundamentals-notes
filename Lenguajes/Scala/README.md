<h1 align="center">Fundamentos de Scala</h1>

<p align="center">
  Este documento ofrece una visión general de Scala, sus características esenciales y su papel en el ecosistema Big Data. Además, incluye enlaces a los capítulos de “Fundamentos” donde se describen en detalle conceptos como tipos de datos, clases, funciones y estructuras de control.
</p>

<p align="center">
  <a href="Fundamentos/2-Tipos-de-datos.md"><img src="https://img.shields.io/badge/Tipos%20Datos-blue.svg" alt="Tipos de datos"/></a>
  <a href="Fundamentos/3-Variables-Inmutabilidad.md"><img src="https://img.shields.io/badge/Variables%20&%20Inmutabilidad-blue.svg" alt="Variables e inmutabilidad"/></a>
  <a href="Fundamentos/4-Clases-y-Objetos.md"><img src="https://img.shields.io/badge/Clases%20&%20Objetos-blue.svg" alt="Clases y Objetos"/></a>
  <a href="Fundamentos/5-Operadores.md"><img src="https://img.shields.io/badge/Operadores-blue.svg" alt="Operadores"/></a>
  <a href="Fundamentos/6-Condicionales.md"><img src="https://img.shields.io/badge/Condicionales-blue.svg" alt="Condicionales"/></a>
  <a href="Fundamentos/7-Bucles.md"><img src="https://img.shields.io/badge/Bucles-blue.svg" alt="Bucles"/></a>
  <a href="Fundamentos/8-Funciones.md"><img src="https://img.shields.io/badge/Funciones-blue.svg" alt="Funciones"/></a>
  <a href="Fundamentos/9-Arrays-y-Vector.md"><img src="https://img.shields.io/badge/Arrays%20&%20Vector-blue.svg" alt="Arrays y Vector"/></a>
  <a href="Fundamentos/10-Listas-y-Colecciones-Inmutables.md"><img src="https://img.shields.io/badge/Listas%20&%20Colecciones-blue.svg" alt="Listas y colecciones inmutables"/></a>
  <a href="Fundamentos/11-Expresiones-regulares.md"><img src="https://img.shields.io/badge/Expresiones%20Regulares-blue.svg" alt="Expresiones regulares"/></a>
</p>

## Estructura de archivos

```markdown
Scala/
├─ README.md
├─ Fundamentos/ ← Archivos de referencia sobre sintaxis y conceptos
│ ├─ 1-Introducción.md
│ ├─ 2-Tipos-de-Datos.md
│ ├─ 3-Variables-y-Inmutabilidad.md
│ ├─ 4-Clases-y-Objetos.md
│ ├─ 5-Operadores.md
│ ├─ 6-Estructuras-Condicionales.md
│ ├─ 7-Bucles.md
│ ├─ 8-Funciones.md
│ ├─ 9-Arrays-y-Vector.md
│ ├─ 10-Listas-y-Colecciones-Inmutables.md
│ └─ 11-Expresiones-Regulares.md
│
└─ Tutoriales/ ← Guías prácticas para configurar proyectos y entornos
├─ 1-Crear-Proyecto-Scala-IntelliJ.md
└─ 2-Scala-en-Jupyter-Notebook.md
```

## ¿Qué es Scala?

[Scala](https://www.scala-lang.org/) es un lenguaje multiparadigma diseñado para ejecutarse sobre la Máquina Virtual de Java (JVM). Combina lo mejor de:

- **Programación orientada a objetos**: todo en Scala es un objeto.
- **Programación funcional**: funciones de orden superior, inmutabilidad y expresiones lambda.

Al compilar se genera bytecode compatible con la JVM, lo que permite aprovechar la amplia ecosistema de bibliotecas Java.

## Características clave

1. **Sintaxis concisa y expresiva**

   - Se necesitan menos líneas de código que en Java para lograr la misma funcionalidad.
   - Inferencia de tipos en la mayoría de los casos.

2. **Tipado estático**

   - Scala es fuertemente tipado. El compilador detecta errores de tipos en tiempo de compilación.
   - Soporta genéricos, tipos algebraicos y _pattern matching_.

3. **Inmutabilidad por defecto**

   - `val` declara valores inmutables.
   - `var` declara variables mutables (pero se recomienda minimizar su uso).

4. **Colecciones inmutables**

   - La biblioteca estándar incluye `List`, `Vector`, `Map`, `Set`, todas inmutables por defecto.

5. **Paralelismo y concurrencia**

   - Integración nativa con _Akka Actors_ para sistemas reactivos.
   - API de _Futures_ y _Promises_ para programación asíncrona.

6. **Interoperabilidad con Java**
   - Puedes invocar cualquier clase Java desde Scala y viceversa.
   - Permite reutilizar librerías Java sin apenas esfuerzo.

## El papel de Scala en Big Data

Apache Spark está escrito principalmente en Scala. Sus ventajas en Big Data incluyen:

- **APIs nativas** en Scala: las operaciones con _RDDs_, _DataFrames_ y _Datasets_ exhiben menor verbosidad que la API Java.
- **Compatibilidad con librerías Java**: puedes reutilizar clientes de Hadoop, Kafka, JDBC y más.
- **Inmutabilidad** y _pattern matching_: ayudan a razonar mejor sobre flujos de datos distribuidos y transformaciones en Spark.
- **DSLs internas**: construye consultas de alto nivel con sintaxis que se asemeja a SQL o a expresiones funcionales.

## Enlaces de interés

- **Documentación oficial de Scala**: https://docs.scala-lang.org/
- **Descargar Scala**: https://www.scala-lang.org/download/
- **Scala Cheatsheets (oficial)**: https://docs.scala-lang.org/cheatsheets/index.html
- **Repositorio de ejemplos Apache Spark (Scala)**: https://github.com/apache/spark/tree/master/examples/src/main/scala
- **Foro y comunidad**: https://users.scala-lang.org/
- **Probar Scala desde el navegador**: https://scastie.scala-lang.org/
- **Tutorial de Scala**: https://tutoriales.edu.lat/pub/scala?alias=tutorial-de-scala
