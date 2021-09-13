# Arquitetura do Multcob

Esse documento consta as decisões e características técnicas do Multcob.



## Componentes Executáveis do Sistema

O Sistema de CRM Multcob é bastante vasto, contendo diversos componentes executáveis para seus diversos casos de uso tais como: 

* Utilização pelo atendente de Atendente de CallCenter para contactar e celebrar acordos de cobrança com os clientes.
* Gestão de Mailing e priorização de ligacões pelo NEC.
* Controle do workflow de cobrança com os contratantes e clientes.
* Acesso, utilização e Controle da aplicação por sistemas externos via APIs.

Para esses casos de uso, o sistema usa diversos executaveis, que são as aplicações desktops, as APIs e o MultcobWorker que é usado em todo o sistema.
 
#### Aplicações Desktop

Os aplicativos desktop são desenvolvidos em .NET Framework 4.5.2 e usando Framework de tela: Windows Forms.

* **MultcobADM**: O MultcobADM é o aplicação de gestão do processo de cobrança de cada carteira de clientes, ele é usado para validar / gerenciar todo o processo de workflow como: geração de mailing / validação de baixar / controle de resultados e fluxo, entre outros. *MultcobADM é a ferramenta para interação com Multiplos Clientes*
* **MultcobCli**: O MultcobCli é a ferramenta de CRM usada no posto de atendimento de forma a ter todas as informações para celebrar acordos e realizar interações com eles. *MultcobCli é a ferramenta para interação de um cliente por vez*.
* **ZancClientEmulator**: O ZancClientEmulator realiza toda a gestão da parte de telecom no posto de atendimento do callcenter, ele é responsavel por recepcionar / gerenciar as chamadas de telecom e mandar os comandos para o CRM Multcob.

#### APIs

Atualmente com o avanço dos canais digitais, cada vez mais um CRM é usado em conjunto com diversos outros sistemas de terceiros, rodando tanto internamente na empresa, quanto externamente na nuvem. Existem diversas APIs no sistema, entre elas:

* **API Carga Horaria**: Controle da Carga Horaria dos Atendentes de CallCenter, a ser usado tanto quando utilizam o Multcob, quanto um CRM de terceiro.
* **API de Acordos**: Permite a consulta dos dados de cada cliente cadastrado nas bases do Multcob e apartir desses dados, celebrar acordos, fazer calculo de politicas entre outros.
* **API de Ocorrencias**: Permite fazer o registro de Ocorrências que são os eventos que ocorrem durante o fluxo de negociação.


#### MultcobWorker

## Acesso a Base de Dados

## Logs

