---
title: 在轉換期間產生記錄檔案
seo-title: 在轉換期間產生記錄檔案
description: 建議的路徑，以根據用於轉換的來源表單類型產生DoR。
seo-description: 建議的路徑，以根據用於轉換的來源表單類型產生DoR。
page-status-flag: never-activated
uuid: 7f0f5bf3-21be-449a-b23e-5946a9fd7ed4
contentOwner: khsingh
discoiquuid: 75f6e6bc-7636-4b40-919c-8b20a6ccbb1f
translation-type: tm+mt
source-git-commit: 640d72d7961ef0c2393bf0ae6745d918e388a056

---


# 建議的工作流程，可針對最適化表單產生記錄檔案 {#recommended-workflows-dor-generation}

記錄檔案(DoR)可讓您保留您提供的資訊記錄，並以最適化的形式提交，以便您稍後參考。
DoR使用基本範本來定義其版面。 您可以使用預設模板生成DoR，或將任何其他模板與最適化表單關聯。

![生成的記錄文檔](assets/document_of_record.gif)

有關生成DoR的詳細資訊，請參 [閱生成適應性表單的記錄文檔](https://helpx.adobe.com/experience-manager/6-5/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.html)。

Automated Forms [Conversion服務可將下列來源表單](../help/introduction.md) ，轉換為最適化表單：

* 非互動式PDF表格
* Acro Forms
* 以XFA為基礎的PDF表單

根據您用於轉換的來源表單，您可以使用下列方式產生DoR:

* 預設範本
* 源表單作為模板——如果選擇此選項，轉換服務會自動將源表單與已轉換的最適化表單關聯為DoR模板。
* 將任何其他模板與已轉換的最適化表單關聯

下表說明您使用的DoR範本如何影響所產生DoR的版面配置：

<table> 
 <tbody>
 <tr>
  <td><p><strong>來源表單</strong></p></td>
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

如表格中所示，如果您使用來源表單做為範本，DoR會保留來源表單的版面配置。
本文說明根據三種來源表單類型產生DoR的建議路徑。

<table> 
 <tbody> 
  <tr> 
   <th><strong>來源表單</strong></th> 
   <th><strong>生成DoR的方法</strong></th> 
  </tr> 
  <tr> 
   <td><p>非互動式PDF表格</p></td> 
   <td> 
    <ul> 
     <li><a href="#generate-document-of-record-using-cloud-configuration">在最適化表單轉換前啟用DoR產生，以使用預設範本產生DoR</a></li> 
     <li><a href="#edit-adaptive-form-properties-generate-document-of-record">在最適化表單轉換後編輯最適化表單屬性，以啟用使用預設或其他表單範本產生DoR</a></li> 
    </ul> </td> 
  </tr>
  <tr> 
   <td><p>Acro Forms或XFA架構的PDF表單</p></td> 
   <td> 
    <ul> 
     <li><a href="#use-input-form-as-template-to-generate-document-of-record">在最適化表單轉換前啟用DoR產生，以來源表單為範本產生DoR</a></li> 
     <li><a href="#edit-adaptive-form-properties-to-generate-document-of-record">在最適化表單轉換後編輯最適化表單屬性，以啟用使用預設範本、來源表單作為範本或任何其他表單範本產生DoR</a></li> 
    </ul> </td> 
  </tr>    
 </tbody> 
</table>

## 為非互動式PDF表單產生記錄檔案 {#generate-document-of-record-non-interactive-pdf}

如果您使用非互動式PDF表單做為「自動化表單轉換」服務的來源表單，您可以：

* 在最適化表單轉換前啟用DoR產生，以使用預設範本產生DoR
* 或在最適化表單轉換後編輯最適化表單屬性，以啟用使用預設或其他表單範本產生DoR

### 在轉換前啟用DoR產生，以使用預設範本產生DoR {#generate-document-of-record-using-cloud-configuration}

1. 選擇 **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Automated Forms Conversion Configuration]** >用於轉換的雲端設定屬性> **[!UICONTROL Advanced]** >選 **[!UICONTROL Generate Document of Record]** 項。

   ![使用雲端設定產生記錄檔案](assets/generate_dor_cloud_config.gif)

1. 點選 **[!UICONTROL Save & Close]** 以儲存設定。

1. [執行轉換](../help/convert-existing-forms-to-adaptive-forms.md)。 請確定您使用在這些指示步驟1中編輯的雲端設定。
提交已轉換的最適化表單時，DoR會使用預設範本自動產生。

### 在轉換後編輯最適化表單屬性，以啟用DoR產生 {#edit-adaptive-form-properties-generate-document-of-record}

如果在將源表單轉換為自適應表單之前未啟用DoR生成，則在轉換後仍可啟用。

1. [在非互動](../help/convert-existing-forms-to-adaptive-forms.md) PDF表單上執行轉換，以產生最適化表單。

1. 在資料夾中選取最適化表 **[!UICONTROL output]** 單，然後點選 **[!UICONTROL Properties]**。

1. 在頁籤 **[!UICONTROL Form Model]** 中，展開該部 **[!UICONTROL Document of Record Template Configuration]** 分並選擇 **[!UICONTROL Generate Document of Record]**。

   ![產生記錄文件](assets/generate_dor_af_properties.png)

1. 點選 **[!UICONTROL Save & Close]** 以儲存設定。

提交已轉換的最適化表單時，DoR會使用預設範本自動產生。 如果要將任何其它DoR模板與已轉換的最適化表單關聯，可以選擇 **[!UICONTROL Associate form template as the Document of Record template]** 選項。

## 為Acro表單或以XFA為基礎的PDF表單產生記錄檔案 {#generate-document-of-record-acroform-xfaform}

如果您使用Acro Form或XFA架構的PDF表單做為自動表單轉換服務的來源表單，您可以：

* 在最適化表單轉換前啟用DoR產生，以使用來源表單做為範本

* 或在最適化表單轉換後編輯最適化表單屬性，以啟用使用預設範本、來源表單作為範本或任何其他表單範本產生DoR

### 在轉換前啟用DoR生成，以使用源表單模板生成DoR {#use-input-form-as-template-to-generate-document-of-record}

1. 選擇 **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Automated Forms Conversion Configuration]** >用於轉換的雲端設定屬性> **[!UICONTROL Advanced]** >選 **[!UICONTROL Generate Document of Record]** 項。

1. 點選 **[!UICONTROL Save & Close]** 以儲存設定。

1. [執行轉換](../help/convert-existing-forms-to-adaptive-forms.md)。 請確定您使用在這些指示步驟1中編輯的雲端設定。
轉換服務會自動將Acro表單或XFA架構的PDF表單與轉換的最適化表單建立關聯，做為DoR範本。
您可以開啟最適化表單屬性，在標籤的區段中檢 **[!UICONTROL Document of Record Template Configuration]** 視DoR **[!UICONTROL Form Model]** 範本。

   ![編輯最適化表單屬性以產生記錄檔案](assets/generate_dor_af_properties_xdp_acro.png)

   提交已轉換的最適化表單時，DoR會使用來源表單範本自動產生。

### 在轉換後編輯最適化表單屬性，以啟用DoR產生 {#edit-adaptive-form-properties-to-generate-document-of-record}

1. [在非互動](../help/convert-existing-forms-to-adaptive-forms.md) PDF表單上執行轉換，以產生最適化表單。

1. 在資料夾中選取最適化表 **[!UICONTROL output]** 單，然後點選 **[!UICONTROL Properties]**。

1. 在頁籤 **[!UICONTROL Form Model]** 中，展開該部 **[!UICONTROL Document of Record Template Configuration]** 分並選擇 **[!UICONTROL Generate Document of Record]** 以使用預設模板啟用DoR生成。
您也可以選擇選 **[!UICONTROL Associate form template as the Document of Record template]** 項並選擇模板，以使用源表單模板或任何其它表單模板啟用DoR生成。

1. 點選 **[!UICONTROL Save & Close]** 以儲存設定。
