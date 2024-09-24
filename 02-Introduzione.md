# Introduzione ai controlli cheats

### [Guida ai controlli](01-Indice.md), ultima revisione 11/9/2024

Un caldo benvenuto da parte mia e da tutta la community SS a chiunque tu sia, che hai deciso di leggere questa guida. Prima di iniziare ci tengo a precisare due cose:

- Questa guida è stata pensata per essere completa, non per forza semplice o intuitiva. Pur coprendo la maggiorparte degli aspetti dei controlli e alcuni dello' informatica forense, questa non è una guida che favorisce chiunque. Se si decide di leggere questa guida bisogna avere una mente libera da ogni preconcetto appreso sui controlli, oltre all'essere aperta per imparare nuove cose, ad accettare nuovi concetti ma, saper anche usare anche lo spirito critico e valutare anche degli eventuali errori, perché pur essendo questa opera di dimensioni mai viste, con un attenta valutazione di tutto ciò che viene spiegato, non tutte le nozioni fornite possono essere precise;

- Questa guida è stata scritta interamente dal sottoscritto _(Leonardo)_, ogni nozione fornita qua è puramente scritta da me. Ciò non significa che le cose imparate le ho inventate io ma, sicuramente non sono stati altri a scriverle così, men che meno ad insegnarle in questo modo. É una guida destinata al pubblico e deve essere, di conseguenza, di pubblico dominio. Questa collezione di documenti è stata pubblicata sotto la licenza GPL 3.0.

***Detto questo, Buona lettura ...***

### Controlli, uno sguardo generale

Il controllo, anche conosciuto come screenshare in inglese, è una pratica che gli staffer utilizzano per dimostrare che un player sta o meno utilizzando dei cheats. Per avere un minimo di conoscenza base su alcuni termini dei controlli partirei proprio da uno dei punti dolenti: il bypass. La definizione comune di bypass è la seguente: “Il bypass avviene quando lo staffer non riesce a trovare i cheats ad un player, nonostante lui li stava utilizzando". Questa è definizione è molto generica e _(secondo me)_ soltanto fonte di dibattito inutile. In primis, molte persone hanno diversi significati di "trovare i cheats", ma io penso che non esista una definizione unica su come trovare i cheats. Ci possono essere due tipi di server, quelli che bannano per possesso e quelli che non lo fanno. Se parliamo di server che bannano per il possesso, trovare un cheat si limita a trovare le tracce dell’esistenza di un cheat qualsiasi in un arco di tempo stabilito dal regolamento. Non ci si dovrebbe preoccupare più di tanto degli orari di esecuzione, poichè è la prova dell’esistenza del cheat in primo luogo a contare come prova per il ban. Purtroppo, pochi server decidono di bannare ancora con questi criteri, perciò ora discutiamo della categoria principale di server:

#### La dimostrazione dell’esecuzione.

Essendo questa una introduzione non mi soffermerò su ogni modo per dimostrare l’esecuzione di un programma ma, ci terrò a precisare due cose fondamentali. Bisogna in questi casi, avere prove che un file eseguibile _(.exe, .jar, etc...)_ o una libreria _(.dll, .dylib, .so)_ sia stata utilizzata e un timestamp che riporta l'orario di esecuzione, poichè un cheat può essere considerato in due modi:

- "fuori istanza"
- "in istanza"

Per istanza si intende il processo di minecraft attuale, perciò bisogna confrontare l’esecuzione del cheat, con il timestamp di avvio del processo di minecraft. Ban fatti per altre motivazioni sarebbero imprecisi e/o senza abbastanza prove. Tutto dipende, alla fine della giornata, dalle regole del server ma, è anche necessario avere una conoscenza base delle casistiche in cui si banna e in cui no. Detto questo per ricollegarci al concetto dei bypass, un ban è valido finché  rispetta le regole del server, non quelle inventate dalla community. Ci tengo a specificarlo perché nel tempo, molteplici episodi di disguidi altamente inutili tra staffers e bypassers hanno avuto luogo, proprio per colpa di incoerenze tra le varie scuole di pensiero riguardo all'argomento bypass. Assumendo che lo staffer in questione abbia seguito alla lettera il suo regolamento e le prove che ha fornito sono necessarie per giustificare il ban, un bypasser non ha motivo di contestare. Un altra casistica invece è, quando lo staffer non trova niente, il bypasser dice di aver usato un "client privato" e lo staffer si sente come giustificato a non aver trovato niente. Purtroppo non funziona così. Nelle varie tecniche per fare controlli ci sono infiniti metodi per dimostrare che un artefatto sia un cheat, perciò lo staffer non è giustificato se il bypasser ha usato un “client privato”. Per concludere, farsi bypassare succede. Gli staffer non dovrebbero bannare per paura di essere bypassati. Si praticano i controlli per eliminare i cheater, non per costruire una reputazione. Alla fine è soltanto un gioco.

#### Strumentazione

I controlli non si fanno di certo evocando demoni pagani o leggendo nella mente del player. Vari strumenti vengono utilizzati per praticare lo screenshare. Gli strumenti usati li possiamo separare in 3 categorie _(2 principali)_:

- Strumenti per la condivisione schermo
- Strumenti per la ricerca di cheats:
    - Tools automatici
    - Tools manuali

Partendo dalla prima, gli strumenti per la condivisione schermo penso siano i più conosciuti; Di questa categoria, fanno parte programmi come:

- Anydesk
- Rustdesk
- Discord
- Teamviewer
- Skype

Preferibile è la situazione in cui lo staffer ha la possibilità di utilizzare mouse e tastiera del pc del player, quindi l’utilizzo di anydesk dovrebbe essere la norma. In alcune casistiche si può usare una semplice presentazione dello schermo ma, è rara come occasione nonché molto inefficace come approccio.

Gli strumenti per la ricerca dei cheats, sono tutti quei programmi che utilizziamo per dimostrare che il player è in possesso e utilizzo di cheats. I tools manuali ci permettono di analizzare una vasta gamma di artefatti, lasciando a noi l'interpretazione di essi e la decisione sul fato del controllato. I tools automatici per controlli, controllano automaticamente vari artefatti, e confrontano le prove con i loro metodi, per verificare se un player ha utilizzato cheats. Questi tool vanno usati con cautela. É sempre meglio avere una conoscenza avanzata dei controlli prima di affidarsi ai tools automatici. Nonostante essi rendono veloce il controllo, aumentano esponenzialmente la quantità di falsi positivi, rendendo più frequenti le casistice di ban ingiusto. Ci sono tante cose da prendere in considerazione se si vuole fare uso di suddetti strumenti, perciò sconsiglio l’uso dei tool automatici ai principianti. Esempi di tool automatici possono essere:

- SSDetector
- Echo
- Avenge