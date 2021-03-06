---
title: 基於資料來源的建議預填及提交最適化表單的工作流程
seo-title: 預填及提交最適化表單的選項
description: 以資料來源為基礎，預填及提交使用Automated forms conversion服務產生的最適化表單工作流程。
seo-description: 以資料來源為基礎，預填及提交使用Automated forms conversion服務產生的最適化表單工作流程。
uuid: 91409a82-141c-4233-82b1-1539a0b250f8
contentOwner: khsingh
topic-tags: forms
discoiquuid: cad34fff-7f9f-4a27-8b5c-d0a523903eec
privatebeta: true
exl-id: 5deef8f5-5098-47c1-b696-b2db59e92931
source-git-commit: 1a3f79925f25dcc7dbe007f6e634f6e3a742bf72
workflow-type: tm+mt
source-wordcount: '2459'
ht-degree: 2%

---

# 基於資料來源的建議預填及提交最適化表單的工作流程 {#recommended-data-source-btased-prefill-and-submit-workflows-for-adaptive-forms}

您可以透過使用Automated forms conversion服務轉換的最適化表單，使用下列任何資料來源：

* 表單資料模型、OData或任何其他第三方服務
* JSON結構
* XSD架構

您可以根據資料來源，選擇產生具有或不具有資料模型的最適化表單。

本文說明在選取資料來源並使用轉換服務產生最適化表單後，預填欄位值和提交選項的建議工作流程。

<table> 
 <tbody> 
  <tr> 
   <th><strong>資料來源</strong></th> 
   <th><strong>建議的工作流程</strong></th> 
  </tr> 
  <tr> 
   <td><p>表單資料模型、OData或任何其他第三方服務</p></td> 
   <td> 
    <p><strong>選項1</strong>:選擇表單資料模型、OData或任何其他第三方服務作為資料源。您<a href="#generate-adaptive-forms-with-no-data-binding">使用Automated forms conversion服務產生沒有資料綁定的適用性表單</a>。 您可以手動系結最適化表單欄位，以形成資料模型實體，並使用「表單資料模型預填服務」選項來預填欄位值。 您可以使用「使用表單資料模型提交」選項來提交最適化表單。</p></td> 
  </tr>
  <tr> 
   <td></td> 
   <td> 
   <p><strong>選項2</strong>:選擇表單資料模型、OData或任何其他第三方服務作為資料源。您<a href="#generate-adaptive-forms-with-no-data-binding">使用Automated forms conversion服務產生沒有資料綁定的適用性表單</a>。 您可以使用規則編輯器系結最適化表單欄位，以預填欄位值。 視需要修改欄位值，並將資料提交至crx-repository。</p>
    </td> 
  </tr>
  <tr> 
   <td></td> 
   <td> 
    <p>有關執行這些工作流的逐步說明，請參閱<a href="#sqldatasource">使用資料庫、OData或任何第三方服務作為資料源。</a></p> </td> 
  </tr>
  <tr>
  <td><p>JSON結構</p></td> 
   <td> 
    <p>選取JSON結構描述作為資料來源。 根據所選資料源：</p></td> 
  </tr>
  <tr>
  <td></td> 
   <td> 
    <p><strong>選項1</strong>:您 <a href="#generate-adaptive-forms-with-no-data-binding">可以使用Automated forms conversion服務產</a> 生沒有資料捆綁的適用性表單，並將JSON結構設為資料來源。您可以手動將適用性表單欄位系結至JSON結構，並使用任何支援的通訊協定</a>來預填欄位值。 <a href="https://helpx.adobe.com/experience-manager/6-5/forms/using/prepopulate-adaptive-form-fields.html#Supportedprotocolsforprefillinguserdata" target="_blank">視需要修改欄位值，並將資料提交至crx-repository。</a></p></td> 
  </tr>
  <tr>
  <td></td> 
   <td> 
    <p>如需執行工作流程的逐步指示，請參閱<a href="#jsondatasource">使用JSON結構作為資料來源。</p></td> 
  </tr>
  <tr>
  <td></td> 
   <td> 
    <p><strong>選項2</strong>:您使 <a href="#generate-adaptive-forms-with-json-binding">用Automated forms conversion服務產生具有JSON</a> 資料二進位的最適化表單。預填服務和表單提交功能無縫。 您不需要任何設定步驟。</p> </td> 
  </tr>
   <tr>
  <td></td> 
   <td> 
    <p>如需執行工作流程的逐步指示，請參閱<a href="#jsonwithdatabinding">使用JSON結構作為資料來源。</a></p> </td> 
  </tr>
  <tr>
  <td><p>XSD架構</p></td> 
   <td> 
    <p>選擇XSD架構作為資料源。 根據所選的資料源，您<a href="#generate-adaptive-forms-with-no-data-binding">使用Automated forms conversion服務生成沒有資料綁定的適用性表單</a>，並將XSD架構配置為資料源。 您可以手動將適用性表單欄位系結至XSD架構，並使用任何支援的通訊協定</a>來預填欄位值。 <a href="https://helpx.adobe.com/experience-manager/6-5/forms/using/prepopulate-adaptive-form-fields.html#Supportedprotocolsforprefillinguserdata" target="_blank">視需要修改欄位值，並將資料提交至crx-repository。</a></p>
    </td> 
  </tr>
  <tr>
  <td></td> 
   <td> 
    <p>有關執行工作流的逐步說明，請參閱<a href="#xsddatasource">使用XSD架構作為資料源。</a></p>
    </td> 
  </tr>
 </tbody> 
</table>


如需Automated forms conversion服務的詳細資訊，請參閱下列文章：

* [自動表單轉換服務簡介](introduction.md)
* [設定自動表單轉換服務](configure-service.md)
* [將列印表單轉換為最適化表單](convert-existing-forms-to-adaptive-forms.md)
* [檢閱並修正轉換後的表格](review-correct-ui-edited.md)

本文提供的資訊基於以下假設：任何閱讀該資訊的人都具備適應性表單概念的基本知識。

## 先決條件{#pre-requisites}

* 設定[AEM製作例項](https://helpx.adobe.com/tw/experience-manager/6-5/sites/deploying/using/deploy.html)
* 在AEM製作例項](configure-service.md)上設定[Automated forms conversion服務

## 適用性表單範例{#sample-adaptive-form}

若要執行使用案例以在最適化表單中預先填入欄位值，並將其提交至資料來源，請下載下列範例PDF檔案。

貸款申請表示例

[取得檔案](assets/sample_loan_application_form.pdf)

PDF檔案可作為Automated forms conversion服務的輸入。 服務會將此檔案轉換為最適化表單。 下圖以PDF格式描述貸款應用程式範例。

![貸款申請表示例](assets/sample_form_new.png)

## 準備表單模型{#prepare-data-for-form-model}的資料

AEM Forms資料整合可讓您設定並連線至不同的資料來源。 使用轉換程式產生最適化表單後，您可以根據表單資料模型、XSD或JSON結構定義表單模型。 您可以使用資料庫、Microsoft Dynamics或任何其他第三方服務來建立表單資料模型。

本教程使用MySQL資料庫作為源來建立表單資料模型。 在資料庫中建立&#x200B;**loanapplication**&#x200B;架構，並根據適用性表單中可用的欄位，將&#x200B;**applicant**&#x200B;表格新增至架構。

![示例資料mysql](assets/sample_data_mysql.png)

可以使用以下DDL語句在資料庫中建立&#x200B;**applicant**&#x200B;表。

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

如果您使用XSD架構作為執行使用案例的表單模型，請建立包含以下文本的XSD檔案：

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

或將XSD架構下載至本機檔案系統。

貸款申請XSD架構示例

[取得檔案](assets/loanapplication.xsd)

有關在適用性表單中使用XSD架構作為表單模型的詳細資訊，請參閱[使用XML架構建立適用性表單](https://helpx.adobe.com/experience-manager/6-5/forms/using/adaptive-form-xml-schema-form-model.html)。

如果您使用JSON結構描述作為執行使用案例的表單模型，請建立包含下列文字的JSON檔案：

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

或將JSON結構下載至本機檔案系統。

貸款應用程式JSON結構描述範例

[取得檔案](assets/demo_schema.json)

如需在適用性表單中使用JSON結構作為表單模型的詳細資訊，請參閱[使用JSON結構建立適用性表單](https://helpx.adobe.com/experience-manager/6-5/forms/using/adaptive-form-json-schema-form-model.html)。

## 產生沒有資料綁定的適用性表單{#generate-adaptive-forms-with-no-data-binding}

使用[Automated forms conversion服務將[貸款申請表](#sample-adaptive-form)示例轉換為沒有資料綁定的最適化表單。 ](convert-existing-forms-to-adaptive-forms.md)請確定您選取&#x200B;**[!UICONTROL Generate adaptive form(s) without data bindings]**&#x200B;核取方塊，以產生沒有資料系結的最適化表單。

![沒有資料捆綁的適用性表單](assets/generate_af_without_binding.png)

產生沒有資料系結的適用性表單後，請為適用性表單選取資料來源：

* [資料庫、OData或任何第三方服務](#sqldatasource)
* [JSON結構](#jsondatasource)
* [XSD架構](#xsddatasource)

>[!NOTE]
> 如果您使用Automated forms conversion服務轉換的適用性表單包含多個具有相同名稱的欄位，請確定這些欄位已系結至資料來源實體，以避免提交期間可能發生資料遺失。


### 使用資料庫、OData或任何第三方服務作為資料源 {#sqldatasource}

使用案例：使用Automated forms conversion服務生成沒有資料綁定的適用性表單，並將MYSQL資料庫配置為資料源。 您可以手動系結最適化表單欄位，以形成資料模型實體，並使用&#x200B;**[!UICONTROL Form Data Model Prefill Service]**&#x200B;選項預填欄位值。 您可使用&#x200B;**[!UICONTROL Submit using Form Data Model]**&#x200B;選項提交最適化表單。

執行使用案例之前：

* [將MySQL資料庫配置為資料源](https://helpx.adobe.com/experience-manager/6-5/forms/using/configure-data-sources.html#configurerelationaldatabase)
* [建立表單資料模型](https://helpx.adobe.com/experience-manager/6-5/forms/using/work-with-form-data-model.html)

根據使用案例，建立&#x200B;**loanapplication**&#x200B;表單資料模型，並將讀取服務引數綁定到&#x200B;**[!UICONTROL Literal]**&#x200B;值。 電話號碼常值必須是在MySQL資料庫的&#x200B;**applicant**&#x200B;架構中配置的記錄之一。 服務會使用值作為引數，從資料來源擷取詳細資料。 您也可以從&#x200B;**[!UICONTROL Binding To]**&#x200B;下拉式清單中選取[使用者設定檔屬性或請求屬性](https://helpx.adobe.com/experience-manager/6-5/forms/using/work-with-form-data-model.html#bindargument)

![設定表單資料模型](assets/configure_model_object.png)

>[!NOTE]
>
>請務必將&#x200B;**get**&#x200B;和&#x200B;**insert**&#x200B;服務新增至表單資料模型、設定及測試服務，再執行使用案例。

執行下列步驟：

1. 選擇&#x200B;**[!UICONTROL output]**&#x200B;資料夾中可用的轉換的&#x200B;**貸款申請表單**，然後點選&#x200B;**[!UICONTROL Properties]**。
1. 點選&#x200B;**[!UICONTROL Form Model]**&#x200B;標籤，從&#x200B;**[!UICONTROL Select From]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL Form Data Model]**，然後點選&#x200B;**[!UICONTROL Select Form Data Model]**&#x200B;以選取&#x200B;**loanapplication**&#x200B;表單資料模型。 點選&#x200B;**[!UICONTROL Save & Close]**&#x200B;以儲存表單。
1. 選擇&#x200B;**示例貸款申請表**&#x200B;並點選&#x200B;**[!UICONTROL Edit]**。
1. 在&#x200B;**[!UICONTROL Content]**&#x200B;標籤中，點選設定圖示：

   ![配置表單容器](assets/configure_form_container.png)

   1. 在&#x200B;**[!UICONTROL Basic]**&#x200B;區段中，從&#x200B;**[!UICONTROL Prefill Service]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL Form Data Model Prefill service]**。

   1. 在&#x200B;**[!UICONTROL Submission]**&#x200B;區段中，從&#x200B;**[!UICONTROL Submit Action]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL Submit using Form Data Model]**。

   1. 使用&#x200B;**[!UICONTROL Data Model to submit]**&#x200B;欄位選取資料模型。
   1. 點選![完成圖示](assets/save_icon.svg)以儲存屬性。

1. 點選「申請人名稱」文字方塊，然後選取![設定圖示](assets/configure_icon.svg)（設定）。

   1. 在「綁定引用」欄位中，選擇「**申請人** > **名稱**」，然後點選「![完成」表徵圖](assets/save_icon.svg)以保存屬性。 同樣，為&#x200B;**地址**、**電話號碼**、**電子郵件**、**佔領**、**年薪（美元）**&#x200B;和&#x200B;**否建立資料綁定。 具有表單資料模型圖元的從屬族成員**&#x200B;欄位。

   ![系結參考](assets/bind_references.png)

1. 點選&#x200B;**[!UICONTROL Preview]**&#x200B;以檢視預填的最適化表單欄位值。
1. 視需要修改欄位值，並提交最適化表單。 欄位值將提交到MySQL資料庫。 您可以刷新資料庫中的&#x200B;**applicant**&#x200B;表，以查看表中更新的值。

**使用案例：** 您可使用Automated forms conversion服務產生沒有資料捆綁的最適化表單，並將MYSQL資料庫設為資料來源。您可以使用規則編輯器系結最適化表單欄位，以預填欄位值。 視需要修改欄位值，並將資料提交至crx-repository。

執行下列步驟以使用[規則編輯器](https://helpx.adobe.com/experience-manager/6-5/forms/using/rule-editor.html)來叫用表單資料模型服務，以系結自適性表單中的欄位和預先填入值：

1. 在&#x200B;**[!UICONTROL output]**&#x200B;資料夾中，選取&#x200B;**貸款申請表範例**，然後點選&#x200B;**[!UICONTROL Edit]**。
1. 在&#x200B;**[!UICONTROL Content]**&#x200B;標籤中，點選設定圖示：

   ![配置表單容器](assets/configure_form_container.png)

   在&#x200B;**[!UICONTROL Basic]**&#x200B;區段中，從&#x200B;**[!UICONTROL Prefill Service]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL Form Data Model Prefill service]**。

1. 點選&#x200B;**[!UICONTROL Applicant Name]**&#x200B;文字方塊，然後點選&#x200B;**[!UICONTROL Edit Rules]**。

   ![編輯規則以建立資料綁定](assets/edit_rules_bind_reference.png)

1. 點選「規則編輯器」頁面上的&#x200B;**[!UICONTROL Create]**。
1. 在&#x200B;**[!UICONTROL Rule Editor]**&#x200B;頁面上：

   1. 為「申請人名稱」文本框選擇狀態。 例如， **[!UICONTROL is initialized]**，在&#x200B;**[!UICONTROL Preview]**&#x200B;模式中呈現表單時，會導致執行&#x200B;**[!UICONTROL Then]**&#x200B;條件。

   1. 在&#x200B;**[!UICONTROL Then]**&#x200B;區段中，從&#x200B;**[!UICONTROL Select Action]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL Invoke Service]**。 Forms例項上的所有服務都會顯示在下拉式清單中。

   1. 從列出表單資料模型的區段中選取&#x200B;**[!UICONTROL Get]**&#x200B;服務。 「輸入」欄位顯示&#x200B;**電話號碼**，該鍵是為&#x200B;**applicant**&#x200B;資料模型定義的主鍵。 系統會根據此欄位，擷取並預填輸出區段中欄位的最適化表單中的值。

   1. 使用「輸出」區段，使用表單資料模型實體建立最適化表單欄位的系結。 例如，使用&#x200B;**name**&#x200B;實體綁定&#x200B;**[!UICONTROL Applicant Name]**&#x200B;適用性表單欄位。

   1. 點選&#x200B;**[!UICONTROL Done]**。 在規則編輯器頁面上再次點選&#x200B;**[!UICONTROL Done]**。

   ![用於綁定引用的規則編輯器](assets/rule_editor_bind_references.png)

1. 點選&#x200B;**[!UICONTROL Preview]**&#x200B;以檢視預填的最適化表單欄位值。

   >[!NOTE]
   >
   >在與適用性表單相關聯的表單資料模型中，確保&#x200B;**get**&#x200B;服務屬性的&#x200B;**[!UICONTROL Return Array]**&#x200B;屬性設為OFF。

1. 視需要修改欄位值，並提交最適化表單。 已提交的資料位於crx-repository中的以下位置：

   `http://host name:port/crx/de/index.jsp#/content/forms/fp/admin/submit/data/latest file available in the folder`

### 使用JSON結構作為資料來源 {#jsondatasource}

**使用案例：** 您使用Automated forms conversion服務產生沒有資料捆綁的適用性表單，並將JSON結構設為資料來源。您可以手動將適用性表單欄位系結至JSON結構，並使用&#x200B;**預覽與資料**&#x200B;選項來預填欄位值。 視需要修改欄位值，並將資料提交至crx-repository。

執行使用案例之前，請確定您具備：

* [符合JSON結構的有效JSON結構](#prepare-data-for-form-model)
* [沒有資料捆綁的最適化表單](#generate-adaptive-forms-with-no-data-binding)

執行下列步驟：

1. 選擇&#x200B;**output**&#x200B;資料夾中可用的轉換的&#x200B;**貸款申請表單**，然後點選&#x200B;**[!UICONTROL Properties]**。
1. 點選&#x200B;**[!UICONTROL Form Model]**&#x200B;標籤，從&#x200B;**[!UICONTROL Select From]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL Schema]**，然後點選&#x200B;**[!UICONTROL Select Schema]**&#x200B;以上傳儲存在本機檔案系統上的&#x200B;**demo.schema JSON**&#x200B;結構。 點選&#x200B;**[!UICONTROL Save & Close]**&#x200B;以儲存表單。
1. 選擇&#x200B;**示例貸款申請表**&#x200B;並點選&#x200B;**[!UICONTROL Edit]**。
1. 點選「申請人名稱」文字方塊，然後選取![設定圖示](assets/configure_icon.svg)（設定）。

   在「綁定引用」欄位中，選擇「**申請人** > **名稱**」，然後點選「![完成」表徵圖](assets/save_icon.svg)以保存屬性。 同樣，為&#x200B;**地址**、**電話號碼**、**電子郵件**、**佔領**、**年薪（美元）**&#x200B;和&#x200B;**否建立資料綁定。 包含JSON結構實體的相依族成員**&#x200B;欄位。

1. 再次選擇&#x200B;**[!UICONTROL output]**&#x200B;資料夾中可用的轉換的&#x200B;**貸款申請表**，然後選擇&#x200B;**[!UICONTROL Preview]** > **[!UICONTROL Preview with Data]**。</br>

   下載範例資料檔案</br>

   [取得檔案](assets/json_data_file.txt)</br>

1. 視需要修改欄位值，並提交最適化表單。 已提交的資料位於crx-repository中的以下位置：

   `http://host name:port/crx/de/index.jsp#/content/forms/fp/admin/submit/data/latest file available in the folder`

### 使用XSD架構作為資料來源 {#xsddatasource}

**使用案例：** 您使用Automated forms conversion服務產生沒有資料捆綁的適用性表單，並將XSD架構設為資料來源。您可以手動將適用性表單欄位系結至XSD架構，並使用&#x200B;**預覽與資料**&#x200B;來預填欄位值。 視需要修改欄位值，並將資料提交至crx-repository。

執行使用案例之前，請確定您具備：

* [與XML架構結構相容的有效XSD架構](#prepare-data-for-form-model)
* [沒有資料捆綁的最適化表單](#generate-adaptive-forms-with-no-data-binding)

執行下列步驟：

1. 選擇&#x200B;**[!UICONTROL output]**&#x200B;資料夾中可用的轉換的&#x200B;**貸款申請表單**，然後點選&#x200B;**[!UICONTROL Properties]**。
1. 點選&#x200B;**[!UICONTROL Form Model]**&#x200B;標籤，從&#x200B;**[!UICONTROL Select From]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL Schema]**，然後點選&#x200B;**[!UICONTROL Select Schema]**&#x200B;以上傳儲存在本機檔案系統上的&#x200B;**loanapplication** XSD架構。 選取XSD架構的根元素，然後點選&#x200B;**[!UICONTROL Save & Close]**&#x200B;以儲存表單。
1. 選擇&#x200B;**示例貸款申請表**&#x200B;並點選&#x200B;**[!UICONTROL Edit]**。
1. 點選「申請人名稱」文字方塊，然後選取![設定圖示](assets/configure_icon.svg)（設定）。
在「綁定引用」欄位中，選擇「**申請人** > **名稱**」，然後點選「![完成表徵圖](assets/save_icon.svg)」以保存屬性。 同樣，為&#x200B;**地址**、**電話號碼**、**電子郵件**、**佔領**、**年薪（美元）**&#x200B;和&#x200B;**否建立資料綁定。 包含XSD架構實體的相依家族成員**&#x200B;欄位。

1. 再次選擇&#x200B;**output**&#x200B;資料夾中可用的轉換的&#x200B;**貸款申請表**，然後選擇&#x200B;**[!UICONTROL Preview]** > **[!UICONTROL Preview with Data]**。</br>

   下載範例資料檔案</br>

   [取得檔案](assets/loan-application-data-xml-data.zip)</br>


1. 視需要修改欄位值，並提交最適化表單。 已提交的資料位於crx-repository中的以下位置：

   `http://host name:port/crx/de/index.jsp#/content/forms/fp/admin/submit/data/latest file available in the folder`

## 使用JSON捆綁{#generate-adaptive-forms-with-json-binding}產生最適化表單

使用[Automated forms conversion服務將[貸款申請表](#sample-adaptive-form)範例轉換為具有資料綁定的最適化表單。 ](convert-existing-forms-to-adaptive-forms.md)產生最適化表單時，請確定您未選取&#x200B;**[!UICONTROL Generate adaptive form(s) without data bindings]**&#x200B;核取方塊。

![具有JSON捆綁的適用性表單](assets/generate_af_with_data_bindings.png)

### 使用JSON結構作為資料來源 {#jsonwithdatabinding}

**使用案例：** 您使用Automated forms conversion服務產生具有JSON資料捆綁的最適化表單。預填服務和表單提交功能無縫。 您不需要任何設定步驟。

在執行使用案例之前，請確定您有[具有資料捆綁的最適化表單](#generate-adaptive-forms-with-json-binding)。

執行下列步驟：

1. 再次選擇&#x200B;**[!UICONTROL output]**&#x200B;資料夾中可用的轉換的&#x200B;**貸款申請表**，然後選擇&#x200B;**[!UICONTROL Preview]** > **[!UICONTROL Preview with Data]**。</br>

   下載範例資料檔案</br>

   [取得檔案](assets/loan_application_data_source_json_data_binding.txt)</br>

1. 視需要修改欄位值，並提交最適化表單。 已提交的資料位於crx-repository中的以下位置：

   `http://host name:port/crx/de/index.jsp#/content/forms/fp/admin/submit/data/latest file available in the folder`

## 將提交的最適化表單JSON資料轉換為XML格式{#convert-submitted-adaptive-form-data-to-xml}

在最適化表單欄位中輸入值並提交時，資料會以JSON格式顯示在crx-repository中。 您可以使用[org.apache.sling.commons.json.xml](https://sling.apache.org/apidocs/sling5/org/apache/sling/commons/json/xml/XML.html#toString) API或下列范常式式碼，將JSON資料格式轉換為XML:

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
