---
Data: 20th June 2023
Descrizione: utilizzo di JAX-RS Jersey. Utilizzo della annotazioni @ApplicationPath, @Path, @GET, @PUT, @POST, @DELETE, @CookieParam, @PathParam, @FormParam, @Context, @XmlRootElement
---

## Java JAX-RS

JAX-RS è una **specifica Java per lo sviluppo di servizi web RESTful**. Le annotazioni JAX-RS forniscono un modo per configurare un servizio web RESTful in modo dichiarativo, rendendo più facile e veloce lo sviluppo di applicazioni web.

### Annotazioni
Ecco alcune delle annotazioni JAX-RS più comuni:

1.  **@Path**: questa annotazione specifica l'URI base per una classe o un metodo del servizio web RESTful. Ad esempio, se si annota una classe con @Path("/hello"), allora il servizio web RESTful associato risponderà alle richieste iniziate con "/hello".
``` java
@Path("/hello")
public class Hello {
}
```

2.  **@GET, @POST, @PUT, @DELETE**: queste annotazioni specificano il tipo di richiesta HTTP associato al metodo annotato. Ad esempio, se si annota un metodo con @GET, allora il metodo risponderà solo alle richieste GET.
``` java
@GET
@Produces(MediaType.APPLICATION_JSON)
public List<Person> getPersons() {
}

@POST
@Consumes(MediaType.APPLICATION_JSON)
@Produces(MediaType.APPLICATION_JSON)
public Person addPerson(Person person) {
}

@PUT
@Path("/{id}")
@Consumes(MediaType.APPLICATION_JSON)
@Produces(MediaType.APPLICATION_JSON)
public Person updatePerson(@PathParam("id") int id, Person person) {
}

@DELETE
@Path("/{id}")
@Produces(MediaType.APPLICATION_JSON)
public Person deletePerson(@PathParam("id") int id) {
}

```

3.  **@Produces, @Consumes**: queste annotazioni specificano il tipo di contenuto dei dati che il metodo può produrre o consumare. Ad esempio, se si annota un metodo con @Produces("application/json"), il metodo produrrà solo dati in formato JSON.
``` java
@POST 
@Path("/add") 
//Richiede un mediatype di tipo JSON
@Consumes(MediaType.APPLICATION_JSON)
//Produce un mediatype di tipo XML
@Produces(MediaType.APPLICATION_XML) 
public CalculationResult add(Numbers numero){
}
```

4.  **@PathParam**: questa annotazione specifica un parametro di percorso nell'URI. Ad esempio, se si annota un metodo con @Path("/{param}") e @PathParam("param"), il valore del parametro di percorso verrà passato come argomento al metodo.
``` java
@Path("/libro/{nomeLibro}")
public String getLibro(@PathParam("nomeLibro") String nomeLibro) {
	return libri.get(nomeLibro);
}
```

5.  **@QueryParam**: questa annotazione specifica un parametro di query nell'URI. Ad esempio, se si annota un metodo con @Path("/users") e @QueryParam("name"), il valore del parametro di query verrà passato come argomento al metodo.
``` java
@GET
public Response readBook(@QueryParam("nomeLibro") String nomeLibro) {
	Libro libro = libri.read(nomeLibro);
	
	return libro != null ? 
	Response.ok(libro).status(200).build() : 
	Response.status(Status.NOT_FOUND).build();	
}
```

6.  **@HeaderParam**: questa annotazione specifica un parametro di intestazione HTTP. Ad esempio, se si annota un metodo con @HeaderParam("Authorization"), il valore dell'intestazione Authorization verrà passato come argomento al metodo.
``` java
@GET
@Path("/{id}")
@Produces(MediaType.APPLICATION_JSON)
public Book getBook(@PathParam("id") int id, @HeaderParam("Authorization") String authHeader){
}
```

7.  **@DefaultValue**: questa annotazione specifica un valore predefinito per un parametro. Ad esempio, se si annota un metodo con @QueryParam("name") e @DefaultValue("guest"), il valore predefinito del parametro "name" sarà "guest" se non viene fornito alcun valore.
``` java
@GET @Path("/hello") 
@Produces(MediaType.TEXT_PLAIN) 
public String sayHello(@QueryParam("name") @DefaultValue("Guest") String guestName){ 
return "Hello, " + guestName + "!"; 
}
```

8. **@ApplicationPath**: annotazione che identifica il percorso dell'applicazione che ricopre il ruolo di percorso URL base delle risorse.
``` java
@ApplicationPath("/api")
public class MyApplication extends Application {
// Nessun codice specifico da aggiungere qui, poiché questa classe viene utilizzata solo per definire il percorso di base.
// Tutte le risorse web sono definite in classi separate annotate con @Path.
}

```

9. **@ContextPath**: percorso in cui confluiscono i file relativi alla root directory del webserver. In questo esempio, tutte le risorse della classe UserResource saranno disponibili sotto il percorso "/api/users". Il metodo getUser risponderà alle richieste iniziate con "/api/users/{id}".
``` java
@Path("/users")
@ContextPath("/api")
public class UserResource {

    @GET
    @Path("/{id}")
    public User getUser(@PathParam("id") int id) {
        // Implementazione del metodo getUser
    }
}
```

10. **Servlet**: componente che consente di gestire l'interazione tra client e server 

11. **ServletContext**: componente che si occupa della condivisione di file e dati tra le varie pagine della WebpAplication.   

12. **@Context**: L'annotazione @Context viene utilizzata per iniettare le informazioni di contesto della richiesta HTTP nella variabile HttpHeaders.          In questo esempio, il servizio web "HelloResource" utilizza l'annotazione @Context per iniettare l'oggetto ServletContext. Il metodo "sayHello" utilizza l'oggetto ServletContext per accedere ad un parametro di inizializzazione dell'applicazione chiamato "app-name". Il valore di questo parametro viene utilizzato per generare il messaggio di saluto.
```java
@Path("/hello")
public class HelloResource {

    @Context
    private ServletContext context;

    @GET
    @Produces(MediaType.TEXT_PLAIN)
    public String sayHello() {
        String appName = context.getInitParameter("app-name");
        return "Hello from " + appName + "!";
    }
}

```

13. **@XmlRootElement**: annotazione che identifica elementi il cui schema viene scritto in XML.
```java
@XmlRootElement(name = "libro")
public class Libro {
	private String name;
	private String autore;
	...
}
```
```xml
<libro>
	<name>...</name>
	<autore>...</autore>
</libro>
```

14. **@CookieParam**: annotazione che consente di estrarre il valore di una variabile all'interno di un cookie.
```java
@Path("/libro/aggiungi/{nomeLibro}")
public Response addBook(@CookieParam("userToken") String userToken, @PathParam("nomeLibro") String nomeLibro) {
	if (tokens.get(userToken) != null) {
		libri.add(nomeLibro);
		return Response.ok("inserito").status(200).build();
	} else return Response.status(Status.NOT_AUTORIZED).build();
}
```

15. **@FormParam**: annotazione che consente di estrarre il valore di una variabile all'interno di un form.
```html
<html>
...
<form action="service/login" method="post">
	<input type="text" name="username" placeholder="Username">
	<input type="password" name="password" placeholder="Password">
	<input type="submit" name="login" value="login">
</form>
</html>
```

```java
@GET
public Response login(@FormParam("username") String username, @FormParam("password") String password) {
	User user = new User(username, SHA(password));
	User read = userPersistence.read(user);
	
	if (!user.equals(read)) return Response.status(Status.NOT_AUTORIZED);
	return Response.ok();
}
```

### Metodi HTTP corrispetivi CRUD: 

- GET: read
- POST: create
- PUT / PATH: update
- DELETE: delete
