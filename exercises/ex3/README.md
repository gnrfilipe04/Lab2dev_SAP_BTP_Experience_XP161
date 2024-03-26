# Exercício 3 - Modificar um Registro de Incidente

## Tempo Estimado

:clock4: 40 minutos

## Objetivo

Os incidentes são atribuídos a um Técnico por um representante de suporte do call center. No início do dia, o técnico começa a trabalhar nesses incidentes enquanto está no local do cliente.

- Se o status de um incidente for `New`, o técnico pode atualizá-lo para `In Process`.
- O técnico também pode atualizar o status para `Closed` depois de resolver o problema do cliente.
- Para encerrar um incidente, um técnico deve:
    - Atualize o ID do dispositivo com defeito inserindo manualmente o código ou digitalizando o código de barras do dispositivo.
    - Carregue uma fotografia do dispositivo de trabalho.
    - Adquira a assinatura digital do cliente confirmando que o problema foi resolvido.
- Se o status de um incidente já estiver `Closed`, o técnico não verá nenhuma opção para modificar os detalhes. Eles têm a capacidade de visualizar seus detalhes e abrir a imagem do dispositivo de trabalho.

| Número do Exercício   | Título                                                 |
|-------------------|-------------------------------------------------------|
| [Exercício 3.1](#exercício-31---crie-uma-nova-página-para-modificar-as-informações-do-incidente)      | Crie uma nova página para modificar as Informações do Incidente  |
| [Exercício 3.2](#exercício-32---adicione-um-botão-cancelar-na-página-atualizar-detalhes-do-incidente)      | Adicione um botão Cancelar na página Atualizar detalhes do incidente|
| [Exercício 3.3](#exercício-33---armazene-os-dados-atualizados-localmente)      | Armazene os dados atualizados localmente                        |
| [Exercício 3.4](#exercício-34---valide-as-entradas-antes-de-salvar-a-entidade-incidente)      | Valide as Entradas antes de salvar a Entidade Incidente   
| [Exercício 3.5](#exercício-35---navegue-até-a-página-de-edição-de-incidentes)      | Navegue até a página Editar Incidente                     |
| [Exercício 3.6](#exercício-36---reimplantar-o-aplicativo)      | Reimplantar o aplicativo                               |
| [Exercício 3.7](#exercício-37---atualize-o-aplicativo-mdk-com-novos-metadados)      | Atualize o aplicativo MDK com novos metadados                   |


### Exercício 3.1 - Crie uma nova página para modificar as Informações do Incidente

Os aplicativos on-line e off-line podem ser modificados pelos usuários. As alterações de aplicativos on-line são salvas no back-end imediatamente, enquanto os aplicativos off-line armazenam as alterações localmente até que sejam sincronizadas no back-end usando uma ação de upload.

Nesta etapa, você criará uma página de Seção com uma seção de Célula de Formulário para os controles de Célula de Formulário. Esta página exibirá um subconjunto de itens da página Detalhes do Incidente, especificamente os campos editáveis pelo técnico.

1. Navegue até **Pages** &rarr; Clique com o botão direito do mouse na pasta **Incident** &rarr; selecione **MDK: New Page**.

    ![MDK](images/3.1.1.png)

2. Escolha **Section** e clique em **Next**.

    ![MDK](images/3.1.2.png)

3. Na etapa **Base Information**, insira o campo **Name** como `Incident_Edit` e clique em **Finish**.

    ![MDK](images/3.1.3.png)

4. Na seção `DesignTimeTarget`, forneça as informações abaixo. Isso permite a validação do contexto de vinculação da página atual e o acesso às entidades Incidente e do Cliente no momento do projeto.

    | Propriedade | Valor |
    |----|----|
    | `Service` | Escolha `IncidentManagement.service` no menu suspenso |
    | `EntitySet` | Escolha `Incident` no menu suspenso |    
    | `QueryOptions` | `$expand=customer` |    

    ![MDK](images/3.1.4.gif)

5. No painel **Properties**, defina a **Caption** como `Update Incident Detail`.

    ![MDK](images/3.1.5.png)

6. Em seguida, você adicionará campos editáveis por um técnico, incluindo status, ID do nome do dispositivo com defeito, imagem do dispositivo e assinatura do cliente. No Editor de Layout, expanda o grupo **Static Container**. Arraste e solte o **Form Cell** na área da Página.

    ![MDK](images/3.1.6.gif)

    >A seção Célula de Formulário é usada para conter controles de Célula de Formulário em uma página de seção.

7. Agora você adicionará controles de Célula de Formulário à seção Célula de Formulário. Expanda o grupo **Form Cell Controls**, arraste e solte um **List Picker** na seção Célula de Formulário na área da página.

    ![MDK](images/3.1.7.gif)

8. Forneça as seguintes informações:

    | Propriedade | Valor |
    |----|----|
    | `Name`| `FCStatus` |
    | `Caption` | `Status` |
    | `AllowEmptySelection` | Escolha `false` no menu suspenso |
    | `IsPickerDismissedOnSelection`  | Escolha `true` no menu suspenso |

    ![MDK](images/3.1.8.png)

    >- `AllowEmptySelection:` Isso desativa ou ativa a seleção do conjunto de valores vazios.
    >- `IsPickerDismissedOnSelection:` Isso permite a demissão automática da visualização da lista depois que uma entrada é selecionada.

9. Quando um técnico está atualizando o status de um incidente, ele deve receber opções específicas, dependendo do status atual do incidente.
   - Se o status atual for `New` ou `In Process`, o técnico deve ver as opções `In Process` e `Closed`.
   - No painel **Properties**, para a propriedade `PickerItems`, forneça os valores como `In Process` e `Closed` para `item0` e `item1`, respectivamente. Clique no `item2` e, em seguida, clique no ícone da lixeira para excluí-lo.

    ![MDK](images/3.1.9.png)

10. Ao atualizar um incidente, o status atual ficará visível no seletor de lista.
    - Se o status atual for `New`, o valor ficará em branco. Isso ocorre porque não faria sentido para eles atualizarem o status para `New` novamente; em vez disso, eles provavelmente escolheriam `In Process` ou `Closed`.
    - Se o status atual for `In Progress`, o técnico tem duas opções:
        - Eles podem deixar o valor padrão como `In Progress`, atualizar o ID do dispositivo e continuar trabalhando no incidente atribuído.
        - Eles podem alterar o status para `Closed` e fornecer todas as informações necessárias para fechar o incidente.
    - Clique no ícone do link para abrir o Navegador de Objetos para a propriedade **Value**. Selecione **OData Objects** no menu suspenso. No campo de pesquisa, procure o status, selecione `Status` e clique duas vezes nele. Clique em **OK**.

    ![MDK](images/3.1.10.gif)


11. Abaixo do controle do seletor de lista na seção Célula de Formulário da área `Incident_Edit.page`, arraste e solte um controle de célula de formulário **Simple Property**. Isso permite que um técnico insira ou digitalize manualmente o ID do dispositivo defeituoso.

    ![MDK](images/3.1.13.gif)

12. Forneça as seguintes informações:

    | Propriedade | Valor |
    |----|----|
    | `Name`| `FCDeviceID` |
    | `Caption` | `Device ID` |
    | `AlternateInput` | Escolha `Barcode` no menu suspenso |
     `Value` | Clique no ícone do link para abrir o Navegador de Objetos e vinculá-lo ao `Device ID` |
    | `PlaceHolder`  | `Type in the device's ID or scan its barcode` |

    ![MDK](images/3.1.14.png)

13. Abaixo do controle de propriedade simples na seção Célula de Formulário da área `Incident_Edit.page`, arraste e solte um controle de Célula de Formulário **Attachment**. Isso permite que um técnico faça o upload de uma imagem do dispositivo que consertou.

    ![MDK](images/3.1.15.gif)

14. Provide the following information:          

    | Propriedade | Valor |
    |----|----|
    | `Name` | `FCDeviceImage` |
    | `IsVisible` | `false` |
    | `AttachmentActionType` | Desmarque a opção `SelectFile` |
    | `AttachmentAddTitle` | `Add` |
    | `AttachmentTitle` | `Device Image` | 

    ![MDK](images/3.1.16.png)

15. Abaixo do controle de anexo na seção Célula de Formulário da área `Incident_Edit.page`, arraste e solte um controle de Célula de Formulário **Inline Signature Capture**. Isso permite que um técnico colete uma assinatura digital do cliente para confirmar que o problema foi resolvido.

    ![MDK](images/3.1.17.gif)

16. Forneça as seguintes informações:

    | Propriedade | Valor |
    |----|----|
    | `Name` | `FCCustomerSignature` |
    | `Caption` | `Customer Signature` |
    | `ShowTimestampInImage` | Escolha `true` no menu suspenso |
    | `TimestampFormatter` | `YYYY-MM-dd 'at' HH:mm:ss` |
    | `WatermarkText` | `Signed by {customer/FirstName} {customer/LastName}` | 
    | `IsVisible` | `false` |

    ![MDK](images/3.1.18.png)

    >- `ShowTimestampInImage:` A data e hora será exibida na imagem de assinatura capturada.
    >- `TimestampFormatter:` Defina uma string padrão de formato DateTime para o carimbo de data/hora na imagem de assinatura capturada.
    >- `WatermarkText:` O texto da marca d'água será exibido na imagem de assinatura capturada.

17. Se a opção `In Process` for escolhida no seletor de lista de Status durante uma modificação de Incidente, as opções para fazer upload de uma Imagem do Dispositivo e capturar a assinatura do cliente devem estar ocultas. No entanto, se o status `Closed` for selecionado, o técnico deve receber opções para fazer upload de uma imagem do dispositivo e coletar a assinatura do cliente. Essa lógica precisa ser adicionada ao `Incident_Edit.page` no aplicativo.

    Selecione o controle do selecionador de lista `Status`, navegue até a guia **Event**, clique em **Create a rule/action** para o evento `OnValueChange`.

    ![MDK](images/3.1.20.png)

18. Em seguida, selecione **Object Type** como **Rule** e **Folders** como `/MDKApp/Rules/Incident`. Clique em **OK**. Isso mantém todos os arquivos relacionados organizados juntos.

    ![MDK](images/3.1.10.png)

19. Forneça o nome `StatusChangeProtocol` à sua regra, clique em **Finish**.

    ![MDK](images/3.1.21.png)

20. Substitua o snippet gerado pelo seguinte código.

    ```JavaScript
    /**
    * Describe this function...
    * @param {IClientAPI} clientAPI
    */
    export default function StatusChangeProtocol(clientAPI) {
        //Get the Sectioned Table based on the name
        const sectionedTable = clientAPI.getPageProxy().getControl('SectionedTable0');
        //Get the section based on the name
        const fcsection = sectionedTable.getSection('SectionFormCell0');
        //Get the control based on the name
        const fcAttachment = fcsection.getControl('FCDeviceImage');
        const fcSignatureCapture = fcsection.getControl('FCCustomerSignature');
        const selectedValue = clientAPI.getValue()[0].ReturnValue;
        if (selectedValue == "In Process") {
            fcAttachment.setVisible(false);
            fcSignatureCapture.setVisible(false);
        } else if (selectedValue == "Closed") {
            fcAttachment.setVisible(true);
            fcSignatureCapture.setVisible(true);
        }
    }
    ```

### Exercício 3.2 - Adicione um Botão Cancelar na página Atualizar detalhes do incidente

Ao atualizar os detalhes do incidente, você deseja dar ao usuário a opção de fechar a página de edição e não salvar nenhum valor inserido.

1. No `Incident_Edit.page`, arraste e solte um controle **Action Bar Item** no canto superior esquerdo da barra de ação.

    ![MDK](images/3.2.1.png)

    >O Action Bar Item é um botão que os usuários podem usar para acionar ações quando pressionados. Você pode adicionar um Item da Barra de Ação apenas à Barra de Ação na parte superior da página.

2. No painel Propriedades, forneça as seguintes informações:

    | Propriedade | Valor |
    |----|----|
    | `Caption` | `Cancel` |
    | `SystemItem` | Clique no **link icon** para abrir o Navegador de Objetos, clique duas vezes no tipo **Cancel** e clique em **OK**. |

    ![MDK](images/3.2.2.png)

    >System Items são ícones predefinidos fornecidos pelo sistema.

3. Navegue até a guia **Events**. Clique no ícone de três pontos, depois clique no **Object Browser** e vincule-o a `CloseModalPage_Cancel.action`. Esta ação fechará a página atual e encerrará quaisquer eventos em andamento.

    ![MDK](images/3.2.3.png)


### Exercício 3.3 - Armazene os dados atualizados localmente

Enquanto um Técnico está atualizando informações de incidentes, como Status, ID do Dispositivo, Imagem do Dispositivo e Assinatura do Cliente, esses detalhes serão comunicados ao back-end por meio de chamadas OData relevantes com base no tipo de entidade e em seus respectivos tipos de propriedade OData.

Você pode encontrar detalhes da definição do serviço em seu projeto de metadados MDK `/Services/. IncidentManagement.xml`.
    
![MDK](images/3.3.1.png)

Para atualizar as propriedades `Status` e `DeviceID` da entidade Incidente, a ação OData Update Entity é usada. <br/> No entanto, ao lidar com as propriedades `DeviceImage` e `ResolutionSignatureImage` da entidade Incidente, que são do tipo Edm.Stream, a ação OData UploadStream é usada. As propriedades do fluxo são usadas para armazenar dados binários, como imagens ou arquivos.

- Agora você adicionará um item da Barra de Ação no `Incident_Edit.page`. Este item acionará uma ação da Entidade de Atualização OData para salvar o Status e o ID do Dispositivo.
- Após a conclusão bem-sucedida da ação OData Update Entity, você iniciará uma ação OData Upload Stream para salvar a Imagem do Dispositivo e a Assinatura do Cliente.
- Depois que as ações de atualização forem executadas com sucesso, feche a página Editar.
- Uma mensagem de falha deve ser exibida se qualquer uma das ações não conseguir executar as alterações.

1. No `Incident_Edit.page`, **drag and drop** um **Action Bar Item** no canto superior direito da barra de ação.

    ![MDK](images/3.3.2.png)

2. No painel Propriedades, forneça as seguintes informações:        

    | Propriedade | Valor |
    |----|----|
    | `Caption` | `Save` |
    | `SystemItem` | Clique no **link icon** para abrir o Navegador de Objetos, clique duas vezes no tipo **Save** e clique em **OK**. |

    ![MDK](images/3.3.3.png)

3. Navegue até a guia **Events**. Clique no ícone de três pontos para a propriedade `OnPress` e selecione `Create a rule/action`.

    ![MDK](images/3.3.4.png)

4. Defina a seleção para o caminho `Object Type` como **Action** e `Folders` como `/MDKApp/Actions/Incident`. Isso mantém todos os arquivos relacionados organizados juntos.

    ![MDK](images/3.3.5.png)   

5. No menu suspenso de pesquisa **Category**, escolha **Data** | clique em **OData** | clique em **Next**.

    ![MDK](images/3.3.6.png)   

6. Na etapa **Base Information**, forneça as seguintes informações e clique em **Next**.

    | Propriedade | Valor |
    |----|----|
    | `Name`| `Incident_UpdateEntity` |
    | `Type` | Selecione `UpdateEntity` no menu suspenso |
    | `Service`| Selecione `IncidentManagement.service` no menu suspenso |
    | `EntitySet`| Selecione `Incident` no menu suspenso |
    | `ReadLink`| Clique no ícone do link para abrir o Navegador de Objetos e clique duas vezes em `readLink` |

    ![MDK](images/3.3.7.png)  

    >O `readLink` é uma referência direta a uma entrada de conjunto de entidades individuais.

7.  Na etapa **Property and Update Links**, desmarque **ID**.

8.  Você vinculará as propriedades `Status` e `DeviceID` OData aos respectivos Controles da Interface do Usuário.
    - Selecione a propriedade `Status` e clique no **link icon** para abrir o Navegador de Objetos.
    - No Navegador de Objetos, altere o menu suspenso para `Control & ClientData` e selecione o botão de opção **Current Page**.
    - Na caixa de pesquisa, comece a digitar `status`. A lista será filtrada para exibir os valores correspondentes. Clique duas vezes na entrada **SelectedValue (Value)** no campo `FCStatus` e clique em **OK** para definir a vinculação.

    ![MDK](images/3.3.8.gif)  

    >`SelectedValue` fornece o valor de retorno da seleção List Picker.

9. Repita a etapa acima para DeviceID.
    - Selecione a propriedade `DeviceID` e clique no **link icon** para abrir o Navegador de Objetos. 
    - Altere o menu suspenso no Navegador de Objetos para `Control & ClientData`, clique no botão de opção **Current Page**.
    - Na caixa de pesquisa, comece a digitar `device`. A lista será filtrada para baixo para mostrar os valores correspondentes. Clique duas vezes na entrada **Value (Value)** no campo `FCDeviceID` e clique em **OK** para definir a vinculação.

    ![MDK](images/3.3.9.gif) 

10. Clique em Concluir. O editor de ação será aberto com o `Incident_UpdateEntity.action` carregado.

11. Quando este `Incident_UpdateEntity.action` falha devido a algum motivo, você pode querer exibir um erro. No `Incident_UpdateEntity.action`, role para baixo e expanda a seção **Common Action Properties**. Clique no ícone do link para a propriedade `Failure Action` para abrir o Navegador de Objetos e vincular a uma ação de mensagem existente `GenericMessageBox.action`.

    ![MDK](images/3.3.10.png) 

12. Vamos substituir as propriedades desta ação e definir algumas informações específicas sobre `Incident_UpdateEntity.action`. Clique no ícone de substituição para abrir o assistente de propriedades de ação de substituição.

    ![MDK](images/3.3.11.png) 

13. Forneça as seguintes informações e clique em **OK**.

    | Propriedade | Valor |
    |----|----|
    | `Message` | `Update entity failure - {#ActionResults:Incident_UpdateEntity/error}` |
    | `Title` | `Update Incident` |

    ![MDK](images/3.3.12.png) 

    >`Incident_UpdateEntity` é o valor do Resultado da Ação do Incident_UpdateEntity.action. Esta referência é usada para passar os resultados para ações subsequentes na cadeia. Essas ações podem fazer referência ao resultado da ação, conforme necessário. Neste caso, se houver uma falha, você acessa a propriedade de erro do resultado da ação para exibir a mensagem de falha OData. <br/> Esta é a sintaxe padrão do Caminho de Destino de Vinculação (também chamada de Caminho de Destino Dinâmico) usada quando você precisa incluir uma vinculação com outras ligações ou dentro de uma string como usada na mensagem aqui. <br/> Você pode excluir a expressão acima e pode apenas exibir uma mensagem genérica.

14. Após a conclusão bem-sucedida do `Incident_UpdateEntity.action`, uma ação do OData Upload Stream deve ser iniciada para salvar a Imagem do Dispositivo e a Assinatura do Cliente. <br/> Clique no ícone `Create a rule/action` para a **Success Action**.

    ![MDK](images/3.3.13.png) 

15. Selecione **Object Type** como **Action** e `Folders` como `/MDKApp/Actions/Incident`. Clique em **OK**.

    ![MDK](images/3.3.5.png)   

16. No menu suspenso de pesquisa **Category**, escolha **Data** | clique em **Media** | clique em **Next**.

    ![MDK](images/3.3.14.png)  

17. Na etapa **Base Information**, forneça as seguintes informações e clique em **Next**.

    | Propriedade | Valor |
    |----|----|
    | `Name`| `Incident_UploadStream` |
    | `Type` | Selecionar `UploadStream` no menu suspenso |
    | `Service`| Selecionar `IncidentManagement.service` no menu suspenso |
    | `EntitySet`| Selecionar `Incident` no menu suspenso |
    | `ReadLink`| Clique no ícone do link para abrir o Navegador de Objetos e clique duas vezes em `readLink` |

    ![MDK](images/3.3.15.png) 

18.  Na etapa **Property and Update Links**, selecione a propriedade `DeviceImage` e clique no **link icon** para abrir o navegador de objetos.
    -  Altere o menu suspenso no Navegador de Objetos para `Control & ClientData`, selecione o botão de opção **Current Page**.
    - Na caixa de pesquisa, comece a digitar `image`. A lista será filtrada para exibir os valores correspondentes. Clique duas vezes na entrada **Value (Value)** no campo `FCDeviceImage` e clique em **OK** para definir a vinculação.

        ![MDK](images/3.3.16.gif) 

19. Selecione a propriedade `ResolutionSignatureImage` e clique no **link icon** para abrir o navegador de objetos.
    -  Altere o menu suspenso no Navegador de Objetos para `Control & ClientData`, selecione o botão de opção **Current Page**.
    - Na caixa de pesquisa, comece a digitar `signature`. A lista será filtrada para exibir os valores correspondentes. Clique duas vezes na entrada **Value (Value)** no campo `FCCustomerSignature` e clique em **OK** para definir a vinculação.
    
        ![MDK](images/3.3.17.png) 

20. Clique em Concluir. O editor de ação será aberto com o `Incident_UploadStream.action` carregado.

21. Quando o `Incident_UploadStream.action` for executado, você pode querer exibir uma mensagem de sucesso e fechar a página. Quando falhar por algum motivo, você pode querer exibir um erro. <br/> No `Incident_UploadStream.action`, role para baixo e expanda a seção **Common Action Properties**. Clique no ícone de link para a propriedade `Success Action` para abrir o Navegador de Objetos e vincular a uma ação de mensagem existente `GenericToastMessage.action`.

    ![MDK](images/3.3.18.png) 

22. Vamos substituir as propriedades desta ação e definir algumas informações específicas sobre o manuseio de `Incident_UploadStream.action`. Clique no ícone de substituição para abrir o assistente de propriedades de ação de substituição. 

    ![MDK](images/3.3.19.png) 

23. Forneça as seguintes informações e clique em **OK**.

    | Propriedade | Valor |
    |----|----|
    | `Message` | `Entity updated` |
    | `Duration` | `2` |
    | `Animated` | Selecione `true` na opção suspensa |
    | `Common Action Properties` &rarr; `Success Action` | Clique no ícone do link e vincule-o a `CloseModalPage_Complete.action` |

    ![MDK](images/3.3.20.png) 

24. Quando este `Incident_UploadStream.action` falha devido a algum motivo, você pode querer exibir um erro. Clique no ícone do link para a propriedade `Failure Action` para abrir o Navegador de Objetos e vincular a uma ação de mensagem existente `GenericMessageBox.action`.

    ![MDK](images/3.3.21.png) 

25. Vamos substituir as propriedades desta ação e definir algumas informações específicas quando `Incident_UploadStream.action` falha. Clique no ícone de substituição para abrir o assistente de propriedades de ação de substituição. 

    ![MDK](images/3.3.22.png) 

26. Forneça as seguintes informações e clique em **OK**.

    | Propriedade | Valor |
    |----|----|
    | `Message` | `Upload Stream failure - {#ActionResults:Incident_UploadStream/error}` |
    | `Title` | `Upload Stream` |

    ![MDK](images/3.3.23.png) 

### Exercício 3.4 - Valide as Entradas antes de salvar a Entidade Incidente

Certifique-se de que o técnico só possa salvar uma entidade incidente depois de fornecer todas as entradas necessárias. Se não o fizerem, mostre a eles uma mensagem apropriada. Por exemplo, se eles tentarem enviar um registro com um status vazio, sem ID de dispositivo, mais de uma imagem de dispositivo ou sem uma assinatura do cliente, eles devem ser solicitados com uma mensagem de aviso.

Para conseguir isso, você precisará implementar uma lógica de negócios que valide os valores de entrada e essa lógica precisa ser vinculada ao item `Save` ActionBar no `Incident_Edit.page`.

1. Em `Incident_Edit.page`, selecione o item `Save` ActionBar e navegue até a guia **Events**. Limpe a vinculação existente para a propriedade `OnPress`.

    ![MDK](images/3.4.8.png) 

2. Clique no ícone de três pontos para a propriedade `OnPress` e selecione `Create a rule/action`.

    ![MDK](images/3.4.9.png) 

3. Selecione **Object Type** como **Rule** e **Folders** como `/MDKApp/Rules/Incident`. Clique em **OK**.

    ![MDK](images/3.1.10.png)


5. Forneça o nome `Incident_ValidateEdit` à sua regra e clique em **Finish**.

    ![MDK](images/3.4.10.png)  

6. Substitua o snippet gerado pelo seguinte código.

    ```JavaScript
    /**
    * Describe this function...
    * @param {IClientAPI} clientAPI
    */
    export default function Incident_ValidateEdit(clientAPI) {
        var attachments = clientAPI.getPageProxy().getControl('SectionedTable0').getSection('SectionFormCell0').getControl('FCDeviceImage').getValue();
        var statusPicker = clientAPI.getPageProxy().getControl('SectionedTable0').getSection('SectionFormCell0').getControl('FCStatus').getValue();
        var currentStatus;
        if (statusPicker.length > 0 && statusPicker[0].ReturnValue) {
            currentStatus = statusPicker[0].ReturnValue;
        }
        var customerSignature = clientAPI.getPageProxy().getControl('SectionedTable0').getSection('SectionFormCell0').getControl('FCCustomerSignature').getValue();
        var deviceID = clientAPI.getPageProxy().getControl('SectionedTable0').getSection('SectionFormCell0').getControl('FCDeviceID').getValue();
        if (!currentStatus) {
            return clientAPI.executeAction({
                "Name": '/MDKApp/Actions/GenericMessageBox.action',
                "Properties": {
                    "Message": "Please select status",
                    "Title": "Validation"
                }
            })
        }
        if (!deviceID) {
            return clientAPI.executeAction({
                "Name": '/MDKApp/Actions/GenericMessageBox.action',
                "Properties": {
                    "Message": "Device ID is required",
                    "Title": "Validation"
                }
            })
        }
        if (currentStatus === "Closed" && attachments.length !== 1) {
            return clientAPI.executeAction({
                "Name": '/MDKApp/Actions/GenericMessageBox.action',
                "Properties": {
                    "Message": attachments.length < 1 ? "Please add 1 device image" : "Max. 1 image allowed for the device",
                    "Title": "Validation"
                }
            })
        }
        if (currentStatus === "Closed" && !customerSignature) {
            return clientAPI.executeAction({
                "Name": '/MDKApp/Actions/GenericMessageBox.action',
                "Properties": {
                    "Message": "Customer Signature is required",
                    "Title": "Validation"
                }
            })
        }
        return clientAPI.executeAction({
            "Name": '/MDKApp/Actions/Incident/Incident_UpdateEntity.action',
            "Properties": {
                "OnSuccess": currentStatus === "Closed" ? "/MDKApp/Actions/Incident/Incident_UploadStream.action" : "/MDKApp/Actions/CloseModalPage_Complete.action"
            }
        })
    }
    ```

### Exercício 3.5 - Navegue até a página de Edição de Incidentes

Para navegar da página Incident Detail para uma nova página para modificar informações do incidente, você adicionará um item da barra de ação na página Incident Detail e o vinculará a uma ação de navegação. Quando o item da barra de ação é pressionado por um técnico, ele abrirá o `Incident_Edit.page`.

1. Em `Incident_Detail.page`, arraste e solte um **Action Bar Item** para o canto superior direito da barra de ação, colocando-o antes do item `View Image` existente.

    ![MDK](images/3.4.1.png)    

2. No painel Propriedades, forneça as seguintes informações:     

    | Propriedade | Valor |
    |----|----|
    | `Caption` | `Edit` |
    | `SystemItem` | Clique no **link icon** para abrir o Navegador de Objetos, clique duas vezes no tipo **Edit** e clique em **OK**. |

    ![MDK](images/3.4.2.png)    

3. O botão Editar só deve ser visível para incidentes que estejam no estado `New` ou `In Process`. Se o status de um incidente for `Closed`, o técnico não deve ter nenhuma opção para alterar os detalhes. Esse comportamento deve ser integrado à lógica do seu aplicativo. <br/> Clique no ícone `Create a rule` para a propriedade **Visible** do item Editar barra de ação.

    ![MDK](images/3.4.3.png)   

4. Selecione **Object Type** como **Rule** e **Folders** como `/MDKApp/Rules/Incident`. Clique em **OK**.

    ![MDK](images/3.1.10.png)

5. Forneça o nome `EditOptionVisibility` à sua regra e clique em **Finish**.

    ![MDK](images/3.4.4.png)  

6. Substitua o snippet gerado pelo seguinte código.

    ```JavaScript
    /**
    * Describe this function...
    * @param {IClientAPI} clientAPI
    */
    export default function EditOptionVisibility(clientAPI) {
        let currentStatus = clientAPI.binding.Status;
        if (currentStatus == "Closed") {
            return false;
        }
        else {
            return true;
        }
    }
    ```

7. Volte para o `Incident_Detail.page`.

8. Navegue até a guia **Events**. Clique no ícone de três pontos para a propriedade `OnPress` e selecione `Create a rule/action`.

    ![MDK](images/3.4.5.png)     

9. Defina a seleção para o `Object Type` como **Action** e escolha o caminho `Folders` como `/MDKApp/Actions/Incident`.

    ![MDK](images/3.3.5.png)   

10. No menu suspenso de pesquisa **Category**, escolha **UI** | clique em **Navigation** | clique em **Next**. 

    ![MDK](images/3.4.6.png)  

11. Forneça as seguintes informações e clique em **Finish** para concluir o processo de criação da ação.

    | Propriedade | Valor |
    |----|----|
    | `Name`| `NavToIncident_Edit` |
    | `PageToOpen` | Selecione `Incident_Edit.page` no menu suspenso |
    | `ModalPage`| Selecione `true` no menu suspenso |
    | `ModalPageFullScreen`| Selecione `false` no menu suspenso |

    ![MDK](images/3.4.7.png)  

    >- `ModalPage:` Isso indica se uma página é modal.
    >- `ModalPageFullScreen:` Em um formato de telefone, a página modal será exibida como uma tela modal de página inteira. Em um fator de forma de tablet, o modal parcial será pop-up e não cobrirá a página inteira ao definir seu valor como falso.

### Exercício 3.6 - Reimplantar o aplicativo

Agora que você criou a página Editar, é hora de implantar as alterações para ver o resultado.

1. Clique com o botão direito do mouse no arquivo `Application.app` no painel do explorador do projeto, escolha `MDK:Deploy` e selecione o destino de implantação como **Mobile Services**. Quando a implantação for bem-sucedida, uma mensagem de sucesso aparecerá. Se a implantação ficar presa, recarregue a página e tente novamente.

    ![MDK](images/3.5.1.png)
    ![MDK](images/3.5.2.png)

    >Alternativamente, você pode selecionar `MDK: Redeploy` na paleta de comandos. Para acessar a paleta de comandos, vá para o menu Exibir e escolha Paleta de Comandos, ou pressione Command+Shift+P em um Mac ou Ctrl+Shift+P em uma máquina Windows. Este comando executará a última implantação.
    
    >![MDK](images/3.5.3.png)

       

### Exercício 3.7 - Atualize o aplicativo MDK com novos metadados

| Steps&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Android | iOS&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|---|---|---|
| 1. Toque na opção **Check for Updates** no `User menu` na página de Incidentes.| ![MDK](images/3.6.1.png)| ![MDK](images/3.6.2.png)|
| 2. Você verá uma `New Version Available!` pop-up. Toque em **Now**.| ![MDK](images/3.6.3.png)| ![MDK](images/3.6.4.png)|
| 3. Navegue até a página Incident detail. <br/><br/> Se o status do incidente já estiver `Closed`, você não verá a opção **Edit** na barra de ação. Em vez disso, você terá a capacidade de abrir a imagem do dispositivo de trabalho. <br/><br/>  Se o status de um incidente for `New` ou `In Process`, você verá a opção **Edit**.| ![MDK](images/3.6.5.gif)| ![MDK](images/3.6.6.gif)|
| 4. Atualize um Incidente. <br/><br/> você pode atualizar o status de `New` para `In Process` ou `Closed` ou de `In Process` para `Closed`. <br/><br/> Ao atualizá-lo para `In Process`, você poderá inserir o ID do dispositivo com defeito, digitando-o manualmente ou digitalizando o código de barras do dispositivo, mas não terá opções para fazer upload de uma imagem do dispositivo ou capturar a assinatura do cliente. <br/><br/> Ao atualizá-lo para `Closed`, você deve ser capaz de inserir o ID do dispositivo com defeito, digitando-o manualmente ou digitalizando o código de barras do dispositivo, e você também deve ver as opções para fazer upload de uma imagem do dispositivo e capturar a assinatura do cliente. <br/><br/> Para digitalizar o código de barras do dispositivo, você pode usar a imagem abaixo. <br/><br/><br/><br/> ![MDK](images/3.6.9.png) | ![MDK](images/3.6.7.gif)| ![MDK](images/3.6.8.gif)|
| 5. Como este é um aplicativo off-line, as alterações são salvas na loja local, que precisa ser enviada ou carregada no back-end explicitamente. <br/><br/> Navegue até a página da lista de incidentes, puxe para baixo na lista de incidentes para fazer upload de alterações para o back-end, OU clique no ícone do menu do usuário e selecione **Sync Changes**. Você deve ver uma mensagem `Sync Completed` exibida. | ![MDK](images/3.6.10.gif) | ![MDK](images/3.6.11.gif)|

## Resumo

Agora você modificou com sucesso uma entidade incidente.

## Navegação

| Anterior | Próximo |
|---|---|
| [Exercise 2](../ex2/README.md) | [Exercise 4](../ex4/README.md) |
