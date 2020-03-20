---
title: 基於資料來源的建議預填及提交最適化表單的工作流程
seo-title: 最適化表單的預先填寫和提交選項
description: 針對使用Automated Forms Conversion Service產生的最適化表單，以資料來源為基礎的預填和提交工作流程。
seo-description: 針對使用Automated Forms Conversion Service產生的最適化表單，以資料來源為基礎的預填和提交工作流程。
uuid: 91409a82-141c-4233-82b1-1539a0b250f8
contentOwner: khsingh
topic-tags: forms
discoiquuid: cad34fff-7f9f-4a27-8b5c-d0a523903eec
privatebeta: true
translation-type: tm+mt
source-git-commit: caccb547a5741eb0e70ddf75630a661f8fe75cb3

---


# 基於資料來源的建議預填及提交最適化表單的工作流程 {#recommended-data-source-btased-prefill-and-submit-workflows-for-adaptive-forms}

您可以使用下列任何資料來源搭配使用自動表單轉換服務轉換的最適化表單：

* 表單資料模型、OData或任何其他第三方服務
* JSON結構描述
* XSD架構

根據資料來源，您可以選擇產生具有或不具有資料模型的最適化表單。

本文說明在選取資料來源並使用轉換服務產生最適化表單後，預先填寫欄位值和提交選項的建議工作流程。

<table> 
 <tbody> 
  <tr> 
   <th><strong>資料來源</strong></th> 
   <th><strong>建議的工作流程</strong></th> 
  </tr> 
  <tr> 
   <td><p>表單資料模型、OData或任何其他第三方服務</p></td> 
   <td> 
    <p><strong>選項1</strong>:您選擇表單資料模型、OData或任何其他第三方服務作為資料源。 您可 <a href="#generate-adaptive-forms-with-no-data-binding">以使用「自動表單轉換」服務</a> ，產生沒有資料系結的最適化表單。 您可以手動將最適化表單欄位系結為表單資料模型實體，並使用「表單資料模型預填服務」選項來預填欄位值。 您可以使用「使用表單資料模型提交」選項來提交最適化表單。</p></td> 
  </tr>
  <tr> 
   <td></td> 
   <td> 
   <p><strong>選項2</strong>:您選擇表單資料模型、OData或任何其他第三方服務作為資料源。 您可 <a href="#generate-adaptive-forms-with-no-data-binding">以使用「自動表單轉換」服務</a> ，產生沒有資料系結的最適化表單。 您可使用規則編輯器來系結最適化表單欄位，以預先填入欄位值。 如有必要，請修改欄位值，並將資料送出至crx-repository。</p>
    </td> 
  </tr>
  <tr> 
   <td></td> 
   <td> 
    <p>有關執行這些工作流的逐步說明，請參 <a href="#sqldatasource">閱使用資料庫、OData或任何第三方服務作為資料源。</a></p> </td> 
  </tr>
  <tr>
  <td><p>JSON結構描述</p></td> 
   <td> 
    <p>您選取JSON結構描述作為資料來源。 根據選取的資料來源：</p></td> 
  </tr>
  <tr>
  <td></td> 
   <td> 
    <p><strong>選項1</strong>:您可 <a href="#generate-adaptive-forms-with-no-data-binding">以使用「自動表單轉換」服務</a> ，產生沒有資料系結的最適化表單，並將JSON結構描述設定為資料來源。 您可以手動將最適化表單欄位系結至JSON結構描述， <a href="https://helpx.adobe.com/experience-manager/6-5/forms/using/prepopulate-adaptive-form-fields.html#Supportedprotocolsforprefillinguserdata" target="_blank">並使用任何支援的通訊協定</a> ，來預先填寫欄位值。 如有必要，請修改欄位值，並將資料送出至crx-repository。</p></td> 
  </tr>
  <tr>
  <td></td> 
   <td> 
    <p>如需執行工作流程的逐步指示，請參 <a href="#jsondatasource">閱使用JSON結構描述作為資料來源。</p></td> 
  </tr>
  <tr>
  <td></td> 
   <td> 
    <p><strong>選項2</strong>:您可 <a href="#generate-adaptive-forms-with-json-binding">以使用「自動表單轉換」服務</a> ，產生具有JSON資料系結的最適化表單。 預填服務和表單提交功能十分順暢。 您不需要任何設定步驟。</p> </td> 
  </tr>
   <tr>
  <td></td> 
   <td> 
    <p>如需執行工作流程的逐步指示，請參 <a href="#jsonwithdatabinding">閱使用JSON結構描述作為資料來源。</a></p> </td> 
  </tr>
  <tr>
  <td><p>XSD架構</p></td> 
   <td> 
    <p>您選擇XSD方案作為資料源。 根據選取的資料來源，您可 <a href="#generate-adaptive-forms-with-no-data-binding">以使用「自動表單轉換」服務產生沒有資料系結的自適應表單</a> ，並將XSD架構設定為資料來源。 您可以手動將最適化表單欄位系結至XSD架構， <a href="https://helpx.adobe.com/experience-manager/6-5/forms/using/prepopulate-adaptive-form-fields.html#Supportedprotocolsforprefillinguserdata" target="_blank">並使用任何支援的通訊協定</a> ，來預先填入欄位值。 如有必要，請修改欄位值，並將資料送出至crx-repository。</p>
    </td> 
  </tr>
  <tr>
  <td></td> 
   <td> 
    <p>如需執行工作流程的逐步指示，請參 <a href="#xsddatasource">閱使用XSD架構作為資料來源。</a></p>
    </td> 
  </tr>
 </tbody> 
</table>


如需Automated Forms Conversion服務的詳細資訊，請參閱下列文章：

* [自動表單轉換服務簡介](introduction.md)
* [設定自動表單轉換服務](configure-service.md)
* [將列印表單轉換為最適化表單](convert-existing-forms-to-adaptive-forms.md)
* [檢閱並修正轉換後的表格](review-correct-ui-edited.md)

本文提供的資訊基於以下假設：任何閱讀該資訊的人都具有適應性表單概念的基本知識。

## 先決條件 {#pre-requisites}

* 設定 [AEM作者例項](https://helpx.adobe.com/experience-manager/6-5/sites/deploying/using/deploy.html)
* 在AEM [作者例項上設定Automated Forms Conversion服務](configure-service.md)

## 範例自適應表單 {#sample-adaptive-form}

若要執行使用案例，以最適化表單預填欄位值並將其送出至資料來源，請下載下列範例PDF檔案。

貸款申請表範例

[取得檔案](assets/sample_loan_application_form.pdf)

PDF檔案是Automated Forms Conversion服務的輸入。 服務將此檔案轉換為自適應格式。 下圖以PDF格式描述貸款申請範例。

![貸款申請表](assets/sample_form_new.png)

## 為表單模型準備資料 {#prepare-data-for-form-model}

AEM Forms Data Integration可讓您設定並連線至不同的資料來源。 使用轉換程式產生最適化表單後，您可以根據表單資料模型、XSD或JSON結構描述來定義表單模型。 您可以使用資料庫、Microsoft Dynamics或任何其他協力廠商服務來建立表單資料模型。

本教程使用MySQL資料庫作為源來建立表單資料模型。 在資料 **庫中建立** loanapplication模式，並根據自適應表單中可用的欄位向模式添加 **applicant** 表。

![示例資料mysql](assets/sample_data_mysql.png)

可以使用以下DDL語句在資料庫中創 **建** applicant表。

```sql
CREATE TABLE `applicant` (
   `name` varchar(45) DEFAULT NULL,
   `address` varchar(45) DEFAULT NULL,
   `phonenumber` int(11) NOT NULL,
   `email` varchar(45) DEFAULT NULL,
   `occupation` varchar(45) DEFAULT NULL,
   `annualsalary` varchar(45) DEFAULT NULL,
   `familymembers` int(11) DEFAULT NULL,
   PRIMARY KEY (`phonenumber`)
 ) ENGINE=InnoDB DEFAULT CHARSET=utf8
```

如果您使用XSD架構作為表單模型來執行使用案例，請使用下列文字建立XSD檔案：

```xml
<?xml version="1.0" encoding="utf-8" ?>
    <xs:schema targetNamespace="http://adobe.com/sample.xsd"
                    xmlns="http://adobe.com/sample.xsd"
                    xmlns:xs="http://www.w3.org/2001/XMLSchema">

<xs:element name="sample" type="SampleType"/>

  <xs:complexType name="SampleType">
    <xs:sequence>
      <xs:element name="name" type="xs:string"/>
   <xs:element name="address" type="xs:string"/>
   <xs:element name="phonenumber" type="xs:int"/>
   <xs:element name="email" type="xs:string"/>
   <xs:element name="occupation" type="xs:string"/>
   <xs:element name="annualsalary" type="xs:string"/>
   <xs:element name="familymembers" type="xs:string"/>
 </xs:sequence>
  </xs:complexType>

  </xs:schema>
```

或者，將XSD架構下載至本機檔案系統。

貸款申請XSD方案示例

[取得檔案](assets/loanapplication.xsd)

有關在最適化表單中使用XSD架構作為表單模型的詳細資訊，請參 [閱使用XML架構建立最適化表單](https://helpx.adobe.com/experience-manager/6-5/forms/using/adaptive-form-xml-schema-form-model.html)。

如果您使用JSON結構描述作為表單模型來執行使用案例，請建立包含下列文字的JSON檔案：

```JSON
{
    "$schema": "http://json-schema.org/draft-04/schema#",
    "definitions": {
        "loanapplication": {
            "type": "object",
            "properties": {
                "name": {
                    "type": "string"
                },
                "address": {
                    "type": "string"
                },
    "phonenumber": {
                    "type": "number"
                },
    "email": {
                    "type": "string"
                },
    "occupation": {
                    "type": "string"
                },
    "annualsalary": {
                    "type": "string"
                },
    "familymembers": {
                    "type": "number"
                }
            }
        }
 },
 "type": "object",
    "properties": {
        "employee": {
            "$ref": "#/definitions/loanapplication"
        }
    }
}
```

或者，將JSON結構描述下載至本機檔案系統。

貸款申請JSON結構描述範例

[取得檔案](assets/demo_schema.json)

如需在最適化表單中使用JSON結構描述作為表單模型的詳細資訊，請參 [閱使用JSON結構描述建立最適化表單](https://helpx.adobe.com/experience-manager/6-5/forms/using/adaptive-form-json-schema-form-model.html)。

## 產生無資料系結的最適化表單 {#generate-adaptive-forms-with-no-data-binding}

使用「 [自動化表單轉換」服務](convert-existing-forms-to-adaptive-forms.md) ，將 [](#sample-adaptive-form) 範例貸款申請表單轉換為不含資料系結的最適化表單。 請確定您選取核取方 **[!UICONTROL Generate adaptive form(s) without data bindings]** 塊，以產生沒有資料系結的最適化表單。

![無資料綁定的自適應表單](assets/generate_af_without_binding.png)

在生成沒有資料綁定的自適應表單後，為自適應表單選擇資料源：

* [資料庫、OData或任何第三方服務](#sqldatasource)
* [JSON結構描述](#jsondatasource)
* [XSD架構](#xsddatasource)

>[!NOTE]
> 如果您使用「自動表單轉換」服務轉換的最適化表單包含多個名稱相同的欄位，請確定這些欄位會系結至資料來源實體，以避免在提交時可能遺失資料。


### 使用資料庫、OData或任何第三方服務做為資料來源 {#sqldatasource}

使用案例：使用Automated Forms Conversion服務生成沒有資料綁定的自適應表單，並將MYSQL資料庫配置為資料源。 您可以手動綁定最適化表單欄位以建立資料模型實體，並使用選 **[!UICONTROL Form Data Model Prefill Service]** 項來預填欄位值。 您可使用選 **[!UICONTROL Submit using Form Data Model]** 項提交最適化表單。

執行使用案例前：

* [將MySQL資料庫配置為資料源](https://helpx.adobe.com/experience-manager/6-5/forms/using/configure-data-sources.html#configurerelationaldatabase)
* [建立表單資料模型](https://helpx.adobe.com/experience-manager/6-5/forms/using/work-with-form-data-model.html)

根據使用案例，建立 **loanapplication** form data model，並將讀取服務引數系結至 **[!UICONTROL Literal]** 值。 電話號碼常值必須是在MySQL資料庫的申請人模式中 **配置的** 其中一條記錄。 服務使用值作為參數，從資料源中獲取詳細資訊。 您也可以從下 [拉式清單中選取「使用者描述檔屬性」或](https://helpx.adobe.com/experience-manager/6-5/forms/using/work-with-form-data-model.html#bindargument)**[!UICONTROL Binding To]** 「請求屬性」

![設定表單資料模型](assets/configure_model_object.png)

>[!NOTE]
>
>在執行使用案 **例之前** ，請確定您將get **and insert** services新增至表單資料模型、設定並測試服務。

執行下列步驟：

1. 在資料夾中選 **取已轉換的貸款申請表** ，然後 **[!UICONTROL output]** 點選一下 **[!UICONTROL Properties]**。
1. 點選標 **[!UICONTROL Form Model]** 簽、從下拉 **[!UICONTROL Form Data Model]** 式清單 **[!UICONTROL Select From]** 中選取，並點選以選 **[!UICONTROL Select Form Data Model]** 取loanapplication表 **** 單資料模型。 點選 **[!UICONTROL Save & Close]** 以儲存表格。
1. 選取貸款 **申請表範例** ，並點選 **[!UICONTROL Edit]**。
1. 在標籤 **[!UICONTROL Content]** 中，點選設定圖示：

   ![設定表單容器](assets/configure_form_container.png)

   1. 在區段 **[!UICONTROL Basic]** 中，從下 **[!UICONTROL Form Data Model Prefill service]** 拉式清 **[!UICONTROL Prefill Service]** 單中選取。

   1. 在區段 **[!UICONTROL Submission]** 中，從下 **[!UICONTROL Submit using Form Data Model]** 拉式清 **[!UICONTROL Submit Action]** 單中選取。

   1. 使用欄位選擇資料 **[!UICONTROL Data Model to submit]** 模型。
   1. 點選 ![完成圖示](assets/save_icon.svg) ，以儲存屬性。

1. 點選「申請人名稱」文字方塊，並選取「 ![設定」圖示](assets/configure_icon.svg) （「設定」）。

   1. 在「系結參考」欄位中，選 **取「申請人** >名稱 **」，然後點選**&#x200B;完成圖示 ![](assets/save_icon.svg) ，以儲存屬性。 同樣地，請為地址 **、**&#x200B;電話號碼 **、**&#x200B;電子郵件、 **Adpriation Salary(美************元)、Allige Laray(Addression Joun)和No建立資料系結。 表單資料模型圖元的** 「從屬族成員」(Dependent Family Members)欄位的值。
   ![系結參照](assets/bind_references.png)

1. 點選 **[!UICONTROL Preview]** 以檢視預先填入的最適化表單欄位值。
1. 視需要修改欄位值，並提交最適化表單。 欄位值將提交到MySQL資料庫。 您可以刷新數 **據庫中** 的申請人表，以查看表中的更新值。

**使用案例：** 使用Automated Forms Conversion服務生成沒有資料綁定的自適應表單，並將MYSQL資料庫配置為資料源。 您可使用規則編輯器來系結最適化表單欄位，以預先填入欄位值。 如有必要，請修改欄位值，並將資料送出至crx-repository。

執行下列步驟，以使 [用規則編輯器](https://helpx.adobe.com/experience-manager/6-5/forms/using/rule-editor.html) ，叫用表單資料模型服務，以在最適化表單中系結欄位和預先填寫值：

1. 在資料夾 **中選取貸款申請表** ，然後 **[!UICONTROL output]** 點選一下 **[!UICONTROL Edit]**。
1. 在標籤 **[!UICONTROL Content]** 中，點選設定圖示：

   ![設定表單容器](assets/configure_form_container.png)

   在區段 **[!UICONTROL Basic]** 中，從下 **[!UICONTROL Form Data Model Prefill service]** 拉式清 **[!UICONTROL Prefill Service]** 單中選取。

1. 點選文 **[!UICONTROL Applicant Name]** 字方塊並點選 **[!UICONTROL Edit Rules]**。

   ![編輯規則以建立資料系結](assets/edit_rules_bind_reference.png)

1. 在「規 **[!UICONTROL Create]** 則編輯器」頁面上點選。
1. 在頁 **[!UICONTROL Rule Editor]** 面上：

   1. 選擇「申請人名稱」文本框的狀態。 例如，在 **[!UICONTROL is initialized]**&#x200B;模式下渲染表單時，會 **[!UICONTROL Then]** 導致執行條件的 **[!UICONTROL Preview]** 結果。

   1. 在區段 **[!UICONTROL Then]** 中，從下 **[!UICONTROL Invoke Service]** 拉式清 **[!UICONTROL Select Action]** 單中選取。 您的Forms例項上的所有服務都會顯示在下拉式清單中。

   1. 從列出 **[!UICONTROL Get]** 表單資料模型的部分中選擇服務。 「輸入」欄位顯 **示電話號碼**，該電話號碼是為申請人資料模型定 **義的主鍵** 。 系統會根據此欄位，擷取並預填「輸出」區段中各欄位的最適化表單值。

   1. 使用「輸出」(Output)部分為具有表單資料模型圖元的自適應表單域建立綁定。 例如，將最適 **[!UICONTROL Applicant Name]** 化表單欄位與名稱 **實體系結** 。

   1. 點選 **[!UICONTROL Done]**。 在「規 **[!UICONTROL Done]** 則編輯器」頁面上再次點選。
   ![用於綁定引用的規則編輯器](assets/rule_editor_bind_references.png)

1. 點選 **[!UICONTROL Preview]** 以檢視預先填入的最適化表單欄位值。

   >[!NOTE]
   >
   >確保在與自 **[!UICONTROL Return Array]** 適應表單關聯的表單資料模型中， **get** service屬性的Property設定為OFF。

1. 視需要修改欄位值，並提交最適化表單。 提交的資料位於crx-repository中的以下位置：

   `http://host name:port/crx/de/index.jsp#/content/forms/fp/admin/submit/data/latest file available in the folder`

### 使用JSON結構描述做為資料來源 {#jsondatasource}

**使用案例：** 您可使用「自動表單轉換」服務產生沒有資料系結的最適化表單，並將JSON結構描述設定為資料來源。 您可以手動將最適化表單欄位系結至JSON結構描述，並使用「 **預覽及資料** 」選項來預先填入欄位值。 如有必要，請修改欄位值，並將資料送出至crx-repository。

在執行使用案例之前，請確定您有：

* [與JSON結構相容的有效JSON結構](#prepare-data-for-form-model)
* [無資料綁定的自適應表單](#generate-adaptive-forms-with-no-data-binding)

執行下列步驟：

1. 選擇輸出資 **料夾中可用的已轉換貸** 款申請表 **,** 然後點選 **[!UICONTROL Properties]**。
1. 點選標 **[!UICONTROL Form Model]** 簽、從下拉 **[!UICONTROL Schema]** 式清單中 **[!UICONTROL Select From]** 選取，然後點選以上傳儲存在本機檔案系統上的 **[!UICONTROL Select Schema]** demo.schema JSON **** 結構描述。 點選 **[!UICONTROL Save & Close]** 以儲存表格。
1. 選取貸款 **申請表範例** ，並點選 **[!UICONTROL Edit]**。
1. 點選「申請人名稱」文字方塊，並選取「 ![設定」圖示](assets/configure_icon.svg) （「設定」）。

   在「系結參考」欄位中，選 **取「申請人** >名稱 **」，然後點選**&#x200B;完成圖示 ![](assets/save_icon.svg) ，以儲存屬性。 同樣地，請為地址 **、**&#x200B;電話號碼 **、**&#x200B;電子郵件、 **Adpriation Salary(美************元)、Allige Laray(Addression Joun)和No建立資料系結。 具有JSON結構描述實體** 的相依族成員欄位。

1. 再次選擇 **資料夾中可用的已轉換貸款申請表** 單，然後選擇 **[!UICONTROL output]** > **[!UICONTROL Preview]****[!UICONTROL Preview with Data]**。</br>

   下載範例資料檔案</br>

   [取得檔案](assets/json_data_file.txt)</br>

1. 視需要修改欄位值，並提交最適化表單。 提交的資料位於crx-repository中的以下位置：

   `http://host name:port/crx/de/index.jsp#/content/forms/fp/admin/submit/data/latest file available in the folder`

### 使用XSD架構作為資料來源 {#xsddatasource}

**使用案例：** 您可使用「自動表單轉換」服務產生沒有資料系結的最適化表單，並將XSD架構設為資料來源。 您可以手動將最適化表單欄位系結至XSD架構，並使用「預覽 **與資料** 」來預先填入欄位值。 如有必要，請修改欄位值，並將資料送出至crx-repository。

在執行使用案例之前，請確定您有：

* [與XML架構結構相容的有效XSD架構](#prepare-data-for-form-model)
* [無資料綁定的自適應表單](#generate-adaptive-forms-with-no-data-binding)

執行下列步驟：

1. 在資料夾中選 **取已轉換的貸款申請表** ，然後 **[!UICONTROL output]** 點選一下 **[!UICONTROL Properties]**。
1. 點選標 **[!UICONTROL Form Model]** 簽、從下拉 **[!UICONTROL Schema]** 式清單中 **[!UICONTROL Select From]** 選取，並點選以上傳儲存在本機檔案系統上的 **[!UICONTROL Select Schema]** loanapplication **** XSD架構。 選擇XSD架構的根元素，並點選 **[!UICONTROL Save & Close]** 以儲存表單。
1. 選取貸款 **申請表範例** ，並點選 **[!UICONTROL Edit]**。
1. 點選「申請人名稱」文字方塊，並選取「 ![設定」圖示](assets/configure_icon.svg) （「設定」）。
在「系結參考」欄位中，選 **取「申請人** >名稱 **」，然後點選「**&#x200B;完成圖示 ![](assets/save_icon.svg) 」以儲存屬性。 同樣地，請為地址 **、**&#x200B;電話號碼 **、**&#x200B;電子郵件、 **Adpriation Salary(美************元)、Allige Laray(Addression Joun)和No建立資料系結。 包含XSD架構實體的相依族成員** (Dependent Family Members)欄位。

1. 再次選擇輸出 **資料夾中可用的已轉換貸** 款申請表 **，然後選擇** > **[!UICONTROL Preview]****[!UICONTROL Preview with Data]**。</br>

   下載範例資料檔案</br>

   [取得檔案](assets/loan-application-data-xml-data.zip)</br>


1. 視需要修改欄位值，並提交最適化表單。 提交的資料位於crx-repository中的以下位置：

   `http://host name:port/crx/de/index.jsp#/content/forms/fp/admin/submit/data/latest file available in the folder`

## 使用JSON系結產生最適化表單 {#generate-adaptive-forms-with-json-binding}

使用「 [自動表單轉換」服務](convert-existing-forms-to-adaptive-forms.md) ，將 [](#sample-adaptive-form) 範例貸款申請表單轉換為具有資料系結的最適化表單。 在生成最適化表單時，請確 **[!UICONTROL Generate adaptive form(s) without data bindings]** 保不要選中該複選框。

![具JSON系結的最適化表單](assets/generate_af_with_data_bindings.png)

### 使用JSON結構描述做為資料來源 {#jsonwithdatabinding}

**使用案例：** 您可使用「自動表單轉換」服務，產生具有JSON資料系結的最適化表單。 預填服務和表單提交功能十分順暢。 您不需要任何設定步驟。

在執行使用案例之前，請確定您有具 [備資料系結的最適化表單](#generate-adaptive-forms-with-json-binding)。

執行下列步驟：

1. 再次選擇 **資料夾中可用的已轉換貸款申請表** 單，然後選擇 **[!UICONTROL output]** > **[!UICONTROL Preview]****[!UICONTROL Preview with Data]**。</br>

   下載範例資料檔案</br>

   [取得檔案](assets/loan_application_data_source_json_data_binding.txt)</br>

1. 視需要修改欄位值，並提交最適化表單。 提交的資料位於crx-repository中的以下位置：

   `http://host name:port/crx/de/index.jsp#/content/forms/fp/admin/submit/data/latest file available in the folder`

## 將提交的最適化表單JSON資料轉換為XML格式 {#convert-submitted-adaptive-form-data-to-xml}

當您在最適化表單欄位中輸入值並送出時，crx-repository中的資料會以JSON格式提供。 您可以使用 [org.apache.sling.commons.json.xml](https://sling.apache.org/apidocs/sling5/org/apache/sling/commons/json/xml/XML.html#toString) API或下列范常式式碼，將JSON資料格式轉換為XML:

```
import org.apache.sling.commons.json.JSONException;
import org.apache.sling.commons.json.JSONObject;
import org.apache.sling.commons.json.xml.XML;
 
public class ConversionUtils {
 
    public static String jsonToXML(String jsonString) throws JSONException {
        //https://sling.apache.org/apidocs/sling5/org/apache/sling/commons/json/xml/XML.html#toString(java.lang.Object)
        //jar - http://maven.ibiblio.org/maven2/org/apache/sling/org.apache.sling.commons.json/2.0.18/
        //Note: Need to extract boundData part before converting to XML
        return XML.toString(new JSONObject(jsonString));
    }
}
```
