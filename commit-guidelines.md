# Linee Guida per Commit
#### 1. Fai commit di un unico tipo e solo di modifiche correlate
Un commit dovrebbe essere un contenitore di modifiche correlate tra loro cioè le modifiche al suo interno dovranno essere tutte mirate al raggiungimento di un unico scopo;  ad esempio se devi fissare due bachi distinti farai due commit separati. Il tool dello staging aiuta a fare commit molto granulari.

#### 2. Fai spesso commit
È più facile risolvere eventuali conflitti e includere solo modifiche correlate.

#### 3. Non fare commit di un lavoro a metà
Dovresti eseguire il commit del codice solo quando un componente logico è completato. Dividi l'implementazione di una funzionalità in blocchi logici che possono essere completati rapidamente in modo da poter committare spesso. Se hai bisogno di una workspace pulita (per estrarre un ramo, inserire modifiche, ecc.) considera invece l'utilizzo della funzione **Stash** di Git.

#### 4. Testa il codice prima di fare commit
Devi essere sicuro che il codice committato sia completo funzionante e senza effetti collaterali.

#### 5. Ogni commit deve avere un messaggio convenzionale
Ogni commit deve avere un messaggio di commit che deve seguire il formato descritto nei [paragrafi seguenti](#formato)

## <a name="formato"></a> Formato del Messagio di Commit
Ogni messaggio di commit è costituito da un'**intestazione**, un **corpo** e un **piè di pagina**
sempre separati da una riga vuota.
L'intestazione ha uno speciale formato che include un **tipo**, un **ambito** e un **oggetto**:

```
INTESTAZIONE (obbligatoria) ---->                 <tipo>(<ambito>): <oggetto>
                                                  <RIGA VUOTA>
CORPO (facoltativa) ---->                         <body>
                                                  <RIGA VUOTA>
PIE' DI PAGINA (facoltativa) ---->                <piè di pagina>
```

L'**intestazione** è obbligatoria mentre l'ambito dell'intestazione, il corpo e il piè di pagina sono
facoltativi.

Il soggetto nell'intestazione deve contenere al **max 50 caratteri** mentre ogni altra riga deve
contenere al **max 100 caratteri**.

**ESEMPI** (da angular):

```
docs(changelog): update changelog to beta.5
```
```
fix(release): need to depend on latest rxjs and zone.js

The version in our package.json gets copied to the one we publish, and users need the latest of these.
```
Più [esempi da angular](https://github.com/angular/angular/commits/master)

### 1. Tipo
Il tipo deve essere sempre presente, deve essere scritto con **caratteri minuscoli** e seguito dall'ambito opzionale e da due punti e uno spazio. Il **punto esclamativo** prima dei due punti indica una modifica importante de è accoppiato al `BREAKING CHANGE` nel piè di pagina. 

Il tipo deve essere uno dei seguenti:

* **build**: Modifiche al sistema di build, strumenti di sviluppo, dipendenze (non rilevanti per utente finale)
* **chore**: modifiche non visibili a utente finale (ad es file configurazione metodi interni privati modifiche .gitgnore ecc..)
* **docs**: Modifiche alla sola documentazione
* **feat**: Aggiunta di una nuova funzionalità
* **fix**: Risoluzione di un bug
* **perf**: Migliora le prestazioni e/o le funzionalità esistenti senza modifiche funzionali
* **refactor**: Modifiche nel codice incentrate sulla sua leggibilità, stile e approccio: non introduce nuove funzion né risolve problemi (stesso output approccio differente)
* **style**: Modifiche che non influiscono sul suo significato e logica (spazi bianchi, punti e virgola, formattazione)
* **test**: Aggiunge nuovi test o corregge quelli esistenti

#### Revert (ripristino)
Se il commit attuale ripristina un commit precedente, deve iniziare con "revert:", seguito dall'**oggetto del commit ripristinato**. Nel corpo dovrebbe essere indicato: `Questo ripristina il commit <SHA>.` e una descrizione chiara del **motivo** per il quale si è deciso di ripristinare il commit.

ESEMPIO:
```
revert: aggiorna changelog a beta.5

Questo commit ripristina il commit 4d755ec perché il changelog rifletta i cambiamenti reali
```


### 2. Ambito
L'ambito, sempre **racchiuso tra parentesi tonde**, è opzionale e indica il campo di visibilità o di azione delle modifiche ad esempio il nome del pacchetto interessato (come percepito dalla persona che legge il changelog generato dai messaggi di commit).

### 3. Oggetto
L'oggetto è obbligatorio e contiene una **descrizione sintetica** delle modifiche illustrando
brevemente cosa fa il commit:

* massimo 50 caratteri
* usa l'imperativo presente: "cambia" non "cambiato" né "cambiamenti"
* non scrivere in maiuscolo la prima lettera
* nessuna punteggiatura alla fine

### 4. Corpo
Il corpo è facoltativo ma quando è presente, come nel soggetto, usa l'imperativo presente e dovrebbe includere la **motivazione** per le modifiche evidenziando le **differenze con il comportamento precedente** e spiegare eventuali effetti collaterali.

* è sempre preceduto da una riga vuota,
* ogni riga del corpo è al massimo di 100 caratteri (poi si va a capo),
* può contenere più paragrafi che devono essere separati da una riga vuota,
* può contenere elenchi puntati le cui voci sono precedute da un - oppure da un *,

### 5. Piè di pagina
Il piè di pagina è opzionale e dovrebbe contenere ogni informazione sui **Breaking Changes** e deprecazioni; è anche il punto in cui
[referenziare gli issue di GitHub](https://help.github.com/articles/closing-issues-via-commit-messages/)
o le pull request che il commit **Chiude** usando una delle seguenti parole chiave:
* `close`
* `closes`
* `fix`
* `fixed`
* `resolve`
* `resolves`
* `resolved`

La sintassi per le parole chiave di chiusura dipende da dove si trovi l'issue: nello stesso repository della pull request oppure su uno diverso.

|Issue collegato	 |Sintassi |Esempio |
|:---------- |:---------- |:---------- |
|Issue nello stesso repository |PAROLA-CHIAVE #NUMERO-ISSUE |`Closes #10` |
|Issue in un diverso repository	|PAROLA-CHIAVE PROPRIETARIO/REPOSITORY#NUMERO-ISSUE	|`Fixes octo-org/octo-repo#100` 
|Issue multipli	|Usa la sintassi completa per ogni issue	|`Resolves #10, resolves #123, resolves octo-org/octo-repo#100`

La sezione **Breaking Changes** dovrebbe iniziare con l'espressione `BREAKING CHANGE:` seguita da uno spazio e un riepilogo della modifica sostanziale, una riga vuota e una descrizione dettagliata della modifica sostanziale che include anche le istruzioni sulla migrazione.

Allo stesso modo, una sezione di **deprecazione** dovrebbe iniziare con `DEPRECATED:` seguito da uno spazio e una breve descrizione di ciò che è deprecato, una riga vuota e una descrizione dettagliata della deprecazione che menziona anche il percorso di aggiornamento consigliato.

ESEMPI:
```
BREAKING CHANGE: <riepilogo delle modifiche di rilievo>
<RIGA VUOTA>
<descrizione della modifica sostanziale + istruzioni sulla migrazione>
<RIGA VUOTA>
<RIGA VUOTA>
Fixes #<numero issue>
```
oppure:
```
DEPRECATED: <cosa è deprecato>
<RIGA VUOTA>
<descrizione della deprecazione + percorso di aggiornamento consigliato>
<RIGA VUOTA>
<RIGA VUOTA>
Closes #<numero pull request>
```