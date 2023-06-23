---
Data: 19th June 2023
Descrizione: servlet, mapping con i metodi dell’http, uso dei database con java per lo sviluppo di webservice tramite JPA, utilizzo dell’applicativo Postman, uso di JSP e forwarding da WebApplication
---
## Servlet
Un **servlet in Java** è un **componente della programmazione server-side** utilizzato per **estendere le funzionalità di un server web**. Essenzialmente, un servlet **riceve richieste HTTP e genera risposte** in base alla logica di programmazione implementata al suo interno.

```java
import javax.servlet.*;
import javax.servlet.http.*;
import java.io.IOException;
import java.io.PrintWriter;

public class MioServlet extends HttpServlet {
    
    public void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        
        // Imposta il tipo di contenuto della risposta
        response.setContentType("text/html");
        
        // Ottiene un oggetto PrintWriter per scrivere la risposta
        PrintWriter out = response.getWriter();
        
        // Scrive il corpo della risposta
        out.println("<html>");
        out.println("<head><title>Mio Servlet</title></head>");
        out.println("<body>");
        out.println("<h1>Ciao, questo è il mio servlet!</h1>");
        out.println("</body>");
        out.println("</html>");
    }
}
```

## Mapping con i metodi dell’HTTP 
Quando si lavora con i servlet in Java, è possibile mappare i metodi HTTP alle diverse operazioni che si desidera eseguire nel servlet. Ecco alcuni esempi di come effettuare il mapping dei metodi HTTP più comuni:

1. `doGet`: Metodo HTTP GET, utilizzato per **richiedere risorse dal server**. È il metodo predefinito quando si accede a un URL tramite il browser.
```java
public void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    // Logica per gestire la richiesta GET
}
```

2. `doPost`: Metodo HTTP POST, utilizzato per **inviare dati al server**. È comunemente utilizzato per l'invio di form HTML o per l'elaborazione di dati sensibili.
```java
public void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    // Logica per gestire la richiesta POST
}
```

3. `doPut`: Metodo HTTP PUT, utilizzato per **aggiornare una risorsa esistente sul server**.
```java
public void doPut(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    // Logica per gestire la richiesta PUT
}
```

4. `doDelete`: Metodo HTTP DELETE, utilizzato per **eliminare una risorsa esistente sul server**.
```java
public void doDelete(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    // Logica per gestire la richiesta DELETE
}
```

Questi sono solo alcuni dei metodi HTTP più comuni. È possibile mappare ulteriori metodi come `doHead`, `doOptions`, `doTrace`, ecc. nel tuo servlet, a seconda delle tue esigenze.

Per effettuare il mapping dei metodi HTTP al tuo servlet, puoi utilizzare l'annotazione `@WebServlet` con l'attributo `urlPatterns`. Ad esempio:
```java
@WebServlet(urlPatterns = {"/myServlet"}, name = "MioServlet")
public class MioServlet extends HttpServlet {
    // ...
}
```

## Java Persistence API
Nello sviluppo di web service in Java, è comune utilizzare Java Persistence API (JPA) per **l'interazione con il database**. **JPA è una specifica Java che definisce un'interfaccia per la persistenza dei dati** e **semplifica l'accesso** e la **gestione dei dati** nelle applicazioni Java.

Ecco una panoramica del processo per utilizzare JPA per l'accesso al database nello sviluppo di web service:

1. **Configurazione del database**: Innanzitutto, è necessario configurare il database a cui ci si desidera connettere. Ciò coinvolge la configurazione delle informazioni di connessione nel file di configurazione dell'applicazione o **tramite annotazioni**, a seconda del framework utilizzato (ad esempio, Java EE, Spring, ecc.).
2. **Definizione delle entità**: Successivamente, è necessario definire le entità che rappresentano le tabelle del database con cui si desidera interagire. Un'entità è una classe Java annotata con `@Entity` che **corrisponde a una tabella del database**. Ogni attributo della classe rappresenta una colonna della tabella.
```java
@Entity
@Table(name = "users")
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(name = "username")
    private String username;

    @Column(name = "password")
    private String password;

    // Getter e Setter
    // ...
}
```
3. **Gestione delle operazioni CRUD**: Utilizzando JPA, puoi facilmente eseguire operazioni di creazione, lettura, aggiornamento e eliminazione (CRUD) sulle entità. Puoi definire metodi nelle classi dei tuoi web service che utilizzano JPA per eseguire queste operazioni tramite **EntityManager**.
```java
@PersistenceContext
private EntityManager entityManager;

public User createUser(User user) {
    entityManager.persist(user);
    return user;
}

public User getUser(Long id) {
    return entityManager.find(User.class, id);
}

public User updateUser(User user) {
    return entityManager.merge(user);
}

public void deleteUser(Long id) {
    User user = entityManager.find(User.class, id);
    if (user != null) {
        entityManager.remove(user);
    }
}
```
4. **Gestione delle transazioni**: Quando si utilizza JPA, è importante gestire le transazioni per **garantire l'integrità dei dati**. Puoi farlo annotando i metodi dei tuoi web service con `@Transactional` (se stai utilizzando un framework che supporta l'annotazione `@Transactional`, ad esempio Spring) o utilizzando il supporto di transazione fornito dalla piattaforma Java EE.
```java
@Transactional
public User createUser(User user) {
    entityManager.persist(user);
    return user;
}
```

## JSP e forwarding da WebApplication 
JSP (JavaServer Pages) **è una tecnologia utilizzata per creare pagine web dinamiche in Java**. Le pagine JSP **possono contenere del codice Java all'interno** di tag speciali, **che viene eseguito sul server per generare il contenuto HTML** da inviare al client.

Per implementare il forwarding (inoltro) da una web application usando JSP, puoi seguire i seguenti passaggi:

1. **Crea una pagina JSP**: Inizia creando una pagina JSP che servirà come destinazione dell'inoltro. Questa pagina conterrà il contenuto HTML che desideri mostrare al client.
2. **Configura il mapping del servlet**: Nel tuo file di configurazione web (come il file `web.xml` o utilizzando annotazioni), associa una servlet all'URL desiderato. Ad esempio:
```xml
<servlet>
    <servlet-name>ForwardServlet</servlet-name>
    <jsp-file>/forwarded-page.jsp</jsp-file>
</servlet>
<servlet-mapping>
    <servlet-name>ForwardServlet</servlet-name>
    <url-pattern>/forward</url-pattern>
</servlet-mapping>
```
3. **Implementa la servlet**: Crea la classe della servlet che gestirà la richiesta e l'inoltro. La servlet può eseguire operazioni aggiuntive o elaborare dati prima di inoltrare la richiesta alla pagina JSP. Ad esempio:
```java
@WebServlet("/forward")
public class ForwardServlet extends HttpServlet {
    
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        // Operazioni aggiuntive se necessario
        
        // Inoltro alla pagina JSP
        RequestDispatcher dispatcher = request.getRequestDispatcher("/forwarded-page.jsp");
        dispatcher.forward(request, response);
    }
}
```
4. **Creazione della pagina JSP inoltrata**: Crea la pagina JSP "forwarded-page.jsp" che rappresenterà la destinazione dell'inoltro. Puoi includere il tuo codice HTML e utilizzare tag JSP per incorporare la logica o i dati necessari.
```jsp
<html>
<head>
    <title>Forwarded Page</title>
</head>
<body>
    <h1>Questa è la pagina inoltrata</h1>
    <!-- Altri contenuti HTML o tag JSP -->
</body>
</html>
```
La pagina JSP "forwarded-page.jsp" può contenere il codice HTML che desideri mostrare al client.

Quando una richiesta viene inviata all'URL associato alla servlet ("forward"), la servlet elaborerà la richiesta, eseguirà eventuali operazioni aggiuntive e quindi inoltrerà la richiesta alla pagina JSP "forwarded-page.jsp". Il contenuto generato dalla pagina JSP verrà quindi restituito al client come risposta.