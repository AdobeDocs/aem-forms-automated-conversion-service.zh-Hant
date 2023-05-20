---
title: 最佳實務和考量
seo-title: Best practices and considerations
description: automated forms conversion服務的最佳做法和注意事項
seo-description: List of styles and patterns in source PDF forms which Automated Forms Conversion service finds difficult to identify
uuid: e24773a2-be14-4184-a168-48aa976d459a
topic-tags: introduction
discoiquuid: 79f2026e-73a5-4bd1-b041-d1399b4ad23e
exl-id: 9ada091a-e7c6-40e9-8196-c568f598fc2a
source-git-commit: 47261710e6616c27c210ac53bffcc2387a06ea7a
workflow-type: tm+mt
source-wordcount: '1247'
ht-degree: 3%

---

# 最佳做法和已知的複雜模式 {#Best-practices-and-considerations2}

本文檔提供了管理員、作者和開發人員在使用時可從中獲益的指導和建議 [!DNL Automated Forms Conversion service]。 它討論了從準備源表單到修復複雜模式（需要為自動轉換付出額外努力）的最佳做法。 這些最佳做法共同促進本公司的整體業績和產出 [!DNL Automated Forms Conversion service]。

## 最佳做法

轉換服務將轉換您的PDF formsAEM [!DNL Forms] 實例到自適應窗體。 下面列出的最佳做法可幫助您提高轉換速度和準確性。 此外，這些最佳做法可幫助您節省轉換活動後花費的時間。

### 上載源之前

您可以按需要一次或分階段上載所有PDF forms。 在上傳表單前，請參閱以下提醒：

* 將資料夾中的表單數保留為小於15，並將資料夾中的總頁數保留為小於50。
* 將資料夾大小保持在10 MB以下。 不要將表單放在子資料夾中。 
* 將頁數保持在小於15的形式下。
* 將源文檔組織為一組8-15個文檔。 將具有通用自適應表單片段的源表單保留在單個批中。
* 不要上載受保護的表單。 該服務不轉換受密碼保護和安全的表單。
* 不上載 [PDFPortfolio](https://helpx.adobe.com/acrobat/using/overview-pdf-portfolios.html)。 該服務不會將PDFPortfolio轉換為自適應格式。
* 不要上載檔案名中帶空格的源表單。 在上載表單之前，從檔案名中刪除空間。
* 不要上載掃描、填寫和表單，而不是使用英語、法語、德語、西班牙語、義大利語和葡萄牙語。 此服務不支援這些表單。

使用XDP表單進行轉換時，請在上載源XPD表單之前執行以下步驟：

* 分析XDP表單並修復可視問題。 確保源文檔使用預期的控制項和結構。 例如，源表單可以具有複選框，而不是單個選區的單選按鈕。 將複選框更改為單選按鈕以生成具有預期元件的自適應表單。
* [將綁定添加到XDP窗體](http://www.adobe.com/go/learn_aemforms_designer_65_tw) 開始轉換。 當綁定在源XDP表單中可用時，服務會在轉換期間自動將綁定應用到相應的自適應表單欄位。 它為您節省了手動應用綁定所需的時間。
* [添加Adobe Sign標籤](https://helpx.adobe.com/sign/using/text-tag.html) 到XDP檔案。 該服務自動將Adobe Sign標籤轉換為相應的自適應表單域。 適應性Forms支援有限數量的Adobe Sign領域。 有關支援欄位的完整清單，請參見 [以自適應形式使用Adobe Sign](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/working-with-adobe-sign.html?lang=en) 文檔。
* 如果可能，將XDP文檔中的複雜表轉換為簡單表。 表格單元格中包含表單域、大小不均勻的單元格、行或列跨越的單元格、合併的單元格、部分邊框或沒有可見邊框的表被視為一個複雜表。 包含上述任何一項的表被視為複雜表。
<!-- * Use sub-forms in XDP documents to create panels in adaptive forms. Service converts each sub-form to one or more adaptive form panels during conversion. -->

### 開始轉換之前

* 建立自適應表單模板。 模板有助於為組織或部門的表單指定統一的結構。
* 在自適應表單模板中指定頁眉和頁腳。 該服務忽略源文檔的頁眉 — 頁腳，並使用自適應表單模板中指定的頁眉 — 頁腳。
* 建立自適應窗體主題。 主題有助於為您的組織或部門的形式提供統一的外觀和感覺。
* 配置表單資料模型以保存資料源並從中檢索。 為表單資料模型建立和配置讀和寫服務。
* 建立自適應表單片段並配置服務以使用自適應表單片段。
* 為需要業務流程自動化的表單準備通用工作流模型。
* 配置Adobe Analytics（如果需要）


## 瞭解複雜模式

AEM [!DNL Forms Automated Conversion service] 使用人工智慧和機器學習算法來理解源表單的佈局和欄位。 每個機器學習服務都不斷從源資料中學習，並在每次混亂中產生改進的輸出。 這些服務從人類經驗中學習。

[!DNL Automated Forms Conversion service] 是用一系列形式訓練的。 它可輕鬆識別源表單中的欄位並生成自適應表單。 但是，PDF forms中也有一些領域和風格，它們很容易被人們看到，但很難為服務理解。 該服務可以將不同於適用欄位類型或面板的欄位或樣式分配給某些欄位或樣式。 下面列出了所有此類欄位和樣式模式。

當服務不斷從源資料中學習時，它將開始識別並為這些模式分配正確的欄位或面板。 目前，你可以 [審閱並更正](review-correct-ui-edited.md) 編輯器來解決這些問題。 在開始解決問題或進一步閱讀之前，請熟悉 [自適應表單元件](https://helpx.adobe.com/experience-manager/6-5/forms/using/introduction-forms-authoring.html)。

### 一般模式 {#general}

| 模式 | 範例 |
|--- |--- |
| **圖案** <br>服務不會將填充的PDF forms轉換為自適應表單。 <br><br>**解決** <br>使用空的自適應表單。 | ![填充窗體](assets/best-practice-filled-forms.png) |
| **圖案** <br>服務無法識別密集表單中的文本和欄位。 <br><br>**解決** <br> 在開始轉換之前，增加密集表單的文本和欄位之間的寬度。 |  |
| **圖案** <br>服務不支援掃描的表單。 <br><br>**解決** <br>不要使用掃描的表單。 | ![掃描的表單](assets/scanned-forms.png) |
| **圖案** <br>服務不提取影像內的影像和文本。 <br><br>**解決** <br> 手動將影像或文本添加到已轉換的表單。 | ![帶文本窗體的影像](assets/best-practice-image-with-text.png) |
| **圖案** <br>帶點線或非清除邊界和邊框的表不會轉換。 <br><br>**解決** <br>使用具有明確顯式邊界和邊框的表。 支援。 | ![非清除表格](assets/best-practice-table-dotted-non-clear.png) |
| **圖案** <br> 自適應表單不支援框外的垂直文本。 因此，服務不會將垂直文本轉換為相應的自適應Forms文本。 <br><br>**解決** <br> 如果需要，可使用自適應表單編輯器添加垂直文本。 | ![非清除表格](assets/vertical-text.png) |



### 選擇組  {#choice-group}

| 模式 | 解析度 |
|--- |--- |
| **圖案** <br> 不會將形狀為框或圓以外的選項組選項轉換為相應的自適應窗體元件。 <br><br>**解決** <br> 將選擇選項形狀更改為框或圓，或使用「審閱」和「正確」編輯器來標識形狀。 | ![選擇欄位 ](assets/best-practice-choice-group-options.png) |

### 表單域 {#form-fields}

| 模式 | 解析度 |
|--- |--- |
| **圖案** <br> 服務不標識沒有清除邊框的欄位。 <br><br>**解決** <br> 使用「審閱」(Review)和「正確」(Correct)編輯器來標識此類欄位。 | ![具有非清除邊界的欄位](assets/best-practice-fields-without-clear-borders.png) |
| **圖案** <br> 服務可能無法識別某些選擇組表單域的底部或右側帶有標題。 <br><br>**解決** <br> 使用「審閱」和「正確」編輯器來標識此類欄位 | ![選擇欄位](assets/best-practice-caption-bottom-right.png) |
| **圖案** <br> 服務會將錯誤類型合併或分配給彼此非常靠近或沒有明確邊框的某些表單域。 <br><br>**解決** <br> 使用「審閱」(Review)和「正確」(Correct)編輯器來標識此類欄位。 | ![選擇欄位](assets/best-practice-placed-very-near.png) |
| **圖案** <br> 服務無法識別帶有遠離字幕或字幕和輸入欄位之間的虛線的欄位。 <br><br>**解決** <br> 使用具有明確邊界的表單域或使用「審閱」和「更正」編輯器修復此類問題。 | ![字幕欄位之間的遠離欄位或虛線](assets/best-practice-far-away-captions-or-a-dotted-line.png) |

### 清單 {#lists}

| 模式 | 解析度 |
|--- |--- |
| **圖案** <br>包含表單域的清單被合併或未轉換為相應的自適應表單元件 <br><br>**解決** <br>使用具有明確邊界的表單域或使用「審閱」和「更正」編輯器修復此類問題。 | ![清單包含選擇組](assets/best-practice-lists-containing-form-fields.png) |
| **圖案** <br>服務可以保留幾個未標識的嵌套清單 <br><br>**解決** <br> 使用「審閱」(Review)和「正確」(Correct)編輯器修復此類問題。 | ![清單包含選擇組](assets/best-practice-nested-lists.png) |
| **圖案** <br> 服務將包含選擇組的某些清單彼此合併 <br><br>**解決** <br> 使用「審閱」(Review)和「正確」(Correct)編輯器修復此類問題。 | ![清單包含選擇組](assets/best-practice-check-box-in-table-cells.png) |

<!--
Comment Type: draft

<h3>Choice groups</h3>
-->

<!--
Comment Type: draft

<ul>
<li>Lists with form fields, nested lists, and nested choice groups are not supported.</li>
<li>Form fields with captions at bottom or right are not supported.</li>
<li>Form fields without borders are not supported.</li>
<li>Hidden form fields are not supported.</li>
<li>Button in PDF forms are not converted to adaptive form buttons.<br /> </li>
<li>Tables with clear explicit boundaries and borders are supported.</li>
<li>Fields with far away captions are not supported.<br /> </li>
<li>Choice groups with only box or circle shaped selectors are supported. </li>
</ul>
-->
