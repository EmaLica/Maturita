---
Data: 17th June 2023
Descrizione: Package, Classi, membri statici, costruttori, tipi primitivi e wrapper, array, oggetti e riferimenti, thread, eccezioni, ereditarietà, overriding e overloading, classe astratte e interfacce, binding dinamico, instanceof, tipi generici, collezioni. Pattern singleton, template method, MVC
---
# Linguaggio Java
### Membri statici
In Java, i membri statici sono **elementi di una classe che appartengono alla classe stessa anziché a istanze specifiche di quella classe**. Ciò significa che i membri statici vengono **condivisi tra tutte le istanze della classe** e possono essere accessibili senza creare un'istanza della classe stessa.

Ci sono due tipi principali di membri statici in Java:
Le variabili statiche sono dichiarate con il modificatore `static` e sono condivise da tutte le istanze della classe. Vengono inizializzate solo una volta, quando la classe viene caricata in memoria, e **mantengono il loro valore finché il programma è in esecuzione**. Sono utilizzate per memorizzare dati comuni a tutte le istanze della classe.
```java
public class MyClass {
    public static int count; // variabile statica

    public MyClass() {
        count++; // incrementa il valore della variabile statica count
    }
}
```
I metodi statici sono dichiarati con il modificatore `static` e possono essere chiamati direttamente dalla classe senza creare un'istanza della stessa. **Possono accedere solo ad altri membri statici della classe e non possono accedere ai membri non statici**.
```java
public class MathUtils {
    public static int add(int a, int b) {
        return a + b;
    }
}
```

### Tipi primitivi e wrapper
In Java, i **tipi primitivi** sono i tipi di base **incorporati nel linguaggio**, mentre i **wrapper sono classi che incapsulano i tipi primitivi fornendo metodi e funzionalità aggiuntive**. I wrapper sono utili quando è necessario trattare i tipi primitivi come oggetti, ad esempio per passarli come argomenti ai metodi che richiedono oggetti o per utilizzare le loro funzionalità aggiuntive come i metodi di conversione.
```java
int number = 42; // tipo primitivo
Integer wrappedNumber = Integer.valueOf(number); // autoboxing

double pi = 3.14; // tipo primitivo
Double wrappedPi = Double.valueOf(pi); // autoboxing

boolean flag = true; // tipo primitivo
Boolean wrappedFlag = Boolean.valueOf(flag); // autoboxing

int unwrappedNumber = wrappedNumber.intValue(); // unboxing
double unwrappedPi = wrappedPi.doubleValue(); // unboxing
boolean unwrappedFlag = wrappedFlag.booleanValue(); // unboxing
```

### Ereditarietà
L'ereditarietà è un concetto fondamentale nella programmazione orientata agli oggetti e anche in Java. Consente di **definire una classe basandosi su un'altra classe esistente**, **ereditando i suoi attributi e metodi**. La classe da cui viene ereditato è chiamata "superclasse" o "classe genitore", mentre la classe che eredita è chiamata "sottoclasse" o "classe figlia".
```java
//Superclasse
public class Veicolo {
    private String marca;

    public void setMarca(String marca) {
        this.marca = marca;
    }

    public String getMarca() {
        return marca;
    }

    public void avvia() {
        System.out.println("Il veicolo è stato avviato.");
    }
}

//Sottoclasse
public class Auto extends Veicolo {
    private int numeroPorte;

    public void setNumeroPorte(int numeroPorte) {
        this.numeroPorte = numeroPorte;
    }

    public int getNumeroPorte() {
        return numeroPorte;
    }

    public void accelerare() {
        System.out.println("L'auto sta accelerando.");
    }
}
```

### Overriding e overloading
###### Overriding
**Overriding** (sovra-scrittura): 
L'overriding si verifica quando **una sottoclasse fornisce una propria implementazione di un metodo già definito nella superclasse**. Per eseguire l'override di un metodo, la sottoclasse deve dichiarare un metodo con la stessa firma (stesso nome, stesso tipo di ritorno e stessi tipi di parametri) della superclasse. L'override permette alla sottoclasse di fornire una specifica implementazione del metodo, sostituendo quella della superclasse.
```java
public class Animal {
    public void makeSound() {
        System.out.println("Il suono generico di un animale.");
    }
}

public class Dog extends Animal {
    @Override
    public void makeSound() {
        System.out.println("Bau bau!");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal animal = new Animal();
        animal.makeSound(); // Output: "Il suono generico di un animale."

        Dog dog = new Dog();
        dog.makeSound(); // Output: "Bau bau!"
    }
}
```

###### Overloading
**Overloading** (sovra-caricamento): 
L'overloading si verifica quando **una classe ha più metodi con lo stesso nome ma con diversi parametri**. I metodi sovraccaricati devono differire per numero, tipo o ordine dei parametri. Possono anche differire per il tipo di ritorno, ma non solo per il tipo di ritorno. L'overloading permette di definire comportamenti diversi per un metodo in base ai parametri passati.
```java
public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }

    public double add(double a, double b) {
        return a + b;
    }
}

public class Main {
    public static void main(String[] args) {
        Calculator calculator = new Calculator();

        int sum1 = calculator.add(2, 3); // Output: 5

        double sum2 = calculator.add(2.5, 3.7); // Output: 6.2
    }
}
```

### Classe astratte e interfacce
###### Classi astratte
Una classe astratta **è una classe che non può essere istanziata direttamente**, ma può essere estesa da altre classi. Può contenere sia **metodi concreti** (con implementazione) che **metodi astratti** (senza implementazione)
```java
public abstract class Shape {
    private String color;

    public Shape(String color) {
        this.color = color;
    }

    public String getColor() {
        return color;
    }

    public abstract double getArea(); // metodo astratto senza implementazione
}

public class Circle extends Shape {
    private double radius;

    public Circle(String color, double radius) {
        super(color);
        this.radius = radius;
    }

    @Override
    public double getArea() {
        return Math.PI * radius * radius;
    }
}
```
###### Interfacce
Un'interfaccia è un contratto che definisce un **insieme di metodi che una classe deve implementare**. A differenza delle classi astratte, le interfacce **non possono contenere implementazioni di metodi**.
```java
public interface Drawable {
    void draw(); // metodo astratto
}

public class Circle implements Drawable {
    private double radius;

    public Circle(double radius) {
        this.radius = radius;
    }

    @Override
    public void draw() {
        System.out.println("Drawing a circle");
    }
}
```


### Binding dinamico
Il binding dinamico, noto anche come late binding o dynamic dispatch, è un **meccanismo utilizzato nel polimorfismo** per **determinare a tempo di esecuzione quale implementazione di un metodo deve essere chiamata**, basandosi sul tipo effettivo dell'oggetto su cui il metodo viene invocato.

In Java, il binding dinamico avviene quando un metodo viene chiamato su un oggetto di una classe specifica, ma la determinazione dell'implementazione del metodo avviene in base al tipo effettivo dell'oggetto a runtime, anziché in base al tipo dichiarato della variabile di riferimento.
```java
public class Animal {
    public void makeSound() {
        System.out.println("Suono generico di un animale");
    }
}

public class Dog extends Animal {
    @Override
    public void makeSound() {
        System.out.println("Bau bau!");
    }
}

public class Cat extends Animal {
    @Override
    public void makeSound() {
        System.out.println("Miao miao!");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal animal1 = new Dog();
        Animal animal2 = new Cat();

        animal1.makeSound(); // Output: "Bau bau!"
        animal2.makeSound(); // Output: "Miao miao!"
    }
}
```

### Istanceof
L'operatore `instanceof` in Java viene utilizzato per **verificare se un oggetto è un'istanza di una determinata classe o se è un'istanza di una classe che implementa un'interfaccia specifica**. Restituisce un valore booleano: `true` se l'oggetto è un'istanza della classe o dell'interfaccia specificata, altrimenti `false`.
```java
public interface Drawable {
    void draw();
}

public class Circle implements Drawable {
    @Override
    public void draw() {
        System.out.println("Disegno un cerchio");
    }
}

public class Rectangle implements Drawable {
    @Override
    public void draw() {
        System.out.println("Disegno un rettangolo");
    }
}

public class Main {
    public static void main(String[] args) {
        Drawable shape1 = new Circle();
        Drawable shape2 = new Rectangle();
        Object object = new Circle();

        System.out.println(shape1 instanceof Circle); // Output: true
        System.out.println(shape2 instanceof Rectangle); // Output: true
        System.out.println(shape2 instanceof Circle); // Output: false
        System.out.println(object instanceof Circle); // Output: true
        System.out.println(object instanceof Rectangle); // Output: false
    }
}
```

### Tipi generici
I tipi generici in Java consentono di creare classi, interfacce e metodi che possono lavorare con **diversi tipi di dati senza specificare il tipo effettivo** in fase di compilazione. Questo offre una maggiore **flessibilità e riutilizzo del codice**.

Classe generica:
```java
public class Box<T> {
    private T content;

    public void setContent(T content) {
        this.content = content;
    }

    public T getContent() {
        return content;
    }
}
```
Metodo generico:
```java
public <T> T findMax(T[] array) {
    T max = array[0];
    for (int i = 1; i < array.length; i++) {
        if (array[i].compareTo(max) > 0) {
            max = array[i];
        }
    }
    return max;
}
```
Interfaccia generica:
```java
public interface List<E> {
    void add(E element);
    E get(int index);
}
```

### Collezioni
Le collezioni in Java forniscono una serie di strutture dati pronte all'uso per **memorizzare e manipolare gruppi di oggetti**. Le collezioni sono implementate tramite interfacce e classi presenti nel framework delle collezioni Java (Java Collections Framework).
- **ArrayList**: Classe che implementa l'interfaccia List e memorizza gli elementi in un array ridimensionabile, consentendo l'accesso agli elementi tramite indici.
- **LinkedList**: Classe che implementa sia le interfacce List che Deque, memorizza gli elementi come una sequenza di nodi collegati, permettendo l'accesso, l'inserimento e la rimozione efficiente di elementi in testa o in coda alla lista.
- **HashSet**: Classe che implementa l'interfaccia Set e utilizza una tabella hash per archiviare gli elementi, non mantiene un ordine specifico e non consente duplicati.
- **TreeSet**: Classe che implementa l'interfaccia SortedSet e utilizza un albero bilanciato per archiviare gli elementi, mantiene gli elementi ordinati in base al valore e consente operazioni di ricerca, inserimento e rimozione efficienti.
- **HashMap**: Classe che implementa l'interfaccia Map e utilizza una tabella hash per memorizzare coppie di chiavi e valori, permette un accesso rapido alle coppie chiave-valore tramite la chiave e non mantiene un ordine specifico delle coppie.
- **TreeMap**: Classe che implementa l'interfaccia SortedMap e utilizza un albero bilanciato per memorizzare coppie di chiavi e valori, mantiene le coppie di chiavi-valori ordinate in base al valore delle chiavi.

### Pattern Singleton
Il pattern Singleton in Java è un **pattern di progettazione creazionale** che garantisce **l'esistenza di una sola istanza di una classe** e fornisce un **punto di accesso globale** a questa istanza.
```java
public class Singleton {
    private static Singleton instance;

    // Costruttore privato per evitare l'istanziazione diretta della classe
    private Singleton() {
    }

    // Metodo statico per ottenere l'istanza Singleton
    public static Singleton getInstance() {
        if (instance == null) {
            synchronized (Singleton.class) {
                if (instance == null) {
                    instance = new Singleton();
                }
            }
        }
        return instance;
    }

    // Altri metodi della classe Singleton
    public void doSomething() {
        // ...
    }
}
```

Nell'implementazione sopra, la classe Singleton ha un **costruttore privato per impedire l'istanziazione** diretta della classe da parte di altre classi. L'unico modo per **ottenere un'istanza della classe** Singleton è utilizzare il metodo `getInstance()`, che restituisce l'istanza esistente se è già stata creata, altrimenti crea una nuova istanza in modo thread-safe utilizzando il double-checked locking.

###### Esempio di utilizzo del Singleton:
```java
Singleton singleton = Singleton.getInstance();
singleton.doSomething();
```

Il pattern Singleton viene spesso utilizzato per **oggetti che devono essere unici nell'applicazione**, ad esempio **logger**, connessioni al database o oggetti di configurazione. È importante notare che il pattern Singleton **non garantisce la sicurezza del thread** in sé, quindi **se l'applicazione utilizza più thread e l'istanza Singleton viene modificata da più thread contemporaneamente**, possono verificarsi **problemi di concorrenza**. In tal caso, è necessario prendere precauzioni aggiuntive per garantire la corretta sincronizzazione o utilizzare un'implementazione alternativa come il Singleton Lazy Holder.

### Template method
Il pattern Template Method in Java è un **pattern comportamentale** che consente di definire il **"scheletro" di un algoritmo in una classe base**, **delegando l'implementazione** di alcuni passaggi specifici alle classi derivate. Il template method definisce l'ordine di esecuzione degli step dell'algoritmo, ma lascia alle sottoclassi il compito di implementare i dettagli specifici di ciascun passo.

```java
public abstract class AbstractClass {
    
    // Template method che definisce l'algoritmo
    public void templateMethod() {
        step1();
        step2();
        step3();
    }
    
    // Passo 1: implementazione generica nella classe base
    protected void step1() {
        System.out.println("Step 1: Eseguito nella classe base");
    }
    
    // Passo 2: da implementare nelle sottoclassi
    protected abstract void step2();
    
    // Passo 3: implementazione generica nella classe base
    protected void step3() {
        System.out.println("Step 3: Eseguito nella classe base");
    }
}

public class ConcreteClass extends AbstractClass {
    
    // Implementazione specifica del passo 2
    protected void step2() {
        System.out.println("Step 2: Eseguito nella classe derivata");
    }
}
```
Il pattern Template Method permette di strutturare l'algoritmo generico in una classe base e lascia la possibilità alle sottoclassi di **personalizzare alcuni passaggi** senza dover ripetere il codice comune. Questo **favorisce l'estensibilità e la riutilizzabilità del codice**.

### Template MVC
Il pattern MVC (Model-View-Controller) è un **pattern architetturale** ampiamente utilizzato per organizzare il codice di un'applicazione. Nel contesto di Java, il pattern MVC può essere implementato utilizzando classi e interfacce.

1. **Modello** (Model) &rarr; Il modello **rappresenta i dati e la logica di business dell'applicazione**. È responsabile per l'accesso e la manipolazione dei dati. Può contenere metodi per leggere, scrivere e aggiornare i dati.
```java
public class Model {
    private String data;

    public String getData() {
        return data;
    }

    public void setData(String data) {
        this.data = data;
    }
}
```
2. **Vista** (View) &rarr; La vista **visualizza i dati e interagisce con l'utente**. È responsabile per la presentazione grafica dei dati e per la ricezione degli input dell'utente.
```java
public class View {
    public void displayData(String data) {
        System.out.println("Data: " + data);
    }

    public String getInput() {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter data: ");
        return scanner.nextLine();
    }
}
```
3. **Controller**: Il controller fa da **mediatore tra il modello e la vista**. Gestisce gli eventi dell'utente, interagisce con il modello per ottenere o aggiornare i dati e aggiorna la vista per riflettere le modifiche.
```java
public class Controller {
    private Model model;
    private View view;

    public Controller(Model model, View view) {
        this.model = model;
        this.view = view;
    }

    public void updateData() {
        String inputData = view.getInput();
        model.setData(inputData);
    }

    public void displayData() {
        String data = model.getData();
        view.displayData(data);
    }
}
```

###### Esempio di utilizzo:
```java
public class Main {
    public static void main(String[] args) {
        Model model = new Model();
        View view = new View();
        Controller controller = new Controller(model, view);

        controller.updateData();
        controller.displayData();
    }
}
```

Il pattern MVC aiuta a **separare i diversi aspetti dell'applicazione**, rendendo il **codice più modulare**, **organizzato e facile da mantenere**. Il modello gestisce i dati, la vista si occupa dell'interfaccia utente e il controller gestisce la logica dell'applicazione.