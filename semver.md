Versionamento Semântico 2.0.0
=============================

Sumário
-------

Dado um número de versão MAIOR.MENOR.PATCH, incremente a:

1. versão MAIOR quando você fizer alterações que tornem a API incompatível;
1. versão MENOR quando você adicionar funcionalidades de uma forma em que a compatibilidade seja mantida, e;
1. versão PATCH quando você fizer consertos de falhas que mantém a compatibilidade.

Etiquetas adicionais para pre-release e metadado de build estão disponíveis como extensões ao formato MAIOR.MENOR.PATCH.

Introdução
----------

No mundo da gestão de software existe um lugar pavoroso chamado "inferno das dependências". Quanto mais cresce o seu sistema e mais pacotes você integra nele, é mais provável que você se encontre, um dia, no poço do desespero. 

Em sistemas com muitas dependências, a liberação de novas versões de pacotes podem rápidamente se tornar um pesadelo. Se as especificações de dependência forem muito apertadas, você corre o risco de travar a versão (a incapacidade de atualizar um pacote sem ter de lançar novas versões de todos os pacotes que dependem dele). Se as dependências estão especificadas muito vagamente, você inevitávelmente será mordido pela promiscuidade entre versões (isso assumindo que a compatibilidade com outras versões fututas é razoável). Inferno das dependências é o lugar onde você está quando o bloqueio e/ou promiscuidade da versão vai impedi-lo, de forma fácil e segura, de mover o projeto adiante.

Como solução para este problema, eu proponho um simples conjunto de regras e requisitos que ditam como os números de versão são atribuídos e incrementados. Estas regras são baseadas, mas não necessáriamente limitadas as bem difundidas práticas comumente em uso tanto nos softwares de código aberto quanto nos de código fechado. Para este sistema funcionar, você primeiramente precisa declarar uma API pública. Isso pode consistir de documentação ou ser executada pelo próprio código. Independentemente disso, é importante que esta API ser clara e precisa. Uma vez que você identifique sua API pública, você comunica as trocas efetuadas com incrementos específicos no seu número de versão. Considere uma versão no formato X.Y.Z (maior.menor.patch). Consertos de erros que não afetam a API incrementam a versão patch, inclusões/modificações que não afetam a compatibilidade entre versões da API incrementam a versão menor e modificações que quebrem a compatibilidade entre versões da API incrementam o valor da versão maior.

Eu chamo este sistema de "Versionamento Semântico". Nele, os números de versão e a forma como eles mudam transmitem sentido sobre o código e sobre o que foi modificado de uma versão para outra do texto.

Especificação do Versionamento Semântico (SemVer)
-------------------------------------------------

As palavras chave "PRECISA", "NÃO PRECISA", "REQUERIDO", "DEVE", "NÃO DEVE", "DEVERIA", "NÃO DEVERIA", "RECOMENDADO", "PODE", e "OPCIONAL" neste documento devem ser interpretadas como descrito na [RFC 2119](http://tools.ietf.org/html/rfc2119).

1. Software usando o Versionamento Semântico PRECISA declarar uma API pública. Esta API pode ser declarada no próprio código fonte ou existir estritamente na documentação. Contudo ao ser feita, deve ser precisa e abrangente.

1. Um número de versão normal PRECISA ter o formato X.Y.Z, onde, X, Y e Z são números inteiros não negativos e NÃO PRECISA conter zeros à esquerda. X é a versão maior, Y a versão menor e Z é a versão de patch. Cada elemento PRECISA ser incrementado numericamente. Por exemplo: 1.9.0 -> 1.10.0 -> 1.11.0.

1. Uma vez publicado um pacote versionado, o conteúdo daquela versão NÃO PRECISA ser modificado. Quaisquer modificações PRECISAM ser liberadas sob uma nova versão.

1. A versão maior zero (0.y.z) é para o desenvolvimento inicial. Qualquer coisa pode mudar a qualquer momento. A API pública não deve ser considerada estável.

1. A versão 1.0.0 define a API pública. A forma como o número de versão é incrementado depois desta liberação depende da API pública e em como ela é modificada.

1. A versão de patch Z (x.y.Z | x > 0) PRECISA ser incrementada somente se reparos de falhas que não quebrem a compatibilidade entre versões foram introduzidos. Um reparo de falha é definido como uma alteração interna que corrige um comportamento indesejado.

1. Versão menor Y (x.Y.z | x > 0) PRECISA ser incrementada se novas funcionalidades, que não quebrem compatibilidade entre versões, foram introduzidas na API pública. PRECISA ser incrementada se qualquer funcionalidade da API pública for marcada como obsoleta. PODE ser incrementada se substanciais novas funcionalidades ou melhorias foram introduzidas no código privado. PODE incluir alterações de patch. A versão patch PRECISA ser reiniciada para 0 quando a versão menor for incrementada.

1. A versão maior X (X.y.z | X > 0) PRECISA ser incrementada se alguma modificação levou à incompatibilidade entre versões da API pública. PODE também incluir alterações de versão menor ou patch. Patch e a versão menor PRECISAM ser reiniciadas para 0 quando a versão maior é incrementada.

1. Uma versão pre-release PODE ser indicada anexando um hífen e uma série de identificadores separados por pontos imediatamente após o número de versão patch. Identificadores PRECISAM abranger somente alfanuméricos ASCII e hífen [0-9A-Za-z-]. Identificadores NÃO PRECISAM estar vazios. Identificadores numéricos NÃO PRECISA incluir zeros à esquerda. Versões de pre-release tem uma precedência menor que a verão normal associada. Uma versão pre-release indica que a versão é instável e pode não satisfazer os requisitos de compatibilidade desejados, como indicado pelas suas versões normais associadas. Exemplos: 1.0.0-alpha, 1.0.0-alpha.1, 1.0.0-0.3.7, 1.0.0-x.7.z.92.

1. Metadado de build PODE ser indicado ao anexar um sinal de mais e uma série de identificadores separados por pontos imediatamente após o número de versão patch ou o de pre-release. Identificadores PRECISAM abranger somente alfanuméricos ASCII e hífen [0-9A-Za-z-]. Identificadores NÃO PRECISAM estar vazios. Metadados de build PRECISAM ser ignorados quando determinando a precedência de versão. Assim, duas versões que diferem apenas nos metadados de construção, têm a mesma precedência. Exemplos: 1.0.0-alpha+001, 1.0.0+20130313144700, 1.0.0-beta+exp.sha.5114f85.

1. A precedência refere-se a como versões são comparadas umas com as outras quando solicitado. A precedência PRECISA ser calculada separando a versão em maior, menor, patch e pre-release, nesta ordem (metadado de build não figura na precedência). A precedência é dererminada pela primeira diferença quando comparando cada um destes identificadores, da esquerda para a direita, como segue: As versões maior, menor e patch são sempre comparadas numéricamente. Exemplo: 1.0.0 < 2.0.0 < 2.1.0 < 2.1.1. Quando maior, menor e patch são iguais, um pre-release tem sempre menor precedência do que uma versão normal. Exemplo: 1.0.0-alpha < 1.0.0. A precedência entre duas versões pre-release com os mesmos valores para as versões maior, menor e patch PRECISAM ser determinada comparando cada identificador separado por pontos, da esquerda para a direita, até encontrar uma diferença, como segue: identificadores consistindo somente de dígitos são comparados numéricamente e identificadores com letras ou hífens são comparados lexicamente usando a ordenação de caracteres ASCII. Identificadores numéricos sempre tem precedência inferior do que os identificadore não numéricos. Um grande conjunto de campos de pre-release tem uma precedência maior do que um conjunto menor, se todos os identificadores precedentes forem iguais. Exemplo: 1.0.0-alpha < 1.0.0-alpha.1 < 1.0.0-alpha.beta < 1.0.0-beta < 1.0.0-beta.2 < 1.0.0-beta.11 < 1.0.0-rc.1 < 1.0.0.

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
