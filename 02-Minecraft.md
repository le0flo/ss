# Minecraft

### [Guida ai controlli](README.md), ultima revisione 11/9/2024

É giusto pensare ai controlli cheats, come una branca dell’informatica forense, ma a differenza delle indagini di forensica digitale, i controlli cheats sono legati molto al gioco che li ospita in primo luogo. Ecco perché qui vi spiego da un punto di vista di tecnico, il gioco Minecraft, insieme ai vari tipi di cheats che ci possiamo aspettare.

### Il gioco e Java

Come ben sappiamo, Minecraft è scritto in java, questo implica che come processo non esisterà mai un ipotetico “minecraft.exe”, bensì Minecraft sarà una semplice task all’interno di un processo della Java Virtual Machine _(java.exe o javaw.exe)_. Il gioco, non essendo appunto scritto in un linguaggio direttamente compilato _(c, c++, c#, rust, etc...)_, viene avviato tramite dei launcher. I launcher si occupano semplicemente di tenere un log delle attività, di offrire alcune peculiarità rispetto a quello default e infine, la cosa più ovvia, scopo stesso dei launcher, è il fatto che hanno un comando personalizzato per avviare il gioco _(in poche parole, un java -jar con tanti argomenti)_. I launcher dicono a Minecraft la sua cartella radice. Per essere più precisi, Minecraft, come tutti i giochi, non ha tutte le informazioni, come texture e assets vari, all’interno dell’eseguibile, bensì si appoggiano su una cartella radice, con all’interno un sistema di cartelle che ordina i vari file e risorse di cui necessita il gioco. La cartella di Minecraft, con l’installazione vanilla, si trova in `C:\Users\{username}\AppData\roaming\.minecraft`. Questo non significa che si può trovare esclusivamente li. Un esempio può essere MultiMC, un launcher usato da modders e player tecnici di Minecraft, che ha come peculiarità quella di creare una cartella di gioco separata per ogni versione, cosa molto comoda per i modders, poichè permette di tenere ordinate tutte le mod e configurazioni necessarie per diverse esperienze di gioco. Per accedere alla cartella di Minecraft giusta, segui la successione sottoscritta:

```
Gioco > (ESC) > Opzioni > Pacchetti Risorse (Resource Packs) > Apri cartella pacchetti risorse.
```

Questa azione aprirà la cartella resource packs sul disco, che ha come parente, la cartella radice di Minecraft.

### I tipi cheats

I cheaters hanno a disposizione una tra le più vaste gamme di cheat rispetto a qualsiasi altro gioco, questo tutto per alcune peculiarità del gioco _(spoler: Java)_. Prima di partire a scheggia su come trovare i cheats, direi che è meglio avere una base teorica su cosa ci dobbiamo aspettare, cosa dobbiamo trovare in quanto staffer, sul pc del player. I client si dividono in quattro categorie principali, che poi analizzeremo per bene:

- Ghost clients
- Injection clients
- External clients
- Autoclickers
- Macro e Debounce timer

Ora i prossimi paragrafi saranno dedicati esclusivamente alla spiegazione nel dettaglio di questi client e di alcune cose fondamentali da sapere, non che metodi vari.

### Ghost clients

Frse i client più semplici da trovare, per la quantità di prove che lasciano alla loro esecuzione, ma anche i più sottovalutati. Per definizione i Ghost clients possono essere:

- Versioni
- Mod
- Librerie

Queste vanno a modificare il gioco fornendo al player vantaggi sleali. La versione è un file .jar del gioco Minecraft modificato che si trova nella cartella ".minecraft/version". Le mod permettono di modificare il gioco senza intaccare la versione originale del gioco. Le librerie, sono i vari file .jar che minecraft usa per fare operazioni basiche, come il rendering etc.., che vengono modificate per aggiungere codice malevolo al gioco, solo un client particolarmente famoso usava questa tecnica, "Serenity".

Se siete dei bravi detective, avete già notato un pattern particolare con questi tipi di clients. Il loro obbiettivo è eseguire codice direttamente all’interno di Minecraft, che poi sia tramite versione o tramite mod o tramite libreria conta poco; quello che conta è il loro scopo, modificare il codice del gioco dall’interno. Una proprietà fondamentale di questi client, è che per la loro natura, non si possono trovare fuori dalla cartella radice di Minecraft. Per finire, essendo parte diretta del gioco, possono essere trovati nella memoria del processo di Minecraft.

### Injection clients

I Ghost clients furono la prima tipologia di cheats creata ma, presto gli anticheat divennero migliori, come le persone che controllavano i giocatori. Ci voleva qualcosa di nuovo e quel qualcosa si è rivelato essere l'Injection client. Questi clients riescono ad accedere al gioco, non facendone direttamente parte. Questo li rende molto più difficili da trovare.

Per capirci qualcosa, forse è meglio capire a il loro funzionamento. Come detto precedentemente, Minecraft è scritto in Java, e esso stesso, fornisce i tools con cui noi sviluppatori possiamo interfacciarci con la Java Virtual Machine. In particolare, questa interfaccia viene usata per implementare del codice compilato _(c, c++, rust)_ all'interno di un programma Java. Queste librerie sono JNI e JvmTI, rispettivamente Java Native Interface e Java Virtual Machine Tool Interface. Non mi soffermerò troppo su JvmTI, ma vi basta sapere che è la versione aggiornata e più sicura di JNI, che al contrario, è molto datata.

Gli Injection clients sono delle librerie dinamiche _(.dll, .dylib, .so)_, che attaccandosi al processo di Minecraft, si iniettano al suo interno, grazie all’interfaccia fornita dalle librerie JNI e JvmTI. Questi clients riescono a modificare il codice del gioco a loro piacimento. É fondamentale capire che gli Injection clients sono soltanto delle librerie. I "cheat makers" però rendono l’utilizzo del cheat più "user friendly", hanno creato dei semplici eseguibili che si occupano di iniettare la libreria, all’interno del processo di Minecraft. Modificando il codice del gioco dall’interno, si possono trovare tracce di questi client nel processo di Minecraft ma, è più difficile trovare altre tracce poichè non sono limitati alla cartella radice di Minecraft.

### External clients

La principale differenza e innovazione rispetto ai precedenti Injection client, è il fatto che loro accedono in modo diverso alla memoria del gioco. Se prima i Ghost e gli Injection riuscivano ad interfacciarsi internamente col gioco, quindi modificando classi e perciò costrutti di alto livello, gli External clients agiscono su costrutti di basso livello, su valori singoli della memoria. Non c’è la necessità che si iniettino all’interno di un processo perché, almeno parlando di Windows, l'API di sistema fornisce funzioni per modificare i valori della memoria dato un indirizzo valido e l’Handle di un processo. Agendo su valori singoli della memoria, è virtualmente impossibile per noi staffer capire se un player ha usato o no un external client basandoci sulla memoria del processo di Minecraft. Come definizione generale si può dare la seguente: Gli external clients sono dei client che agiscono su valori singoli della memoria. Per concludere, questo fatto di poter agire su valori invece che costrutti di alto livello, li limita in ambito di funzionalità.

### Autoclickers

Gli autoclickers, non sono perforza legati a Minecraft in se per se. Essi esistono da molto più tempo e sono molto facili da nascondere. Interagiscono poco con il processo di Minecraft, sfruttando invece l'API del rispettivo sistema operativo per simulare i click. Non essendo trovabili nella memoria del processo di Minecraft, assumono un pattern di ricerca nel pc, simile a quello applicato agli External clients ma, bisogna stare attenti. A differenza degli External clients, gli autoclickers possono essere scritti in linguaggi compilati e non, il che aumenta la quantità di artefatti da controllare e le casistiche possibili.

### Macro e Debounce timer

Le macro sono molto semplici come concetto. Sono delle istruzioni che si assegnano ad un tasto tramite un software esterno o dedicato alla periferica scelta. Su Minecraft, si utilizzano per aumentare la velocità dei click del player. Il Debounce timer invece è un argomento caldo sulla quale discutere, ma vorrei chiarire comunque sulla posizione del debounce timer come cheat. Il debounce timer è una feature dei mouse che è stata implementata tanto tempo fa, per prevenire un problema con gli switch dei mouse. Essendo gli switch essenzialmente una molla, quando cliccati rimbalzano, inviando al computer un secondo, terzo, quarto click e così via. Il debounce timer, è il tempo che il firmware del mouse aspetta prima di inviare un secondo segnale di click al computer. Quando un click viene registrato, parte un timer che dura N millisecondi _(generalmente 10 o 16 ms)_, evitando qualsiasi tipo click accidentale da parte del mouse. Questa feature, su alcuni mouse, è modificabile o totalmente rimovibile, permettendo al player di cliccare più del dovuto, facendo uso di particolari metodi, innescando un "double click". Questi metodi rientrano tutti nella categoria di "Mouse Abuse". Su alcuni server, il debounce timer sotto 10ms è bannabile, proprio perché viene considerato un vantaggio sleale nei confronti del player medio, fornito di un mouse non adatto al double clicking. Su determinati server viene considerato cheating, l'uso di metodi "Mouse Abuse" se in possesso di mouse roccat o bloody, poichè, nonostante la capacità di attivare il debounce timer per evitare il double click, risulta difettoso. Per evitare confusione, basta seguire in modo preciso il regolamento del server.

### Conclusioni

Abbiamo visto in modo approfondito, quali sono i possibili cheats che dobbiamo cercare su Minecraft, come riconoscerli e le loro caratteristiche.
