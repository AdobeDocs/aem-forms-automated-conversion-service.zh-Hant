---
title: 擴展預設元模型
seo-title: Extend the default meta-model
description: 擴展預設元模型，以添加特定於您的組織的模式、驗證和實體，並在運行Automated forms conversion服務時將配置應用於自適應表單域。
seo-description: Extend the default meta-model to add pattern, validations, and entities specific to your organization and apply configurations to adaptive form fields while running the Automated Forms Conversion service.
uuid: f98b4cca-f0a3-4db8-aef2-39b8ae462628
topic-tags: forms
discoiquuid: cad72699-4a4b-4c52-88a5-217298490a7c
exl-id: f679059c-18aa-4cb5-8368-ed27e96c20de
source-git-commit: e3ba3807668084495acb77f57ea2da6d5a53e626
workflow-type: tm+mt
source-wordcount: '2565'
ht-degree: 1%

---

# 擴展預設元模型 {#extend-the-default-meta-model}

automated forms conversion服務識別並提取源表單中的表單對象。 語義映射器幫助服務確定如何以自適應形式表示提取的對象。 例如，源窗體可以有多種不同類型的日期表示。 語義映射器幫助將源表單的日期表單對象的所有表示與自適應表單的日期元件進行映射。 語義映射器還允許服務在轉換期間對自適應表單元件預配置和應用驗證、規則、資料模式、幫助文本和輔助功能屬性。

![](assets/meta-model.gif)

元模型是JSON架構。 在開始使用元模型之前，請確保您精通JSON。 您必須具有建立、編輯和讀取以JSON格式保存的資料的經驗。

## 預設元模型 {#default-meta-model}

automated forms conversion服務具有預設元模型。 它是JSON架構，並駐留在Adobe雲上，與Automated forms conversion服務的其他元件一起。 您可以在本地伺服器上找到元模型的副本，AEM地址為：http://&lt;server>:&lt;port>/aem/forms.html/content/dam/formsanddocuments/metamodel/`global.schema.json`。 您也可以 [按一下這裡](assets/en.globalschema.json) 訪問或下載英語語言架構。 元模型 [法語](assets/fr.globalschema.json)。 [德語](assets/de.globalschema.json) [西班牙語](assets/es.globalschema.json)。 [義大利語](assets/it.globalschema.json), [葡萄牙語](assets/pt_br.globalschema.json) 語言也可供下載。

元模型的模式是從位於https://schema.org/docs/schemas.html的模式實體中派生的。 它有Person、PostalAddress、LocalBusiness和https://schema.org上定義的更多實體。 元模型的每個實體都遵守JSON架構對象類型。 以下代碼表示一個樣例元模型結構：

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

1. 登錄到您的AEM Forms實例。
1. 導航到 **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]** **>** **[!UICONTROL Meta Model]** 的子菜單。
1. 選擇 **[!UICONTROL global.schema.json]** 檔案和點擊 **[!UICONTROL Download]**。 將出現下載對話框。 選擇 **[!UICONTROL Download asset(s) as binary files]** 的雙曲餘切值。 點選 **[!UICONTROL Download]**。已下載存檔。

   <!--
   Comment Type: draft

   <li><p>Extract the archive and open the global.schema.json file for editing. </p> </li>
   -->

   <!--
   Comment Type: draft

   <li>Step text</li>
   -->

## 理解元模型 {#understanding-the-meta-model}

元模型指包含實體的JSON架構檔案。 JSON架構檔案中的所有實體都包括名稱和ID。 每個實體可包含多個屬性。 實體及其屬性可能因域而異。 可以使用關鍵字和欄位配置來擴展模式檔案，以將模式屬性映射到自適應表單元件。

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

在本例中， **事件** 表示具有值的實體的名稱 **ID** 如 **埃文蒂德**。 事件實體包括多個屬性：

* 開始日期
* 結束日期
* 位置

的 **全部** 元模型中的構造允許實體之間的繼承。

每個屬性還可包括：

* [JSON架構屬性](#jsonschemaproperties)
* [基於關鍵字的搜索將屬性應用於生成的自適應表單域](#keywordsearch)
* [其他屬性](#additionalproperties)

![元模型屬性](assets/meta_model_elements.gif)

基於使用 **aem:affKeyword**，轉換服務對源表單域執行搜索操作。 轉換服務將JSON架構屬性和附加屬性應用到滿足搜索條件的欄位。

在本示例中，轉換服務在源窗體中搜索電話、電話、行動電話、工作電話、家庭電話、電話號碼、電話號碼和電話號碼關鍵字。 基於包含這些關鍵字的欄位，轉換服務在轉換後將類型、模式和aem:afProperties應用到自適應表單欄位。

### 生成的自適應表單域的JSON架構屬性 {#jsonschemaproperties}

元模型支援以下JSON架構公共屬性，用於使用Automated forms conversion服務生成的自適應表單域：

<table> 
 <tbody> 
  <tr> 
   <th><strong>屬性名稱</strong></th> 
   <th><strong>說明</strong></th> 
  </tr> 
  <tr> 
   <td><p>標題</p></td> 
   <td> 
    <p>元模型中標題屬性內提及的文本用作搜索關鍵字，以對生成的自適應表單域執行操作。 例如，修改自適應表單域的標籤。 有關詳細資訊，請參見 <strong>修改表單域的標籤</strong> 在 <a href="#custommetamodelexamples">自定義元模型示例。</a></p> </td> 
  </tr>
  <td><p>說明</p></td> 
   <td> 
    <p>description屬性為生成的自適應表單欄位設定幫助文本。 有關詳細資訊，請參見 <strong>將幫助文本添加到表單域</strong> 在 <a href="#custommetamodelexamples">自定義元模型示例。</a></p> </td> 
  </tr>
  <td><p>類型</p></td> 
   <td> 
    <p>type屬性定義生成的自適應表單域的資料類型。 title屬性的可能值包括：</p>
    <ul> 
     <li>字串：生成文本資料類型的自適應表單域。</li> 
     <li>數字：生成數字資料類型的自適應表單域。</li>
     <li>整數：生成子類型設定為整數的數字資料類型的自適應表單域。</li>
     <li>布爾值：生成開關自適應窗體元件。</li>
     </ul><p>有關在元模型中使用type屬性的詳細資訊，請參見 <strong>修改表單域的類型</strong> 在 <a href="#custommetamodelexamples">自定義元模型示例。</a></p></td> 
  </tr>
  <td><p>圖案</p></td> 
   <td> 
    <p>該模式屬性基於規則運算式限制所生成的自適應表單域的值。 例如，元模型中的以下代碼將生成的自適應表單域的值限制為十位數：<br>"模式":"/\\d{10}/"<br>同樣，元模型中的以下代碼將欄位的值限制為特定日期格式。<br> "模式":"日期{DD MMM,YYYY}",</p> </td> 
  </tr>
  <td><p>格式</p></td> 
   <td> 
    <p>format屬性基於命名模式（而不是規則運算式）來限制生成的自適應表單域的值。 format屬性的可能值包括：<ul><li>電子郵件：生成電子郵件自適應表單元件。</li><li>主機名：生成文本框自適應窗體元件。</li></ul>有關在元模型中使用format屬性的詳細資訊，請參見 <strong>修改表單域的格式</strong> 在 <a href="#custommetamodelexamples">自定義元模型示例。</a></p> </td> 
  </tr>
  <td><p>枚舉和枚舉名稱</p></td> 
   <td> 
    <p>enum和enumNames屬性將下拉清單、複選框或單選按鈕欄位的值限制為固定集。 enumNames中列出的值將顯示在用戶介面上。 使用枚舉屬性列出的值用於計算。<br>有關詳細資訊，請參見 <strong>將表單域轉換為自適應表單中的多選項複選框</strong>。 <strong>將文本欄位轉換為自適應表單中的下拉清單</strong>, <strong>將其他選項添加到下拉清單</strong> 在 <a href="#custommetamodelexamples">自定義元模型示例。</a></p> </td> 
  </tr>
 </tbody> 
</table>

### 基於關鍵字的搜索將屬性應用於生成的自適應表單域 {#keywordsearch}

automated forms conversion服務在轉換期間對源表單執行關鍵字搜索。 在過濾滿足搜索標準的欄位後，轉換服務將為元模型中那些欄位定義的屬性應用到生成的自適應表單欄位。

使用 **aem:affKeyword** 屬性。

```
{
  "numberfields": {
      "type": "number",
      "aem:affKeyword": ["Bank account number"]
 }
}
```

在本示例中，轉換服務使用 **aem:affKeyword** 搜索關鍵字。 檢索 **銀行帳號** 文本，轉換服務將欄位轉換為 **數** 使用 **類型** 屬性。

### 生成的自適應表單域的附加屬性 {#additionalproperties}

您可以使用 **aem:afProperties** 在元模型中為使用Automated forms conversion服務生成的自適應表單域定義以下附加屬性：

<table> 
 <tbody> 
  <tr> 
   <th><strong>屬性名稱</strong></th> 
   <th><strong>說明</strong></th> 
  </tr> 
  <tr> 
   <td><p>多行</p></td> 
   <td> 
    <p>multiLine屬性在轉換後將源表單域轉換為自適應表單中的多行欄位。 有關詳細資訊，請參見 <strong>將字串欄位轉換為多行欄位</strong> 在 <a href="#custommetamodelexamples">自定義元模型示例。</a></p> </td> 
  </tr>
  <td><p>強制</p></td> 
   <td> 
    <p>強制屬性將轉換後自適應表單域的輸入設定為強制。<br>有關詳細資訊，請參見 <strong>將驗證添加到自適應表單域</strong> 在 <a href="#custommetamodelexamples">自定義元模型示例。</a></p>
    </td> 
  </tr>
  <td><p>jcr:title</p></td> 
   <td> 
    <p>jcr:title屬性（帶有標題JSON架構屬性）使您能夠在轉換後修改自適應表單欄位的標籤。<br>有關詳細資訊，請參見 <strong>修改表單域的標籤</strong> 在 <a href="#custommetamodelexamples">自定義元模型示例。</a><br>請參閱 <a href="https://helpx.adobe.com/experience-manager/6-5/forms/using/adaptive-form-json-schema-form-model.html" target="_blank">使用JSON架構建立自適應表單</a> 有關可以使用JSON架構應用於自適應表單域的更多屬性的資訊。</p>
    <p></p></td> 
  </tr>
  <td><p>sling:resourceType和guideNodeClass</p></td> 
   <td> 
    <p>sling:resourceType和guideNodeClass屬性使您能夠將表單域映射到相應的自適應表單元件。<br>有關詳細資訊，請參見 <strong>將表單域轉換為自適應表單中的多選項複選框</strong> 和 <strong>將文本欄位轉換為自適應表單中的下拉清單</strong> 在 <a href="#custommetamodelexamples">自定義元模型示例。</a></p> </td> 
  </tr>
  <td><p>validatePictureClause</p></td> 
   <td> 
    <p>validatePictureClause屬性設定轉換後自適應表單欄位中允許的格式的驗證。<br>有關詳細資訊，請參見 <strong>將驗證添加到自適應表單域</strong> 在 <a href="#custommetamodelexamples">自定義元模型示例。</p> </td> 
  </tr>
 </tbody> 
</table>

## 使用您自己的語言建立自定義元模型{#language-specific-meta-model}

可以建立語言特定的元模型。 這種元模型有助於您以自己選擇的語言建立映射規則。 automated forms conversion服務允許您以下語言建立元模型：

* English(en)
* French(fr)
* German(de)
* Spanish(es)
* Italian(it)
* 葡萄牙語(pt-br)

添加 *aem：語言* 元模型的頂部為metatag標籤以指定其語言。 例如，

```JSON
"metaTags": {
        "aem:Language": "fr"
    }
```

當未指定任何語言時，服務會認為元模型是英語。

### 建立語言特定元模型的注意事項

* 確保每個鍵的名稱都是英語。 例如， emailAddress。
* 確保所有實體引用和所有id鍵的預定義值僅包含ASCII字元。 例如&quot;id&quot;:&quot;ContactPoint&quot; / &quot;$ref&quot;:&quot;#ContactPoint&quot;。
* 確保與下列鍵對應的所有值都使用指定的元模型語言：
   * aem:affKeyword
   * 標題
   * 說明
   * 枚舉名稱
   * shortDescription（簡短描述）
   * validatePictureClauseMessage

   例如，當元模型的語言是法語(「aem:Language」)時：「fr」)，確保所有說明和消息都使用法語。

* 確保所有 [JSON架構屬性](#jsonschemaproperties) 僅使用支援的值。 例如，type屬性只能跨選定的String、Number、Integer和Boolean值。

下圖顯示了英語元模型和相應法語元模型的示例：

![](assets/language-specific-meta-model-comparison.png)

## 使用自定義元模型修改自適應表單域 {#modify-adaptive-form-fields-using-custom-meta-model}

除了預設元模型中列出的模式和驗證外，您的組織還可以有模式和驗證。 可以擴展預設元模型，以添加特定於您組織的模式、驗證和實體。 automated forms conversion服務在轉換期間將自定義元模型應用於表單域。 您可以在發現新模式、驗證和特定於您組織的實體時，繼續更新元模型。

automated forms conversion服務使用在以下位置保存的預設元模型，在轉換期間將源表單域映射到自適應表單域：

http://&lt;server>:&lt;port>/aem/forms.html/content/dam/formsanddocuments/metamodel/global.schema.json

但是，可以將自定義元模型保存在資料夾中，並修改轉換服務屬性以在轉換期間使用自定義元模型。

### 在轉換過程中使用自定義元模型 {#use-custom-meta-model-during-conversion}

執行以下步驟以在轉換期間使用自定義元模型：

1. 在中建立資料夾 **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]** 並將自定義元模型JSON架構檔案上載到資料夾。
1. 使用以下方式開啟轉換服務屬性：

   **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Automated Forms Conversion Configuration]** > **&lt;properties of=&quot;&quot; selected=&quot;&quot; configuration=&quot;&quot;>**

1. 在 **[!UICONTROL Basic]** 頁籤中，指定自定義元模型的位置 **[!UICONTROL Custom Meta-model]** 欄位和攻擊 **[!UICONTROL Save & Close]**。
1. [運行轉換](convert-existing-forms-to-adaptive-forms.md#start-the-conversion-process) 將自定義元模型應用到轉換進程。

### 自定義元模型示例 {#custommetamodelexamples}

使用自定義元模型修改自適應表單域屬性的一些常見示例包括：

* 修改表單域的標籤
* 修改表單域的類型
* 將幫助文本添加到表單域
* 將表單域轉換為自適應表單中的多選單選按鈕
* 修改表單域的格式
* 將驗證添加到自適應表單域
* 將表單域轉換為自適應表單中的下拉清單選項
* 將其他選項添加到下拉清單
* 將字串欄位轉換為多行欄位

#### 修改表單域的標籤 {#modify-the-label-of-a-form-field}

**示例：** 在轉換後，將窗體中的銀行帳號標籤修改為自適應窗體中的自定義帳號。

在此自定義元模型中，轉換服務使用 **標題** 屬性。 檢索 **銀行帳號** 文本，轉換服務將文本替換為 **客戶帳號** 與 **jcr：標題** 屬性 **aem:afProperties** 的子菜單。

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

#### 修改表單域的類型 {#modify-the-type-of-a-form-field}

**示例**:修改 **銀行帳號** 在轉換後轉換為自適應表單中的「數字類型」欄位之前，在窗體中輸入文本類型的欄位。

在此自定義元模型中，轉換服務使用 **aem:affKeyword** 搜索關鍵字。 檢索 **銀行帳號** 文本，轉換服務使用 **類型** 屬性。

```
{
  "numberfields": {
      "type": "number",
      "aem:affKeyword": ["Bank account number"]
 }
}
```

#### 將幫助文本添加到表單域 {#add-help-text-to-a-form-field}

**示例**:將幫助文本添加到 **銀行帳號** 自適應窗體的欄位。

在此自定義元模型中，轉換服務使用 **aem:affKeyword** 搜索關鍵字。 檢索 **銀行帳號** 文本，轉換服務使用 **描述** 屬性。

```
{
  "numberfields": {
      "type": "number",
      "aem:affKeyword": ["Bank account number"],
   "description": "Specify your bank account number."
 }
}
```

#### 將表單域轉換為自適應表單中的多選項複選框 {#convert-a-form-field-to-multiple-choice-check-boxes-in-the-adaptive-form}

**示例**:轉換 **國家/地區** 在轉換之前，在自適應窗體中選擇「轉換後」複選框。

在此自定義元模型中，轉換服務使用 **aem:affKeyword** 搜索關鍵字。 檢索 **國家/地區** 文本，轉換服務使用 **枚舉** 屬性：

* 印度
* 英格蘭
* 澳大利亞
* 紐西蘭

**sling:resourceType** 和 **guideNodeClass** 屬性將表單域映射到複選框自適應表單元件。

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

#### 修改表單域的格式 {#modify-the-format-of-a-form-field}

**示例**:修改 **電子郵件地址** 的子菜單。

在此自定義元模型中，轉換服務使用 **aem:affKeyword** 搜索關鍵字。 檢索 **電子郵件地址** 文本，轉換服務使用 **格式** 屬性。

```
{
   "additionalDetails" : {
      "aem:affKeyword": ["E-mail Address"],
       "type" : "string",
       "format" : "email"
  } 
}
```

#### 將驗證添加到自適應表單域 {#add-validations-to-adaptive-form-fields}

**示例1:** 將驗證添加到 **郵遞區號** 的子菜單。

在此自定義元模型中，轉換服務使用 **aem:affKeyword** 鍵。 檢索 **郵遞區號** 文本，轉換服務使用 **validatePictureClause** 在 **aem:afProperties** 的子菜單。 根據驗證，為 **郵遞區號** 轉換後自適應表單中的欄位必須包含六個字元。

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

**示例2:** 將驗證添加到 **銀行帳號** 的子菜單。

在此自定義元模型中，轉換服務使用 **aem:affKeyword** 鍵。 檢索 **銀行帳號** 文本，轉換服務使用 **強制** 在 **aem:afProperties** 的子菜單。 根據驗證，必須為 **銀行帳號** 的子菜單。

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

#### 將文本欄位轉換為自適應表單中的下拉清單 {#convert-a-text-field-to-drop-down-list-in-the-adaptive-form}

**示例**:轉換 **國家/地區** 轉換前的窗體中的字串類型欄位，轉換後的自適應窗體中的下拉清單選項。

在此自定義元模型中，轉換服務使用 **aem:affKeyword** 鍵。 檢索 **國家/地區** 文本，轉換服務使用 **枚舉** 屬性：

* 印度
* 英格蘭
* 澳大利亞
* 紐西蘭

**sling:resourceType** 和 **guideNodeClass** 屬性將表單域映射到下拉自適應表單元件。

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

#### 將其他選項添加到下拉清單 {#add-additional-options-to-the-drop-down-list}

**示例：** 添加 **斯里蘭卡** 作為現有下拉清單的附加選項。

要添加附加選項，請更新 **枚舉** 的下界。 在此示例中，更新 **枚舉** 屬性 **斯里蘭卡** 作為附加選項。 中列出的值 **枚舉** 屬性顯示在下拉清單中。

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

**示例：** 轉換 **地址** 字串類型的欄位轉換為轉換後窗體中的多行欄位。

在此自定義元模型中，轉換服務使用 **aem:affKeyword** 鍵。 檢索 **地址** 文本，服務使用 **多行** 在 **aem:afProperties** 的子菜單。

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
