---
title: 將具有JSON架構的已轉換的自適應表單提交到資料庫
description: 通過建立表單資料模型並在工作流中引用它，將具有JSON架構的已轉換自適應表單提交到數AEM據庫。
uuid: f98b4cca-f0a3-4db8-aef2-39b8ae462628
topic-tags: forms
discoiquuid: cad72699-4a4b-4c52-88a5-217298490a7c
exl-id: 5447b66f-9fac-476f-ab8a-9290bb1f9c0d
source-git-commit: 1a3f79925f25dcc7dbe007f6e634f6e3a742bf72
workflow-type: tm+mt
source-wordcount: '1504'
ht-degree: 2%

---

# 使用 AEM 工作流程整合最適化表單與資料庫 {#submit-forms-to-database-using-forms-portal}

automated forms conversion服務允許您將非互動式PDF表單、Acro表單或基於XFA的PDF表單轉換為自適應表單。 在啟動轉換過程時，可以選擇生成帶資料綁定或不帶資料綁定的自適應表單。

如果選擇生成沒有資料綁定的自適應表單，則轉換後可將轉換後的自適應表單與表單資料模型、XML架構或JSON架構整合。 對於表單資料模型，需要手動將自適應表單域與表單資料模型綁定。 但是，如果生成具有資料綁定的自適應表單，則轉換服務會自動將自適應表單與JSON架構關聯，並在自適應表單和JSON架構中可用的欄位之間建立資料綁定。 然後，您可以將自適應表單與您選擇的資料庫整合，在表單中填充資料，然後將其提交到資料庫。 同樣，在成功與資料庫整合後，可以配置轉換後的自適應表單中的欄位，以從資料庫中檢索值並預填充自適應表單欄位。

下圖描述了將轉換後的自適應表單與資料庫整合的不同階段：

![資料庫整合](assets/integrate-adaptive-form-with-database.png)

本文介紹了成功執行所有這些整合階段的逐步說明。

## 先決條件 {#pre-requisites}

* 設定AEM6.4或6.5作者實例
* 安裝 [最新服務包](https://helpx.adobe.com/tw/experience-manager/aem-releases-updates.html) 你AEM的
* AEM Forms附加軟體包的最新版本
* 配置 [automated forms conversion服務](configure-service.md)
* 設定資料庫。 示例實現中使用的資料庫是MySQL 5.6.24。但是，可以將轉換後的自適應表單與您選擇的任何資料庫整合。

## 示例自適應窗體 {#sample-adaptive-form}

要執行使用案例以使用工作流將轉換的自適應表單與資料AEM庫整合，請下載以下示例PDF檔案。

您可以使用以下方式下載示例「聯繫我們」表單：

[取得檔案](assets/sample_contact_us_form.pdf)

PDF檔案用作Automated forms conversion服務的輸入。 服務將此檔案轉換為自適應格式。 下圖以PDF格式描述了示例聯繫人窗體。

![示例貸款申請表](assets/sample_contact_us_form.png)

## 安裝mysql-connector-java-5.1.39-bin.jar檔案 {#install-mysql-connector-java-file}

在所有作者和發佈實例上執行以下步驟以安裝mysql-connector-java-5.1.39-bin.jar檔案：

1. 導航到 `http://server:port/system/console/depfinder` 並搜索com.mysql.jdbc包。
1. 在「導出者」(Exported by)列中，檢查包是否由任何捆綁包導出。 如果包未由任何包導出，則繼續。
1. 導航到 `http://server:port/system/console/bundles` 按一下 **[!UICONTROL Install/Update]**。
1. 按一下 **[!UICONTROL Choose File]** 並瀏覽以選擇mysql-connector-java-5.1.39-bin.jar檔案。 另外，選擇 **[!UICONTROL Start Bundle]** 和 **[!UICONTROL Refresh Packages]** 複選框。
1. 按一下 **[!UICONTROL Install]** 或 **[!UICONTROL Update]**。 完成後，重新啟動伺服器。
1. （僅限Windows）關閉作業系統的系統防火牆。

## 為表單模型準備資料 {#prepare-data-for-form-model}

AEM Forms資料整合允許您配置和連接到不同的資料源。 使用轉換過程生成自適應表單後，可以基於表單資料模型、XSD或JSON架構定義表單模型。 可以使用資料庫、Microsoft動態或任何其他第三方服務來建立表單資料模型。

本教程使用MySQL資料庫作為源建立表單資料模型。 在資料庫中建立架構並添加 **聯繫人** 表到基於自適應表單中可用欄位的模式。

![示例資料mysql](assets/db_entries_sample_form.png)

可以使用以下DDL語句建立 **聯繫人** 表格。

```sql
CREATE TABLE `contactus` (
   `name` varchar(45) NOT NULL,
   `email` varchar(45) NOT NULL,
   `phonenumber` varchar(10) DEFAULT NULL,
   `issuedesc` varchar(1000) DEFAULT NULL,
   PRIMARY KEY (`email`)
 ) ENGINE=InnoDB DEFAULT CHARSET=utf8
```

## 配置實例和數AEM據庫之間的連接 {#configure-connection-between-aem-instance-and-database}

執行以下配置步驟以在實例和MYSQL數AEM據庫之間建立連接：

1. 轉至AEMWeb Console「配置」頁 `http://server:port/system/console/configMgr`。
1. 查找並按一下以開啟 **[!UICONTROL Apache Sling Connection Pooled DataSource]** 在「Web Console Configuration（Web控制台配置）」中，在「編輯」模式下。 指定屬性的值，如下表所述：

   <table> 
    <tbody> 
    <tr> 
    <th><strong>屬性</strong></th> 
    <th><strong>值</strong></th> 
    </tr> 
    <tr> 
    <td><p>資料源名稱</p></td> 
    <td><p>用於從資料源池篩選驅動程式的資料源名稱。</p></td>
    </tr>
    <tr> 
    <td><p>JDBC驅動程式類</p></td> 
    <td><p>com.mysql.jdbc.Driver</p></td>
    </tr>
    <tr> 
    <td><p>JDBC連接URI</p></td> 
    <td><p>jdbc:mysql://[主機]:[port]/[schema_name]</p></td>
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
    <td><p>已提交讀取</p></td>
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
    <td><p>最大等待時間</p></td> 
    <td><p>100000</p></td>
    </tr>
     <tr> 
    <td><p>Test借用</p></td> 
    <td><p>已核取</p></td>
    </tr>
     <tr> 
    <td><p>Test空閒時</p></td> 
    <td><p>已核取</p></td>
    </tr>
     <tr> 
    <td><p>驗證查詢</p></td> 
    <td><p>示例值為SELECT 1(mysql)、從雙(oracle)中選擇1、SELECT 1(MS Sql Server)(validationQuery)</p></td>
    </tr>
     <tr> 
    <td><p>驗證查詢超時</p></td> 
    <td><p>10000</p></td>
    </tr>
    </tbody> 
    </table>

## 建立表單資料模型 {#create-form-data-model}

將MYSQL配置為資料源後，請執行以下步驟建立表單資料模型：

1. 在作AEM者實例中，導航到 **[!UICONTROL Forms]** > **[!UICONTROL Data Integrations]**。

1. 點擊 **[!UICONTROL Create]** > **[!UICONTROL Form Data Model]**。

1. 在 **[!UICONTROL Create Form Data Model]** 嚮導，指定 **工作流_提交** 作為窗體資料模型的名稱。 點選 **[!UICONTROL Next]**。

1. 選擇在上一節中配置的MYSQL資料源，然後點擊 **[!UICONTROL Create]**。

1. 點擊 **[!UICONTROL Edit]** 並展開左窗格中列出的資料源以選擇 **聯繫人** 表格 **[!UICONTROL get]**, **[!UICONTROL insert]** 服務和點擊 **[!UICONTROL Add Selected]**。

   ![示例資料mysql](assets/fdm_details_workfdlow_submit.png)

1. 在右窗格中選擇資料模型對象，然後點擊 **[!UICONTROL Edit Properties]**。 選擇 **[!UICONTROL get]** 和 **[!UICONTROL insert]** 從 **[!UICONTROL Read Service]** 和 **[!UICONTROL Write Service]** 下拉清單。 指定讀取服務的參數並點擊 **[!UICONTROL Done]**。

1. 在 **[!UICONTROL Services]** 頁籤 **[!UICONTROL get]** 服務和點擊 **[!UICONTROL Edit Properties]**。 選擇 **[!UICONTROL Output Model Object]**，禁用 **[!UICONTROL Return array]** 切換，然後點擊 **[!UICONTROL Done]**。

1. 選擇 **[!UICONTROL Insert]** 服務和點擊 **[!UICONTROL Edit Properties]**。 選擇 **[!UICONTROL Input Model Object]** 點擊 **[!UICONTROL Done]**。

1. 點擊 **[!UICONTROL Save]** 來修改標籤元素的屬性。

您可以使用以下方式下載示例表單資料模型：

[取得檔案](assets/DownloadedFormsPackage_1497728018502500.zip)

## 使用JSON綁定生成自適應表單 {#generate-adaptive-forms-with-json-binding}

使用 [automated forms conversion服務要轉換](convert-existing-forms-to-adaptive-forms.md) 這樣 [聯繫我們表單](#sample-adaptive-form) 到具有資料綁定的自適應窗體。 確保不選擇 **[!UICONTROL Generate adaptive form(s) without data bindings]** 的子菜單。

![具有JSON綁定的自適應窗體](assets/generate_af_with_data_bindings.png)

選擇已轉換 **聯繫我們表單** 的 **[!UICONTROL output]** 資料夾 **[!UICONTROL Forms & Documents]** 點擊 **[!UICONTROL Edit]**。 點擊 **[!UICONTROL Preview]**，在自適應窗體欄位中輸入值並點擊 **[!UICONTROL Submit]**。

登錄到 **crx儲存庫** 導航 */content/forms/fp/admin/submit/data* 以JSON格式查看提交的值。 以下是提交轉換後的JSON格式的示例資料 **聯繫我們** 自適應格式：

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

## 建立工作流模型以處理JSON資料 {#create-workflow-model}

執行以下步驟以建立工作流模型以將自適應表單資料提交到資料庫：

1. 開啟「工作流模型」控制台。 預設URL為 `https://server:port/libs/cq/workflow/admin/console/content/models.html/etc/workflow/models`。

1. 選擇 **[!UICONTROL Create]**，則 **[!UICONTROL Create Model]**。 的 **[!UICONTROL Add Workflow Model]** 對話框。

1. 輸入 **[!UICONTROL Title]** 和 **[!UICONTROL Name]** （可選）。 比如說， **工作流_json_submit**。 點擊 **[!UICONTROL Done]** 的子菜單。

1. 選擇工作流模型並點擊 **[!UICONTROL Edit]** 以編輯模式開啟模型。 點擊+並添加 **[!UICONTROL Invoke Form Data Model Service]** 的子菜單。

1. 點擊 **[!UICONTROL Invoke Form Data Model Service]** 步驟和點擊 ![配置](assets/configure_icon.png)。

1. 在 **[!UICONTROL Form Data Model]** 頁籤，選擇在 **[!UICONTROL Form Data Model path]** 選擇 **[!UICONTROL insert]** 從 **[!UICONTROL Service]** 的子菜單。

1. 在 **[!UICONTROL Input for Service]** 頁籤 **[!UICONTROL Provide input data using literal, variable, or a workflow metadata, and a JSON file]** 從下拉清單中，選擇 **[!UICONTROL Map input fields from input JSON]** 複選框，選擇 **[!UICONTROL Relative to payload]**，提供 **data.xml** 值 **[!UICONTROL Select input JSON document using]** 的子菜單。

1. 在 **[!UICONTROL Service Arguments]** 部分，為表單資料模型參數提供以下值：

   ![啟動表單資料模型服務](assets/invoke_form_data_model_service.png)

   請注意，表單資料模型欄位（例如，contacttus點名）被映射到 **afData.afBoundData.data.name1**，它指提交的自適應表單的JSON架構綁定。

## 配置自適應表單提交 {#configure-adaptive-form-submission}

執行以下步驟，將自適應表單提交到您在上一節中建立的工作流模型：

1. 選擇在中可用的轉換的「聯繫我們」表單 **[!UICONTROL output]** 資料夾 **[!UICONTROL Forms & Documents]** 點擊 **[!UICONTROL Edit]**。

1. 通過點擊開啟自適應窗體屬性 **[!UICONTROL Form Container]** 然後敲 ![配置](assets/configure_icon.png)。

1. 在 **[!UICONTROL Submission]** 選擇 **[!UICONTROL Invoke an AEM workflow]** 從 **[!UICONTROL Submit Action]** 下拉清單中，選擇在上一節中建立的工作流模型，然後指定 **data.xml** 的 **[!UICONTROL Data File Path]** 的子菜單。

1. 點擊 ![保存](assets/save_icon.png) 的子菜單。

1. 點擊 **[!UICONTROL Preview]**，在自適應窗體欄位中輸入值並點擊 **[!UICONTROL Submit]**。 提交的值現在顯示在MYSQL資料庫表中，而不是 **crx儲存庫**。

## 配置自適應表單以從資料庫中預填充值

執行以下步驟，根據表中定義的主鍵（本例中為「電子郵件」），將自適應表單配置為從MYSQL資料庫預填充值：

1. 點擊 **電子郵件** 自適應窗體和抽頭 ![編輯規則](assets/edit-rules.png)。

1. 點擊 **[!UICONTROL Create]** 選擇 **[!UICONTROL is changed]** 從 **[!UICONTROL Select State]** 下拉清單 **[!UICONTROL When]** 的子菜單。

1. 在 **[!UICONTROL Then]** 選擇 **[!UICONTROL Invoke Service]** 和 **得** 作為您在本文章上一節中建立的表單資料模型的服務。

1. 選擇 **電子郵件** 的 **[!UICONTROL Input]** 以及表格資料模型的其餘三個欄位， **名稱**。 **電話號碼**, **問題說明** 的 **[!UICONTROL Output]** 的子菜單。 點擊 **[!UICONTROL Done]** 按鈕。

   ![配置電子郵件預填充設定](assets/email_prefill_settings.png)

   因此，根據MYSQL資料庫中現有的電子郵件條目，您可以預填中其餘三個欄位的值 **[!UICONTROL Preview]** 的子菜單。 例如，如果在 **電子郵件** 欄位(基於 [準備表單資料模型](#prepare-data-for-form-model) )和頁籤， **名稱**。 **電話號碼**, **問題說明** 在自適應窗體中自動顯示。

可以使用以下方式下載示例轉換的自適應表單：

[取得檔案](assets/DownloadedFormsPackage_1498226829041200.zip)
