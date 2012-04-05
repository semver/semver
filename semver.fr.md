Le versionnement sémantique 2.0.0-rc.1
======================================

Dans le monde de la gestion de logiciels, il existe un endroit terrifiant appelé
"l'enfer des dépendances" (de l'anglais dependencies hell). Plus votre système
se développe et plus vous intégrez de composants dans votre logiciel, plus vous
êtes susceptible de vous trouver un jour dans cette abîme de désespoir.

Dans les systèmes avec de nombreuses dépendances, publier une nouvelle version
d'un composant peut vite devenir un cauchemar. Si les règles de dépendance sont
trop strictes, vous risquez de verrouiller les versions (incapacité de mettre à
jour un composant sans avoir à publier une nouvelle version de chaque composant
qui en dépend). Si les règles de dépendances sont trop lâches, vous allez
inévitablement être rattrapé par la promiscuité de version (supposez une
compatibilité avec plus de futures versions que raisonnable). L'enfer des
dépendances est l'endroit où vous vous trouvez lorsque les verrous de versions
ou la promiscuité de versions vous empêchent d'avancer sans risque dans votre
projet.

Comme solution à ce problème, je propose un ensemble de règles et exigences
simples qui dictent la façon dont les numéros de version sont attribués et
incrémentés. Pour que ce système fonctionne, vous devez d'abord déclarer une API
publique. Il peut s'agir d'un document ou de règles appliquées par le code
lui-même. Quoiqu'il en soit, il est important que cette API soit claire et
précise. Une fois que celle-ci est prête, vous communiquez ses modifications avec
les incrémentations spécifiques à votre numéro de version. Considérons le format
de version "X.Y.Z" (Majeur.Mineur.Patch). Les correctifs n'affectant pas l'API
incrémentent la version de patch, des ajouts ou modifications rétro-compatibles
incrémentent la version mineure et les modifications rétro-incompatibles
incrémentent la version majeure.

J'appelle ce système "versionnement sémantique". Avec ce système, les numéros
de version et la façon dont ils changent donnent du sens au code sous-jacent et
à ce qui a été modifié d'une version à l'autre.


Spécifications du versionnement sémantique (SemVer)
---------------------------------------------------

Les mots clés "DOIT", "NE DOIT PAS", "OBLIGATOIRE", "DEVRAIT", "NE DEVRAIT PAS",
"RECOMMANDÉ", "PEUT", et "OPTIONNEL" dans ce document doivent être interprétés
comme décrit dans la RFC 2119.

1. Tout logiciel utilisant le Versionnement Sémantique DOIT déclarer une API
publique. Cette API peut être déclarée dans le code lui-même ou dans un
document. Dans tous les cas, elle doit être précise et claire.

1. Un numéro de version standard DOIT prendre la forme X.Y.Z où X, Y et Z sont
des entiers non négatifs. X est la version majeure, Y est la version mineure, et
Z est la version de patch. Chaque élément DOIT augmenter numériquement par
incréments d'une unité. Par exemple : 1.9.0 -> 1.10.0 -> 1.11.0.

1. Quand un numéro de version majeur est incrémenté, la version mineure et la
version patch DOIVENT être remises à zéro. Quand un numéro de version mineur est
incrémenté, la version patch DOIT être remise à zéro. Par exemple:
1.1.3 -> 2.0.0 et 2.1.7 -> 2.2.0.

1. Une fois qu'une version d'un composant est publiée, le contenu de cette
version NE DOIT PAS être modifié. Toute modification doit être publiée comme une
nouvelle version.

1. La version majeure zéro (0.y.z) sert au développement initial. Tout peut
changer à tout moment. L'API publique ne devrait pas être considérée comme stable.

1. La version 1.0.0 définit l'API publique. La façon dont le numéro de version
est incrémenté après la publication est dépendante de cette API publique.

1. La version de patch Z (x.y.Z | x > 0) DOIT être incrémentée si des
corrections d'anomalies rétro-compatibles sont effectuées. Une correction
d'anomalie est définie comme un changement interne qui corrige un comportement
incorrect.

1. La version mineure Y (x.Y.z | x > 0) DOIT être incrémentée si une nouvelle
fonctionnalité rétro-compatible est introduite dans l'API publique. Elle DOIT
être incrémentée si une fonctionnalité de l'API publique est marquée comme
obsolète. Elle PEUT être incrémentée si une nouvelle fonctionnalité ou
amélioration est introduite dans le code privé. Elle PEUT inclure des
changements de niveau de patch. La version de patch DOIT être remise à 0 lorsque
la version mineure est incrémentée.

1. La version majeure X (X.y.z | X > 0) DOIT être incrémentée si des changements
rétro-incompatibles sont introduits à l'API publique. Elle PEUT inclure des
changements mineurs et de patch. Les numéros de version de patch et mineurs
DOIVENT être remis à 0 lorsque la version majeure est incrémentée.

1. Une version admissible PEUT être notée par l'ajout d'un tiret et une
série d'identifiants séparés par des points suivant immédiatement la version de
patch. Les identifiants DOIVENT être composés uniquement de caractères
alphanumériques ASCII et de tirets [0-9A-Za-z-]. Des versions de prépublication
sont utilisables et précèdent la version normale associée (version de
prépublication < version normale). 
Exemples : 1.0.0-alpha, 1.0.0-alpha.1, 1.0.0-0.3.7, 1.0.0-x.7.z.92.

1. Une version de construction PEUT être représentée par l'ajout d'un signe
"plus" et d'une série d'identifiants séparés par des points suivant
immédiatement la version de patch ou de prépublication. Les identifiants DOIVENT
être composés uniquement de caractères alphanumériques ASCII et de tirets
[0-9A-Za-z-]. Les versions de construction sont utilisables et suivent 
la version normale associée (version de construction > version normale). 
Exemples: 1.0.0+build.1, 1.3.7+build.11.e0f985a.

1. La priorité DOIT être calculée en séparant les numéros de version, dans
l'ordre, en identifiants majeur, mineur, patch, de prépublication et de
construction. Les numéros de version majeur, mineur, et de patch sont toujours
comparés numériquement. Pour les versions de prépublication et de construction,
la priorité DOIT être déterminée en comparant chaque identifiant séparé par un
point comme suit : les identifiants composés de chiffres seulement sont comparés
numériquement et les identifiants composés de lettres ou de tirets sont comparés
dans l'ordre de tri ASCII. Les identifiants numériques précèdent les
identifiants non numériques (identifiants numériques < identifiants
non-numériques). Exemple : 1.0.0-alpha < 1.0.0-alpha.1 < 1.0.0-beta.2 <
1.0.0-beta.11 < 1.0.0-RC.1 < 1.0.0-RC.1+build.1 < 1.0.0 < 1.0.0+0.3.7 <
1.3.7+build < 1.3.7+build.2.b8f12d7 < 1.3.7+build.11.e0f985a.


Pourquoi utiliser le versionnement sémantique ?
-----------------------------------------------

Cette idée n'est ni nouvelle ni révolutionnaire. Vous utilisez déjà probablement
un système similaire. Le problème est que "similaire" n'est pas suffisant. Seul
le respect d'une certaine forme de spécification peut garantirt que les numéros
de version soient une information utile pour la gestion des dépendances. En
donnant un nom et une définition claire aux idées ci-dessus, il devient facile
de communiquer vos intentions pour les utilisateurs de votre logiciel. Une fois
que ces intentions sont claires, souples (mais pas trop souples) les
spécifications de dépendances peuvent enfin se faire.

Un exemple simple montrera comment le versionnement sémantique peut faire de
l'enfer des dépendances une chose du passé. Considérons une bibliothèque appelée 
"CamionDePompier". Elle nécessite un composant Sémantiquement Versionné nommé
"Échelle". Au moment où CamionDePompier est créé, Échelle est à la version
3.1.0. Puisque CamionDePompier utilise des fonctionnalités de la version 3.1.0,
vous pouvez spécifier une dépendance avec Échelle comme supérieure ou égale à
3.1.0, mais inférieure à 4.0.0. Maintenant, quand la version 3.1.1 et 3.2.0
d'Échelle deviennent disponibles, vous pouvez les communiquer à votre système de
gestion de composants et savoir qu'ils seront compatibles avec les logiciels
existants dépendants.

En tant que développeur responsable, vous voudrez bien sûr vérifier que toute
mise à jour de composant fonctionne comme annoncée. Le monde réel étant ce qu'il
est, il n'y a rien que nous puissions faire, sinon d'être vigilant. Ce que vous
pouvez faire est de laisser le Versionnement Sémantique vous offrir une façon
saine de publier et mettre à niveau des composants, sans avoir à publier une
nouvelle version pour tous les composants dépendants, vous permettant ainsi
d'économiser du temps et des complications.

Si tout cela vous semble intéressant, tout ce que vous avez à faire pour
commencer à utiliser le Versionnement Sémantique est de déclarer que vous le
faites, puis suivre les règles. Ajoutez un lien vers ce site dans vos fichiers
README pour que les autres connaissent les règles et puissent en bénéficier.


FAQ
---

### Comment dois-je gérer les révisions dans la phase initiale de développement 0.y.z ?

La chose la plus simple à faire est de commencer votre version de développement
initial à 0.1.0 puis d'incrémenter la version mineure pour chaque version
ultérieure.

### Comment puis-je savoir quand publier la version 1.0.0 ?

Si votre logiciel est utilisé en production, il devrait probablement déjà être
en 1.0.0. Si vous avez une API stable dont les utilisateurs dépendent, vous
devriez être en 1.0.0. Si vous vous inquiétez beaucoup sur la
rétro-compatibilité, vous devriez probablement déjà être en 1.0.0.

### N'est-ce pas décourager le développement rapide et des itérations courtes ?

La version majeure zéro est faite pour le développement rapide. Si vous décidez
de changer l'API tous les jours, vous devez soit être encore en version 0.x.x ou
sur une branche de développement distincte de la prochaine version majeure.

### Si même le plus petit changement incompatible à l'API publique nécessite une montée de version majeure, ne vais-je pas me retrouver à la version 42.0.0 très rapidement ?

C'est une question de développement responsable et de prévoyance. Les
changements rétro-incompatibles ne doivent pas être introduits à la légère dans
un logiciel qui a beaucoup de code dépendant. Le coût qui doit être engagé pour
monter de version peut être important. Avoir besoin de monter de version majeure
pour publier des changements incompatibles signifie que vous réfléchirez à
l'impact de vos modifications et évaluerez le rapport coût/bénéfice.

### Documenter l'ensemble de l'API publique est trop de travail !

Il est de votre responsabilité en tant que développeur professionnel de bien
documenter tout logiciel qui est destiné à être utilisé par d'autres. Gérer la
complexité du logiciel est une partie très importante pour garder un projet
efficace, et c'est difficile à faire si personne ne sait comment utiliser votre
logiciel ou ne connait pas les bonnes méthodes à appeler. À long terme, le
versionnement sémantique et l'effort sur une API publique bien définie peut
faire fonctionner tout et tout le monde sans problème.

### Que dois-je faire si j'ai accidentellement publié un changement rétro-incompatible dans une version mineure ?

Dès que vous réalisez que vous avez cassé la spécification du versionnement
sémantique, réglez le problème et sortez une nouvelle version mineure qui
corrige le problème et restaure la rétro-compatibilité. Rappelez-vous, il est
inacceptable de modifier les versions publiées, même dans ce cas. Documentez
éventuellement la version en erreur et informez vos utilisateurs de ce probléme.

### Que dois-je faire si je mets à jour mes propres dépendances sans changer l'API publique ?

Cela peut être considéré comme compatible, dans la mesure où cela n'affecte pas
l'API publique. Un logiciel qui a les mêmes dépendances que votre composant
devrait avoir ses propres dépendances et l'auteur remarquera s'il y a un
conflit.
Déterminer si le changement est de niveau patch ou mineur dépend de la raison
pour laquelle vous avez actualisé vos dépendances : était-ce pour corriger un
bug ou introduire une nouvelle fonctionnalité ? On peut plutôt s'attendre à du
code supplémentaire pour ce dernier cas, auquel cas c'est évidemment une version
mineure.

### Que dois-je faire si je corrige un bug pour faire en sorte qu'il soit conforme avec la documentation associée (autrement dit, le code était désynchronisé de la documentation du composant) ?

A vous de décider. Si vous avez un large public qui va être considérablement
affecté en revenant à ce que l'API publique prévoyait, alors il peut être
préférable de publier une version majeure, même si le correctif est considéré
comme une version de patch. Rappelez-vous : le versionnement sémantique consiste
essentiellement à transmettre du sens dans la façon dont le numéro de version
change. Si ces changements sont importants pour vos utilisateurs, utilisez le
numéro de version pour les en informer.

### Comment dois-je traiter les fonctionnalités obsolètes ?

Les fonctionnalités obsolètes sont une part normale du développement de
logiciels et il est souvent nécessaire d'aller de l'avant. Lorsque vous
dépréciez une partie de votre API publique, vous devez faire deux choses :
(1) mettre à jour la documentation pour tenir les utilisateurs au courant du
changement,
(2) publier une nouvelle version mineure avec la dépréciation en place. Avant de
supprimer complètement la fonctionnalité dans une nouvelle version majeure, il
devrait y avoir au moins une version mineure qui contient la dépréciation de
sorte que les utilisateurs puissent effectuer la transition en douceur.


À propos
--------

La spécification du versionnement sémantique a été écrite par Tom
Preston-Werner, l'inventeur des Gravatars et cofondateur de GitHub.

Si vous souhaitez laisser des commentaires, veuillez ouvrir un sujet sur GitHub.


Licence
-------

Creative Commons - CC BY 3.0
http://creativecommons.org/licenses/by/3.0/