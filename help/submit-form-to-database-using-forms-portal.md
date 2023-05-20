---
title: 使用Forms門戶向資料庫提交自適應表單
description: 擴展預設元模型，以添加特定於您的組織的模式、驗證和實體，並在運行Automated forms conversion服務時將配置應用於自適應表單域。
uuid: f98b4cca-f0a3-4db8-aef2-39b8ae462628
topic-tags: forms
discoiquuid: cad72699-4a4b-4c52-88a5-217298490a7c
source-git-commit: ead1b4ee177029c60f095dc596b1f3db5878760e
workflow-type: tm+mt
source-wordcount: '1152'
ht-degree: 1%

---


# 使用Forms門戶將自適應表單與資料庫整合 {#submit-forms-to-database-using-forms-portal}

automated forms conversion服務允許您將非互動式PDF表單、Acro表單或基於XFA的PDF表單轉換為自適應表單。 在啟動轉換過程時，可以選擇生成帶資料綁定或不帶資料綁定的自適應表單。

如果選擇生成沒有資料綁定的自適應表單，則轉換後可將轉換後的自適應表單與表單資料模型、XML架構或JSON架構整合。 但是，如果生成具有資料綁定的自適應表單，則轉換服務會自動將自適應表單與JSON架構關聯，並在自適應表單和JSON架構中可用的欄位之間建立資料綁定。 然後，您可以將自適應表單與您選擇的資料庫整合，在表單中填充資料，然後使用Forms門戶將其提交到資料庫。

下圖描述了使用Forms門戶將轉換的自適應表單與資料庫整合的不同階段：

![資料庫整合](assets/database_integration.gif)

本文介紹了成功執行所有這些整合階段的逐步說明。

本文討論的示例是定制資料和元資料服務的參考實現，以將Forms門戶頁面與資料庫整合。 示例實現中使用的資料庫是MySQL 5.6.24。但是，您可以將Forms門戶頁面與您選擇的任何資料庫整合。

## 先決條件 {#pre-requisites}

* 設定AEM6.4或6.5作者實例
* 安裝 [最新服務包](https://helpx.adobe.com/tw/experience-manager/aem-releases-updates.html) 你AEM的
* AEM Forms附加軟體包的最新版本
* 配置 [automated forms conversion服務](configure-service.md)
* 設定資料庫。 示例實現中使用的資料庫是MySQL 5.6.24。但是，可以將轉換後的自適應表單與您選擇的任何資料庫整合。

## 設定實例和資料AEM庫之間的連接 {#set-up-connection-aem-instance-database}

設定實例與MYSQL數AEM據庫之間的連接包括：

* [安裝MYSQL連接器包](#install-mysql-connector-java-file)

* [在資料庫中建立架構和表](#create-schema-and-tables-in-database)

* [配置連接設定](#configure-connection-between-aem-instance-and-database)

* [設定和配置用於Forms門戶整合的示例包](#set-up-and-configure-sample)

### 安裝mysql-connector-java-5.1.39-bin.jar檔案 {#install-mysql-connector-java-file}

在所有作者和發佈實例上執行以下步驟以安裝mysql-connector-java-5.1.39-bin.jar檔案：

1. 導航到http://[伺服器]:[埠]/system/console/depfinder並搜索com.mysql.jdbc包。
1. 在「導出者」(Exported by)列中，檢查包是否由任何捆綁包導出。 如果包未由任何包導出，則繼續。
1. 導航到http://[伺服器]:[埠]/system/console/bundles，按一下 **[!UICONTROL Install/Update]**。
1. 按一下 **[!UICONTROL Choose File]** 並瀏覽以選擇mysql-connector-java-5.1.39-bin.jar檔案。 另外，選擇 **[!UICONTROL Start Bundle]** 和 **[!UICONTROL Refresh Packages]** 複選框。
1. 按一下 **[!UICONTROL Install]** 或 **[!UICONTROL Update]**。 完成後，重新啟動伺服器。
1. （僅限Windows）關閉作業系統的系統防火牆。

### 在資料庫中建立架構和表 {#create-schema-and-tables-in-database}

執行以下步驟在資料庫中建立模式和表：

1. 使用以下SQL陳述式在資料庫中建立架構：

   ```sql
   CREATE SCHEMA `formsportal` ;
   ```

   何處 **表單門戶** 引用架構的名稱。

1. 建立 **資料** 資料庫架構中使用以下SQL陳述式的表：

   ```sql
    CREATE TABLE `data` (
        `owner` varchar(255) DEFAULT NULL,
        `data` longblob,
        `metadataId` varchar(45) DEFAULT NULL,
        `id` varchar(45) NOT NULL,
        PRIMARY KEY (`id`)
        ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

1. 建立 **元資料** 資料庫架構中使用以下SQL陳述式的表：

   ```sql
   CREATE TABLE `metadata` (
       `formPath` varchar(1000) DEFAULT NULL,
       `formType` varchar(100) DEFAULT NULL,
       `description` text,
       `formName` varchar(255) DEFAULT NULL,
       `owner` varchar(255) DEFAULT NULL,
       `enableAnonymousSave` varchar(45) DEFAULT NULL,
       `renderPath` varchar(1000) DEFAULT NULL,
       `nodeType` varchar(45) DEFAULT NULL,
       `charset` varchar(45) DEFAULT NULL,
       `userdataID` varchar(45) DEFAULT NULL,
       `status` varchar(45) DEFAULT NULL,
       `formmodel` varchar(45) DEFAULT NULL,
       `markedForDeletion` varchar(45) DEFAULT NULL,
       `showDorClass` varchar(255) DEFAULT NULL,
       `sling:resourceType` varchar(1000) DEFAULT NULL,
       `attachmentList` longtext,
       `draftID` varchar(45) DEFAULT NULL,
       `submitID` varchar(45) DEFAULT NULL,
       `id` varchar(60) NOT NULL,
       `profile` varchar(255) DEFAULT NULL,
       `submitUrl` varchar(1000) DEFAULT NULL,
       `xdpRef` varchar(1000) DEFAULT NULL,
       `agreementId` varchar(255) DEFAULT NULL,
       `nextSigners` varchar(255) DEFAULT NULL,
       `eSignStatus` varchar(45) DEFAULT NULL,
       `pendingSignID` varchar(45) DEFAULT NULL,
       `agreementDataId` varchar(255) DEFAULT NULL,
       `enablePortalSubmit` varchar(45) DEFAULT NULL,
       `submitType` varchar(45) DEFAULT NULL,
       `dataType` varchar(45) DEFAULT NULL,
       `jcr:lastModified` varchar(45) DEFAULT NULL,
       PRIMARY KEY (`id`),
       UNIQUE KEY `ID_UNIQUE` (`id`)
       ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

1. 建立 **可附加** 資料庫架構中使用以下SQL陳述式的表：

   ```sql
   CREATE TABLE `additionalmetadatatable` (
       `value` text,
       `key` varchar(255) NOT NULL,
       `id` varchar(60) NOT NULL,
       PRIMARY KEY (`id`,`key`),
       CONSTRAINT ‘additionalmetadatatable_fk’ FOREIGN KEY (`id`) REFERENCES `metadata` (`id`) ON DELETE CASCADE
       ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

1. 建立 **評論** 資料庫架構中使用以下SQL陳述式的表：

   ```sql
   CREATE TABLE `commenttable` (
       `commentId` varchar(255) DEFAULT NULL,
       `comment` text DEFAULT NULL,
       `ID` varchar(255) DEFAULT NULL,
       `commentowner` varchar(255) DEFAULT NULL,
       `time` varchar(255) DEFAULT NULL);
   ```

### 配置實例和數AEM據庫之間的連接 {#configure-connection-between-aem-instance-and-database}

執行以下配置步驟以在實例和MYSQL數AEM據庫之間建立連接：

1. 轉至AEMWeb Console「配置」頁 *http://[主機]:[埠]/system/console/configMgr*。
1. 按一下以開啟 **[!UICONTROL Forms Portal Draft and Submission Configuration]** 的子菜單。
1. 指定屬性的值，如下表所述：

   <table> 
    <tbody> 
    <tr> 
    <th><strong>屬性</strong></th> 
    <th><strong>說明</strong></th>
    <th><strong>值</strong></th> 
    </tr> 
    <tr> 
    <td><p>Forms門戶草稿資料服務</p></td> 
    <td><p>草稿資料服務的標識符</p></td>
    <td><p>formsportal.sampledataservice</p></td> 
    </tr>
    <tr> 
    <td><p>Forms門戶草稿元資料服務</p></td> 
    <td><p>草稿元資料服務的標識符</p></td>
    <td><p>formsportal.samplemetadataservice</p></td> 
    </tr>
    <tr> 
    <td><p>Forms門戶提交資料服務</p></td> 
    <td><p>提交資料服務的標識符</p></td>
    <td><p>formsportal.sampledataservice</p></td> 
    </tr>
    <tr> 
    <td><p>Forms門戶提交元資料服務</p></td> 
    <td><p>提交元資料服務的標識符</p></td>
    <td><p>formsportal.samplemetadataservice</p></td> 
    </tr>
    <tr> 
    <td><p>Forms門戶待簽資料服務</p></td> 
    <td><p>掛起簽名資料服務的標識符</p></td>
    <td><p>formsportal.sampledataservice</p></td> 
    </tr>
    <tr> 
    <td><p>Forms門戶掛起簽名元資料服務</p></td> 
    <td><p>掛起簽名元資料服務的標識符</p></td>
    <td><p>formsportal.samplemetadataservice</p></td> 
    </tr>
    </tbody> 
    </table>
1. 保持其他配置原樣，然後按一下 **[!UICONTROL Save]**。
1. 查找並按一下以開啟 **[!UICONTROL Apache Sling Connection Pooled DataSource]** 在「Web Console Configuration（Web控制台配置）」中，在「編輯」模式下。 指定屬性的值，如下表所述：

   <table> 
    <tbody> 
    <tr> 
    <th><strong>屬性</strong></th> 
    <th><strong>值</strong></th> 
    </tr> 
    <tr> 
    <td><p>資料源名稱</p></td> 
    <td><p>用於從資料源池篩選驅動程式的資料源名稱。 示例實現使用FormsPortal作為資料源名稱。</p></td>
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

### 設定和配置示例 {#set-up-and-configure-sample}

對所有作者和發佈實例執行以下步驟以安裝和配置示例：

1. 下載以下內容 **aem-fp-db-integration-sample-pkg-6.1.2-zip** 檔案系統。

[取得檔案](assets/aem-fp-db-integration-sample-pkg-6.1.2.zip)

1. 轉至AEM包管理器 *http://[主機]:[埠]/crx/packmgr/*。
1. 按一下 **[!UICONTROL Upload Package]**.
1. 瀏覽以選擇 **aem-fp-db-integration-sample-pkg-6.1.2-zip** 包，按一下 **[!UICONTROL OK]**。
1. 按一下 **[!UICONTROL Install]** 的子菜單。

## 為Forms門戶整合配置已轉換的自適應表單 {#configure-converted-adaptive-form-for-forms-portal-integration}

執行以下步驟，以啟用使用Forms門戶頁的自適應表單提交：
1. [運行轉換](convert-existing-forms-to-adaptive-forms.md#start-the-conversion-process) 將源窗體轉換為自適應窗體。
1. 在編輯模式下開啟自適應窗體。
1. 按一下「表單容器」並選擇「配置」 ![配置自適應窗體](assets/configure-adaptive-form.png)。
1. 在 **[!UICONTROL Submission]** 選擇 **[!UICONTROL Forms Portal Submit Action]** 從 **[!UICONTROL Submit Action]** 的子菜單。
1. 點擊 ![保存模板策略](assets/edit_template_done.png) 按鈕。

## 建立和配置Forms門戶頁 {#create-configure-forms-portal-page}

執行以下步驟建立Forms門戶頁並配置該頁，以便您可以使用此頁提交自適應表單：

1. 登錄到作者AEM實例並點擊 **[!UICONTROL Adobe Experience Manager]** >  **[!UICONTROL Sites]**。
1. 選擇要保存新的Forms門戶頁面的位置並點擊 **[!UICONTROL Create]** > **[!UICONTROL Page]**。
1. 選擇頁面模板，點擊 **[!UICONTROL Next]**，指定頁面標題並點擊 **[!UICONTROL Create]**。
1. 點擊 **[!UICONTROL Edit]** 來配置頁面。
1. 在頁眉中，點擊 ![編輯模板](assets/edit_template_sites.png)  > **[!UICONTROL Edit Template]** 開啟頁面的模板。
1. 點擊佈局容器和點擊 ![編輯模板策略](assets/edit_template_policy.png)。 在 **[!UICONTROL Allowed Components]** 頁籤 **[!UICONTROL Document Services]** 和 **[!UICONTROL Document Services Predicates]** 選項，然後點擊 ![保存模板策略](assets/edit_template_done.png)。
1. 插入 **[!UICONTROL Search & Lister]** 的子菜單。 因此，實例上可用的所有現有自適應AEM表單都會列在頁面上。
1. 插入 **[!UICONTROL Drafts & Submissions]** 的子菜單。 兩個頁籤， **[!UICONTROL Draft Forms]** 和 **[!UICONTROL Submitted Forms]**，顯示在Forms門戶頁面。 的 **[!UICONTROL Draft Forms]** 頁籤還顯示使用中所述步驟生成的轉換的自適應窗體 [為Forms門戶整合配置已轉換的自適應表單](#configure-converted-adaptive-form-for-forms-portal-integration)

1. 點擊 **[!UICONTROL Preview]**，按一下已轉換的自適應表單，為自適應表單域指定值並提交。 為自適應表單域指定的值將提交到整合資料庫。
