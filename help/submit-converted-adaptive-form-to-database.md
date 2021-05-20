---
title: 使用JSON結構將轉換的最適化表單提交至資料庫
description: 建立表單資料模型並在AEM工作流程中參考該模型，將具有JSON結構描述的轉換適用性表單提交至資料庫。
uuid: f98b4cca-f0a3-4db8-aef2-39b8ae462628
topic-tags: forms
discoiquuid: cad72699-4a4b-4c52-88a5-217298490a7c
exl-id: 5447b66f-9fac-476f-ab8a-9290bb1f9c0d
source-git-commit: 1a3f79925f25dcc7dbe007f6e634f6e3a742bf72
workflow-type: tm+mt
source-wordcount: '1505'
ht-degree: 2%

---

# 使用 AEM 工作流程整合最適化表單與資料庫 {#submit-forms-to-database-using-forms-portal}

automated forms conversion服務可讓您將非互動式PDF表單、Acro表單或XFA型PDF表單轉換為最適化表單。 啟動轉換程式時，您可以選擇產生具有或不具有資料系結的最適化表單。

如果您選擇生成沒有資料綁定的適用性表單，則可以在轉換後將轉換的適用性表單與表單資料模型、XML架構或JSON架構整合。 對於表單資料模型，您需要手動將最適化表單欄位與表單資料模型系結。 不過，如果您產生具有資料系結的適用性表單，轉換服務會自動將適用性表單與JSON結構描述建立關聯，並在適用性表單和JSON結構描述中可用的欄位之間建立資料系結。 然後，您可以將最適化表單與您選擇的資料庫整合、填寫表單中的資料，然後將其提交至資料庫。 同樣地，成功與資料庫整合後，您可以設定轉換後適用性表單中的欄位，以從資料庫擷取值並預填適用性表單欄位。

下圖說明將轉換的最適化表單與資料庫整合的不同階段：

![資料庫整合](assets/integrate-adaptive-form-with-database.png)

本文說明成功執行所有這些整合階段的逐步指示。

## 先決條件{#pre-requisites}

* 設定AEM 6.4或6.5製作例項
* 為您的AEM執行個體安裝[最新Service Pack](https://helpx.adobe.com/tw/experience-manager/aem-releases-updates.html)
* 最新版AEM Forms附加元件套件
* 配置[Automated forms conversion服務](configure-service.md)
* 設定資料庫。 示例實施中使用的資料庫是MySQL 5.6.24。但是，您可以將轉換的最適化表單與您選擇的任何資料庫整合。

## 適用性表單範例{#sample-adaptive-form}

若要執行使用案例以使用AEM工作流程整合轉換的最適化表單與資料庫，請下載下列範例PDF檔案。

您可以下載範例「聯絡我們」表單，方法如下：

[取得檔案](assets/sample_contact_us_form.pdf)

PDF檔案可作為Automated forms conversion服務的輸入。 服務會將此檔案轉換為最適化表單。 下圖以PDF格式描述範例聯絡方式。

![貸款申請表示例](assets/sample_contact_us_form.png)

## 安裝mysql-connector-java-5.1.39-bin.jar檔案{#install-mysql-connector-java-file}

在所有製作執行個體和發佈執行個體上執行下列步驟，以安裝mysql-connector-java-5.1.39-bin.jar檔案：

1. 導航到`http://server:port/system/console/depfinder`並搜索com.mysql.jdbc包。
1. 在「匯出依據」欄中，檢查套件是否由任何套件匯出。 如果包未由任何包導出，請繼續。
1. 導覽至`http://server:port/system/console/bundles`，然後按一下&#x200B;**[!UICONTROL Install/Update]**。
1. 按一下&#x200B;**[!UICONTROL Choose File]**&#x200B;並瀏覽以選擇mysql-connector-java-5.1.39-bin.jar檔案。 同時，選擇&#x200B;**[!UICONTROL Start Bundle]**&#x200B;和&#x200B;**[!UICONTROL Refresh Packages]**&#x200B;複選框。
1. 按一下&#x200B;**[!UICONTROL Install]**&#x200B;或&#x200B;**[!UICONTROL Update]**。 完成後，重新啟動伺服器。
1. （僅限Windows）關閉作業系統的系統防火牆。

## 準備表單模型{#prepare-data-for-form-model}的資料

AEM Forms資料整合可讓您設定並連線至不同的資料來源。 使用轉換程式產生最適化表單後，您可以根據表單資料模型、XSD或JSON結構定義表單模型。 您可以使用資料庫、Microsoft Dynamics或任何其他第三方服務來建立表單資料模型。

本教程使用MySQL資料庫作為源來建立表單資料模型。 在資料庫中建立架構，並根據適用性表單中可用的欄位，將&#x200B;**contactus**&#x200B;表格新增至架構。

![示例資料mysql](assets/db_entries_sample_form.png)

可以使用以下DDL語句在資料庫中建立&#x200B;**contactus**&#x200B;表。

```sql
CREATE TABLE `contactus` (
   `name` varchar(45) NOT NULL,
   `email` varchar(45) NOT NULL,
   `phonenumber` varchar(10) DEFAULT NULL,
   `issuedesc` varchar(1000) DEFAULT NULL,
   PRIMARY KEY (`email`)
 ) ENGINE=InnoDB DEFAULT CHARSET=utf8
```

## 配置AEM實例和資料庫{#configure-connection-between-aem-instance-and-database}之間的連接

執行以下配置步驟以建立AEM實例和MYSQL資料庫之間的連接：

1. 前往`http://server:port/system/console/configMgr`的AEM Web主控台設定頁面。
1. 查找並按一下，在Web控制台配置的編輯模式下開啟&#x200B;**[!UICONTROL Apache Sling Connection Pooled DataSource]**。 指定屬性的值，如下表所述：

   <table> 
    <tbody> 
    <tr> 
    <th><strong>屬性</strong></th> 
    <th><strong>值</strong></th> 
    </tr> 
    <tr> 
    <td><p>資料源名稱</p></td> 
    <td><p>用於從資料源池中篩選驅動程式的資料源名稱。</p></td>
    </tr>
    <tr> 
    <td><p>JDBC驅動程式類</p></td> 
    <td><p>com.mysql.jdbc.Driver</p></td>
    </tr>
    <tr> 
    <td><p>JDBC連接URI</p></td> 
    <td><p>jdbc:mysql://[host]:[port]/[schema_name]</p></td>
    </tr>
    <tr> 
    <td><p>使用者名稱</p></td> 
    <td><p>對資料庫表進行身份驗證和執行操作的用戶名</p></td>
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
    <td><p>最小空閒連接</p></td> 
    <td><p>10</p></td>
    </tr>
    <tr> 
    <td><p>初始大小</p></td> 
    <td><p>10</p></td>
    </tr>
    <tr> 
    <td><p>等待次數上限</p></td> 
    <td><p>100000</p></td>
    </tr>
     <tr> 
    <td><p>借閱時測試</p></td> 
    <td><p>已核取</p></td>
    </tr>
     <tr> 
    <td><p>空閒時測試</p></td> 
    <td><p>已核取</p></td>
    </tr>
     <tr> 
    <td><p>驗證查詢</p></td> 
    <td><p>示例值為SELECT 1(mysql)、從dual(oracle)中選擇1、SELECT 1(MS Sql Server)(validationQuery)</p></td>
    </tr>
     <tr> 
    <td><p>驗證查詢超時</p></td> 
    <td><p>10000</p></td>
    </tr>
    </tbody> 
    </table>

## 建立表單資料模型{#create-form-data-model}

將MYSQL配置為資料源後，請執行以下步驟以建立表單資料模型：

1. 在AEM製作例項中，導覽至&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL Data Integrations]**。

1. 點選&#x200B;**[!UICONTROL Create]** > **[!UICONTROL Form Data Model]**。

1. 在&#x200B;**[!UICONTROL Create Form Data Model]**&#x200B;精靈中，將&#x200B;**workflow_submit**&#x200B;指定為表單資料模型的名稱。 點選&#x200B;**[!UICONTROL Next]**。

1. 選擇您在上一節中配置的MYSQL資料源，然後點選&#x200B;**[!UICONTROL Create]**。

1. 點選&#x200B;**[!UICONTROL Edit]**&#x200B;並展開左窗格中列出的資料來源，以選取&#x200B;**Contactus**&#x200B;表格、**[!UICONTROL get]**&#x200B;和&#x200B;**[!UICONTROL insert]**&#x200B;服務，然後點選&#x200B;**[!UICONTROL Add Selected]**。

   ![示例資料mysql](assets/fdm_details_workfdlow_submit.png)

1. 在右窗格中選擇資料模型對象，然後點選&#x200B;**[!UICONTROL Edit Properties]**。 從&#x200B;**[!UICONTROL Read Service]**&#x200B;和&#x200B;**[!UICONTROL Write Service]**&#x200B;下拉清單中選擇&#x200B;**[!UICONTROL get]**&#x200B;和&#x200B;**[!UICONTROL insert]**。 指定讀取服務的參數，然後點選&#x200B;**[!UICONTROL Done]**。

1. 在&#x200B;**[!UICONTROL Services]**&#x200B;標籤中，選取&#x200B;**[!UICONTROL get]**&#x200B;服務並點選&#x200B;**[!UICONTROL Edit Properties]**。 選取&#x200B;**[!UICONTROL Output Model Object]**，停用&#x200B;**[!UICONTROL Return array]**&#x200B;切換，然後點選&#x200B;**[!UICONTROL Done]**。

1. 選取&#x200B;**[!UICONTROL Insert]**&#x200B;服務，然後點選&#x200B;**[!UICONTROL Edit Properties]**。 選取&#x200B;**[!UICONTROL Input Model Object]**，然後點選&#x200B;**[!UICONTROL Done]**。

1. 點選&#x200B;**[!UICONTROL Save]**&#x200B;以儲存表單資料模型。

您可以使用下列方式下載範例表單資料模型：

[取得檔案](assets/DownloadedFormsPackage_1497728018502500.zip)

## 使用JSON捆綁{#generate-adaptive-forms-with-json-binding}產生最適化表單

使用[Automated forms conversion服務將[「聯絡我們」表單](#sample-adaptive-form)轉換為具有資料綁定的最適化表單。 ](convert-existing-forms-to-adaptive-forms.md)產生最適化表單時，請確定您未選取&#x200B;**[!UICONTROL Generate adaptive form(s) without data bindings]**&#x200B;核取方塊。

![具有JSON捆綁的適用性表單](assets/generate_af_with_data_bindings.png)

選取&#x200B;**[!UICONTROL Forms & Documents]**&#x200B;中&#x200B;**[!UICONTROL output]**&#x200B;資料夾中可用的轉換後&#x200B;**聯絡我們表單**，然後點選&#x200B;**[!UICONTROL Edit]**。 點選&#x200B;**[!UICONTROL Preview]**，在最適化表單欄位中輸入值，然後點選&#x200B;**[!UICONTROL Submit]**。

登入&#x200B;**crx-repository**&#x200B;並導覽至&#x200B;*/content/forms/fp/admin/submit/data*&#x200B;以JSON格式檢視提交的值。 提交轉換的&#x200B;**聯絡我們**&#x200B;適用性表單時，以下是JSON格式的範例資料：

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

您現在需要建立工作流模型，以便處理此資料，並使用您在前幾節中建立的表單資料模型將其提交到MYSQL資料庫。

## 建立工作流程模型以處理JSON資料{#create-workflow-model}

執行下列步驟以建立工作流模型，將最適化表單資料提交至資料庫：

1. 開啟「工作流模型」控制台。 預設URL為`https://server:port/libs/cq/workflow/admin/console/content/models.html/etc/workflow/models`。

1. 依次選擇&#x200B;**[!UICONTROL Create]**&#x200B;和&#x200B;**[!UICONTROL Create Model]**。 將顯示&#x200B;**[!UICONTROL Add Workflow Model]**&#x200B;對話框。

1. 輸入&#x200B;**[!UICONTROL Title]**&#x200B;和&#x200B;**[!UICONTROL Name]**（可選）。 例如， **workflow_json_submit**。 點選&#x200B;**[!UICONTROL Done]**&#x200B;以建立模型。

1. 選擇工作流模型，然後點選&#x200B;**[!UICONTROL Edit]**&#x200B;以在編輯模式中開啟模型。 點選+並新增&#x200B;**[!UICONTROL Invoke Form Data Model Service]**&#x200B;步驟至工作流程模型。

1. 點選&#x200B;**[!UICONTROL Invoke Form Data Model Service]**&#x200B;步驟，然後點選![設定](assets/configure_icon.png)。

1. 在&#x200B;**[!UICONTROL Form Data Model]**&#x200B;標籤中，選擇您在&#x200B;**[!UICONTROL Form Data Model path]**&#x200B;欄位中建立的表單資料模型，然後從&#x200B;**[!UICONTROL Service]**&#x200B;下拉清單中選擇&#x200B;**[!UICONTROL insert]**。

1. 在&#x200B;**[!UICONTROL Input for Service]**&#x200B;標籤中，從下拉清單中選擇&#x200B;**[!UICONTROL Provide input data using literal, variable, or a workflow metadata, and a JSON file]**，選擇&#x200B;**[!UICONTROL Map input fields from input JSON]**&#x200B;複選框，選擇&#x200B;**[!UICONTROL Relative to payload]**，並提供&#x200B;**data.xml**&#x200B;作為&#x200B;**[!UICONTROL Select input JSON document using]**&#x200B;欄位的值。

1. 在&#x200B;**[!UICONTROL Service Arguments]**&#x200B;區段中，為表單資料模型引數提供下列值：

   ![啟動表單資料模型服務](assets/invoke_form_data_model_service.png)

   請注意，表單資料模型欄位（例如contactus dot name）已對應至&#x200B;**afData.afBoundData.data.name1**，此欄位指的是已提交適用性表單的JSON結構系結。

## 設定最適化表單提交{#configure-adaptive-form-submission}

執行下列步驟，將最適化表單提交至您在前一節中建立的工作流程模型：

1. 選擇&#x200B;**[!UICONTROL Forms & Documents]**&#x200B;中&#x200B;**[!UICONTROL output]**&#x200B;資料夾中可用的已轉換「聯繫人」表單，然後點選&#x200B;**[!UICONTROL Edit]**。

1. 點選&#x200B;**[!UICONTROL Form Container]**&#x200B;然後點選![Configure](assets/configure_icon.png)，以開啟最適化表單屬性。

1. 在&#x200B;**[!UICONTROL Submission]**&#x200B;區段中，從&#x200B;**[!UICONTROL Submit Action]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL Invoke an AEM workflow]**，選取您在前一節中建立的工作流程模型，並在&#x200B;**[!UICONTROL Data File Path]**&#x200B;欄位中指定&#x200B;**data.xml**。

1. 點選![儲存](assets/save_icon.png)以儲存屬性。

1. 點選&#x200B;**[!UICONTROL Preview]**，在最適化表單欄位中輸入值，然後點選&#x200B;**[!UICONTROL Submit]**。 提交的值現在顯示在MYSQL資料庫表中，而不是&#x200B;**crx-repository**。

## 設定最適化表單以從資料庫預填值

執行下列步驟以配置最適化表單，以根據表中定義的主鍵預填來自MYSQL資料庫的值（此情況下為電子郵件）:

1. 點選最適化表單中的&#x200B;**E-mail**&#x200B;欄位，然後點選![Edit rule](assets/edit-rules.png)。

1. 點選&#x200B;**[!UICONTROL Create]**&#x200B;並從&#x200B;**[!UICONTROL When]**&#x200B;區段的&#x200B;**[!UICONTROL Select State]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL is changed]**。

1. 在&#x200B;**[!UICONTROL Then]**&#x200B;區段中，選取&#x200B;**[!UICONTROL Invoke Service]**&#x200B;和&#x200B;**get**&#x200B;作為您在本文前一節中建立的表單資料模型服務。

1. 在&#x200B;**[!UICONTROL Input]**&#x200B;部分選擇&#x200B;**電子郵件**，並在&#x200B;**[!UICONTROL Output]**&#x200B;部分選擇表單資料模型的其餘三個欄位： **名稱**、**電話號碼**&#x200B;和&#x200B;**問題說明**。 點選&#x200B;**[!UICONTROL Done]**&#x200B;以儲存設定。

   ![配置電子郵件預填設定](assets/email_prefill_settings.png)

   因此，您可以根據MYSQL資料庫中現有的電子郵件條目，在最適化表單的&#x200B;**[!UICONTROL Preview]**&#x200B;模式中預填其餘三個欄位的值。 例如，如果您在&#x200B;**E-mail**&#x200B;欄位中指定aya.tan@xyz.com（根據本文[Prepare form data model](#prepare-data-for-form-model)區段中的現有資料）並在欄位之外指定Tab，則其餘三個欄位（**Name**、**Phone Number**&#x200B;和&#x200B;**Isue Description**）會自動顯示在最適化表單中。

您可以使用下列方式下載範例轉換的最適化表單：

[取得檔案](assets/DownloadedFormsPackage_1498226829041200.zip)
