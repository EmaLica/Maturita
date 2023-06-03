---
title: Tepsit
author: Ema
date: 10/02/2023
---
glassfish 4.1
le versioni antecendenti hanno problemi con l'esportazione in JSON

scambio di dati xml e json
framework front-end angulajs 

New Project > Java Web > Web Application 
Server = Glassfish 4.1.
ContexPath = URL in localhost 
FrameWork = None

OnSave -> Glassfish Deploy

1. Specificare Application Path (URI che identifica il servizio) mediante annotazioni [ @ApplicationPath("") ]
2. I metodi della classe mappata vengono inoltrati all'Application Path
3. Alle richieste HTTP mediante annotazioni (@GET, @POST, @PUT, @DELETE ...) vengono mappati i metodi;

```java

package service;

import javax.ws.*;
import javax.ws.core.*;

@ApplicationPath("service_name");
public class Service extends Application {
	@GET
	public String loadPage() {
		return "<h1>Hello, World</h1>";
	}
}

```

1. La parte variabile dell'URL viene identificata mediante annotazione: @Path("{nome_variabile}") 
2. Si associa il parametro del percorso con le variabili dell'applicazione mediante annotazione @PathParam("nome_variabile") Tipo variabile
```java
package service;

import javax.ws.*;
import javax.ws.core.*;

@ApplicationPath("service_name");
public class Service extends Application {
	@GET
	@Path("{user_name}");
	public String loadPage(@PathParam("user_name") String user_name) {
		return System.out.format("<h1>Hello %s!</h1>", user_name);
	}
}

```

1. Si possono mappare parte constanti e variabili

```java
package service;

import javax.ws.*;
import javax.ws.core.*;

@ApplicationPath("service_name");
public class Service extends Application {
	@GET
	@Path("{user_name}/color/{color}");
	public String loadPage(@PathParam("user_name") String user_name, @PathParam("color") String color) {
		return System.out.format("<h1>Hello %s!</h1><h1>%s</h1>", user_namem color);
	}
}

```

1. URL:
Glassfish, ContexPath, Application, Percorso
localhost:8080/contex/app/index.html

2. Ogni richiesta del client ha come risposta una nuova istanza dell'applicazione da parte di Glassfish

1. Specificare a JAXRS di inoltrare in XML mediante annotazione 
```java
@Annotazione
public class Book implements Serializable {
	...
}

@ApplicationPath("service_name");
public class Service extends Application {
	@GET
	@Path("book");
	public String loadPage(@PathParam("book") Book book) 
		return Book;
	}
}



@ApplicationPath("service_name");
public class Service extends Application {
	@GET
	@Path("book");
	@Consumes("text/json")
	public void create(Book book) {
		String isbn = book.getIsbn();
		if ( !books.containsKey(isbn) ) books.put(isbn, book);
	}
}
```

POSTMAN:

Header:
key: ContentType
value: application/json
description: 

```json
Body > raw: 
{ 
	"isbn": "myisbn",
	"author": "myauthor",
	"name": "myname"
}
```
HTTP ERROR 415: UNSUPPORTED MEDIA TYPE

Contenuto proveniente da un FORM: @Consumes(MediaType.APPLICATION_FORM_URLENCODED)
Variabile ricevuta dal form: @FormParam("form-input-name")

Nel form: 
```java
<form action="path/method"> ... </form>

@CookieParam()
Response.ok("").cookie(new NewCookie())

WebApplicationException(Response.Status.FORBIDDEN)
```
CODICI HTTP 200, 300, 400, 500

// input form
// sql query
// cookie

NewCookie vs Cookie ?