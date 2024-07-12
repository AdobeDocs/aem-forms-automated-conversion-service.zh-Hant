---
title: 使用Forms入口網站提交最適化表單至資料庫
description: 擴展預設元模型以新增組織特定的模式、驗證和實體，並在執行Automated forms conversion服務(AFCS)時將設定套用至調適型表單欄位。
uuid: f98b4cca-f0a3-4db8-aef2-39b8ae462628
topic-tags: forms
discoiquuid: cad72699-4a4b-4c52-88a5-217298490a7c
source-git-commit: c2392932d1e29876f7a11bd856e770b8f7ce3181
workflow-type: tm+mt
source-wordcount: '1159'
ht-degree: 1%

---


# 使用Forms入口網站整合最適化表單與資料庫 {#submit-forms-to-database-using-forms-portal}

automated forms conversion服務(AFCS)可讓您將非互動式PDF表單、Acro表單或XFAPDF表單轉換為最適化表單。 起始轉換程式時，您可以選擇產生具有或不具有資料繫結的最適化表單。

如果您選擇產生沒有資料繫結的調適型表單，則可以在轉換後整合已轉換的調適型表單與表單資料模型、XML結構描述或JSON結構描述。 不過，如果您產生具有資料繫結的調適型表單，轉換服務會自動將調適型表單與JSON結構描述相關聯，並在調適型表單和JSON結構描述中可用的欄位之間建立資料繫結。 然後，您可以將最適化表單與您選擇的資料庫整合、在表單中填寫資料，並使用Forms入口網站將其提交至資料庫。

下圖說明使用Forms入口網站將轉換後的適用性表單與資料庫整合的不同階段：

![資料庫整合](assets/database_integration.gif)

本文會說明如何成功執行所有這些整合階段的逐步指示。

本文討論的範例是參考實作自訂資料和中繼資料服務，以整合Forms入口網站頁面與資料庫。 範例實作中使用的資料庫是MySQL 5.6.24。不過，您可以將Forms Portal頁面與您選擇的任何資料庫整合。

## 必要條件 {#pre-requisites}

* 設定AEM 6.4或6.5編寫執行個體
* 為您的AEM執行個體安裝[最新Service Pack](https://helpx.adobe.com/tw/experience-manager/aem-releases-updates.html)
* 最新版本的AEM Forms附加元件套件
* 設定[Automated forms conversion服務(AFCS)](configure-service.md)
* 設定資料庫。 範例實作中使用的資料庫是MySQL 5.6.24。不過，您可以將轉換後的最適化表單與您選擇的任何資料庫整合。

## 設定AEM執行個體與資料庫之間的連線 {#set-up-connection-aem-instance-database}

設定AEM執行處理與MYSQL資料庫之間的連線包含：

* [安裝MYSQL聯結器套件](#install-mysql-connector-java-file)

* [在資料庫中建立綱要和表格](#create-schema-and-tables-in-database)

* [正在設定連線設定](#configure-connection-between-aem-instance-and-database)

* [設定和設定Forms Portal整合的範例套件](#set-up-and-configure-sample)

### 安裝mysql-connector-java-5.1.39-bin.jar檔案 {#install-mysql-connector-java-file}

在所有作者和發佈執行個體上執行以下步驟，以安裝mysql-connector-java-5.1.39-bin.jar檔案：

1. 導覽至http://[伺服器]：[連線埠]/system/console/depfinder，並搜尋com.mysql.jdbc套件。
1. 在「匯出者」欄中，檢查封裝是否由任何束匯出。 如果套件未由任何套件組合匯出，請繼續。
1. 瀏覽至http://[伺服器]：[連線埠]/system/console/bundles，然後按一下&#x200B;**[!UICONTROL Install/Update]**。
1. 按一下&#x200B;**[!UICONTROL Choose File]**&#x200B;並瀏覽以選取mysql-connector-java-5.1.39-bin.jar檔案。 此外，選取&#x200B;**[!UICONTROL Start Bundle]**&#x200B;和&#x200B;**[!UICONTROL Refresh Packages]**&#x200B;核取方塊。
1. 按一下&#x200B;**[!UICONTROL Install]**&#x200B;或&#x200B;**[!UICONTROL Update]**。 完成後，請重新啟動伺服器。
1. （僅限Windows）關閉作業系統的系統防火牆。

### 在資料庫中建立綱要和表格 {#create-schema-and-tables-in-database}

執行以下步驟，在資料庫中建立綱要和表格：

1. 使用下列SQL敘述句在資料庫中建立綱要：

   ```sql
   CREATE SCHEMA `formsportal` ;
   ```

   其中&#x200B;**formsportal**&#x200B;參考結構描述的名稱。

1. 使用下列SQL陳述式在資料庫結構描述中建立&#x200B;**資料**&#x200B;資料表：

   ```sql
    CREATE TABLE `data` (
        `owner` varchar(255) DEFAULT NULL,
        `data` longblob,
        `metadataId` varchar(45) DEFAULT NULL,
        `id` varchar(45) NOT NULL,
        PRIMARY KEY (`id`)
        ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

1. 使用下列SQL陳述式，在資料庫結構描述中建立&#x200B;**中繼資料**&#x200B;表格：

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

1. 使用下列SQL陳述式在資料庫結構描述中建立&#x200B;**additionalmetadatatable**&#x200B;資料表：

   ```sql
   CREATE TABLE `additionalmetadatatable` (
       `value` text,
       `key` varchar(255) NOT NULL,
       `id` varchar(60) NOT NULL,
       PRIMARY KEY (`id`,`key`),
       CONSTRAINT ‘additionalmetadatatable_fk’ FOREIGN KEY (`id`) REFERENCES `metadata` (`id`) ON DELETE CASCADE
       ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

1. 使用下列SQL陳述式在資料庫結構描述中建立&#x200B;**備注資料表**：

   ```sql
   CREATE TABLE `commenttable` (
       `commentId` varchar(255) DEFAULT NULL,
       `comment` text DEFAULT NULL,
       `ID` varchar(255) DEFAULT NULL,
       `commentowner` varchar(255) DEFAULT NULL,
       `time` varchar(255) DEFAULT NULL);
   ```

### 設定AEM執行個體與資料庫之間的連線 {#configure-connection-between-aem-instance-and-database}

執行以下設定步驟來建立AEM執行處理與MYSQL資料庫之間的連線：

1. 移至&#x200B;*http://[主機]：[連線埠]/system/console/configMgr*&#x200B;的AEM Web主控台組態頁面。
1. 按一下以編輯模式開啟&#x200B;**[!UICONTROL Forms Portal Draft and Submission Configuration]**。
1. 指定特性值，如下表所述：

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
    <td><p>草稿中繼資料服務的識別碼</p></td>
    <td><p>formsportal.samplemetadataservice</p></td> 
    </tr>
    <tr> 
    <td><p>Forms入口網站提交資料服務</p></td> 
    <td><p>用於提交資料服務的識別碼</p></td>
    <td><p>formsportal.sampledataservice</p></td> 
    </tr>
    <tr> 
    <td><p>Forms入口網站提交中繼資料服務</p></td> 
    <td><p>用於提交中繼資料服務的識別碼</p></td>
    <td><p>formsportal.samplemetadataservice</p></td> 
    </tr>
    <tr> 
    <td><p>Forms入口網站等待簽署的資料服務</p></td> 
    <td><p>擱置簽署資料服務的識別碼</p></td>
    <td><p>formsportal.sampledataservice</p></td> 
    </tr>
    <tr> 
    <td><p>Forms入口網站等待簽署中繼資料服務</p></td> 
    <td><p>擱置簽署中繼資料服務的識別碼</p></td>
    <td><p>formsportal.samplemetadataservice</p></td> 
    </tr>
    </tbody> 
    </table>
1. 將其他設定維持原狀，然後按一下&#x200B;**[!UICONTROL Save]**。
1. 在Web主控台組態中尋找並按一下以編輯模式開啟&#x200B;**[!UICONTROL Apache Sling Connection Pooled DataSource]**。 指定特性值，如下表所述：

   <table> 
    <tbody> 
    <tr> 
    <th><strong>屬性</strong></th> 
    <th><strong>值</strong></th> 
    </tr> 
    <tr> 
    <td><p>資料來源名稱</p></td> 
    <td><p>從資料來源集區篩選驅動程式的資料來源名稱。 範例實作使用FormsPortal作為資料來源名稱。</p></td>
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

### 設定範例 {#set-up-and-configure-sample}

在所有作者和發佈執行個體上執行以下步驟，以安裝和設定範例：

1. 將下列&#x200B;**aem-fp-db-integration-sample-pkg-6.1.2.zip**&#x200B;封裝下載至您的檔案系統。

[取得檔案](assets/aem-fp-db-integration-sample-pkg-6.1.2.zip)

1. 移至&#x200B;*http://[主機]：[連線埠]/crx/packmgr/*&#x200B;的AEM封裝管理員。
1. 按一下「**[!UICONTROL Upload Package]**」。
1. 瀏覽以選取&#x200B;**aem-fp-db-integration-sample-pkg-6.1.2.zip**&#x200B;封裝，然後按一下&#x200B;**[!UICONTROL OK]**。
1. 按一下封裝旁的&#x200B;**[!UICONTROL Install]**&#x200B;以安裝封裝。

## 設定已轉換的Forms Portal整合適用性表單 {#configure-converted-adaptive-form-for-forms-portal-integration}

執行以下步驟，透過Forms Portal頁面啟用最適化表單提交：
1. [執行轉換](convert-existing-forms-to-adaptive-forms.md#start-the-conversion-process)，將來源表單轉換為最適化表單。
1. 在編輯模式中開啟最適化表單。
1. 點選「表單容器」，然後選取「設定![設定自適應表單](assets/configure-adaptive-form.png)」。
1. 在&#x200B;**[!UICONTROL Submission]**&#x200B;區段中，從&#x200B;**[!UICONTROL Submit Action]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL Forms Portal Submit Action]**。
1. 點選![儲存範本原則](assets/edit_template_done.png)以儲存設定。

## 建立及設定Forms入口網站頁面 {#create-configure-forms-portal-page}

執行以下步驟來建立Forms Portal頁面並進行設定，以便您可以使用此頁面提交調適型表單：

1. 登入AEM作者執行個體並點選「**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Sites]**」。
1. 選取您要儲存新Forms入口網站頁面的位置，然後點選「**[!UICONTROL Create]** > **[!UICONTROL Page]**」。
1. 選取頁面的範本、點選&#x200B;**[!UICONTROL Next]**、指定頁面的標題，然後點選&#x200B;**[!UICONTROL Create]**。
1. 點選&#x200B;**[!UICONTROL Edit]**&#x200B;以設定頁面。
1. 在頁面標頭中，點選「![編輯範本](assets/edit_template_sites.png) > **[!UICONTROL Edit Template]**」以開啟頁面的範本。
1. 點選[配置容器]，然後點選![編輯範本原則](assets/edit_template_policy.png)。 在&#x200B;**[!UICONTROL Allowed Components]**&#x200B;標籤中，啟用&#x200B;**[!UICONTROL Document Services]**&#x200B;和&#x200B;**[!UICONTROL Document Services Predicates]**&#x200B;選項，然後點選![儲存範本原則](assets/edit_template_done.png)。
1. 在頁面中插入&#x200B;**[!UICONTROL Search & Lister]**&#x200B;元件。 因此，您AEM執行個體上可用的所有現有調適型表單都會列在頁面上。
1. 在頁面中插入&#x200B;**[!UICONTROL Drafts & Submissions]**&#x200B;元件。 Forms入口網站頁面上會顯示兩個索引標籤&#x200B;**[!UICONTROL Draft Forms]**&#x200B;和&#x200B;**[!UICONTROL Submitted Forms]**。 **[!UICONTROL Draft Forms]**&#x200B;索引標籤也會顯示使用[為Forms入口網站整合設定已轉換的最適化表單](#configure-converted-adaptive-form-for-forms-portal-integration)中提及的步驟所產生的已轉換最適化表單

1. 點選&#x200B;**[!UICONTROL Preview]**，點選轉換的最適化表單，指定最適化表單欄位的值並提交它。 您為最適化表單欄位指定的值會提交至整合式資料庫。
