---
Data: 19th June 2023
Descrizione: WebService Rest e WebApplication, wadl per la descrizione dei servizi
---
# Applicazione ParkingPass
### Package Dominio
#### Classe Utente
```java
@Entity
@XmlRootElement
public class Utente implements Serializable {
    @Id
    private String username;
    private String password;
    private String nome;
    private String cognome;
    //Tre targhe massime per utente, per rispettare la prima forma normale abbiamo tolto l'hashmap
    private String targa1;
    private String targa2;
    private String targa3;

    public String getNome() {
        return nome;
    }

    public String getNomeCompleto() {
        return nome + cognome;
    }

    public void setNome(String nome) {
        this.nome = nome;
    }

    public String getCognome() {
        return cognome;
    }

    public void setCognome(String cognome) {
        this.cognome = cognome;
    }
    
    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public String getPassword() {
        return password;
    }

    public void setPassword(String password) {
        this.password = password;
    }

    public String getTarga1() {
        return targa1;
    }

    public void setTarga1(String targa1) {
        this.targa1 = targa1;
    }

    public String getTarga2() {
        return targa2;
    }

    public void setTarga2(String targa2) {
        this.targa2 = targa2;
    }

    public String getTarga3() {
        return targa3;
    }
    public void setTarga3(String targa3) {
        this.targa3 = targa3;
    }
}
```

### Package Service
#### Classe AbstractFacade
```java
public abstract class AbstractFacade<T> {

    private Class<T> entityClass;

    public AbstractFacade(Class<T> entityClass) {
        this.entityClass = entityClass;
    }

    protected abstract EntityManager getEntityManager();

    public void create(T entity) {
        getEntityManager().persist(entity);
    }

    public void edit(T entity) {
        getEntityManager().merge(entity);
    }

    public void remove(T entity) {
        getEntityManager().remove(getEntityManager().merge(entity));
    }

    public T find(Object id) {
        return getEntityManager().find(entityClass, id);
    }

    public List<T> findAll() {
        javax.persistence.criteria.CriteriaQuery cq = getEntityManager().getCriteriaBuilder().createQuery();
        cq.select(cq.from(entityClass));
        return getEntityManager().createQuery(cq).getResultList();
    }

    public List<T> findRange(int[] range) {
        javax.persistence.criteria.CriteriaQuery cq = getEntityManager().getCriteriaBuilder().createQuery();
        cq.select(cq.from(entityClass));
        javax.persistence.Query q = getEntityManager().createQuery(cq);
        q.setMaxResults(range[1] - range[0] + 1);
        q.setFirstResult(range[0]);
        return q.getResultList();
    }

    public int count() {
        javax.persistence.criteria.CriteriaQuery cq = getEntityManager().getCriteriaBuilder().createQuery();
        javax.persistence.criteria.Root<T> rt = cq.from(entityClass);
        cq.select(getEntityManager().getCriteriaBuilder().count(rt));
        javax.persistence.Query q = getEntityManager().createQuery(cq);
        return ((Long) q.getSingleResult()).intValue();
    }

}
```
#### Classe ApplicationConfig
```java
@javax.ws.rs.ApplicationPath("app")
public class ApplicationConfig extends Application {
    @Override
    public Set<Class<?>> getClasses() {
        Set<Class<?>> resources = new java.util.HashSet<>();
        addRestResourceClasses(resources);
        return resources;
    }

    private void addRestResourceClasses(Set<Class<?>> resources) {
        resources.add(service.UtenteFacadeREST.class);
      
    }
}
```
#### Classe UtenteFacadeREST
```java
@Stateless
@Path("parcheggio")
public class UtenteFacadeREST extends AbstractFacade<Utente> {

    @PersistenceContext(unitName = "ParkingPassPU")
    private EntityManager em;

    public UtenteFacadeREST() {
        super(Utente.class);
    }

    @POST
    @Override
    @Consumes({MediaType.APPLICATION_XML, MediaType.APPLICATION_JSON})
    public void create(Utente entity) {
        super.create(entity);
    }

    @PUT
    @Path("{id}")
    @Consumes({MediaType.APPLICATION_XML, MediaType.APPLICATION_JSON})
    public void edit(@PathParam("id") String id, Utente entity) {
        super.edit(entity);
    }

    @DELETE
    @Path("{id}")
    public void remove(@PathParam("id") String id) {
        super.remove(super.find(id));
    }

    @GET
    @Path("{id}")
    @Produces({MediaType.APPLICATION_XML, MediaType.APPLICATION_JSON})
    public Utente find(@PathParam("id") String id) {
        return super.find(id);
    }

    @GET
    @Override
    @Produces({MediaType.APPLICATION_XML, MediaType.APPLICATION_JSON})
    public List<Utente> findAll() {
        return super.findAll();
    }

    @GET
    @Path("{from}/{to}")
    @Produces({MediaType.APPLICATION_XML, MediaType.APPLICATION_JSON})
    public List<Utente> findRange(@PathParam("from") Integer from, @PathParam("to") Integer to) {
        return super.findRange(new int[]{from, to});
    }

    @GET
    @Path("count")
    @Produces(MediaType.TEXT_PLAIN)
    public String countREST() {
        return String.valueOf(super.count());
    }

    @POST
    @Path("register")
    public Response register(@FormParam("username") String username, @FormParam("password") String password, @FormParam("nome") String nome,
            @FormParam("cognome") String cognome,
            @FormParam("codice") String codice) {
        //26663a0c1f85622d314196cfcdf718d587dbcb7d52e3c952855197b11d390dfd = ahs652
        if (Hash.SHA256(codice).equals("26663a0c1f85622d314196cfcdf718d587dbcb7d52e3c952855197b11d390dfd")) {
            Utente utente = new Utente();
            utente.setUsername(username);
            utente.setPassword(password);
            utente.setNome(nome);
            utente.setCognome(cognome);
            try {
                // Salva l'utente nel database
                create(utente);
                return Response.ok().status(Response.Status.CREATED).build();
            } catch (Exception e) {
                // In caso di errore durante la creazione dell'utente
                return Response.serverError().build();
            }
        } else {
            return Response.status(Response.Status.UNAUTHORIZED).build();
        }
    }

    @GET
    @Path("login")
    public Response login(@QueryParam("username") String username, @QueryParam("password") String password) {
        Utente u = em.find(Utente.class, username);
        if (u.getPassword().equals(password))
            return Response.ok("http://localhost:8080/ParkingPass/dashboard.html").status(Response.Status.ACCEPTED).build();
        return Response.status(Response.Status.NOT_FOUND).build();
    }
    
   @GET
    @Path("qr")
    @Produces("image/png")
    public Response getQr(@FormParam("username") String username, @FormParam("targa") String targa) throws EccezioneCripto {
        Rsa chiave = new Rsa();
        //chiave aes = p2s5v8y/B?E(H+MbQeThVmYq3t6w9z$C
        Aes seggreto = new Aes("p2s5v8y/B?E(H+MbQeThVmYq3t6w9z$C");
        //stringa che identifica il ticket del parcheggio
        String kitkat = chiave.cifraPrivata(targa + ";" + "2024/05/20" + ";" + seggreto.cifraToString(em.find(Utente.class, username).getNomeCompleto()), "MIIEuwIBADANBgkqhkiG9w0BAQEFAASCBKUwggShAgEAAoIBAQCPJifXB9Ls9J4NZKYVljUQ4PNVstGpOb2nTN36gSBlCqkq2mN6DXl8vhsxPsaGF0Mppl42Md25qxqd30rNJkIJciv2jYWpQ8B10Apt5XqaFbdTsVR2xN/pKudIzo5gfnyAED+6NJjAmdLdnnJmNIzzWeYgfH7az6HmmI4xqHJBSTmP8o4C2nNMnwhQR8Umjyjk+mZyokIQLm3zLOyDINc7IeuOvWJMn2KiiaufGVCDw9zt8ajnYXCqyJB1xfiKs2RS0Zyo9NMoE/oAW7huZxWXALfTRZsIit0ilxCpWi1oqh6BJ6K2lnIvz+c5EBf8iF7TYoBrWwtdA7grL7leyPJfAgMBAAECgf91+/zaPpiatQOQBmTdZfBW+RGWkMw9rlmiirhqwALzRNYpe9aBwplfN1EyRYta+dFhgr4j7PXTEjPd6yy76cyD/JY/oGWKHU2DzPTLn1htp3hygrYbLilfBP2cBKNU5Ou4oavkzXUZSa+C+hVQKAAEkxQZsoLb1kaaySJpy2xgYb49KcO49He8avcYy8CX1OFisNETXnF4lw76kgwkFvhXKTyxlgCFnK4AWuiGpUGpVb0aGELwGarinqrdwrXs5JZNoHvxMdYO2eWmUElAL2bzo6W0v2k2t+dLmWKIcls+RWGZ3P4SKuX6YmYLzDRCgrYYinl6gY2t7DllXi5PrzkCgYEAx1uuIcoqpcbY+AocTm9NKR8fthDNfZX01VZ5YBFxfPTGPm7Vif5CnfWf4xfBP4SmFUMjW45yRx1K7+NTtcyxgHWIKmbetHjwoc+0YABkNnvPa+LBa4vyZaTLZeivvoEDaoaVCaTijJyZzBQMkLCQQubUiqFf6ynEL+SK2ccZvwMCgYEAt9IbKtf3J63zUSqN6+5cHddcQ3iodc8dDGVXTurYeBWrDSYvzArjMla6k0oCMCtKL3p6JUUVQJ9XWGY/0RNq0qQA6HfcJt7Vv+x0d0pBK2BMeZ/2F0Sg0UG8SFE/zLPuvdcXVmtKYSbjJYqwuPiZglDzLsoBJ0E6y9UXbyXM4nUCgYA6UET1OU+UQkAA/eQdxUzKtIHwHaYeEBkXtj22riOGK4s5g+4OeUM/NTPZl389dy2llofnJhmjV5wt407/JKrfKoHz9Tc7jwzEKB9Y3YRys3CO3Ds7nCoBNV0RqCiQDujS5h7+PS7Pdpc+LLcoM51fFGojSuTlwsfSQoWjAiwzxQKBgQCbj92Z5matV9LAb8jnTzL5thXIq8W03W/x25mFmc1T4tJ9MEHm5ZfcM/V1TH6JkTkY8QeJnusbYz2h+/Yp08rlNBHoqfbPlmlCILN3eImqUbamfy7eBiAqtvzGHqxlaiiy0+JWKjop+aTlUne4MfqHhEYo5J8RP2yor09DqrO3OQKBgE2OCtAdxbio57doHmFm1lTtz6wFYZw6ynd5yDlrC59y/exoE1ZnWbKuZ3CX02u+fedcFCLcnkp4VeOtKim/R5UKcYDlbEQ8ziut/GE2BUxr/EsKD2u9p+/LKsZMGoq4kzeX+wEwqqQEejQn9lwYJ/5vUXE8L+dyyoaLBZogkxv4");
       if (em.find(Utente.class, username).getTarga1().isEmpty()) {
           em.find(Utente.class, username).setTarga1(kitkat);
       } else if (em.find(Utente.class, username).getTarga2().isEmpty()) {
           em.find(Utente.class, username).setTarga2(kitkat);
       } else em.find(Utente.class, username).setTarga3(kitkat);
        return Response.ok(QR.createQRCodeBufferedImage(kitkat, 500)).build();
    }

    @Override
    protected EntityManager getEntityManager() {
        return em;
    }

}
```

# Wadl
**WADL** (Web Application Description Language) **è un linguaggio XML utilizzato per descrivere i servizi Web e le loro interfacce**. Tuttavia, WADL non è ampiamente utilizzato e ha perso popolarità rispetto ad **altri formati come Swagger** (OpenAPI Specification).
Ecco un esempio di come potrebbe apparire un documento WADL per descrivere un servizio Web REST:
```xml
<application xmlns="http://wadl.dev.java.net/2009/02"
             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
             xsi:schemaLocation="http://wadl.dev.java.net/2009/02 wadl.xsd">
    <resources base="http://localhost:8080/api">
        <resource path="/resource1">
            <method name="GET" id="resource1Get">
                <response>
                    <representation mediaType="application/xml"/>
                </response>
            </method>
            <method name="POST" id="resource1Post">
                <request>
                    <representation mediaType="application/xml"/>
                </request>
                <response>
                    <representation mediaType="application/xml"/>
                </response>
            </method>
        </resource>
        <resource path="/resource2">
            <!-- Altri metodi e risorse qui -->
        </resource>
    </resources>
</application>
```

