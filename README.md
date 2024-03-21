# AD162 - Desenvolva aplicativos móveis com SAP Build Code e acesse-os via SAP Mobile Start

## SAP Build Code
No ano passado, a SAP lançou o SAP Build para capacitar especialistas de negócios para construir aplicações, implementar automações e compor sites de negócios. Este ano, a família Build está sendo expandida para oferecer um atalho poderoso para o desenvolvimento de aplicações em nuvem com a introdução do **SAP Build Code**.

<p align="center"><img src="./assets/images/img-build-code-architecture.png" width="100%" /></p>

O **SAP Build Code** unifica ferramentas essenciais de desenvolvimento de aplicativos, como SAP Business Application Studio, SAP Cloud Application Programming Model (CAP), SAPUI5, SAP Mobile Services e SAP Document Management Services. Ele é alimentado pelo copiloto generativo de IA, Joule, e permite interoperabilidade com ABAP Cloud. Além disso, facilita a colaboração perfeita com as soluções de “low-code” do SAP Build e fornece recursos robustos de governança e gerenciamento do ciclo de vida.

<p align="center"><img src="./assets/images/img-build-code-benefits.png" width="100%" /></p>

Este exercício prático ajudará você a aprender como **construir aplicativos móveis usando SAP Build Code**.

## Descrição
Acelere o desenvolvimento usando o **SAP Build Code** para consumir um serviço SAP Cloud Application Programming (CAP) Model para desenvolvimento móvel. Crie um aplicativo móvel nativo e multiplataforma usando o kit de desenvolvimento móvel e reúna todo o seu trabalho no aplicativo SAP Mobile Start – a plataforma de lançamento para aplicativos móveis da SAP.

## Requisitos
Para concluir os exercícios da sessão abaixo, primeiro preencha os [pre-requisitos](./exercises/ex0/README.md).

## Caso de uso
ACME é uma empresa popular de eletrônicos. A ACME contrata representantes de suporte de call center para processar e gerenciar incidentes de clientes. Um representante de suporte da central de atendimento (Processador) recebe uma chamada telefônica de um cliente existente e cria um novo incidente em nome do cliente. A ACME emprega técnicos que usam aplicativos móveis para processar esses incidentes.

### Criação do Incidente ([AD161](https://github.com/SAP-samples/teched2023-AD161))
- Mary relata um problema que está enfrentando com seu dispositivo eletrônico ACME.
- Raj, um representante de suporte, registra o incidente usando o aplicativo Incident Management.
- Raj registra as informações de contato e detalhes do problema de Mary.

### Resolução do Incidente (AD162 - This Hands On Session)
- Anna, uma técnica, usa o aplicativo ACME Technician Incident Management.
- Anna visualiza as tarefas atribuídas a ela.
- Anna seleciona uma tarefa para ver os detalhes.
- Anna viaja até a casa de Mary para atendimento no local.
- Depois de corrigir o problema, Anna carrega uma imagem de resolução.
- Anna solicita a assinatura digital de Mary para encerrar o incidente.
- Como técnica itinerante, Anna acessa notícias organizacionais e de folha de pagamento por meio do aplicativo SAP Mobile Start.
- Ela inicia facilmente o aplicativo Incident Management no SAP Mobile Start.

## Entenda seu back-end de programação de aplicativos SAP Cloud
O back-end para esta sessão prática (AD162) foi criado usando o SAP Cloud Application Programming Model, que por sua vez se conecta a um banco de dados HANA. Três entidades são definidas no arquivo `schema.cds` e depois expostas como um serviço.
  
![LCAP View of the Back-End](./assets/images/img-2.png)

Esta sessão se concentrará na construção de um aplicativo móvel usando um back-end SAP Cloud Application Programming. Para saber mais sobre como construir um back-end usando SAP Cloud Application Programming Model (CAP), confira a sessão [session AD161](https://github.com/SAP-samples/teched2023-AD161).

## Exercícios
| Número do exercício | Título | Tempo estimado (mins) |
| ---- | ---- | --- |
| [Exercício 1](./exercises/ex1/README.md) | Execute o aplicativo inicialmente em seu dispositivo | 10 |
| [Exercício 2](./exercises/ex2/README.md) | Aprimore a lista de incidentes gerada e a página de detalhes | 20 |
| [Exercício 3](./exercises/ex3/README.md) | Modificar um registro de incidente | 40 |
| [Exercício 4](./exercises/ex4/README.md) | Integre com SAP Mobile Start | 10 |


## Como obter suporte
O suporte para o conteúdo deste repositório está disponível durante a sessão online para a qual este conteúdo foi projetado. Caso contrário, você poderá solicitar suporte por meio da guia [Problemas](../../issues).

## Additional Support and Learning Resources
- Continue your learning with additional [MDK tutorials](https://help.sap.com/doc/f53c64b93e5140918d676b927a3cd65b/Cloud/en-US/docs-en/guides/getting-started/mdk/overview.html#tutorials)

- Check out the SAP Community for [Mobile Development](https://community.sap.com/topics/mobile-technology) & [Mobile Experience](https://community.sap.com/topics/mobile-experience)

- Learn more about SAP Cloud Application Programming Model by [visting the official documentation](https://cap.cloud.sap/docs/) and [with these additional resources](https://cap.cloud.sap/docs/resources/)

## License
Copyright (c) 2023 SAP SE or an SAP affiliate company. All rights reserved. This project is licensed under the Apache Software License, version 2.0 except as noted otherwise in the [LICENSE](LICENSES/Apache-2.0.txt) file.
