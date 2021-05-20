---
title: 使用Forms Portal將最適化表單提交至資料庫
description: 擴充預設元模型，以新增貴組織專屬的模式、驗證和實體，並在執行Automated forms conversion服務時將設定套用至最適化表單欄位。
uuid: f98b4cca-f0a3-4db8-aef2-39b8ae462628
topic-tags: forms
discoiquuid: cad72699-4a4b-4c52-88a5-217298490a7c
source-git-commit: ead1b4ee177029c60f095dc596b1f3db5878760e
workflow-type: tm+mt
source-wordcount: '1153'
ht-degree: 1%

---


# 使用Forms Portal {#submit-forms-to-database-using-forms-portal}整合最適化表單與資料庫

automated forms conversion服務可讓您將非互動式PDF表單、Acro表單或XFA型PDF表單轉換為最適化表單。 啟動轉換程式時，您可以選擇產生具有或不具有資料系結的最適化表單。

如果您選擇生成沒有資料綁定的適用性表單，則可以在轉換後將轉換的適用性表單與表單資料模型、XML架構或JSON架構整合。 不過，如果您產生具有資料系結的適用性表單，轉換服務會自動將適用性表單與JSON結構描述建立關聯，並在適用性表單和JSON結構描述中可用的欄位之間建立資料系結。 然後，您就可以將最適化表單與您選擇的資料庫整合、填寫表單中的資料，並使用Forms入口網站將其提交至資料庫。

下圖說明使用Forms Portal整合轉換後的最適化表單與資料庫的不同階段：

![資料庫整合](assets/database_integration.gif)

本文說明成功執行所有這些整合階段的逐步指示。

本文探討的範例是自訂資料和中繼資料服務的參考實作，以整合Forms Portal頁面與資料庫。 示例實施中使用的資料庫是MySQL 5.6.24。但是，您可以將Forms門戶頁與您選擇的任何資料庫整合。

## 先決條件{#pre-requisites}

* 設定AEM 6.4或6.5製作例項
* 為您的AEM執行個體安裝[最新Service Pack](https://helpx.adobe.com/tw/experience-manager/aem-releases-updates.html)
* 最新版AEM Forms附加元件套件
* 配置[Automated forms conversion服務](configure-service.md)
* 設定資料庫。 示例實施中使用的資料庫是MySQL 5.6.24。但是，您可以將轉換的最適化表單與您選擇的任何資料庫整合。

## 設定AEM實例和資料庫{#set-up-connection-aem-instance-database}之間的連接

在AEM實例和MYSQL資料庫之間設定連接包括：

* [安裝MYSQL連接器包](#install-mysql-connector-java-file)

* [在資料庫中建立架構和表](#create-schema-and-tables-in-database)

* [配置連接設定](#configure-connection-between-aem-instance-and-database)

* [設定和設定Forms Portal整合的範例套件](#set-up-and-configure-sample)

### 安裝mysql-connector-java-5.1.39-bin.jar檔案{#install-mysql-connector-java-file}

在所有製作執行個體和發佈執行個體上執行下列步驟，以安裝mysql-connector-java-5.1.39-bin.jar檔案：

1. 導航到http://[server]:[port]/system/console/depfinder並搜索com.mysql.jdbc包。
1. 在「匯出依據」欄中，檢查套件是否由任何套件匯出。 如果包未由任何包導出，請繼續。
1. 導覽至http://[server]:[port]/system/console/bundles ，然後按一下&#x200B;**[!UICONTROL Install/Update]**。
1. 按一下&#x200B;**[!UICONTROL Choose File]**&#x200B;並瀏覽以選擇mysql-connector-java-5.1.39-bin.jar檔案。 同時，選擇&#x200B;**[!UICONTROL Start Bundle]**&#x200B;和&#x200B;**[!UICONTROL Refresh Packages]**&#x200B;複選框。
1. 按一下&#x200B;**[!UICONTROL Install]**&#x200B;或&#x200B;**[!UICONTROL Update]**。 完成後，重新啟動伺服器。
1. （僅限Windows）關閉作業系統的系統防火牆。

### 在資料庫{#create-schema-and-tables-in-database}中建立架構和表

執行以下步驟在資料庫中建立架構和表：

1. 使用以下SQL陳述式在資料庫中建立架構：

   ```sql
   CREATE SCHEMA `formsportal` ;
   ```

   其中&#x200B;**formsportal**&#x200B;表示架構的名稱。

1. 使用以下SQL陳述式在資料庫架構中建立&#x200B;**data**&#x200B;表：

   ```sql
    CREATE TABLE `data` (
        `owner` varchar(255) DEFAULT NULL,
        `data` longblob,
        `metadataId` varchar(45) DEFAULT NULL,
        `id` varchar(45) NOT NULL,
        PRIMARY KEY (`id`)
        ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

1. 使用以下SQL陳述式在資料庫架構中建立&#x200B;**metadata**&#x200B;表：

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

1. 使用以下SQL陳述式在資料庫架構中建立&#x200B;**additionalmetadatatable**&#x200B;表：

   ```sql
   CREATE TABLE `additionalmetadatatable` (
       `value` text,
       `key` varchar(255) NOT NULL,
       `id` varchar(60) NOT NULL,
       PRIMARY KEY (`id`,`key`),
       CONSTRAINT ‘additionalmetadatatable_fk’ FOREIGN KEY (`id`) REFERENCES `metadata` (`id`) ON DELETE CASCADE
       ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

1. 使用以下SQL陳述式在資料庫架構中建立&#x200B;**commenttable**&#x200B;表：

   ```sql
   CREATE TABLE `commenttable` (
       `commentId` varchar(255) DEFAULT NULL,
       `comment` text DEFAULT NULL,
       `ID` varchar(255) DEFAULT NULL,
       `commentowner` varchar(255) DEFAULT NULL,
       `time` varchar(255) DEFAULT NULL);
   ```

### 配置AEM實例和資料庫{#configure-connection-between-aem-instance-and-database}之間的連接

執行以下配置步驟以建立AEM實例和MYSQL資料庫之間的連接：

1. 前往&#x200B;*http://[host]:[port]/system/console/configMgr*&#x200B;的AEM Web控制台配置頁。
1. 按一下以在編輯模式中開啟&#x200B;**[!UICONTROL Forms Portal Draft and Submission Configuration]**。
1. 指定屬性的值，如下表所述：

   <table> 
    <tbody> 
    <tr> 
    <th><strong>屬性</strong></th> 
    <th><strong>說明</strong></th>
    <th><strong>值</strong></th> 
    </tr> 
    <tr> 
    <td><p>Forms入口網站草稿資料服務</p></td> 
    <td><p>草稿資料服務的識別碼</p></td>
    <td><p>formsportal.sampledataservice</p></td> 
    </tr>
    <tr> 
    <td><p>Forms入口網站草稿中繼資料服務</p></td> 
    <td><p>草稿元資料服務的識別碼</p></td>
    <td><p>formsportal.samplemetadataservice</p></td> 
    </tr>
    <tr> 
    <td><p>Forms Portal提交資料服務</p></td> 
    <td><p>提交資料服務的標識符</p></td>
    <td><p>formsportal.sampledataservice</p></td> 
    </tr>
    <tr> 
    <td><p>Forms Portal提交中繼資料服務</p></td> 
    <td><p>提交元資料服務的標識符</p></td>
    <td><p>formsportal.samplemetadataservice</p></td> 
    </tr>
    <tr> 
    <td><p>Forms Portal待簽署資料服務</p></td> 
    <td><p>掛起簽名資料服務的標識符</p></td>
    <td><p>formsportal.sampledataservice</p></td> 
    </tr>
    <tr> 
    <td><p>Forms Portal擱置中的簽署中繼資料服務</p></td> 
    <td><p>待定簽名元資料服務的標識符</p></td>
    <td><p>formsportal.samplemetadataservice</p></td> 
    </tr>
    </tbody> 
    </table>
1. 保留其他配置原樣，然後按一下&#x200B;**[!UICONTROL Save]**。
1. 查找並按一下，在Web控制台配置的編輯模式下開啟&#x200B;**[!UICONTROL Apache Sling Connection Pooled DataSource]**。 指定屬性的值，如下表所述：

   <table> 
    <tbody> 
    <tr> 
    <th><strong>屬性</strong></th> 
    <th><strong>值</strong></th> 
    </tr> 
    <tr> 
    <td><p>資料源名稱</p></td> 
    <td><p>用於從資料源池中篩選驅動程式的資料源名稱。 實作範例使用FormsPortal做為資料來源名稱。</p></td>
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

### 設定範例{#set-up-and-configure-sample}

在所有製作和發佈執行個體上執行下列步驟，以安裝和設定範例：

1. 將下列&#x200B;**aem-fp-db-integration-sample-pkg-6.1.2.zip**&#x200B;套件下載至您的檔案系統。

[取得檔案](assets/aem-fp-db-integration-sample-pkg-6.1.2.zip)

1. 前往AEM套件管理器，網址為&#x200B;*http://[host]:[port]/crx/packmgr/*。
1. 按一下 **[!UICONTROL Upload Package]**.
1. 瀏覽以選取&#x200B;**aem-fp-db-integration-sample-pkg-6.1.2.zip**&#x200B;套件，然後按一下&#x200B;**[!UICONTROL OK]**。
1. 按一下套件旁的&#x200B;**[!UICONTROL Install]**&#x200B;以安裝該套件。

## 設定已轉換的Forms Portal整合適用表單{#configure-converted-adaptive-form-for-forms-portal-integration}

執行下列步驟，使用Forms Portal頁面啟用最適化表單提交：
1. [執行轉](convert-existing-forms-to-adaptive-forms.md#start-the-conversion-process) 換，將來源表單轉換為最適化表單。
1. 在編輯模式中開啟最適化表單。
1. 點選「表單容器」並選取「設定![設定適用性表單](assets/configure-adaptive-form.png)」。
1. 在&#x200B;**[!UICONTROL Submission]**&#x200B;區段中，從&#x200B;**[!UICONTROL Submit Action]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL Forms Portal Submit Action]**。
1. 點選![儲存範本原則](assets/edit_template_done.png)以儲存設定。

## 建立並設定Forms Portal頁面{#create-configure-forms-portal-page}

執行下列步驟來建立Forms Portal頁面並加以設定，以便您能使用此頁面提交最適化表單：

1. 登入AEM製作例項，然後點選&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Sites]**。
1. 選取您要儲存新Forms Portal頁面的位置，然後點選&#x200B;**[!UICONTROL Create]** > **[!UICONTROL Page]**。
1. 選取頁面的範本，點選&#x200B;**[!UICONTROL Next]**，指定頁面的標題，然後點選&#x200B;**[!UICONTROL Create]**。
1. 點選&#x200B;**[!UICONTROL Edit]**&#x200B;以設定頁面。
1. 在頁首中，點選![編輯範本](assets/edit_template_sites.png) > **[!UICONTROL Edit Template]**&#x200B;以開啟頁面的範本。
1. 點選「配置容器」，然後點選「![編輯範本原則](assets/edit_template_policy.png)」。 在&#x200B;**[!UICONTROL Allowed Components]**&#x200B;標籤中，啟用&#x200B;**[!UICONTROL Document Services]**&#x200B;和&#x200B;**[!UICONTROL Document Services Predicates]**&#x200B;選項，然後點選![儲存範本原則](assets/edit_template_done.png)。
1. 在頁面中插入&#x200B;**[!UICONTROL Search & Lister]**&#x200B;元件。 因此，頁面上會列出您AEM例項上可用的所有現有最適化表單。
1. 在頁面中插入&#x200B;**[!UICONTROL Drafts & Submissions]**&#x200B;元件。 **[!UICONTROL Draft Forms]**&#x200B;和&#x200B;**[!UICONTROL Submitted Forms]**&#x200B;這兩個標籤會顯示在Forms Portal頁面上。 **[!UICONTROL Draft Forms]**&#x200B;索引標籤也會顯示已轉換的最適化表單，這些表單是使用[設定已轉換的Forms Portal整合適用的最適化表單](#configure-converted-adaptive-form-for-forms-portal-integration)中提及的步驟產生

1. 點選&#x200B;**[!UICONTROL Preview]**，點選轉換的最適化表單，指定最適化表單欄位的值並提交。 您為適用性表單欄位指定的值會提交至整合資料庫。
