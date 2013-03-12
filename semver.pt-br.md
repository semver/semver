Versionamento Semântico 2.0.0-rc.1
==================================

No mundo de gerenciamento de software existe algo terrível conhecido como
inferno das dependências ("dependency hell"). Quanto mais o sistema cresce, e
mais pacotes são integrados nele, mais provável é que um dia você se encontre
neste poço de desespero.

Em sistemas com muitas dependências, lançar novos pacotes de versões pode se
tornar rapidamente um pesadelo. Se as especificações das dependências são muito
amarradas você corre o risco de um bloqueio de versão (A falta de capacidade de
atualizar um pacote sem ter de liberar novas versões de cada pacote dependente).
Se as dependências são vagamente especificadas, você irá inevitavelmente ser
mordido pela 'promiscuidade da versão' (assumindo compatibilidade com futuras
versões mais do que é razoável). Inferno das dependências é onde você está
quando um bloqueio de versão e/ou promiscuidade de versão te impede de seguir
em frente com seu projeto de maneira fácil e segura.

Como uma solução para este problema proponho um conjunto simples de regras e
requisitos que ditam como os números das versões são atribuídos e incrementados.

Para que este sistema funcione, primeiro você precisa declarar uma API pública.
Isto pode consistir de documentação ou ser determinada pelo próprio código. De
qualquer maneira, é importante que esta API seja clara e precisa. Depois de
identificada a API pública, você comunica as mudanças com incrementos
específicos para o seu número de versão. Considere o formato de versão X.Y.Z
(Maior.Menor.Correção). Correção de falhas (Bug Fixes) que não afetam a API,
incrementa a versão de Correção, adições/alterações compatíveis com as versões
anteriores da API incrementa a versão Menor, e alterações incompatíveis com as
versões anteriores da API incrementa a versão Maior.

Eu chamo esse sistema de "Versionamento Semântico". Sob este esquema, os números
de versão e a forma como eles mudam, transmite o significado do código
subjacente e o que foi modificado de uma versão para a próxima.

Especificação de Versionamento Semântico (SemVer)
-------------------------------------------------

As palavras-chaves "DEVE", "NÃO DEVE", "OBRIGATÓRIO", "DEVERÁ", "NÃO DEVERÁ",
"DEVERIA", "NÃO DEVERIA", "RECOMENDADO", "PODE" e "OPCIONAL" no presente 
documento devem ser interpretados como descrito na [RFC 2119] 
(http://tools.ietf.org/html/rfc2119).

1. Software usando Versionamento Semântico DEVE declarar uma API pública. Esta 
API poderá ser declarada no próprio código ou existir estritamente na 
documentação, desde que seja precisa e compreensiva.

2. Um número de versão normal DEVE ter o formato de X.Y.Z, onde X, Y, e Z são
inteiros não negativos. X é a versão Maior, Y é a versão Menor, e Z é a versão
de Correção. Cada elemento DEVE aumentar numericamente por incrementos de um.
Por exemplo: 1.9.0 -> 1.10.0 -> 1.11.0.

3. Uma vez que um pacote de versionado foi lançado(released), o conteúdo desta
versão NÃO DEVE ser modificado. Qualquer modificação DEVE ser lançado como uma
nova versão.

4. No início do desenvolvimento, a versão Maior DEVE ser zero (0.y.z). Qualquer
coisa pode mudar a qualquer momento. A API pública não deve ser considerada
estável.

5. Versão 1.0.0 define a API como pública. A maneira como o número de versão é
incrementado após este lançamento é dependente da API pública e como ela muda.

6. Versão de Correção Z (x.y.Z | x > 0) DEVE ser incrementado apenas se mantiver
compatibilidade e introduzir correção de bugs. Uma correção de bug é definida
como uma mudança interna que corrige um comportamento incorreto.

7. Versão Menor Y (x.Y.z | x > 0) DEVE  ser incrementada se uma funcionalidade
nova e compatível for intruduzida na API pública. DEVE ser incrementada se
qualquer funcionalidade da API pública for definida como descontinuada. PODE ser
incrementada se uma nova funcionalidade ou melhoria substancial for introduzida
dentro do código privado. PODE incluir mudanças a nível de correção. A versão de
Correção deve ser redefinida para 0 quando a versão Menor for incrementada.

8. Versão Maior X (X.y.z | X > 0) DEVE ser incrementada se forem introduzidas
mudanças incompatíveis na API pública. PODE incluir alterações a nível de versão
Menor e de versão de Correção. Versão de Correção e Versão Menor devem ser 
redefinidas para 0 quando a versão Maior for incrementada.

9. Uma versão de pré-lançamento (pre-release) PODE ser identificada adicionando
um hífen (dash) e uma série de identificadores separados por ponto (dot)
imediatamente após a versão de Correção. o identificador DEVE ser composto
apenas por caracteres alfanumérios e hífen (dash)[0-9A-Za-z-]. Versão de
Pré-Lançamento (Pré-Release) tem  precedência inferior à versão normal a que
está associada. Exemplos: 1.0.0-alpha, 1.0.0-alpha.1, 1.0.0-0.3.7,
1.0.0-x.7.z.92.

10. Uma versão de Construção (build) PODE ser identificada por adicionar um
sinal de adição (+) e uma série de identificadores separados por ponto
imediatamente após a versão de Correção ou Pré-Lançamento (pre-release). 
Identificador DEVE ser composto apenas por caracteres alfanumérios e hífen 
[0-9A-Za-z-]. Versões de Construção têm precedência maior à versão normal a que 
está associada. Exemplos: 1.0.0+build.1, 1.3.7+build.11.e0f985a.

11. A precendência DEVE ser calculada separando identificadores de versão em 
Maior, Menor, Correção, Pré-lançamento e Construção, nesta ordem. Versões Maior,
Menor e Correção são sempre comparadas numericamente. A precedência de versões
de Pré-lançamento e Construção DEVE ser determinada comparando cada
identificador separado por ponto da seguinte forma: identificadores consistindo
apenas dígitos são comparados numericamente e identificadores com letras ou
hífen são comparados lexicalmente na ordem de classificação ASCII.
Identificadores numéricos sempre têm menor precedência do que os não numéricos.
Exemplo: 1.0.0-alpha < 1.0.0-alpha.1 < 1.0.0-beta.2 < 1.0.0-beta.11 < 1.0.0-rc.1
< 1.0.0-rc.1+build.1 < 1.0.0 < 1.0.0+0.3.7 < 1.3.7+build < 1.3.7+build.2.b8f12d7
< 1.3.7+build.11.e0f985a.

Por que usar Versionamento Semântico?
----------------------------
Esta não é uma ideia nova ou revolucionária. De fato, você provavelmente já faz
algo próximo a isso. O problema é que "próximo" não é bom o bastante. Sem a
aderência a algum tipo de especificação formal, os números de versão são
essencialmente inúteis para gerenciamento de dependências. Dando um nome e
definições claras às ideias acima, fica fácil comunicar suas intenções aos
usuários de seu software. Uma vez que estas intenções estão claras,
especificações de dependências flexíveis (mas não tão flexíveis) finalmente
podem ser feitas.

Um exemplo simples vai demonstrar como o Versionamento Semântico pode fazer do
inferno de dependência uma coisa do passado. Considere uma biblioteca chamada
"CaminhaoBombeiros". Ela requer um pacote versionado dinamicamente chamado
"Escada". Quando CaminhaoBombeiros foi criado, Escada estava na versão 3.1.0.
Como CaminhaoBombeiros utiliza algumas funcionalidades que foram inicialmente
introduzidas na versão 3.1.0, você pode especificar, com segurança, a
dependência da Escada como maior ou igual a 3.1.0 porém menor que 4.0.0. Agora,
quando Escada versão 3.1.1 e 3.2.0 estiverem disponíveis, você poderá lança-los
ao seu sistema de gerenciamento de pacote e saberá que eles serão compatíveis
com os softwares dependentes existentes.

Como um desenvolvedor responsável você irá, é claro, querer certificar-se que
qualquer atualização no pacote funcionará como anunciado. O mundo real é um
lugar bagunçado; não há nada que possamos fazer quanto a isso senão sermos
vigilantes. O que você pode fazer é deixar o Versionamento Semântico lhe
fornecer uma maneira sensata de lançar e atualizar pacotes sem precisar
atualizar para novas versões de pacotes dependentes, salvando-lhe tempo e
aborrecimento.

Se tudo isto soa desejável, tudo que você precisar fazer para começar a usar
Versionamento Semântico é declarar que você o esta usando e então, seguir as
regras. Adicione um link para este website no seu README para que outros saibam
as regras e possam beneficiar-se delas.

FAQ
---

### Como devo lidar com revisões na fase 0.y.z de desenvolvimento inicial?

A coisa mais simples a se fazer é começar sua versão de desenvolvimento inicial
em 0.1.0 e, então, incrementar a uma versão 'menor' em cada lançamento
subsequente.

### Como eu sei quando lançar a versão 1.0.0?

Se seu software está sendo usado em produção, ele já deve ser provavelmente
1.0.0. Se você possui uma API estável a qual usuários passaram a depender, deve
ser 1.0.0. Se você está se preocupando bastante com compatibilidade com versões
anteriores, já deve ser 1.0.0.

### Isto não desencoraja o desenvolvimento ágil e iteração rápida?

A versão Maior zero tem o foco exatamente no desenvolvimento rápido. Se você
está mudando a API todo dia, provavelmente você está na versão 0.y.z ou num
branch separado de desenvolvimento, trabalhando numa próxima versão Maior.

### Se mesmo a menor mudança incompatível com a API pública requer aumento da 
versão maior, não vou acabar na versão 42.0.0 muito rapidamente?

Esta é uma questão de desenvolvimento responsável e conhecimento antecipado.
Mudanças incompatíveis não devem ser levemente introduzidas para o software que
tem um monte de código dependente. O custo que deve ser incorrido para atualizar
pode ser significante. Tendo que aumentar a versão maior para lançar mudanças
incompatíveis, significa que você pensará no impacto das suas mudanças, e 
avaliará a relação de custo/benefício envolvida.

### Documentar toda a API pública dá muito trabalho!

É sua responsabilidade como desenvolvedor profissional documentar corretamente o
software que será usado por outros. Gerenciar a complexidade de software é uma
parte muito importante para manter o projeto eficiente, e isto é difícil de
fazer se ninguém sabe como usá-lo ou que métodos são seguros de chamar. A longo
prazo, Versionamento Semântico e a insistência em uma API pública bem definida
podem deixar tudo e todos funcionamente suavemente.

### O que eu faço se, acidentalmente, liberar uma mudança incompatível com
versões anteriores como uma versão menor (minor version)?

Assim que você perceber que quebrou a especificação de versionamento semântico,
conserte o problema e lance uma nova versão menor, que corrige o problema e
restaura a compatibilidade. Mesmo sob esta circunstância, é inaceitável 
modificar versões lançadas. Se for apropriado, documente a versão ofensiva e
informe seus usuários do problema de forma que eles fiquem cientes da versão em
questão.

### O que devo fazer se eu atualizar minhas próprias dependências sem modificar
a API pública?

Isso seria considerado compatível, uma vez que não afeta a API pública. Software
que depende explicitamente da mesmas dependências que seu pacote, deve ter sua
própria especificação de dependência e o autor notificará quaisquer conflitos.
Para determinar se a mudança é a nível de correção ou modificação de nível menor
dependente se você atualizou suas dependências a fim de corrigir um bug ou
introduzir nova funcionalidade. Eu normalmente esperaria código adicional para 
última instância, caso em que é obviamente um incremento no nível menor.

###  O que devo fazer se o erro que está sendo corrigido retorna o código para
estar em conformidade com a API pública (ou seja, o código estava incorretamente
fora de sincronia com a documentação da API pública)?

Use o bom senso. Se você tem um público enorme que será drasticamente impactado
pela mudança de comportamento de volta para o que a API pública pretendida, 
então pode ser melhor realizar um lançamento de uma versão maior, mesmo que a 
correção pudesse ser considerada estritamente uma versão de correção.Lembre-se, 
Versionamento Semântico trata de transmitir o conhecimento das mudanças 
ocorridas na versão. Se estas mudanças são importantes para seus usuários, 
utilize o número da versão para informá-los.

### Como devo lidar com descontinuação de funcionalidades?

Descontinuar funcionalidades é um processo comum no desenvolvimento de software e
muitas vezes é necessário para haver progresso. Quando você descontinua partes de
sua API pública, você deve fazer duas coisas: (1) atualizar sua documentação,
para que os usuários saibam das mudanças, (2) lançar uma versão Menor anunciando
a descontinuação. Antes de remover completamente a funcionalidade em uma versão 
Maior deve haver ao menos uma versão Menor que possui a descontinução anunciada, 
fazendo com que os usuários realizem uma transição tranquila para a nova API.


Sobre
-----

A Especificação da Semântica de Versionamento é autoria de [Tom
Preston-Werner](http://tom.preston-werner.com), criador do Gravatars e 
co-founder do GitHub.

A tradução deste documento para Português-Brasil foi iniciada de forma 
colaborativa pela [Wend Tecnologia] (https://github.com/wendtecnologia) através
de [Walker de Alencar Oliveira] (https://github.com/walkeralencar) e teve a 
participação de:
* [William G. Comnisky] (https://github.com/wcomnisky)
* [Rafael Sirotheau] (https://github.com/rafasirotheau)
* [Arthur Almeida] (https://github.com/arthuralmeidap)
* [Alberto Guimarães Viana] (https://github.com/albertogviana)
* Rafael Lúcio
* Josiel Rocha
* Alessandro Leite
* Vinícius Assef

Toda colaboração na tradução pode ser acompanhada no link:
http://okfnpad.org/ep/pad/view/Fh9hjBPVu9/latest

Caso queira deixar sua opinião, por favor [abra uma issue no GitHub]
(https://github.com/walkeralencar/semver/issues)

Licença
-------

Creative Commons - CC BY 3.0
http://creativecommons.org/licenses/by/3.0/
