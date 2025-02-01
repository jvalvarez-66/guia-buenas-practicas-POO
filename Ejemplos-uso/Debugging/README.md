# Utilizar la IA para mejorar la deteccion de errores
**Fecha:** febrero de 2024 <br>
**IA:** ChatGPT-4o

- [Volver al Índice Principal de los Ejemplos de Uso](/Ejemplos-uso/README.md)
- [Volver al Índice Principal de la Guía](/README.md)
## Contexto 💡
La idea es utilizar la IA para que seas capaz de mejorar con la deteccion de errores, pudiendo ser estos logicos, de sintaxis o incluso de como esta estructurado el codigo.
En este caso se han puesto 3 casos de pruebas que van aumentado en dificultad.

## 💬 Diálogo

## Nivel facil
### Pregunta Usuario
Generame un prgrama facil el cual contenga errores, sin decirme cuales son, haz que los errores sean tanto sintacticos como logicos

<details>
<summary>Contestacion de ChatGPT</summary>
<br>

Aquí tienes un programa sencillo en Java que contiene algunos errores tanto sintácticos como lógicos:
```Java
import java.util.Scanner;

public class Calculadora {
    public static void main(String args) { 
        Scanner scanner = new Scanner(System.in);

        System.out.println("Bienvenido a la calculadora básica.");
        System.out.println("Por favor, introduce el primer número:");
        double numero1 = scanner.nextLine();

        System.out.println("Introduce el segundo número:");
        double numero2 = scanner.nextInt();

        System.out.println("Elige una operación: suma, resta, multiplica, divide");
        String operacion = scanner.nextLine();

        double resultado;
        if (operacion == "suma") { 
            resultado = numero1 + numero2;
        } else if (operacion.equals("resta")) {
            resultado = numero1 + numero2; 
        } else if (operacion.equals("multiplica")) {
            resultado = numero1 * numero2;
        } else if (operacion.equals("divide")) {
            resultado = numero1 / 0; 
        } else {
            System.out.println("Operación no válida");
            resultado = 0;
        }

        System.out.println("El resultado es: " + resultado);
        scanner.close();
    }
}
```
</details>
Este programa tiene errores que abarcan diferentes aspectos. Intenta identificar y corregir los errores para que el programa funcione correctamente. ¡Diviértete resolviendo el reto!

### Pregunta  Usuario
Para capturar el primer numero tendrias que hacerun wrap a double y la division nunca puede ser por 0, tambien en main se deberia de poner con dos ( ) para que quedara asi main(String ( ) args)

### Respuesta Chatgpt:
¡Correcto! Has identificado varios de los errores en el programa. Aquí hay un desglose de los errores que mencionaste y otros que podrías encontrar:
<ol>
   <li> Declaración incorrecta del método main:
    El método principal debería declararse como public static void main(String[] args) en lugar de public static void main(String args).</li>

   <li>  Captura incorrecta del número:
    Usar scanner.nextLine() para leer un número no es correcto. La solución sería usar Double.parseDouble(scanner.nextLine()) para convertir la entrada a double.</li>

   <li>  División por cero:
    En el caso de la operación de división, no puedes dividir por cero. Es necesario manejar este caso para evitar un error de ejecución.</li>

   <li>  Comparación incorrecta de cadenas:
    La comparación de cadenas con == no funciona como se espera en Java. Debería usarse .equals() o .equalsIgnoreCase() para comparar cadenas correctamente.</li>

   <li>  Lógica incorrecta en la resta:
    En el bloque de la operación "resta", el código realiza una suma en lugar de una resta.</li> 
</ol>

## Nivel Medio

### Pregunta Usuario
Genérame un prgrama de dificultad media el cual contenga errores, sin decirme cuáles son, haz que los errores sean tanto sintácticos como logicos
<details>
<summary>Contestacion de ChatGPT</summary>
<br>

Aquí tienes un programa de dificultad media en Java que contiene errores tanto sintácticos como lógicos. ¡Buena suerte encontrándolos! 🚀
```Java
import java.util.Scanner;

public class GestorDeEstudiantes {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("Bienvenido al Gestor de Estudiantes");
        System.out.print("¿Cuántos estudiantes deseas registrar? ");
        int cantidadEstudiantes = scanner.nextInt();

        String[] nombres = new String[cantidadEstudiantes];
        double[] calificaciones = new double[cantidadEstudiantes];

        // Registro de estudiantes
        for (int i = 0; i <= cantidadEstudiantes; i++) {
            System.out.print("Introduce el nombre del estudiante " + (i + 1) + ": ");
            nombres[i] = scanner.nextLine();

            System.out.print("Introduce la calificación del estudiante " + (i + 1) + ": ");
            calificaciones[i] = scanner.nextDouble();
        }

        // Cálculo de estadísticas
        double suma = 0;
        for (int i = 0; i < cantidadEstudiantes; i++) {
            suma += calificaciones[i];
        }
        double promedio = suma / cantidadEstudiantes;

        System.out.println("\nEstudiantes registrados:");
        for (int i = 0; i < cantidadEstudiantes; i++) {
            System.out.println("Nombre: " + nombres[i] + ", Calificación: " + calificaciones[i]);
        }

        System.out.println("\nPromedio general: " + promedio);

        // Búsqueda de estudiante con la calificación más alta
        String mejorEstudiante = "";
        double mejorCalificacion = 0;

        for (int i = 1; i < cantidadEstudiantes; i++) { 
            if (calificaciones[i] > mejorCalificacion) {
                mejorCalificacion = calificaciones[i];
                mejorEstudiante = nombres[i];
            }
        }

        System.out.println("El estudiante con la mejor calificación es: " + mejorEstudiante + " con " + mejorCalificacion);

        scanner.close();
    }
}
```
</details>

### Respuesta Usuario
La búsqueda del estudiante con más nota es incorrecto, logica incorrecta registrando estudiantes en el bucle
### Respuesta ChatGPT
¡Exacto! Identificaste con precisión dos errores importantes en el programa. Analicemos los problemas que mencionaste y otros que también podrían estar presentes:
<ol>
<li> Búsqueda del estudiante con la mejor calificación

El bucle comienza con i = 1 y la variable mejorCalificacion está inicializada en 0. Esto hace que si la primera calificación es menor que 0 (aunque improbable), el resultado sería incorrecto. Además, el primer estudiante no se evalúa correctamente en la búsqueda.
</li><li>Lógica incorrecta en el registro de estudiantes

Dentro del bucle for, se usa scanner.nextLine() después de scanner.nextInt(), lo que genera un problema con el salto de línea residual. Esto provoca un comportamiento inesperado al leer los nombres de los estudiantes.</li>
</ol>
Programa Corregido

Aquí tienes una versión corregida con las observaciones aplicadas:
<details>
<summary>Contestacion de ChatGPT</summary>
<br>

```Java
import java.util.Scanner;

public class GestorDeEstudiantes {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("Bienvenido al Gestor de Estudiantes");
        System.out.print("¿Cuántos estudiantes deseas registrar? ");
        int cantidadEstudiantes = scanner.nextInt();
        scanner.nextLine(); // Consumir el salto de línea residual

        String[] nombres = new String[cantidadEstudiantes];
        double[] calificaciones = new double[cantidadEstudiantes];

        // Registro de estudiantes
        for (int i = 0; i < cantidadEstudiantes; i++) { // Corregido límite del bucle
            System.out.print("Introduce el nombre del estudiante " + (i + 1) + ": ");
            nombres[i] = scanner.nextLine(); // Ahora funciona correctamente

            System.out.print("Introduce la calificación del estudiante " + (i + 1) + ": ");
            calificaciones[i] = scanner.nextDouble();
            scanner.nextLine(); // Consumir salto de línea residual después de nextDouble
        }

        // Cálculo de estadísticas
        double suma = 0;
        for (int i = 0; i < cantidadEstudiantes; i++) {
            suma += calificaciones[i];
        }
        double promedio = suma / cantidadEstudiantes;

        System.out.println("\nEstudiantes registrados:");
        for (int i = 0; i < cantidadEstudiantes; i++) {
            System.out.println("Nombre: " + nombres[i] + ", Calificación: " + calificaciones[i]);
        }

        System.out.println("\nPromedio general: " + promedio);

        // Búsqueda de estudiante con la calificación más alta
        String mejorEstudiante = nombres[0];
        double mejorCalificacion = calificaciones[0];

        for (int i = 1; i < cantidadEstudiantes; i++) { // Corregido índice inicial
            if (calificaciones[i] > mejorCalificacion) {
                mejorCalificacion = calificaciones[i];
                mejorEstudiante = nombres[i];
            }
        }

        System.out.println("El estudiante con la mejor calificación es: " + mejorEstudiante + " con " + mejorCalificacion);

        scanner.close();
    }
}

```
</details>

## Nivel Alto
### Pregunta del Usuario
Generame un prgrama de dificultad alta el cual contenga todo tipo de errores logicos sintacticos o malas uilizaciones de patrones, multiples clases, y generacidad, decirme cuales son.

<details>
<summary>Contestacion de ChatGPT</summary>

```Java
  import java.util.ArrayList;
  import java.util.List;

// Clase genérica para gestionar empleados
class Gestor<T> {
    private List<T> items;

    // Constructor
    public Gestor() {
        items = new ArrayList<>();
    }

    // Agregar elemento a la lista
    public void addEmpleado(T empleado) {
        items.add(empleado);
    }

    // Obtener el empleado por índice
    public T getEmpleado(int index) {
        return items.get(index); 
    }

    // Mostrar todos los empleados
    public void mostrarEmpleados() {
        for (T empleado : items) {
            System.out.println(empleado.toString()); 
        }
    }
}

// Clase base abstracta para empleados
abstract class Empleado {
    private String nombre;
    private double salario;

    public Empleado(String nombre, double salario) {
        this.nombre = nombre;
        this.salario = salario;
    }

    public String getNombre() {
        return nombre;
    }

    public double getSalario() {
        return salario;
    }

    public void setSalario(double salario) {
        if (salario >= 0) {
            salario = salario; 
        }
    }

    @Override
    public String toString() {
        return "Empleado: " + nombre + ", Salario: " + salario;
    }
}

// Clase concreta para un tipo de empleado
class Programador extends Empleado {
    private String lenguaje;

    public Programador(String nombre, double salario, String lenguaje) {
        super(nombre, salario);
        this.lenguaje = lenguaje;
    }

    public String getLenguaje() {
        return lenguaje;
    }

    @Override
    public String toString() {
        return super.toString() + ", Lenguaje: " + lenguaje;
    }
}

// Clase principal
public class Main {
    public static void main(String args) {
        Gestor<Empleado> gestor = new Gestor<>();

        // Crear empleados
        gestor.addEmpleado(new Programador("Alice", 50000, "Java"));
        gestor.addEmpleado(new Empleado("Bob", 40000) {
            @Override
            public void setSalario(double salario) {
                super.setSalario(salario);
            }
        });

        gestor.addEmpleado(new Programador("Charlie", -60000, "Python"));

        // Mostrar empleados
        System.out.println("Lista de empleados:");
        gestor.mostrarEmpleados();

        // Intentar obtener un empleado fuera de rango
        System.out.println("Empleado en la posición 5:");
        System.out.println(gestor.getEmpleado(5)); 
    }
}
```
</details>

### Respuesta Usuario <br>
Main mal declarado, permite un salario negativo de un trabajador,intento de instanciar una clase empleado que es abstracta, setSalario no modifica el salario correctamente y hay atributos definidos que no se usan

### Respuesta Chatgpt:

<ol>
 <li> main mal declarado
El método principal está declarado incorrectamente como main(String args) en lugar de main(String[] args).</li>
<li>
Salario negativo permitido
No hay validación adecuada para evitar que un empleado tenga un salario negativo al instanciarlo.</li>
<li>
Instanciación de clase abstracta
Se intenta instanciar la clase abstracta Empleado directamente, lo cual no es permitido.</li>
<li>
setSalario no modifica el salario correctamente
Dentro del método, el valor del salario no se asigna al atributo de la clase debido al uso incorrecto de la referencia.</li>
<li>
Atributos definidos pero no utilizados
Por ejemplo, se define el atributo lenguaje en la clase Programador, pero su implementación no está correctamente justificada o aprovechada.</li>
</ol>

<details>
<summary>Correccion de ChatGPT</summary>

```Java
import java.util.ArrayList;
import java.util.List;

// Clase genérica para gestionar empleados
class Gestor<T extends Empleado> { // Restricción en generics para aceptar solo subclases de Empleado
    private List<T> items;

    // Constructor
    public Gestor() {
        items = new ArrayList<>();
    }

    // Agregar elemento a la lista
    public void addEmpleado(T empleado) {
        items.add(empleado);
    }

    // Obtener el empleado por índice
    public T getEmpleado(int index) {
        if (index >= 0 && index < items.size()) {
            return items.get(index);
        } else {
            throw new IndexOutOfBoundsException("Índice fuera de rango");
        }
    }

    // Mostrar todos los empleados
    public void mostrarEmpleados() {
        for (T empleado : items) {
            System.out.println(empleado);
        }
    }
}

// Clase base abstracta para empleados
abstract class Empleado {
    private String nombre;
    private double salario;

    public Empleado(String nombre, double salario) {
        this.nombre = nombre;
        setSalario(salario); // Validación en el setter
    }

    public String getNombre() {
        return nombre;
    }

    public double getSalario() {
        return salario;
    }

    public void setSalario(double salario) {
        if (salario >= 0) {
            this.salario = salario;
        } else {
            throw new IllegalArgumentException("El salario no puede ser negativo");
        }
    }

    @Override
    public String toString() {
        return "Empleado: " + nombre + ", Salario: $" + salario;
    }
}

// Clase concreta para un tipo de empleado
class Programador extends Empleado {
    private String lenguaje;

    public Programador(String nombre, double salario, String lenguaje) {
        super(nombre, salario);
        this.lenguaje = lenguaje;
    }

    public String getLenguaje() {
        return lenguaje;
    }

    @Override
    public String toString() {
        return super.toString() + ", Lenguaje: " + lenguaje;
    }
}

// Clase principal
public class Main {
    public static void main(String[] args) { // Declaración correcta de main
        Gestor<Empleado> gestor = new Gestor<>();

        // Crear empleados
        gestor.addEmpleado(new Programador("Alice", 50000, "Java"));
        gestor.addEmpleado(new Programador("Charlie", 60000, "Python"));

        // Mostrar empleados
        System.out.println("Lista de empleados:");
        gestor.mostrarEmpleados();

        // Intentar obtener un empleado fuera de rango
        try {
            System.out.println("Empleado en la posición 5:");
            System.out.println(gestor.getEmpleado(5)); // Manejado con excepción
        } catch (IndexOutOfBoundsException e) {
            System.out.println("Error: " + e.getMessage());
        }

        // Intentar agregar un empleado con salario negativo
        try {
            gestor.addEmpleado(new Programador("Bob", -40000, "C++")); // Lanzará excepción
        } catch (IllegalArgumentException e) {
            System.out.println("Error al agregar empleado: " + e.getMessage());
        }
    }
}

```
</details>