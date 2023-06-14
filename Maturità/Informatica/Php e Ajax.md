---
Data: 14th June 2023
Descrizione: php e ajax
---
## PHP 
### Connessione al DB
```php
// Parametri di connessione al database
$servername = "localhost";
$username = "nome_utente";
$password = "password";
$dbname = "nome_database";

// Creazione della connessione
$conn = new mysqli($servername, $username, $password, $dbname);

// Verifica della connessione
if ($conn->connect_error) {
    die("Connessione fallita: " . $conn->connect_error);
}

echo "Connessione al database avvenuta con successo";

// Esegui le operazioni sul database...

// Chiusura della connessione
$conn->close();
```
### Operazioni sulle tabelle
- Creazione tabella
```php
// Query di creazione della tabella 
$sql = "CREATE TABLE users ( id INT(11) AUTO_INCREMENT PRIMARY KEY, nome VARCHAR(50) NOT NULL, email VARCHAR(50) NOT NULL, password VARCHAR(255) NOT NULL, data_registrazione TIMESTAMP DEFAULT CURRENT_TIMESTAMP )";
// Esecuzione della query 
if (mysqli_query($conn, $sql)) {
echo "Tabella 'users' creata con successo!"; } 
else { 
echo "Errore nella creazione della tabella: " . mysqli_error($conn); }
```
- Inserimento tuple
```php
// Dati del nuovo record 
$nome = "Mario Rossi"; $email = "mario@example.com"; $password = "mypass123"; 
// Query di inserimento 
$sql = "INSERT INTO users (nome, email, password) VALUES ('$nome', '$email', '$password')"; 
// Esecuzione della query 
if (mysqli_query($conn, $sql)) { echo "Nuovo record inserito con successo!"; } else { echo "Errore durante l'inserimento del record: " . mysqli_error($conn); }
```
- Aggiornamento
```php
// Dati dell'aggiornamento 
$id = 1; // ID del record da aggiornare 
$nome = "Nuovo nome"; $email = "nuovaemail@example.com"; 
// Query di aggiornamento 
$sql = "UPDATE users SET nome='$nome', email='$email' WHERE id=$id"; 
// Esecuzione della query 
if (mysqli_query($conn, $sql)) { echo "Record aggiornato con successo!"; } else { echo "Errore durante l'aggiornamento del record: " . mysqli_error($conn); }
```
- Cancellazione
```php
// ID del record da cancellare 
$id = 1; 
// Query di cancellazione 
$sql = "DELETE FROM users WHERE id=$id"; 
// Esecuzione della query 
if (mysqli_query($conn, $sql)) { echo "Record cancellato con successo!"; } else { echo "Errore durante la cancellazione del record: " . mysqli_error($conn); }
```
### Query al DB
```php
```
### Form con metodo GET
```html
<!DOCTYPE html>
<html>
<head>
    <title>Form con metodo POST</title>
</head>
<body>
    <form action="processa.php" method="GET">
        <label for="nome">Nome:</label>
        <input type="text" name="nome" id="nome">
        <br>
        <label for="cognome">Cognome:</label>
        <input type="text" name="cognome" id="cognome">
        <br>
        <input type="submit" value="Invia">
    </form>
</body>
</html>
```
```php
//INIZIO PHP
$nome = $_GET['nome'];
$cognome = $_GET['cognome'];

echo "Ciao, $nome $cognome!";
```
### Form con metodo POST
```html
<!DOCTYPE html>
<html>
<head>
    <title>Form con metodo POST</title>
</head>
<body>
    <form action="processa.php" method="POST">
        <label for="nome">Nome:</label>
        <input type="text" name="nome" id="nome">
        <br>
        <label for="cognome">Cognome:</label>
        <input type="text" name="cognome" id="cognome">
        <br>
        <input type="submit" value="Invia">
    </form>
</body>
</html>
```
```php
//INIZIO PHP
$nome = $_POST['nome'];
$cognome = $_POST['cognome'];

echo "Ciao, $nome $cognome!";
```
### Prepared Query
```php
// Parametri di connessione al database
$servername = "localhost";
$username = "nome_utente";
$password = "password";
$dbname = "nome_database";

try {
    // Creazione della connessione PDO
    $conn = new PDO("mysql:host=$servername;dbname=$dbname", $username, $password);

    // Imposta l'opzione per restituire le eccezioni in caso di errori
    $conn->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);

    // Esempio di prepared query per l'inserimento di dati
    $stmt = $conn->prepare("INSERT INTO nome_tabella (colonna1, colonna2) VALUES (:valore1, :valore2)");

    // Associa i valori ai parametri della query
    $stmt->bindParam(':valore1', $valore1);
    $stmt->bindParam(':valore2', $valore2);

    // Assegna i valori ai parametri
    $valore1 = "valore1";
    $valore2 = "valore2";

    // Esegui la query preparata
    $stmt->execute();

    echo "Dati inseriti correttamente";

} catch(PDOException $e) {
    echo "Errore nella connessione al database: " . $e->getMessage();
}

// Chiusura della connessione
$conn = null;
```
Nell'esempio sopra, viene utilizzato l'oggetto PDO per creare la connessione al database. Successivamente, viene preparata una query con valori parametrici utilizzando il metodo `prepare()`. I valori dei parametri vengono associati tramite il metodo `bindParam()` e quindi assegnati alle variabili. Infine, la query preparata viene eseguita utilizzando il metodo `execute()`.
### SQL Injection
**SQL injection** è una **vulnerabilità** che si **verifica quando le query** SQL **non** sono correttamente **sanificate o validate** e **consentono ad un attaccante di inserire comandi SQL non autorizzati** o dannosi all'interno di una query. In sostanza, un attaccante sfrutta l'input dell'utente per manipolare le query SQL e ottenere accesso non autorizzato al database o eseguire azioni indesiderate.
**Le soluzioni** per prevenire l'SQL injection includono:

1. **Utilizzare prepared statements o query parametriche**: Le prepared statements consentono di separare la struttura della query SQL dai dati inseriti dall'utente. I valori dei parametri vengono trattati separatamente dalla query e vengono automaticamente sanificati dal driver del database. Questo previene l'iniezione di codice dannoso.
Esempio di prepared statement in PHP utilizzando PDO:
```php
$stmt = $conn->prepare("SELECT * FROM utenti WHERE username = ?");
$stmt->execute([$username]);
```
2. **Utilizzare funzioni di escape**: Le funzioni di escape consentono di sanificare i dati inseriti dall'utente prima di utilizzarli nelle query SQL. Queste funzioni modificano i caratteri speciali in modo che vengano interpretati come parte dei dati e non come parte della query.
Esempio di escape string in PHP utilizzando la funzione `mysqli_real_escape_string()`:
```php
$username = mysqli_real_escape_string($conn, $_POST['username']);
$password = mysqli_real_escape_string($conn, $_POST['password']);
$query = "SELECT * FROM utenti WHERE username = '$username' AND password = '$password'";
```
3. **Limitare i privilegi del database**
4. **Validare e filtrare l'input dell'utente**
5. **Implementare meccanismi di autenticazione e autorizzazione**
6. **Mantenere il software aggiornato**
## Cookies e Sessioni in PHP
In PHP, i cookies e le sessioni sono strumenti utilizzati per gestire lo stato e mantenere le informazioni tra diverse richieste del browser. Entrambi i meccanismi consentono di memorizzare dati lato server o lato client durante l'interazione con un'applicazione web. 
### Cookies
- I cookies sono piccoli file di testo che vengono salvati sul dispositivo dell'utente (solitamente nel browser) quando si visita un sito web.
- In PHP, è possibile impostare, leggere e modificare i cookies utilizzando le funzioni native come `setcookie()` e `$_COOKIE`.
- I cookies possono essere utilizzati per memorizzare informazioni come preferenze dell'utente, dati di autenticazione o tracciamento delle attività dell'utente.
- I cookies vengono inviati dal server al client nel header HTTP e vengono inclusi nelle richieste successive dal client al server.
- È importante notare che i cookies sono memorizzati lato client e possono essere letti o modificati dall'utente.
```php
// Imposta un cookie
$cookieName = 'nome_cookie';
$cookieValue = 'valore_cookie';
$expiryTime = time() + 3600; // Scade dopo 1 ora

// La funzione setcookie() viene utilizzata per impostare un cookie
setcookie($cookieName, $cookieValue, $expiryTime, '/');

// Legge il valore di un cookie
if (isset($_COOKIE[$cookieName])) {
    $cookieValue = $_COOKIE[$cookieName];
    echo "Il valore del cookie è: " . $cookieValue;
} else {
    echo "Il cookie non è stato impostato.";
}
```
### Sessioni
- Le sessioni sono un meccanismo per mantenere lo stato dell'utente durante le interazioni con un'applicazione web.
- In PHP, una sessione viene creata quando l'utente accede al sito web e viene associata a un identificatore univoco chiamato session ID.
- L'identificatore di sessione viene solitamente memorizzato come un cookie nel browser dell'utente.
- Le informazioni di sessione vengono memorizzate lato server e possono includere variabili di sessione che mantengono i dati specifici dell'utente durante la sessione.
- Le variabili di sessione possono essere impostate, lette e modificate utilizzando l'array associativo `$_SESSION`.
- Le sessioni sono generalmente più sicure rispetto ai cookies perché i dati sensibili rimangono lato server.
- La durata di una sessione può essere configurata e una sessione può scadere dopo un certo periodo di inattività dell'utente o alla chiusura del browser.
```php
// Avvia la sessione
session_start();

// Imposta una variabile di sessione
$_SESSION['nome_variabile'] = 'valore_variabile';

// Accedi alla variabile di sessione
$nomeVariabile = $_SESSION['nome_variabile'];
echo "Il valore della variabile di sessione è: " . $nomeVariabile;

// Termina la sessione
session_destroy();
```
###### Esempio Sessioni
`index.php`
```php
// Avvia la sessione
session_start();

// Imposta una variabile di sessione
$_SESSION['username'] = 'emanuele';

echo 'Sessione avviata. <a href="pagina2.php">Vai alla pagina 2</a>';
```
Nel file `index.php` viene avviata una sessione utilizzando la funzione `session_start()`. Successivamente, viene impostata una variabile di sessione chiamata `'username'` con il valore `'emanuele'`. Infine, viene visualizzato un messaggio con un link per passare alla pagina successiva.

`pagina2.php`
```php
// Riprendi la sessione
session_start();

// Controlla se la variabile di sessione 'username' esiste
if (isset($_SESSION['username'])) {
    $username = $_SESSION['username'];
    echo 'Benvenuto, ' . $username . '!';

    // Cancella la variabile di sessione 'username'
    unset($_SESSION['username']);
} else {
    echo 'Accesso negato!';
}
```
Nel file `pagina2.php` viene ripresa la sessione utilizzando nuovamente la funzione `session_start()`. Viene poi controllato se la variabile di sessione `'username'` esiste. Se esiste, viene stampato un messaggio di benvenuto con il valore della variabile di sessione. Successivamente, la variabile di sessione `'username'` viene cancellata utilizzando `unset()` per simulare un logout.
## Ajax
### Esempio 1 
Invio di dati tramite metodo POST e gestione della risposta in PHP Javascript (AJAX):
```js
// Creazione dell'oggetto XMLHttpRequest
var xhr = new XMLHttpRequest();

// Definizione della funzione di gestione della risposta
xhr.onreadystatechange = function() {
  if (xhr.readyState === 4 && xhr.status === 200) {
    var response = xhr.responseText;
    console.log(response);
  }
};

// Configurazione della richiesta
xhr.open("POST", "process.php", true);
xhr.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");

// Creazione dei dati da inviare
var data = "param1=valore1&param2=valore2";

// Invio della richiesta
xhr.send(data);
```
PHP (process.php):
```php
// Recupero dei dati inviati tramite POST
$param1 = $_POST['param1'];
$param2 = $_POST['param2'];

// Elaborazione dei dati
// ...

// Creazione della risposta
$response = "Risposta elaborata";

// Invio della risposta
echo $response;
```
### Esempio 2
Caricamento di dati da un file PHP tramite metodo GET e gestione della risposta in JavaScript Javascript (AJAX):
```js
// Creazione dell'oggetto XMLHttpRequest
var xhr = new XMLHttpRequest();

// Definizione della funzione di gestione della risposta
xhr.onreadystatechange = function() {
  if (xhr.readyState === 4 && xhr.status === 200) {
    var response = xhr.responseText;
    console.log(response);
  }
};

// Configurazione della richiesta
xhr.open("GET", "data.php", true);

// Invio della richiesta
xhr.send();
```
PHP (data.php):
```php
// Recupero dei dati da una fonte (ad esempio un database)
$data = array(
  "valore1" => "Dato 1",
  "valore2" => "Dato 2",
);

// Conversione dei dati in formato JSON
$jsonData = json_encode($data);

// Invio dei dati come risposta
header("Content-Type: application/json");
echo $jsonData;
```