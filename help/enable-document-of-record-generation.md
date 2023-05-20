---
title: 在轉換過程中生成記錄文件
seo-title: Generate Document of Record during conversion
description: 根據用於轉換的源表單類型生成DoR的建議路徑。
seo-description: Recommended paths to generate a DoR based on the type of source forms used for conversion.
page-status-flag: never-activated
uuid: 7f0f5bf3-21be-449a-b23e-5946a9fd7ed4
contentOwner: khsingh
discoiquuid: 75f6e6bc-7636-4b40-919c-8b20a6ccbb1f
exl-id: c24313cd-2b9b-4209-9505-a8e14d8dc530
source-git-commit: 1a3f79925f25dcc7dbe007f6e634f6e3a742bf72
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 2%

---

# 啟用最適化表單生成記錄文件的建議工作流程 {#recommended-workflows-dor-generation}

「記錄文檔」(DoR)使您能夠保留您提供的資訊的記錄並以自適應形式提交，以便您以後可以參考它。
DoR使用基本模板定義其佈局。 可以使用預設模板或將任何其它模板與自適應表單相關聯來生成DoR。

![生成的記錄文檔](assets/document_of_record.gif)

有關生成DoR的詳細資訊，請參見 [為自適應表單生成記錄文檔](https://helpx.adobe.com/experience-manager/6-5/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.html)。

的 [automated forms conversion服務](../help/introduction.md) 將以下源表單轉換為自適應表單：

* 非互動式PDF forms
* 阿克羅Forms
* 基於XFA的PDF forms

根據用於轉換的源窗體，可以使用以下方式生成DoR:

* 預設模板
* 源表單作為模板 — 如果選擇此選項，則轉換服務會自動將源表單與轉換後的自適應表單作為DoR模板相關聯。
* 將任何其他模板與已轉換的自適應表單關聯

下表說明了您使用的DoR模板如何影響生成的DoR的佈局的示例：

<table> 
 <tbody>
 <tr>
  <td><p><strong>源窗體</strong></p></td>
  <td><p><strong>生成的DoR</strong></p></td> 
   </tr>
  <tr>
   <td><img src="assets/source_xdp_updated.png"/></td>
   <td><p>如果使用預設模板生成DoR:</br><img src="assets/source_form_default_updated.png"/></td>
   </tr>
   <tr>
   <td></td>
   <td><p>如果使用源表單作為模板來生成DoR:</br></p><img src="assets/source_form_dor_updated.png"/></td>
   </tr>
  </tbody>
</table>

如表所示，如果使用源表單作為模板，DoR將保留源表單的佈局。
本文介紹了基於三種源表單生成DoR的建議路徑。

<table> 
 <tbody> 
  <tr> 
   <th><strong>源窗體</strong></th> 
   <th><strong>生成DoR的方法</strong></th> 
  </tr> 
  <tr> 
   <td><p>非互動式PDF forms</p></td> 
   <td> 
    <ul> 
     <li><a href="#generate-document-of-record-using-cloud-configuration">在自適應表單轉換之前啟用DoR生成，以使用預設模板生成DoR</a></li> 
     <li><a href="#edit-adaptive-form-properties-generate-document-of-record">在自適應表單轉換後編輯自適應表單屬性，以使用預設或任何其他表單模板啟用DoR生成</a></li> 
    </ul> </td> 
  </tr>
  <tr> 
   <td><p>AcroForms或XFAPDF forms</p></td> 
   <td> 
    <ul> 
     <li><a href="#use-input-form-as-template-to-generate-document-of-record">在自適應表單轉換前啟用DoR生成，以使用源表單作為模板生成DoR</a></li> 
     <li><a href="#edit-adaptive-form-properties-to-generate-document-of-record">在自適應表單轉換後編輯自適應表單屬性，以啟用使用預設模板、源表單作為模板或任何其他表單模板生成DoR</a></li> 
    </ul> </td> 
  </tr>    
 </tbody> 
</table>

## 為非互動式PDF forms生成記錄文檔 {#generate-document-of-record-non-interactive-pdf}

如果使用非互動式PDF表單作為Automated forms conversion服務的源表單，則可以：

* 在自適應表單轉換之前啟用DoR生成，以使用預設模板生成DoR
* 或在自適應表單轉換後編輯自適應表單屬性，以啟用使用預設或任何其他表單模板生成DoR

### 在轉換前啟用DoR生成，以使用預設模板生成DoR {#generate-document-of-record-using-cloud-configuration}

1. 選擇 **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Automated Forms Conversion Configuration]** >用於轉換的雲配置屬性> **[!UICONTROL Advanced]** > **[!UICONTROL Generate Document of Record]** 的雙曲餘切值。

   ![使用雲配置生成記錄文檔](assets/generate_dor_cloud_config.gif)

1. 點擊 **[!UICONTROL Save & Close]** 按鈕。

1. [運行轉換](../help/convert-existing-forms-to-adaptive-forms.md)。 確保使用這些說明步驟1中編輯的雲配置。
在提交轉換後的自適應表單時，DoR將使用預設模板自動生成。

### 在轉換後編輯自適應表單屬性以啟用DoR生成 {#edit-adaptive-form-properties-generate-document-of-record}

如果在將源窗體轉換為自適應窗體之前未啟用DoR生成，則在轉換後仍可啟用。

1. [運行轉換](../help/convert-existing-forms-to-adaptive-forms.md) 在非互動式PDF窗體上生成自適應窗體。

1. 在 **[!UICONTROL output]** 資料夾和點擊 **[!UICONTROL Properties]**。

1. 在 **[!UICONTROL Form Model]** 的 **[!UICONTROL Document of Record Template Configuration]** 選擇 **[!UICONTROL Generate Document of Record]**。

   ![產生記錄文件](assets/generate_dor_af_properties.png)

1. 點擊 **[!UICONTROL Save & Close]** 按鈕。

在提交轉換後的自適應表單時，DoR將使用預設模板自動生成。 如果要將任何其它DoR模板與轉換後的自適應表單相關聯，可以選擇 **[!UICONTROL Associate form template as the Document of Record template]** 的雙曲餘切值。

## 為AcroForms或基於XFA的PDF forms生成記錄文檔 {#generate-document-of-record-acroform-xfaform}

如果使用Acro表單或基於XFA的PDF表單作為Automated forms conversion服務的源表單，則可以：

* 在自適應表單轉換之前啟用DoR生成，以使用源表單作為模板生成DoR

* 或在自適應表單轉換後編輯自適應表單屬性，以啟用使用預設模板、源表單作為模板或任何其他表單模板生成DoR

### 在轉換前啟用DoR生成，以使用源表單模板生成DoR {#use-input-form-as-template-to-generate-document-of-record}

1. 選擇 **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Automated Forms Conversion Configuration]** >用於轉換的雲配置屬性> **[!UICONTROL Advanced]** > **[!UICONTROL Generate Document of Record]** 的雙曲餘切值。

1. 點擊 **[!UICONTROL Save & Close]** 按鈕。

1. [運行轉換](../help/convert-existing-forms-to-adaptive-forms.md)。 確保使用這些說明步驟1中編輯的雲配置。
轉換服務自動將Acro表單或基於XFA的PDF表單與轉換後的自適應表單關聯為DoR模板。
可以開啟自適應表單屬性以在 **[!UICONTROL Document of Record Template Configuration]** 部分 **[!UICONTROL Form Model]** 頁籤。

   ![編輯自適應表單屬性以生成記錄文檔](assets/generate_dor_af_properties_xdp_acro.png)

   在提交轉換後的自適應表單時，DoR將使用源表單模板自動生成。

### 在轉換後編輯自適應表單屬性以啟用DoR生成 {#edit-adaptive-form-properties-to-generate-document-of-record}

1. [運行轉換](../help/convert-existing-forms-to-adaptive-forms.md) 在非互動式PDF窗體上生成自適應窗體。

1. 在 **[!UICONTROL output]** 資料夾和點擊 **[!UICONTROL Properties]**。

1. 在 **[!UICONTROL Form Model]** 的 **[!UICONTROL Document of Record Template Configuration]** 選擇 **[!UICONTROL Generate Document of Record]** 使用預設模板啟用DoR生成。
也可以選擇 **[!UICONTROL Associate form template as the Document of Record template]** 選項，然後選擇該模板以啟用使用源表單模板或任何其他表單模板生成DoR。

1. 點擊 **[!UICONTROL Save & Close]** 按鈕。
