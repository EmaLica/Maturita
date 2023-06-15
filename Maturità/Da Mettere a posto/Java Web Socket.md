### WebSocket
In Java la classe WebSocket offre un'alternativa alla limitazione di una comunicazione efficiente tra il server e il browser web, fornendo comunicazioni client/server bidirezionali, full-duplex e in tempo reale. Il server può inviare dati al client in qualsiasi momento. Poiché viene eseguito su TCP, fornisce anche una comunicazione a basso livello di latenza e riduce l'overhead di ogni messaggio.

### Configurazione Endpoint
Esistono due modi per configurare gli endpoint: quello basato sulle annotazioni e quello basato sulle estensioni. Si può estendere la classe javax.websocket.Endpoint o utilizzare annotazioni dedicate a livello di metodo. Poiché il modello di annotazione porta a un codice più pulito rispetto al modello programmatico, l'annotazione è diventata la scelta convenzionale di codifica. In questo caso, gli eventi del ciclo di vita degli endpoint WebSocket sono gestiti dalle seguenti annotazioni:

1. @ServerEndpoint: se decorato con @ServerEndpoint, il contenitore assicura la disponibilità della classe come server WebSocket in ascolto su uno spazio URI specifico
2. @ClientEndpoint: Una classe decorata con questa annotazione è trattata come un client WebSocket.
3. @OnOpen: Un metodo Java con @OnOpen viene invocato dal container quando viene avviata una nuova connessione WebSocket.
4. @OnMessage: Un metodo Java, annotato con @OnMessage, riceve le informazioni dal container WebSocket quando viene inviato un messaggio all'endpoint.
5. @OnError: Un metodo con @OnError viene invocato quando si verifica un problema nella comunicazione.
6. @OnClose: Utilizzato per decorare un metodo Java che viene chiamato dal container quando la connessione WebSocket viene chiusa.
```java
@ServerEndpoint(value="/chat/{username}")
public class ChatEndpoint {
 
    private Session session;
    private static Set<ChatEndpoint> chatEndpoints 
    = new CopyOnWriteArraySet<>();
    private static HashMap<String, String> users = new HashMap<>();

    @OnOpen
    public void onOpen(
      Session session, 
      @PathParam("username") String username) throws IOException {
 
        this.session = session;
        chatEndpoints.add(this);
        users.put(session.getId(), username);

        Message message = new Message();
        message.setFrom(username);
        message.setContent("Connected!");
        broadcast(message);
    }

    @OnMessage
    public void onMessage(Session session, Message message) 
      throws IOException {
 
        message.setFrom(users.get(session.getId()));
        broadcast(message);
    }

    @OnClose
    public void onClose(Session session) throws IOException {
 
        chatEndpoints.remove(this);
        Message message = new Message();
        message.setFrom(users.get(session.getId()));
        message.setContent("Disconnected!");
        broadcast(message);
    }

    @OnError
    public void onError(Session session, Throwable throwable) {
        // Do error handling here
    }

    private static void broadcast(Message message) 
      throws IOException, EncodeException {
 
        chatEndpoints.forEach(endpoint -> {
            synchronized (endpoint) {
                try {
                    endpoint.session.getBasicRemote().
                      sendObject(message);
                } catch (IOException | EncodeException e) {
                    e.printStackTrace();
                }
            }
        });
    }
}
```
Quando un nuovo utente si collega (@OnOpen) viene immediatamente mappato in una struttura dati di utenti attivi. Quindi, viene creato un messaggio e inviato a tutti gli endpoint utilizzando il metodo broadcast.

Questo metodo viene utilizzato anche ogni volta che viene inviato un nuovo messaggio (@OnMessage) da uno qualsiasi degli utenti connessi: questo è lo scopo principale della chat.

Se a un certo punto si verifica un errore, il metodo con l'annotazione @OnError lo gestisce. Si può usare questo metodo per registrare le informazioni sull'errore e cancellare gli endpoint.

Infine, quando un utente non è più connesso alla chat, il metodo @OnClose cancella l'endpoint e comunica a tutti gli utenti che un utente è stato disconnesso.

### Tipi di messaggio
La specifica WebSocket supporta due formati di dati on-wire: testo e binario. L'API supporta entrambi questi formati e aggiunge funzionalità per lavorare con oggetti Java e messaggi di controllo dello stato di salute (ping-pong), come definito nella specifica:
1. Testo: Qualsiasi dato testuale (java.lang.String, primitive o classi wrapper equivalenti).
2. Binario: Dati binari (ad esempio audio, immagini, ecc.) rappresentati da un java.nio.ByteBuffer o da un byte[] (array di byte).
3. Oggetti Java: L'API consente di lavorare con rappresentazioni native (oggetti Java) nel codice e di utilizzare trasformatori personalizzati (codificatori/decodificatori) per convertirli in formati on-wire compatibili (testo, binario) consentiti dal protocollo WebSocket.
4. Ping-Pong: Un javax.websocket.PongMessage è un riconoscimento inviato da un peer WebSocket in risposta a una richiesta di controllo dello stato di salute (ping).
Per la nostra applicazione, utilizzeremo gli oggetti Java. Creeremo le classi per la codifica e la decodifica dei messaggi.

### Encoder
Un codificatore prende un oggetto Java e produce una rappresentazione tipica adatta alla trasmissione come messaggio, come JSON, XML o rappresentazione binaria. I codificatori possono essere utilizzati implementando le interfacce Encoder.Text<T> o Encoder.Binary<T>. 
Nel codice sottostante definiamo la classe Message da codificare e nel metodo encode utilizziamo Gson per codificare l'oggetto Java in JSON:

```java
public class Message {
    private String from;
    private String to;
    private String content;
    
    //standard constructors, getters, setters
}
```

```java
public class Message {
    public class MessageEncoder implements Encoder.Text<Message> {

    private static Gson gson = new Gson();

    @Override
    public String encode(Message message) throws EncodeException {
        return gson.toJson(message);
    }

    @Override
    public void init(EndpointConfig endpointConfig) {
        // Custom initialization logic
    }

    @Override
    public void destroy() {
        // Close resources
    }
}
}
```

### Decoder
Un decodificatore è l'opposto di un codificatore e viene utilizzato per ritrasformare i dati in un oggetto Java. I decodificatori possono essere implementati utilizzando le interfacce Decoder.Text<T> o Decoder.Binary<T>.

Come abbiamo visto con l'encoder, il metodo di decodifica è quello in cui prendiamo il JSON recuperato nel messaggio inviato all'endpoint e usiamo Gson per trasformarlo in una classe Java chiamata Message.

```java
public class MessageDecoder implements Decoder.Text<Message> {

    private static Gson gson = new Gson();

    @Override
    public Message decode(String s) throws DecodeException {
        return gson.fromJson(s, Message.class);
    }

    @Override
    public boolean willDecode(String s) {
        return (s != null);
    }

    @Override
    public void init(EndpointConfig endpointConfig) {
        // Custom initialization logic
    }

    @Override
    public void destroy() {
        // Close resources
    }
}
```

### Impostare Encoder e Decoder nel Server Endpoint

```java
@ServerEndpoint( 
  value="/chat/{username}", 
  decoders = MessageDecoder.class, 
  encoders = MessageEncoder.class )
```