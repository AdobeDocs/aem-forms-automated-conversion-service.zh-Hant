---
title: 擴展預設元模型
seo-title: 擴展預設元模型
description: 擴充預設元模型，以新增貴組織專屬的模式、驗證和實體，並在執行Automated forms conversion服務時將設定套用至最適化表單欄位。
seo-description: 擴充預設元模型，以新增貴組織專屬的模式、驗證和實體，並在執行Automated forms conversion服務時將設定套用至最適化表單欄位。
uuid: f98b4cca-f0a3-4db8-aef2-39b8ae462628
topic-tags: forms
discoiquuid: cad72699-4a4b-4c52-88a5-217298490a7c
exl-id: f679059c-18aa-4cb5-8368-ed27e96c20de
source-git-commit: 3f91fc0541f8fe8dbc997ae0b401c8a0a49347dd
workflow-type: tm+mt
source-wordcount: '2569'
ht-degree: 1%

---

# 擴展預設元模型 {#extend-the-default-meta-model}

automated forms conversion服務識別並從來源表單中擷取表單物件。 語義映射器有助於服務決定如何以最適化形式表示擷取的物件。 例如，源表單可以有許多不同類型的日期表示。 語義映射器幫助將源表單的日期表單對象的所有表示與自適應表單的日期元件映射。 語義映射器還允許服務在轉換期間將驗證、規則、資料模式、幫助文本和輔助功能屬性預配置並應用到最適化表單元件。

![](assets/meta-model.gif)

中繼模型是JSON結構描述。 開始使用中繼模型之前，請確定您熟悉JSON。 您必須具備建立、編輯和讀取JSON格式儲存之資料的經驗。

## 預設元模型 {#default-meta-model}

automated forms conversion服務具有預設元模型。 此為JSON結構，與Automated forms conversion服務的其他元件一起駐留在Adobe雲端。 您可以在本機AEM伺服器上找到中繼模型的復本：http://&lt;server>:&lt;port>/aem/forms.html/content/dam/formsanddocuments/metamodel/`global.schema.json`。 您也可以[按一下這裡](assets/en.globalschema.json)來存取或下載英文架構。 [法文](assets/fr.globalschema.json)、[德文](assets/de.globalschema.json)和[西班牙文](assets/es.globalschema.json)語言的元模型也可供下載。

元模型的模式是從https://schema.org/docs/schemas.html上的架構實體派生的。 https://schema.org上定義了人員、郵遞區號、本地業務和更多實體。 元模型的每個實體都遵守JSON結構描述物件類型。 以下代碼表示元模型結構示例：

```
   "Entity": {
      "id": "Entity",
      "properties": {
        "name": {
          "type": "string"
        },

        "description": {
          "type": "string",
          "description": "Description of the item"
        }
      }
    }
```

## 下載預設元模型 {#download-the-default-meta-model}

執行以下步驟將預設元模型下載到本地檔案系統：

1. 登入您的AEM Forms執行個體。
1. 導覽至&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]** **** **[!UICONTROL Meta Model]**&#x200B;資料夾。
1. 選取&#x200B;**[!UICONTROL global.schema.json]**&#x200B;檔案，然後點選&#x200B;**[!UICONTROL Download]**。 下載對話框隨即出現。 選擇&#x200B;**[!UICONTROL Download asset(s) as binary files]**&#x200B;選項。 點選&#x200B;**[!UICONTROL Download]**。 已下載封存。

   <!--
   Comment Type: draft

   <li><p>Extract the archive and open the global.schema.json file for editing. </p> </li>
   -->

   <!--
   Comment Type: draft

   <li>Step text</li>
   -->

## 了解元模型 {#understanding-the-meta-model}

中繼模型是指包含實體的JSON結構描述檔案。 JSON結構檔案中的所有實體都包含名稱和ID。 每個實體可包含多個屬性。 實體及其屬性可能會根據網域而有所不同。 您可以使用關鍵字和欄位設定來擴大結構檔案，以將結構屬性對應至最適化表單元件。

```
"Event": {
      "id": "Eventid",
      "allOf": [
        {
          "$ref": "#Entity"
        },
        {
          "properties": {
            "startDate": {
              "type": "string",
              "format": "date",
              "description": "Specify the start date and time of the event in ISO 8601 date format."
            },
            "endDate": {
              "type": "string",
              "format": "date",
              "description": "Specify the end date and time of the event in ISO 8601 date format."
            },
            "location": {
              "$ref": "#PostalAddress",
              "description": "Specify the location of the event."
            }
          }
        }
      ]
    }
```

在此範例中，**Event**&#x200B;代表實體的名稱，其值為&#x200B;**id**&#x200B;為&#x200B;**Eventid**。 事件實體包含多個屬性：

* startDate
* endDate
* 位置

元模型中的&#x200B;**allOf**&#x200B;結構允許實體之間的繼承。

每個屬性可進一步包括：

* [JSON結構屬性](#jsonschemaproperties)
* [以關鍵字為基礎的搜尋，將屬性套用至產生的最適化表單欄位](#keywordsearch)
* [其他屬性](#additionalproperties)

![元模型屬性](assets/meta_model_elements.gif)

根據使用&#x200B;**aem:affKeyword**&#x200B;參考的關鍵字，轉換服務會對來源表單欄位執行搜尋操作。 轉換服務會將JSON結構屬性和其他屬性套用至符合搜尋條件的欄位。

在此示例中，轉換服務在源表單中搜索電話、電話、行動電話、工作電話、家庭電話、電話號碼、電話號碼和電話號碼關鍵字。 根據包含這些關鍵字的欄位，轉換服務會在轉換後將類型、模式和aem:afProperties套用至最適化表單欄位。

### 產生的最適化表單欄位的JSON結構屬性 {#jsonschemaproperties}

中繼模型支援下列使用Automated forms conversion服務產生的適用性表單欄位的JSON結構通用屬性：

<table> 
 <tbody> 
  <tr> 
   <th><strong>屬性名稱</strong></th> 
   <th><strong>說明</strong></th> 
  </tr> 
  <tr> 
   <td><p>標題</p></td> 
   <td> 
    <p>在中繼模型的標題屬性中提及的文字可作為搜尋關鍵字，以對產生的最適化表單欄位執行動作。 例如，修改最適化表單欄位的標籤。 如需詳細資訊，請參閱<a href="#custommetamodelexamples">自訂元模型範例中的<strong>修改表單欄位</strong>的標籤。</a></p> </td> 
  </tr>
  <td><p>說明</p></td> 
   <td> 
    <p>說明屬性會為產生的最適化表單欄位設定說明文字。 有關詳細資訊，請參閱<a href="#custommetamodelexamples">自定義元模型示例中的<strong>向表單欄位</strong>添加幫助文本。</a></p> </td> 
  </tr>
  <td><p>類型</p></td> 
   <td> 
    <p>type屬性會定義所產生最適化表單欄位的資料類型。 標題屬性的可能值包括：</p>
    <ul> 
     <li>字串：產生文字資料類型的最適化表單欄位。</li> 
     <li>數字：產生數值資料類型的最適化表單欄位。</li>
     <li>整數：生成將子類型設定為整數的數值資料類型的自適應表單欄位。</li>
     <li>布林值：生成交換機自適應表單元件。</li>
     </ul><p>有關在元模型中使用type屬性的詳細資訊，請參閱<a href="#custommetamodelexamples">自定義元模型示例中的<strong>修改表單欄位的類型</strong>。</a></p></td> 
  </tr>
  <td><p>圖樣</p></td> 
   <td> 
    <p>模式屬性會根據規則運算式來限制所產生適用性表單欄位的值。 例如，元模型中的下列程式碼會將產生的最適化表單欄位值限制為十位數：<br>"pattern":"/\\d{10}/"<br>同樣地，元模型中的以下代碼將欄位的值限制為特定日期格式。<br> "pattern":"date{DD MMM, YYYY}",</p> </td> 
  </tr>
  <td><p>格式</p></td> 
   <td> 
    <p>format屬性會根據命名模式（而非規則運算式）來限制所產生適用性表單欄位的值。 format屬性的可能值包括：<ul><li>電子郵件：產生電子郵件最適化表單元件。</li><li>主機名：生成文本框最適化表單元件。</li></ul>有關在元模型中使用format屬性的詳細資訊，請參閱<a href="#custommetamodelexamples">自定義元模型示例中的<strong>修改表單欄位</strong>的格式。</a></p> </td> 
  </tr>
  <td><p>enum和enumNames</p></td> 
   <td> 
    <p>enum和enumNames屬性將下拉式清單、核取方塊或選項按鈕欄位的值限制為固定集。 enumNames中列出的值顯示在用戶介面上。 使用列舉屬性列出的值用於計算。<br>如需詳細資訊，請 <strong>參閱在最適化表單中將表單欄位轉換為多選核取方塊</strong>、 <strong>在最適化表單中將文字欄位轉換為下拉式清單</strong>，以及 <strong>在自訂中繼模型範例中新增其</strong> 他 <a href="#custommetamodelexamples">選項。</a></p> </td> 
  </tr>
 </tbody> 
</table>

### 以關鍵字為基礎的搜尋，將屬性套用至產生的最適化表單欄位 {#keywordsearch}

automated forms conversion服務在轉換期間對來源表單執行關鍵字搜尋。 篩選符合搜尋准則的欄位後，轉換服務會將元模型中這些欄位所定義的屬性套用至產生的最適化表單欄位。

使用&#x200B;**aem:affKeyword**&#x200B;屬性參考關鍵字。

```
{
  "numberfields": {
      "type": "number",
      "aem:affKeyword": ["Bank account number"]
 }
}
```

在此範例中，轉換服務使用&#x200B;**aem:affKeyword**&#x200B;內的文字作為搜尋關鍵字。 擷取表單中的&#x200B;**銀行帳號**&#x200B;文字後，轉換服務會使用&#x200B;**type**&#x200B;屬性，將欄位轉換為&#x200B;**number**&#x200B;類型。

### 產生的最適化表單欄位的其他屬性 {#additionalproperties}

您可以使用中繼模型中的&#x200B;**aem:afProperties**&#x200B;屬性，為使用Automated forms conversion服務產生的適用性表單欄位定義下列其他屬性：

<table> 
 <tbody> 
  <tr> 
   <th><strong>屬性名稱</strong></th> 
   <th><strong>說明</strong></th> 
  </tr> 
  <tr> 
   <td><p>multiLine</p></td> 
   <td> 
    <p>multiLine屬性在轉換後將源表單欄位轉換為最適化表單中的多行欄位。 如需詳細資訊，請參閱<a href="#custommetamodelexamples">自訂元模型範例中的<strong>將字串欄位轉換為多行欄位</strong> 。</a></p> </td> 
  </tr>
  <td><p>強制</p></td> 
   <td> 
    <p>強制屬性會將轉換後適用性表單欄位的輸入設為強制。<br>如需詳細資訊，請參 <strong>閱自訂中繼模型範例中</strong> 的將 <a href="#custommetamodelexamples">驗證新增至最適化表單欄位。</a></p>
    </td> 
  </tr>
  <td><p>jcr:title</p></td> 
   <td> 
    <p>jcr:title屬性與標題JSON結構屬性可讓您在轉換後修改最適化表單欄位的標籤。<br>如需詳細資訊，請 <strong>參閱自訂元模型範例中</strong> 的 <a href="#custommetamodelexamples">修改表單欄位標籤。</a><br>請參 <a href="https://helpx.adobe.com/experience-manager/6-5/forms/using/adaptive-form-json-schema-form-model.html" target="_blank">閱使用JSON結構建</a> 立最適化表單，以取得更多可使用JSON結構套用至最適化表單欄位的屬性資訊。</p>
    <p></p></td> 
  </tr>
  <td><p>sling:resourceType和guideNodeClass</p></td> 
   <td> 
    <p>sling:resourceType和guideNodeClass屬性可讓您將表單欄位對應至對應的最適化表單元件。<br>如需詳細資訊， <strong>請參閱自適性表單中的「將表單欄位轉換為多選項」核取方塊，以及</strong> 自 <strong>訂中繼模型範例中的「將文字欄位轉換為</strong> 下拉 <a href="#custommetamodelexamples">式清單」。</a></p> </td> 
  </tr>
  <td><p>validatePictureClause</p></td> 
   <td> 
    <p>validatePictureClause屬性設定轉換後自適應表單欄位中允許的格式的驗證。<br>如需詳細資訊，請參 <strong>閱自訂中繼模型範例中</strong> 的將 <a href="#custommetamodelexamples">驗證新增至最適化表單欄位。</p> </td> 
  </tr>
 </tbody> 
</table>

## 以您自己的語言建立自訂元模型{#language-specific-meta-model}

您可以建立語言特定的元模型。 此類元模型可協助您以所選擇的語言建立對應規則。 automated forms conversion服務可讓您以下列語言建立元模型：

* English(en)
* French(fr)
* German(de)
* 西班牙文()

將&#x200B;*aem:Language*&#x200B;中繼標籤標籤新增至中繼模型頂端，以指定其語言。 例如，

```JSON
"metaTags": {
        "aem:Language": "de"
    }
```

英語是元模型的預設語言。

### 建立語言特定元模型的考量

* 確保每個索引鍵的名稱都使用英文。 例如， emailAddress。
* 請確定所有&#x200B;*id*&#x200B;鍵的所有實體參考和預先定義的值都使用英文。 例如&quot;id&quot;:&quot;ContactPoint&quot; / &quot;$ref&quot;:&quot;實體&quot;。
* 確保元模型中包含的以下鍵的描述或消息與元模型的語言相對應：
   * aem:affKeyword
   * 標題
   * 說明
   * enumNames
   * shortDescription
   * validatePictureClauseMessage

   例如，當元模型的語言是法文時(「aem:Language」：&quot;fr&quot;)，請確定所有說明和訊息都使用法文。

* 請確定所有[JSON結構屬性](#jsonschemaproperties)僅使用支援的值。

下圖顯示了英語元模型和相應的法語元模型的示例：

![](assets/language-specific-meta-model-comparison.png)

## 使用自訂中繼模型修改最適化表單欄位 {#modify-adaptive-form-fields-using-custom-meta-model}

除了預設元模型中列出的模式和驗證之外，您的組織還可以具有模式和驗證。 您可以擴展預設元模型，以添加特定於貴組織的模式、驗證和實體。 automated forms conversion服務會在轉換期間將自訂中繼模型套用至表單欄位。 您可以隨著發現組織特有的新模式、驗證和實體而持續更新元模型。

automated forms conversion服務使用儲存在以下位置的預設元模型，在轉換期間將來源表單欄位對應至最適化表單欄位：

http://&lt;server>:&lt;port>/aem/forms.html/content/dam/formsanddocuments/metamodel/global.schema.json

不過，您可以在資料夾中儲存自訂中繼模型，並修改轉換服務屬性，以便在轉換期間使用自訂中繼模型。

### 轉換期間使用自訂中繼模型 {#use-custom-meta-model-during-conversion}

執行下列步驟以在轉換期間使用自訂中繼模型：

1. 在&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**&#x200B;中建立資料夾，並將自訂中繼模型JSON結構檔案上傳至資料夾。
1. 使用下列項目開啟轉換服務屬性：

   **[!UICONTROL Tools]** >  **[!UICONTROL Cloud Services]** >  **[!UICONTROL Automated Forms Conversion Configuration]**>所 **&lt;>選配置的屬性**>****

1. 在&#x200B;**[!UICONTROL Basic]**&#x200B;標籤中，在&#x200B;**[!UICONTROL Custom Meta-model]**&#x200B;欄位中指定自訂元模型的位置，然後點選&#x200B;**[!UICONTROL Save & Close]**。
1. [執行轉](convert-existing-forms-to-adaptive-forms.md#start-the-conversion-process) 換以將自訂元模型套用至轉換程式。

### 自訂元模型範例 {#custommetamodelexamples}

使用自訂中繼模型來修改最適化表單欄位屬性的一些常見範例包括：

* 修改表單欄位的標籤
* 修改表單欄位的類型
* 將幫助文本添加到表單欄位
* 在最適化表單中將表單欄位轉換為多選選項按鈕
* 修改表單欄位的格式
* 將驗證新增至最適化表單欄位
* 將表單欄位轉換為最適化表單中的下拉式清單選項
* 新增其他選項至下拉式清單
* 將字串欄位轉換為多行欄位

#### 修改表單欄位的標籤 {#modify-the-label-of-a-form-field}

**範例：** 轉換後，將表單中的「銀行帳號」標籤修改為最適化表單中的「自訂帳號」。

在此自訂中繼模型中，轉換服務使用&#x200B;**title**&#x200B;屬性作為搜尋關鍵字。 擷取表單中的&#x200B;**銀行帳號**&#x200B;文字後，轉換服務會以&#x200B;**aem:afProperties**&#x200B;區段中&#x200B;**jcr:title**&#x200B;屬性提及的&#x200B;**客戶帳號**&#x200B;字串取代文字。

```
{
  "numberfields": {
      "type": "number",
   "title": "Bank account number",
   "aem:afProperties" : {
    "jcr:title" : "Customer account number"
   }
   }
}
```

#### 修改表單欄位的類型 {#modify-the-type-of-a-form-field}

**範例**:在轉換 **後，** 修改表單中文本類型的銀行帳戶編號欄位，然後再轉換為最適化表單中的編號類型欄位。

在此自訂中繼模型中，轉換服務會使用&#x200B;**aem:affKeyword**&#x200B;內的文字作為搜尋關鍵字。 擷取表單中的&#x200B;**銀行帳號**&#x200B;文字後，轉換服務會使用&#x200B;**type**&#x200B;屬性將欄位轉換為數字類型。

```
{
  "numberfields": {
      "type": "number",
      "aem:affKeyword": ["Bank account number"]
 }
}
```

#### 將幫助文本添加到表單欄位 {#add-help-text-to-a-form-field}

**範例**:將「說明」文字新增至 **最適化** 表單的「銀行帳戶編號」欄位。

在此自訂中繼模型中，轉換服務會使用&#x200B;**aem:affKeyword**&#x200B;內的文字作為搜尋關鍵字。 擷取表單中的&#x200B;**銀行帳號**&#x200B;文字後，轉換服務會使用&#x200B;**description**&#x200B;屬性，將「說明」文字新增至最適化表單欄位。

```
{
  "numberfields": {
      "type": "number",
      "aem:affKeyword": ["Bank account number"],
   "description": "Specify your bank account number."
 }
}
```

#### 將表單欄位轉換為最適化表單中的多選核取方塊 {#convert-a-form-field-to-multiple-choice-check-boxes-in-the-adaptive-form}

**範例**:轉換前 **** 將表單中字串類型的「國家/地區」欄位轉換為轉換後最適化表單中的核取方塊。

在此自訂中繼模型中，轉換服務使用&#x200B;**aem:affKeyword**&#x200B;內的文字作為搜尋關鍵字。 擷取表單中的&#x200B;**Country**&#x200B;文字後，轉換服務會使用&#x200B;**enum**&#x200B;屬性，將欄位轉換為下列核取方塊：

* 印度
* 英格蘭
* 澳大利亞
* 紐西蘭

**sling:** resourceTypeand  **** guideNodeClassproperties將表單欄位對應至核取方塊適用性表單元件。

```
{
"title": {
    "aem:affKeyword": [
      "country"
    ],
    "type" : "string",
    "enum": [
      "India",
      "England",
      "Australia",
      "New Zealand"
    ],
    "aem:afProperties": {
      "sling:resourceType": "fd/af/components/guidecheckbox",
      "guideNodeClass": "guidecheckbox"
    }
  }
}
```

#### 修改表單欄位的格式 {#modify-the-format-of-a-form-field}

**範例**:將「電子郵件地址」 **的格** 式修改為電子郵件格式。

在此自訂中繼模型中，轉換服務使用&#x200B;**aem:affKeyword**&#x200B;內的文字作為搜尋關鍵字。 擷取表單中的&#x200B;**電子郵件地址**&#x200B;文字後，轉換服務會使用&#x200B;**format**&#x200B;屬性將欄位轉換為電子郵件格式。

```
{
   "additionalDetails" : {
      "aem:affKeyword": ["E-mail Address"],
       "type" : "string",
       "format" : "email"
  } 
}
```

#### 將驗證新增至最適化表單欄位 {#add-validations-to-adaptive-form-fields}

**範例1:** 將驗證新增至適 **用** 性表單的「郵遞區號」欄位。

在此自訂中繼模型中，轉換服務使用&#x200B;**aem:affKeyword**&#x200B;內的文字作為搜尋關鍵字。 擷取表單中的&#x200B;**郵遞區號**&#x200B;文字後，轉換服務會使用&#x200B;**aem:afProperties**&#x200B;區段中定義的&#x200B;**validatePictureClause**&#x200B;屬性，將驗證新增至欄位。 根據驗證，您在轉換後自適性表單中為&#x200B;**郵遞區號**&#x200B;欄位指定的輸入必須包含6個字元。

```
{
   "postalCode" : {
      "aem:affKeyword": ["Postal Code"],
      "type" : "string",
      "aem:afProperties" : {
        "validatePictureClause" : "\\d{6}"
      } 
   }
}
```

**範例2:** 將驗證新增至適 **用性** 表單的「銀行帳戶編號」欄位。

在此自訂中繼模型中，轉換服務使用&#x200B;**aem:affKeyword**&#x200B;內的文字作為搜尋關鍵字。 擷取表單中的&#x200B;**銀行帳號**&#x200B;文字後，轉換服務會使用&#x200B;**aem:afProperties**&#x200B;區段中定義的&#x200B;**強制**&#x200B;屬性，將驗證新增至欄位。 根據驗證，您必須先為&#x200B;**銀行帳號**&#x200B;欄位指定值，然後才能在轉換後提交表單。

```
{
  "numberfields": {
      "type": "number",
      "aem:affKeyword": ["Bank account number"],
   "aem:afProperties" : {
        "mandatory": "true"
      }   
   }
}
```

#### 將文字欄位轉換為最適化表單中的下拉式清單 {#convert-a-text-field-to-drop-down-list-in-the-adaptive-form}

**範例**:將轉換 **** 前表單中字串類型的「國家/地區」欄位轉換為轉換後最適化表單中的下拉式選項。

在此自訂中繼模型中，轉換服務使用&#x200B;**aem:affKeyword**&#x200B;內的文字作為搜尋關鍵字。 擷取表單中的&#x200B;**Country**&#x200B;文字後，轉換服務會使用&#x200B;**enum**&#x200B;屬性，將欄位轉換為下列下拉式清單選項：

* 印度
* 英格蘭
* 澳大利亞
* 紐西蘭

**sling:** resourceTypeand  **** guideNodeClassproperties將表單欄位對應至下拉式最適化表單元件。

```
{
"title": {
    "aem:affKeyword": [
      "country"
    ],
    "type" : "string",
    "enum": [
      "India",
      "England",
      "Australia",
      "New Zealand"
    ],
    "aem:afProperties": {
      "sling:resourceType": "fd/af/components/guidedropdownlist",
      "guideNodeClass": "guideDropDownlist"
    }
  }
}
```

#### 新增其他選項至下拉式清單 {#add-additional-options-to-the-drop-down-list}

**範例：** 使 **用** 自訂中繼模型，將Sri Lankaas新增為現有的下拉式清單中的額外選項。

若要新增額外的選項，請使用新選項更新&#x200B;**enum**&#x200B;屬性。 在此範例中，以&#x200B;**斯里蘭卡**&#x200B;作為額外選項更新&#x200B;**enum**&#x200B;屬性。 列於&#x200B;**enum**&#x200B;屬性中的值會顯示在下拉式清單中。

```
{
"title": {
    "aem:affKeyword": [
      "country"
    ],
    "type" : "string",
    "enum": [
      "India",
      "England",
      "Australia",
      "New Zealand",
   "Sri Lanka"
    ],
    "aem:afProperties": {
      "sling:resourceType": "fd/af/components/guidecheckbox",
      "guideNodeClass": "guidecheckbox"
    }
  }
}
```

#### 將字串欄位轉換為多行欄位 {#convert-a-string-field-to-a-multi-line-field}

**範例：** 轉換 **** 後，將字串類型的「位址」欄位轉換為表單中的多行欄位。

在此自訂中繼模型中，轉換服務使用&#x200B;**aem:affKeyword**&#x200B;內的文字作為搜尋關鍵字。 擷取表單中的&#x200B;**Address**&#x200B;文字後，服務會使用&#x200B;**aem:afProperties**&#x200B;區段中定義的&#x200B;**multiLine**&#x200B;屬性，將文字欄位轉換為多行欄位。

```
{
 "multiLine" : {
   "aem:affKeyword": [
      "Address"
    ],
    "type" : "string",
    "aem:afProperties": {
      "multiLine": "true"
    }
  }
}
```
