# Exercício 2 - Aprimore a lista de incidentes gerada e a página de detalhes

## Tempo estimado

:clock4: 20 minutos

## Objetivo

Neste exercício, você fará algumas melhorias no
- Página da lista de incidentes
    - Primeiro, você exibirá o nome do cliente. 
    - Em seguida, você adicionará uma barra de feedback de filtro que aparecerá acima da lista de incidentes para filtrar incidentes com base em determinados critérios. 
- Página de detalhes do incidente
    - Você substituirá o cabeçalho de objeto existente por um cabeçalho de perfil. Essa melhoria fornecerá informações adicionais e acesso aprimorado a vários métodos de comunicação com um cliente.

| Número do exercício   | Título                                                 |
|-------------------|-------------------------------------------------------|
| [Exercício 2.1](#exercise-21---display-customer-name-on-the-incident-list-page)      | Exibir o nome do cliente na página Lista de incidentes  |
| [Exercício 2.2](#exercise-22---add-a-filter-feedback-bar-on-the-incident-list-page)      | Adicionar uma barra de feedback de filtro na página Lista de incidentes  |
| [Exercício 2.3](#exercise-23---replace-the-existing-object-header-with-profile-header-ui-control)      | Substitua o cabeçalho do objeto existente pelo controle da UI do cabeçalho do perfil  |
| [Exercício 2.4](#exercise-24---redeploy-the-application)      | Reimplantar o aplicativo  |
| [Exercício 2.5](#exercise-25---update-the-mdk-app-with-new-metadata)      | Atualize o aplicativo MDK com novos metadados  |

### Exercício 2.1 - Exibir o nome do cliente na página Lista de incidentes

Como técnico, você pode querer ver quem relatou um incidente sem navegar até a página de detalhes. Você também pode filtrar a lista de incidentes com base no status (como novo ou em processo) e na urgência (como alta).

1. A entidade Incidente possui uma propriedade de navegação `customer` definida na definição do serviço OData que permite acessar informações do cliente. 

    Para encontrar a definição de serviço, navegue até `Services` &rarr; `.IncidentManagement.xml` em seu projeto de metadados MDK. Você usará esta propriedade de navegação `customer` para acessar os detalhes de um cliente.
   
    ![MDK](images/2.1.1.png)

2. A propriedade de navegação `customer` já foi definida na página da lista de Incidentes. Esta informação pode ser encontrada navegando até `Pages` &rarr; `Incident` &rarr; `Incident_List.page`. Selecione o controle Object Table para encontrar a ligação da propriedade `QueryOptions`.

    ![MDK](images/2.1.2.png)

3. Role para baixo pelas propriedades da Tabela de objetos e clique no ícone do link próximo à propriedade **Footnote** para abrir o Navegador de objetos.
    - Digite manualmente `Reported by` no campo Expressão, seguido de um espaço.
    - No campo de busca, procure pelo nome do cliente, selecione `FirstName` e clique em `Insert`. A caixa de expressão irá gerar a ligação `Reported by {customer/FirstName}` **Don't close the Object Browser window**.
    - Adicione um espaço após o valor gerado.
    - Procure o sobrenome do cliente no campo de pesquisa, selecione `LastName` e clique em `Insert`. 
        > A caixa de expressão irá gerar a ligação `Reported by {customer/FirstName} {customer/LastName}`. 
    - Clique em **OK** para definir esse valor no campo de controle.

    ![MDK](images/2.1.3.gif)

### Exercício 2.2 - Adicionar uma barra de feedback de filtro na página Lista de incidentes

Uma barra de feedback do filtro é uma barra horizontal que aparece acima de uma lista de conteúdo (em uma tabela seccionada). Ele usa chips interativos para indicar quais filtros foram aplicados à lista e permite que os usuários apliquem rapidamente os filtros usados ​​com frequência.

1. Em `Incident_List.page`, navegue até a `Sectioned Table` destacada.

    ![MDK](images/2.2.1.png)

2. No painel Propriedade, selecione **Object Collection** para a propriedade `FastFilters` na seção **FilterFeebackBar**.

    ![MDK](images/2.2.2.png)

3. Clique em **Add**. Você verá um objeto `item0` gerado. Expanda-o para visualizar suas propriedades.

    ![MDK](images/2.2.3.png)

4. Preencha as seguintes informações:

    | Propriedade | Valor |
    |----|----|
    | `DisplayValue` | `High Priority` |
    | `FilterType` | Choose `Filter` from the dropdown |
    | `ReturnValue` | `Urgency eq 'High'` |    

    ![MDK](images/2.2.4.png)    

5. Adicione outro item ao `FastFilters` e preencha as seguintes informações: 

    | Propriedade | Valor |
    |----|----|
    | `DisplayValue` | `Open Status` |
    | `FilterType` | Choose `Filter` from the dropdown |    
    | `ReturnValue` | `Status eq 'New' or Status eq 'In Process'` |    

    ![MDK](images/2.2.5.png)   

6. Defina **true** para a propriedade `ShowAllFilters`, se ainda não estiver definida.

    ![MDK](images/2.2.6.png) 

### Exercício 2.3 - Substitua o cabeçalho do objeto existente pelo controle da UI do cabeçalho do perfil

Um controle de UI de cabeçalho de perfil fornece informações adicionais e aprimora o acesso a vários métodos de comunicação com um cliente.

1. Navegue até `Pages` &rarr; `Incident` &rarr; `Incident_Detail.page`. Atualize as `QueryOptions` da página `DesignTimeTarget` para acessar as informações do cliente em tempo de design. Clique nos ícones de três pontos para abrir o Navegador de objetos da propriedade `QueryOptions`.

    ![MDK](images/2.3.1.png) 

    >A propriedade `DesignTimeTarget` é semelhante ao Target, mas é usada apenas para tempo de design. Isso permite que o Navegador de Objetos mostre uma lista filtrada com base no Design Time Target em vez da lista completa de todas as Entidades.

2. Selecione a propriedade de expansão `customer` e você notará que o valor da expressão é atualizado de acordo. Clique em **OK** para fechar o Editor de Expressões de Opções de Consulta. Agora você pode acessar e vincular informações do cliente a qualquer controle na página de detalhes.

    ![MDK](images/2.3.2.png) 

3. Clique na área destacada para acessar o controle Object Header existente.

    ![MDK](images/2.3.3.png) 

4. Clique com o botão direito no controle Object Header e **Delete**.

    ![MDK](images/2.3.4.png) 

5. Agora, você adicionará o controle **Profile Header** para exibir informações como nome, localização e métodos de comunicação com um cliente. <br/> No Layout Editor, expanda **Controls** &rarr; **Static Container** e arraste e solte o controle **Profile Header** na parte superior da área da página.

    ![MDK](images/2.3.5.gif) 

6. No painel **Properties** em **Appearance**, limpe o valor padrão da propriedade `Description`. 

7. Para a propriedade `DetailImage`, clique no ícone do link para abrir o Object Browser, procure o ícone SAP `customer` e clique duas vezes nele. 

    ![MDK](images/2.3.6.gif) 

8. Para a propriedade `Headline`, clique no ícone do link para abrir o Navegador de objetos e vincular ao nome e sobrenome do cliente.

     > Certifique-se de que `OData Objects` esteja selecionado no menu suspenso.

    - No campo de pesquisa, procure por `first`, selecione `FirstName` e **clique duas vezes nele**. A ligação `{customer/FirstName}` será gerada na caixa de expressão. **Não feche a janela do Navegador de objetos**.
    - Adicione um espaço após o valor gerado.
    - Procure por `last` no campo de pesquisa, selecione `LastName` e **clique em `Insert`**. Você notará a ligação `{customer/FirstName} {customer/LastName}` gerada na caixa de expressão. 
    - Clique em **OK** para definir o valor para o campo de controle.

    ![MDK](images/2.3.7.gif) 

9. Siga instruções semelhantes para a propriedade `Subheadline`, vinculando-a aos valores de cidade e país do cliente `{customer/AddressCountry}`. 

    ![MDK](images/2.3.8.gif)  

10. Na seção `ActivityItems` no painel Propriedades, clique em **Add** para criar um novo item de atividade.

    ![MDK](images/2.3.9.png) 

11. Expanda o item recém-adicionado e clique no ícone de três pontos de `ActivityValue` para abrir o Navegador de objetos. Vincule a propriedade `Phone` da entidade Cliente.

    ![MDK](images/2.3.10.gif) 

12. Adicione mais dois itens de atividade de maneira semelhante para Email e Mensagem e vincule-os às propriedades Email e Telefone do cliente.

    ![MDK](images/2.3.11.png) 

### Exercício 2.4 - Reimplantar o aplicativo

Agora que você concluiu as alterações nas páginas Lista de incidentes e Detalhes, é hora de implantar as alterações para ver o resultado.

1. Clique com o botão direito no arquivo `Application.app` no painel do explorador de projetos, escolha `MDK:Deploy` e selecione o destino de implementação como **Mobile Services**. Quando a implantação for bem-sucedida, uma mensagem de sucesso aparecerá. Se a implantação travar, recarregue a página e tente novamente.

    ![MDK](images/2.4.1.png)
    ![MDK](images/2.4.2.png)

    >Alternativamente, você pode selecionar `MDK: Redeploy` na paleta de comandos. Para acessar a paleta de comandos, vá ao menu Exibir e escolha Paleta de Comandos ou pressione Command+Shift+P em um Mac ou Ctrl+Shift+P em uma máquina Windows. Este comando executará a última implantação.
    
    >![MDK](images/2.4.3.png)


### Exercício 2.5 - Atualize o aplicativo MDK com novos metadados

| Steps&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Android | iOS&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|---|---|---|
| 1. Toque na opção **Check for updates** no `User menu` na página Incidentes.| ![MDK](images/2.5.1.png)| ![MDK](images/2.5.2.png)|
| 2. Você verá um pop-up `New Version Available!`. Toque em **Now**.| ![MDK](images/2.5.3.png)| ![MDK](images/2.5.4.png)|
| 3. Na página Lista de incidentes, agora você vê o nome do cliente e uma barra de filtros para aplicar filtros rápidos. <br/><br/>- Na página Detalhes, um cabeçalho de perfil exibirá os detalhes do cliente e itens de comunicação. Isso permitirá que você envie um e-mail, faça uma ligação ou envie uma mensagem ao cliente. | ![MDK](images/2.5.5.gif)| ![MDK](images/2.5.6.gif)|



## Sumário

Você aprimorou as páginas de incidentes para melhor atender o técnico. Agora eles podem compreender facilmente as informações e entrar em contato com o cliente quando necessário.

## Navigation

| Previous| Next |
|---|---|
| [Exercise 1](../ex1/README.md) | [Exercise 3](../ex3/README.md) |
