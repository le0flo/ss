# I processi e la memoria RAM

### [Guida ai controlli](01-Indice.md), ultima revisione 11/9/2024

I processi sono la parte più importante nel mondo dei controlli e della forensica digitale. I processi sono le istanze di un programma _(.exe per windows)_ in esecuzione. I processi vengono gestiti nella CPU, dal PCB _(Process Control Block)_ e il TCB _(Thread control block)_. Questi, gestiscono rispettivamente processi e thread e hanno informazioni sulla loro memoria, il loro ultimo avvio, le loro risorse e così via. Una applicazione come "Task Manager", indica tutti i processi che sono in esecuzione, ma si limita ad indicare i processi e il loro impatto sull’hardware _(percentuale di ram usata, cpu etc..)_. Per avere una visione più dettagliata, possiamo usare programmi come "Process Explorer" dalla Sysinternal suite e tanti altri simili. Il più utilizzato in ambito controlli è proprio "System Informer" _(ex. Process Hacker)_. Da notare è il fatto che, parlando di Windows, stiamo interagendo con un sistema proprietario e non saremo mai in possesso del codice sorgente di tale sistema operativo. Ciò implica che le nostre capacità di indagine si limitano a questi programmi offerti da queste persone. Non si riesce ad ottenere in modo semplice qualsiasi tipo di informazione se non fornita dalla "Windows API".

Quando un programma viene avviato, viene creato un processo, che contiene le seguenti informazioni _(P.S. non sono tutte)_:

- Il file eseguibile da cui deriva il processo
- Il path di quel file
- Il processo parente
- La console parente
- Gli argomenti con cui è stato avviato
- La directory a cui sta accedendo
- I threads
- I moduli
- La memoria allocata al processo
- Il programma stesso
- Gli Handles

Cerchiamo di spiegare ora queste varie informazioni riguardo al processo. Piccola premessa, tutte queste informazioni sono riguardo hai processi che sono in esecuzione, quando un processo viene terminato, le informazioni elencate li sopra non sono salvate, almeno non raw. Sistemi come il prefetch salvano alcune di quelle informazioni con obbiettivo di ottimizzazione ad un successivo avvio del medesimo programma, ma le informazioni raw così non sono salvate da nessuna parte, anche perché la ram è appunto una memoria volatile, oltre che incredibilmente limitata rispetto alla dimensione dei programmi.

### Processo parente

Il processo parente, è il processo che ha avviato quel programma. Se noi facciamo doppio click su un eseguibile di qualsiasi tipo, il processo parente di quel processo sarà "explorer.exe". Una cosa molto importante è il fatto che processi particolari come i servizi, hanno sempre dei processi parente noti, quindi un ipotetico processo che prova a fingersi un servizio di sistema è facile da notare, in quantp esso non ha lo stesso processo parente del servizio emulato e/o di qualsiasi servizio comune. Il 90% dei servizi ha come processo parente "services.exe", oppure "svchost.exe". Servizi come il "csrss.exe" e "wininit.exe" non hanno un processo noto come parente, perché essi sono avviati direttamente dal sistema operativo.

### Argomenti di avvio

Gli argomenti con cui un processo è stato avviato, sono le opzioni che si possono fornire ad un programma per alterare l'input iniziale. Alcuni processi hanno lo stesso eseguibile, ma si distinguino per gli argomenti di avvio, apparendo come processi separati ed autonomi.

### I threads

Nei sistemi moderni, ogni processo ha uno o più thread, ed è un modo di suddividere il lavoro della CPU. Il processo di Minecraft ha tanti thread, come alla fine ogni processo di un programma moderno.

### I moduli

I file eseguibili non hanno spesso tutto il codice al loro interno. Facendo un esempio semplice, chiunque abbia provato a vedere la cartella di gioco di fortnite, ha visto che ci sono "FortniteWinShipping64.exe", che è l’eseguibile responsabile per l’avvio di fortnite. Questo pesa relativamente poco, una cosa come 200 Megabytes. Non sembra normale, considerando che il gioco pesa 60 Gigabytes e più. Questo perché fa utilizzo delle librerie dinamiche. Le librerie dinamiche o DLL su Windows, sono librerie che possono essere caricate dai programmi per usufruire di assets statici o pezzi di codice. La comodità sta nella loro dinamicità. Possono essere caricate da un programma più volte e a piacimento. Questo permette una condizione fondamentale nei sistemi moderni: la risuabilità del codice. I moduli sono importanti per trovare un cheater. Un esempio noto può essere Minecraft. I cheat maker, sia che si tratta di  un Injection client, sia che si tratti di un External client, non vanno a mirare il processo “javaw.exe” in se per se, bensì un modulo particolare, il "jvm.dll". Questo modulo contiene le istruzioni della jvm appena creata, quindi il codice del gioco. Risulta perciò un punto di accesso per i cheater, alla memoria del processo. Quando un Injection client si collega a Minecraft, crea un collegamento particolare con questo modulo e tramite librerie come JNI viene a contatto con il codice arbitrario del gioco. Gli External clients, per modificare i valori specifici della memoria, vanno a cercare gli offsets degli indirizzi che puntano al modulo "jvm.dll", poichè è dove effettivamente quei valori si trovano. I moduli di un processo sono fondamentali per capire cosa fa.

### Gli handles

Meglio conosciuti come "Risorse" in italiano, gli handles sono ogni singolo file aperto da un determinato processo. Per esempio, quando andiamo a fare il self destruct di una mod, non possiamo eliminarla o spostarla. Questo perché l’handle che il processo di Minecraft ha su quel file è ancora attivo. Il metodo bypass per "unloaddare" una mod, consiste nell'andare manualmente con process hacker a chiudere l’handle che la "Java Virtual Machine" ha sulla mod, rendendola così spostabile ed eliminabile. Qualsiasi risorsa aperta dal processo si trova negli handles. Alcune di queste informazioni vengono salvate nel prefetch, come i nomi degli eseguibili, le risorse e le directory aperte, ma i prefetch sono manipolabili in vari modi, e di conseguenza possono risultare inaffidabili. Un artefatto importante nei controlli, è controllare la memoria di alcuni processi. All’interno ci potrebbero essere segnali dell’esecuzione avvenuta di determinati programmi, a volte possibili cheats. Metodi come il "pcaclient" si basano su questa proprietà della memoria del processo.

Ora facciamo una breve lista di processi e servizi utili in un controllo:

#### explorer.exe

Forse il più noto, l’explorer è la shell che ci permette di interagire graficamente con il sistema operativo, e ha tante informazioni importanti. Osservando come la memoria del processo si comporta, si è notato che ogni file visualizzato nell’explorer appare nella sua memoria, come altre cose tra cui il "pcaclient", utile per vedere gli ultimi 10 processi eseguiti (metodo deprecato ma comunque utile da controllare)

#### csrss.exe

Il "client server runtime process" è forse l’artefatto più importante di tutti. Ogni eseguibile viene registrato nella memoria di questo processo. Sembrerebbè il metodo finale. Purtroppo per noi però la Windows API, può dare problemi di permessi quando si tratta di accedere alla memoria di processi delicati come il soprascritto e questo è uno di quegli esempi più noti. Molto spesso neanche System Informer può accedere a tale memoria e programmi tools automatici si possono scordare di avere accesso a questa parte di memoria. Con questo processo, possiamo provare che un programma è stato eseguito, ma senza alcuna informazione riguardo il quando. In questi casi, è importante capire se un cheat era in istanza oppure no. Il "csrss.exe" un processo utilissimo per i nostri scopi, nonstante la sua difficoltà nell’accederci. Metodi in sviluppo ci permettono di scaricare tutta la memoria RAM e isolare quella di determinati processi. Chissà in un prossimo futuro potremmo automatizzare il controllo del "csrss.exe" e approfondire la nostra conoscenza su questi processi di basso livello.

#### msmpeng.exe

Questo è il processo del servizio anti-malware del Windows Defender. Un processo poco conosciuto e poco esplorato, ma pieno di potenzialità. Facendo parte della suite di antivirus di Windows, ha informazioni su tutti i programmi eseguiti e quindi possibili flag di cheats in particolare.

### Conclusione

Tantissimi altri processi vengono revisionati per l'estrazione di artefatti. Io ho scelto quelli più affidabili e utili in un vero controllo, secondo la mia umile opinione. Il mondo delle "stringhe" magiche di Process Hacker è un mondo superficiale e che si basa su tanti falsi positivi e metodi volatili, che un giorno vanno e un altro no. Quando si ha a che fare con la memoria RAM, bisogna realizzare che essa è volatile. Le stringhe sono utili in situazioni molto specifiche, ma non sono niente in confronto allo studio accurato di artefatti più importanti e che ci danno un sguardo generale su cosa è successo nel computer. Lo studio della memoria RAM in modo avanzato sta andando avanti e si stanno scoprendo artefatti nuovi. È un mondo complicato e difficile da tradurre in informazioni significative per noi umani, ciò nonostante è un argomento fondamentale nelle indagini forensi.