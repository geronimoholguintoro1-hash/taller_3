# taller_3
Definición de Diagrama de Clases: Es la vista estática de un sistema UML que define clases, atributos, métodos y sus relaciones
Estructura del rectángulo UML: Divide la clase en 3 compartimentos verticales: Nombre (arriba, único obligatorio), Atributos (centro) y Métodos (abajo)
Sintaxis de declaración: En UML el tipo va después del nombre (nombre: tipo), mientras que en Java va antes (tipo nombre).
Símbolos de visibilidad UML:
   * + = Pública (public)
   * - = Privada (private)
   * # = Protegida (protected)
   * ~ = De paquete / Default (sin modificador en Java)
Regla de encapsulamiento: De más restringido a más abierto: private < ~ (paquete) < protected < public. Se debe priorizar siempre el nivel más privado
Interfaces en Java: Sus miembros son explícita o implícitamente públicos (public). Sus atributos son siempre public static final (constantes)
Clases de Nivel Superior (Top-Level): Solo pueden ser public o de paquete (package-private). Nunca private ni protected. Un archivo .java solo puede tener una clase pública con el mismo nombre del archivo
Clases Anidadas (Nested Classes): Se declaran dentro de otra clase, no generan archivo .java propio y sí pueden ser private o protected En UML se representan con el símbolo ⊕ (círculo con cruz)
Herencia Sellada en Java (sealed y permits):
   * Concepto: Permite a una clase o interfaz definir explícitamente qué clases pueden heredar de ella
   * Subclases permitidas: Tienen la obligación de declararse bajo una de tres modalidades:
     * final: Cierra la herencia; nadie más puede heredar de ella
     * sealed: Vuelve a restringir la herencia especificando sus propios permits
     * non-sealed: Reabre la herencia, permitiendo que cualquier clase la extienda
Representación en UML: Se dibuja como una generalización normal (triángulo hueco) anotando {sealed} en la superclase. De forma opcional, se marca cada subclase con {final}, {sealed} o {non-sealed}
Sistema de Módulos de Java (JPMS):
   * Definición: Agrupa paquetes en módulos para brindar un nivel de control de acceso y encapsulamiento fuerte por encima de public/private
   * Archivo de configuración: Se define en el archivo module-info.java en la raíz del módulo
Directivas principales:
     * exports paquete;: Hace visibles los tipos públicos de ese paquete a otros módulos
     * exports paquete to moduloA;: Exportación cualificada hacia módulos específicos
     * requires modulo;: Declara dependencia de otro módulo
     * requires transitive modulo;: Propaga la dependencia hacia quienes dependan de este módulo
     * opens paquete;: Permite acceso por reflexión en tiempo de ejecución
  Tipos de Flechas y Relaciones en UML:
   * Herencia / Generalización (extends): Línea sólida con triángulo hueco
   * Realización / Implementación (implements): Línea punteada con triángulo hueco
   * Asociación: Línea sólida con flecha abierta (representa un atributo que referencia a otra clase)
   * Dependencia: Línea punteada con flecha abierta (uso temporal como parámetro o variable local)
   * Agregación: Línea sólida con rombo hueco ("tiene", la parte existe independientemente del todo)
   * Composición: Línea sólida con rombo lleno ("tiene", la parte no vive sin el todo)
  Asociación Unidireccional:
   * Concepto: Solo una de las clases conoce a la otra; la relación navega en un único sentido
   * Implementación: La clase de origen incluye un atributo del tipo de la clase destino, mientras que la clase destino no guarda ninguna referencia de vuelta

// Pais.java
public class Pais {
    private String nombre;
    private Ciudad capital;
}

// Ciudad.java
public class Ciudad {
    private String nombre;
    private Pais pais;
}

// Empleado.java
public class Empleado {
    private String nombre;
    private Empleado jefe;
}

// Aula.java
public class Aula {
    private String codigo;
    private Proyector proyector;
}

// Proyector.java
public class Proyector {
    private String marca;
}

// Persona.java
public class Persona {
    private String nombre;
    private Corazon corazon = new Corazon();
}

// Corazon.java
public class Corazon {
    private int ritmo;
}

// 7. Multiplicidades (Cliente.java y Pedido.java)
import java.util.List;
import java.util.ArrayList;

public class Cliente {
    private String nombre;
    private List<Pedido> pedidos = new ArrayList<>();
}

public class Pedido {
    private int numero;
}

// 8. Clase asociación (Matricula.java, Estudiante.java, Curso.java)
public class Matricula {
    private Estudiante estudiante;
    private Curso curso;
    private String fecha;
    private double nota;
}

public class Estudiante {
    private String nombre;
}

public class Curso {
    private String titulo;
}

// 9.1 Herencia / generalización (Animal.java y Perro.java)
public class Animal {
    protected String nombre;

    public void comer() {
        System.out.println(nombre + " está comiendo");
    }
}

public class Perro extends Animal {
    public void ladrar() {
        System.out.println(nombre + " está ladrando");
    }
}

// 9.2 Clases y métodos abstractos (Figura.java y Circulo.java)
public abstract class Figura {
    protected String nombre;

    public abstract double area();

    public void describir() {
        System.out.println(nombre + " con area " + area());
    }
}

public class Circulo extends Figura {
    private double radio;

    @Override
    public double area() {
        return 3.1416 * radio * radio;
    }
}
// 9.3 Realización / implementación (implements)
// Volador.java
public interface Volador {
    void volar();
}

// Pajaro.java
public class Pajaro implements Volador {
    private String nombre;

    @Override
    public void volar() {
        System.out.println(nombre + " está volando");
    }
}

// 9.4 Generalización entre interfaces (extends)
// Coleccion.java
public interface Coleccion {
    void agregar();
}

// Lista.java
public interface Lista extends Coleccion {
    void ordenar();
}

// 10.1 Dependencia estándar («use»)
// Reporte.java
public class Reporte {
    public void generar(Datos d) {
        System.out.println(d.total());
    }
}

// Datos.java
public class Datos {
    private int valores;

    public int total() {
        return valores;
    }
}

// 10.2 Dependencia de instanciación («instantiate»)
// Fabrica.java
public class Fabrica {
    public void crear() {
        Producto p = new Producto();
        p.mostrar();
    }
}

// Producto.java
public class Producto {
    private String nombre;

    public void mostrar() {
        System.out.println(nombre);
    }
}

// 10.3 Dependencia de retorno
// Repositorio.java
public class Repositorio {
    public Usuario buscar() {
        return new Usuario();
    }
}

// Usuario.java
public class Usuario {
    private String nombre;
}
// 10.4 Dependencia de parámetro de tipo (genéricos)
// Servicio.java
import java.util.List;

public class Servicio {
    public void procesar(List<Cliente> clientes) {
        for (Cliente c : clientes) {
            c.saludar();
        }
    }
}

// Cliente.java
public class Cliente {
    private String nombre;

    public void saludar() {
        System.out.println("Hola, soy " + nombre);
    }
}

// 11.1 Clase interna (inner class)
// Externa.java
public class Externa {
    private int valor = 10;

    public class Interna {
        public int leer() {
            return valor;
        }
    }
}

// 11.2 Clase estática anidada (static nested)
// Externa.java
public class Externa {
    public static class Anidada {
        private int x;
    }

    public void usar() {
        Anidada a = new Anidada();
    }
}

// 11.3 Clase local
// Procesador.java
public class Procesador {
    public void ejecutar() {
        class Local {
            int paso;
        }
        Local l = new Local();
        l.paso = 1;
    }
}
// 11.4. Clase anónima

// Accion.java
public interface Accion {
    void ejecutar();
}

// Boton.java
public class Boton {
    public void configurar() {
        Accion a = new Accion() { // clase anónima: implementa Accion sin nombre
            @Override
            public void ejecutar() {
                System.out.println("clic");
            }
        };
        a.ejecutar();
    }
}


// 11.5. Dependencia de paquete (import)

// Factura.java
package app.ventas;

import app.modelo.Producto; // dependencia hacia el paquete app.modelo

public class Factura {
    public void agregar(Producto p) {
    }
}


// 12.1. Registros (record) y su composición

// Pedido.java
public record Pedido(Cliente cliente, double total) {
    // Java genera: campos final, constructor,
    // accesores cliente() y total(), equals, hashCode, toString
}

// Cliente.java
public class Cliente {
    private String nombre;
}


// 12.2. Template binding (genéricos en el diagrama)

// Caja.java
public class Caja<T> {
    private T contenido; // T es el parámetro de tipo

    public void guardar(T valor) {
        this.contenido = valor;
    }

    public T obtener() {
        return contenido;
    }
}

// Uso.java
public class Uso {
    public void ejemplo() {
        Caja<String> caja = new Caja<String>(); // binding: T -> String
        caja.guardar("hola");
    }
}
