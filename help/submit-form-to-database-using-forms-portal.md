---
title: 使用Forms Portal將最適化表單提交至資料庫
description: 擴充預設中繼模型，以新增組織專屬的模式、驗證和實體，並在執行自動表單轉換服務時將組態套用至最適化表單欄位。
uuid: f98b4cca-f0a3-4db8-aef2-39b8ae462628
topic-tags: forms
discoiquuid: cad72699-4a4b-4c52-88a5-217298490a7c
translation-type: tm+mt
source-git-commit: 040b0ddb489b5bdfd640a93b22cd7bc512a39aea

---


# 使用Forms Portal整合最適化表單與資料庫 {#submit-forms-to-database-using-forms-portal}

「自動表單轉換」服務可讓您將非互動式PDF表單、Acro表單或以XFA為基礎的PDF表單轉換為最適化表單。 在開始轉換程式時，您可以選擇是否使用資料系結產生最適化表單。

如果您選擇產生不含資料系結的最適化表單，則轉換後可將轉換的最適化表單與表單資料模型、XML架構或JSON架構整合。 不過，如果您產生具有資料系結的最適化表單，轉換服務會自動將最適化表單與JSON結構描述關聯，並在最適化表單和JSON結構描述中可用的欄位間建立資料系結。 然後，您可以將最適化表單與您選擇的資料庫整合、填寫表單中的資料，並使用表單入口網站將它送出至資料庫。

下圖描述了使用Forms Portal將已轉換的自適應表單與資料庫整合的不同階段：

![資料庫整合](assets/database_integration.gif)

本文說明成功執行所有這些整合階段的逐步指示。

本文討論的範例是自訂資料和中繼資料服務的參考實作，以整合Forms Portal頁面與資料庫。 示例實施中使用的資料庫是MySQL 5.6.24。不過，您可以將Forms Portal頁面與您選擇的任何資料庫整合。

## 先決條件 {#pre-requisites}

* AEM 6.5作者實例與最新的AEM 6.5 Service Pack
* AEM Forms附加元件套件的最新版本
* [自動化表單轉換服務](configure-service.md)
* 要與整合的資料庫。 示例實施中使用的資料庫是MySQL 5.6.24。不過，您可將Forms Portal與您選擇的任何資料庫整合。

## 設定AEM實例與資料庫之間的連線 {#set-up-connection-aem-instance-database}

在AEM實例和MYSQL資料庫之間設定連接包括：

* [安裝MYSQL連接器包](#install-mysql-connector-java-file)

* [在資料庫中建立方案和表](#create-schema-and-tables-in-database)

* [配置連接設定](#configure-connection-between-aem-instance-and-database)

* [設定和設定Forms Portal整合的範例套件](#set-up-and-configure-sample)

### 安裝mysql-connector-java-5.1.39-bin.jar檔案 {#install-mysql-connector-java-file}

對所有作者和發佈實例執行以下步驟以安裝mysql-connector-java-5.1.39-bin.jar檔案：

1. 導覽至http://[server]:[port]/system/console/depfinder並搜尋com.mysql.jdbc套件。
1. 在「導出者」(Exported by)列中，檢查軟體包是否由任何包導出。 如果軟體包未由任何包導出，請繼續。
1. 導覽至http://[server]:[port]/system **[!UICONTROL Install/Update]**/console/bundles，然後按一下。
1. 單 **[!UICONTROL Choose File]** 擊並瀏覽以選擇mysql-connector-java-5.1.39-bin.jar檔案。 此外，請選取 **[!UICONTROL Start Bundle]** 和核取 **[!UICONTROL Refresh Packages]** 方塊。
1. 按一下 **[!UICONTROL Install]** 或 **[!UICONTROL Update]**。 完成後，重新啟動伺服器。
1. （僅限Windows）關閉您作業系統的系統防火牆。

### 在資料庫中建立模式和表 {#create-schema-and-tables-in-database}

執行以下步驟以在資料庫中建立模式和表：

1. 使用以下SQL陳述式在資料庫中建立模式：

   ```sql
   CREATE SCHEMA `formsportal` ;
   ```

   其中 **formsportal** 是指架構的名稱。

1. 使用以 **下SQL陳述式** ，在資料庫模式中建立資料表：

   ```sql
    CREATE TABLE `data` (
        `owner` varchar(255) DEFAULT NULL,
        `data` longblob,
        `metadataId` varchar(45) DEFAULT NULL,
        `id` varchar(45) NOT NULL,
        PRIMARY KEY (`id`)
        ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

1. 使用以 **下SQL陳述式** ，在資料庫架構中建立元資料表：

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

1. 使用以 **下SQL陳述式在資料庫模式中建立** additionalmetadatatable表：

   ```sql
   CREATE TABLE `additionalmetadatatable` (
       `value` text,
       `key` varchar(255) NOT NULL,
       `id` varchar(60) NOT NULL,
       PRIMARY KEY (`id`,`key`),
       CONSTRAINT ‘additionalmetadatatable_fk’ FOREIGN KEY (`id`) REFERENCES `metadata` (`id`) ON DELETE CASCADE
       ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

1. 使用以 **下SQL陳述式** ，在資料庫模式中建立可注釋表：

   ```sql
   CREATE TABLE `commenttable` (
       `commentId` varchar(255) DEFAULT NULL,
       `comment` text DEFAULT NULL,
       `ID` varchar(255) DEFAULT NULL,
       `commentowner` varchar(255) DEFAULT NULL,
       `time` varchar(255) DEFAULT NULL);
   ```

### 設定AEM例項與資料庫之間的連線 {#configure-connection-between-aem-instance-and-database}

執行下列設定步驟，以建立AEM例項與MYSQL資料庫之間的連線：

1. 前往「AEM Web Console Configuration」（AEM Web Console設定）頁 *面[:]http://[host]:* port/system/console/configMgr。
1. 按一下以在編 **[!UICONTROL Forms Portal Draft and Submission Configuration]** 輯模式中開啟。
1. 指定屬性的值，如下表所述：

   <table> 
    <tbody> 
    <tr> 
    <th><strong>屬性</strong></th> 
    <th><strong>說明</strong></th>
    <th><strong>值</strong></th> 
    </tr> 
    <tr> 
    <td><p>Forms Portal草稿資料服務</p></td> 
    <td><p>草稿資料服務的識別碼</p></td>
    <td><p>formsportal.sampledataservice</p></td> 
    </tr>
    <tr> 
    <td><p>Forms Portal草稿中繼資料服務</p></td> 
    <td><p>草稿中繼資料服務的識別碼</p></td>
    <td><p>formsportal.samplemetadataservice</p></td> 
    </tr>
    <tr> 
    <td><p>Forms Portal提交資料服務</p></td> 
    <td><p>用於提交資料服務的標識符</p></td>
    <td><p>formsportal.sampledataservice</p></td> 
    </tr>
    <tr> 
    <td><p>Forms Portal提交中繼資料服務</p></td> 
    <td><p>用於提交元資料服務的標識符</p></td>
    <td><p>formsportal.samplemetadataservice</p></td> 
    </tr>
    <tr> 
    <td><p>Forms Portal擱置中的Sign Data Service</p></td> 
    <td><p>待定Sign資料服務的識別碼</p></td>
    <td><p>formsportal.sampledataservice</p></td> 
    </tr>
    <tr> 
    <td><p>Forms Portal擱置中的Sign中繼資料服務</p></td> 
    <td><p>待審Sign中繼資料服務的識別碼</p></td>
    <td><p>formsportal.samplemetadataservice</p></td> 
    </tr>
    </tbody> 
    </table>
1. 保持其他配置不變，然後按一下 **[!UICONTROL Save]**。
1. 在「Web控制台配置」中， **[!UICONTROL Apache Sling Connection Pooled DataSource]** 查找並按一下以在編輯模式下開啟。 指定屬性的值，如下表所述：

   <table> 
    <tbody> 
    <tr> 
    <th><strong>屬性</strong></th> 
    <th><strong>值</strong></th> 
    </tr> 
    <tr> 
    <td><p>資料來源名稱</p></td> 
    <td><p>用於從資料源池中過濾驅動程式的資料源名稱。 範例實作使用FormsPortal作為資料來源名稱。</p></td>
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

### 設定並設定範例 {#set-up-and-configure-sample}

對所有作者和發佈實例執行以下步驟以安裝和配置示例：

1. 將下列 **** aem-fp-db-integration-sample-pkg-6.1.2.zip套件下載至您的檔案系統。

   [取得檔案](assets/aem-fp-db-integration-sample-pkg-6.1.2.zip)

1. 前往AEM封裝管理器，網址 *為[http://]host[:]port*/crx/packmgr/。
1. 按一下 **[!UICONTROL Upload Package]**.
1. 瀏覽以選 **取aem-fp-db-integration-sample-pkg-6.1.2.zip套件** ，然後按一下 **[!UICONTROL OK]**。
1. 按一 **[!UICONTROL Install]** 下套件旁的，以安裝套件。

## 設定已轉換的最適化表單，以整合Forms Portal {#configure-converted-adaptive-form-for-forms-portal-integration}

執行下列步驟，以啟用使用「表單入口網站」頁面的自適應表單提交：
1. [執行轉換](convert-existing-forms-to-adaptive-forms.md#start-the-conversion-process) ，將來源表單轉換為最適化表單。
1. 在編輯模式中開啟最適化表單。
1. 點選「表單容器」並選取「設定 ![自訂表單](assets/configure-adaptive-form.png)」。
1. 在區段 **[!UICONTROL Submission]** 中，從下 **[!UICONTROL Forms Portal Submit Action]** 拉式清 **[!UICONTROL Submit Action]** 單中選取。
1. 點選「 ![儲存範本原則](assets/edit_template_done.png) 」以儲存設定。

## 建立和設定Forms Portal頁面 {#create-configure-forms-portal-page}

執行下列步驟以建立Forms Portal頁面並加以設定，以便您使用此頁面提交最適化表單：

1. 登入AEM作者例項並點選 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Sites]**。
1. 選擇您要儲存新Forms Portal頁面的位置，然後點選 **[!UICONTROL Create]** > **[!UICONTROL Page]**。
1. 選取頁面的範本、點選、 **[!UICONTROL Next]**&#x200B;指定頁面的標題並點選 **[!UICONTROL Create]**。
1. 點選 **[!UICONTROL Edit]** 以設定頁面。
1. 在頁首中，點選「 ![編輯範本](assets/edit_template_sites.png) > **[!UICONTROL Edit Template]** 」以開啟頁面的範本。
1. 點選「版面容器」並點選「 ![編輯範本原則」](assets/edit_template_policy.png)。 在標籤 **[!UICONTROL Allowed Components]** 中，啟用和選 **[!UICONTROL Document Services]** 項， **[!UICONTROL Document Services Predicates]** 然後點選「 ![儲存範本」原則](assets/edit_template_done.png)。
1. 在頁 **[!UICONTROL Search & Lister]** 面中插入元件。 因此，您的AEM實例上所有現有的可用最適化表單都會列在頁面上。
1. 在頁 **[!UICONTROL Drafts & Submissions]** 面中插入元件。 兩個標籤 **[!UICONTROL Draft Forms]** 和 **[!UICONTROL Submitted Forms]**，會顯示在Forms Portal頁面上。 該選 **[!UICONTROL Draft Forms]** 項卡還顯示已轉換的最適化表單，這些表單是使用配置已轉換的適 [應性表單以進行Forms Portal整合的步驟生成的](#configure-converted-adaptive-form-for-forms-portal-integration)

1. 點選 **[!UICONTROL Preview]**、點選已轉換的最適化表單、指定最適化表單欄位的值並送出。 您為最適化表單欄位指定的值會提交至整合式資料庫。
