---
title: 將轉換後的適用性表單與JSON結構描述提交至資料庫
description: 透過建立表單資料模型並在AEM工作流程中參照它，將轉換後的適用性表單與JSON結構描述提交至資料庫。
solution: Experience Manager Forms
feature: Adaptive Forms
topic: Administration
topic-tags: forms
role: Admin, Developer
level: Beginner, Intermediate
exl-id: 5447b66f-9fac-476f-ab8a-9290bb1f9c0d
source-git-commit: c2392932d1e29876f7a11bd856e770b8f7ce3181
workflow-type: tm+mt
source-wordcount: '1506'
ht-degree: 1%

---

# 使用AEM工作流程整合最適化表單與資料庫 {#submit-forms-to-database-using-forms-portal}

automated forms conversion服務(AFCS)可讓您將非互動式PDF表單、Acro表單或XFAPDF表單轉換為最適化表單。 起始轉換程式時，您可以選擇產生具有或不具有資料繫結的最適化表單。

如果您選擇產生沒有資料繫結的調適型表單，則可以在轉換後整合已轉換的調適型表單與表單資料模型、XML結構描述或JSON結構描述。 對於表單資料模型，您需要手動將最適化表單欄位與表單資料模型繫結。 不過，如果您產生具有資料繫結的調適型表單，轉換服務會自動將調適型表單與JSON結構描述建立關聯，並在調適型表單和JSON結構描述中可用的欄位之間建立資料繫結。 然後，您可以將最適化表單與您選擇的資料庫整合、在表單中填寫資料，並將資料提交至資料庫。 同樣地，成功與資料庫整合後，您可以在轉換後的調適型表單中設定欄位，以從資料庫擷取值並預填調適型表單欄位。

下圖說明將轉換後的適用性表單與資料庫整合的不同階段：

![資料庫整合](assets/integrate-adaptive-form-with-database.png)

本文會說明如何成功執行所有這些整合階段的逐步指示。

## 必要條件 {#pre-requisites}

* 設定AEM 6.4或6.5編寫執行個體
* 為您的AEM執行個體安裝[最新Service Pack](https://helpx.adobe.com/tw/experience-manager/aem-releases-updates.html)
* 最新版本的AEM Forms附加元件套件
* 設定[Automated forms conversion服務](configure-service.md)
* 設定資料庫。 範例實作中使用的資料庫是MySQL 5.6.24。不過，您可以將轉換後的最適化表單與您選擇的任何資料庫整合。

## 最適化表單範例 {#sample-adaptive-form}

若要執行使用案例以使用AEM工作流程將轉換後的適用性表單與資料庫整合，請下載以下範例PDF檔案。

您可以使用以下下載範例「聯絡我們」表單：

[取得檔案](assets/sample_contact_us_form.pdf)

PDF檔案可作為Automated forms conversion服務(AFCS)的輸入。 此服務會將此檔案轉換為最適化表單。 下圖是以PDF格式呈現的範例連絡人表格。

![貸款申請表範例](assets/sample_contact_us_form.png)

## 安裝mysql-connector-java-5.1.39-bin.jar檔案 {#install-mysql-connector-java-file}

在所有作者和發佈執行個體上執行以下步驟，以安裝mysql-connector-java-5.1.39-bin.jar檔案：

1. 瀏覽至`http://server:port/system/console/depfinder`並搜尋com.mysql.jdbc套件。
1. 在「匯出者」欄中，檢查封裝是否由任何束匯出。 如果套件未由任何套件組合匯出，請繼續。
1. 瀏覽至`http://server:port/system/console/bundles`並按一下&#x200B;**[!UICONTROL Install/Update]**。
1. 按一下&#x200B;**[!UICONTROL Choose File]**&#x200B;並瀏覽以選取mysql-connector-java-5.1.39-bin.jar檔案。 此外，選取&#x200B;**[!UICONTROL Start Bundle]**&#x200B;和&#x200B;**[!UICONTROL Refresh Packages]**&#x200B;核取方塊。
1. 按一下&#x200B;**[!UICONTROL Install]**&#x200B;或&#x200B;**[!UICONTROL Update]**。 完成後，請重新啟動伺服器。
1. （僅限Windows）關閉作業系統的系統防火牆。

## 為表單模型準備資料 {#prepare-data-for-form-model}

AEM Forms資料整合可讓您設定並連線至不同的資料來源。 使用轉換程式產生最適化表單後，您可以根據表單資料模型、XSD或JSON結構描述定義表單模型。 您可以使用資料庫、Microsoft Dynamics或任何其他協力廠商服務來建立表單資料模型。

本教學課程使用MySQL資料庫作為建立表單資料模型的來源。 在資料庫中建立結構描述，並根據最適化表單中可用的欄位，將&#x200B;**contactus**&#x200B;資料表新增到結構描述中。

![範例資料mysql](assets/db_entries_sample_form.png)

您可以使用下列DDL敘述句在資料庫中建立&#x200B;**contactus**&#x200B;資料表。

```sql
CREATE TABLE `contactus` (
   `name` varchar(45) NOT NULL,
   `email` varchar(45) NOT NULL,
   `phonenumber` varchar(10) DEFAULT NULL,
   `issuedesc` varchar(1000) DEFAULT NULL,
   PRIMARY KEY (`email`)
 ) ENGINE=InnoDB DEFAULT CHARSET=utf8
```

## 設定AEM執行個體與資料庫之間的連線 {#configure-connection-between-aem-instance-and-database}

執行以下設定步驟來建立AEM執行處理與MYSQL資料庫之間的連線：

1. 移至`http://server:port/system/console/configMgr`的AEM Web主控台設定頁面。
1. 在Web主控台組態中尋找並按一下以編輯模式開啟&#x200B;**[!UICONTROL Apache Sling Connection Pooled DataSource]**。 指定特性值，如下表所述：

   <table> 
    <tbody> 
    <tr> 
    <th><strong>屬性</strong></th> 
    <th><strong>值</strong></th> 
    </tr> 
    <tr> 
    <td><p>資料來源名稱</p></td> 
    <td><p>從資料來源集區篩選驅動程式的資料來源名稱。</p></td>
    </tr>
    <tr> 
    <td><p>JDBC驅動程式類別</p></td> 
    <td><p>com.mysql.jdbc.Driver</p></td>
    </tr>
    <tr> 
    <td><p>JDBC連線URI</p></td> 
    <td><p>jdbc:mysql://[host]：[port]/[schema_name]</p></td>
    </tr>
    <tr> 
    <td><p>使用者名稱</p></td> 
    <td><p>用於驗證資料庫表格並執行動作的使用者名稱</p></td>
    </tr>
    <tr> 
    <td><p>密碼</p></td> 
    <td><p>與使用者名稱關聯的密碼</p></td>
    </tr>
    <tr> 
    <td><p>交易隔離</p></td> 
    <td><p>READ_COMMITTED</p></td>
    </tr>
    <tr> 
    <td><p>最大使用中連線</p></td> 
    <td><p>1000</p></td>
    </tr>
    <tr> 
    <td><p>最大閒置連線</p></td> 
    <td><p>100</p></td>
    </tr>
    <tr> 
    <td><p>最小閒置連線</p></td> 
    <td><p>10</p></td>
    </tr>
    <tr> 
    <td><p>初始大小</p></td> 
    <td><p>10</p></td>
    </tr>
    <tr> 
    <td><p>等待上限</p></td> 
    <td><p>100000</p></td>
    </tr>
     <tr> 
    <td><p>借入時測試</p></td> 
    <td><p>已核取</p></td>
    </tr>
     <tr> 
    <td><p>閒置時測試</p></td> 
    <td><p>已核取</p></td>
    </tr>
     <tr> 
    <td><p>驗證查詢</p></td> 
    <td><p>範例值為SELECT 1(mysql)、select 1 from dual(oracle)、SELECT 1(MS Sql Server) (validationQuery)</p></td>
    </tr>
     <tr> 
    <td><p>驗證查詢逾時</p></td> 
    <td><p>10000</p></td>
    </tr>
    </tbody> 
    </table>

## 建立表單資料模型 {#create-form-data-model}

設定MYSQL做為資料來源後，請執行以下步驟來建立表單資料模型：

1. 在AEM作者執行個體中，瀏覽至&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL Data Integrations]**。

1. 點選&#x200B;**[!UICONTROL Create]** > **[!UICONTROL Form Data Model]**。

1. 在&#x200B;**[!UICONTROL Create Form Data Model]**&#x200B;精靈中，將&#x200B;**workflow_submit**&#x200B;指定為表單資料模型的名稱。 點選&#x200B;**[!UICONTROL Next]**。

1. 選取您在上一節中設定的MYSQL資料來源，然後點選&#x200B;**[!UICONTROL Create]**。

1. 點選&#x200B;**[!UICONTROL Edit]**&#x200B;並展開左窗格中列出的資料來源，以選取&#x200B;**contactus**&#x200B;表格、**[!UICONTROL get]**&#x200B;和&#x200B;**[!UICONTROL insert]**&#x200B;服務，然後點選&#x200B;**[!UICONTROL Add Selected]**。

   ![範例資料mysql](assets/fdm_details_workfdlow_submit.png)

1. 在右窗格中選取資料模型物件，然後點選&#x200B;**[!UICONTROL Edit Properties]**。 從&#x200B;**[!UICONTROL Read Service]**&#x200B;和&#x200B;**[!UICONTROL Write Service]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL get]**&#x200B;和&#x200B;**[!UICONTROL insert]**。 指定讀取服務的引數，然後點選&#x200B;**[!UICONTROL Done]**。

1. 在&#x200B;**[!UICONTROL Services]**&#x200B;標籤中，選取&#x200B;**[!UICONTROL get]**&#x200B;服務並點選&#x200B;**[!UICONTROL Edit Properties]**。 選取&#x200B;**[!UICONTROL Output Model Object]**、停用&#x200B;**[!UICONTROL Return array]**&#x200B;切換功能，然後點選&#x200B;**[!UICONTROL Done]**。

1. 選取&#x200B;**[!UICONTROL Insert]**&#x200B;服務並點選&#x200B;**[!UICONTROL Edit Properties]**。 選取&#x200B;**[!UICONTROL Input Model Object]**&#x200B;並點選&#x200B;**[!UICONTROL Done]**。

1. 點選&#x200B;**[!UICONTROL Save]**&#x200B;以儲存表單資料模型。

您可以使用以下下載範例表單資料模型：

[取得檔案](assets/DownloadedFormsPackage_1497728018502500.zip)

## 產生具有JSON繫結的最適化表單 {#generate-adaptive-forms-with-json-binding}

使用[Automated forms conversion服務(AFCS)將](convert-existing-forms-to-adaptive-forms.md) [聯絡我們表單](#sample-adaptive-form)轉換為具有資料繫結的最適化表單。 確保在產生最適化表單時不要選取&#x200B;**[!UICONTROL Generate adaptive form(s) without data bindings]**&#x200B;核取方塊。

![具有JSON繫結的最適化表單](assets/generate_af_with_data_bindings.png)

選取可在&#x200B;**[!UICONTROL Forms & Documents]**&#x200B;的&#x200B;**[!UICONTROL output]**&#x200B;資料夾中取得的&#x200B;**連絡我們表單**，然後點選&#x200B;**[!UICONTROL Edit]**。 點選&#x200B;**[!UICONTROL Preview]**，在最適化表單欄位中輸入值，然後點選&#x200B;**[!UICONTROL Submit]**。

登入&#x200B;**crx-repository**&#x200B;並導覽至&#x200B;*/content/forms/fp/admin/submit/data*，以檢視JSON格式的提交值。 以下是您提交轉換的&#x200B;**聯絡我們**&#x200B;最適化表單時，JSON格式的範例資料：

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

您需要立即建立工作流程模型，以便處理此資料，並使用您在前幾節中建立的表單資料模型將其提交至MYSQL資料庫。

## 建立工作流程模型以處理JSON資料 {#create-workflow-model}

執行以下步驟來建立工作流程模型，以將最適化表單資料提交至資料庫：

1. 開啟「工作流程模型」主控台。 預設URL為`https://server:port/libs/cq/workflow/admin/console/content/models.html/etc/workflow/models`。

1. 選取&#x200B;**[!UICONTROL Create]**，然後選取&#x200B;**[!UICONTROL Create Model]**。 **[!UICONTROL Add Workflow Model]**&#x200B;對話方塊隨即顯示。

1. 輸入&#x200B;**[!UICONTROL Title]**&#x200B;和&#x200B;**[!UICONTROL Name]** （選擇性）。 例如，**workflow_json_submit**。 點選&#x200B;**[!UICONTROL Done]**&#x200B;以建立模型。

1. 選取工作流程模型並點選&#x200B;**[!UICONTROL Edit]**&#x200B;以在編輯模式中開啟模型。 點選+並將&#x200B;**[!UICONTROL Invoke Form Data Model Service]**&#x200B;步驟新增至工作流程模型。

1. 點選&#x200B;**[!UICONTROL Invoke Form Data Model Service]**&#x200B;步驟並點選![設定](assets/configure_icon.png)。

1. 在&#x200B;**[!UICONTROL Form Data Model]**&#x200B;索引標籤中，選取您在&#x200B;**[!UICONTROL Form Data Model path]**&#x200B;欄位中建立的表單資料模型，並從&#x200B;**[!UICONTROL Service]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL insert]**。

1. 在&#x200B;**[!UICONTROL Input for Service]**&#x200B;索引標籤中，從下拉式清單中選取&#x200B;**[!UICONTROL Provide input data using literal, variable, or a workflow metadata, and a JSON file]**，選取&#x200B;**[!UICONTROL Map input fields from input JSON]**&#x200B;核取方塊，選取&#x200B;**[!UICONTROL Relative to payload]**，並提供&#x200B;**data.xml**&#x200B;作為&#x200B;**[!UICONTROL Select input JSON document using]**&#x200B;欄位的值。

1. 在&#x200B;**[!UICONTROL Service Arguments]**&#x200B;區段中，為表單資料模型引數提供下列值：

   ![啟動表單資料模型服務](assets/invoke_form_data_model_service.png)

   請注意，表單資料模型欄位（例如contactus dot name）對應至&#x200B;**afData.afBoundData.data.name1**，這表示已提交的最適化表單的JSON結構描述繫結。

## 設定最適化表單提交 {#configure-adaptive-form-submission}

執行以下步驟，將最適化表單提交至您在前一節中建立的工作流程模型：

1. 選取&#x200B;**[!UICONTROL Forms & Documents]**&#x200B;中&#x200B;**[!UICONTROL output]**&#x200B;資料夾中可用的轉換連絡人表單，然後點選&#x200B;**[!UICONTROL Edit]**。

1. 點選&#x200B;**[!UICONTROL Form Container]**，然後點選![設定](assets/configure_icon.png)，開啟最適化表單屬性。

1. 在&#x200B;**[!UICONTROL Submission]**&#x200B;區段中，從&#x200B;**[!UICONTROL Submit Action]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL Invoke an AEM workflow]**，選取您在上一區段中建立的工作流程模型，並在&#x200B;**[!UICONTROL Data File Path]**&#x200B;欄位中指定&#x200B;**data.xml**。

1. 點選![儲存](assets/save_icon.png)以儲存屬性。

1. 點選&#x200B;**[!UICONTROL Preview]**，在最適化表單欄位中輸入值，然後點選&#x200B;**[!UICONTROL Submit]**。 送出的值現在顯示在MYSQL資料庫表格中，而非&#x200B;**crx-repository**。

## 設定最適化表單以預填資料庫的值

執行以下步驟來設定最適化表單，以根據表格中定義的主索引鍵從MYSQL資料庫預先填入值（在此案例中為電子郵件）：

1. 點選最適化表單中的&#x200B;**電子郵件**&#x200B;欄位，然後點選![編輯規則](assets/edit-rules.png)。

1. 點選&#x200B;**[!UICONTROL Create]**&#x200B;並從&#x200B;**[!UICONTROL When]**&#x200B;區段的&#x200B;**[!UICONTROL Select State]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL is changed]**。

1. 在&#x200B;**[!UICONTROL Then]**&#x200B;區段中，選取&#x200B;**[!UICONTROL Invoke Service]**&#x200B;和&#x200B;**get**&#x200B;作為您在此文章前一個區段中建立的表單資料模型的服務。

1. 在&#x200B;**[!UICONTROL Input]**&#x200B;區段中選取&#x200B;**電子郵件**，並在&#x200B;**[!UICONTROL Output]**&#x200B;區段中選取表單資料模型的其餘三個欄位、**名稱**、**電話號碼**&#x200B;以及&#x200B;**問題說明**。 點選&#x200B;**[!UICONTROL Done]**&#x200B;以儲存設定。

   ![設定電子郵件預填設定](assets/email_prefill_settings.png)

   因此，您可以根據MYSQL資料庫中現有的電子郵件專案，以最適化表單的&#x200B;**[!UICONTROL Preview]**&#x200B;模式預先填入其餘三個欄位的值。 例如，如果您在&#x200B;**電子郵件**&#x200B;欄位中指定aya.tan@xyz.com （根據本文的[準備表單資料模型](#prepare-data-for-form-model)區段中的現有資料）並以標籤退出欄位，其餘三個欄位（**名稱**、**電話號碼**&#x200B;和&#x200B;**問題說明**）會自動顯示在最適化表單中。

您可使用以下方式下載範例轉換後的最適化表單：

[取得檔案](assets/DownloadedFormsPackage_1498226829041200.zip)
