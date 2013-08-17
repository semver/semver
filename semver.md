Semantic Versioning 2.0.0
==============================

Summary
-------

Given a version number MAJOR.MINOR.PATCH, increment the:

1. MAJOR version when you make incompatible API changes,
1. MINOR version when you add functionality in a backwards-compatible
   manner, and
1. PATCH version when you make backwards-compatible bug fixes.

Additional labels for pre-release and build metadata are available as extensions
to the MAJOR.MINOR.PATCH format.

Introduction
------------

In the world of software management there exists a dread place called
"dependency hell." The bigger your system grows and the more packages you
integrate into your software, the more likely you are to find yourself, one
day, in this pit of despair.

In systems with many dependencies, releasing new package versions can quickly
become a nightmare. If the dependency specifications are too tight, you are in
danger of version lock (the inability to upgrade a package without having to
release new versions of every dependent package). If dependencies are
specified too loosely, you will inevitably be bitten by version promiscuity
(assuming compatibility with more future versions than is reasonable).
Dependency hell is where you are when version lock and/or version promiscuity
prevent you from easily and safely moving your project forward.

As a solution to this problem, I propose a simple set of rules and
requirements that dictate how version numbers are assigned and incremented.
These rules are based on but not necessarily limited to pre-existing
widespread common practices in use in both closed and open-source software.
For this system to work, you first need to declare a public API. This may
consist of documentation or be enforced by the code itself. Regardless, it is
important that this API be clear and precise. Once you identify your public
API, you communicate changes to it with specific increments to your version
number. Consider a version format of X.Y.Z (Major.Minor.Patch). Bug fixes not
affecting the API increment the patch version, backwards compatible API
additions/changes increment the minor version, and backwards incompatible API
changes increment the major version.

I call this system "Semantic Versioning." Under this scheme, version numbers
and the way they change convey meaning about the underlying code and what has
been modified from one version to the next.


Semantic Versioning Specification (SemVer)
------------------------------------------

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be
interpreted as described in [RFC 2119](http://tools.ietf.org/html/rfc2119).

1. Software using Semantic Versioning MUST declare a public API. This API
could be declared in the code itself or exist strictly in documentation.
However it is done, it should be precise and comprehensive.

1. A normal version number MUST take the form X.Y.Z where X, Y, and Z are
non-negative integers, and MUST NOT contain leading zeroes. X is the
major version, Y is the minor version, and Z is the patch version.
Each element MUST increase numerically. For instance: 1.9.0 -> 1.10.0 -> 1.11.0.

1. Once a versioned package has been released, the contents of that version
MUST NOT be modified. Any modifications MUST be released as a new version.

1. Major version zero (0.y.z) is for initial development. Anything may change
at any time. The public API should not be considered stable.

1. Version 1.0.0 defines the public API. The way in which the version number
is incremented after this release is dependent on this public API and how it
changes.

1. Patch version Z (x.y.Z | x > 0) MUST be incremented if only backwards
compatible bug fixes are introduced. A bug fix is defined as an internal
change that fixes incorrect behavior.

1. Minor version Y (x.Y.z | x > 0) MUST be incremented if new, backwards
compatible functionality is introduced to the public API. It MUST be
incremented if any public API functionality is marked as deprecated. It MAY be
incremented if substantial new functionality or improvements are introduced
within the private code. It MAY include patch level changes. Patch version
MUST be reset to 0 when minor version is incremented.

1. Major version X (X.y.z | X > 0) MUST be incremented if any backwards
incompatible changes are introduced to the public API. It MAY also include minor
and patch level changes. Patch and minor version MUST be reset to 0 when major
version is incremented.

1. A pre-release version MAY be denoted by appending a hyphen and a
series of dot separated identifiers immediately following the patch
version. Identifiers MUST comprise only ASCII alphanumerics and hyphen
[0-9A-Za-z-]. Identifiers MUST NOT be empty. Numeric identifiers MUST
NOT include leading zeroes. Pre-release versions have a lower
precedence than the associated normal version. A pre-release version
indicates that the version is unstable and might not satisfy the
intended compatibility requirements as denoted by its associated
normal version. Examples: 1.0.0-alpha, 1.0.0-alpha.1, 1.0.0-0.3.7,
1.0.0-x.7.z.92.

1. Build metadata MAY be denoted by appending a plus sign and a series of dot
separated identifiers immediately following the patch or pre-release version.
Identifiers MUST comprise only ASCII alphanumerics and hyphen [0-9A-Za-z-].
Identifiers MUST NOT be empty. Build metadata MUST be ignored when determining
version precedence. Thus two versions that differ only in the build metadata,
have the same precedence. Examples: 1.0.0-alpha+001, 1.0.0+20130313144700,
1.0.0-beta+exp.sha.5114f85.

1. Precedence refers to how versions are compared to each other when ordered.
Precedence MUST be calculated by separating the version into major, minor, patch
and pre-release identifiers in that order (Build metadata does not figure
into precedence). Precedence is determined by the first difference when
comparing each of these identifiers from left to right as follows: Major, minor,
and patch versions are always compared numerically. Example: 1.0.0 < 2.0.0 <
2.1.0 < 2.1.1. When major, minor, and patch are equal, a pre-release version has
lower precedence than a normal version. Example: 1.0.0-alpha < 1.0.0. Precedence
for two pre-release versions with the same major, minor, and patch version MUST
be determined by comparing each dot separated identifier from left to right
until a difference is found as follows: identifiers consisting of only digits
are compared numerically and identifiers with letters or hyphens are compared
lexically in ASCII sort order. Numeric identifiers always have lower precedence
than non-numeric identifiers. A larger set of pre-release fields has a higher
precedence than a smaller set, if all of the preceding identifiers are equal.
Example: 1.0.0-alpha < 1.0.0-alpha.1 < 1.0.0-alpha.beta < 1.0.0-beta <
1.0.0-beta.2 < 1.0.0-beta.11 < 1.0.0-rc.1 < 1.0.0.

Backus–Naur Form Grammar para versões SemVer válidas
----------------------------------------------------

    <semver válido> ::= <versão core>
                     | <versão core> "-" <pre-release>
                     | <versão core> "+" <build>
                     | <versão core> "-" <pre-release> "+" <build>

    <versão core> ::= <maior> "." <menor> "." <patch>

    <maior> ::= <identificador numérico>

    <menor> ::= <identificador numérico>

    <patch> ::= <identificador numérico>

    <pre-release> ::= <identificadores pre-release separados-por-ponto>

    <identificadores pre-release separados-por-ponto> ::= <pre-release identifier>
                                              | <pre-release identifier> "." <identificadores pre-release separados-por-ponto>

    <build> ::= <identificadores build separados-por-ponto>

    <identificadores build separados-por-ponto> ::= <identificador build>
                                        | <identificador build> "." <identificadores build separados-por-ponto>

    <pre-release identifier> ::= <identificadores alfanuméricos>
                               | <numeric identifier>

    <identificador build> ::= <identificadores alfanuméricos>
                         | <dígitos>

    <identificadores alfanuméricos> ::= <não-dígitos>
                                | <não-dígitos> <identificador caracteres>
                                | <identificador caracteres> <não-dígitos>
                                | <identificador caracteres> <não-dígitos> <identificador caracteres>

    <identificador numérico> ::= "0"
                           | <dígitos positivos>
                           | <dígitos positivos> <dígitos>

    <identificador caracteres> ::= <identificador caracter>
                              | <identificador caracter> <identificador caracteres>

    <identificador caracter> ::= <dígito>
                             | <não-dígitos>

    <não-dígitos> ::= <letras>
                  | "-"

    <dígitos> ::= <dígito>
               | <dígito> <dígitos>

    <dígito> ::= "0"
              | <dígitos positivos>

    <dígitos positivos> ::= "1" | "2" | "3" | "4" | "5" | "6" | "7" | "8" | "9"

    <letras> ::= "A" | "B" | "C" | "D" | "E" | "F" | "G" | "H" | "I" | "J"
               | "K" | "L" | "M" | "N" | "O" | "P" | "Q" | "R" | "S" | "T"
               | "U" | "V" | "W" | "X" | "Y" | "Z" | "a" | "b" | "c" | "d"
               | "e" | "f" | "g" | "h" | "i" | "j" | "k" | "l" | "m" | "n"
               | "o" | "p" | "q" | "r" | "s" | "t" | "u" | "v" | "w" | "x"
               | "y" | "z"

Porque usar o Versionamento Semântico?
----------------------------

Esta não é uma idéia nova ou revolucionária. Na verdade, você provavelmente já faz algo mais ou menos assim. O problema é que "mais ou menos" não é o suficiente. Sem observância a algum tipo formal de especificação, os números de versão são essencialmente inúteis para a gestão de dependências. Ao dar um nome e uma definição clara para as idéias acima, fica mais fácil comunicar as suas intenções aos usuários do seu software. Uma vez que estas intenções são claras, pode-se fazer especificações de dependencias flexíveis (mas não muito flexíveis).

Um simples exemplo demonstrará como o Versionamento Semântico pode transformar o inferno das dependências algo do passado. Considere uma biblioteca chamada "Firetruck". Ela requer um pacote semânticamente versionado chamado "Ladder". No momento em que Firetruck está sendo criado, Ladder está na versão 3.1.0. Já que Firetruck usa algumas funcionalidades que foram introduzidas na versão 3.1.0, você pode seguramente especificar a dependência de Ladder em uma versão sendo maior ou igual a 3.1.0 mas menor que 4.0.0. Agora, quando Ladder versão 3.1.1 e 3.2.0 estiverem disponíveis, você pode utilizá-las no ser sistema de gestão de pacotes sabendo que elas serão compatíveis com o seu software.

Como um desenvolvedor responsável você irá, claro, querer verificar que qualquer atualização de pacotes funciona como anunciado. O mundo real é bem bagunçado e não podemos fazer nada além de estarmos sempre vigilantes e atentos. O que você pode fazer é deixar o Versionamento Semântico prover como uma forma sã de liberar atualizações de pacotes sem ter de lançar novas versões de pacotes dependentes, poupando tempo e aborrecimentos.

Se tudo isso soa desejável, o que você tem de fazer é começar a usar o Versionamento Semântico e anunciar para o seu usuário, e então, seguir as regras. No seu arquivo LEIAME aponte para este site para que outros saibam destas regras e possam também se beneficiar delas.

FAQ
---

### Como que eu devo lidar com revisões 0.y.z na fase inicial de desenvolvimento?

A forma mais simples a fazer é iniciar seu desenvolvimento na versão 0.1.0 e ir incrementando o número da versão menor a cada nova liberação.

### Como saber quando liberar a versão 1.0.0?

Se o seu software já está sendo usado em produção, então provavelmente ele deveria ser 1.0.0. Se você tem uma API estável da qual usuários dependem, você deveria ser 1.0.0. Se você está muito preocupado com quebras de compatibilidade, você provavelmente deveria ser 1.0.0.

### Isto não desencoraja o desenvolvimento ágil e iterações rápidas?

A verão maior em zero é estar falando sobre desenvolvimento ágil. Se você está trocando a API todo o dia, então você precisa ou estar na versão 0.y.z ou em um outro branch de desenvolvimento, trabalhando na próxima versão maior.

### Se as menores alterações que quebram a compatibilidade entre versões da API pública requerem o lançamento de uma versão maior, eu não vou acabar chegando na verão 42.0.0 muito rapidamente?

Esta é uma questão de desenvolvimento responsável e previsão. Alterações que gerem incompatibilidade entre versões não devem ser introduzidas aos poucos em um software que tem muitos consumidores, afinal, o custo de fazer um upgrade pode ser significativo. Ser obrigado a liberar versões maiores para as alterações que geram quebras de compatibilidade significa que você terá de pensar nos impactos gerados pelas suas modificações e avaliar o custo/benefício envolvido.

### Documentar toda a API pública é muito trabalho!

É sua responsabilidade como um desenvolvedor profissional documentar corretamente o software que se destina a ser utilizado por outras pessoas. Gerir a complexidade do software é uma parte muito importante para manter um projeto eficiente, e isso é difícil de fazer se ninguém sabe como usar o software, ou quais métodos são seguros para chamar. No longo prazo, o versionamento semântico, e a insistência em tem uma API pública bem definida pode manter todos e tudo funcionando perfeitamente.

### O que eu faço se eu acidentalmente liberar uma mudança incompatível como uma versão menor?

Assim que você perceber que você quebrou a especificação de versão semântica, conserte o problema e lançe uma nova versão menor para que a correção restaure a compatibilidade com versões anteriores. Mesmo nesta circunstância, é inaceitável modificar releases já versionados. Se for o caso,
documente a versão modificada e informe os seus usuários sobre o problema para que eles fiquem cientes da versão modificada.

### O que devo fazer se eu atualizar minhas próprias dependências, sem alterar a API pública?

Isso seria considerado compatível, uma vez que não afeta a API pública. Software que depende explicitamente nas mesmas dependências que o seu pacote deve ter suas próprias especificações de dependência e o autor vai notar quaisquer conflitos. Determinar se a mudança é um nível de patch ou de menor nível modificação depende se você atualizou suas dependências a fim de corrigir um bug, ou introduzir novas funcionalidades. Eu costumo esperar código adicional em última instância, no caso em que é, obviamente, um incremento do nível secundário.

### E se eu inadvertidamente alterei a API pública de uma forma que é incompatível com a forma como o número de versão foi trocado (ex. a alteração quebra a compatibilidade entre as versões, mas está numerada como se fosse um patch)

Use de bom senso. Se você tem uma grande audiência que será drasticamente impactada pela troca no comportamento da API pública, então o melhor é liberá-la como uma versão maior, mesmo que a alteração possa ser considerada somente como um patch. Lembre-se, versionamento semântico é transmitir significado pela forma como o número de versão muda. Se as modificações são importantes para os seus usuários, use o número da versão para informá-los.

### Como lidar com a descontinuação de funcionalidade?

Descontinuar uma funcionalidade existente é algo normal no desenvolvimento de
software e geralmente necessário para que se possa progredir. Quando você
descontinuar parte da sua API pública, você precisa fazer duas coisas:
(1) atualizar a sua documentação para que seus usuários possam saber da
alteração, (2) lançar uma versão menor já com o aviso de descontinuação,
antes de você, em um release maior, remover completamente a funcionalidade
descontinuada, permitindo que seus usuários façam tranquilamente a transição
para a nova API.

### SemVer tem um limite de tamanho para a string de versão?

Não, mas use de bom senso. Por exemplo, uma string de versão de 255
caracteres provavelmente é um exagero, bem ainda, alguns sistemas podem
impor seus próprios limites no tamanho da string de versão.

Sobre
-----

A especificação do Versionamento Semântico é de autoria de [Tom
Preston-Werner](http://tom.preston-werner.com), criador do Gravatars
e cofundador do GitHub.

Se você quiser dar feedback, por favor [abra um issue no
GitHub](https://github.com/mojombo/semver/issues).


Licença
-------

Creative Commons - CC BY 3.0
http://creativecommons.org/licenses/by/3.0/
