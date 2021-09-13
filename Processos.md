# Processos de Engenharia de Software do Multcob

O Multcob é um sistema bastante grande, sendo desenvolvido a mais de 15 anos, com mais de 1.5 milhão de linhas, e com uma solution com quase 170 projetos.

Um software desse tamanho precisa de uma estrutura de engenharia de software bastante clara, robusta e funcional e o objetivo desse documento é melhor explicar esse funcionamento.

## Estrutura de Gestão e Controle de Versão

Se utiliza git para o controle de versão do sistema, e ele é a principal forma de troca de informação e colaboraçáo entre os desenvolvedores. 

No uso do git, usamos as seguintes "doutrinas": MonoRepo e GitFlow

### [MonoRepo](https://www.atlassian.com/git/tutorials/monorepos)

No Monorepo, temos apenas um(1) repositório de git para todo o projeto. 

Essa doutrina é bastante útil para nós porque na realidade o sistema Multcob tem vários executáveis e apis que compartilham muito código. Sem ela, teriamos q possivelmente ter um CRM para cada um dos contratantes. 

### [GitFlow](https://www.atlassian.com/br/git/tutorials/comparing-workflows/gitflow-workflow)

No GitFlow, cada branch do git representa um conjunto lógico de alterações no sistema, esses branches tem a seguinte estrutura:

* **master**: Contém a versáo estável de maior significação, com o seguinte padrão: (N.*.*.*), ou seja, determinada pelo primeiro digito da versáo. Ela geralmente é gerada em media a cada 2-3 anos.
* **desenvolvimento**: Contém a subversão estável do sistema, com o seguinte padrão: (N.N.*.*), ou seja, determinada pelo primeiro e segundo digito da versão. Ela geralmente é gerada em media a cada 2-3 meses.
* **staging\_\(N\)\_\(N\)**: Os branches de staging com os dois digitos da próxima versáo são versões *semi-estaveis*, usadas em produçáo para agregar funcionalidades para próxima geraçáo da versáo estável.
    * *Hotfixes*: Sáo colocadas na branch: staging\_\(N\)\_\(N\), por serem de baixa complexidade e geralmente contendo apenas um commit.       
* **staging\_\(NomeBranch\)**: Esses branches contém uma (1) funcionalidade em desenvolvimento e que náo está estavel para merge em produção.

## Linguagem de Programação e Frameworks

O Multcob é desenvolvido primáriamente em .NET Framework 4.5.2, usando VB.NET. 

Ele está sendo migrado para C# usando .NET Framework 5.0, sendo as APIs o primeiro grupo de funcionalidades a serem migradas.

Procuramos desenvolver todas as funcionalidades do sistema usando .NET puro, sem a dependencia de componentes de terceiros, sendo as principais exceções:

* **Python**: Para uso em pre-processadores de arquivos de texto de clientes para importaçáo de dados.
* **ReactJS**: Uso em conjunto com o Chrome Embedded Framework para as novas telas de acordo usando WebViews do CEF (Chrome Embedded Framework). 

## Integração Contínua

Toda a geração de versáo é automatica, usando jenkins no servidor 144. Cada job do jenkins recebe o nome do branch sa ser gerado versão, e temos dai a construçáo dos artefatos necessários. 
