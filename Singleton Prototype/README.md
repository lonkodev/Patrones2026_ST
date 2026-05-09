
# 📚 Unidad 2: Patrones de Diseño

---

## ✅ Contenidos abordados en clase

### 🔁 Patrón Singleton (Repaso)
- Vimos cómo garantizar que una clase tenga **una única instancia global**.
- Ejemplo en Java con `ContadorGlobal`.

```java
class ContadorGlobal {
    private static ContadorGlobal instancia;
    private int contador = 0;

    private ContadorGlobal() {
        System.out.println("Contador iniciado");
    }

    public static ContadorGlobal getInstancia() {
        if (instancia == null) {
            instancia = new ContadorGlobal();
        }
        return instancia;
    }

    public void incrementar() {
        contador++;
    }

    public int obtenerValor() {
        return contador;
    }
}

public class DemoSingleton {
    public static void main(String[] args) {
        ContadorGlobal a = ContadorGlobal.getInstancia();
        a.incrementar();
        a.incrementar();

        ContadorGlobal b = ContadorGlobal.getInstancia();
        b.incrementar();
        b.incrementar();
        b.incrementar();
        b.incrementar();

        System.out.println("Valor final: " + b.obtenerValor());

        if (a == b) {
            System.out.println("✅ Mismo objeto compartido (Singleton)");
        } else {
            System.out.println("❌ Diferentes instancias (NO Singleton)");
        }
    }
}

```
- Si queremos romperlo solo debemos cambiar la visibilidad a `private ContadorGlobal()`
- Luego cambiar `ContadorGlobal.getInstancia();` por `new ContadorGlobal();` 

### 🧬 Patrón Prototype
- Se explicó cómo **clonar objetos** sin usar `new`.
- Analizamos diferencias entre:
  - `Shallow Copy` (copia superficial, comparte referencias)
  - `Deep Copy` (copia independiente)
- Ejemplo práctico: clase `Caja` clonando listas.

```java
import java.util.ArrayList;
import java.util.List;

class Caja implements Cloneable {
    public List<String> elementos = new ArrayList<>();

    public void agregar(String item) {
        elementos.add(item);
    }

    @Override
    public Caja clone() {
        try {
            return (Caja) super.clone();
        } catch (CloneNotSupportedException e) {
            throw new AssertionError();
        }
    }
}

public class DemoPrototype {
    public static void main(String[] args) {
        Caja caja1 = new Caja();
        caja1.agregar("Lapiz");

        Caja caja2 = caja1.clone();
        caja2.agregar("Regla");

        System.out.println("Caja 1: " + caja1.elementos);
        System.out.println("Caja 2: " + caja2.elementos);

    }

}
```

- Si queremos romperlo solo debemos cambiar ` Caja clone()` `return (Caja) super.clone();`
- Por
```java
Caja caja = (Caja) super.clone();
caja.elementos = new ArrayList<>(this.elementos);
return caja;
```

---
