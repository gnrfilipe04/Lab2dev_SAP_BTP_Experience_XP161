# Exercício 4 - Integrar com o SAP Mobile Start

## Tempo estimado

:clock4: 10 minutos

## Objetivo

O aplicativo SAP Mobile Start é o seu ponto de entrada nativo para o universo móvel da SAP. Descubra como os aplicativos personalizados aparecem no SAP Mobile Start e podem ser lançados. Experimente o SAP Mobile Start no seu próprio dispositivo móvel.

> **Observação:** Devido ao tempo limitado no workshop prático, o conteúdo necessário no SAP Build Work Zone, a edição padrão foi pré-criada para esta sessão. Você pode conferir outros recursos para saber mais sobre como expor esse conteúdo ao SAP Mobile Start por conta própria.

| Número do Exercício | Título                                                 |
|-------------------|-------------------------------------------------------|
| [Exercício 4.1](#exercício-41---acesso-ao-work-zone-standard-edition) | Acesso ao Work Zone, standard edition |
| [Exercício 4.2](#exercício-42---configure-a-aplicação-sap-mobile-start) | Configure a aplicação SAP Mobile Start |

### Exercício 4.1 - Acesso ao Work Zone, standard edition

1. Abra o [Site Manager](https://ad162-egls99xc.dt.launchpad.cfapps.eu10.hana.ondemand.com/sites#Site-Directory?sap-app-origin-hint=) do SAP Build Work Zone, standard edition no seu navegador.

   >**Observação:** Como este ambiente é compartilhado entre todos os participantes desta sessão, não altere ou exclua o conteúdo. Por favor, use seu próprio ambiente, por exemplo, usando o [free tier of SAP BTP](https://discovery-center.cloud.sap/serviceCatalog/sap-build-work-zone-standard-edition/?region=all&tab=feature).

2. Você pode encontrar um Site pré-criado `AD162` na visão geral do Site Diretory. Clique no ícone **gear** para verificar os detalhes.

   <p align="center">
      <img src="./images/img-4-1-2.png" width="100%" />
   </p>

3. No lado direito, você pode observar o conteúdo de um sistema S/4HANA para a função comercial **Purchaser** que foi adicionada por seus instrutores para este curso.

   <p align="center">
      <img src="./images/img-4-1-3.png" width="100%" />
   </p>

4. Volte e navegue agora para o **Content Manager** no lado esquerdo do Gerenciador de Sites.

   <p align="center">
      <img src="./images/img-4-1-4.png" width="100%" />
   </p>

5. Aqui você pode observar, dois aplicativos nativos foram criados para representar seu aplicativo nativo Pro-code para iOS e Android.

   <p align="center">
      <img src="./images/img-4-1-5.png" width="100%" />
   </p>

6. Volte para o **Site Directory** e inicie o Site preparado usando o ícone **launch**

   <p align="center">
      <img src="./images/img-4-1-6.png" width="100%" />
   </p>

7. No site do Work Zone, você já pode ver alguns aplicativos de negócios no seu navegador. Vá para **Profile** e abra as **Settings** no canto superior direito.

   <p align="center">
      <img src="./images/img-4-1-7.png" width="100%" />
   </p>

8. Navegue até a seção **SAP Mobile Start Application** e selecione **Register** para mostrar o QR-Code que pode ser usado para integração.
   
   <p align="center">
      <img src="./images/img-4-1-8.png" width="100%" />
   </p>

   > Certifique-se de ter escolhido a plataforma correta iOS / Android acima.

### Exercício 4.2 - Configure a aplicação SAP Mobile Start

| Passos&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Android | iOS&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|
| --- | --- | --- |
| 1. Abra **SAP Mobile Start** no seu celular. Se você ainda não o tem, instale-o na App Store ou no Google Play. Você pode usar os QRs de instalação para encontrar o aplicativo rapidamente. | ![Android](images/img-4-2-1-and.png) | ![iOS](images/img-4-2-1-ios.png) |
| 2. Depois de concordar com o contrato de licença do usuário final e a política de privacidade, toque no botão **Scan / Get Started** no SAP Mobile Start. | ![Android](images/img-4-2-2-and.jpeg) | ![iOS](images/img-4-2-2-ios.png) |
| 3. Você será solicitado a fazer login com suas credenciais fornecidas. Use o endereço de e-mail no formato `ad162-###@education.cloud.sap` (substituindo `###` pelo seu número de 3 dígitos) e a senha. | N/A | N/A |
| 4. Toque na guia **Apps** na barra de guias inferior. Você pode ver o aplicativo que integra nosso aplicativo móvel criado neste curso na seção **AD162 Apps**| ![Android](images/img-4-2-4-and.jpeg) | ![iOS](images/img-4-2-4-ios.jpeg) |
| 5. Tocar nele iniciará o **Mobile Services Client** para experimentar seu aplicativo. Se ele ainda não estiver instalado, você será redirecionado para a App Store ou o Google Play. | N/A | N/A |


## Resumo

Você aprendeu como o conteúdo integrado ao SAP Build Work Zone, edição padrão, aparecerá no SAP Mobile Start. Você experimentou o lançamento de um aplicativo nativo do Mobile Start e como outro exemplo de conteúdo de negócios da S/4HANA pode construir a base para o ponto de entrada nativo para o universo móvel da SAP. Esse conteúdo pode vir de Provedores de Conteúdo como S/4HANA ou ser personalizado e integrado para atender às suas necessidades.

Saiba mais sobre o SAP Mobile Start e como expor conteúdo nos dois workshops práticos a seguir do TechEd 2023:

- DT162 - Saiba como configurar e configurar o SAP Mobile Start com o SAP S/4HANA
- XP161 - Desenvolva Aplicativos Móveis com o SAP Build Apps, Acesse-os via SAP Mobile Start

## Navegação

| Anterior | Próximo |
| --- | --- |
| [Exercise 3](../ex3/README.md) | [Conclusion](../../Conclusion.md) |
