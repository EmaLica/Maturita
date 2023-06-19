---
Data: 19th June 2023
Descrizione: sintassi XML e struttura ad albero dei documenti, definizione di XML mediante schemi XSD, definizione degli elementi semplici e degli attributi. Body di una request o di una response http in formato JSON e XML
---
# XML e JSON
### Sintassi XML e struttura ad albero dei documenti
**XML**, acronimo di eXtensible Markup Language, **è un linguaggio di markup** che consente di definire regole personalizzate per la struttura dei documenti. Un documento XML è costituito da **elementi**, **attributi** e **testo**. La sintassi XML richiede che ogni elemento sia racchiuso tra tag di apertura e chiusura, ad esempio:
```xml
<nomeElemento>Contenuto</nomeElemento>
```
Gli elementi possono contenere altri elementi o testo, formando una struttura ad albero. Ad esempio:
```xml
<persona>
  <nome>Mario</nome>
  <cognome>Rossi</cognome>
</persona>
```

### Definizione di XML mediante schemi XSD
Gli **XML Schema Definition** (**XSD**) sono **file utilizzati per definire la struttura**, il **tipo e i vincoli dei documenti XML**. Uno schema XSD specifica quali elementi possono essere presenti, quali attributi possono avere e quali valori sono accettabili. Gli schemi XSD definiscono il "contratto" per la struttura dei documenti XML.

###### Esempio file XML
```xml
<person>
  <name>John Doe</name>
  <age>30</age>
</person>
```

###### Schema XSD del file XML &uarr;
```xml
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">

  <xs:element name="person">
    <xs:complexType>
      <xs:sequence>
        <xs:element name="name" type="xs:string"/>
        <xs:element name="age" type="xs:positiveInteger"/>
      </xs:sequence>
    </xs:complexType>
  </xs:element>

</xs:schema>
```

### Definizione degli elementi semplici e degli attributi
Gli **elementi XML** possono essere di **due tipi**: elementi **complessi** e elementi **semplici**. Un elemento **semplice contiene solo testo**, mentre un elemento **complesso può contenere altri elementi**. Gli attributi, invece, forniscono informazioni aggiuntive sugli elementi.

Esempio di definizione di un elemento semplice:
```xml
<xs:element name="nome" type="xs:string"/>
```
Nell'esempio sopra, l'elemento "nome" è definito come un elemento semplice di tipo stringa.

Esempio di definizione di un attributo:
```xml
<xs:attribute name="id" type="xs:int"/>
```

### Body di una request o di una response HTTP in formato JSON e XML
Il body di una richiesta o di una risposta HTTP può essere formattato in diversi formati, tra cui **JSON e XML**. Ecco un esempio di come potrebbe apparire il body di una richiesta o di una risposta in entrambi i formati.

**JSON**:
```json
{
  "nome": "Emanuele",
  "cognome": "Licata"
}
```

**XML**:
```xml
<persona>
  <nome>Mario</nome>
  <cognome>Rossi</cognome>
</persona>
```

Entrambi gli esempi rappresentano lo stesso insieme di dati, ma utilizzano formati differenti. **JSON utilizza la sintassi degli oggetti JavaScript**, mentre **XML utilizza una struttura ad albero** con elementi e tag di apertura/chiusura.