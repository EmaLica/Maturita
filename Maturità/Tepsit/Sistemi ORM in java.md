---
Data: 19th June 2023
Descrizione: Definizione di un ORM, JPA, annotazioni principali (@Entity, @NamedQueries, @NamedQuery, @id, @GeneratedValue, @OneToMany, @ManyToOne, @ManyToMany), relazioni uno a molti e molti a molti unidirezionale e bidirezionale. Uso del database Derby
---
# ORM in Java
Un **ORM** (Object-Relational Mapping) **è una tecnica che consente di mappare le entità e le relazioni di un database relazionale** a oggetti nel linguaggio di programmazione utilizzato, facilitando l'interazione tra il database e l'applicazione.
**L'ORM agisce come uno strato di astrazione tra l'applicazione e il database**, consentendo di manipolare i dati come oggetti senza dover scrivere query SQL manualmente. L'ORM si occupa di tradurre le operazioni sugli oggetti nell'applicazione in operazioni corrispondenti sul database.
Di seguito sono elencati i principali concetti e componenti che costituiscono un ORM:

1. **Entità**: Le entità rappresentano gli oggetti del dominio dell'applicazione che devono essere persistiti nel database. Ogni entità corrisponde a una tabella nel database e ogni istanza dell'entità corrisponde a una riga nella tabella.
2. **Relazioni**: Le relazioni tra le entità rappresentano le associazioni o le dipendenze tra gli oggetti nel dominio dell'applicazione. Le relazioni possono essere uno-a-uno, uno-a-molti o molti-a-molti e vengono tradotte in relazioni tra tabelle nel database.
3. **Mapping delle entità**: Il mapping delle entità definisce la corrispondenza tra le proprietà degli oggetti nel linguaggio di programmazione e le colonne nel database. Vengono definite annotazioni o configurazioni per stabilire quali proprietà corrispondono a quali colonne.
4. **Operazioni CRUD**: L'ORM fornisce metodi per eseguire le operazioni CRUD (Create, Read, Update, Delete) sulle entità. Questi metodi astraggono le operazioni SQL sottostanti, consentendo all'applicazione di lavorare direttamente con gli oggetti.
5. **Gestione delle transazioni**: L'ORM gestisce le transazioni per garantire l'integrità dei dati. Le transazioni possono essere gestite in modo esplicito, in cui l'applicazione inizia, conferma o annulla le transazioni, oppure in modo implicito, in cui l'ORM gestisce automaticamente le transazioni per ogni operazione.
6. **Query**: L'ORM fornisce un linguaggio o una sintassi per eseguire query complesse sul database senza scrivere SQL diretto. Spesso, un ORM offre un linguaggio di query specifico dell'ORM che consente di esprimere le operazioni di interrogazione in modo più intuitivo utilizzando le proprietà e le relazioni degli oggetti.
7. **Cache**: Alcuni ORM forniscono funzionalità di caching per migliorare le prestazioni delle operazioni di lettura dei dati. La cache memorizza gli oggetti letti dal database in memoria, riducendo così le query al database stesso.

Utilizzare un ORM semplifica lo sviluppo di applicazioni che interagiscono con il database, consentendo di concentrarsi sulla logica dell'applicazione senza dover gestire manualmente le query SQL e le operazioni di mapping tra oggetti e tabelle.

# JPA
**JPA** (Java Persistence API) **è una specifica Java che definisce un framework per la persistenza dei dati**. JPA facilita l'interazione tra un'applicazione Java e un database relazionale utilizzando un approccio basato sugli oggetti.

**JPA fornisce un set di annotazioni e un'API per eseguire operazioni di persistenza** dei dati **senza scrivere direttamente codice SQL**. La specifica JPA è implementata da diversi framework ORM (Object-Relational Mapping), tra cui Hibernate, EclipseLink e OpenJPA, che forniscono l'implementazione concreta delle specifiche JPA.
#### Definire un'entità
```java
import javax.persistence.Entity;
import javax.persistence.Id;

@Entity
public class Customer {
    @Id
    private Long id;
    private String name;
    // altre proprietà e metodi getter/setter
}
```
#### Configurare un'unità di persistenza
```java
<persistence xmlns="http://java.sun.com/xml/ns/persistence"
             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
             xsi:schemaLocation="http://java.sun.com/xml/ns/persistence http://java.sun.com/xml/ns/persistence/persistence_2_0.xsd"
             version="2.0">
    <persistence-unit name="myPersistenceUnit" transaction-type="RESOURCE_LOCAL">
        <class>com.example.Customer</class>
        <properties>
            <!-- Configurazione del provider JPA e dettagli di connessione al database -->
        </properties>
    </persistence-unit>
</persistence>
```
#### Eseguire operazioni di persistenza utilizzando JPA
```java
import javax.persistence.EntityManager;
import javax.persistence.EntityManagerFactory;
import javax.persistence.Persistence;

public class Main {
    public static void main(String[] args) {
        EntityManagerFactory emf = Persistence.createEntityManagerFactory("myPersistenceUnit");
        EntityManager em = emf.createEntityManager();

        // Esempio di operazioni CRUD
        em.getTransaction().begin();

        Customer customer = new Customer();
        customer.setId(1L);
        customer.setName("Emanuele Licata");

        em.persist(customer); // Operazione di creazione
        
		// Operazione di lettura
        Customer retrievedCustomer = em.find(Customer.class, 1L); 
        // Operazione di aggiornamento
        retrievedCustomer.setName("Nuovo Nome"); 

        em.remove(retrievedCustomer); // Operazione di eliminazione

        em.getTransaction().commit();

        em.close();
        emf.close();
    }
}
```

### Annotazioni
1. `@Entity`: L'annotazione `@Entity` viene utilizzata per definire una classe come entità persistente. L'entità corrisponde a una tabella nel database.
2. `@NamedQueries` e `@NamedQuery`: L'annotazione `@NamedQueries` viene utilizzata per definire una serie di query nominate associate a un'entità. L'annotazione `@NamedQuery` viene utilizzata per definire una query specifica all'interno di `@NamedQueries`. Le query nominate possono essere richiamate utilizzando il loro nome nell'EntityManager.
3. `@Id`: L'annotazione `@Id` viene utilizzata per indicare che un campo corrisponde alla chiave primaria dell'entità.
4. `@GeneratedValue`: L'annotazione `@GeneratedValue` viene utilizzata in combinazione con `@Id` per specificare la generazione automatica del valore della chiave primaria. Può essere utilizzata con diverse strategie come `AUTO`, `IDENTITY`, `SEQUENCE`, ecc.
5. `@OneToMany`: L'annotazione `@OneToMany` viene utilizzata per definire una relazione uno-a-molti tra due entità. Indica che un'entità contiene una collezione o una lista di istanze di un'altra entità.
6. `@ManyToOne`: L'annotazione `@ManyToOne` viene utilizzata per definire una relazione molti-a-uno tra due entità. Indica che un'entità fa riferimento a un'altra entità.
7. `@ManyToMany`: L'annotazione `@ManyToMany` viene utilizzata per definire una relazione molti-a-molti tra due entità. Indica che entrambe le entità hanno una relazione di associazione reciproca.

#### Esempio:
```java
@Entity
@Table(name = "students")
@NamedQueries({
    @NamedQuery(name = "Student.findAll", query = "SELECT s FROM Student s"),
    @NamedQuery(name = "Student.findByAge", query = "SELECT s FROM Student s WHERE s.age = :age")
})
public class Student {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;
    private int age;
    
    @OneToMany(mappedBy = "student")
    private List<Course> courses;
    
    @ManyToOne
    @JoinColumn(name = "university_id")
    private University university;
    
    @ManyToMany
    @JoinTable(name = "student_subject",
               joinColumns = @JoinColumn(name = "student_id"),
               inverseJoinColumns = @JoinColumn(name = "subject_id"))
    private List<Subject> subjects;
    
    // Costruttori, getter, setter e altri metodi
}
```
Nell'esempio sopra, abbiamo definito un'entità `Student` con l'annotazione `@Entity`. Abbiamo anche specificato il nome della tabella nel database utilizzando l'annotazione `@Table`. Abbiamo utilizzato `@Id` per indicare il campo `id` come chiave primaria generata automaticamente.

Abbiamo utilizzato `@NamedQueries` per definire due query nominate, "Student.findAll" e "Student.findByAge". Queste query possono essere richiamate successivamente nell'EntityManager.

L'annotazione `@OneToMany` viene utilizzata per definire la relazione uno-a-molti tra `Student` e `Course`. L'annotazione `@ManyToOne` viene utilizzata per definire la relazione molti-a-uno tra `Student` e `University`. L'annotazione `@ManyToMany` viene utilizzata per definire la relazione molti-a-molti tra `Student` e `Subject`. Le annotazioni `@JoinColumn` e `@JoinTable` vengono utilizzate per specificare i nomi delle colonne e delle tabelle per la relazione.

### 1:N e N:N unidirezionale e bidirezionale
Le relazioni uno-a-molti e molti-a-molti possono essere definite come unidirezionali o bidirezionali. 

#### Unidirezionali
Relazione **1:N unidirezionale**:

- Nella relazione uno-a-molti unidirezionale, un'entità (lato "uno") ha una collezione di entità correlate (lato "molti").
- La relazione viene definita solo su uno dei lati dell'associazione.
- L'entità "molti" non ha un riferimento all'entità "uno".
- Viene utilizzata l'annotazione `@OneToMany` sull'entità "uno" per definire la relazione.

Relazione **N:N unidirezionale**:

- Nella relazione molti-a-molti unidirezionale, un'entità (lato "uno") ha una collezione di entità correlate (lato "molti").
- La relazione viene definita solo su uno dei lati dell'associazione.
- Entrambe le entità non hanno un riferimento l'una all'altra.
- Viene utilizzata l'annotazione `@ManyToMany` sull'entità "uno" o "molti" per definire la relazione.

#### Bidirezionali
Relazione **1:N bidirezionale**:

- Nella relazione uno-a-molti bidirezionale, un'entità (lato "uno") ha una collezione di entità correlate (lato "molti"), e l'entità correlata (lato "molti") ha un riferimento all'entità principale (lato "uno").
- Entrambe le entità si riferiscono reciprocamente.
- Viene utilizzata l'annotazione `@OneToMany` sull'entità "uno" per definire la relazione, e l'annotazione `@ManyToOne` sull'entità "molti" per indicare la relazione verso l'entità "uno".

Relazione **N:N bidirezionale**:

- Nella relazione molti-a-molti bidirezionale, entrambe le entità (lato "uno" e lato "molti") hanno una collezione di entità correlate.
- Entrambe le entità si riferiscono reciprocamente.
- Viene utilizzata l'annotazione `@ManyToMany` su entrambe le entità per definire la relazione, e viene specificata una tabella di join con l'annotazione `@JoinTable`.