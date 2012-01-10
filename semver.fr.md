Le Versionnement Sémantique 2.0.0-rc.1
======================================

Dans le monde de la gestion de logiciels, il existe un endroit terrifiant appelé
"l'enfer des dépendances". Plus votre système se développe et plus vous intégrez
de composants dans votre logiciel, plus vous êtes susceptible de vous trouver,
un jour, dans cette ab�me de désespoir.

Dans les systèmes avec de nombreuses dépendances, publier une nouvelle version
d'un composant peut vite devenir un cauchemar. Si les règles de dépendance sont
trop strictes, vous risquez de verrouiller les versions (incapacité de mettre à
jour un composant sans avoir à publier une nouvelle version de chaque composant
qui en dépend). Si les règles de dépendances sont trop lâches, vous allez
inévitablement être rattrapés par la promiscuité de version (supposer une
compatibilité avec plus de futures versions que raisonnable). L'enfer des
dépendances est l'endroit où vous vous trouvez lorsque les verrous de versions
et/ou la promiscuité de versions vous empêchent d'avancer sans risque dans votre
projet.

Comme solution � ce probl�me, je propose un ensemble de r�gles et exigences
simples qui dictent la fa�on dont les num�ros de version sont attribu�s et
incr�ment�s. Pour que ce syst�me fonctionne, vous devez d'abord d�clarer une API
publique. Il peut s'agir d�un document ou de r�gles appliqu�es par le code
lui-m�me. Quoiqu�il en soit, il est important que cette API soit claire et
pr�cise. Une fois qu�elle est pr�te, vous lui communiquez les modifications avec
les incr�mentations sp�cifiques � votre num�ro de version. Consid�rons le format
de version "X.Y.Z" (Majeur.Mineur.Patch). Les correctifs n'affectant pas l�API
incr�mentent la version de patch, des ajouts ou modifications r�tro-compatibles
incr�mentent la version mineure et les modifications r�tro-incompatibles
incr�mentent la version majeure.

J'appelle ce syst�me "Versionnement S�mantique". Avec ce syst�me, les num�ros
de version et la fa�on dont ils changent donnent du sens au code sous-jacent et
� ce qui a �t� modifi� d'une version � l'autre.


Sp�cifications du Versionnement S�mantique (SemVer)
---------------------------------------------------

Les mots cl�s "DOIT", "NE DOIT PAS", "REQUIS", "DEVRAIT", "NE DEVRAIT PAS",
"RECOMMAND�", "PEUT", et "FACULTATIF" dans ce document doivent �tre interpr�t�s
comme d�crit dans la RFC 2119.

1. Tout logiciel utilisant le Versionnement S�mantique DOIT d�clarer une API
publique. Cette API peut �tre d�clar�e dans le code lui-m�me ou dans un
document. Dans tous les cas, elle doit �tre pr�cise et claire.

1. Un num�ro de version standard DOIT prendre la forme X.Y.Z o� X, Y et Z sont
des entiers non n�gatifs. X est la version majeure, Y est la version mineure, et
Z est la version de patch. Chaque �l�ment DOIT augmenter num�riquement par
incr�ments d'une unit�. Par exemple : 1.9.0 -> 1.10.0 -> 1.11.0.

1. Quand un num�ro de version majeur est incr�ment�, la version mineure et la
version patch DOIVENT �tre remises � z�ro. Quand un num�ro de version mineur est
incr�ment�, la version patch DOIT �tre remise � z�ro. Par exemple:
1.1.3 -> 2.0.0 et 2.1.7 -> 2.2.0.

1. Une fois qu�une version d�un composant est publi�e, le contenu de cette
version NE DOIT PAS �tre modifi�. Toute modification doit �tre publi�e comme une
nouvelle version.

1. La version majeure z�ro (0.y.z) sert au d�veloppement initial. Tout peut
changer � tout moment. L'API publique ne doit pas �tre consid�r�e comme stable.

1. La version 1.0.0 d�finit l'API publique. La fa�on dont le num�ro de version
est incr�ment� apr�s la publication est d�pendante de cette API publique.

1. La version de patch Z (x.y.Z | x > 0) DOIT �tre incr�ment�e si des
corrections d�anomalies r�tro-compatibles sont effectu�es. Une correction
d�anomalie est d�finie comme un changement interne qui corrige un comportement
incorrect.

1. La version mineure Y (x.Y.z | x > 0) DOIT �tre incr�ment�e si une nouvelle
fonctionnalit�, r�tro-compatible est introduite � l'API publique. Elle DOIT �tre
incr�ment�e si une fonctionnalit� de l�API publique est marqu�e comme obsol�te.
Elle PEUT �tre incr�ment�e si une nouvelle fonctionnalit� ou am�lioration est
introduite dans le code priv�. Elle PEUT inclure des changements de niveau de
patch. La version de patch DOIT �tre remise � 0 lorsque la version mineure est
incr�ment�e.

1. La version majeure X (X.y.z | X > 0) DOIT �tre incr�ment�e si des changements
r�tro-incompatibles sont introduits � l'API publique. Elle PEUT inclure des
changements mineurs et de patch. Les num�ros de version de patch et mineurs
DOIVENT �tre remis � 0 lorsque la version majeure est incr�ment�e.

1. Une version de pr�publication PEUT �tre not�e par l'ajout d'un tiret et une
s�rie d�identifiants s�par�s par des points suivant imm�diatement la version de
patch. Les identifiants DOIVENT �tre compos�s uniquement de caract�res
alphanum�riques ASCII et de tirets [0-9A-Za-z-]. Des versions de pr�publication
sont utilisables, mais ont une priorit� moindre par rapport � la version normale
associ�e. Exemples : 1.0.0-alpha, 1.0.0-alpha.1, 1.0.0-0.3.7, 1.0.0-x.7.z.92.

1. Une version de construction PEUT �tre repr�sent�e par l'ajout d'un signe
"plus" et d�une s�rie d�identifiants s�par�s par des points suivant
imm�diatement la version de patch ou de pr�publication. Les identifiants DOIVENT
�tre compos�s uniquement de caract�res alphanum�riques ASCII et de tirets
[0-9A-Za-z-]. Les versions de construction sont utilisables et ont une priorit�
plus �lev�e que la version normale associ�e. Exemples: 1.0.0+build.1,
1.3.7+build.11.e0f985a.

1. La priorit� DOIT �tre calcul�e en s�parant les num�ros de version en
identifiants majeur, mineur, patch, pr�publication et de construction dans cet
ordre. Les num�ros de version majeur, mineur, et de patch sont toujours compar�s
num�riquement. Pour les versions de pr�publication et de construction, la
priorit� DOIT �tre d�termin�e en comparant chaque identifiant s�par� par un
point comme suit : les identifiants compos�s de chiffres seulement sont compar�s
num�riquement et les identifiants compos�s de lettres ou de tirets sont compar�s
dans l�ordre de tri ASCII. Les identifiants num�riques ont toujours priorit�
inf�rieure par rapport aux identifiants non num�riques. Exemple : 1.0.0-alpha <
1.0.0-alpha.1 < 1.0.0-beta.2 < 1.0.0-beta.11 < 1.0.0-RC.1 < 1.0.0-RC.1+build.1 <
1.0.0 < 1.0.0+0.3.7 < 1.3.7+build < 1.3.7+build.2.b8f12d7 <
1.3.7+build.11.e0f985a.


Pourquoi utiliser le Versionnement S�mantique ?
-----------------------------------------------

Ce n'est pas une id�e nouvelle ni r�volutionnaire. En fait, vous utilisez
probablement d�j� un syst�me proche de celui-ci. Le probl�me est que "proche"
n'est pas suffisant. Sans le respect d'une certaine forme de sp�cification, les
num�ros de version sont essentiellement inutiles pour la gestion des
d�pendances. En donnant un nom et une d�finition claire aux id�es ci-dessus, il
devient facile de communiquer vos intentions pour les utilisateurs de votre
logiciel. Une fois que ces intentions sont claires, souples (mais pas trop
souple) les sp�cifications de d�pendances peuvent enfin se faire.

Un exemple simple montrera comment le Versionnement S�mantique peut faire de
l'enfer des d�pendances une chose du pass�. Consid�rons une librairie appel�e 
"CamionDePompier". Elle n�cessite un composant S�mantiquement Versionn� nomm�
"�chelle". Au moment o� CamionDePompier est cr��, �chelle est � la version
3.1.0. Puisque CamionDePompier utilise des fonctionnalit�s de la version 3.1.0,
vous pouvez sp�cifier une d�pendance avec �chelle comme sup�rieure ou �gale �
3.1.0, mais inf�rieure � 4.0.0. Maintenant, quand la version 3.1.1 et 3.2.0
d��chelle deviennent disponibles, vous pouvez les communiquer � votre syst�me de
gestion de composants et savoir qu'ils seront compatibles avec les logiciels
existants d�pendants.

En tant que d�veloppeur responsable, bien s�r, vous voudrez v�rifier que toute
mise � jour de composant fonctionne comme annonc�. Le monde r�el �tant ce qu�il
est, il n'y a rien que nous puissions faire sinon �tre vigilant. Ce que vous
pouvez faire est de laisser le Versionnement S�mantique vous offrir une fa�on
saine de publier et mettre � niveau des composants, sans avoir � publier une
nouvelle version pour tous les composants d�pendants, vous permettant ainsi
d'�conomiser du temps et des complications.

Si tout cela vous semble int�ressant, tout ce que vous avez � faire pour
commencer � utiliser le Versionnement S�mantique est de d�clarer que vous le
faites, puis suivre les r�gles. Ajoutez un lien vers ce site dans vos fichiers
README pour que les autres connaissent les r�gles et puissent en b�n�ficier.


FAQ
---

### Comment dois-je g�rer les r�visions dans la phase initiale de d�veloppement
0.y.z ?

La chose la plus simple � faire est de commencer votre version de d�veloppement
initial � 0.1.0 puis incr�menter la version mineure pour chaque version
ult�rieure.

### Comment puis-je savoir quand publier la version 1.0.0 ?

Si votre logiciel est utilis� en production, il devrait probablement d�j� �tre
en 1.0.0. Si vous avez une API stable dont les utilisateurs d�pendent, vous devriez
�tre en 1.0.0. Si vous vous inqui�tez beaucoup sur la r�tro-compatibilit�,
vous devriez probablement d�j� �tre en 1.0.0.

### N'est-ce pas d�courager le d�veloppement rapide et des it�rations courtes ?

La version majeure z�ro est faite pour le d�veloppement rapide. Si vous d�cidez
de changer l'API tous les jours, vous devez soit �tre encore en version 0.x.x ou
sur une branche de d�veloppement distincte de la prochaine version majeure.

### Si m�me le plus petit changement incompatible � l'API publique n�cessite une
mont�e de version majeure, ne vais-je pas me retrouver � la version 42.0.0 tr�s
rapidement ?

C'est une question de d�veloppement responsable et de pr�voyance. Les
changements r�tro-incompatibles ne doivent pas �tre introduits � la l�g�re dans
un logiciel qui a beaucoup de code d�pendant. Le co�t qui doit �tre engag� pour
monter de version peut �tre important. Avoir besoin de monter de version majeure
pour publier des changements incompatibles signifie que vous r�fl�chirez �
l'impact de vos modifications et �valuerez le rapport co�t/b�n�fice.

### Documenter l'ensemble de l�API publique est trop de travail !

Il est de votre responsabilit� en tant que d�veloppeur professionnel de bien
documenter tout logiciel qui est destin� � �tre utilis� par d'autres. G�rer la
complexit� du logiciel est une partie tr�s importante pour garder un projet
efficace, et c'est difficile � faire si personne ne sait comment utiliser votre
logiciel ou ne connait pas les bonnes m�thodes � appeler. � long terme, le
Versionnement S�mantique et l�effort sur une API publique bien d�finie peut
faire fonctionner tout et tout le monde sans probl�me.

### Que dois-je faire si j'ai accidentellement publi� un changement
r�tro-incompatible dans une version mineure ?

D�s que vous r�alisez que vous avez cass� la sp�cification du Versionnement
S�mantique, r�glez le probl�me et sortez une nouvelle version mineure qui
corrige le probl�me et restaure la r�tro-compatibilit�. Rappelez-vous, il est
inacceptable de modifier les versions publi�es, m�me dans ce cas. Documentez
�ventuellement la version en erreur et informez vos utilisateurs de ce probl�me.

### Que dois-je faire si je mets � jour mes propres d�pendances sans changer
l'API publique?

Cela peut �tre consid�r� comme compatible, dans la mesure o� cela n'affecte pas
l'API publique. Un logiciel qui a les m�mes d�pendances que votre composant
devrait avoir ses propres d�pendances et l'auteur remarquera s�il y a un
conflit.
D�terminer si le changement est de niveau patch ou mineur d�pend de la raison
pour laquelle vous avez actualis� vos d�pendances : �tait-ce pour corriger un
bug ou introduire une nouvelle fonctionnalit� ? On peut plut�t s�attendre � du
code suppl�mentaire pour ce dernier cas, auquel cas c'est �videmment une version
mineure.

### Que dois-je faire si je corrige un bug pour faire en sorte qu�il soit
conforme avec la documentation associ�e (autrement dit, le code �tait
d�synchronis� de la documentation du composant) ?

A vous de d�cider. Si vous avez un large public qui va �tre consid�rablement
affect� en revenant � ce que l'API publique pr�voyait, alors il peut �tre
pr�f�rable de publier une version majeure, m�me si le correctif est consid�r�
comme une version de patch. Rappelez-vous : le Versionnement S�mantique consiste
essentiellement � transmettre du sens dans la fa�on dont le num�ro de version
change. Si ces changements sont importants pour vos utilisateurs, utilisez le
num�ro de version pour les informer.

### Comment dois-je traiter les fonctionnalit�s obsol�tes ?

Les fonctionnalit�s obsol�tes sont une part normale du d�veloppement de
logiciels et il est souvent n�cessaire d�aller de l'avant. Lorsque vous
d�pr�ciez une partie de votre API publique, vous devez faire deux choses :
(1) mettre � jour la documentation pour tenir les utilisateurs au courant du
changement,
(2) publier une nouvelle version mineure avec la d�pr�ciation en place. Avant de
supprimer compl�tement la fonctionnalit� dans une nouvelle version majeure, il
devrait y avoir au moins une version mineure qui contient la d�pr�ciation de
sorte que les utilisateurs puissent faire la transition en douceur.


� propos
--------

La sp�cification du Versionnement S�mantique a �t� �crite par Tom
Preston-Werner, l'inventeur des Gravatars et cofondateur de GitHub.

Si vous souhaitez laisser des commentaires, veuillez ouvrir un sujet sur GitHub.


Licence
-------

Creative Commons - CC BY 3.0
http://creativecommons.org/licenses/by/3.0/
