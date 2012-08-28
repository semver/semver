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

### How should I deal with revisions in the 0.y.z initial development phase?

The simplest thing to do is start your initial development release at 0.1.0
and then increment the minor version for each subsequent release.

### How do I know when to release 1.0.0?

If your software is being used in production, it should probably already be
1.0.0. If you have a stable API on which users have come to depend, you should
be 1.0.0. If you're worrying a lot about backwards compatibility, you should
probably already be 1.0.0.

### Doesn't this discourage rapid development and fast iteration?

Major version zero is all about rapid development. If you're changing the API
every day you should either still be in version 0.x.x or on a separate
development branch working on the next major version.

### If even the tiniest backwards incompatible changes to the public API require a major version bump, won't I end up at version 42.0.0 very rapidly?

This is a question of responsible development and foresight. Incompatible
changes should not be introduced lightly to software that has a lot of
dependent code. The cost that must be incurred to upgrade can be significant.
Having to bump major versions to release incompatible changes means you'll
think through the impact of your changes, and evaluate the cost/benefit ratio
involved.

### Documenting the entire public API is too much work!

It is your responsibility as a professional developer to properly document
software that is intended for use by others. Managing software complexity is a
hugely important part of keeping a project efficient, and that's hard to do if
nobody knows how to use your software, or what methods are safe to call. In
the long run, Semantic Versioning, and the insistence on a well defined public
API can keep everyone and everything running smoothly.

### What do I do if I accidentally release a backwards incompatible change as a minor version?

As soon as you realize that you've broken the Semantic Versioning spec, fix
the problem and release a new minor version that corrects the problem and
restores backwards compatibility. Remember, it is unacceptable to modify
versioned releases, even under this circumstance. If it's appropriate,
document the offending version and inform your users of the problem so that
they are aware of the offending version.

### What should I do if I update my own dependencies without changing the public API?

That would be considered compatible since it does not affect the public API.
Software that explicitly depends on the same dependencies as your package
should have their own dependency specifications and the author will notice any
conflicts. Determining whether the change is a patch level or minor level
modification depends on whether you updated your dependencies in order to fix
a bug or introduce new functionality. I would usually expect additional code
for the latter instance, in which case it's obviously a minor level increment.

### What should I do if the bug that is being fixed returns the code to being compliant with the public API (i.e. the code was incorrectly out of sync with the public API documentation)?

Use your best judgment. If you have a huge audience that will be drastically
impacted by changing the behavior back to what the public API intended, then
it may be best to perform a major version release, even though the fix could
strictly be considered a patch release. Remember, Semantic Versioning is all
about conveying meaning by how the version number changes. If these changes
are important to your users, use the version number to inform them.

### How should I handle deprecating functionality?

Deprecating existing functionality is a normal part of software development and
is often required to make forward progress. When you deprecate part of your
public API, you should do two things: (1) update your documentation to let
users know about the change, (2) issue a new minor release with the deprecation
in place. Before you completely remove the functionality in a new major release
there should be at least one minor release that contains the deprecation so
that users can smoothly transition to the new API.


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
