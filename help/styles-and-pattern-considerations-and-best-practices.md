---
title: '最佳實務和考量 '
seo-title: '最佳實務和考量 '
description: 自動化表單轉換服務的最佳做法和注意事項
seo-description: 自動化表單轉換服務發現難以識別的來源PDF表單樣式和樣式清單
uuid: e24773a2-be14-4184-a168-48aa976d459a
topic-tags: introduction
discoiquuid: 79f2026e-73a5-4bd1-b041-d1399b4ad23e
translation-type: tm+mt
source-git-commit: a5d663c2a59895eb71eb5287586bc6b3862927fc

---


# 最佳實踐和已知的複雜模式 {#Best-practices-and-considerations2}

本檔案提供管理員、作者和開發人員在使用自動表單轉換服務時可從中獲益的准則和建議。 它討論從準備來源表單到修正複雜模式（需要額外努力以自動化轉換）的最佳實務。 這些最佳實務可共同協助自動化表單轉換服務的整體效能與輸出。

## 最佳實務

轉換服務會將AEM Forms例項上可用的PDF表單轉換為最適化表單。 下列最佳實務可協助您提高轉換速度和準確性。 此外，這些最佳實務可協助您節省轉換活動後花費的時間。

### 上傳來源之前

您可以視需要一次或分階段上傳所有PDF表格。 在上傳表單前，請參閱以下提醒：

* 將資料夾中的表單數保持在小於15，並將資料夾中的頁數總數保持在小於50。
* 將檔案夾大小保持在10 MB以下。 請勿將表單保留在子資料夾中。
* 將頁數保持在小於15的形式中。
* 將來源檔案整理成8-15份檔案。 在單一批次中使用通用的最適化表單片段來保留來源表單。
* 請勿上傳受保護的表單。 該服務不會轉換受密碼保護和安全的表單。
* Do not upload the [PDF Portfolios](https://helpx.adobe.com/acrobat/using/overview-pdf-portfolios.html). 本服務不會將PDF資料夾轉換為最適化表單。
* 請勿上傳掃描、彩色、非英文和填寫的表格。 此服務不支援這些表單。
* 請勿上傳檔案名稱中含空格的來源表單。 在上傳表單之前，先從檔案名稱中移除空格。

當您使用XDP表單進行轉換時，請先執行下列步驟，再上傳來源XPD表單：

* 分析XDP表單並修正視覺問題。 確保來源檔案使用預期的控制項和結構。 例如，源表單中可以有複選框，而不是單選選項的單選按鈕。 將核取方塊變更為選項按鈕，以產生具有預期元件的最適化表單。
* [開始轉換前，先將系結新增至XDP](http://www.adobe.com/go/learn_aemforms_designer_65) 表單。 當源XDP表單中有綁定可用時，服務會在轉換期間自動將綁定應用到相應的自適應表單域。 它可為您節省手動套用系結所需的時間。
* [將Adobe Sign標籤新增至](https://helpx.adobe.com/sign/using/text-tag.html) XDP檔案。 服務會自動將Adobe Sign標籤轉換為對應的最適化表單欄位。 Adaptive Forms支援有限數目的Adobe Sign欄位。 如需支援欄位的完整清單，請參 [閱在最適化表單檔案中使用Adobe Sign](https://docs.adobe.com/content/help/en/experience-manager-65/forms/adaptive-forms-advanced-authoring/working-with-adobe-sign.html) 。
* 在XDP檔案中使用子表單，以最適化表單建立面板。 服務在轉換期間將每個子表單轉換為自適應表單面板。
* 盡可能將XDP檔案中的複雜表轉換為簡單表。 表格單元格中包含表格欄位、大小不均勻的單元格、行或列跨越的單元格、合併的單元格、部分邊框或沒有可見邊框的表格被視為複雜表格。 具有上述任一項的表被視為複雜表。

### 開始轉換前

* 建立最適化表單範本。 範本可協助您為組織或部門的表單指定統一的結構。
* 在最適化表單範本中指定頁首和頁尾。 服務忽略源文檔的頁眉——頁腳，並使用在自適應表單模板中指定的頁眉——頁腳。
* 建立最適化表單主題。 主題可協助您為組織或部門的表單提供統一的外觀和感覺。
* 設定表單資料模型以儲存並擷取資料來源。 為表單資料模型建立和設定讀取和寫入服務。
* 建立最適化表單片段並設定服務以使用您的最適化表單片段。
* 針對需要商業程式自動化的表單，準備常用的工作流程模型。
* 視需要設定Adobe Analytics


## 瞭解複雜圖樣

AEM Forms Automated Conversion服務使用人工智慧和機器學習演算法來瞭解來源表單的版面配置和欄位。 每項機器學習服務都會持續從來源資料中學習，並在每次流失時產生改善的輸出。 這些服務從人類的體驗中學習。

自動化表單轉換服務是針對大量表單進行培訓的。 它可輕鬆識別來源表單中的欄位，並產生最適化表單。 不過，PDF表格中有些欄位和樣式很容易讓人看得到，但是卻很難為服務瞭解。 服務可指派不同於適用欄位類型或面板給某些欄位或樣式。 以下列出所有此類欄位和樣式模式。

服務會開始識別並指派正確的欄位或面板給這些模式，因為它會不斷從來源資料中學習。 目前，您可以使用「檢閱」 [和「更正」編輯器](review-correct-ui-edited.md) ，來修正此類問題。 在開始修正問題或進一步閱讀之前，請先熟悉最適 [化表單元件](https://helpx.adobe.com/experience-manager/6-5/forms/using/introduction-forms-authoring.html)。

### 一般模式 {#general}

| 圖樣 | 範例 |
|--- |--- |
| **Pattern**<br> Service不會將彩色PDF表單轉換為最適化表單。 <br><br>**解析度&#x200B;**<br>：使用黑白或灰階PDF表格。 | ![彩色表格](assets/best-practice-coloured-forms.png) |
| **Pattern** <br>Service不會將填寫的PDF表單轉換為最適化表單。 <br><br>**解析度&#x200B;**<br>使用空的最適化表單。 | ![填寫表單](assets/best-practice-filled-forms.png) |
| **Pattern** <br>Service無法識別密集表單中的文字和欄位。 <br><br>**解析度&#x200B;**<br>—在開始轉換之前，增加密集表單的文字和欄位之間的寬度。 |  |
| **Pattern** <br>Service不支援掃描的表單。 <br><br>**解析度&#x200B;**<br>請勿使用掃描的表單。 | ![掃描的表單](assets/scanned-forms.png) |
| **Pattern** <br>Service不會擷取影像和影像中的文字。 <br><br>**解析度&#x200B;**<br>：手動將影像或文字新增至轉換的表單。 | ![包含文字表單的影像](assets/best-practice-image-with-text.png) |
| **具有**<br>點狀或非清除邊界和邊界的陣清單不進行轉換。 <br><br>**解析度&#x200B;**(<br>Resolution)使用具有明確邊界和邊界的表。 支援。 | ![非清除表格表單](assets/best-practice-table-dotted-non-clear.png) |
| **「圖樣**<br> 」最適化表單不支援立即可用的垂直文字。 因此，服務不會將垂直文字轉換為對應的Adaptive Forms文字。 <br><br>**解析度&#x200B;**(<br>Resolution)視需要使用最適化表單編輯器來新增垂直文字。 | ![非清除表格表單](assets/vertical-text.png) |



### Choice Group {#choice-group}

| 圖樣 | 解析度 |
|--- |--- |
| **「陣列選** 擇」(Pattern <br> Choice)組選項中除框或圓形外的形狀不會轉換為相應的自適應表單元件。 <br><br>**解析度&#x200B;**<br>：將選擇的形狀選項變更為方塊或圓形，或使用「檢閱與修正」編輯器來識別形狀。 | ![選擇欄位 ](assets/best-practice-choice-group-options.png) |

### 表單欄位 {#form-fields}

| 圖樣 | 解析度 |
|--- |--- |
| **模式**<br> 服務不會識別沒有明確邊界的欄位。 <br><br>**解析度&#x200B;**<br>：使用「檢閱」和「修正」編輯器來識別這些欄位。 | ![具有非清晰邊界的欄位](assets/best-practice-fields-without-clear-borders.png) |
| **Pattern**<br> Service可能無法識別表單底部或右側有標題的某些選擇群組表單欄位。 <br><br>**解析度&#x200B;**<br>：使用「審閱」和「更正」編輯器來識別這些欄位 | ![選擇欄位](assets/best-practice-caption-bottom-right.png) |
| **Pattern**<br> Service會將錯誤的類型合併或指定給彼此相距甚遠或邊界不明確的某些表單域。 <br><br>**解析度&#x200B;**<br>：使用「檢閱」和「修正」編輯器來識別這些欄位。 | ![選擇欄位](assets/best-practice-placed-very-near.png) |
| **Pattern**<br> Service可能無法識別字幕遠離或字幕與輸入欄位間虛線的欄位。 <br><br>**解決方&#x200B;**<br>法：使用邊界明確的表單欄位，或使用「檢閱與修正」編輯器來修正此類問題。 | ![字幕欄位之間的遠離欄位或虛線](assets/best-practice-far-away-captions-or-a-dotted-line.png) |

### 清單 {#lists}

| 圖樣 | 解析度 |
|--- |--- |
| **包含表**<br><br><br>****<br>單欄位的模式清單將合併或不轉換為相應的自適應表單元件解析度使用具有清晰邊界的表單欄位，或使用「查看」和「更正」編輯器來修復此類問題。 | ![清單包含選擇組](assets/best-practice-lists-containing-form-fields.png) |
| **Pattern** <br>Service可讓數個巢狀清單保留未識別的「解析度」( <br><br>**Resolution **)「使用檢閱<br>」(Use Review)和「更正」(Correct)編輯器來修正此類問題。 | ![清單包含選擇組](assets/best-practice-nested-lists.png) |
| **Pattern**<br> Service會合併某些包含選擇群組的清單，以相互 <br><br>**解析&#x200B;**<br>「使用檢閱和更正」編輯器來修正此類問題。 | ![清單包含選擇組](assets/best-practice-check-box-in-table-cells.png) |

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
