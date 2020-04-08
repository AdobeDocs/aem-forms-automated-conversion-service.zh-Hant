---
title: 擴展預設元模型
seo-title: 擴展預設元模型
description: 擴充預設中繼模型，以新增組織專屬的模式、驗證和實體，並在執行自動表單轉換服務時將組態套用至最適化表單欄位。
seo-description: 擴充預設中繼模型，以新增組織專屬的模式、驗證和實體，並在執行自動表單轉換服務時將組態套用至最適化表單欄位。
uuid: f98b4cca-f0a3-4db8-aef2-39b8ae462628
topic-tags: forms
discoiquuid: cad72699-4a4b-4c52-88a5-217298490a7c
translation-type: tm+mt
source-git-commit: ffab4d916cbd545078f4b72b8de5c9968f23b0da

---


# 擴展預設元模型 {#extend-the-default-meta-model}

Automated Forms Conversion服務可識別並擷取來源表單中的表單物件。 語義映射器幫助服務決定如何以自適應形式表示提取的對象。 例如，來源表單可以有許多不同的日期表示類型。 語義映射器幫助將源表單的日期表單對象的所有表示與自適應表單的日期元件映射。 語義映射器還允許服務在轉換期間預先配置並應用驗證、規則、資料模式、幫助文本和輔助功能屬性到自適應表單元件。

![](assets/meta-model.gif)

Meta-model是JSON結構描述。 在您開始使用meta-model之前，請確定您已熟悉JSON。 您必須具備建立、編輯和讀取儲存為JSON格式之資料的經驗。

## 預設元模型 {#default-meta-model}

自動表單轉換服務有預設的中繼模型。 它是JSON結構描述，並與Automated Forms Conversion服務的其他元件一起駐留在Adobe Cloud。 您可在本機AEM伺服器上尋找中繼模型的副本，網址為：

http://&lt;server>:&lt;port>/aem/forms.html/content/dam/formsanddocuments/metamodel/global.schema.json。

元模型的模式是從位於https://schema.org/docs/schemas.html的模式實體中衍生出來的。 它有Person、PostalAddress、LocalBusiness等實體，定義於https://schema.org。 中繼模型的每個實體都符合JSON結構描述物件類型。 下列程式碼代表範例元模型結構：

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

## 下載預設中繼模型 {#download-the-default-meta-model}

執行以下步驟將預設元模型下載到本地檔案系統：

1. 登入您的AEM Forms例項。
1. 導覽至 **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]** > ******[!UICONTROL Meta Model]** 資料夾。
1. 選取檔 **[!UICONTROL global.schema.json]** 案並點選 **[!UICONTROL Download]**。 將出現下載對話框。 選擇選 **[!UICONTROL Download asset(s) as binary files]** 項。 點選 **[!UICONTROL Download]**。 會下載封存。

   <!--
   Comment Type: draft

   <li><p>Extract the archive and open the global.schema.json file for editing. </p> </li>
   -->

   <!--
   Comment Type: draft

   <li>Step text</li>
   -->

## 瞭解元模型 {#understanding-the-meta-model}

中繼模型會參照包含實體的JSON結構描述檔。 JSON結構描述檔中的所有實體都包含名稱和ID。 每個實體可包含多個屬性。 圖元及其屬性可能會根據域而有所不同。 您可以使用關鍵字和欄位配置來增強模式檔案，以將模式屬性映射到自適應表單元件。

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

在此範例中， **Event** 代表實體的名稱，其值的 **id為****Eventid**。 事件實體包含多個屬性：

* startDate
* endDate
* 位置

元模 **型中的** allOf構造可實現圖元間的繼承。

每個屬性可進一步包括：

* [JSON結構描述屬性](#jsonschemaproperties)
* [將屬性套用至產生的最適化表單欄位的關鍵字搜尋](#keywordsearch)
* [其他屬性](#additionalproperties)

![元模型屬性](assets/meta_model_elements.gif)

根據使用 **aem:affKeyword所參考的關鍵字**，轉換服務會對來源表單欄位執行搜尋作業。 轉換服務會將JSON結構描述屬性和其他屬性套用至符合搜尋准則的欄位。

在此範例中，轉換服務在來源表單中搜尋電話、電話、行動電話、工作電話、家庭電話、電話號碼、電話號碼關鍵字。 根據包含這些關鍵字的欄位，轉換服務會在轉換後將type、pattern和aem:afProperties套用至最適化表單欄位。

### 產生的最適化表單欄位的JSON結構描述屬性 {#jsonschemaproperties}

中繼模型支援下列JSON結構描述通用屬性，以用於使用「自動表單轉換」服務產生的最適化表單欄位：

<table> 
 <tbody> 
  <tr> 
   <th><strong>屬性名稱</strong></th> 
   <th><strong>說明</strong></th> 
  </tr> 
  <tr> 
   <td><p>標題</p></td> 
   <td> 
    <p>中繼模型中標題屬性中提及的文字會當做搜尋關鍵字，以對產生的最適化表單欄位執行動作。 例如，修改最適化表單欄位的標籤。 如需詳細資訊，請 <strong>參閱自訂中繼模型範例中的</strong><a href="#custommetamodelexamples">修改表單欄位標籤。</a></p> </td> 
  </tr>
  <td><p>說明</p></td> 
   <td> 
    <p>description屬性為生成的自適應表單欄位設定幫助文本。 如需詳細資訊，請參 <strong>閱自訂中繼模型範例中的「新增說明</strong><a href="#custommetamodelexamples">文字至表單欄位」。</a></p> </td> 
  </tr>
  <td><p>類型</p></td> 
   <td> 
    <p>type屬性定義生成的自適應表單域的資料類型。 標題屬性的可能值包括：</p>
    <ul> 
     <li>字串：生成文本資料類型的自適應表單欄位。</li> 
     <li>數字：生成數字資料類型的自適應表單欄位。</li>
     <li>整數：生成具有子類型設定為整數的數字資料類型的自適應表單欄位。</li>
     <li>布林值：生成交換機自適應表單元件。</li>
     </ul><p>有關在元模型中使用type屬性的詳細資訊，請參 <strong>閱自定義元模型示例中的</strong><a href="#custommetamodelexamples">修改表單欄位類型。</a></p></td> 
  </tr>
  <td><p>模式</p></td> 
   <td> 
    <p>pattern屬性基於規則運算式來限制生成的自適應表單域的值。 例如，中繼模型中的下列程式碼會將產生的最適化表單欄位值限制為十位數：<br>"pattern":"/\\d{10}/"同樣地，中繼模型中的下列程式碼會限制欄位的值為特定的日期格式。<br><br> 「模式」:"date{DD MMM, YYYY}",</p> </td> 
  </tr>
  <td><p>格式</p></td> 
   <td> 
    <p>format屬性會根據命名模式（而非規則運算式）來限制所產生的最適化表單欄位的值。 format屬性的可能值包括：<ul><li>電子郵件：產生電子郵件最適化表單元件。</li><li>主機名：生成文本框自適應表單元件。</li></ul>有關在元模型中使用format屬性的詳細資訊，請參 <strong>閱自定義元模型示例中的</strong><a href="#custommetamodelexamples">修改表單欄位的格式。</a></p> </td> 
  </tr>
  <td><p>enum和enumNames</p></td> 
   <td> 
    <p>enum和enumNames屬性將下拉式清單、核取方塊或選項按鈕欄位的值限制為固定集。 enumNames中列出的值顯示在用戶介面上。 使用enum屬性列出的值用於計算。<br>如需詳細資訊，請參 <strong>閱「在最適化表單中將表單欄位轉換為多選項」核取方塊、「在最適化表單中將文字欄位轉換為下拉式清單</strong>」，以及「自訂中繼模型範例」中的「將其他選項新增至下拉式清單 <strong></strong><strong></strong><a href="#custommetamodelexamples">」。</a></p> </td> 
  </tr>
 </tbody> 
</table>

### 將屬性套用至產生的最適化表單欄位的關鍵字搜尋 {#keywordsearch}

Automated Forms Conversion服務會在轉換期間對來源表單執行關鍵字搜尋。 篩選符合搜尋准則的欄位後，轉換服務會將中繼模型中這些欄位所定義的屬性套用至產生的最適化表單欄位。

使用 **aem:affKeyword屬性參考關鍵字** 。

```
{
  "numberfields": {
      "type": "number",
      "aem:affKeyword": ["Bank account number"]
 }
}
```

在此範例中，轉換服務會使用 **aem:affKeyword中的文字作為搜尋關鍵字** 。 在擷取表單 **中的「銀行帳號** 」文字後，轉換服務會使用type屬性，將欄位 **轉換為** 數字類型 **** 。

### 產生的最適化表單欄位的其他屬性 {#additionalproperties}

您可以使用 **meta-model中的aem:afProperties** 屬性，為使用「自動表單轉換」服務產生的最適化表單欄位定義下列其他屬性：

<table> 
 <tbody> 
  <tr> 
   <th><strong>屬性名稱</strong></th> 
   <th><strong>說明</strong></th> 
  </tr> 
  <tr> 
   <td><p>multiLine</p></td> 
   <td> 
    <p>multiLine屬性在轉換後，會將來源表單欄位轉換為自適應表單中的多行欄位。 如需詳細資訊，請 <strong>參閱自訂中繼模型範例中的「將字串欄位轉換為多行欄位</strong><a href="#custommetamodelexamples">」(Convert a string field to a multi-line field)。</a></p> </td> 
  </tr>
  <td><p>強制</p></td> 
   <td> 
    <p>強制屬性將轉換後最適化表單欄位的輸入設為強制。<br>如需詳細資訊，請參 <strong>閱自訂中繼模型範例中的新增驗證至</strong><a href="#custommetamodelexamples">最適化表單欄位。</a></p>
    </td> 
  </tr>
  <td><p>jcr:title</p></td> 
   <td> 
    <p>jcr:title屬性與標題JSON結構描述屬性可讓您在轉換後修改最適化表單欄位的標籤。<br>如需詳細資訊，請 <strong>參閱自訂中繼模型範例中的</strong><a href="#custommetamodelexamples">修改表單欄位標籤。</a><br>如需 <a href="https://helpx.adobe.com/experience-manager/6-5/forms/using/adaptive-form-json-schema-form-model.html" target="_blank"></a> 您可以套用至使用JSON結構描述之最適化表單欄位的更多屬性資訊，請參閱使用JSON結構描述建立最適化表單。</p>
    <p></p></td> 
  </tr>
  <td><p>sling:resourceType和guideNodeClass</p></td> 
   <td> 
    <p>sling:resourceType和guideNodeClass屬性可讓您將表單欄位對應至對應的最適化表單元件。<br>如需詳細資訊，請參 <strong>閱自訂中繼模型範例中最適化表單中的「將表單欄位轉換為多選項」核取方塊</strong><strong></strong><a href="#custommetamodelexamples">，以及將文字欄位轉換為最適化表單中的下拉式清單。</a></p> </td> 
  </tr>
  <td><p>validatePictureClause</p></td> 
   <td> 
    <p>validatePictureClause屬性會針對轉換後自適應表單欄位中允許的格式設定驗證。<br>如需詳細資訊，請參 <strong>閱自訂中繼模型範例中的新增驗證至</strong><a href="#custommetamodelexamples">最適化表單欄位。</p> </td> 
  </tr>
 </tbody> 
</table>

## 使用自訂元模型修改自適應表單欄位 {#modify-adaptive-form-fields-using-custom-meta-model}

除了預設中繼模型中列出的模式和驗證外，您的組織也可以有這些模式和驗證。 可以擴展預設元模型，以添加特定於組織的模式、驗證和圖元。 「自動表單轉換」服務會在轉換期間將自訂中繼模型套用至表單欄位。 您可以不斷更新元模型，將其作為新模式、驗證和特定於您組織的實體被發現。

自動表單轉換服務使用儲存在下列位置的預設中繼模型，在轉換期間將來源表單欄位對應至最適化表單欄位：

http://&lt;server>:&lt;port>/aem/forms.html/content/dam/formsanddocuments/metamodel/global.schema.json

不過，您可以將自訂中繼模型儲存在資料夾中，並修改轉換服務屬性，以便在轉換期間使用自訂中繼模型。

### 在轉換期間使用自訂中繼模型 {#use-custom-meta-model-during-conversion}

執行下列步驟，在轉換期間使用自訂中繼模型：

1. 在>中建立資 **[!UICONTROL Forms]** 料夾 **[!UICONTROL Forms & Documents]** ，並將自訂中繼模型JSON結構描述檔上傳至資料夾。
1. 使用下列方式開啟轉換服務屬性：

   **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Automated Forms Conversion Configuration]**> **&lt;選定配置的**&#x200B;屬性&#x200B;**>**

1. 在標 **[!UICONTROL Basic]** 簽中，指定自訂中繼模型在欄位中的位置並 **[!UICONTROL Custom Meta-model]** 點選 **[!UICONTROL Save & Close]**。
1. [執行轉換](convert-existing-forms-to-adaptive-forms.md#start-the-conversion-process) ，將自訂元模型套用至轉換程式。

### 自訂元模型範例 {#custommetamodelexamples}

使用自訂元模型修改自適應表單欄位屬性的常見範例包括：

* 修改表單欄位的標籤
* 修改表單欄位的類型
* 將「說明」文字新增至表格欄位
* 將表單欄位轉換為最適化表單中的多選單選按鈕
* 修改表單欄位的格式
* 新增驗證至最適化表單欄位
* 將表單欄位轉換為最適化表單中的下拉式清單選項
* 新增其他選項至下拉式清單
* 將字串欄位轉換為多行欄位

#### 修改表單欄位的標籤 {#modify-the-label-of-a-form-field}

**範例：** 在轉換後，將表單中的銀行帳號標籤修改為最適化表單中的自訂帳號。

在此自訂元模型中，轉換服務會使用 **title** 屬性作為搜尋關鍵字。 在擷取表單中的 **Bank帳號** ，轉換服務會以在 **aem:PropertiesSection中提及的** jcr:title ******** 屬性的Customer帳號字串取代文字。

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

**範例**:在轉換 **後，修改表單中文字類型的「銀行帳戶號碼** 」欄位，再轉換為最適化表單中的「編號類型」欄位。

在此自訂中繼模型中，轉換服務會使用 **aem:affKeyword中的文字作為搜尋關鍵字** 。 在擷取表單 **中的「銀行帳號** 」文字後，轉換服務會使用type屬性，將欄位轉換為 **數字類型** 。

```
{
  "numberfields": {
      "type": "number",
      "aem:affKeyword": ["Bank account number"]
 }
}
```

#### 將「說明」文字新增至表格欄位 {#add-help-text-to-a-form-field}

**範例**:將「說明」文字新增至 **最適化表單的「銀行帳號** 」欄位。

在此自訂中繼模型中，轉換服務會使用 **aem:affKeyword中的文字作為搜尋關鍵字** 。 在擷取表單 **中的銀行帳號** (Bank account number **)文字後，轉換服務會使用description屬性，將「說明(Help)」文字新增至最適化表** 單欄位。

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

**範例**:在轉換 **前，將表單中字串類型的「國家／地區** 」欄位轉換為轉換後最適化表單中的核取方塊。

在此自訂中繼模型中，轉換服務會使用 **aem:affKeyword中的文字作為搜尋關鍵字** 。 在擷取表單中 **的Country** 文字後，轉換服務會使用enum屬性，將欄位轉換為下列核 **取方塊** :

* 印度
* 英格蘭
* 澳大利亞
* 紐西蘭

**sling:resourceType** and **guideNodeClass** properties將表單欄位對應至核取方塊最適化表單元件。

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

**範例**:將「電子郵件地址」欄 **位的格式** ，修改為電子郵件格式。

在此自訂中繼模型中，轉換服務會使用 **aem:affKeyword中的文字作為搜尋關鍵字** 。 在擷取表單 **中的「電子郵件位址** 」文字後，轉換服務會使用format屬性，將欄位轉換為電子郵件 **格式** 。

```
{
   "additionalDetails" : {
      "aem:affKeyword": ["E-mail Address"],
       "type" : "string",
       "format" : "email"
  } 
}
```

#### 新增驗證至最適化表單欄位 {#add-validations-to-adaptive-form-fields}

**範例1:** 新增驗證至最適化 **表單的「郵遞區號** 」欄位。

在此自訂中繼模型中，轉換服務會使用 **aem:affKeyword中的文字作為搜尋關鍵字** 。 在擷取表單中 **的「郵遞區號** 」文字後，轉換服務會使用aem:afProperties區段中定義的 **validatePictureClause** 屬性，將驗證新增至 **** 欄位。 根據驗證，您在轉換後以最適化表單為「郵遞區號 **** 」欄位所指定的輸入必須包含6個字元。

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

**範例2:** 將驗證新增至最適 **化表單的** 「銀行帳號」欄位。

在此自訂中繼模型中，轉換服務會使用 **aem:affKeyword中的文字作為搜尋關鍵字** 。 在擷取表單中 **的Bank帳號** ( **Bank account number** )文字後，轉換服務會使用aem:afProperties區段中定義的強制屬性，將驗證新增至欄位 **** 。 根據驗證，您必須先為「銀行帳號」欄位指定值， **然後才能在轉換後** 提交表格。

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

**範例**:將轉換 **前表單中字串類型的「國家** 」欄位轉換為轉換後最適化表單中的下拉式選項。

在此自訂中繼模型中，轉換服務會使用 **aem:affKeyword中的文字作為搜尋關鍵字** 。 在擷取表單 **中的Country** 文字後，轉換服務會使用enum屬性，將欄位轉換為下列下拉式清單 **選項** :

* 印度
* 英格蘭
* 澳大利亞
* 紐西蘭

**sling:resourceType** and **guideNodeClass** properties將表單欄位對應至下拉式最適化表單元件。

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

**範例：** 使用 **自訂中繼模型** ，將斯里蘭卡新增為現有下拉式清單的額外選項。

若要新增額外選項，請使用新 **選項** ，更新enum屬性。 在此範例中，以 **Sri Lanka** 為額外選 **項更新enum屬性** 。 列於列舉 **屬性中** 的值會顯示在下拉式清單中。

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

**範例：** 轉換 **後** ，將字串類型的「位址」欄位轉換為表單中的多行欄位。

在此自訂中繼模型中，轉換服務會使用 **aem:affKeyword中的文字作為搜尋關鍵字** 。 在擷取表單中 **的Address** 文字後，服務會使用aem:afProperties區段中定義的多行屬性，將文字欄位轉換為多行欄位 ******** 。

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
