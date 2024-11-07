<div style="text-align: justify;">

# 🔧 Refactorizar para Mejorar el Código <a id='comienzo'></a>
 
**Fecha:** septiembre de 2024  
**IA:** ChatGPT-4o
---  

- [Volver al Índice Principal de los Ejemplos de uso](/Ejemplos-uso/README.md)

- [Volver al Índice Principal de la Guía](/README.md)

---

## Contexto 💡

La **refactorización** es el proceso de reestructurar el código fuente de un programa sin alterar su funcionalidad externa. Su objetivo principal es mejorar la calidad interna del código, haciéndolo más limpio, legible y eficiente. Durante la refactorización, se eliminan redundancias, se optimiza la estructura, se simplifican las funciones y se mejora la cohesión de los módulos, lo que facilita su comprensión y reduce la complejidad.

Esto no solo permite a los desarrolladores entender y trabajar con el código de manera más eficiente, sino que también disminuye el riesgo de errores al agregar nuevas funcionalidades o corregir problemas, mejorando así el mantenimiento a largo plazo.

### 🧑‍💻 Ejemplo de refactorización con un asistente IA:

A continuación, se propone un ejemplo donde el estudiante (_driver_) elabora un código para la gestión de un juego de adivinar un número, que hace uso de la idea de **vidas** (intentos). En este ejemplo, se implementa la estructura básica de las clases `JuegoConVidas` y `JuegoAdivinaNumero`, donde la primera actúa como plantilla para gestionar los intentos, y la segunda extiende esta lógica para definir las reglas específicas de un juego concreto.

La última clase es la principal donde se prueba la dinámica del juego. Se le solicita al asistente IA que realice un proceso de refactorización sobre las dos clases que forman la jerarquía de clases.

## 💬 Diálogo:

**Driver:** "Dado el código que se presenta a continuación, llevar a cabo un proceso de refactorización que facilite la legibilidad del código y su posterior mantenimiento. No es necesario incluir tratamiento de excepciones, que se llevarán a cabo en etapas posteriores. En concreto, el parámetro del método `juega`, un `String`, se  valida previamente antes de pasarselo al parámetro para que tenga formato de número entero."

<details><summary>Código Original 🚧</summary>

```java
public abstract class JuegoConVidas {
    private int vidas;
    private int vidas_iniciales;
    private int record = 0;

    public JuegoConVidas(int v) {
        vidas = v;
        vidas_iniciales = v;
    }

    public boolean quitaVida() {
        boolean flag = true;
        if (--vidas == 0) {
            System.out.println("No te quedan vidas. Juego terminado");
            flag = false;
        } else {
            System.out.println("vidas restantes " + vidas);
        }
        return flag;
    }

    public void reiniciaPartida() {
        vidas = vidas_iniciales;
    }

    public void actualizaRecord() {
        if (vidas == record)
            System.out.println("has alcanzado el record");
        if (vidas > record) {
            record = vidas;
            System.out.println("Nuevo record: " + record);
        }
    }

    public abstract boolean juega(String cad);
}

public class JuegoAdivinaNumero extends JuegoConVidas {
    private int numeroAdivinar;

    public JuegoAdivinaNumero(int v, int adivinar) {
        super(v);
        numeroAdivinar = adivinar;
    }

    public boolean juega(String a) {
        Integer num = (Integer) Integer.parseInt(a);
        boolean flag;
        if ((num >= 0) && (num <= 10))
            flag = true;
        else {
            System.out.println("fuera de rango");
            flag = false;
        }
        if (flag) {
            if (num == numeroAdivinar) {
                System.out.println("Has acertado!!!!, Enhorabuena");
                actualizaRecord();
                return false;
            } else {
                if ((num > numeroAdivinar))
                    System.out.println("más pequeño");
                else
                    System.out.println("más grande");
                return quitaVida();
            }
        }
        return true;
    }
}

public class PracticaJuego {

    public static void main(String[] args) {
        JuegoConVidas j = new JuegoAdivinaNumero(5, 5);
        jugar(j);
    }

    public static void jugar(JuegoConVidas j) {
        String car;
        j.reiniciaPartida();
        do {
            System.out.println("introduce tu respuesta");
            car = MyInput.readString();
        } while (j.juega(car));
    }
}
```

</details>
<br>

## 🔎 Observer:

"Aquí tienes el código refactorizado, con mejoras en la legibilidad, estructura y nomenclatura. Se han realizado cambios como el uso de convenciones de nombres más consistentes, extracción de métodos para reducir la longitud de las funciones y mejoras en el formato."

<details><summary>Código Refactorizado ✨</summary>

```java
// Clase abstracta JuegoConVidas refactorizada
public abstract class JuegoConVidas {
    private int vidas;
    private int vidasIniciales;
    private int record = 0;

    public JuegoConVidas(int vidas) {
        this.vidas = vidas;
        this.vidasIniciales = vidas;
    }

    public boolean quitarVida() {
        vidas--;
        if (vidas == 0) {
            System.out.println("No te quedan vidas. Juego terminado");
            return false;
        }
        System.out.println("Vidas restantes: " + vidas);
        return true;
    }

    public void reiniciarPartida() {
        vidas = vidasIniciales;
    }

    public void actualizarRecord() {
        if (vidas == record) {
            System.out.println("Has alcanzado el récord");
        } else if (vidas > record) {
            record = vidas;
            System.out.println("Nuevo récord: " + record);
        }
    }

    // Método abstracto que se implementará en las subclases
    public abstract boolean jugar(String entrada);
}

// Clase JuegoAdivinaNumero refactorizada
public class JuegoAdivinaNumero extends JuegoConVidas {
    private int numeroAdivinar;

    public JuegoAdivinaNumero(int vidas, int numeroAdivinar) {
        super(vidas);
        this.numeroAdivinar = numeroAdivinar;
    }

    @Override
    public boolean jugar(String entrada) {
        // Conversión del parámetro String a un número entero
        int numero = Integer.parseInt(entrada);

        // Verificar si el número está dentro del rango válido
        if (!esNumeroValido(numero)) {
            System.out.println("Fuera de rango.");
            return true; // No se pierde vida si el número está fuera de rango
        }

        // Comprobar si el número es el correcto
        if (numero == numeroAdivinar) {
            System.out.println("¡Has acertado! Enhorabuena.");
            actualizarRecord();
            return false; // El juego termina al acertar
        }

        // Sugerencia para ayudar al jugador a encontrar el número correcto
        mostrarPista(numero);
        return quitarVida(); // Se quita una vida si no acertó
    }

    private boolean esNumeroValido(int numero) {
        return numero >= 0 && numero <= 10;
    }

    private void mostrarPista(int numero) {
        if (numero > numeroAdivinar) {
            System.out.println("El número es más pequeño");
        } else {
            System.out.println("El número es más grande");
        }
    }
}
```

</details>
<br>

## 🔄 Refactorización realizada:

1. **Cambio de nombres de métodos y atributos:**
   - `quitaVida` se cambió a `quitarVida` para que el nombre del método sea más descriptivo.
   - `reiniciaPartida` se cambió a `reiniciarPartida` por la misma razón.
   - `actualizaRecord` se cambió a `actualizarRecord`.
   - Los atributos `vidas_iniciales` se cambiaron a `vidasIniciales` para seguir las convenciones de Java.

2. **Extracción de métodos:**
   - Se creó el método `esNumeroValido(int numero)` en la clase `JuegoAdivinaNumero` para validar que el número esté dentro del rango.
   - Se creó el método `mostrarPista(int numero)` para simplificar la lógica y hacer que el método `jugar(String entrada)` sea más claro.

3. **Mejoras de formato y estilo:**
   - Uso de sangrías y espaciado consistentes para facilitar la lectura.
   - Mensajes más claros y específicos para mejorar la interacción con el usuario.

4. **Simplificación de lógica:**
   - Se eliminó la necesidad de utilizar variables temporales como `flag` que hacían que la lógica del método `jugar` fuera más confusa.

### 💬 Comentarios:

El proceso de refactorización se llevó a cabo de manera satisfactoria, introduciendo refactorizaciones tales como el método `esNumeroValido(int numero)`, que puede ser utilizado de manera polimórfica en futuras extensiones.

[- Volver al comienzo del Ejemplo de Uso](#comienzo)
</div>