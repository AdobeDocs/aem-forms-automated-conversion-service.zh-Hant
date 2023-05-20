---
title: 設定自動表單轉換服務
description: 準AEM備實例使用Automated forms conversion服務
role: User, Admin
exl-id: 8f21560f-157f-41cb-ba6f-12a4d6e18555
source-git-commit: 47261710e6616c27c210ac53bffcc2387a06ea7a
workflow-type: tm+mt
source-wordcount: '2684'
ht-degree: 7%

---

# 設定自動表單轉換服務 {#about-this-help}

本幫助介紹管理員如AEM何配置Automated forms conversion服務，以自動將其PDF forms轉換為自適應表單。 此幫助適用於您組織AEM的IT和管理員。 所提供的資訊基於以下假設：任何閱讀本幫助的人都熟悉以下技術：

* 安裝、配置和管理Adobe Experience Manager和AEM包，

* 使用Linux®和Microsoft® Windows®作業系統，

* 配置SMTP郵件伺服器

<!--- >[!VIDEO](https://video.tv.adobe.com/v/29267/) 

**Watch the video or read the article to configure Automated Forms Conversion service** -->

## 上線{#onboarding}

該服務可免費向6.4AEMForms和6.AEM5Forms本地客戶和Adobe管理服務企業客戶提供。 您可以聯絡 Adobe Sales 團隊或您的 Adobe 代表，請求存取該服務。該服務還面向AEM Formsas a Cloud Service客戶免費預啟用。

Adobe 為您的組織啟用存取權，並向您指定的組織管理員提供所需的權限。管理員可以授予組織的 AEM Forms 開發人員（使用者）存取權限以連接到該服務。 

## 必備條件 {#prerequisites}

您需要以下人員才能使用Automated forms conversion服務：

* automated forms conversion服務已為您的組織啟用
* 具有轉換服務管理員權限的Adobe ID帳戶
* 具有最新AEMService Pack或最新更新的啟動和運AEM行的6.4、6.5或AEM Formsas a Cloud Service作者實AEM例。
* 屬於AEMforms-user組AEM的用戶（在實例上）

## 設定環境 {#setuptheservice}

使用服務之前，請準AEM備您的作者實例以連接到在Adobe雲上運行的服務。 按列出的順序執行以下步驟，為服務準備實例：

1. [下載並安裝AEM6.4、AEM6.5或板載AEM Formsas a Cloud Service](#aemquickstart)
1. [下載並安裝最新AEM的Service Pack](#servicepack)
1. [下載並安裝最新的AEM Forms附加軟體包](#downloadaemformsaddon)
1. （可選） [下載並安裝最新的連接器包](#installConnectorPackage)
1. [建立自定義主題和模板](#referencepackage)

### 下載並安裝AEM6.4或AEM6.5或板載AEM Formsas a Cloud Service {#aemquickstart}


automated forms conversion服務在作者實AEM例上運行。 您需AEM要6.4AEM、6.5或AEM Formsas a Cloud Service來設定作AEM者實例。

* 如果未啟動和AEM運行6.4AEM或6.5，請從以下位置下載。 下載後AEM，有關設定作者實例的說AEM明，請參見 [部署和維護](https://helpx.adobe.com/experience-manager/6-5/sites/deploying/using/deploy.html#defaultlocalinstall):

   * 如果您是現有AEM客戶，請AEM從下AEM載6.4或6.5 [Adobe許可網站](http://licensing.adobe.com)。

   * 如果您是Adobe合作夥伴，請使用 [Adobe合作夥伴培訓計畫](https://adobe.allegiancetech.com/cgi-bin/qwebcorporate.dll?idx=82357Q) 請求AEM6.4或AEM6.5。

* 如果您使用AEM Formsas a Cloud Service，請在板上查看 [AEM Formsas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/setup-environment/setup-forms-cloud-service.html?lang=en#setup-environment) 和 [設定本地開發環境](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/setup-environment/setup-local-development-environment.html?lang=en#setup-environment)。

### (AEM僅適用於6.4AEM和6.5)下載和安AEM裝最新Service Pack {#servicepack}

下載並安裝最新AEM的Service Pack。 有關詳細說明，請參見或 [《 AEM 6.4 Service Pack發行說明》](https://helpx.adobe.com/tw/experience-manager/6-4/release-notes/sp-release-notes.html) 或 [《 AEM 6.5 Service Pack發行說明》](https://helpx.adobe.com/tw/experience-manager/6-5/release-notes/sp-release-notes.html)。

### (AEM僅適用於6.4AEM和6.5)下載並安裝AEM Forms附加軟體包  {#downloadaemformsaddon}

實AEM例包含基本表單功能。 轉換服務需要AEM Forms的全部功能。 下載並安裝AEM Forms附加軟體包以利用AEM Forms的所有功能。 需要包來設定和運行轉換服務。 有關詳細說明，請參見 [安裝和配置資料捕獲功能。](https://helpx.adobe.com/tw/experience-manager/6-5/forms/using/installing-configuring-aem-forms-osgi.html)

>[!NOTE]
> 確保在安裝附加軟體包後執行強制安裝後配置。

<!-- ### (Optional) Download and install connector package  {#installConnectorPackage}

The connector package provides early access to the [Auto-detect logical sections](convert-existing-forms-to-adaptive-forms.md#run-the-conversion) features and improvements delivered in release AFC-2020.03.1. Do not install the package if you do not require feature and improvements delivered in AFC-2020.03.1.  You can [download the connector package from AEM Package Share](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/featurepack/AFCS-Connector-2020.03.1). -->


### 建立自定義主題和模板 {#referencepackage}

如果AEM從6.4或AEM6.5開始 [生產模式](https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/production-ready.html) （nosamplecontent運行模式），未安裝引用包。 引用包包含示例主題和模板。 automated forms conversion服務需要至少一個主題和一個模板來將PDF表單轉換為自適應表單。 建立您自己和點的自定義主題和模板 [服務配置](#configure-the-cloud-service) 在使用服務之前使用自定義模板和主題。

您還可以下載和安裝 [AEM Forms參考資產](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) 檔案包。 它建立一些參考主題和模板。

## 設定服務 {#configure-the-service}

在您繼續配置服務並將本地實例與Adobe雲上運行的服務連接之前，請瞭解連接到該服務所需的角色和權限。 該服務使用兩種不同類型的人員，即管理員和開發人員：

* **管理員**:管理員負責管理其組織的Adobe軟體和服務。 管理員授予其組織中的開發人員訪問權限，以連接到在Automated forms conversion雲上運行的Adobe服務。 為組織設定管理員時，管理員將收到帶標題的電子郵件 **[!UICONTROL 'You now have administrator rights to manage Adobe software and services for your organization']**。 如果您是管理員，請檢查郵箱中是否有以前提及的標題的電子郵件，然後繼續 [授予您組織開發人員的訪問權限](#adduseranddevs)。

![管理員訪問權限授予電子郵件](assets/admin-console-adobe-io-access-grantedx75.png)

* **開發人員**:開發人員將本地AEM Forms作者實例連接到在Adobe雲上運行的Automated forms conversion服務。 當管理員授予開發人員連接到Automated forms conversion服務的權限時，會向開發人員發送一封電子郵件，其標題為「您現在擁有開發人員權限，可以管理您組織的AdobeAPI整合。 如果您是開發人員，請檢查郵箱中是否包含先前提到的標題的電子郵件，然後繼續 [將本地實AEM例連接到Adobe雲上的Automated forms conversion服務。](#connectafcadobeio)

![開發人員訪問授權電子郵件](assets/email-developer-accessx94.png)

### (僅適用於AEM6.4和AEM6.5的管理員)授予您組織的開發人員的訪問權限 {#adduseranddevs}

Adobe啟用您組織的訪問權限並為管理員提供所需權限後，管理員可以登錄Admin Console（下面的詳細說明），建立配置檔案，並將開發人員添加到配置檔案中。 開發人員可以將AEM Forms的本地實例連接到Adobe雲上的Automated forms conversion服務。

開發人員是您組織中指定用於運行轉換服務的成員。 只有添加到AdobeAutomated forms conversion服務配置檔案的開發人員才有權使用Automated forms conversion服務。 執行以下步驟建立配置檔案並向其添加開發人員。 至少需要一個配置檔案才能授予組織開發人員所需的訪問權限：

1. 登錄到 [Admin Console](https://adminconsole.adobe.com/)。 使用 **Adobe ID** 已設定為使用Automated forms conversion服務登錄的管理員。 不要登錄任何其他ID或Federated ID。
1. 按一下 **[!UICONTROL Automated Forms Conversion]** 的雙曲餘切值。
1. 按一下 **[!UICONTROL New Profile]** 的 **[!UICONTROL Products]** 頁籤。
1. 指定 **[!UICONTROL Name]**。 **[!UICONTROL Display Name]**, **[!UICONTROL Description]** 的子菜單。 按一下 **[!UICONTROL Done]**. 建立配置檔案。

   ![指定新配置檔案的詳細資訊。](assets/create-new-profile-details.png)

1. 將開發人員添加到配置檔案。 要添加開發人員，請執行以下操作：
   1. 在 [Admin Console](https://adminconsole.adobe.com/enterprise)，導航至「概述」頁籤。
   1. 按一下 **[!UICONTROL Assign Developers]** 在所需產品卡上。
   1. 輸入開發人員的電子郵件地址以及（可選）名和姓。
   1. 選擇產品配置檔案。 點選 **[!UICONTROL Save]**。

對所有用戶重複上述步驟。 有關添加開發人員的詳細資訊，請參閱 [管理開發人員](https://helpx.adobe.com/enterprise/using/manage-developers.html)。

一旦管理員將開發人員添加到Adobe I/O配置檔案中，就通過電子郵件通知開發人員。 在收到電子郵件後，開發人員可以 [將本地AEM Forms實例與Adobe雲上的Automated forms conversion服務連接](#connectafcadobeio)。

### （僅適用於開發人員）將您的本地AEM Forms實例連接到Adobe雲上的Automated forms conversion服務 {#connectafcadobeio}

在管理員為您提供開發人員訪問權限後，您可以將本地AEM Forms實例連接到在Adobe雲上運行的Automated forms conversion服務。 按所列順序執行以下步驟，將AEM Forms實例連接到服務：

* [配置電子郵件通知](configure-service.md#configureemailnotification)
* [將用戶添加到表單用戶組](#adduserstousergroup)
* [獲取公共證書](#obtainpubliccertificates)
* [在Adobe Developer控制台上配置服務API](#createintegration)
* [配置雲服務](configure-service.md#configure-the-cloud-service)

#### 配置電子郵件通知 {#configureemailnotification}

automated forms conversion服務使用第CQ天郵件服務來發送電子郵件通知。 這些電子郵件通知包含有關成功或失敗轉換的資訊。 如果選擇不接收通知，請跳過這些步驟。 執行以下步驟來配置第CQ天郵件服務：

* 6AEM.4Forms或AEM6.5Forms:

   1. 轉到AEM配置管理器 `http://localhost:4502/system/console/configMgr`
   1. 開啟「第CQ天郵件服務」配置。 為 **[!UICONTROL SMTP server host name]**。 **[!UICONTROL SMTP server port]**, **[!UICONTROL From address]** 的子菜單。 按一下 **[!UICONTROL Save]**.

      您可以與電子郵件服務提供商或IT管理員聯繫，以獲取有關SMTP伺服器的主機名和埠的資訊。 您可以在「發件人」欄位中使用任何有效的電子郵件地址。 例如，notification@example.com或donotreply@example.com。

   1. 開啟 **[!UICONTROL Day CQ Link Externalizer]** 配置。 在 **[!UICONTROL Domains]** 欄位，指定本地、作者和發佈實例的實際主機名或IP地址和埠號。 按一下 **[!UICONTROL Save]**.

* 對於AEM Formsas a Cloud Service, [記錄支援票證以啟用電子郵件服務](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#sending-email)。

#### 將用戶添加到表單用戶組 {#adduserstousergroup}

在指定用於運行服務的用戶AEM的配置檔案中指定電子郵件地址。 確保用戶是 [表單用戶](https://experienceleague.adobe.com/docs/experience-manager-65/forms/manage-administer-aem-forms/forms-groups-privileges-tasks.html) 組。 電子郵件被發送到運行轉換的用戶的電子郵件地址。 要為用戶指定電子郵件地址並將用戶添加到表單用戶組，請執行以下操作：

1. 以管理員身份登錄到AEM Forms作AEM者實例。 使用本地憑AEM據登錄。 不要使用Adobe ID登錄。 點擊 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Users]**。

1. 選擇指定用於運行轉換服務並點擊的用戶 **[!UICONTROL Properties]**。 將開啟「編輯用戶設定」頁。
1. 在 **[!UICONTROL Email]** 欄位和攻擊 **[!UICONTROL Save]**。 在成功完成或轉換失敗時，這些電子郵件將發送到指定的電子郵件地址。
1. 點擊 **組** 頁籤。 在「選擇組」頁籤中，鍵入並選擇 **表單用戶** 組。 點擊 **保存並關閉**。 用戶現在是表單用戶組的成員。

#### (僅AEM適用於6.4AEM和6.5) {#obtainpubliccertificates}

公共證書允許您在Adobe I/O時對配置檔案進行身份驗證。

1. 登錄到您的AEM Forms作者實例。 瀏覽到 **[!UICONTROL Tools]**> **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**. 點選 **[!UICONTROL Create]**。的 **[!UICONTROL Adobe IMS Technical Account Configuration]** 的子菜單。

   ![「Adobe IMS技術帳戶配置」頁](assets/adobe-ims-technical-account-configuration.png)

1. 選擇 **[!UICONTROL Automated Forms Conversion Service]** 在雲解決方案中。

1. 選擇 **[!UICONTROL Create new certificate]** 框中，指定別名。 別名的作用是對話方塊的名稱。點選 **[!UICONTROL Create certificate]**。對話方塊隨即顯示。按一下 **[!UICONTROL OK]**. 證書已建立。

1. 點擊 **[!UICONTROL Download Public Key]** 並保存 *AEM-Adobe-IMS.crt* 電腦上的證書檔案。 證書檔案用於 [在Adobe Developer控制台上配置服務API](#createintegration)。 點選 **[!UICONTROL Next]**。

1. 指定以下內容：

   * 標題：指定標題。
   * 授權伺服器： [https://ims-na1.adobelogin.com](https://ims-na1.adobelogin.com)\

   將其他欄位留空（稍後提供）。 保持頁面開啟。

   <!--
   Comment Type: draft

   <li> </li>
   -->

   <!--
   Comment Type: draft

   <li>Step text</li>
   -->

#### (僅適AEM用於6.4AEM和6.5)在Adobe Developer控制台上配置服務API {#createintegration}

要使用Automated forms conversion服務，請建立項目，並將自動Forms配置服務API添加到Adobe Developer控制台上的項目。 整合生成API密鑰、客戶端密鑰、負載(JWT)。

1. 登錄到 [https://console.adobe.io/](https://console.adobe.io/)。 使用您的Adobe ID，您的管理員設定的登錄到Adobe I/O控制台以登錄的開發人員帳戶。
1. 從右上角選擇您的組織。 如果您不清楚自己的組織為何，請聯絡您的管理員。
1. 點選 **[!UICONTROL Create new project]**。將顯示一個螢幕，以開始新項目。 點選 **[!UICONTROL Add API]**。此時將顯示一個螢幕，其中列出了為您的帳戶啟用的所有API。
1. 選擇 **[!UICONTROL Automated Forms Conversion service]** 點擊 **[!UICONTROL Next]**。 將顯示一個用於配置API的螢幕。
1. 選擇 [!UICONTROL Upload your public key] 選項，上AEM載下載於 [獲取公共證書](#obtainpubliccertificates) 截面和點擊 **[!UICONTROL Next]**。 出現「Create a new Service Account(JWT)credential(建立新服務帳戶(JWT)憑據)」選項。 點選 **[!UICONTROL Next]**。
1. 選擇產品配置檔案並點擊 **[!UICONTROL Save configured API]**。 選擇在建立時建立的配置檔案 [授予您組織的開發人員的訪問權限](#adduseranddevs)。 如果您不知道要選擇的配置檔案，請與管理員聯繫。
1. 點擊 **[!UICONTROL Service Account (JWT)]** 查看將本地實例連接到Automated forms conversion服務所需的API密鑰、客戶端AEM密鑰和其他資訊。 頁面上的資訊用於在本地電腦上建立IMS配置。

1. 開啟本地實例上的「IMS配置」頁。 在[取得公開憑證](#obtainpubliccertificates)這一節的結尾，您已保持此頁面開啟。

   ![指定標題、API密鑰、客戶端密鑰和負載 ](assets/ims-configuration-details.png)

1. 在「Adobe IMS技術」頁上，指定API密鑰和客戶端密鑰。 使用在Adobe Developer控制台頁的服務帳戶(JWT)上指定的值。

   >[!NOTE]
   >
   >
   >對於負載，請使用Adobe Developer控制台的「服務帳戶」(JWT)頁的「生成JWT」頁籤中提供的代碼。

1. 點選 **[!UICONTROL Save]**。建立IMS配置。

   >[!CAUTION]
   >
   >僅建立一個IMS配置。 不要建立多個IMS配置。

1. 選擇IMS配置並點擊 **[!UICONTROL Check Health]**。 對話方塊隨即顯示。點選 **[!UICONTROL Check]**。成功連線時，*已成功擷取 Token* 訊息就會顯示。

   ![成功連接時，將顯示標籤成功檢索的消息。 ](assets/health-check.png)

   <br/> <br/>

#### 配置Cloud Service {#configure-the-cloud-service}

建立Cloud Service配置以將AEM實例連接到轉換服務。 它還允許您指定轉換的模板、主題和表單片段。 您可以為每組表單建立多個單獨的雲服務配置。 例如，您可以為銷售部門表單單獨配置，而為客戶支援表單單獨配置。 執行以下步驟建立雲服務配置：

1. 在你的AEM Forms案例上，點擊 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Tools]**> **[!UICONTROL Cloud Services]** > **[!UICONTROL Automate Forms Conversion Configuration]**。
1. 點擊 **[!UICONTROL Global]** 資料夾和點擊 **[!UICONTROL Create]**。 將顯示用於建立Automated forms conversion配置的頁。 配置在全局資料夾中建立。 您也可以在現有的其他資料夾中建立配置，或為配置建立資料夾。

1. 在 **[!UICONTROL Create Automated Forms Conversion Configuration]** ，指定以下欄位的值並點擊 **[!UICONTROL Next]**。

   | 欄位 | 說明 |
   |--- |--- |
   | 標題 | 配置的唯一標題。 標題顯示在用於開始轉換的UI中。 |
   | 名稱 | 配置的唯一名稱。 配置將以指定的名稱保存在CRX-Repository中。 名稱可以與標題相同。 |
   | 縮略圖位置 | 配置的縮略圖位置。 |
   | 服務 URL | automated forms conversion雲上的Adobe服務的URL。 使用 `https://aemformsconversion.adobe.io/` URL。 |
   | 範本 | 要應用於已轉換表單的預設模板。 在開始轉換之前，您始終可以指定不同的模板。 模板包含自適應表單的基本結構和初始內容。 您可以從現成提供的模板中選擇模板。 您也可以建立自定義模板。 |
   | 主題 | 要應用於轉換表單的預設主題。 在開始轉換之前，您始終可以指定不同的主題。  您可以按一下該表徵圖，選擇現成的主題。 您還可以建立自定義主題。 |
   | 現有片段 | 現有片段的位置（如果有）。 |
   | 自訂中繼模型 | 自定義元模型的.schema.json檔案的路徑。 您可以為英語、法語、德語、西班牙語、義大利語和葡萄牙語建立單獨的元模型。 |

1. 在 **[!UICONTROL Advanced]** 頁籤 **[!UICONTROL Create Automated Forms Conversion Configuration]** 頁中，為以下欄位指定值：

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
   <td>選擇選項以自動為轉換的表單生成記錄文檔。 此選項僅用於基於XFA的表單(XDP和PDF forms)。 啟用此選項後，在提交表單後，您可以允許客戶以打印或文檔格式記錄他們在表單中填寫的資訊，供其將來參考。 這稱為記錄文檔。</td>
   </tr>
   <tr>
   <td>啟動 Analytics</td>
   <td>(僅適AEM用於6.4AEM和6.5)選擇選項，以在所有轉換的表單上啟用Adobe Analytics。 在使用此選項之前，請確保為您的AEM Forms實例啟用Adobe Analytics。</td>
   </tr>
   </tbody>
   </table>

   * 如果源是副檔名為.XDP的基於XFA的表單，則輸出DOR將保留XFA佈局，否則轉換服務使用現成模板為其他基於XFA的表單生成DOR。
   * 提交XFA表單時，表單的提交資料將另存為XML元素或屬性。 比如說， `<Amount currency="USD"> 10.00 </Amount>`。 幣種將另存為屬性和幣種金額，10.00將另存為要素。 自適應表單的提交資料沒有屬性，它只有元素。 因此，當基於XFA的表單被轉換為自適應表單時，自適應表單提交資料包含每個此類屬性的元素。 例如，

   ```css
      {
         "Type": "Principal",
   
         "Amount": "10.00",
   
         "currency": "USD"
      }
   ```

1. 點選 **[!UICONTROL Create]**。雲端設定此時已建立。您的AEM Forms實例已準備好開始將舊表單轉換為自適應表單。
