---
title: 設定自動錶單轉換服務(AFCS)
description: 準備好您的AEM執行個體以使用自動錶單轉換服務(AFCS)
solution: Experience Manager Forms
feature: Adaptive Forms
topic: Administration
topic-tags: forms
role: Admin, Developer, User
level: Beginner, Intermediate
exl-id: 8f21560f-157f-41cb-ba6f-12a4d6e18555
source-git-commit: 54cd2cf2fdc4f9b420125e4c04c87bec1b7f368d
workflow-type: tm+mt
source-wordcount: '2366'
ht-degree: 3%

---

# 設定自動錶單轉換服務(AFCS) {#about-this-help}

本文說明AEM管理員如何設定自動錶單轉換服務(AFCS)，以自動將其PDF forms轉換為最適化Forms。 本文適用於貴組織的IT和AEM管理員。 所提供的資訊係基於閱讀本文者皆熟悉下列技術的假設：

* 安裝、設定和管理Adobe Experience Manager和AEM套件，

* 使用Linux®和Microsoft® Windows®作業系統，

<!--- >[!VIDEO](https://video.tv.adobe.com/v/29267/) 

**Watch the video or read the article to configure Automated Forms Conversion service (AFCS)** -->

## 上線{#onboarding}

AEM 6.5 Forms內部部署定期客戶和Adobe代管服務企業客戶可免費使用該服務。 您可以聯絡Adobe銷售團隊或您的Adobe代表，要求存取該服務。 AEM Forms as a Cloud Service客戶也可以免費使用這項服務並預先啟用它。

Adobe 為您的組織啟用存取權，並向您指定的組織管理員提供所需的權限。管理員可以向貴組織的AEM Forms開發人員（使用者）授予存取權，以便連線到該服務。

## 先決條件 {#prerequisites}

您需要下列專案才能使用自動錶單轉換服務(AFCS)：

* 您的組織已啟用自動錶單轉換服務(AFCS)
* 具有轉換服務之管理員許可權的Adobe ID帳戶
* 已開始執行且包含最新AEM Service Pack的AEM 6.5或AEM Forms as a Cloud Service製作執行個體包含最新更新。
* 身為表單使用者群組成員的AEM使用者(在您的AEM執行個體上)

## 設定環境 {#setuptheservice}

在使用服務之前，請準備您的AEM作者執行個體以連線到Adobe Cloud上執行的服務。 按照列出的順序執行以下步驟，準備執行個體以供服務使用：

1. [下載並安裝AEM 6.5或內建AEM Forms as a Cloud Service](#aemquickstart)
1. [(僅適用於AEM 6.5)下載並安裝最新的AEM Service Pack](#servicepack)
1. [(僅適用於AEM 6.5)下載並安裝最新的AEM Forms附加元件套件](#downloadaemformsaddon)
1. [建立自訂主題和範本](#referencepackage)

### 1.下載並安裝AEM 6.5或內建AEM Forms as a Cloud Service {#aemquickstart}


自動錶單轉換服務(AFCS)會在AEM作者執行個體上執行。 您需要AEM 6.5或AEM Forms as a Cloud Service才能設定AEM編寫執行個體。

* 如果您尚未啟動並執行AEM 6.5，請從以下位置下載。 下載AEM之後，如需設定AEM作者執行個體的指示，請參閱[部署和維護](https://helpx.adobe.com/experience-manager/6-5/sites/deploying/using/deploy.html#defaultlocalinstall)：

   * 如果您是AEM現有客戶，請從[AEM授權網站](http://licensing.adobe.com)下載Adobe 6.5。

   * 如果您是Adobe合作夥伴，請使用[Adobe合作夥伴訓練計畫](https://adobe.allegiancetech.com/cgi-bin/qwebcorporate.dll?idx=82357Q)要求AEM 6.5。

* 如果您使用AEM Forms as a Cloud Service，請參閱上線[AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/setup-environment/setup-forms-cloud-service.html?lang=en#setup-environment)和[設定本機開發環境](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/setup-environment/setup-local-development-environment.html?lang=en#setup-environment)。

### 2. (僅適用於AEM 6.5)下載並安裝AEM最新Service Pack {#servicepack}

下載並安裝最新的AEM Service Pack。 如需詳細指示，請參閱[AEM 6.5 Service Pack發行說明](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/release-notes/release-notes)。

### 3. (僅適用於AEM 6.5)下載並安裝AEM Forms附加元件套件   {#downloadaemformsaddon}

AEM執行個體包含基本表單功能。 轉換服務需要AEM Forms的完整功能。 下載並安裝AEM Forms附加元件套件，以使用AEM Forms的所有功能。 需要套件才能設定並執行轉換服務。 如需詳細指示，請參閱[安裝及設定資料擷取功能。](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/install-aem-forms/osgi-installation/installing-configuring-aem-forms-osgi)
https://adminconsole.adobe.com/
>[!NOTE]
> 安裝附加套件後，請務必執行必要的安裝後組態。
>

<!-- ### (Optional) Download and install connector package  {#installConnectorPackage}

The connector package provides early access to the [Auto-detect logical sections](convert-existing-forms-to-adaptive-forms.md#run-the-conversion) features and improvements delivered in release AFC-2020.03.1. Do not install the package if you do not require feature and improvements delivered in AFC-2020.03.1.  You can [download the connector package from AEM Package Share](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/featurepack/AFCS-Connector-2020.03.1). -->


### 4.建立自訂主題和範本 {#referencepackage}

參考套件包含範例主題和範本。 自動錶單轉換服務(AFCS)需要至少一個主題和一個範本，才能將PDF表單轉換為最適化表單。 建立您自己的自訂主題和範本，並指向[服務組態](#configure-the-cloud-service)，以在使用服務之前使用自訂範本和主題。

您也可以在作者執行個體上下載並安裝[AEM Forms參考Assets](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)套件。 它會建立一些參考主題和範本。

## 設定存取權和許可權

在您繼續設定服務並連線您的執行個體與Adobe Cloud上執行的服務之前，請瞭解連線到服務所需的角色和許可權。 此服務使用兩種不同型別的角色：管理員和開發人員：

* **管理員**：管理員負責管理其組織的Adobe軟體與服務。 管理員可向組織內的開發人員授予存取權，以連線至在Adobe Cloud上執行的自動錶單轉換服務(AFCS)。 為組織布建管理員時，管理員會收到標題為&#x200B;**[!UICONTROL 'You now have administrator rights to manage Adobe software and services for your organization']**&#x200B;的電子郵件。 如果您是系統管理員，請檢查信箱中是否有先前提及標題的電子郵件，並繼續[授與組織開發人員的存取權](#adduseranddevs)。

![管理員存取權授與電子郵件](assets/admin-console-adobe-io-access-grantedx75.png)

* **開發人員**：開發人員將AEM Forms作者執行個體連線至在Adobe Cloud上執行的Automated Forms Conversion Service (AFCS)。 當管理員授予開發人員連線至自動錶單轉換服務(AFCS)的許可權時，會向開發人員傳送一封電子郵件(標題為「您現在擁有管理貴組織Adobe API整合的開發者存取權」)。 如果您是開發人員，請檢查信箱中是否有包含先前提及標題的電子郵件，然後繼續前往[將您本端的AEM執行個體連線至Adobe Cloud上的自動錶單轉換服務。](#connectafcadobeio)

![開發人員存取權授與電子郵件](assets/email-developer-accessx94.png)

### 授予組織開發人員存取權

在Adobe為您的組織啟用存取權並提供所需的許可權給管理員後，管理員可以登入Admin Console （下面的詳細說明）、建立設定檔，並將開發人員新增到設定檔。 開發人員可以將AEM Forms的例項連線至Adobe Cloud上的自動錶單轉換服務(AFCS)。

開發人員是您指定執行轉換服務的組織成員。 只有已新增至Adobe自動化表單轉換服務(AFCS)設定檔的開發人員，才有權使用自動化表單轉換服務(AFCS)。
執行以下步驟來建立設定檔並新增開發人員。 至少需要一個設定檔，才能將必要的存取權授予組織的開發人員：

1. 登入[Admin Console](https://adminconsole.adobe.com/)。 使用布建管理員的&#x200B;**Adobe ID**&#x200B;以使用自動錶單轉換服務(AFCS)登入。
1. 按一下&#x200B;**[!UICONTROL Automated Forms Conversion]**&#x200B;選項。
1. 在&#x200B;**[!UICONTROL Products]**&#x200B;索引標籤中按一下&#x200B;**[!UICONTROL New Profile]**。
1. 指定設定檔的&#x200B;**[!UICONTROL Name]**、**[!UICONTROL Display Name]**&#x200B;和&#x200B;**[!UICONTROL Description]**。 按一下 **[!UICONTROL Done]**。例如，將設定檔建立為&#x200B;**AFC_Flamingo_Test_Dev**。

   ![指定新設定檔的詳細資料。](assets/create-new-profile-details.png)

1. 將開發人員新增至設定檔。 若要新增開發人員：
   1. 在[Admin Console](https://adminconsole.adobe.com/enterprise)中，導覽至「概觀」標籤。
   1. 按一下所需產品卡上的&#x200B;**[!UICONTROL Assign Developers]**。
   1. 輸入開發人員電子郵件地址，以及名字和姓氏（可選）。
   1. 選取產品設定檔。 按一下&#x200B;**[!UICONTROL Save]**。

對所有使用者重複上述步驟。 如需新增開發人員的詳細資訊，請參閱[管理開發人員](https://helpx.adobe.com/enterprise/using/manage-developers.html)。

管理員將開發人員新增到Adobe I/O設定檔後，開發人員會透過電子郵件（如果已設定）收到通知。

<!--
### Configure email notification for local AEM Forms instance

Automated Forms Conversion service (AFCS) uses the Day CQ mail service to send email notifications. These email notifications contain information about successful or failed conversions. If you choose not receive notification, skip these steps. Perform the following steps to configure the Day CQ Mail Service:

* **For AEM 6.5 Forms**:

   1. Go to AEM configuration manager at `http://[server]:[port]/system/console/configMgr`
   2. Open the Day CQ Mail Service configuration. Specify a value for the **[!UICONTROL SMTP server host name]**, **[!UICONTROL SMTP server port]**, and **[!UICONTROL From address]** fields. Click **[!UICONTROL Save]**.

      You can contact your email service provider or IT administrator for information about host name and port of SMTP server. You can use any valid email address in the from field. For example, notification@example.com or donotreply@example.com.

   3. Open the **[!UICONTROL Day CQ Link Externalizer]** configuration. In the **[!UICONTROL Domains]** field, specify the actual host name or IP address and port number for local, author, and publish instances. Click **[!UICONTROL Save]**.

* For AEM Forms as a Cloud Service, [log a support ticket to enable the email service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#sending-email). -->

### 新增使用者至表單 — 使用者群組 {#adduserstousergroup}

在指定用來執行服務的AEM使用者之設定檔中，指定電子郵件地址。 確定使用者是&#x200B;**forms-users**&#x200B;群組的成員。 會將電子郵件傳送至執行轉換之使用者的電子郵件地址。 若要指定使用者的電子郵件地址，並將使用者新增至表單使用者群組：

1. 以AEM管理員身分登入您的AEM Forms作者執行個體。 使用您的本機AEM憑證登入。
1. 按一下&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Users]**。
1. 選取指定要執行轉換服務的使用者，然後按一下&#x200B;**[!UICONTROL Properties]**。 **編輯使用者設定**&#x200B;頁面隨即開啟。
1. 在&#x200B;**[!UICONTROL Email]**&#x200B;欄位中指定電子郵件地址，然後按一下&#x200B;**[!UICONTROL Save]**。 成功完成或轉換失敗時，會將電子郵件傳送至指定的電子郵件地址。

   ![指定電子郵件](/help/using/assets/specify-email.png)
1. 按一下「**群組**」標籤。 在[選取群組]索引標籤中，輸入並選取&#x200B;**表單 — 使用者**&#x200B;群組。
1. 按一下&#x200B;**儲存並關閉**。 使用者現在是forms-users群組的成員。

   ![新增使用者群組](/help/using/assets/add-user-group.png)

## 將您的AEM Forms執行個體連線至Adobe Cloud上的自動錶單轉換服務(AFCS)

管理員為您提供開發人員存取權後，您就可以將您的AEM Forms執行個體連線至Adobe Cloud上執行的自動錶單轉換服務(AFCS)。
執行以下步驟，將AEM Forms執行個體連線至自動錶單轉換服務：

[1.在Adobe Developer Console上設定服務API](#configure-the-service-apis-on-adobe-developer-console)

[2.建立Adobe IMS設定](#2-create-adobe-ims-configurations)

[3.建立自動化表單轉換設定](#3-create-automated-forms-conversion-configuration)

### 1.在Adobe Developer Console上設定服務API

若要使用自動錶單轉換服務(AFCS)，請建立專案，並將&#x200B;**自動Forms設定服務** API新增至Adobe Developer Console上的專案。 整合會產生API金鑰、使用者端密碼、技術帳戶ID、範圍與組織ID。
若要在Adobe Developer Console上設定自動錶單轉換服務API，請執行以下步驟：

1. 登入https://developer.adobe.com/console 。 使用您的管理員已布建以登入Adobe I/O主控台的Adobe ID開發人員帳戶來登入。
1. 從右上角選取您的組織。 如果您不清楚自己的組織為何，請聯絡您的管理員。
1. 按一下 **[!UICONTROL Create new project]**。隨即顯示開始使用新專案的畫面。

   ![建立新的API專案](/help/using/assets/create-new-api-project.png)

1. 按一下 **[!UICONTROL Add API]**。隨即顯示畫面，列出已為您的帳戶啟用的所有API。
   ![新增API](/help/using/assets/add-api.png)

1. 選取&#x200B;**[!UICONTROL Automated Forms Conversion service]**&#x200B;並按一下&#x200B;**[!UICONTROL Next]**。 隨即顯示設定API的畫面。
   ![選取AFCS API](/help/using/assets/select-afcs-api.png)

1. 選取&#x200B;**OAuth伺服器對伺服器**&#x200B;驗證方法。
1. 指定&#x200B;**[!UICONTROL Credential Name]**&#x200B;並按一下&#x200B;**[!UICONTROL Next]**。
   ![指定認證名稱](/help/using/assets/specify-credential-name.png)
1. 選取&#x200B;**產品設定檔**。 例如，選取設定檔作為&#x200B;**AFC_Flamingo_Test_Dev**。
1. 按一下「**[!UICONTROL Save configured API]**」。
   ![選取設定檔](/help/using/assets/select-profile.png)

   >[!NOTE]
   >
   > 選取在您組織的開發人員授與存取權時建立的設定檔。 如果您不知道要選取的設定檔，請聯絡管理員。

1. 按一下&#x200B;**[!UICONTROL OAuth Server-to-Server]**&#x200B;以檢視API金鑰、使用者端密碼，以及將您的AEM執行個體連線至自動錶單轉換服務(AFCS)所需的其他資訊。
   ![選取Oath認證](/help/using/assets/select-oauth-credential.png)

   頁面上的資訊會用於建立IMS設定，如[在AEM作者執行個體上建立IMS技術設定](#2-create-ims-technical-configuration-on-aem-author-instance)區段中所述。

   ![OAuth認證詳細資料](/help/using/assets/oauth-credentials-details.png)

### 2.建立Adobe IMS設定

登入您的作者執行個體以建立Adobe IMS設定。 使用&#x200B;**OAuth認證詳細資料**&#x200B;來擷取API金鑰、使用者端密碼、技術帳戶ID、範圍以及組織ID。

1. 登入您的AEM Forms作者執行個體。 導覽至&#x200B;**[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**。
1. 按一下「**[!UICONTROL Create]**」。

   ![建立IMS Adobe設定](/help/using/assets/create-ims-conf.png)

1. **[!UICONTROL Adobe IMS Technical Account Configuration]**&#x200B;頁面隨即顯示。

   ![Adobe IMS技術帳戶設定頁面](assets/adobe-ims-technical-account-configuration.png)
1. 在&#x200B;**雲端解決方案**&#x200B;中選取&#x200B;**[!UICONTROL Automated Forms Conversion Service]**。
1. 指定下列專案：

   * **標題**：指定標題。
   * **授權伺服器**： [https://ims-na1.adobelogin.com](https://ims-na1.adobelogin.com)
   * 從[在Adobe Developer Console](#1-configure-the-service-apis-on-adobe-developer-console)上設定服務API區段擷取下列專案：
      * **使用者端識別碼**：複製並貼上&#x200B;**API金鑰（使用者端識別碼）**。
      * **使用者端密碼**：複製並貼上&#x200B;**使用者端密碼**。
      * **領域**：複製並貼上&#x200B;**領域**。
      * **組織ID**：複製並貼上&#x200B;**技術帳戶ID**。

     ![建立IMS Adobe設定](/help/using/assets/save-ims-configuration.png)

1. 按一下 **[!UICONTROL Save]**。Adobe IMS設定已建立。

   >[!CAUTION]
   >
   > 僅建立一個IMS設定。 請勿建立多個IMS設定。

1. 選取&#x200B;**Adobe IMS設定**&#x200B;並按一下&#x200B;**[!UICONTROL Check Health]**。 對話方塊隨即顯示。
   ![檢查健康狀態](/help/using/assets/check-health.png)

   **檢查**&#x200B;對話方塊出現。

1. 按一下「**[!UICONTROL Check]**」。

   ![檢查健康狀態](/help/using/assets/check-dialog.png)

   成功連線時，*已成功擷取 Token* 訊息就會顯示。

   ![成功連線時，已成功擷取Token訊息就會顯示。](/help/using/assets/healthy-dialog.png)

1. 按一下&#x200B;**關閉**。

### 3.建立自動化表單轉換設定

建立自動錶單轉換設定，將您的AEM執行個體連線到轉換服務。 它也可讓您指定轉換的範本、主題和表單片段。 您可以為每組表單分別建立多個雲端服務設定。
例如，您可以針對銷售部門表單設定不同的組態，而針對客戶支援表單設定不同的組態。 執行以下步驟來建立雲端服務設定：

1. 在您的AEM Forms執行個體上，按一下&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Tools]**> **[!UICONTROL Cloud Services]** > **[!UICONTROL Automate Forms Conversion Configuration]**。
1. 選取&#x200B;**[!UICONTROL Global]**&#x200B;資料夾並按一下&#x200B;**[!UICONTROL Create]**。
**建立自動錶單轉換組態**&#x200B;的頁面已顯示。 設定是在&#x200B;**全域**&#x200B;資料夾中建立。 您也可以在現有的不同資料夾中建立設定，或為您的設定建立資料夾。
   ![選取全域資料夾](/help/using/assets/create-afcs-cloud-conf.png)
1. 在&#x200B;**[!UICONTROL Create Automated Forms Conversion Configuration]**&#x200B;頁面上，指定下列欄位的值並按一下&#x200B;**[!UICONTROL Next]**。

   ![AFCS組態](/help/using/assets/create-afcs-config.png)

   | 欄位 | 說明 |
   |--- |--- |
   | 標題 | 設定的唯一標題。 標題會顯示在用來開始轉換的UI中。 |
   | 名稱 | 設定的唯一名稱。 設定會以指定名稱儲存在CRX存放庫中。 名稱可與標題相同。 |
   | 縮圖位置 | 設定的縮圖位置。 |
   | 服務 URL | Adobe Cloud上自動錶單轉換服務(AFCS)的URL。 使用`https://aemformsconversion.adobe.io/` URL。 |
   | 範本 | 要套用至轉換表單的預設範本。 在開始轉換之前，您一律可以指定不同的範本。 範本包含最適化表單的基本結構和初始內容。 您可以從提供的現成範本中選擇範本。 您也可以建立自訂範本。 |
   | 主題 | 要套用至轉換表單的預設主題。 在開始轉換之前，您可以隨時指定不同的主題。  您可以按一下圖示，選擇隨開即用的主題。 您也可以建立自訂主題。 |
   | 現有片段 | 現有片段的位置（如果有）。 |
   | 自訂中繼模型 | 自訂中繼模型的.schema.json檔案路徑。 您可以建立英文、法文、德文、西班牙文、義大利文和葡萄牙文的個別中繼模型。 |

1. 在&#x200B;**[!UICONTROL Create Automated Forms Conversion Configuration]**&#x200B;頁面的&#x200B;**[!UICONTROL Advanced]**&#x200B;標籤中，指定下列欄位的值：
   ![AFCS組態](/help/using/assets/afcs-config.png)

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
   <td>選取選項，以針對轉換的表單自動產生記錄檔案。 此選項僅適用於XFA型表單(XDP和PDF forms)。 當您啟用選項時，在提交表單後，您可以允許客戶以列印或檔案格式來記錄他們在表單中填寫的資訊，以供日後參考。 這稱為記錄檔案。</td>
   </tr>
   <tr>
   <td>啟動 Analytics</td>
   <td>(適用於AEM 6.5)選取選項，以在所有轉換的表單上啟用Adobe Analytics。 使用選項之前，請確定您的AEM Forms執行個體已啟用Adobe Analytics 。</td>
   </tr>
   </tbody>
   </table>

   * 當來源是副檔名為.XDP的XFA型表單時，輸出DOR會保留XFA配置，否則轉換服務會使用現成的範本為其他XFA型表單產生DOR。
   * 提交XFA表單時，表單的提交資料會儲存為XML元素或屬性。 例如 `<Amount currency="USD"> 10.00 </Amount>`。貨幣會儲存為屬性和貨幣金額，10.00會儲存為元素。 最適化表單的提交資料沒有屬性，只有元素。 因此，當以XFA為基礎的表單轉換為最適化表單時，最適化表單提交資料會包含每個這類屬性的元素。 例如，

   ```css
      {
         "Type": "Principal",
   
         "Amount": "10.00",
   
         "currency": "USD"
      }
   ```

1. 按一下 **[!UICONTROL Create]**。雲端設定此時已建立。您的AEM Forms執行個體已準備好開始將舊版表單轉換為最適化Forms。
