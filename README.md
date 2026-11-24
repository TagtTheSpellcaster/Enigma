# Emulatore Storico Enigma M3 & M4

![Version](https://img.shields.io/badge/version-1.0-blue.svg)
![License: AGPL v3](https://img.shields.io/badge/License-AGPL_v3-blue.svg)
![HTML5](https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-Vanilla-F7DF1E?logo=javascript&logoColor=black)
![GitHub Pages](https://img.shields.io/badge/GitHub%20Pages-Ready-222222?logo=github)

Un emulatore interattivo, storicamente e crittograficamente fedele, delle celebri macchine cifranti elettromeccaniche **Enigma M3** (usata dall'esercito tedesco) ed **Enigma M4** (usata dai sommergibili U-Boot della marina tedesca). Realizzato in un unico file autosufficiente senza librerie esterne, pensato per la didattica, la divulgazione storica e lo studio della crittografia.

## Indice dei contenuti

1. [Che cos'è e come nasce Enigma](#che-cosè-e-come-nasce-enigma)
2. [Come funziona la macchina (spiegato semplice)](#come-funziona-la-macchina-spiegato-semplice)
3. [L'impiego militare e la differenza tra M3 e M4](#limpiego-militare-e-la-differenza-tra-m3-e-m4)
4. [La violazione del codice: dai matematici polacchi a Bletchley Park](#la-violazione-del-codice-dai-matematici-polacchi-a-bletchley-park)
5. [Guida all'uso dell'emulatore](#guida-alluso-dellemulatore)
6. [Installazione e pubblicazione su GitHub Pages](#installazione-e-pubblicazione-su-github-pages)
7. [Licenza](#licenza)

## Che cos'è e come nasce Enigma

Oggi diamo per scontato che i nostri messaggi su WhatsApp o le nostre password viaggino protetti da sistemi matematici invisibili. Cento anni fa, però, per inviare un messaggio segreto via radio (dove chiunque avesse un'antenna poteva intercettarlo) bisognava trasformare il testo in una sequenza incomprensibile di lettere usando cifrari scritti a mano su tabelle di carta. Era un processo lento e pieno di errori umani.

Nel **1918**, alla fine della Prima Guerra Mondiale, un ingegnere tedesco di nome **Arthur Scherbius** brevettò un'invenzione rivoluzionaria: **Enigma**. All'inizio non era pensata per la guerra: Scherbius la vendeva a banche e grandi aziende per proteggere i segreti commerciali e i telegrammi finanziari.

A partire dalla fine degli anni Venti, però, le forze armate tedesche (prima la Marina e poi l'Esercito e l'Aviazione) capirono il potenziale straordinario di quella macchina. La acquistarono, la modificarono aggiungendo nuovi livelli di sicurezza e la resero il cuore delle comunicazioni militari della Germania nazista durante tutta la **Seconda Guerra Mondiale**.

## Come funziona la macchina (spiegato semplice)

A prima vista Enigma sembra una grossa macchina da scrivere chiusa in una scatola di legno. In realtà **non stampa nulla su carta**: funziona con una batteria, dei fili elettrici e delle lampadine.

Quando premi un tasto (per esempio la lettera **`A`**), la corrente elettrica parte dalla batteria, attraversa un labirinto di cavi e fa accendere una lampadina con sopra scritta un'altra lettera (per esempio **`G`**). Un secondo operatore seduto accanto legge la lettera illuminata e la annota su un foglio.

Ma qual è il segreto che rendeva Enigma così difficile da decifrare? **Il labirinto cambia forma ad ogni singolo tasto premuto.**

Ecco i 4 componenti principali che attraversa la corrente elettrica:

### 1. Il Pannello a Prese (*Steckerbrett* o *Plugboard*)

Sul davanti della macchina ci sono 26 prese, una per ogni lettera dell'alfabeto. Prima ancora di iniziare a scrivere, l'operatore collega alcune coppie di lettere con dei cavi elettrici (di solito 10 cavi, che scambiano 20 lettere).

* Se colleghi un cavo tra **`A`** e **`V`**, ogni volta che premi `A` la macchina la trasforma subito in `V` prima ancora che il segnale raggiunga i rotori.

### 2. I Rotori (*Walzen*)

Sono il vero cervello meccanico di Enigma. Sono dischi spessi con 26 contatti elettrici su una faccia e 26 sull'altra, collegati all'interno da un groviglio di fili incrociati.

* **Il movimento a contachilometri:** Ogni volta che premi un tasto, **prima** che passi la corrente, il rotore di destra scatta in avanti di una posizione (esattamente come i numeri del contachilometri di un'auto o le lancette di un orologio). Quando il rotore di destra ha fatto un giro completo (26 scatti), fa avanzare di uno scatto il rotore centrale; quando quello centrale fa un giro completo, fa scattare quello di sinistra.
* **Perché è geniale?** Se premi due volte di fila il tasto **`E`**, la prima volta si accenderà ad esempio la lampadina **`K`**, mentre la seconda volta i rotori si sono già spostati e si accenderà la **`P`**. Un cifrario di questo tipo si chiama **polialfabetico**.
* **L'anello (*Ringstellung*):** Ogni rotore ha anche un anello esterno con le lettere dalla `A` alla `Z` (numerate da `01` a `26`) che può essere ruotato rispetto ai fili interni, aggiungendo un ulteriore livello di sfasamento.

### 3. Il Riflettore (*Umkehrwalze*)

In fondo ai rotori c'è un disco fisso che non gira, chiamato **riflettore**. Riceve il segnale elettrico, lo scambia su un altro filo e lo **rimanda indietro** attraverso gli stessi rotori, ma lungo un percorso diverso, fino a uscire di nuovo dal pannello a prese e accendere la lampadina finale.

> **Il trucco della reciprocità (come si decifra un messaggio?):**
> Proprio grazie al riflettore, Enigma è una macchina **simmetrica**: non esiste un interruttore "Cifra / Decifra". Se con una certa configurazione iniziale premendo **`A`** si accende **`G`**, allora riportando i rotori alla stessa identica posizione iniziale e premendo **`G`**, la corrente farà il percorso esattamente al contrario e accenderà **`A`**!
> Per questo motivo, chi riceveva un messaggio via radio doveva solo impostare la propria Enigma esattamente come quella del mittente e digitare il testo cifrato: sulle lampadine compariva il messaggio in chiaro.

### Il numero astronomico delle combinazioni

Scegliendo 3 rotori su 5 disponibili, impostandone le posizioni iniziali, gli anelli interni e 10 cavi sul pannello frontale, la Enigma M3 poteva essere configurata in circa **158 milioni di miliardi di miliardi** ($1,58 \times 10^{20}$) di modi diversi. Per i vertici militari tedeschi era matematicamente inviolabile.

## L'impiego militare e la differenza tra M3 e M4

I comandanti tedeschi distribuivano ogni mese un **libro delle chiavi** (*Schlüsselzettel*), un foglio stampato con inchiostro rosso solubile in acqua (così da poterlo distruggere in un secchio d'acqua in caso di cattura). Su questo foglio era scritta la **chiave del giorno**: quali rotori montare, su quali lettere posizionarli all'inizio della giornata e quali cavi collegare.

* **Enigma M3 (Wehrmacht — Esercito e Aviazione):** Utilizzava **3 rotori** scelti tra 5 disponibili (`I–V`) e un riflettore standard (`UKW-B` o `UKW-C`). I messaggi venivano trasmessi in codice Morse divisi in gruppi di **5 lettere** (*Fünfergruppen*).
* **Enigma M4 (Kriegsmarine — Sommergibili U-Boot):** Nel 1942 l'ammiraglio Karl Dönitz sospettò che gli Alleati stessero leggendo i messaggi dei suoi sommergibili nell'Atlantico. Fece progettare una versione potenziata: la **M4**. Per far entrare **4 rotori** nella stessa scatola di legno della M3, gli ingegneri costruirono un riflettore più sottile (*UKW dünn*) e un quarto rotore sottile (*Zusatzwalze*, chiamato **Beta** o **Gamma**) posizionato all'estrema sinistra. Questo quarto rotore poteva essere regolato all'inizio, ma non ruotava durante la digitazione. I messaggi navali venivano trasmessi in gruppi di **4 lettere** (*Vierergruppen*).

## La violazione del codice: dai matematici polacchi a Bletchley Park

La storia di come Enigma fu sconfitta è una delle pagine più affascinanti della storia della scienza e dimostra che nessun sistema è davvero invincibile se si analizzano gli errori umani e la matematica.

### 1. I pionieri polacchi (1932–1939)

Contrariamente a quanto si pensa spesso, i primi a violare Enigma non furono gli inglesi, ma tre giovani matematici polacchi dell'Ufficio Cifra di Varsavia: **Marian Rejewski**, **Jerzy Różycki** e **Henryk Zygalski**.

* A partire dal 1932, Rejewski usò la **teoria dei gruppi** (una branca dell'algebra astratta) per ricostruire da zero il cablaggio interno dei rotori senza aver mai visto una macchina militare tedesca.
* I polacchi costruirono anche le prime macchine elettromeccaniche per trovare le chiavi giornaliere, chiamate **Bomba** (*Bomba kryptologiczna*).
* Nell'estate del **1939**, poche settimane prima che la Germania invadesse la Polonia, i servizi segreti polacchi convocarono a Varsavia i crittanalisti britannici e francesi e consegnarono loro i progetti e due repliche funzionanti di Enigma. Fu un regalo decisivo per le sorti della guerra.

### 2. Bletchley Park e Alan Turing (1939–1945)

In Gran Bretagna il lavoro proseguì in gran segreto nella tenuta vittoriana di **Bletchley Park**, dove lavorarono migliaia di persone (in gran parte donne, matematici, linguisti, campioni di scacchi ed enigmisti).

Il matematico inglese **Alan Turing**, insieme al collega **Gordon Welchman**, progettò una macchina elettromeccanica molto più potente chiamata **Bombe**. La *Bombe* non provava tutte le combinazioni a caso, ma sfruttava due punti deboli fondamentali di Enigma:

1. **Nessuna lettera poteva mai essere cifrata in sé stessa:** a causa del circuito del riflettore, una `A` non diventava mai `A`. Questo permetteva di scartare istantaneamente milioni di posizioni sbagliate.
2. **Le parole prevedibili (*Cribs*):** I tedeschi erano molto metodici. Ogni mattina alle 6:00 inviavano il bollettino meteorologico che conteneva quasi sempre la parola *WETTERBERICHT* ("bollettino meteo") e chiudevano molti messaggi con *HEIL HITLER*. Indovinando dove si trovavano queste parole nel testo cifrato, la *Bombe* di Turing riusciva a dedurre la configurazione dei rotori in poche ore.

Quando nel 1942 entrò in servizio la **Enigma M4** degli U-Boot, Bletchley Park rimase "al buio" per quasi dieci mesi, durante i quali i sommergibili tedeschi affondarono centinaia di navi alleate. Il codice fu violato di nuovo grazie alla cattura dei libri cifrari dal sommergibile **U-559** e alla costruzione di *Bombe* ancora più veloci, contribuendo ad accorciare la Seconda Guerra Mondiale di almeno due anni e gettando le basi per la nascita dei moderni computer.

## Guida all'uso dell'emulatore

L'applicazione riproduce fedelmente l'aspetto, i suoni meccanici e la logica matematica originale.

### 1. Scegliere la macchina (in alto a destra)

Usa il selettore metallico in alto a destra per passare istantaneamente tra:

* **`M3 (3 Rotori)`**: finitura in mogano caldo, 3 rotori (`I–V`), riflettori `UKW-B` / `UKW-C` e nastro telegrafico in gruppi da **5 lettere**.
* **`M4 (4 Rotori)`**: finitura in rovere scuro marinato, 4 rotori (*Zusatzwalze* `Beta`/`Gamma` evidenziato in ottone + 3 rotori `I–VIII`), riflettori sottili `UKW-B dünn` / `UKW-C dünn` e nastro in gruppi da **4 lettere**.

*Nota: Le due macchine mantengono configurazioni, cavi e nastri completamente indipendenti in memoria.*

### 2. Configurare i rotori (*Walzenlage* e *Ringstellung*)

* **Tipo di rotore:** Usa i menu a tendina in cima a ciascun alloggiamento per scegliere quali rotori inserire. Nella M4, i rotori `VI`, `VII` e `VIII` riportano `(2x)` perché possiedono due tacche di avanzamento (`Z` e `M`).
* **Posizione iniziale:** Clicca sui pulsanti **`▲`** e **`▼`** accanto a ogni finestrella (oppure usa la **rotella del mouse** direttamente sopra la finestra o la ruota zigrinata) per impostare le lettere iniziali.
* **Anello (*Ring*):** Usa il selettore in basso in ogni blocco per regolare lo sfasamento dell'anello interno (`01-A` fino a `26-Z`).

### 3. Collegare i cavi (*Steckerbrett*)

* Clicca su una lettera nel pannello inferiore e poi su una seconda lettera: verrà tracciato un cavo intrecciato colorato tra le due prese. Cliccando su una presa già occupata, il cavo viene scollegato.
* In alternativa, puoi scrivere direttamente le coppie nel campo **`Coppie:`** (es. `AV BS CG DL`) e premere **Applica**.

### 4. Cifrare e decifrare un messaggio

* Digita con la tua **tastiera fisica** (`A–Z`) oppure clicca sui tasti circolari della **Tastatur** QWERTZ.
* Osserva i rotori scattare in avanti (incluso il celebre fenomeno meccanico del *double-stepping* del rotore centrale) e la lampadina corrispondente illuminarsi sul **Glühlampenfeld**.
* Sul **nastro di carta** in basso vedrai sia il testo digitato sia il risultato cifrato.
* **Prova a decifrare:** Dopo aver cifrato una parola (es. `CIAO`), annota il risultato cifrato, riporta i rotori alla posizione iniziale di partenza e digita il testo cifrato: sul nastro riapparirà `CIAO`!

### 5. I Test Storici Autentici (Pulsante dorato in alto a sinistra)

Cliccando il pulsante dorato in alto a sinistra puoi eseguire due vere decifrazioni storiche documentate negli archivi:

* **In modalità M3 — Test Barbarossa 1941:** Imposta la chiave reale dell'esercito tedesco del **7 luglio 1941** (Riflettore `B`, rotori `II-IV-V`, anelli `02-21-12`, posizione `B-L-A`) e decifra automaticamente sul nastro l'inizio di un vero bollettino dell'Operazione Barbarossa (`AUFKL XABTE ILUNG...`).
* **In modalità M4 — Test U-264 1942:** Imposta la chiave reale del sommergibile **U-264** del capitano Hartwig Looks del novembre **1942** (Riflettore `UKW-B dünn`, rotori `Beta-II-IV-I`, anelli `01-01-01-22`, posizione `V-J-N-A`) e decifra il vero messaggio intercettato nell'Atlantico (`VONV ONJL OOKS...`).

## Installazione e pubblicazione su GitHub Pages

Il progetto è composto da un unico file HTML (`index.html`) privo di dipendenze esterne.

1. Crea un nuovo repository su GitHub (es. `enigma-emulator`).
2. Carica nella cartella principale i file `index.html` e `README.md`.
3. Vai su **Settings** $\rightarrow$ **Pages** nel tuo repository.
4. Sotto la voce **Source**, seleziona `Deploy from a branch`, scegli il branch `main` e la cartella `/ (root)`, quindi clicca su **Save**.
5. Dopo pochi secondi il tuo emulatore sarà online e accessibile da qualsiasi computer, tablet o smartphone.

## Licenza

Questo progetto è distribuito sotto licenza **GNU Affero General Public License v3.0 (AGPL-3.0)**.
Puoi usare, studiare, modificare e redistribuire liberamente il codice sorgente, a condizione che ogni versione modificata o resa disponibile in rete mantenga la stessa licenza libera e aperta.