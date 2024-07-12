---
title: 基於資料來源的建議預填及提交最適化表單的工作流程
description: 針對使用Automated forms conversion服務(AFCS)產生的最適化表單，以資料來源為基礎的預先填寫和提交工作流程。
solution: Experience Manager Forms
feature: Adaptive Forms
topic: Administration
topic-tags: forms
role: Admin, Developer
level: Beginner, Intermediate
contentOwner: khsingh
exl-id: 5deef8f5-5098-47c1-b696-b2db59e92931
source-git-commit: c2392932d1e29876f7a11bd856e770b8f7ce3181
workflow-type: tm+mt
source-wordcount: '2397'
ht-degree: 1%

---

# 基於資料來源的建議預填及提交最適化表單的工作流程 {#recommended-data-source-btased-prefill-and-submit-workflows-for-adaptive-forms}

您可以透過透過Automated forms conversion服務(AFCS)轉換的最適化表單，使用下列任何資料來源：

* 表單資料模型、OData或任何其他協力廠商服務
* JSON結構描述
* XSD結構描述

根據資料來源，您可以選擇產生含有或不含資料模型的最適化表單。

本文說明選取資料來源並使用轉換服務產生最適化表單後，要預先填入欄位值和提交選項的建議工作流程。

<table> 
 <tbody> 
  <tr> 
   <th><strong>資料來源</strong></th> 
   <th><strong>建議的工作流程</strong></th> 
  </tr> 
  <tr> 
   <td><p>表單資料模型、OData或任何其他協力廠商服務</p></td> 
   <td> 
    <p><strong>選項1</strong>：您選取表單資料模型、OData或任何其他協力廠商服務做為資料來源。 您<a href="#generate-adaptive-forms-with-no-data-binding">使用Automated forms conversion服務(AFCS)產生無資料繫結的最適化表單</a>。 您可以手動將最適化表單欄位繫結至表單資料模型實體，並使用「表單資料模型預填服務」選項來預填欄位值。 使用「使用表單資料模型提交」選項來提交最適化表單。</p></td> 
  </tr>
  <tr> 
   <td></td> 
   <td> 
   <p><strong>選項2</strong>：您選取表單資料模型、OData或任何其他協力廠商服務做為資料來源。 您<a href="#generate-adaptive-forms-with-no-data-binding">使用Automated forms conversion服務(AFCS)產生無資料繫結的最適化表單</a>。 您可以使用規則編輯器繫結調適型表單欄位以預填欄位值。 如有需要，請修改欄位值，並將資料提交至crx-repository。</p>
    </td> 
  </tr>
  <tr> 
   <td></td> 
   <td> 
    <p>如需執行這些工作流程的逐步指示，請參閱<a href="#sqldatasource">使用資料庫、OData或任何協力廠商服務做為資料來源。</a></p> </td> 
  </tr>
  <tr>
  <td><p>JSON結構描述</p></td> 
   <td> 
    <p>選取JSON結構描述作為資料來源。 根據選取的資料來源：</p></td> 
  </tr>
  <tr>
  <td></td> 
   <td> 
    <p><strong>選項1</strong>：您<a href="#generate-adaptive-forms-with-no-data-binding">使用Automated forms conversion服務(AFCS)產生無資料繫結的最適化表單</a>，並將JSON結構描述設定為資料來源。 您手動將最適化表單欄位繫結到JSON結構描述，然後<a href="https://helpx.adobe.com/experience-manager/6-5/forms/using/prepopulate-adaptive-form-fields.html#Supportedprotocolsforprefillinguserdata" target="_blank">使用任何支援的通訊協定</a>來預先填入欄位值。 如有需要，請修改欄位值，並將資料提交至crx-repository。</p></td> 
  </tr>
  <tr>
  <td></td> 
   <td> 
    <p>如需執行工作流程的逐步指示，請參閱<a href="#jsondatasource">使用JSON結構描述作為資料來源。</p></td> 
  </tr>
  <tr>
  <td></td> 
   <td> 
    <p><strong>選項2</strong>：您<a href="#generate-adaptive-forms-with-json-binding">使用Automated forms conversion服務(AFCS)產生具有JSON資料繫結的最適化表單</a>。 預填服務與表單提交功能順暢無礙。 您不需要任何設定步驟。</p> </td> 
  </tr>
   <tr>
  <td></td> 
   <td> 
    <p>如需執行工作流程的逐步指示，請參閱<a href="#jsonwithdatabinding">使用JSON結構描述作為資料來源。</a></p> </td> 
  </tr>
  <tr>
  <td><p>XSD結構描述</p></td> 
   <td> 
    <p>選取XSD結構描述作為資料來源。 根據選取的資料來源，您<a href="#generate-adaptive-forms-with-no-data-binding">使用Automated forms conversion服務(AFCS)產生無資料繫結的最適化表單</a>，並將XSD結構描述設定為資料來源。 您手動將最適化表單欄位繫結到XSD結構描述，然後<a href="https://helpx.adobe.com/experience-manager/6-5/forms/using/prepopulate-adaptive-form-fields.html#Supportedprotocolsforprefillinguserdata" target="_blank">使用任何支援的通訊協定</a>來預先填入欄位值。 如有需要，請修改欄位值，並將資料提交至crx-repository。</p>
    </td> 
  </tr>
  <tr>
  <td></td> 
   <td> 
    <p>如需執行工作流程的逐步指示，請參閱<a href="#xsddatasource">使用XSD結構描述做為資料來源。</a></p>
    </td> 
  </tr>
 </tbody> 
</table>


如需Automated forms conversion服務(AFCS)的詳細資訊，請參閱下列文章：

* [automated forms conversion服務簡介](introduction.md)
* [設定Automated forms conversion服務](configure-service.md)
* [將列印表單轉換為最適化表單](convert-existing-forms-to-adaptive-forms.md)
* [檢閱並修正轉換後的表單](review-correct-ui-edited.md)

本文提供的資訊乃基於以下假設，即任何閱讀此假設的人皆具備調適型表單概念的基本知識。

## 必要條件 {#pre-requisites}

* 設定[AEM作者執行個體](https://helpx.adobe.com/experience-manager/6-5/sites/deploying/using/deploy.html)
* 在AEM編寫執行個體](configure-service.md)上設定[Automated forms conversion服務(AFCS)

## 最適化表單範例 {#sample-adaptive-form}

若要執行使用案例以預先填寫最適化表單中的欄位值並將它們提交至資料來源，請下載以下範例PDF檔案。

貸款申請表範例

[取得檔案](assets/sample_loan_application_form.pdf)

PDF檔案可作為Automated forms conversion服務(AFCS)的輸入。 此服務會將此檔案轉換為最適化表單。 下圖以PDF格式說明範例貸款申請。

![貸款申請表範例](assets/sample_form_new.png)

## 為表單模型準備資料 {#prepare-data-for-form-model}

AEM Forms資料整合可讓您設定並連線至不同的資料來源。 使用轉換程式產生最適化表單後，您可以根據表單資料模型、XSD或JSON結構描述定義表單模型。 您可以使用資料庫、Microsoft Dynamics或任何其他協力廠商服務來建立表單資料模型。

本教學課程使用MySQL資料庫作為建立表單資料模型的來源。 在資料庫中建立&#x200B;**loanapplication**&#x200B;結構描述，並根據最適化表單中可用的欄位，將&#x200B;**application**&#x200B;資料表新增到結構描述中。

![範例資料mysql](assets/sample_data_mysql.png)

您可以使用下列DDL陳述式在資料庫中建立&#x200B;**應徵者**&#x200B;資料表。

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

如果您使用XSD結構描述作為表單模型來執行使用案例，請建立包含以下文字的XSD檔案：

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

或將XSD結構描述下載至本機檔案系統。

貸款應用程式XSD結構描述範例

[取得檔案](assets/loanapplication.xsd)

如需有關使用XSD結構描述作為調適型表單中的表單模型的詳細資訊，請參閱[使用XML結構描述建立調適型表單](https://helpx.adobe.com/experience-manager/6-5/forms/using/adaptive-form-xml-schema-form-model.html)。

如果您使用JSON結構描述作為表單模型來執行使用案例，請建立包含以下文字的JSON檔案：

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

或將JSON結構描述下載至本機檔案系統。

貸款應用程式JSON結構描述範例

[取得檔案](assets/demo_schema.json)

如需有關使用JSON結構描述作為調適型表單中的表單模型的詳細資訊，請參閱[使用JSON結構描述建立調適型表單](https://helpx.adobe.com/experience-manager/6-5/forms/using/adaptive-form-json-schema-form-model.html)。

## 產生無資料繫結的最適化表單 {#generate-adaptive-forms-with-no-data-binding}

使用[Automated forms conversion服務將](convert-existing-forms-to-adaptive-forms.md) [範例貸款申請表單](#sample-adaptive-form)轉換為無資料繫結的最適化表單。 請確定您選取&#x200B;**[!UICONTROL Generate adaptive form(s) without data bindings]**&#x200B;核取方塊以產生無資料繫結的最適化表單。

![無資料繫結的最適化表單](assets/generate_af_without_binding.png)

產生無資料繫結的調適型表單後，請為調適型表單選取資料來源：

* [資料庫、OData或任何協力廠商服務](#sqldatasource)
* [JSON結構描述](#jsondatasource)
* [XSD結構描述](#xsddatasource)

>[!NOTE]
> 如果您使用Automated forms conversion服務(AFCS)轉換的最適化表單包含多個同名欄位，請確保這些欄位已繫結至資料來源實體，以避免在提交期間可能遺失資料。
>

### 使用資料庫、OData或任何第三方服務做為資料來源 {#sqldatasource}

使用案例：您可以使用Automated forms conversion服務(AFCS)產生無資料繫結的最適化表單，並將MYSQL資料庫設定為資料來源。 您手動將最適化表單欄位繫結到表單資料模型實體，並使用&#x200B;**[!UICONTROL Form Data Model Prefill Service]**&#x200B;選項預先填寫欄位值。 您使用&#x200B;**[!UICONTROL Submit using Form Data Model]**&#x200B;選項來提交最適化表單。

執行使用案例之前：

* [將MySQL資料庫設定為資料來源](https://helpx.adobe.com/experience-manager/6-5/forms/using/configure-data-sources.html#configurerelationaldatabase)
* [建立表單資料模型](https://helpx.adobe.com/experience-manager/6-5/forms/using/work-with-form-data-model.html)

根據使用案例，建立&#x200B;**載入應用程式**&#x200B;表單資料模型，並將讀取服務引數繫結至&#x200B;**[!UICONTROL Literal]**&#x200B;值。 電話號碼常值必須是MySQL資料庫的&#x200B;**應徵者**&#x200B;結構描述中設定的其中一個記錄。 服務會使用值作為引數，從資料來源擷取詳細資料。 您也可以從&#x200B;**[!UICONTROL Binding To]**&#x200B;下拉式清單中選取[使用者設定檔屬性或要求屬性](https://helpx.adobe.com/experience-manager/6-5/forms/using/work-with-form-data-model.html#bindargument)

![設定表單資料模型](assets/configure_model_object.png)

>[!NOTE]
>
>在執行使用案例之前，請確定您已新增&#x200B;**get**&#x200B;和&#x200B;**insert**&#x200B;服務至表單資料模型、設定及測試服務。

執行以下步驟：

1. 選取&#x200B;**[!UICONTROL output]**&#x200B;資料夾中可用的已轉換的&#x200B;**範例貸款申請表單**，然後點選&#x200B;**[!UICONTROL Properties]**。
1. 點選&#x200B;**[!UICONTROL Form Model]**&#x200B;標籤，從&#x200B;**[!UICONTROL Select From]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL Form Data Model]**，然後點選&#x200B;**[!UICONTROL Select Form Data Model]**&#x200B;以選取&#x200B;**借出應用程式**&#x200B;表單資料模型。 點選&#x200B;**[!UICONTROL Save & Close]**&#x200B;以儲存表單。
1. 選取&#x200B;**範例貸款申請表單**&#x200B;並點選&#x200B;**[!UICONTROL Edit]**。
1. 在「**[!UICONTROL Content]**」標籤中，點選「設定」圖示：

   ![設定表單容器](assets/configure_form_container.png)

   1. 在&#x200B;**[!UICONTROL Basic]**&#x200B;區段中，從&#x200B;**[!UICONTROL Prefill Service]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL Form Data Model Prefill service]**。

   1. 在&#x200B;**[!UICONTROL Submission]**&#x200B;區段中，從&#x200B;**[!UICONTROL Submit Action]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL Submit using Form Data Model]**。

   1. 使用&#x200B;**[!UICONTROL Data Model to submit]**&#x200B;欄位選取資料模型。
   1. 點選![完成圖示](assets/save_icon.svg)以儲存屬性。

1. 點選「申請人名稱」文字方塊，然後選取![設定圖示](assets/configure_icon.svg) （設定）。

   1. 在[繫結參考]欄位中，選取&#x200B;**應徵者** > **名稱**，然後點選![完成圖示](assets/save_icon.svg)以儲存內容。 同樣地，為&#x200B;**地址**、**電話號碼**、**電子郵件**、**職業**、**年薪（美元）**&#x200B;和&#x200B;**否，建立資料繫結。 具有表單資料模型實體的相依家族成員**&#x200B;欄位。

   ![繫結參考](assets/bind_references.png)

1. 點選&#x200B;**[!UICONTROL Preview]**&#x200B;以檢視預填的最適化表單欄位值。
1. 如有需要，請修改欄位值並提交最適化表單。 欄位值會提交至MySQL資料庫。 您可以重新整理資料庫中的&#x200B;**應徵者**&#x200B;資料表，以檢視資料表中更新的值。

**使用案例：**&#x200B;您使用Automated forms conversion服務(AFCS)產生無資料繫結的最適化表單，並將MYSQL資料庫設定為資料來源。 您可以使用規則編輯器繫結調適型表單欄位以預填欄位值。 如有需要，請修改欄位值，並將資料提交至crx-repository。

執行以下步驟以使用[規則編輯器](https://helpx.adobe.com/experience-manager/6-5/forms/using/rule-editor.html)來叫用表單資料模型服務，以繫結最適化表單中的欄位和預填值：

1. 選取&#x200B;**[!UICONTROL output]**&#x200B;資料夾中的&#x200B;**範例貸款申請表**，然後點選&#x200B;**[!UICONTROL Edit]**。
1. 在「**[!UICONTROL Content]**」標籤中，點選「設定」圖示：

   ![設定表單容器](assets/configure_form_container.png)

   在&#x200B;**[!UICONTROL Basic]**&#x200B;區段中，從&#x200B;**[!UICONTROL Prefill Service]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL Form Data Model Prefill service]**。

1. 點選&#x200B;**[!UICONTROL Applicant Name]**&#x200B;文字方塊並點選&#x200B;**[!UICONTROL Edit Rules]**。

   ![編輯規則以建立資料繫結](assets/edit_rules_bind_reference.png)

1. 在規則編輯器頁面上點選&#x200B;**[!UICONTROL Create]**。
1. 在&#x200B;**[!UICONTROL Rule Editor]**&#x200B;頁面上：

   1. 選取「申請人名稱」文字方塊的州。 例如，**[!UICONTROL is initialized]**，當您以&#x200B;**[!UICONTROL Preview]**&#x200B;模式轉譯表單時，這會導致&#x200B;**[!UICONTROL Then]**&#x200B;條件的執行。

   1. 在&#x200B;**[!UICONTROL Then]**&#x200B;區段中，從&#x200B;**[!UICONTROL Select Action]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL Invoke Service]**。 Forms執行個體上的所有服務都會顯示在下拉式清單中。

   1. 從列出表單資料模型的區段中選取&#x200B;**[!UICONTROL Get]**&#x200B;服務。 輸入欄位顯示&#x200B;**phonenumber**，這是為&#x200B;**應徵者**&#x200B;資料模型定義的主索引鍵。 系統會根據此欄位，擷取並預填輸出區段中欄位適用性表單的值。

   1. 使用「輸出」區段建立最適化表單欄位與表單資料模型實體的繫結。 例如，將&#x200B;**[!UICONTROL Applicant Name]**&#x200B;最適化表單欄位與&#x200B;**名稱**&#x200B;實體繫結。

   1. 點選 **[!UICONTROL Done]**。在規則編輯器頁面上再次點選&#x200B;**[!UICONTROL Done]**。

   ![繫結參考的規則編輯器](assets/rule_editor_bind_references.png)

1. 點選&#x200B;**[!UICONTROL Preview]**&#x200B;以檢視預填的最適化表單欄位值。

   >[!NOTE]
   >
   >確定與最適化表單關聯的表單資料模型中，**get**&#x200B;服務屬性的&#x200B;**[!UICONTROL Return Array]**&#x200B;屬性設定為OFF。

1. 如有需要，請修改欄位值並提交最適化表單。 提交的資料可在crx-repository中的以下位置找到：

   `http://host name:port/crx/de/index.jsp#/content/forms/fp/admin/submit/data/latest file available in the folder`

### 使用JSON結構描述作為資料來源 {#jsondatasource}

**使用案例：**&#x200B;您使用Automated forms conversion服務(AFCS)產生無資料繫結的最適化表單，並將JSON結構描述設定為資料來源。 您手動將最適化表單欄位繫結到JSON結構描述，並使用&#x200B;**含有資料的預覽**&#x200B;選項來預填欄位值。 如有需要，請修改欄位值，並將資料提交至crx-repository。

在執行使用案例之前，請確定您擁有：

* [符合JSON結構描述結構的有效JSON結構描述](#prepare-data-for-form-model)
* [無資料繫結的最適化表單](#generate-adaptive-forms-with-no-data-binding)

執行以下步驟：

1. 選取&#x200B;**輸出**&#x200B;資料夾中可用的已轉換的&#x200B;**範例貸款申請表單**，然後點選&#x200B;**[!UICONTROL Properties]**。
1. 點選「**[!UICONTROL Form Model]**」標籤，從「**[!UICONTROL Select From]**」下拉式清單中選取「**[!UICONTROL Schema]**」，然後點選「**[!UICONTROL Select Schema]**」以上傳儲存在本機檔案系統上的&#x200B;**demo.schema JSON**&#x200B;結構描述。 點選&#x200B;**[!UICONTROL Save & Close]**&#x200B;以儲存表單。
1. 選取&#x200B;**範例貸款申請表單**&#x200B;並點選&#x200B;**[!UICONTROL Edit]**。
1. 點選「申請人名稱」文字方塊，然後選取![設定圖示](assets/configure_icon.svg) （設定）。

   在[繫結參考]欄位中，選取&#x200B;**應徵者** > **名稱**，然後點選![完成圖示](assets/save_icon.svg)以儲存內容。 同樣地，為&#x200B;**地址**、**電話號碼**、**電子郵件**、**職業**、**年薪（美元）**&#x200B;和&#x200B;**否，建立資料繫結。 具有JSON結構描述實體的相依家族成員**&#x200B;欄位。

1. 再次選取&#x200B;**[!UICONTROL output]**&#x200B;資料夾中可用的轉換的&#x200B;**範例貸款申請表單**，然後選取&#x200B;**[!UICONTROL Preview]** > **[!UICONTROL Preview with Data]**。</br>

   下載範例資料檔</br>

   [取得檔案](assets/json_data_file.txt)</br>

1. 如有需要，請修改欄位值並提交最適化表單。 提交的資料可在crx-repository中的以下位置找到：

   `http://host name:port/crx/de/index.jsp#/content/forms/fp/admin/submit/data/latest file available in the folder`

### 使用XSD結構描述做為資料來源 {#xsddatasource}

**使用案例：**&#x200B;您使用Automated forms conversion服務(AFCS)產生無資料繫結的最適化表單，並將XSD結構描述設定為資料來源。 您手動將最適化表單欄位繫結到XSD結構描述，並使用&#x200B;**含有資料的預覽**&#x200B;來預填欄位值。 如有需要，請修改欄位值，並將資料提交至crx-repository。

在執行使用案例之前，請確定您擁有：

* [符合XML結構描述結構的有效XSD結構描述](#prepare-data-for-form-model)
* [無資料繫結的最適化表單](#generate-adaptive-forms-with-no-data-binding)

執行以下步驟：

1. 選取&#x200B;**[!UICONTROL output]**&#x200B;資料夾中可用的已轉換的&#x200B;**範例貸款申請表單**，然後點選&#x200B;**[!UICONTROL Properties]**。
1. 點選&#x200B;**[!UICONTROL Form Model]**&#x200B;標籤，從&#x200B;**[!UICONTROL Select From]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL Schema]**，然後點選&#x200B;**[!UICONTROL Select Schema]**&#x200B;以上傳儲在本機檔案系統上的&#x200B;**loanapplication** XSD結構描述。 選取XSD結構描述的根元素，然後點選&#x200B;**[!UICONTROL Save & Close]**&#x200B;以儲存表單。
1. 選取&#x200B;**範例貸款申請表單**&#x200B;並點選&#x200B;**[!UICONTROL Edit]**。
1. 點選「申請人名稱」文字方塊，然後選取![設定圖示](assets/configure_icon.svg) （設定）。
在「繫結參考」欄位中，選取**應徵者** > **名稱**，然後點選![完成圖示](assets/save_icon.svg)以儲存屬性。 同樣地，為&#x200B;**地址**、**電話號碼**、**電子郵件**、**職業**、**年薪（美元）**&#x200B;和&#x200B;**否，建立資料繫結。 具有XSD結構描述實體的相依家族成員**&#x200B;欄位。

1. 再次選取&#x200B;**輸出**&#x200B;資料夾中可用的已轉換的&#x200B;**範例貸款申請表單**，然後選取&#x200B;**[!UICONTROL Preview]** > **[!UICONTROL Preview with Data]**。</br>

   下載範例資料檔</br>

   [取得檔案](assets/loan-application-data-xml-data.zip)</br>


1. 如有需要，請修改欄位值並提交最適化表單。 提交的資料可在crx-repository中的以下位置找到：

   `http://host name:port/crx/de/index.jsp#/content/forms/fp/admin/submit/data/latest file available in the folder`

## 產生具有JSON繫結的最適化表單 {#generate-adaptive-forms-with-json-binding}

使用[Automated forms conversion服務(AFCS)將](convert-existing-forms-to-adaptive-forms.md) [範例貸款申請表單](#sample-adaptive-form)轉換為具有資料繫結的最適化表單。 確保在產生最適化表單時不要選取&#x200B;**[!UICONTROL Generate adaptive form(s) without data bindings]**&#x200B;核取方塊。

![具有JSON繫結的最適化表單](assets/generate_af_with_data_bindings.png)

### 使用JSON結構描述作為資料來源 {#jsonwithdatabinding}

**使用案例：**&#x200B;您使用Automated forms conversion服務(AFCS)產生具有JSON資料繫結的最適化表單。 預填服務與表單提交功能順暢無礙。 您不需要任何設定步驟。

在執行使用案例之前，請確定您有[具有資料繫結的最適化表單](#generate-adaptive-forms-with-json-binding)。

執行以下步驟：

1. 再次選取&#x200B;**[!UICONTROL output]**&#x200B;資料夾中可用的轉換的&#x200B;**範例貸款申請表單**，然後選取&#x200B;**[!UICONTROL Preview]** > **[!UICONTROL Preview with Data]**。</br>

   下載範例資料檔</br>

   [取得檔案](assets/loan_application_data_source_json_data_binding.txt)</br>

1. 如有需要，請修改欄位值並提交最適化表單。 提交的資料可在crx-repository中的以下位置找到：

   `http://host name:port/crx/de/index.jsp#/content/forms/fp/admin/submit/data/latest file available in the folder`

## 將提交的自適應表單JSON資料轉換為XML格式 {#convert-submitted-adaptive-form-data-to-xml}

當您在適用性表單欄位中輸入值並提交時，crx存放庫中的資料可使用JSON格式。 您可以使用[org.apache.sling.commons.json.xml](https://sling.apache.org/apidocs/sling5/org/apache/sling/commons/json/xml/XML.html#toString) API或下列範常式式碼，將JSON資料的格式轉換為XML：

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
