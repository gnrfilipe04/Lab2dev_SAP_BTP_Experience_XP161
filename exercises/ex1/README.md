# Exercício 1 – Execute o aplicativo inicial em seu dispositivo

## Tempo estimado

:clock4: 10 minutos

## Objetivo


Neste exercício, você executará um aplicativo SAP Mobile Development Kit (MDK) inicial em seu dispositivo.

| Número do Exercício | Título |
| --- | --- |
| [Exercício 1.1](#exercise-11---launch-the-sap-business-application-studio-for-mdk-development) | Lançar o SAP Business Application Studio para desenvolvimento MDK |
| [Exercício 1.2](#exercise-12---change-the-workspace-to-the-project-explorer) | Mude o espaço de trabalho para o Project Explorer |
| [Exercício 1.3](#exercise-13---clone-the-mdk-project) | Clone o projeto MDK |
| [Exercício 1.4](#exercise-14---provide-your-assigned-service-worker-id-to-filter-related-incidents) | Forneça seu ID de Service Worker atribuído para filtrar incidentes relacionados |
| [Exercício 1.5](#exercise-15---deploy-the-application) | Implantar o aplicativo |
| [Exercício 1.6](#exercise-16---display-the-qr-code-for-onboarding-the-mobile-app) | Exibir o QR Code para integração do aplicativo móvel |
| [Exercício 1.7](#exercise-17---run-the-app) | Iniciar a aplicação |

### Exercício 1.1 - Lançar o SAP Business Application Studio para desenvolvimento MDK 

1. Inicie o [SAP Business Application Studio](https://ad162-egls99xc.eu10cf.applicationstudio.cloud.sap/index.html) no seu browser Google Chrome.

    >Cancele a seleção do certificado do usuário se um prompt aparecer no navegador.

2. Forneça as credenciais de login que foram compartilhadas com você durante a sessão. 

    ![MDK](images/1.1.1.png)

3. Se o seu espaço de desenvolvimento estiver no estado `STOPPED`, inicie-o clicando no ícone de execução.

    ![MDK](images/1.1.2.png)  

    Quando estiver no estado `RUNNING`, abra-o clicando no nome.    

    ![MDK](images/1.1.3.png) 

### Exercício 1.2 - Mude o espaço de trabalho para o Project Explorer

Agora você mudará seu espaço de trabalho para a pasta `projects`.

1. Clique no ícone do Explorer e selecione **Open folder**.

    ![MDK](images/1.2.1.png) 

2. Se ainda não estiver selecionado, escolha a pasta `projects` e clique em **OK**.

    ![MDK](images/1.2.2.png) 

    A página do SAP Business Application Studio será recarregada e a pasta de projetos será aberta como espaço de trabalho.

    ![MDK](images/1.2.3.png)      

### Exercício 1.3 - Clone o projeto MDK

Antes de iniciar os exercícios da sessão, você primeiro clonará o repositório git na área de trabalho do Business Application Studio.

1. Copie o URL abaixo.

    ```URL
    https://github.com/jitendrakansal/MDKApp.git
    ```

2. Na página `Get Started`, clique em `Clone from Git`.

    ![MDK](images/1.3.12.png) 

3. No campo `Provide repository URL`, cole o URL e pressione **Enter**.

    ![MDK](images/1.3.13.png) 

4. Clique em **Cancel**. O repositório clonado será adicionado ao explorador de projetos.

    ![MDK](images/1.3.14.png)  

### Exercício 1.4 - Forneça seu ID de Service Worker atribuído para filtrar incidentes relacionados

1. Expanda o projeto `MDKApp` e navegue até `Pages` &rarr; `Incident`. Clique com o botão direito em `Incident_List.page` e abra com **Text Editor**.

    ![MDK](images/1.3.10.gif)   

2. Substitua `workerID` por um valor de ID do Service Worker compartilhado com você e feche a página clicando no sinal `x`.

    ![MDK](images/1.3.11.png)  

### Exercício 1.5 - Implantar o aplicativo

Agora você implantará as definições de aplicativo no SAP Mobile Services.

1. Clique com o botão direito em `Application.app` e selecione **MDK: Deploy**.

    ![MDK](images/1.4.22.png) 

2. Se você não tiver uma sessão CF ativa, poderá ser solicitado que você faça login no Cloud Foundry. Se solicitado, clique em **Login** para continuar. Caso contrário, prossiga diretamente para a etapa 8.

    ![MDK](images/1.3.3.png)

3. Escolha **Senha SSO** como seu método de autenticação e clique no hiperlink destacado. Isso abrirá uma nova página do navegador.

    ![MDK](images/1.3.4.png)

4. Uma nova aba será aberta no seu navegador. Insira `tdct3ched1-platform` como a chave de origem para o IdP personalizado e clique em **Sign in with alternative identity provider**.

    ![MDK](images/1.3.5.png)

    > Cancele a seleção do certificado se for solicitado no navegador.

5. Copie o código de autenticação temporário.

    ![MDK](images/1.3.6.png)

6. Volte para a página SAP Business Application Studio. Cole o código copiado no campo denominado **Enter your SSO Passcode** e clique em **Enter**.

    ![MDK](images/1.3.7.png)

7. Agora você está conectado ao Cloud Foundry. Defina o destino do Cloud Foundry escolhendo a organização e o espaço apropriados no menu suspenso e clique em **Apply**. Depois que o destino do Cloud Foundry for definido, a guia `Cloud Foundry Sign in` será fechada automaticamente.

    ![MDK](images/1.3.8.png)
    
8. Selecione o destino de implantação como **Mobile services**.

    ![MDK](images/1.4.23.png) 

9. Selecione **Standard** no cenário do Mobile Services.

    ![MDK](images/1.4.24.png)  

10. Selecione o ID do aplicativo de serviços móveis `sap.mobile.user.xyz` atribuído a você.

    ![MDK](images/1.4.25.png) 

11. Se você quiser habilitar a origem para depuração do pacote implantado, escolha **Yes**.

    ![MDK](images/1.4.26.png) 

    Você deverá ver a mensagem **Deploy to Mobile Services successfully!**.

    ![MDK](images/1.4.27.png) 

### Exercício 1.6 - Exibir o QR Code para integração do aplicativo móvel

Agora você executará o aplicativo inicial no cliente móvel instalado em seu dispositivo, digitalizando o QR Code integrado. 

1. Expanda o projeto `MDKApp`, clique em `Application.app` para abri-lo no MDK Application Editor e clique no ícone **Application QR Code**.

    ![MDK](images/1.3.1.png)


2. O QR Code de integração agora é exibido. Deixe a caixa de diálogo Integração aberta enquanto avança para a próxima etapa.

    ![MDK](images/1.3.9.png)

### Exercício 1.7 - Execute o aplicativo

| Steps&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Android | iOS&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  |
| --- | --- | --- |
| 1. Inicie o aplicativo **`Mobile Svcs`** em seu dispositivo móvel. Toque em **Agree** em `End User License Agreement and Privacy Statement`. | ![MDK](images/1.4.1.png) | ![MDK](images/1.4.2.png) |
| 2. Toque em **Scan** para iniciar a câmera do dispositivo para digitalizar o código QR integrado e conceder permissão para acessar a câmera. Observe que se você já possui o cliente MDK integrado, toque em *Get Started* e *Scan new QR Code* para continuar. | ![MDK](images/1.4.3.png) | ![MDK](images/1.4.4.png) |
| 3. Assim que a verificação for bem-sucedida, toque em **Continue**. | ![MDK](images/1.4.5.png) | ![MDK](images/1.4.6.png) |
| 4. Use as credenciais de login que foram compartilhadas com você durante a sessão para fazer login no SAP BTP. | ![MDK](images/1.4.7.png) | ![MDK](images/1.4.8.png) |
| 5. Crie uma senha com pelo menos 5 caracteres para desbloquear o aplicativo e toque em **Next**. | ![MDK](images/1.4.9.png) | ![MDK](images/1.4.10.png) |
| 6. Confirme a senha e toque em **Done**. | ![MDK](images/1.4.11.png) | ![MDK](images/1.4.12.png) |
| 7. Você tem a opção de ativar a autenticação biométrica para acesso mais rápido aos dados do aplicativo. No iOS, toque em **Enabled** se desejar usar esse recurso. No Android, forneça suas informações biométricas. | ![MDK](images/1.4.13.png) | ![MDK](images/1.4.14.png) |
| 8. Toque em **Next**. Se quiser que seu cliente MDK envie notificações, toque em **Allow**, caso contrário, toque em **Don't Allow**. | ![MDK](images/1.4.15.png) ![MDK](images/1.4.15.1.png) | NA |
| 9. Toque em **Now** para aceitar as definições de metadados implantados. | ![MDK](images/1.4.16.png) | ![MDK](images/1.4.17.png) |
| 10. Depois de aceitar a atualização do aplicativo, a loja offline será inicializada. Você verá uma lista de incidentes atribuídos a você e um ícone de menu do usuário na página principal. O menu do usuário inclui os seguintes itens:<br/><br/>- **Sync Changes:** isso permite que você carregue quaisquer alterações locais do cliente móvel para o back-end e baixe quaisquer alterações do back-end para o cliente móvel.<br/><br/>- **Support:** Isso fornece uma maneira fácil para os usuários entrarem em contato com o suporte por meio de uma célula de contato. As informações de contato são definidas nas configurações globais.<br/><br/>- **Activity Log** A opção na página Suporte permite que o usuário ative ou desative o logon do cliente, defina o nível de log, defina categorias de rastreamento, alterne o rastreamento OData e, se habilitado no aplicativo Mobile Services, carregue os logs atuais do cliente. <br/><br/>- **Check for Updates:** Isso verifica se novos metadados foram implantados na atualização do aplicativo Mobile Services. Se novos metadados forem encontrados, eles serão baixados e solicitarão que o usuário aplique as alterações.<br/><br/>- **About:** Esta página exibe o ID do usuário/dispositivo atual, o nome do aplicativo, a versão dos metadados e as informações da versão do cliente.<br/><br/>- **Logout:** Isso redefine completamente o cliente, apagando todos os dados baixados e metadados do aplicativo, e retorna o usuário à tela do contrato de licença. | ![MDK](images/1.4.18.png) | ![MDK](images/1.4.19.png) |
| 11. Toque em qualquer um dos incidentes para navegar até a página de detalhes, onde você encontrará mais informações sobre o incidente. Você também pode acessar o endereço do cliente por meio de um aplicativo de mapas. Se o incidente estiver marcado como `closed`, estará disponível uma opção para visualizar a imagem do dispositivo com defeito. | ![MDK](images/1.4.20.gif) | ![MDK](images/1.4.21.gif) |






>After scanning and onboarding using the URL, it will be remembered. If you log out and onboard again, you'll be prompted to either continue using the current application or to scan a new QR code.

## Summary

You now have the starting application running in your MDK client.

## Navigation

|  Next |
|---|
| [Exercise 2](../ex2/README.md) |
