Semantic Versioning 2.0.0-rc.1
==============================

Nel mondo della gestione del software esiste un posto terribile chiamato
"inferno delle dipendenze". Più cresce il sistema, più crescono i pacchetti 
da integrare in esso e più è probabile ritrovarsi, un giorno, in questa
valle di lacrime.

Nei sistemi con molte dipendenze, il rilascio di nuove versioni dei package 
può diventare presto un incubo. Se le specifiche sulle dipendenze sono troppo
stringenti, si corre il rischio di finire quanto prima in un cosiddetto
_version lock_ (ossia l'impossibilità di aggiornare un package senza dover
anche rilasciare le nuove versioni di ciascun altro package ad esso dipendente).
Se invece le dipendenze sono troppo lasche, si verrà inevitabilmente colti dal
fenomeno della _version promiscuity_ (assumendo una compatibilità con più versioni future
di quanto non sia ragionevole).
L'inferno delle dipendenze si ha appunto quando ci si trova in una di queste 
due situazioni estreme - version lock e/o version promiscuity - che impedisce
l'aggiornamento facile e sicuro del progetto.

Come soluzione a questo problema, propongo un semplice insieme di regole 
e requisiti che determinino come i numeri di versione vengano assegnati e incrementati.
Affinché questo metodo funzioni, si deve innanzitutto dichiarare un API pubblica.
Questa può essere semplicemente documentazione o meglio ancora codice che ne 
valida i vincoli. A prescindere, l'importante è che un API simile sia chiara e precisa.
Una volta identificate le tue API pubbliche, si comunicano le modifiche ad esse
attraverso incrementi specifici al numero di versione.
Si consideri un formato di versione del tipo X.Y.Z (Major.Minor.Patch).
Le risoluzioni ad anomalie che non intaccano le firme delle API causano un incremento della
sola componente patch del numero di versione, aggiunte/modifiche retrocompatibili delle API 
causano un incremento della componente minor del numero di versione version, e infine
modifiche non retrocompatibili delle API si traducono nella modifica della componente
major del numero di versione.

Chiamo questo metodo "Semantic Versioning." Seguendo questo sistema, i numeri
di versione e il modo in cui cambiano nel tempo assume un significato ben preciso
sul tipo di modifiche avvenute sul codice.


Specifiche del Semantic Versioning (SemVer)
-------------------------------------------

Le parole chiave "DEVE" ("MUST"), "NON DEVE" ("MUST NOT"), "OBBLIGATORIO" ("REQUIRED"), "SHALL", "SHALL NOT", "DOVREBBE" ("SHOULD"),
"NON DOVREBBE" ("SHOULD NOT"), "CONSIGLIATO" ("RECOMMENDED"), "PUO'" ("MAY"), e "OPZIONALE" ("OPTIONAL") in questo documento sono da intendersi
secondo quanto descritto nell'RFC 2119.

1. Il software che utilizza il Semantic Versioning DEVE dichiarare una API pubblica. Questa API
può essere dichiarata nel codice stesso oppure esistere esclusivamente nella documentazione.
Comunuqe sia, dovrebbe essere precisa e completa.

1. Un numero di versione normale DEVE essere della forma X.Y.Z dove X, Y, e Z sono
interi non negativi. X è il numero di versione _major_, Y è il _minor_, e Z
è quello di _patch_. Ognuno di questi numeri DEVE aumentare numericamente per incrementi di
uno. Per esempio: 1.9.0 -> 1.10.0 -> 1.11.0.

1. Una volta che un package versionato è stato rilasciato, i contenuti di tale versione
NON DEVONO essere modificati. Qualsiasi modifica deve essere rilasciata come nuova versione.

1. La versione *major* zero (0.y.z) serve per lo sviluppo iniziale. Tutto può cambiare in qualunque
momento. L'API pubblica non dovrebbe essere considerata stabile.

1. La versione *1.0.0* definisce l'API pubblica. Il modo in cui il numero di versione si
incrementa dopo questa release dipende dalle API pubbliche specifiche e da come cambiano.

1. La verione *patch* Z (x.y.Z | x > 0) DEVE essere incrementata solamente se le modifiche
introdotte sono tutte risoluzioni di anomalie retrocompatibili. Si definisce risoluzione di anomalia
una modifica al codice interno che corregge un comportamento non corretto del software.

1. La versione *minor* Y (x.Y.z | x > 0) DEVE essere incrementata quando vengono introdotte
nuove funzionalità retrocompatibili alle API pubbliche. DEVE essere incrementata se una
qualunque delle funzionalità esposte dalle API pubbliche viene contrassegnata come
deprecata. PUO' essere incrementata qualora siano introdotte sostanziali nuove funzionalità o 
miglioramenti nel codice. PUO' anche includere modifiche a livello di patch. La versione patch
DEVE essere riportata a 0 quando la versione minor viene incrementata.

1. La versione *major* X (X.y.z | X > 0) DEVE essere incrementata qualora una qualsiasi
modifica non retrocompatibile sia introdotta nelle API pubbliche. PUO' includere 
modifiche di livello minor e patch. Le versioni patch e minor DEVONO essere riportate a 0
quando la versione major viene incrementata.

1. Una versione di pre-release PUO' essere contrassegnata aggiungendo - subito dopo la versione patch -
un trattino seguito da una serie di identificatori separati da punti. Gli identificatori
DEVONO essere composti esclusivamente da caratteri ASCII alfanumerici e trattini [0-9A-Za-z-].
Le versioni di pre-release soddisfano i requisiti della versione normale, ma hanno rispetto
ad essa una precedenza minore. Esempi: 1.0.0-alpha, 1.0.0-alpha.1, 1.0.0-0.3.7,
1.0.0-x.7.z.92.

1. Una versione di build PUO' essere contrassegnata aggiungendo - subito dopo la versione patch 
o di pre-release - un segno più seguito da una serie di identificatori separati da punti.
Gli identificatori DEVONO essere composti esclusivamente da caratteri ASCII alfanumerici e 
trattini [0-9A-Za-z-]. Le versioni di build soddisfano i requisiti della versione normale ed
hanno rispetto ad essa una precedenza maggiore. Esempi: 1.0.0+build.1, 1.3.7+build.11.e0f985a.

1. La precedenza DEVE essere calcolata separando le versioni in major, minor, patch, 
identificatori di pre-release e identificatori di build in questo ordine. 
Le versioni major, minor, e patch vengono sempre confrontate numericamente.
La precedenza fra versioni di pre-release e di build DEVE essere determinata
per comparazione di ciascun identificatore separato da punto in questo modo:
gli identificatori costituiti da soli caratteri numerici sono confrontati 
numericamente e gli identificatori costituiti da soli caratteri letterari
o trattini sono confrontti lessicalmente secondo i criteri di ordinamento ASCII.
Gli identificatori numerici hanno sempre precedenza minore rispetto a quelli non 
numerici. Esempi: 1.0.0-alpha < 1.0.0-alpha.1 < 1.0.0-beta.2 < 1.0.0-beta.11 <
1.0.0-rc.1 < 1.0.0-rc.1+build.1 < 1.0.0 < 1.0.0+0.3.7 < 1.3.7+build <
1.3.7+build.2.b8f12d7 < 1.3.7+build.11.e0f985a.

Perché usare il Semantic Versioning?
------------------------------------

Non si tratta di un'idea rivoluzionaria. Infatti, probabilmente, state già
utilizzando convenzioni simili a questa. Il problema è che l'approssimazione
della similitudine non è sufficiente. Fintanto che non sono conformi ad una
qualche specifica formale, i numeri di versione sono essenzialmente inutili
ai fini di una gestione delle dipendenze. Dando un nome ed una definizione
precisa alle idee di cui sopra, diventa facile comunicare le proprie intenzioni
agli utenti del vostro software. Una volta che queste intenzioni sono chiare, 
si possono finalmente produrre specifiche di dipendenza flessibili (ma non troppo).

Un semplice esempio dimostrerà come il Semantic Versioning può rendere l'inferno
delle dipendenze un qualcosa di legato al passato. Si consideri una libreria
chiamata "Firetruck." Questa richiede un package chiamato "Ladder", versionato 
semanticamente. All'epoca in cui è stata creata Firetruck, Ladder era alla versione
3.1.0. Dal momento che Firetruck utilizza alcune delle funzionalità che erano
state originariamente introdotte nella 3.1.0, si può tranquillamente indicare in
modo sicuro la dipendenza verso Ladder come maggiore o uguale a 3.1.0, ma minore
di 4.0.0. Ora, nel momento in cui diventano disponibili le versioni 3.1.1 e 3.2.0 
della libreria Ladder, le si possono mettere a disposizione del proprio sistema
di gestione dei pacchetti sapendo che saranno compatibili con il software già
esistente dipendente da Ladder.

Da bravo sviluppatore, naturalmente, vorrai controllare che ciascun aggiornamento 
di package funzioni come pubblicizzato. Il mondo reale è un luogo disordinato;
non ci possiamo fare nulla se non essere vigili. Ciò che puoi fare è lasciare che 
il Semantic Versioning ti fornisca un modo sano per rilasciare e aggiornare
i package, senza essere costretti a lanciare nuove versioni dei pacchetti di dipendenza,
facendoti risparmiare tempo e fatica.

Se tutto ciò ti appare desiderabile, tutto ciò che devi fare per iniziare ad usare il
Semantic Versioning è di dichiarare che lo stai facendo e poi iniziare a eguire le regole.
Metti anche un collegamento a questo sito web all'interno del tuo README, affinché anche
altri possano apprendere le regole e possano trarne a loro volta benefici.


FAQ
---

### Come mi dovrei trattare le revisioni 0.y.z nella fase iniziale dello sviluppo?

La cosa più semplice da fare è quella di cominciare con un rilascio iniziale di sviluppo alla 0.1.0
e incrementare sucessivamente la versione minor ad ogni nuovo rilascio.

### Quando decido di passare alla release 1.0.0?

Se il tuo software è usato in produzione, dovrebbe probabilmente già essere in versione 1.0.0.
Se si hanno delle API stabili su cui gli utenti possono cominciare a stabilire delle dipendenze,
allora si dovrebbe già essere in 1.0.0.
Se ci si stanno ponendo dubbi sulla retrocomaptibilità, allora si dovrebbe già essere in 1.0.0.

### Tutto ciò non disincentiva lo sviluppo rapido e le iterazioni veloci?

La versione major zero è tutta oriantata allo sviluppo rapido. Se si stanno cambiando quotidianamente
le API, o si è ancora in version 0.x.x, oppure in un ramo di sviluppo separato, al lavoro sulla prossima
versione major.

### Se anche la minima modifica non retrocompatibile alle API pubbliche richiede l'avanzamento di versione major, non si rischia di finire alla versione 42.0.0 troppo in fretta?

Qui si tratta di una questione di sviluppo responsabile e lungimiranza.
Le modifiche che introducono incompatibilità non dovrebbero essere introdotte
alla leggera nel software che ha molte dipendenze con altro codice. Il costo 
nel quale si potrebbe incappare per un eventuale aggiornamento dell'altro
software potrebbe essere non trascurabile.
Il fatto di dover portare avanti la versione major al ogni rilascio di modifiche incompatibili
implica che si sia indotti a pensare molto bene all'impatto delle proprie scelte e a valutare
altrettanto bene il rapporto costo/beneficio del cambiamento.

### La documentazione dei tutte le API pubbliche è un lavoro troppo oneroso!

Rientra nelle responsabilità di uno sviluppatore professionista la corretta documentazione
del software che si intende fornire a disposizione di altri. La gestione della complessità
del software è una grossa e importante parte del compito di mantenere efficiente un progetto
ed è difficile farlo se nessuno sa come si usa il vostro software, o quali metodi possono 
essere invocati in modo sicuro. Nel lungo termine, il Semantic Versioning, e la disciplina 
nel mantenere un ben definito insieme di API pubbliche, può fare in modo che tutto
proceda in modo liscio.

### Cosa facico se per sbaglio rilascio una modifica non retrocompatibile come una versione minor?

Non appena ci si accorge di aver violato la specifica del Semantic Versioning, si deve
correggere il problema e rilasciare una nuova versione minor che ripristini la 
retrocompatibilità. Si tenga sempre presente che è inaccettabile cambiare le versioni
già rilasciate, anhe in questa circostana. Se è il caso, tuttalpiù, si documenti opportunamente
la versione errata e si informino gli utenti del problema, affinché siano al corrente del
problema.

### Cosa devo fare se aggiorno le mie stesse dipendenze senza cambiare l'interfaccia pubblica delle mie API?

Un'operazione del genere è da considerarsi compatibilie, in quanto non intacca le API pubbliche.
Il software che ha dipendenze esplicite nei confronti delle medesime dipendenze del vostro package
dovrebbe avere le proprie specifiche di dipendenza e l'autore noterà eventuali conflitti.
Stabilire se la modifica debba considerarsi a livello di patch o di minor dipende sostanzialmente
dalle ragioni per cui si è deciso di procedere all'aggiornamento di dipendenze sul proprio package:
se lo si è fatto per correggere un'anomalia, piuttosto che per introdurre nuove funzionalità.
Tipicamente mi aspetterei ulteriore codice nel secondo caso, per cui in tal caso si tratterebbe 
ovviamente di una nuova versione minor.

### Che cosa devo fare se è il codice correttivo dell'anomalia risolta a fare in modo che il codice sia aderente alle API pubbliche (es. il codice era erroneamente disallineato rispetto alla documentazione delle API pubbliche)?

Si usi il buon senso. Se si ha un audience così vasta per il proprio package che 
la modificha avrebbe un impatto evidentemente molto importante, riportando 
il comportamento ad una situazione coerente con ciò che era inteso dalle specifiche
della documentazione pubblica delle API, allora potrebbe valer la pena di rilasciare 
il tutto come una nuova versione major, anche se tecnicamente si tratterebbe solo 
di una correzione di livello patch. 
Si ricordi che il Semantic Versioning è funzionale alla definizione di un significato
condiviso sul cambio del numero i versione. Se queste modifiche sono importanti per i
vostri utenti, si utilizzi il numero di versione in modo opportuno per informarli in
merito.

### Come devo trattare le funzionalità deprecate?

La deprecazione di parti esistenti di funzionalità è un processo normale dello sviluppo
del software e spesso si rende necessario per realizzare dei progressi. Quando si 
depreca una parte delle proprie API pubbliche, si devono fare due cose:
(1) aggiornare la documentazione per notificare gli utenti circa il cambiamento
(2) preventivare un nuovo rilascio di versione minor contenente la deprecazione.
Prima di rimuovere completamente la funzionalità in un ulteriore nuovo rilascio major,
dovrebbe intercorrere almeno una minor release contenente la deprecazione, al fine di permettere
agli utenti della vostra libreria una transizione non traumatica alle nuove API.


About
-----

Le specifiche di Semantic Versioning sono state scirtte da [Tom
Preston-Werner](http://tom.preston-werner.com), inventore di Gravatars e
co-fodatore di GitHub.
La traduzione in italiano è stata curata da [Andrea Salicetti](http://www.andreasalicetti.com), socio
e sviluppatore di Blomming.

Se volete lasciare un feedback, [aprite una segnalazione su GitHub](https://github.com/mojombo/semver/issues).


Licenza
-------

Creative Commons - CC BY 3.0
http://creativecommons.org/licenses/by/3.0/
