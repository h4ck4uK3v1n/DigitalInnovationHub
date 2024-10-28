## Programación Funcional Con Java

### ¿Qué es la Programación Funcional?

- La programación funcional es un **paradigma** de programación que trata la computación como la evaluación de **funciones** **matemáticas** y evita el cambio de estado y los datos mutables.
- La programación funcional es declarativa en lugar de imperativa, y el estado de la aplicación fluye a través de funciones puras. En contraste con la programación orientada a objetos, donde el estado de la aplicación generalmente se comparte y se ubica junto con los métodos en los objetos.

### Programación Funcional en Java

- Java 8 introdujo un nuevo paquete `java.util.function` que contiene interfaces funcionales que se pueden usar como **expresiones lambda**.
- Java 8 también introdujo una nueva sintaxis llamada **referencia de método** que se puede usar para expresiones lambda.
- Un ejemplo es la interfaz funcional `Predicate` que tiene un método `test(T t)` que devuelve un valor booleano. Esta interfaz se puede usar para expresiones lambda y referencias de métodos.

```java
public interface Predicate<T> {
    boolean test(T t);
}
public class Example{
    public static void main(String[] args) {
        Predicate<String> predicate = (s) -> !s.isEmpty();
        predicate.test("foo");              // true
        predicate.negate().test("foo");     // false
        Predicate<Boolean> nonNull = Objects::nonNull;
        Predicate<Boolean> isNull = Objects::isNull;
        Predicate<String> isEmpty = String::isEmpty;
        Predicate<String> isNotEmpty = isEmpty.negate();
    }
}
```

### Interfaces Funcionales

- Una interfaz funcional es una interfaz que contiene solo un método abstracto.
- Solo pueden tener una funcionalidad para exhibir.
- A partir de Java 8 en adelante, las expresiones lambda se pueden utilizar para representar la instancia de una interfaz funcional.
- Un ejemplo de la interfaz funcional es el ejemplo anterior, la interfaz `Predicate` es una interfaz funcional porque solo tiene un método abstracto test(T t).

### Expresiones Lambda

- Una expresión lambda es un bloque corto de código que toma parámetros y devuelve un valor.
- Las expresiones lambda son similares a los métodos y se llaman (funciones anónimas), pero no necesitan un nombre y se pueden implementar directamente en el cuerpo de un método.

***Para entender el concepto de la programación funcional en Java, debes entender algunos conceptos clave***

### ¿Qué es una Función?

- Una función es un bloque de código que realiza una tarea específica.
- Una función toma uno o más parámetros de entrada, opera sobre ellos y produce una salida.
- La salida producida por una función se llama el valor de retorno de la función.

### ¿Qué es una Función Pura?

- Una función pura es una función donde el valor de retorno está determinado solo por sus valores de entrada, sin efectos secundarios observables.
- Así es como funcionan las funciones en matemáticas: `Math.cos(x)` siempre devolverá el mismo resultado para el mismo valor de x.
- Las funciones puras no tienen efectos secundarios observables, como llamadas a la red o a la base de datos.

### ¿Qué es una Función de Orden Superior?

- Una función de orden superior es una función que toma funciones como parámetros o devuelve una función.
- Las funciones de orden superior se utilizan a menudo para:
    - Abstraer o aislar acciones, efectos o control de flujo asíncrono utilizando funciones de devolución de llamada, promesas, monadas, etc...
    - Crear utilidades que pueden actuar en una amplia variedad de tipos de datos
    - Aplicar parcialmente una función a sus argumentos o crear una función curada con el propósito de reutilización o composición de funciones
    - Tomar una lista de funciones y devolver alguna composición de esas funciones de entrada
- Un ejemplo de la función de orden superior es el siguiente ejemplo:

```java
public class Example{
    public static void main(String[] args) {
        Function<Integer, Integer> add1 = x -> x + 1;
        Function<Integer, Integer> mult2 = x -> x * 2;
        Function<Integer, Integer> add1Mult2 = add1.andThen(mult2);
        add1Mult2.apply(2);         // 6
        Function<Integer, Integer> mult2add1 = add1.compose(mult2);
        mult2add1.apply(2);         // 5
    }
}
```

- La explicación es :
    - La función add1 suma 1 al valor de entrada.
    - La función mult2 multiplica el valor de entrada por 2.
    - La función add1Mult2 primero aplica la función add1 al valor de entrada, y luego aplica la función mult2 al resultado.
    - La función mult2add1 primero aplica la función mult2 al valor de entrada, y luego aplica la función add1 al resultado.

### Inmutabilidad

- La inmutabilidad es un concepto que establece que el estado de un objeto no se puede modificar después de que se crea.
- La inmutabilidad es un concepto clave en la programación funcional porque ayuda a evitar efectos secundarios.
- Un ejemplo es el siguiente ejemplo:

```java
public class Example{
    public static void main(String[] args) {
        List<String> names = new ArrayList<>();
        names.add("John");
        names.add("Freddy");
        names.add("Samuel");
        names.add("Lauren");
        names.remove(0);
        System.out.println(names);     // [Freddy, Samuel, Lauren]
    }
}
```

### **Funciones como ciudadanos de primera clase**

Cuando hablamos de "ciudadanos de primera clase" en el contexto de funciones en un lenguaje de programación, estamos diciendo que las funciones son tratadas como cualquier otro tipo de dato en ese lenguaje. Puedes asignarlas a variables, pasarlas como parámetros a otras funciones, retornarlas como resultados de funciones y almacenarlas en estructuras de datos. Este enfoque brinda flexibilidad y poder expresivo en la manipulación de funciones, lo cual es una característica central de los lenguajes que admiten la programación funcional.

1. **Ser asignadas a variables:** Puedes asignar una función a una variable, de manera similar a como asignas un valor entero o una cadena. Esto permite que las funciones sean manipuladas y pasadas como argumentos a otras funciones.
    
    ```java
    Function<Integer, Integer> cuadrado = x -> x * x;
    
    ```
    
2. **Ser pasadas como argumentos:** Puedes pasar funciones como argumentos a otras funciones. Esto es fundamental para implementar el paradigma de programación funcional y permite una mayor flexibilidad en el diseño del código.
    
    ```java
    public static void procesarNumero(int numero, Function<Integer, Integer> operacion) {
        int resultado = operacion.apply(numero);
        System.out.println("Resultado: " + resultado);
    }
    
    // Uso
    procesarNumero(5, cuadrado);
    
    ```
    
3. **Ser devueltas por otras funciones:** Puedes devolver una función desde otra función, permitiendo construir funciones de orden superior.
    
    ```java
    public static Function<Integer, Integer> obtenerFuncion(boolean doblar) {
        if (doblar) {
            return x -> x * 2;
        } else {
            return x -> x + 5;
        }
    }
    
    // Uso
    Function<Integer, Integer> funcion = obtenerFuncion(true);
    int resultado = funcion.apply(3);
    
    ```
    
4. **Ser almacenadas en estructuras de datos:** Puedes almacenar funciones en estructuras de datos como listas o mapas, lo que puede ser útil para crear estrategias flexibles y dinámicas.
    
    ```java
    List<Function<Integer, Integer>> operaciones = new ArrayList<>();
    operaciones.add(x -> x * 2);
    operaciones.add(x -> x + 5);
    
    // Uso
    int resultado1 = operaciones.get(0).apply(3);  // resultado1 = 6
    int resultado2 = operaciones.get(1).apply(3);  // resultado2 = 8
    
    ```
    

Este enfoque es parte fundamental de la programación funcional y permite escribir código más modular, reutilizable y expresivo en Java. Con la introducción de expresiones lambda en Java 8 y las interfaces funcionales en el paquete `java.util.function`, se ha mejorado significativamente la capacidad del lenguaje para tratar a las funciones como ciudadanos de primera clase.

### **Funciones puras e Impuras**

Las funciones puras e impuras se refieren a las características y comportamiento de funciones en términos de efectos secundarios y determinismo.

#### Funciones Puras:

Se podría decir que las funciones puras también cumple el principio SRP (Una única responsabilidad).

Las funciones puras son funciones que tienen dos características fundamentales:

1. **Determinismo:** Dada la misma entrada, una función pura siempre producirá la misma salida. No hay variabilidad en el resultado basada en estados externos o variables globales.
2. **No Efectos Secundarios Observables:** Una función pura no realiza cambios en el estado del programa fuera de la función. Esto significa que no modifica variables globales, no realiza operaciones de entrada/salida y no causa ningún otro efecto observable en el entorno.
    1. no modifica la base de datos
    2. no genera archivos

**Características de Funciones Puras:**

- **Reproducibilidad:** Dada una entrada específica, una función pura siempre dará el mismo resultado, lo que facilita la depuración y el razonamiento sobre el código.
- [**Testabilidad](Programacio%CC%81n%20Funcional%20Con%20Java%20ae32563745dc467fb864925c4e9db63b.md):** Debido a su determinismo y falta de efectos secundarios, las funciones puras son fáciles de probar. Puedes prever y controlar las entradas y evaluar directamente las salidas.
- **Composición:** Las funciones puras son fácilmente componibles. Puedes combinar funciones puras para crear funciones más complejas sin preocuparte por efectos colaterales inesperados.

**Ejemplo de Función Pura:**

```java
// Función pura que calcula el cuadrado de un número.
public int cuadrado(int x) {
    return x * x;
}

// using functional interfaces
Function<Integer, Integer> square = (x) -> x * x;

```

En este ejemplo, la función `cuadrado` toma un argumento `x` y devuelve el resultado del cuadrado de `x`. No realiza operaciones de entrada/salida, no modifica variables globales y siempre produce el mismo resultado para una entrada dada.

> Una función pura puede invocar a otra función pura y no a una función impura, mientras una función impura puede invocar a ambas sea pura e impura
> 

#### **Funciones Impuras:**

Las funciones impuras son aquellas que no cumplen con alguna o ambas de las características de las funciones puras. Pueden tener efectos secundarios observables y/o no ser deterministas.

**Características de Funciones Impuras:**

- **Efectos Secundarios:** Pueden modificar variables globales, realizar operaciones de entrada/salida u otros cambios en el estado del programa.
- **No Determinismo:** La misma entrada no garantiza la misma salida en todas las llamadas.

**Ejemplo de Función Impura:**

```java
// Función impura que imprime un mensaje y retorna el cuadrado de un número.
public int cuadradoConImpureza(int x) {
    System.out.println("Calculando el cuadrado de " + x);
    return x * x;
}

```

En este ejemplo, la función `cuadradoConImpureza` tiene un efecto secundario observable: imprime un mensaje en la consola. Esto la hace impura porque va más allá del cálculo del resultado y afecta al entorno exterior.

En resumen, el uso de funciones puras en programación funcional mejora la **legibilidad**, [**testabilidad](Programacio%CC%81n%20Funcional%20Con%20Java%20ae32563745dc467fb864925c4e9db63b.md)** y mantenimiento del código, al tiempo que facilita el razonamiento sobre el comportamiento del programa. Las funciones impuras, aunque pueden ser necesarias en ciertos casos, tienden a ser más difíciles de entender y de razonar debido a sus posibles efectos secundarios y falta de determinismo.

### **Entendiendo dos jugadores clave: `SAM` y `FunctionalInterface`**

En el contexto de Java, los términos SAM (Single Abstract Method) y Functional Interface se utilizan de manera intercambiable y están relacionados. Un SAM es una interfaz que tiene un único método abstracto, y un Functional Interface es una interfaz que cumple con esta condición. A partir de Java 8, con la introducción de expresiones lambda, estas interfaces se vuelven fundamentales para trabajar con funciones anónimas de manera más concisa.

Por ejemplo, considera la interfaz `Runnable` en Java:

```java
@FunctionalInterface
public interface Runnable {
    void run();
}

```

Esta interfaz tiene un solo método abstracto (`run`), y además, está anotada con `@FunctionalInterface`. La anotación `@FunctionalInterface` no es estrictamente necesaria, pero se utiliza para indicar que la interfaz está diseñada para ser utilizada como un Functional Interface, y el compilador emitirá un error si se intenta agregar más de un método abstracto.

Con Java 8, puedes usar expresiones lambda para proporcionar implementaciones concisas de interfaces funcionales:

```java
// Uso de expresión lambda con Runnable
Runnable myRunnable = () -> System.out.println("Hello from Runnable");

```

Aquí, `myRunnable` es una instancia de una interfaz funcional (`Runnable`) mediante el uso de una expresión lambda.

En resumen, SAM (Single Abstract Method) y Functional Interface son conceptos que se utilizan para describir interfaces con un solo método abstracto en Java, y estos se volvieron más prominentes y útiles con la introducción de expresiones lambda en Java 8.

### **Operador de Referencia**

El operador de referencia en Java es una característica que se introdujo en Java 8 para simplificar la expresión de las lambdas que se utilizan comúnmente con interfaces funcionales. Permite referenciar métodos existentes o constructores mediante un nombre en lugar de proporcionar una implementación directa del método.

Existen cuatro tipos principales de operadores de referencia en Java:

1. **Referencia a un método estático:**
Puedes referenciar un método estático utilizando el nombre de la clase que lo contiene.
Estructura: `(ClassName::methodName)`

```java
// Expresión lambda
Function<String, Integer> parseInt = s -> Integer.parseInt(s);    
// Operador de referencia a método estático
Function<String, Integer> parseIntRef = Integer::parseInt;
```
    
2. **Referencia a un método de instancia de un objeto particular:**
Puedes referenciar un método de instancia de un objeto específico utilizando el nombre del objeto seguido por el doble colon y el nombre del método. Estructura: `(objectOfClass::methodName)`

```java
    // Expresión lambda
    BiPredicate<String, String> startsWith = (s1, s2) -> s1.startsWith(s2);
    
    // Operador de referencia a método de instancia
    BiPredicate<String, String> startsWithRef = String::startsWith;
```
    
3. **Referencia a un método de instancia de un tipo arbitrario:**
Puedes referenciar un método de instancia de un tipo arbitrario utilizando el nombre del tipo seguido por el doble colon y el nombre del método.

```java
    // Expresión lambda
    Comparator<String> lengthComparator = (s1, s2) -> s1.length() - s2.length();
    
    // Operador de referencia a método de instancia de tipo arbitrario
    Comparator<String> lengthComparatorRef = Comparator.comparing(String::length);
    
```
    
4. **Referencia a un constructor:**
Puedes referenciar un constructor utilizando el nombre de la clase seguido por `::` y `new`. Estructura: `(super::methodName)`
```java
// Expresión lambda
Supplier<List<String>> listSupplier = () -> new ArrayList<>();
    
// Operador de referencia a constructor
Supplier<List<String>> listSupplierRef = ArrayList::new;
```
    

El uso de operadores de referencia puede hacer que el código sea más conciso y legible, especialmente cuando estás trabajando con interfaces funcionales y expresiones lambda. Estos operadores facilitan la reutilización de código existente al referenciar métodos ya definidos en lugar de proporcionar una implementación directa.

### **Analizando la inferencia de tipos**

La inferencia de tipos es una característica en lenguajes de programación que permite al compilador deducir o inferir el tipo de una variable basándose en el contexto y en el tipo de datos con el que se está trabajando. Java introduce la inferencia de tipos local (también conocida como "var") a partir de Java 10, y esto se utiliza para declarar variables locales de una manera más concisa sin tener que repetir explícitamente el tipo de la variable.

Veamos un ejemplo para entender mejor la inferencia de tipos en Java:

Antes de Java 10:

```java
List<String> listaDeCadenas = new ArrayList<String>();

```

Con inferencia de tipos (Java 10 y posteriores):

```java
var listaDeCadenas = new ArrayList<String>();

```

En este caso, la palabra clave `var` se utiliza en lugar de la declaración explícita del tipo de la variable. El compilador infiere que `listaDeCadenas` es de tipo `ArrayList<String>` basándose en el tipo de datos utilizado en el lado derecho de la asignación.

La inferencia de tipos no significa que Java se esté convirtiendo en un lenguaje de tipado dinámico; más bien, sigue siendo un lenguaje de tipado estático. El tipo de la variable se determina en tiempo de compilación, y una vez que se ha inferido, la variable es tratada como si se hubiera declarado con el tipo explícito.

Algunas consideraciones sobre la inferencia de tipos:

1. **Contexto de Uso:** La inferencia de tipos depende del contexto de uso de la variable. El tipo de la variable se infiere según el tipo de datos con el que está siendo inicializada.
2. **No se aplica a variables de instancia:** La inferencia de tipos se aplica solo a variables locales con inicialización. No se puede utilizar para declarar variables de instancia de una clase.
3. **Claridad y Legibilidad:** Mientras que la inferencia de tipos puede hacer que el código sea más conciso, es importante utilizarla con moderación y en situaciones donde el tipo sea obvio. La claridad y legibilidad del código son fundamentales.

Ejemplo:

```java
var mensaje = "Hola, mundo!"; // Inferencia de tipo String
var numeros = List.of(1, 2, 3, 4, 5); // Inferencia de tipo List<Integer>

```

En resumen, la inferencia de tipos en Java proporciona una manera más concisa de declarar variables locales, reduciendo la redundancia en la escritura del código mientras se mantiene la seguridad de tipos estáticos. Es decir java Adivina el tipo de dato en tiempo de compilación, el tipo de dato es asignado en base a dato que se le da

### **Dándole nombre a un viejo amigo: `Chaining`**

El "`chaining`" en programación se refiere a la práctica de encadenar varias operaciones o métodos en una sola expresión o línea de código. Esta técnica es comúnmente utilizada en programación funcional y en algunos casos en programación orientada a objetos.

En el contexto de la programación funcional, el `chaining` se asocia a menudo con el concepto de "`pipelining`" o "composición de funciones". Consiste en aplicar una serie de funciones o transformaciones de manera secuencial, donde el resultado de una función se pasa como entrada a la siguiente. Esto puede hacer que el código sea más conciso y expresivo.

Ejemplo de `chaining` en programación funcional en Java:

```java
List<String> nombres = Arrays.asList("Juan", "María", "Carlos", "Ana");

// Usando expresiones lambda y chaining
long cantidadLetras = nombres.stream()
                            .filter(nombre -> nombre.startsWith("M"))
                            .mapToInt(String::length)
                            .sum();

System.out.println("La suma de las longitudes de los nombres que comienzan con 'M' es: " + cantidadLetras);

```

En este ejemplo, se utiliza el `chaining` con la API de `Streams` en Java para realizar varias operaciones en una única línea. El método `stream()` crea un flujo de datos a partir de la lista de nombres, y luego se encadenan operaciones como `filter` y `mapToInt` para filtrar los nombres que comienzan con "M" y calcular la suma de las longitudes de esos nombres.

En el contexto de programación orientada a objetos, el `chaining` se refiere a invocar varios métodos de manera secuencial en el mismo objeto. Esto puede ser especialmente útil cuando los métodos retornan el propio objeto, permitiendo encadenar más operaciones.

Ejemplo de `chaining` en Java:

```java
StringBuilder builder = new StringBuilder();

builder.append("Hola").append(" ").append("Mundo").append("!");

String resultado = builder.toString();
System.out.println(resultado);  // Salida: Hola Mundo!

```

En este caso, los métodos `append` del objeto `StringBuilder` devuelven el propio objeto `StringBuilder`, lo que permite encadenar múltiples llamadas en una sola línea.

El `chaining` es una técnica que puede mejorar la legibilidad y concisión del código, pero también debe usarse con moderación para no comprometer la claridad del código.

### **Entendiendo la composición de funciones**

El "pipelining" o "composición de funciones" en Java se refiere a la aplicación secuencial de funciones o transformaciones a través de un flujo de datos, donde el resultado de una función se pasa como entrada a la siguiente. Esto se logra utilizando combinaciones de funciones (o métodos) que procesan datos de manera encadenada.

En Java, la programación funcional y el uso de expresiones lambda facilitan la implementación de este enfoque. La API de Streams en Java es un buen ejemplo de cómo se puede aplicar el "pipelining" para operaciones de procesamiento de datos en colecciones.

Veamos un ejemplo simple de composición de funciones en Java utilizando expresiones lambda y la API de Streams:

```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class Main {
    public static void main(String[] args) {
        List<String> palabras = Arrays.asList("Java", "es", "divertido", "y", "poderoso");

        // Aplicar pipelining o composición de funciones con Streams
        List<String> resultado = palabras.stream()
                .filter(palabra -> palabra.length() > 3)       // Filtrar palabras con longitud mayor a 3
                .map(String::toUpperCase)                     // Convertir a mayúsculas
                .collect(Collectors.toList());                // Recolectar los resultados en una lista

        // Imprimir el resultado
        System.out.println(resultado);
    }
}

```

En este ejemplo:

1. `.stream()`: Convierte la lista de palabras en un flujo de datos (Stream).
2. `.filter(...)`: Filtra las palabras que tienen una longitud mayor a 3 caracteres.
3. `.map(...)`: Convierte cada palabra a mayúsculas.
4. `.collect(...)`: Recolecta los resultados en una lista.

Esto muestra cómo las operaciones se encadenan de manera secuencial, aplicando una tras otra sobre los elementos del flujo de datos. Cada operación toma el resultado de la anterior y lo transforma o filtra según la lógica proporcionada.

Este enfoque facilita la creación de código más declarativo y legible, donde puedes expresar la lógica de procesamiento de datos de manera más concisa y comprensible. La composición de funciones es una parte fundamental de la programación funcional, y Java, especialmente a partir de la versión 8, proporciona características que permiten aprovechar este paradigma de manera efectiva.

### Interfaces del paquete `java.util.function`

Claro, aquí tienes una breve descripción de todas las interfaces en el paquete `java.util.function`:

1. **`BiConsumer<T, U>`:**
    - **Propósito:** Acepta dos argumentos de tipo T y U, realiza operaciones sin devolver resultados.
    - **Uso:** Se utiliza para operaciones que consumen dos argumentos.
    - **Ejemplo:**
        
        ```java
        BiConsumer<String, Integer> imprimirCantidadLetras = (str, num) -> System.out.println("La palabra " + str + " tiene " + num + " letras.");
        imprimirCantidadLetras.accept("Hola", 4);
        
        ```
        
2. **`BiFunction<T, U, R>`:**
    - **Propósito:** Acepta dos argumentos de tipo T y U, devuelve un resultado de tipo R.
    - **Uso:** Se utiliza para transformaciones que involucran dos tipos de datos.
    - **Ejemplo:**
        
        ```java
        BiFunction<Integer, Integer, Integer> suma = (a, b) -> a + b;
        int resultado = suma.apply(3, 4);
        
        ```
        
3. **`BinaryOperator<T>`:**
    - **Propósito:** Es una especialización de `BiFunction` donde los dos argumentos y el resultado son del mismo tipo T.
    - **Uso:** Se utiliza para operaciones binarias que comparten el mismo tipo de entrada y salida.
    - **Ejemplo:**
        
    ```java
    BinaryOperator<Integer> multiplicacion = (a, b) -> a * b;
    int resultado = multiplicacion.apply(5, 3);
        
    ```
        
    - **Propósito:** Evalúa un predicado sobre dos argumentos de tipo T y U, devuelve un valor booleano.
4. **`BiPredicate<T, U>`:**
    - **Uso:** Se utiliza para evaluar condiciones que involucran dos tipos de datos.
    - **Ejemplo:**
        
```java
BiPredicate<String, Integer> esLongitudCorrecta = (str, num) -> str.length() == num;
boolean resultado = esLongitudCorrecta.test("Hola", 4);     
```
        
5. **`BooleanSupplier`:**
    - **Propósito:** No toma argumentos y devuelve un valor booleano.
    - **Uso:** Se utiliza para proveer valores booleanos sin tomar parámetros.
    - **Ejemplo:**
        
```java
BooleanSupplier obtenerValor = () -> true;
boolean resultado = obtenerValor.getAsBoolean();
```
        
6. **`Consumer<T>`:**
    - **Propósito:** Acepta un argumento de tipo T y realiza operaciones sin devolver resultados.
    - **Uso:** Se utiliza para operaciones que consumen un solo argumento.
    - **Ejemplo:**
        
```java
Consumer<String> imprimirMensaje = mensaje -> System.out.println(mensaje);
imprimirMensaje.accept("Hola, mundo!");       
```
        
7. **`DoubleBinaryOperator`, `DoubleConsumer`, `DoubleFunction<R>`, `DoublePredicate`, `DoubleSupplier`, `DoubleToIntFunction`, `DoubleToLongFunction`, `DoubleUnaryOperator`:**
    - Son interfaces especializadas para operaciones con valores de tipo `double`.
8. **`Function<T, R>`:**
    - **Propósito:** Acepta un argumento de tipo T y devuelve un resultado de tipo R.
    - **Uso:** Se utiliza para transformar un tipo de dato en otro.
    - **Ejemplo:**
        
```java
Function<Integer, String> convertirAString = num -> String.valueOf(num);
String resultado = convertirAString.apply(42);
```
        
9. **`IntBinaryOperator`, `IntConsumer`, `IntFunction<R>`, `IntPredicate`, `IntSupplier`, `IntToDoubleFunction`, `IntToLongFunction`, `IntUnaryOperator`:**
    - Son interfaces especializadas para operaciones con valores de tipo `int`.
10. **`LongBinaryOperator`, `LongConsumer`, `LongFunction<R>`, `LongPredicate`, `LongSupplier`, `LongToDoubleFunction`, `LongToIntFunction`, `LongUnaryOperator`:**
    - Son interfaces especializadas para operaciones con valores de tipo `long`.
11. **`ObjDoubleConsumer<T>`, `ObjIntConsumer<T>`, `ObjLongConsumer<T>`:**
    - Aceptan un objeto de tipo T y un valor primitivo, pero no devuelven resultados.
    - Se utilizan para operaciones que consumen un objeto y un valor primitivo.
12. **`Predicate<T>`:**
    - **Propósito:** Evalúa un predicado sobre un solo argumento de tipo T y devuelve un valor booleano.
    - **Uso:** Se utiliza para realizar pruebas y devolver un valor booleano.
    - **Ejemplo:**
        
	```java
	Predicate<Integer> esPar = num -> num % 2 == 0;
	boolean resultado = esPar.test(6);
	```
        
13. **`Supplier<T>`:**
    - **Propósito:** No toma argumentos y suministra un resultado de tipo T.
    - **Uso:** Se utiliza para generar o proporcionar valores.
    - **Ejemplo:**
        
	```java
	Supplier<Double> obtenerNumeroAleatorio = () -> Math.random();
	double numeroAleatorio = obtenerNumeroAleatorio.get();
	```
        
14. **`ToDoubleBiFunction<T, U>`, `ToDoubleFunction<T>`, `ToIntBiFunction<T, U>`, `ToIntFunction<T>`, `ToLongBiFunction<T, U>`, `ToLongFunction<T>`:**
    - Convierten objetos de tipo T en valores primitivos (`double`, `int`, `long`).
15. **`UnaryOperator<T>`:**
    - **Propósito:** Es una especialización de `Function` donde el argumento y el resultado son del mismo tipo T.
    - **Uso:** Se utiliza para operaciones unarias que comparten el mismo tipo de entrada y salida.
    - **Ejemplo:**
        
    ```java
    UnaryOperator<String> agregarSaludo = mensaje -> "Hola, " + mensaje;
    String resultado = agregarSaludo.apply("mundo");
    ```
        
## Efectos secundarios observables

Estas interfaces forman la base de la programación funcional en Java y proporcionan una manera concisa y expresiva de trabajar con funciones y expresiones lambda en el lenguaje. Pueden ser utilizadas en una variedad de contextos, como Streams, para realizar operaciones más efectivas y legibles en colecciones de datos