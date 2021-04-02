---
title: 設定自動表單轉換服務
description: 讓您的AEM實例使用Automated forms conversion服務
role: 業務從業人員、管理員
translation-type: tm+mt
source-git-commit: a9bab62fbe5ecc4b233e9bc55b9e461a5967b471
workflow-type: tm+mt
source-wordcount: '2673'
ht-degree: 6%

---


# 設定自動表單轉換服務 {#about-this-help}

本說明說明管理員如AEM何設定Automated forms conversion服務，以自動將PDF forms轉換為可調式表單。 本說明適用於貴組織的AEMIT和管理員。 提供的資訊基於以下假設：閱讀本「說明」的人熟悉下列技術：

* 安裝、配置和管理Adobe Experience Manager和AEM包，

* 使用Linux®和Microsoft® Windows®作業系統，

* 配置SMTP郵件伺服器

<!--- >[!VIDEO](https://video.tv.adobe.com/v/29267/) 

**Watch the video or read the article to configure Automated Forms Conversion service** -->

## 入門{#onboarding}

此服務可免費提供6.4AEMForms和6.AEM5Forms內部部署定期客戶和Adobe管理服務企業客戶。 您可以聯絡 Adobe Sales 團隊或您的 Adobe 代表，請求存取該服務。該服務還免費提供，作為Cloud Service客戶，AEM Forms也可以預先使用。

Adobe 為您的組織啟用存取權限，並向您指定的組織管理員提供所需的特權。 管理員可以授予組織的 AEM Forms 開發人員（使用者）存取權限以連接到該服務。 

## 必備條件 {#prerequisites}

您需要下列項目才能使用Automated forms conversion服務：

* automated forms conversion服務已為您的組織啟用
* 具有轉換服務管理員權限的Adobe ID帳戶
* 以Cloud Service作者例項AEM6.4、AEM6.5或AEM Forms的身分啟動並執行，具備最新的Service AEM Pack或最新更新。
* 屬於AEM表單——使AEM用者群組的使用者（在您的例項上）

## 設定環境 {#setuptheservice}

在使用服務之前，請準備您AEM的作者實例以連線至在Adobe雲端執行的服務。 在列出的序列中執行以下步驟，為服務準備實例：

1. [下載並安AEM裝6.4、AEM 6.5或以AEM Forms為Cloud Service板載](#aemquickstart)
1. [下載並安裝最新AEM的Service Pack](#servicepack)
1. [下載並安裝最新的AEM Forms附加套件](#downloadaemformsaddon)
1. （可選）[下載並安裝最新的連接器軟體包](#installConnectorPackage)
1. [建立自訂主題和範本](#referencepackage)

### 下載並安AEM裝6.4或AEM6.5或AEM Forms板載作為Cloud Service{#aemquickstart}


automated forms conversion服務在作者實AEM例上執行。 您需AEM要6.4、AEM6.5或AEM Forms做為Cloud Service才能設定作AEM者例項。

* 如果您沒有AEM6.4或AEM6.5啟動和執行，請從以下位置下載。 下載後AEM，如需設定作者例項的AEM指示，請參閱部署和維護](https://helpx.adobe.com/experience-manager/6-5/sites/deploying/using/deploy.html#defaultlocalinstall)。:[

   * 如果您是現有AEM客戶，請從AEM[Adobe授權網站](http://licensing.adobe.com)下載6.4或6.5。

   * 如果您是Adobe合作夥伴，請使用[Adobe合作夥伴培訓計畫](https://adobe.allegiancetech.com/cgi-bin/qwebcorporate.dll?idx=82357Q)要求AEM6.4AEM或6.5。

* 如果您將AEM Forms用作Cloud Service，請參閱到[AEM Forms作為Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/setup-environment/setup-forms-cloud-service.html?lang=en#setup-environment)和[設定本地開發環境](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/setup-environment/setup-local-development-environment.html?lang=en#setup-environment)。

### (AEM僅限6.4和AEM6.5)下載並安裝最AEM新的Service Pack {#servicepack}

下載並安裝最新AEM的Service Pack。 有關詳細說明，請參閱[AEM 6.4 Service Pack發行說明](https://helpx.adobe.com/tw/experience-manager/6-4/release-notes/sp-release-notes.html)或[AEM 6.5 Service Pack發行說明](https://helpx.adobe.com/tw/experience-manager/6-5/release-notes/sp-release-notes.html)。

### (AEM僅限6.4和AEM6.5版)下載並安裝AEM Forms附加套件{#downloadaemformsaddon}

例項AEM包含基本表單功能。 轉換服務需要AEM Forms的完整功能。 下載並安裝AEM Forms附加套件，以運用AEM Forms的所有功能。 需要軟體包才能設定並運行轉換服務。 有關詳細說明，請參閱[安裝和配置資料捕獲功能。](https://helpx.adobe.com/experience-manager/6-5/forms/using/installing-configuring-aem-forms-osgi.html)

>[!NOTE]
> 確保在安裝附加軟體包後執行強制安裝後配置。


<!-- ### (Optional) Download and install connector package  {#installConnectorPackage}

The connector package provides early access to the [Auto-detect logical sections](convert-existing-forms-to-adaptive-forms.md#run-the-conversion) features and improvements delivered in release AFC-2020.03.1. Do not install the package if you do not require feature and improvements delivered in AFC-2020.03.1.  You can [download the connector package from AEM Package Share](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/featurepack/AFCS-Connector-2020.03.1). -->


### 建立自訂主題和範本{#referencepackage}

如果您在AEM[生AEM產模式](https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/production-ready.html)（nosamplecontent執行模式）中啟動6.4或6.5，則不安裝參考軟體包。 參考套件包含範例主題和範本。 automated forms conversion服務至少需要一個主題和一個範本，才能將PDF表單轉換為最適化表單。 建立您自己的自訂主題和範本，並指向[service configuration](#configure-the-cloud-service)使用服務前，使用自訂範本和主題。

您也可以下載並安裝[AEM Forms參考資產](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)套件至您的作者實例。 它會建立一些參考主題和範本。

## 設定服務 {#configure-the-service}

在您繼續設定服務並連線您的本機執行個體與Adobe雲上執行的服務之前，請先瞭解連線至服務所需的角色和權限。 本服務使用兩種不同的角色類型：管理員和開發人員：

* **管理員**:管理員負責管理組織的Adobe軟體和服務。管理員授與其組織中開發人員的存取權，以連線至在Adobe雲端執行的Automated forms conversion服務。 為組織布建管理員時，管理員會收到標題為&#x200B;**[!UICONTROL 'You now have administrator rights to manage Adobe software and services for your organization']**&#x200B;的電子郵件。 如果您是管理員，請檢查郵箱中是否有前述標題的電子郵件，然後繼續[授予您組織開發人員的存取權。](#adduseranddevs)

![管理員存取權授與電子郵件](assets/admin-console-adobe-io-access-grantedx75.png)

* **開發人員**:開發人員會將本機AEM Forms作者例項連結至在Adobe雲端執行的Automated forms conversion服務。當管理員授與開發人員連線至Automated forms conversion服務的權限時，您現在可以存取「您」標題的電子郵件會傳送給開發人員，以管理您組織的AdobeAPI整合。 如果您是開發人員，請檢查郵箱中是否有前述標題的電子郵件，然後繼續[將您的本AEM地實例連接至Adobe雲上的Automated forms conversion服務。](#connectafcadobeio)

![開發人員存取授權電子郵件](assets/email-developer-accessx94.png)

### (僅適用於AEM6.4和AEM6.5的管理員)授與貴組織開發人員的存取權{#adduseranddevs}

在Adobe為您的組織啟用存取權並為管理員提供必要的權限後，管理員可以登入Admin Console（下面的詳細說明）、建立描述檔，以及將開發人員新增至描述檔。 開發人員可將AEM Forms的本機執行個體連接至Adobe雲的Automated forms conversion服務。

開發人員是指定用來執行轉換服務的組織成員。 只有新增至AdobeAutomated forms conversion服務設定檔的開發人員才有權使用Automated forms conversion服務。 執行下列步驟以建立描述檔並新增開發人員至描述檔。 至少需要一個描述檔才能授予貴組織開發人員必要的存取權：

1. 登入[Admin Console](https://adminconsole.adobe.com/)。 使用已設定的&#x200B;**Adobe ID**&#x200B;管理員，使用Automated forms conversion服務登錄。 請勿使用任何其他ID或Federated ID登入。
1. 按一下&#x200B;**[!UICONTROL Automated Forms Conversion]**&#x200B;選項。
1. 按一下&#x200B;**[!UICONTROL Products]**&#x200B;頁籤中的&#x200B;**[!UICONTROL New Profile]**。
1. 為配置檔案指定&#x200B;**[!UICONTROL Name]**、**[!UICONTROL Display Name]**&#x200B;和&#x200B;**[!UICONTROL Description]**。 按一下 **[!UICONTROL Done]**. 會建立描述檔。

   ![指定新描述檔的詳細資訊。](assets/create-new-profile-details.png)

1. 將開發人員新增至設定檔。 若要新增開發人員：
   1. 在[Admin Console](https://adminconsole.adobe.com/enterprise)中，導航至「概述」頁籤。
   1. 按一下所需產品卡上的&#x200B;**[!UICONTROL Assign Developers]**。
   1. 輸入開發人員的電子郵件地址，或者輸入名字和姓氏。
   1. 選擇產品設定檔。 點選&#x200B;**[!UICONTROL Save]**。

對所有使用者重複上述步驟。 如需有關新增開發人員的詳細資訊，請參閱[管理開發人員](https://helpx.adobe.com/enterprise/using/manage-developers.html)。

一旦管理員將開發人員新增至Adobe I/O設定檔，開發人員就會收到電子郵件通知。 在收到電子郵件後，開發人員可繼續[連接本機AEM Forms實例與Adobe雲上的Automated forms conversion服務。](#connectafcadobeio)

### （僅限開發人員）將您當地的AEM Forms實例連接至Adobe雲{#connectafcadobeio}上的Automated forms conversion服務

在管理員提供您開發人員存取權後，您就可以將您的本機AEM Forms例項連接至在Adobe雲端執行的Automated forms conversion服務。 在所列順序中執行以下步驟，將您的AEM Forms實例連接到服務：

* [設定電子郵件通知](configure-service.md#configureemailnotification)
* [新增使用者至表單使用者群組](#adduserstousergroup)
* [取得公開憑證](#obtainpubliccertificates)
* [在Adobe開發人員主控台上設定服務API](#createintegration)
* [設定雲端服務](configure-service.md#configure-the-cloud-service)

#### 設定電子郵件通知{#configureemailnotification}

automated forms conversion服務使用Day CQ郵件服務來傳送電子郵件通知。 這些電子郵件通知包含有關成功或失敗轉換的資訊。 如果您選擇不接收通知，請跳過這些步驟。 執行以下步驟來配置Day CQ Mail服務：

* 對AEM6.4Forms或AEM6.5Forms:

   1. 前往位AEM於`http://localhost:4502/system/console/configMgr`的配置管理器
   1. 開啟Day CQ Mail Service設定。 指定&#x200B;**[!UICONTROL SMTP server host name]**、**[!UICONTROL SMTP server port]**&#x200B;和&#x200B;**[!UICONTROL From address]**&#x200B;欄位的值。 按一下 **[!UICONTROL Save]**.

      有關SMTP伺服器的主機名和埠的資訊，請與電子郵件服務提供商或IT管理員聯繫。 您可以在from欄位中使用任何有效的電子郵件地址。 例如，notification@example.com或donotreply@example.com。

   1. 開啟&#x200B;**[!UICONTROL Day CQ Link Externalizer]**&#x200B;配置。 在&#x200B;**[!UICONTROL Domains]**&#x200B;欄位中，指定本機、作者和發佈例項的實際主機名稱或IP位址和埠號。 按一下 **[!UICONTROL Save]**.

* 對於作為Cloud Service的AEM Forms,[記錄支援票證以啟用電子郵件服務](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#sending-email)。

#### 將用戶添加到表單用戶組{#adduserstousergroup}

在指定執行服務之使用者的個人檔案AEM中指定電子郵件地址。 確保用戶是[forms user](https://helpx.adobe.com/experience-manager/6-4/forms/using/forms-groups-privileges-tasks.html)組的成員。 電子郵件會傳送至執行轉換之使用者的電子郵件地址。 要指定用戶的電子郵件地址並將用戶添加到表單用戶組，請執行以下操作：

1. 以管理員身分登入您的AEM Forms作AEM者例項。 使用您的本AEM機認證登入。 請勿使用Adobe ID登入。 點選&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Users]**。

1. 選擇指定用於運行轉換服務的用戶，然後點選&#x200B;**[!UICONTROL Properties]**。 此時將開啟「編輯用戶設定」頁。
1. 在&#x200B;**[!UICONTROL Email]**&#x200B;欄位中指定電子郵件地址，然後點選&#x200B;**[!UICONTROL Save]**。 當轉換成功或失敗時，這些電子郵件會傳送至指定的電子郵件地址。
1. 點選&#x200B;**群組**&#x200B;標籤。 在「選擇組」頁籤中，鍵入並選擇&#x200B;**forms-users**&#x200B;組。 點選&#x200B;**儲存並關閉**。 使用者現在是表單使用者群組的成員。

#### (僅AEM適用於6.4AEM和6.5)取得公共憑證{#obtainpubliccertificates}

公開憑證可讓您在Adobe I/O時驗證個人檔案。

1. 登入您的AEM Forms作者實例。 導航到 **[!UICONTROL Tools]**> **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**. 點選&#x200B;**[!UICONTROL Create]**。 此時將顯示&#x200B;**[!UICONTROL Adobe IMS Technical Account Configuration]**&#x200B;頁。

   ![「AdobeIMS技術帳戶配置」頁](assets/adobe-ims-technical-account-configuration.png)

1. 在雲端解決方案中選取&#x200B;**[!UICONTROL Automated Forms Conversion Service]**。

1. 選中&#x200B;**[!UICONTROL Create new certificate]**&#x200B;複選框並指定別名。 別名的作用是對話方塊的名稱。點選&#x200B;**[!UICONTROL Create certificate]**。 對話方塊隨即顯示。按一下 **[!UICONTROL OK]**. 將建立證書。

1. 點選&#x200B;**[!UICONTROL Download Public Key]**&#x200B;並將&#x200B;*AEM-Adobe-IMS.crt*&#x200B;憑證檔案儲存在您的電腦上。 憑證檔案用於[在Adobe開發人員主控台(Developer Console)上設定服務API。 ](#createintegration)點選&#x200B;**[!UICONTROL Next]**。

1. 指定下列項目：

   * 標題：指定標題。
   * 授權伺服器：[https://ims-na1.adobelogin.com](https://ims-na1.adobelogin.com)\

   現在將其他欄位留空（稍後將提供）。 保持頁面開啟。

   <!--
   Comment Type: draft

   <li> </li>
   -->

   <!--
   Comment Type: draft

   <li>Step text</li>
   -->

#### (AEM僅限6.4和AEM6.5版)在Adobe開發人員主控台上設定服務API {#createintegration}

若要使用Automated forms conversion服務，請建立專案，並在Adobe開發人員主控台(Developer Console)上將自動化Forms組態服務API新增至專案。 整合會產生API金鑰、用戶端密碼、裝載(JWT)。

1. 登入[https://console.adobe.io/](https://console.adobe.io/)。 使用您的Adobe ID開發人員帳戶（您的管理員已布建）登入Adobe I/O主控台以登入。
1. 從右上角選擇您的組織。 如果您不清楚自己的組織為何，請聯絡您的管理員。
1. 點選&#x200B;**[!UICONTROL Create new project]**。 此時會出現一個畫面，讓您開始使用新專案。 點選&#x200B;**[!UICONTROL Add API]**。 此時會出現一個畫面，其中列出您帳戶所有已啟用的API。
1. 選擇&#x200B;**[!UICONTROL Automated Forms Conversion service]**&#x200B;並點選&#x200B;**[!UICONTROL Next]**。 此時會出現用於設定API的畫面。
1. 選擇[!UICONTROL Upload your public key]選項，上傳下載AEM於[取得公共憑證](#obtainpubliccertificates)區段中的-Adobe-IMS.crt檔案，然後點選&#x200B;**[!UICONTROL Next]**。 此時將顯示「建立新服務帳戶(JWT)」憑據選項。 點選&#x200B;**[!UICONTROL Next]**。
1. 選擇產品配置檔案並點選&#x200B;**[!UICONTROL Save configured API]**。 選擇在[授予您組織開發人員存取權時建立的設定檔。 ](#adduseranddevs)如果您不知道要選擇的配置式，請與管理員聯繫。
1. 點選&#x200B;**[!UICONTROL Service Account (JWT)]**&#x200B;以檢視API金鑰、用戶端密碼和將您的本機執行個體連接至Automated forms conversion服務所需AEM的其他資訊。 頁面上的資訊可用來在本機電腦上建立IMS設定。

1. 在您的本機例項上開啟「IMS設定」頁面。 在[取得公開憑證](#obtainpubliccertificates)這一節的結尾，您已保持此頁面開啟。

   ![指定標題、API金鑰、用戶端密碼和裝載  ](assets/ims-configuration-details.png)

1. 在「AdobeIMS技術」頁面上，指定「API金鑰」和「用戶端密碼」。 使用「Adobe開發人員控制台」頁面的「服務帳戶」(JWT)上指定的值。

   >[!NOTE]
   >
   >
   >對於裝載，請使用Adobe開發人員控制台的「服務帳戶(JWT)」頁面的「生成JWT」頁籤中提供的代碼。

1. 點選&#x200B;**[!UICONTROL Save]**。 建立IMS設定。

   >[!CAUTION]
   >
   >僅建立一個IMS設定。 請勿建立多個IMS組態。

1. 選擇IMS設定，然後點選&#x200B;**[!UICONTROL Check Health]**。 對話方塊隨即顯示。點選&#x200B;**[!UICONTROL Check]**。 成功連線時，*已成功擷取 Token* 訊息就會顯示。

   ![在成功連線時，會顯示成功擷取的Token訊息。  ](assets/health-check.png)

   <br/> <br/>

#### 配置Cloud Service{#configure-the-cloud-service}

建立Cloud Service設定，將您的AEM例項連接至轉換服務。 它也可讓您指定轉換的範本、主題和表單片段。 您可以針對每組表單分別建立多個雲端服務組態。 例如，您可以為銷售部門表單設定個別設定，並為客戶支援表單設定個別設定。 執行下列步驟以建立雲端服務設定：

1. 在您的AEM Forms實例上，按一下&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Tools]**> **[!UICONTROL Cloud Services]** > **[!UICONTROL Automate Forms Conversion Configuration]**。
1. 點選&#x200B;**[!UICONTROL Global]**&#x200B;資料夾並點選&#x200B;**[!UICONTROL Create]**。 將顯示建立Automated forms conversion配置的頁。 配置在「全局」資料夾中建立。 您也可以在存在的不同資料夾中建立配置，或為配置建立資料夾。

1. 在&#x200B;**[!UICONTROL Create Automated Forms Conversion Configuration]**&#x200B;頁面上，指定下列欄位的值，然後點選&#x200B;**[!UICONTROL Next]**。

   | 欄位 | 說明 |
   |--- |--- |
   | 標題 | 設定的唯一標題。 標題會顯示在用於開始轉換的UI中。 |
   | 名稱 | 配置的唯一名稱。 配置將以指定的名稱保存在CRX-Repository中。 名稱可以與標題相同。 |
   | 縮圖位置 | 配置的縮略圖位置。 |
   | 服務 URL | Adobe雲上的Automated forms conversion服務URL。 使用`https://aemformsconversion.adobe.io/` URL。 |
   | 範本 | 要套用至轉換表單的預設範本。 開始轉換前，您隨時可以指定不同的範本。 範本包含最適化表單的基本結構和初始內容。 您可以從現成可用的範本中選擇範本。 您也可以建立自訂範本。 |
   | 主題 | 套用至轉換表單的預設主題。 開始轉換之前，您隨時可以指定不同的主題。  您可以按一下圖示，選擇現成可用的主題。 您也可以建立自訂主題。 |
   | 現有片段 | 現有片段的位置（如果有）。 |
   | 自訂元模型 | 自訂中繼模型的。schema.json檔案路徑。 |



1. 在&#x200B;**[!UICONTROL Create Automated Forms Conversion Configuration]**&#x200B;頁面的&#x200B;**[!UICONTROL Advanced]**&#x200B;標籤中，指定下列欄位的值：

   <table>
   <thead>
   <tr>
   <th>欄位</th>
   <th>說明</th>
   </tr>
   </thead>
   <tbody>
   <tr>
   <td >產生記錄文件</td>
   <td>選擇為轉換的表單自動生成記錄文檔的選項。 此選項僅適用於XFA型表單(XDP和PDF forms)。 當您啟用此選項時，在提交表格後，您可讓客戶以列印或檔案格式記錄他們在表格中填入的資訊，以供日後參考。 這稱為記錄檔案。</td>
   </tr>
   <tr>
   <td>啟動 Analytics</td>
   <td>(僅AEM適用於6.4AEM和6.5)選擇選項，以啟用所有轉換表單上的Adobe Analytics。 在使用此選項之前，請確定已為您的AEM Forms實例啟用Adobe Analytics。</td>
   </tr>
   </tbody>
   </table>

   * 當來源是副檔名為。XDP的XFA型表格時，輸出DOR會保留XFA版面配置，否則轉換服務會使用現成可用的範本，為其他XFA型表格產生DOR。
   * 提交XFA表單時，表單的提交資料會儲存為XML元素或屬性。 例如，`<Amount currency="USD"> 10.00 </Amount>`。 貨幣會儲存為屬性和貨幣金額，而10.00會儲存為元素。 自適應表單的提交資料沒有屬性，只有元素。 因此，當基於XFA的表單被轉換為自適應表單時，自適應表單提交資料包含每個此類屬性的元素。 例如，

   ```css
      {
         "Type": "Principal",
   
         "Amount": "10.00",
   
         "currency": "USD"
      }
   ```

1. 點選&#x200B;**[!UICONTROL Create]**。 雲端設定此時已建立。您的AEM Forms實例已準備好開始將舊式表單轉換為自適應表單。
