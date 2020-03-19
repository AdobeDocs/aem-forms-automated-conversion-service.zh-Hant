---
title: 使用JSON結構描述將轉換的最適化表單提交至資料庫
description: 建立表單資料模型並在AEM工作流程中參考表單資料模型，以JSON結構描述將轉換的最適化表單提交至資料庫。
uuid: f98b4cca-f0a3-4db8-aef2-39b8ae462628
topic-tags: forms
discoiquuid: cad72699-4a4b-4c52-88a5-217298490a7c
translation-type: tm+mt
source-git-commit: c552f4073ac88ca9016a746116a27a5898df7f7d

---


# 使用 AEM 工作流程整合最適化表單與資料庫 {#submit-forms-to-database-using-forms-portal}

「自動表單轉換」服務可讓您將非互動式PDF表單、Acro表單或以XFA為基礎的PDF表單轉換為最適化表單。 在開始轉換程式時，您可以選擇是否使用資料系結產生最適化表單。

如果您選擇產生不含資料系結的最適化表單，則轉換後可將轉換的最適化表單與表單資料模型、XML架構或JSON架構整合。 對於表單資料模型，您需要手動將自適應表單欄位與表單資料模型系結。 不過，如果您產生具有資料系結的最適化表單，轉換服務會自動將最適化表單與JSON結構描述關聯，並在最適化表單和JSON結構描述中可用的欄位間建立資料系結。 然後，您可以將最適化表單與您選擇的資料庫整合、填寫表單中的資料，並將它送出至資料庫。 同樣地，在成功與資料庫整合後，您可以配置轉換的自適應表單中的欄位，以便從資料庫中檢索值並預填充自適應表單欄位。

下圖描述了將已轉換的自適應表單與資料庫整合的不同階段：

![資料庫整合](assets/integrate-adaptive-form-with-database.png)

本文說明成功執行所有這些整合階段的逐步指示。

## 先決條件 {#pre-requisites}

* 設定AEM 6.4或6.5作者實例
* 為您 [的AEM實例安裝](https://helpx.adobe.com/experience-manager/aem-releases-updates.html) 最新的Service Pack
* AEM Forms附加元件套件的最新版本
* Configure [Automated Forms Conversion service](configure-service.md)
* 設定資料庫。 示例實施中使用的資料庫是MySQL 5.6.24。不過，您可以將轉換的最適化表單與您選擇的任何資料庫整合。

## 範例自適應表單 {#sample-adaptive-form}

若要執行使用案例，以使用AEM工作流程將轉換的最適化表單與資料庫整合，請下載下列範例PDF檔案。

您可以使用下列方式下載範例聯絡我們表單：

[取得檔案](assets/sample_contact_us_form.pdf)

PDF檔案是Automated Forms Conversion服務的輸入。 服務將此檔案轉換為自適應格式。 下圖以PDF格式描述範例聯絡我們表單。

![貸款申請表](assets/sample_contact_us_form.png)

## 安裝mysql-connector-java-5.1.39-bin.jar檔案 {#install-mysql-connector-java-file}

對所有作者和發佈實例執行以下步驟以安裝mysql-connector-java-5.1.39-bin.jar檔案：

1. 導覽至 `http://server:port/system/console/depfinder` 並搜尋com.mysql.jdbc套件。
1. 在「導出者」(Exported by)列中，檢查軟體包是否由任何包導出。 如果軟體包未由任何包導出，請繼續。
1. 導覽至並 `http://server:port/system/console/bundles` 按一下 **[!UICONTROL Install/Update]**。
1. 單 **[!UICONTROL Choose File]** 擊並瀏覽以選擇mysql-connector-java-5.1.39-bin.jar檔案。 此外，請選取 **[!UICONTROL Start Bundle]** 和核取 **[!UICONTROL Refresh Packages]** 方塊。
1. 按一下 **[!UICONTROL Install]** 或 **[!UICONTROL Update]**。 完成後，重新啟動伺服器。
1. （僅限Windows）關閉您作業系統的系統防火牆。

## 為表單模型準備資料 {#prepare-data-for-form-model}

AEM Forms Data Integration可讓您設定並連線至不同的資料來源。 使用轉換程式產生最適化表單後，您可以根據表單資料模型、XSD或JSON結構描述來定義表單模型。 您可以使用資料庫、Microsoft Dynamics或任何其他協力廠商服務來建立表單資料模型。

本教程使用MySQL資料庫作為源來建立表單資料模型。 在資料庫中建立模式，並根 **據自適應表單中可用的欄位** ，將Contacttus表添加到模式。

![示例資料mysql](assets/db_entries_sample_form.png)

可以使用以下DDL語句在資料庫中創 **建Contacttus** 表。

```sql
CREATE TABLE `contactus` (
   `name` varchar(45) NOT NULL,
   `email` varchar(45) NOT NULL,
   `phonenumber` varchar(10) DEFAULT NULL,
   `issuedesc` varchar(1000) DEFAULT NULL,
   PRIMARY KEY (`email`)
 ) ENGINE=InnoDB DEFAULT CHARSET=utf8
```

## 設定AEM例項與資料庫之間的連線 {#configure-connection-between-aem-instance-and-database}

執行下列設定步驟，以建立AEM例項與MYSQL資料庫之間的連線：

1. 請前往「AEM Web Console設定」頁面(網址為 `http://server:port/system/console/configMgr`)。
1. 在「Web控制台配置」中， **[!UICONTROL Apache Sling Connection Pooled DataSource]** 查找並按一下以在編輯模式下開啟。 指定屬性的值，如下表所述：

   <table> 
    <tbody> 
    <tr> 
    <th><strong>屬性</strong></th> 
    <th><strong>值</strong></th> 
    </tr> 
    <tr> 
    <td><p>資料來源名稱</p></td> 
    <td><p>用於從資料源池中過濾驅動程式的資料源名稱。</p></td>
    </tr>
    <tr> 
    <td><p>JDBC驅動程式類</p></td> 
    <td><p>com.mysql.jdbc.driver</p></td>
    </tr>
    <tr> 
    <td><p>JDBC連接URI</p></td> 
    <td><p>jdbc:mysql://[host]:[port]/[schema_name]</p></td>
    </tr>
    <tr> 
    <td><p>使用者名稱</p></td> 
    <td><p>對資料庫表進行驗證和執行操作的用戶名</p></td>
    </tr>
    <tr> 
    <td><p>密碼</p></td> 
    <td><p>與用戶名關聯的密碼</p></td>
    </tr>
    <tr> 
    <td><p>事務隔離</p></td> 
    <td><p>READ_COMMITTED</p></td>
    </tr>
    <tr> 
    <td><p>最大活動連接數</p></td> 
    <td><p>1000</p></td>
    </tr>
    <tr> 
    <td><p>最大空閒連接數</p></td> 
    <td><p>100</p></td>
    </tr>
    <tr> 
    <td><p>最小空閒連接數</p></td> 
    <td><p>10</p></td>
    </tr>
    <tr> 
    <td><p>初始大小</p></td> 
    <td><p>10</p></td>
    </tr>
    <tr> 
    <td><p>最大等待</p></td> 
    <td><p>100000</p></td>
    </tr>
     <tr> 
    <td><p>借閱測試</p></td> 
    <td><p>已核取</p></td>
    </tr>
     <tr> 
    <td><p>空閒時測試</p></td> 
    <td><p>已核取</p></td>
    </tr>
     <tr> 
    <td><p>驗證查詢</p></td> 
    <td><p>示例值包括SELECT 1(mysql)、從dual(oracle)中選擇1、SELECT 1(MS Sql Server)(validationQuery)</p></td>
    </tr>
     <tr> 
    <td><p>驗證查詢超時</p></td> 
    <td><p>10000</p></td>
    </tr>
    </tbody> 
    </table>

## Create form data model {#create-form-data-model}

將MYSQL配置為資料源後，請執行以下步驟以建立表單資料模型：

1. 在AEM作者例項中，導覽至 **[!UICONTROL Forms]** > **[!UICONTROL Data Integrations]**。

1. 點選 **[!UICONTROL Create]** > **[!UICONTROL Form Data Model]**。

1. 在精靈 **[!UICONTROL Create Form Data Model]** 中，指 **定workflow_submit** 為表單資料模型的名稱。 點選 **[!UICONTROL Next]**。

1. 選擇您在上一節中配置的MYSQL資料源，然後點選 **[!UICONTROL Create]**。

1. 點選 **[!UICONTROL Edit]** 並展開左窗格中所列的資料來源，以選 **取Contact** 表格、 **[!UICONTROL get]**&#x200B;和 **[!UICONTROL insert]** 服務，然後點選 **[!UICONTROL Add Selected]**。

   ![示例資料mysql](assets/fdm_details_workfdlow_submit.png)

1. 在右窗格中選取資料模型物件，然後點選 **[!UICONTROL Edit Properties]**。 從 **[!UICONTROL get]** 和下 **[!UICONTROL insert]** 拉 **[!UICONTROL Read Service]** 式清單中選 **[!UICONTROL Write Service]** 擇和。 指定讀取服務的引數，然後點選 **[!UICONTROL Done]**。

1. 在標籤 **[!UICONTROL Services]** 中，選取服務 **[!UICONTROL get]** 並點選 **[!UICONTROL Edit Properties]**。 選取 **[!UICONTROL Output Model Object]**、停用切 **[!UICONTROL Return array]** 換並點選 **[!UICONTROL Done]**。

1. 選擇服務 **[!UICONTROL Insert]** 並點選 **[!UICONTROL Edit Properties]**。 選取並點 **[!UICONTROL Input Model Object]** 選該項目 **[!UICONTROL Done]**。

1. 點選 **[!UICONTROL Save]** 以儲存表單資料模型。

您可以使用下列方式下載範例表單資料模型：

[取得檔案](assets/DownloadedFormsPackage_1497728018502500.zip)

## 使用JSON系結產生最適化表單 {#generate-adaptive-forms-with-json-binding}

使用「 [自動表單轉換」服務](convert-existing-forms-to-adaptive-forms.md) ，將「聯 [](#sample-adaptive-form) 絡我們」表單轉換為具有資料系結的最適化表單。 在生成最適化表單時，請確 **[!UICONTROL Generate adaptive form(s) without data bindings]** 保不要選中該複選框。

![具JSON系結的最適化表單](assets/generate_af_with_data_bindings.png)

在中，選取資 **料夾中可用的已轉換「聯絡我** 們」表單， **[!UICONTROL output]** 然後點選 **[!UICONTROL Forms & Documents]****[!UICONTROL Edit]**。 點選 **[!UICONTROL Preview]**、在最適化表單欄位中輸入值，然後點選 **[!UICONTROL Submit]**。

登入 **crx-repository** ，並導覽至 */content/forms/fp/admin/submit/data* ，以JSON格式檢視已提交的值。 以下是當您提交轉換的「聯絡我們」最適化表單時，JSON格式 **的範例資** 料：

```json
{
  "afData": {
    "afUnboundData": {
      "data": {}
    },
    "afBoundData": {
      "data": {
        "name1": "Gloria",
        "email": "abc@xyz.com",
        "phone_number": "2346578965",
        "issue_description": "Test message"
      }
    },
    "afSubmissionInfo": {
      "computedMetaInfo": {},
      "stateOverrides": {},
      "signers": {},
      "afPath": "/content/dam/formsanddocuments/docs_conversion/output/sample_form_json",
      "afSubmissionTime": "20191204014007"
    }
  }
}
```

您現在需要建立一個工作流模型，該工作流模型可以處理此資料，並使用您在前幾節中建立的表單資料模型將其提交到MYSQL資料庫。

## 建立工作流程模型以處理JSON資料 {#create-workflow-model}

執行以下步驟以建立工作流模型，以便將自適應表單資料提交到資料庫：

1. 開啟「工作流模型」控制台。 預設URL為 `https://server:port/libs/cq/workflow/admin/console/content/models.html/etc/workflow/models`。

1. 選擇 **[!UICONTROL Create]**，然後 **[!UICONTROL Create Model]**。 此時將 **[!UICONTROL Add Workflow Model]** 出現對話框。

1. 輸入和 **[!UICONTROL Title]** ( **[!UICONTROL Name]** 可選)。 例如， **workflow_json_submit**。 點選 **[!UICONTROL Done]** 以建立模型。

1. 選取工作流模型，並點選 **[!UICONTROL Edit]** 以在編輯模式中開啟模型。 點選+並新增 **[!UICONTROL Invoke Form Data Model Service]** 步驟至工作流程模型。

1. 點選步驟 **[!UICONTROL Invoke Form Data Model Service]** 並點選「 ![設定](assets/configure_icon.png)」。

1. 在選 **[!UICONTROL Form Data Model]** 項卡中，選擇已在欄位中建立的表單資料模 **[!UICONTROL Form Data Model path]** 型，並從 **[!UICONTROL insert]** 下拉列 **[!UICONTROL Service]** 表中選擇。

1. 在標 **[!UICONTROL Input for Service]** 簽中，從 **[!UICONTROL Provide input data using literal, variable, or a workflow metadata, and a JSON file]** 下拉式清單中選取、選 **[!UICONTROL Map input fields from input JSON]** 取核取方塊、選 **[!UICONTROL Relative to payload]**&#x200B;取並提供 **data.xml** 作為欄位的 **[!UICONTROL Select input JSON document using]** 值。

1. 在該節 **[!UICONTROL Service Arguments]** 中，為表單資料模型參數提供以下值：

   ![啟動表單資料模型服務](assets/invoke_form_data_model_service.png)

   請注意，表單資料模型欄位（例如contactus dot name）會對應至 **afData.afBoundData.data.name1**，此欄位是指已提交最適化表單的JSON架構系結。

## 設定最適化表單提交 {#configure-adaptive-form-submission}

執行以下步驟，將最適化表單提交到您在上一節中建立的工作流模型：

1. 在中，選取資料夾中可用的轉換「聯絡我 **[!UICONTROL output]** 們」表單， **[!UICONTROL Forms & Documents]** 然後點選 **[!UICONTROL Edit]**。

1. 點選並點選「設定」，以開啟 **[!UICONTROL Form Container]** 最適化的表 ![單屬性](assets/configure_icon.png)。

1. 在區 **[!UICONTROL Submission]** 段中， **[!UICONTROL Invoke an AEM workflow]** 從下拉式清 **[!UICONTROL Submit Action]** 單中選取，選取您在上一區段中建立的工作流程模型，並在欄位中指 **定data.xml****[!UICONTROL Data File Path]** 。

1. 點選「 ![儲存](assets/save_icon.png) 」以儲存屬性。

1. 點選 **[!UICONTROL Preview]**、在最適化表單欄位中輸入值，然後點選 **[!UICONTROL Submit]**。 提交的值現在顯示在MYSQL資料庫表中，而不是 **crx-repository**。

## 配置自適應表單以從資料庫預填充值

執行以下步驟，以根據表中定義的主鍵（在本例中為電子郵件）配置自適應表單以預填充MYSQL資料庫中的值：

1. 點選最適 **化表單中的** 「電子郵件」欄位，並點選「編 ![輯」規則](assets/edit-rules.png)。

1. 點選 **[!UICONTROL Create]** 並 **[!UICONTROL is changed]** 從區段 **[!UICONTROL Select State]** 的下拉式清單中選 **[!UICONTROL When]** 取。

1. 在該 **[!UICONTROL Then]** 節中，選 **[!UICONTROL Invoke Service]** 取 **** 並取得您在本文上一節中建立的表單資料模型。

1. 在 **節中選擇E-mail** , **[!UICONTROL Input]** 並在其餘三個欄位中選擇表單資料模型、 **名稱**、 **********[!UICONTROL Output]** 電話號、Oracle Phone Issue Description中的E-mail。 點選 **[!UICONTROL Done]** 以儲存設定。

   ![設定電子郵件預填設定](assets/email_prefill_settings.png)

   因此，根據MYSQL資料庫中現有的E-mail條目，可以在自適應表單模式中預填充其餘三個字 **[!UICONTROL Preview]** 段的值。 例如，如果在 **E-mail** field(根據本文「 [Prepare form model](#prepare-data-for-form-model) 」一節的現有欄位中指定aya.tan@xyz.com **，並跳出欄位，則其餘三個欄位、** Name **、Phone NumberTacklist、****** Callusion Issue Description自動在最適化表單中顯示資料。

您可以使用下列方式下載範例轉換的最適化表單：

[取得檔案](assets/DownloadedFormsPackage_1498226829041200.zip)
