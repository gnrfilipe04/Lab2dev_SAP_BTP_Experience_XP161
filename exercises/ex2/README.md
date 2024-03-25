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

    >The `DesignTimeTarget` property is similar to Target, but is only used for design time. This allows the Object Browser to show a filtered list based on the Design Time Target rather than the full list of all Entities.

2. Select the `customer` expand property, you'll notice that the expression value updates accordingly. Click **OK** to close the Query Options Expression Editor. You can now access and bind customer information to any control on the detail page.

    ![MDK](images/2.3.2.png) 

3. Click on the highlighted area to access the existing Object Header control.

    ![MDK](images/2.3.3.png) 

4. Right-click on the Object Header control and **Delete** it.

    ![MDK](images/2.3.4.png) 

5. Now, you will add the **Profile Header** control to display information such as name, location, and communication methods with a customer. <br/> In the Layout Editor, expand the **Controls** &rarr; **Static Container** group, then drag and drop the **Profile Header** control onto the top of the page area.

    ![MDK](images/2.3.5.gif) 

6. In the **Properties** pane under **Appearance**, clear the default value for the `Description` property. 

7. For the `DetailImage` property, click on the link icon to open the Object Browser, search for the `customer` SAP icon and double click on it. 

    ![MDK](images/2.3.6.gif) 

8. For the `Headline` property, click on the link icon to open the Object Browser and bind to Customer's First and Last names.

     > Ensure that `OData Objects` is selected in the dropdown menu.

    - In the search field, look for `first`, select `FirstName` and **double-click on it**. The binding `{customer/FirstName}` will be generated in the expression box. **Do not close the Object Browser window**.
    - Add a space after the generated value.
    - Look for `last` in the search field, select `LastName` and **click on `Insert`**. You'll notice the binding `{customer/FirstName} {customer/LastName}` generated in the expression box. 
    - Click **OK** to set the value to the control field.

    ![MDK](images/2.3.7.gif) 

9. Follow similar instructions for the `Subheadline` property, binding it to the customer's city and country values `{customer/AddressCity} {customer/AddressCountry}`. 

    ![MDK](images/2.3.8.gif)  

10. Under the `ActivityItems` section in the Properties pane, click **Add** to create a new activity item.

    ![MDK](images/2.3.9.png) 

11. Expand the newly added item, then click the three-dot icon for the `ActivityValue` to open the Object Browser. Bind the `Phone` property of the Customer entity.

    ![MDK](images/2.3.10.gif) 

12. Add two more activity items in a similar manner for Email and Message, and bind them to the customer's Email and Phone properties.

    ![MDK](images/2.3.11.png) 

### Exercise 2.4 - Redeploy the application

Now that you have completed the changes to the Incident List and Detail pages it is time to deploy the changes to see the result.

1. Right-click the `Application.app` file in the project explorer pane, choose `MDK:Deploy` and then select deploy target as **Mobile Services**. When the deployment is successful, a success message will appear. If the deployment gets stuck, reload the page and try again.

    ![MDK](images/2.4.1.png)
    ![MDK](images/2.4.2.png)

    >Alternatively, you can select `MDK: Redeploy` from the command palette. To access the command palette, go to the View menu and choose Command Palette, or press Command+Shift+P on a Mac or Ctrl+Shift+P on a Windows machine. This command will perform the last deployment.
    
    >![MDK](images/2.4.3.png)


### Exercise 2.5 - Update the MDK app with new metadata

| Steps&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Android | iOS&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|---|---|---|
| 1. Tap the **Check for Updates** option in the `User menu` on the Incidents page.| ![MDK](images/2.5.1.png)| ![MDK](images/2.5.2.png)|
| 2. You will see a `New Version Available!` pop-up.  Tap **Now**.| ![MDK](images/2.5.3.png)| ![MDK](images/2.5.4.png)|
| 3. On the Incident list page, you now see the customer's name and a filter bar for applying quick filters. <br/><br/>- On the Detail page, a profile header will display the customer's details and communication items. This will allow you to email, make a phone call, or send a message to the customer.| ![MDK](images/2.5.5.gif)| ![MDK](images/2.5.6.gif)|



## Summary

You've enhanced the incident pages to better suit the technician. They can now easily understand the information and reach out to the customer when needed.

## Navigation

| Previous| Next |
|---|---|
| [Exercise 1](../ex1/README.md) | [Exercise 3](../ex3/README.md) |
