---
title: 基於資料來源的建議預填及提交最適化表單的工作流程
seo-title: Prefill and submit options for adaptive forms
description: 基於資料源的預填和提交工作流，用於使用Automated forms conversion服務生成的自適應表單。
seo-description: Data-source based prefill and submit workflows for adaptive forms generated using Automated Forms Conversion Service.
uuid: 91409a82-141c-4233-82b1-1539a0b250f8
contentOwner: khsingh
topic-tags: forms
discoiquuid: cad34fff-7f9f-4a27-8b5c-d0a523903eec
privatebeta: true
exl-id: 5deef8f5-5098-47c1-b696-b2db59e92931
source-git-commit: 1a3f79925f25dcc7dbe007f6e634f6e3a742bf72
workflow-type: tm+mt
source-wordcount: '2437'
ht-degree: 2%

---

# 基於資料來源的建議預填及提交最適化表單的工作流程 {#recommended-data-source-btased-prefill-and-submit-workflows-for-adaptive-forms}

您可以使用以下任意資料源，並使用Automated forms conversion服務轉換自適應表單：

* 表單資料模型、OData或任何其他第三方服務
* JSON架構
* XSD架構

根據資料源，可以選擇生成帶有或不帶資料模型的自適應表單。

本文介紹在選擇資料源並使用轉換服務生成自適應表單後，預填充欄位值和提交選項的建議工作流。

<table> 
 <tbody> 
  <tr> 
   <th><strong>資料來源</strong></th> 
   <th><strong>建議的工作流</strong></th> 
  </tr> 
  <tr> 
   <td><p>表單資料模型、OData或任何其他第三方服務</p></td> 
   <td> 
    <p><strong>選項1</strong>:您選擇表單資料模型、OData或任何其他第三方服務作為資料源。 你 <a href="#generate-adaptive-forms-with-no-data-binding">生成無資料綁定的自適應窗體</a> 使用Automated forms conversion服務。 您可以手動綁定自適應表單域以形成資料模型實體，並使用「表單資料模型預填充服務」選項預填充欄位值。 使用「使用表單資料模型提交」選項提交自適應表單。</p></td> 
  </tr>
  <tr> 
   <td></td> 
   <td> 
   <p><strong>選項2</strong>:您選擇表單資料模型、OData或任何其他第三方服務作為資料源。 你 <a href="#generate-adaptive-forms-with-no-data-binding">生成無資料綁定的自適應窗體</a> 使用Automated forms conversion服務。 可以使用規則編輯器綁定自適應表單域以預填充欄位值。 如有必要，修改欄位值，並將資料提交到crx-repository。</p>
    </td> 
  </tr>
  <tr> 
   <td></td> 
   <td> 
    <p>有關執行這些工作流的逐步說明，請參見 <a href="#sqldatasource">使用資料庫、OData或任何第三方服務作為資料源。</a></p> </td> 
  </tr>
  <tr>
  <td><p>JSON架構</p></td> 
   <td> 
    <p>選擇JSON架構作為資料源。 基於所選資料源：</p></td> 
  </tr>
  <tr>
  <td></td> 
   <td> 
    <p><strong>選項1</strong>:你 <a href="#generate-adaptive-forms-with-no-data-binding">生成無資料綁定的自適應窗體</a> 使用Automated forms conversion服務並將JSON架構配置為資料源。 您可以手動將自適應表單域綁定到JSON架構 <a href="https://helpx.adobe.com/experience-manager/6-5/forms/using/prepopulate-adaptive-form-fields.html#Supportedprotocolsforprefillinguserdata" target="_blank">使用任何受支援的協定</a> 的子菜單。 如有必要，修改欄位值，並將資料提交到crx-repository。</p></td> 
  </tr>
  <tr>
  <td></td> 
   <td> 
    <p>有關執行工作流的逐步說明，請參見 <a href="#jsondatasource">將JSON架構用作資料源。</p></td> 
  </tr>
  <tr>
  <td></td> 
   <td> 
    <p><strong>選項2</strong>:你 <a href="#generate-adaptive-forms-with-json-binding">生成具有JSON資料綁定的自適應表單</a> 使用Automated forms conversion服務。 預填服務和表單提交功能無縫。 您不需要任何配置步驟。</p> </td> 
  </tr>
   <tr>
  <td></td> 
   <td> 
    <p>有關執行工作流的逐步說明，請參見 <a href="#jsonwithdatabinding">將JSON架構用作資料源。</a></p> </td> 
  </tr>
  <tr>
  <td><p>XSD架構</p></td> 
   <td> 
    <p>選擇XSD架構作為資料源。 根據所選資料源， <a href="#generate-adaptive-forms-with-no-data-binding">生成無資料綁定的自適應窗體</a> 使用Automated forms conversion服務並將XSD架構配置為資料源。 您可以手動將自適應表單域綁定到XSD架構 <a href="https://helpx.adobe.com/experience-manager/6-5/forms/using/prepopulate-adaptive-form-fields.html#Supportedprotocolsforprefillinguserdata" target="_blank">使用任何受支援的協定</a> 的子菜單。 如有必要，修改欄位值，並將資料提交到crx-repository。</p>
    </td> 
  </tr>
  <tr>
  <td></td> 
   <td> 
    <p>有關執行工作流的逐步說明，請參見 <a href="#xsddatasource">使用XSD架構作為資料源。</a></p>
    </td> 
  </tr>
 </tbody> 
</table>


有關Automated forms conversion服務的詳細資訊，請參閱以下文章：

* [自動表單轉換服務簡介](introduction.md)
* [設定自動表單轉換服務](configure-service.md)
* [將列印表單轉換為最適化表單](convert-existing-forms-to-adaptive-forms.md)
* [檢閱並修正轉換後的表單](review-correct-ui-edited.md)

本文提供的資訊是基於一個假設，即任何閱讀該資訊的人都具有自適應形式概念的基本知識。

## 先決條件 {#pre-requisites}

* 配置 [AEM作者實例](https://helpx.adobe.com/tw/experience-manager/6-5/sites/deploying/using/deploy.html)
* 配置 [automated forms conversion文AEM件](configure-service.md)

## 示例自適應窗體 {#sample-adaptive-form}

要執行使用案例以在自適應表單中預填充欄位值並將其提交到資料源，請下載以下示例PDF檔案。

貸款申請表示例

[取得檔案](assets/sample_loan_application_form.pdf)

PDF檔案用作Automated forms conversion服務的輸入。 服務將此檔案轉換為自適應格式。 下圖以PDF格式描述了示例貸款應用程式。

![示例貸款申請表](assets/sample_form_new.png)

## 為表單模型準備資料 {#prepare-data-for-form-model}

AEM Forms資料整合允許您配置和連接到不同的資料源。 使用轉換過程生成自適應表單後，可以基於表單資料模型、XSD或JSON架構定義表單模型。 可以使用資料庫、Microsoft動態或任何其他第三方服務來建立表單資料模型。

本教程使用MySQL資料庫作為源建立表單資料模型。 建立 **Loan Application（貸款應用）** 在資料庫中模式並添加 **申請人** 表到基於自適應表單中可用欄位的模式。

![示例資料mysql](assets/sample_data_mysql.png)

可以使用以下DDL語句建立 **申請人** 表格。

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

如果您使用XSD架構作為表單模型來執行使用案例，請使用以下文本建立XSD檔案：

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

或將XSD架構下載到本地檔案系統。

示例貸款應用程式XSD架構

[取得檔案](assets/loanapplication.xsd)

有關在自適應表單中將XSD架構用作表單模型的詳細資訊，請參見 [使用XML架構建立自適應表單](https://helpx.adobe.com/experience-manager/6-5/forms/using/adaptive-form-xml-schema-form-model.html)。

如果使用JSON架構作為表單模型來執行使用案例，請使用以下文本建立JSON檔案：

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

或將JSON架構下載到本地檔案系統。

示例貸款應用程式JSON架構

[取得檔案](assets/demo_schema.json)

有關將JSON架構用作自適應表單中的表單模型的詳細資訊，請參見 [使用JSON架構建立自適應表單](https://helpx.adobe.com/experience-manager/6-5/forms/using/adaptive-form-json-schema-form-model.html)。

## 生成沒有資料綁定的自適應表單 {#generate-adaptive-forms-with-no-data-binding}

使用 [automated forms conversion服務要轉換](convert-existing-forms-to-adaptive-forms.md) 這樣 [示例貸款申請表](#sample-adaptive-form) 到無資料綁定的自適應窗體。 確保選擇 **[!UICONTROL Generate adaptive form(s) without data bindings]** 複選框，以生成無資料綁定的自適應窗體。

![無資料綁定的自適應窗體](assets/generate_af_without_binding.png)

在生成沒有資料綁定的自適應表單後，為自適應表單選擇資料源：

* [資料庫、OData或任何第三方服務](#sqldatasource)
* [JSON架構](#jsondatasource)
* [XSD架構](#xsddatasource)

>[!NOTE]
> 如果使用Automated forms conversion服務轉換的自適應表單包含多個具有相同名稱的欄位，請確保這些欄位綁定到資料源實體以避免在提交過程中可能丟失資料。

### 將資料庫、OData或任何第三方服務用作資料源 {#sqldatasource}

用例：使用Automated forms conversion服務生成沒有資料綁定的自適應表單，並將MYSQL資料庫配置為資料源。 可以手動綁定自適應表單域以形成資料模型實體，並使用 **[!UICONTROL Form Data Model Prefill Service]** 的子菜單。 使用 **[!UICONTROL Submit using Form Data Model]** 的子菜單。

在執行使用案例之前：

* [將MySQL資料庫配置為資料源](https://helpx.adobe.com/experience-manager/6-5/forms/using/configure-data-sources.html#configurerelationaldatabase)
* [建立表單資料模型](https://helpx.adobe.com/experience-manager/6-5/forms/using/work-with-form-data-model.html)

根據使用案例，建立 **Loan Application（貸款應用）** 表單資料模型和將讀取服務參數綁定到 **[!UICONTROL Literal]** 值。 電話號碼文字值必須是在 **申請人** MySQL資料庫的架構。 服務將值用作從資料源獲取詳細資訊的參數。 也可以選擇 [用戶配置檔案屬性或請求屬性](https://helpx.adobe.com/experience-manager/6-5/forms/using/work-with-form-data-model.html#bindargument) 從 **[!UICONTROL Binding To]** 下拉清單

![配置表單資料模型](assets/configure_model_object.png)

>[!NOTE]
>
>確保添加 **得** 和 **插入** 服務到表單資料模型、配置和test服務，然後再執行使用案例。

執行以下步驟：

1. 選擇已轉換 **示例貸款申請表** 的 **[!UICONTROL output]** 資料夾和點擊 **[!UICONTROL Properties]**。
1. 點擊 **[!UICONTROL Form Model]** 頁籤 **[!UICONTROL Form Data Model]** 從 **[!UICONTROL Select From]** 下拉清單，然後點擊 **[!UICONTROL Select Form Data Model]** 的 **Loan Application（貸款應用）** 表單資料模型。 點擊 **[!UICONTROL Save & Close]** 的子菜單。
1. 選擇 **示例貸款申請表** 點擊 **[!UICONTROL Edit]**。
1. 在 **[!UICONTROL Content]** 頁籤，按一下「configure」表徵圖：

   ![配置表單容器](assets/configure_form_container.png)

   1. 在 **[!UICONTROL Basic]** 選擇 **[!UICONTROL Form Data Model Prefill service]** 從 **[!UICONTROL Prefill Service]** 的子菜單。

   1. 在 **[!UICONTROL Submission]** 選擇 **[!UICONTROL Submit using Form Data Model]** 從 **[!UICONTROL Submit Action]** 的子菜單。

   1. 使用 **[!UICONTROL Data Model to submit]** 的子菜單。
   1. 點擊 ![完成表徵圖](assets/save_icon.svg) 的子菜單。

1. 按一下「申請人姓名」文本框並選擇 ![配置表徵圖](assets/configure_icon.svg) （配置）。

   1. 在「綁定引用」欄位中，選擇 **申請人** > **名稱**，然後點擊 ![完成表徵圖](assets/save_icon.svg) 的子菜單。 同樣，為 **地址**。 **電話號碼**。 **電子郵件**。 **職業**。 **年薪（美元）**, **不。 家庭成員** 欄位。

   ![綁定引用](assets/bind_references.png)

1. 點擊 **[!UICONTROL Preview]** 的子菜單。
1. 如有必要，修改欄位值，並提交自適應表單。 欄位值將提交到MySQL資料庫。 您可以刷新 **申請人** 的子菜單。

**用例：** 使用Automated forms conversion服務生成沒有資料綁定的自適應表單，並將MYSQL資料庫配置為資料源。 可以使用規則編輯器綁定自適應表單域以預填充欄位值。 如有必要，修改欄位值，並將資料提交到crx-repository。

執行以下步驟以使用 [規則編輯器](https://helpx.adobe.com/experience-manager/6-5/forms/using/rule-editor.html) 要調用表單資料模型服務以在自適應表單中綁定欄位和預填充值：

1. 選擇 **示例貸款申請表** 的 **[!UICONTROL output]** 資料夾和點擊 **[!UICONTROL Edit]**。
1. 在 **[!UICONTROL Content]** 頁籤，按一下「configure」表徵圖：

   ![配置表單容器](assets/configure_form_container.png)

   在 **[!UICONTROL Basic]** 選擇 **[!UICONTROL Form Data Model Prefill service]** 從 **[!UICONTROL Prefill Service]** 的子菜單。

1. 點擊 **[!UICONTROL Applicant Name]** 文本框和點擊 **[!UICONTROL Edit Rules]**。

   ![編輯規則以建立資料綁定](assets/edit_rules_bind_reference.png)

1. 點擊 **[!UICONTROL Create]** 的子菜單。
1. 在 **[!UICONTROL Rule Editor]** 頁：

   1. 為「申請人名稱」文本框選擇狀態。 比如說， **[!UICONTROL is initialized]**，導致執行 **[!UICONTROL Then]** 條件 **[!UICONTROL Preview]** 的子菜單。

   1. 在 **[!UICONTROL Then]** 選擇 **[!UICONTROL Invoke Service]** 從 **[!UICONTROL Select Action]** 的子菜單。 您的Forms實例上的所有服務都顯示在下拉清單中。

   1. 選擇 **[!UICONTROL Get]** 表格資料模型部分中的服務。 將顯示「輸入」欄位 **電話號碼**，是為 **申請人** 資料模型。 系統將基於此欄位檢索並預填充「輸出」節中欄位的自適應格式值。

   1. 使用「輸出」部分為具有表單資料模型圖元的自適應表單域建立綁定。 例如，綁定 **[!UICONTROL Applicant Name]** 具有 **名稱** 的雙曲餘切值。

   1. 點選 **[!UICONTROL Done]**。點擊 **[!UICONTROL Done]** 的上界。

   ![用於綁定引用的規則編輯器](assets/rule_editor_bind_references.png)

1. 點擊 **[!UICONTROL Preview]** 的子菜單。

   >[!NOTE]
   >
   >確保 **[!UICONTROL Return Array]** 屬性設定為OFF **得** 與自適應表單關聯的表單資料模型中的服務屬性。

1. 如有必要，修改欄位值，並提交自適應表單。 已提交的資料位於crx-repository中的以下位置：

   `http://host name:port/crx/de/index.jsp#/content/forms/fp/admin/submit/data/latest file available in the folder`

### 將JSON架構用作資料源 {#jsondatasource}

**用例：** 使用Automated forms conversion服務生成沒有資料綁定的自適應表單，並將JSON架構配置為資料源。 您可以手動將自適應表單域綁定到JSON架構，並使用 **使用資料預覽** 的子菜單。 如有必要，修改欄位值，並將資料提交到crx-repository。

在執行使用案例之前，請確保：

* [與JSON架構結構相容的有效JSON架構](#prepare-data-for-form-model)
* [無資料綁定的自適應窗體](#generate-adaptive-forms-with-no-data-binding)

執行以下步驟：

1. 選擇已轉換 **示例貸款申請表** 的 **輸出** 資料夾和點擊 **[!UICONTROL Properties]**。
1. 點擊 **[!UICONTROL Form Model]** 頁籤 **[!UICONTROL Schema]** 從 **[!UICONTROL Select From]** 下拉清單，然後點擊 **[!UICONTROL Select Schema]** 上載 **demo.schema JSON** 模式已保存在本地檔案系統上。 點擊 **[!UICONTROL Save & Close]** 的子菜單。
1. 選擇 **示例貸款申請表** 點擊 **[!UICONTROL Edit]**。
1. 按一下「申請人姓名」文本框並選擇 ![配置表徵圖](assets/configure_icon.svg) （配置）。

   在「綁定引用」欄位中，選擇 **申請人** > **名稱**，然後點擊 ![完成表徵圖](assets/save_icon.svg) 的子菜單。 同樣，為 **地址**。 **電話號碼**。 **電子郵件**。 **職業**。 **年薪（美元）**, **不。 家庭成員** 具有JSON架構實體的欄位。

1. 選擇已轉換 **示例貸款申請表** 的 **[!UICONTROL output]** 再次選擇資料夾 **[!UICONTROL Preview]** > **[!UICONTROL Preview with Data]**。</br>

   下載示例資料檔案</br>

   [取得檔案](assets/json_data_file.txt)</br>

1. 如有必要，修改欄位值，並提交自適應表單。 已提交的資料位於crx-repository中的以下位置：

   `http://host name:port/crx/de/index.jsp#/content/forms/fp/admin/submit/data/latest file available in the folder`

### 將XSD架構用作資料源 {#xsddatasource}

**用例：** 使用Automated forms conversion服務生成沒有資料綁定的自適應表單，並將XSD架構配置為資料源。 您可以手動將自適應表單域綁定到XSD架構，並使用 **使用資料預覽** 的子菜單。 如有必要，修改欄位值，並將資料提交到crx-repository。

在執行使用案例之前，請確保：

* [符合XML架構結構的有效XSD架構](#prepare-data-for-form-model)
* [無資料綁定的自適應窗體](#generate-adaptive-forms-with-no-data-binding)

執行以下步驟：

1. 選擇已轉換 **示例貸款申請表** 的 **[!UICONTROL output]** 資料夾和點擊 **[!UICONTROL Properties]**。
1. 點擊 **[!UICONTROL Form Model]** 頁籤 **[!UICONTROL Schema]** 從 **[!UICONTROL Select From]** 下拉清單，然後點擊 **[!UICONTROL Select Schema]** 上載 **Loan Application（貸款應用）** XSD架構已保存在本地檔案系統上。 為XSD架構選擇根元素，然後點擊 **[!UICONTROL Save & Close]** 的子菜單。
1. 選擇 **示例貸款申請表** 點擊 **[!UICONTROL Edit]**。
1. 按一下「申請人姓名」文本框並選擇 ![配置表徵圖](assets/configure_icon.svg) （配置）。
在「綁定引用」欄位中，選擇 **申請人** > **名稱**，然後點擊 ![完成表徵圖](assets/save_icon.svg) 的子菜單。 同樣，為 **地址**。 **電話號碼**。 **電子郵件**。 **職業**。 **年薪（美元）**, **不。 家庭成員** 帶有XSD架構實體的欄位。

1. 選擇已轉換 **示例貸款申請表** 的 **輸出** 再次選擇資料夾 **[!UICONTROL Preview]** > **[!UICONTROL Preview with Data]**。</br>

   下載示例資料檔案</br>

   [取得檔案](assets/loan-application-data-xml-data.zip)</br>


1. 如有必要，修改欄位值，並提交自適應表單。 已提交的資料位於crx-repository中的以下位置：

   `http://host name:port/crx/de/index.jsp#/content/forms/fp/admin/submit/data/latest file available in the folder`

## 使用JSON綁定生成自適應表單 {#generate-adaptive-forms-with-json-binding}

使用 [automated forms conversion服務要轉換](convert-existing-forms-to-adaptive-forms.md) 這樣 [示例貸款申請表](#sample-adaptive-form) 到具有資料綁定的自適應窗體。 確保不選擇 **[!UICONTROL Generate adaptive form(s) without data bindings]** 的子菜單。

![具有JSON綁定的自適應窗體](assets/generate_af_with_data_bindings.png)

### 將JSON架構用作資料源 {#jsonwithdatabinding}

**用例：** 使用Automated forms conversion服務生成具有JSON資料綁定的自適應表單。 預填服務和表單提交功能無縫。 您不需要任何配置步驟。

在執行使用案例之前，請確保 [具有資料綁定的自適應格式](#generate-adaptive-forms-with-json-binding)。

執行以下步驟：

1. 選擇已轉換 **示例貸款申請表** 的 **[!UICONTROL output]** 再次選擇資料夾 **[!UICONTROL Preview]** > **[!UICONTROL Preview with Data]**。</br>

   下載示例資料檔案</br>

   [取得檔案](assets/loan_application_data_source_json_data_binding.txt)</br>

1. 如有必要，修改欄位值，並提交自適應表單。 已提交的資料位於crx-repository中的以下位置：

   `http://host name:port/crx/de/index.jsp#/content/forms/fp/admin/submit/data/latest file available in the folder`

## 將提交的自適應表單JSON資料轉換為XML格式 {#convert-submitted-adaptive-form-data-to-xml}

在自適應表單欄位中輸入值並提交時，在crx-repository中，資料以JSON格式可用。 可以使用 [org.apache.sling.commons.json.xml](https://sling.apache.org/apidocs/sling5/org/apache/sling/commons/json/xml/XML.html#toString) API或以下示例代碼：

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
