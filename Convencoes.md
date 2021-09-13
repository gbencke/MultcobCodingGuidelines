# Codificação

## Convenções de Codigo

O Sistema Multcob, como é desenvolvido por várias pessoas, é um codigo que precisa ser rapidamente entendido por qualquer pessoa, de forma rapida e sem ambiguidade...

Quando mergeando versões, analisando o código que será usado por outro colega, é importante observar as seguintes convenções / boas práticas:

* Usar PascalCase em nomes de variaveis / metodos / classes
* Sempre observar o padráo de prefixação sendo usado para o código especifico sendo usado, como por exemplo:
   * Interfaces, começam com a letra I
   * Variáveis privadas começam com _
   * Classes representando entidades começam com CBO
   * Classes que são repositórios de entidades, começam com CPG
   * Janelas de aplicativos começam com frm
   * Entre vários outros... 
* Em nomes de branches de código sempre usar snake_case, pois é a forma que menos dá problema quando em integração com várias ferramentas de construção e gestão de código.


* Usar português para nomes de classes, membros e variaveis 

## Boas Práticas de Codificação

Num software sendo desenvolvido a mais ou menos 15 anos, já se desenvolveu um sistema de boas práticas no sistema, que são regras informais, e que são seguidas informalmente pelos desenvolvedores. 

Entre eles estão:

* Utilização de processos-filhos chamado workers para operações longas e complexas que säo de natureza diferente do processo pai, e/ou de arquitetura diferente, por exemplo:
    * **MultcobADM.exe** chama o **MultcobWorker.exe** para realizar a importação de dados, porque não do escopo do MultcobADM saber da lógica de importação de dados no sistema
    * **API de Acordos** chama o **MultcobWorker.exe** porque a API de Acordos é feita em python e a nova versão em .NET 5, de forma que a API apenas se preocupa com a gestáo de requisições e respostas e não com as operações em si.
    * **MultcobCli.exe** e **ZancClientEmulator.exe** o MultcobCli apenas tem informação sobre o cliente a nível de CRM, ele deixa toda a gestão da ligação telefonica para o ZancClientEmulator e troca informações com o MultcobCli via um canal local TCP/IP
* Evitar ao máximo o uso de pacotes .NET externos e de terceiros, e que não venham na instalação básica do .NET Framework. Acreditamos que a adição de pacotes de terceiros aumentam em muito o risco de problemas inesperados no código, dessa forma, *procuramos desenvolver o nosso código usando oque vem com o .NET Framework, apesar de "em teoria" ser mais trabalho*. **Exceções devem ser analisadas caso a caso.**
* A maior parte das operações de negócio no sistema são comuns a vários contratantes, porém, sua lógica interna pode ser radicalmente diferente. Por exemplo: Calculo de Divida ativa existem em todos os contratantes, mas, na PORTOCRED é feita de forma totalmente diferente do que no BRADESCO. Para atentar esse fato, **recomendamos não usar blocos de if e seletores e usar Herança/Interfaces e classes abstratas para a melhor organização do código**.

