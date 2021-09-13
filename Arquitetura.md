# Arquitetura do Multcob

Esse documento consta as decisões e características técnicas do Multcob.

## Componentes Executáveis do Sistema

O Sistema de CRM Multcob é bastante vasto, contendo diversos componentes executáveis para seus diversos casos de uso tais como: 

* Utilização pelo atendente de Atendente de CallCenter para contactar e celebrar acordos de cobrança com os clientes.
* Gestão de Mailing e priorização de ligacões pelo NEC.
* Controle do workflow de cobrança com os contratantes e clientes.
* Acesso, utilização e Controle da aplicação por sistemas externos via APIs.

Para esses casos de uso, o sistema usa diversos executaveis, que são as aplicações desktops, as APIs e o MultcobWorker que é usado em todo o sistema.
 
### Aplicações Desktop

Os aplicativos desktop são desenvolvidos em .NET Framework 4.5.2 e usando Framework de tela: Windows Forms.

* **MultcobADM**: O MultcobADM é o aplicação de gestão do processo de cobrança de cada carteira de clientes, ele é usado para validar / gerenciar todo o processo de workflow como: geração de mailing / validação de baixar / controle de resultados e fluxo, entre outros. *MultcobADM é a ferramenta para interação com Multiplos Clientes*
* **MultcobCli**: O MultcobCli é a ferramenta de CRM usada no posto de atendimento de forma a ter todas as informações para celebrar acordos e realizar interações com eles. *MultcobCli é a ferramenta para interação de um cliente por vez*.
* **ZancClientEmulator**: O ZancClientEmulator realiza toda a gestão da parte de telecom no posto de atendimento do callcenter, ele é responsavel por recepcionar / gerenciar as chamadas de telecom e mandar os comandos para o CRM Multcob.

### APIs

Atualmente com o avanço dos canais digitais, cada vez mais um CRM é usado em conjunto com diversos outros sistemas de terceiros, rodando tanto internamente na empresa, quanto externamente na nuvem. Existem diversas APIs no sistema, entre elas:

* **API de Carga Horaria**: Controle da Carga Horaria dos Atendentes de CallCenter, a ser usado tanto quando utilizam o Multcob, quanto um CRM de terceiro.
* **API de Acordos**: Permite a consulta dos dados de cada cliente cadastrado nas bases do Multcob e apartir desses dados, celebrar acordos, fazer calculo de politicas entre outros.
* **API de Ocorrencias**: Permite fazer o registro de Ocorrências que são os eventos que ocorrem durante o fluxo de negociação. Dessa forma, sistemas externos podem fazer a marcaçáo de eventos que ocorreram fora do CRM, como geração de boletos, celebração de acordos em agencias bancárias, contatos por website do contratante, e vários outros.

### MultcobWorker

O MultcobWorker é um aplicativo de linha comando que é muito especial, e merece uma categoria a parte.

Porque na realidade ele encapsula diversas funcionalidades dentro dele de forma a ser usado como worker em operações de lógica de negócio de forma paralela, então, quando estamos consumindo dados de importação de forma multhreaded são os workers q paralelizam o trabalho a ser feito.

Nas APIs, o MultcobWorker é usado para encapsular e executar uma determinada operação de negócio de forma que a API apenas se especialize em receber a requisição http do cliente, chamar o worker, e enviar de volta o retorno daquela operação.

## Acesso a Base de Dados

O Multcob por ser um sistema relativamente legado, ele não usa em todo o seu código, um mecanismo de ORM (Object-Relational-Mapping), sendo a maior parte da escrita e leitura de dados sendo feita escrevendo de forma manual os comandos em SQL.

Nos projetos mais recentes, temos optado por usar um ORM .NET chamado Linq2DB que permite a manipulação de dados de banco de dados usando LINQ. Essa é a biblioteca a ser usada daqui para frente em novos desenvolvimentos.

## Logs

Por ser um software que é executado em diversas frentes, tanto em postos de atendimento de callcenter, quanto em APIs, quanto em backoffices da empresa, é necessário o uso extensivo de logs de forma a permitir uma rastreabilidade de oque aconteceu durante a execução de um módulo específico do sistema.

Esses logs, muitas vezes, na realidade são a principal forma de depuração do programa, exatamente pela característica distribuida dele. Todos os logs sao atômicos a nivel de programa e de máquina sendo executada, e fiquem gravadas na máquina local do usuário.

A maior parte do código usa a classe: ZancShared.SHSyncLog para a produção de logs que podem dai ser enviados por email para os desenvolvedores. 

