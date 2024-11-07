<div style="text-align: justify;">

# ♻️ Refactorización para Reutilizar (polimorfismo) <a id='comienzo'></a>
---
**Fecha:** septiembre de 2024  
**IA:** ChatGPT-4o 

- [Volver al Índice Principal de los Ejemplos de uso](/Ejemplos-uso/README.md)
- [Volver al Índice Principal de la Guía](/README.md)

---

## Contexto 💡

Como ya se ha visto, solicitar a la IA que te ayude a refactorizar tu código puede ser beneficioso para mejorar la legibilidad y el mantenimiento del mismo. La IA puede sugerir la creación de métodos adicionales y la separación de la lógica en diferentes clases. Este tipo de mejoras puede tener un efecto muy positivo en el proceso de aprendizaje para entender conceptos tan importantes como el **polimorfismo** (reutilización de código).  

Siguiendo con el ejemplo propuesto anteriormente (refactorización para mejorar el código), se propone extender la clase `JuegoAdivinaNumero` a dos nuevos juegos: `JuegoAdivinaNumeroPar` y `JuegoAdivinaNumeroImpar`. Estas dos nuevas clases representan el mismo juego, pero con restricciones sobre el tipo de números que se pueden utilizar en cada caso. Así, el estudiante puede ver que no necesita reescribir el método `juega` en estas dos últimas clases, sino solo redefinir el método refactorizado `esNumeroValido(...)` para lograr una extensión efectiva.

### Ejemplo de clase `JuegoAdivinaNumeroImpar` 🎮

El caso del juego `JuegoAdivinaNumeroPar` es similar, pero con una comprobación diferente.

## 💬 Diálogo

**Driver:** "Dado el siguiente código refactorizado, procede a extender la clase `JuegoAdivinaNumero` a una clase denominada `JuegoAdivinaNumeroImpar` que implica jugar a adivinar números entre 0 y 10, pero en este caso solo impares."



<details><summary>Código Original 🚧</summary>

```java
// Clase abstracta JuegoConVidas
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

// Clase JuegoAdivinaNumero
public class JuegoAdivinaNumero extends JuegoConVidas {
    protected int numeroAdivinar;

    public JuegoAdivinaNumero(int vidas, int numeroAdivinar) {
        super(vidas);
        this.numeroAdivinar = numeroAdivinar;
    }

    @Override
    public boolean jugar(String entrada) {
        int numero = Integer.parseInt(entrada);

        if (!esNumeroValido(numero)) {
            System.out.println("Fuera de rango.");
            return true; // No se pierde vida si el número está fuera de rango
        }

        if (numero == numeroAdivinar) {
            System.out.println("¡Has acertado! Enhorabuena.");
            actualizarRecord();
            return false; // El juego termina al acertar
        }

        mostrarPista(numero);
        return quitarVida(); // Se quita una vida si no acertó
    }

    protected boolean esNumeroValido(int numero) {
        return numero >= 0 && numero <= 10;
    }

    protected void mostrarPista(int numero) {
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

### Código Extendido ✨

**Observer:** "Para extender la funcionalidad de la clase `JuegoAdivinaNumero` a una nueva clase llamada `JuegoAdivinaNumeroImpar`, que implica jugar a adivinar solo números impares entre 0 y 10, necesitamos hacer algunos ajustes:"

1. Crear la nueva clase `JuegoAdivinaNumeroImpar` que herede de `JuegoAdivinaNumero`.
2. Sobrescribir los métodos necesarios para asegurarnos de que solo se permitan números impares.
3. Modificar la validación para que solo se considere válido un número impar.

<details><summary>Ver el código</summary>

```java
// Nueva clase JuegoAdivinaNumeroImpar que extiende de JuegoAdivinaNumero
public class JuegoAdivinaNumeroImpar extends JuegoAdivinaNumero {

    public JuegoAdivinaNumeroImpar(int vidas, int numeroAdivinar) {
        super(vidas, numeroAdivinar);
        // Asegurar que el número a adivinar sea impar
        if (numeroAdivinar % 2 == 0) {
            throw new IllegalArgumentException("El número a adivinar debe ser impar.");
        }
    }

    @Override
    protected boolean esNumeroValido(int numero) {
        // Validar que el número esté dentro del rango y sea impar
        return numero >= 0 && numero <= 10 && numero % 2 != 0;
    }

    @Override
    public boolean jugar(String entrada) {
        int numero = Integer.parseInt(entrada);

        if (!esNumeroValido(numero)) {
            System.out.println("Número fuera de rango o no es impar.");
            return true; // Continuar jugando sin perder vida
        }

        if (numero == numeroAdivinar) {
            System.out.println("¡Has acertado! Enhorabuena.");
            actualizarRecord();
            return false; // El juego termina al acertar
        }

        mostrarPista(numero);
        return quitarVida(); // Se quita una vida si no acertó
    }
}
```

</details>

### ✏️ Explicación de la Implementación

1. **Clase `JuegoAdivinaNumeroImpar`:**
   - Hereda de `JuegoAdivinaNumero`.
   - En el constructor de la nueva clase, se valida que el número a adivinar sea impar. Si no es así, se lanza una excepción `IllegalArgumentException`.

2. **Sobrescritura del método `esNumeroValido(int numero)`:**
   - Se modifica la validación para que acepte solo números **impares** entre 0 y 10.

3. **Sobrescritura del método `jugar(String entrada)`:**
   - La lógica se ajusta para asegurarse de que solo se juegue con números impares válidos.
   - Si el número no es impar o está fuera de rango, se muestra un mensaje específico.

Con esta implementación, se puede crear un objeto de `JuegoAdivinaNumeroImpar` y pasarle un número impar como objetivo. La validación adicional se encargará de que solo se acepten números impares como respuestas y mantendrá el juego dentro de los límites especificados.

## 🚨 Comentarios

Como se puede observar, el asistente IA nos da una implementación que no hace uso de la refactorización para reutilizar código mediante el **polimorfismo**, mecanismo fundamental en el paradigma de la programación orientada a objetos. El asistente IA no **se da cuenta** del contexto y que no es necesario reescribir el método `jugar` en la clase `JuegoAdivinaNumeroImpar`, sino solo redefinir el método `esNumeroValido(int numero)` para reutilizar el código.

### 🔄 Continuación del Diálogo

**Driver:** "En la implementación haz uso del polimorfismo para reutilizar código."

**Observer:** "Claro, para hacer uso del polimorfismo y reutilizar código, podemos aprovechar la estructura existente de la clase `JuegoAdivinaNumero` y sobrescribir solo aquellos métodos que cambian la lógica, en lugar de reescribir todo el método `jugar`. Vamos a refactorizar la clase `JuegoAdivinaNumeroImpar` para centrarnos en el uso del polimorfismo."

<details><summary>Ver el código</summary>

```java
// Nueva clase JuegoAdivinaNumeroImpar que extiende de JuegoAdivinaNumero
public class JuegoAdivinaNumeroImpar extends JuegoAdivinaNumero {

    public JuegoAdivinaNumeroImpar(int vidas, int numeroAdivinar) {
        super(vidas, numeroAdivinar);
        if (numeroAdivinar % 2 == 0) {
            throw new IllegalArgumentException("El número a adivinar debe ser impar.");
        }
    }

    @Override
    protected boolean esNumeroValido(int numero) {
        // Validar que el número esté dentro del rango y sea impar
        return super.esNumeroValido(numero) && numero % 2 != 0;
    }

    @Override
    protected void mostrarPista(int numero) {
        if (numero % 2 == 0) {
            System.out.println("Recuerda que debes adivinar un número impar.");
        } else {
            super.mostrarPista(numero);
        }
    }
}
```

</details>
<br>

### ✨ Explicación de la Implementación con Polimorfismo

1. **Uso de `super` para reutilizar código:**
   - Se sobrescriben los métodos `esNumeroValido(int numero)` y `mostrarPista(int numero)` en la clase `JuegoAdivinaNumeroImpar` y se reutiliza el código de la clase base `JuegoAdivinaNumero` usando `super.esNumeroValido(numero)`.

2. **Sobrescritura de `esNumeroValido(int numero)`:**
   - Se llama a `super.esNumeroValido(numero)` para verificar que el número esté en el rango permitido (0-10) y luego se añade una condición adicional para verificar que el número sea impar (`numero % 2 != 0`).

3. **Sobrescritura de `mostrarPista(int numero)`:**
   - Se sobrescribe el método `mostrarPista` para agregar una pista específica si el número ingresado es par. Si el número es impar, se usa la implementación de la clase base `super.mostrarPista(numero)`.

### ✅ Ventajas del Enfoque

- **Reutilización de código:** No se repite la lógica del método `jugar` en la clase `JuegoAdivinaNumeroImpar`. La clase `JuegoAdivinaNumeroImpar` reutiliza el método `jugar` de la clase base (`JuegoAdivinaNumero`), aprovechando así el polimorfismo.
- **Extensibilidad:** Las clases `JuegoAdivinaNumero` y `JuegoAdivinaNumeroImpar` se pueden extender con más subclases que alteren la validación de números o el comportamiento del juego sin modificar la estructura original.

Con esta implementación, se mantiene la estructura del código clara, se reduce la duplicación y se hace uso eficiente del polimorfismo para manejar las diferencias entre juegos que comparten una base común.

### ✏️ Comentarios

Con el nuevo apunte, donde se le dice explicitamente que use el polimorfirmo, el asistente IA entiende el propósito y lo aplica correctamente, pero ha sido necesario indicárselo ya que no fue capaz de inferirlo a partir del contexto.

[- Volver al comienzo del Ejemplo de Uso](#comienzo)
</div>