---
title: 已知問題
seo-title: Known Issues
description: automated forms conversion服務的已知問題和限制
seo-description: Before you begin using AEM Forms Automated Forms Conversion service, learn about the known issues and limitations of the service
uuid: b1dc661b-ccd3-457f-acbb-4bd25db86e1e
topic-tags: introduction
discoiquuid: 9cd2363c-47a0-46e9-98cd-1fe088b9cd6e
exl-id: 35f59e02-e38e-473a-94c8-123e0a85ac8e
source-git-commit: 47261710e6616c27c210ac53bffcc2387a06ea7a
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 1%

---

# 已知問題和限制 {#known-issues-limitations}

開始使用AEM FormsAutomated forms conversion服務前，請先檢閱下列已知問題和限制：

## 已知問題 {#known-issues}

* 包含要轉換的表單的資料夾總數不應超過15個表單和50頁。 源資料夾的大小不應超過10 MB。 請勿在來源資料夾中建立子資料夾。
* 有些表單對象很容易在人眼中看到，但是[難以識別服務](styles-and-pattern-considerations-and-best-practices.md)。 使用[查看並更正編輯器](review-correct-ui-edited.md)來標識和轉換此類表單對象。
* 檢閱和修正編輯器：

   * 沒有還原動作。 「保存」按鈕將永久保存更改。
   * 不支援XFA型表單的可重複面板。
   * 如果使用「審閱和更正」編輯器修改表中的清單，行寬不會自動調整，文本可能會溢出到表的下一行。
   * **[!UICONTROL Auto-detect multi-column layout from input forms]**&#x200B;功能無法搭配「檢閱」和「修正」編輯器和表單片段使用。
   * 使用檢閱和修正編輯器建立的手寫簽名無法載入已發佈的適用性表單。


* 針對XFA型表單：
   * 不支援從XFA型表單擷取片段。
   * 不支援XFA指令碼。 例如，用於自動產生下拉式元件值的指令碼。
   * 元模型對選擇組無效
   * 未識別單一字元的「選擇組」選項
   * 如果源文檔是動態XFA(.XDP)，並且它[以自適應形式](https://helpx.adobe.com/experience-manager/6-5/forms/using/xfa-api-supported-in-adaptive-form.html#supportedxfaelementsandtheirmappinginadaptiveformsbr)定義XFA屬性的行為，則源文檔的存在屬性不遵守。 例如，源文檔中的欄位被標籤為隱藏，指令碼使該欄位可見，然後該欄位在輸出最適化表單中保持可見。

* 使用&#x200B;**為生成的最適化表單使用輸入AcroForm作為記錄文檔(DoR)選項時，請考慮以下事項：**

<table>
    <tr>
        <td>複合文本欄位的綁定和資料丟失。 複合文本欄位有多個文本框彼此對齊。 例如，在AcroForm中，信用卡號被拆分到多個文本框中，每個文本框都有單獨的綁定。 將AcroForm轉換為最適化表單時，轉換的最適化表單具有適用於所有文字方塊的單一系結。 在將AcroForm轉換為最適化表單之前，請修改AcroForm，使用單一文字方塊接受信用卡號碼。</td>
        <td><img  src="assets/creditCard_Composite.png"/>                                                            </td>
    </tr>
    <tr>
        <td>複合日期欄位的系結和資料會遺失。 複合日期欄位由三個不同欄位組成。 例如，AcroForm中的出生日期欄位被拆分為三個獨立欄位。 適用性表單提供現成可用的日期選取器元件。 若要在保留AcroForm綁定的同時使用適用性表單的日期選擇器元件，在將AcroForm轉換為適用性表單之前，請修改AcroForm以使用單一日期欄位。</td>
        <td><img  src="assets/CompositeDateField.png"/></td>
    </tr>
    <tr>
        <td>如果複選框的大小大於隨附的文本，則不會檢測複選框，並且AcroForm中的綁定將丟失。 修改AcroForm以使複選框的大小小於隨附文本。</td>
        <td><img  src="assets/large-text-box.png"/><br/><img  src="assets/small-text-box.png"/></td>
    </tr>
    <tr>
        <td>如果輸入欄位與對應的文字欄位不對齊，則不會偵測輸入欄位。  </td>
        <td><img  src="assets/non-alingned-fields.png"/></td>
    </tr>
    <tr >
        <td>該服務將AcroForm的所有複選框轉換為不同的選擇組。 將建立單獨的選擇組以保留與AcroForm的綁定。 請勿在最適化表單中合併選擇群組。 這將導致綁定丟失。 如果合併選擇組，請再次轉換表單以重新獲得丟失的綁定。 </td>
        <td></td>
    </tr>
    <tr >
        <td>某些表的彈回數在自動生成的記錄文檔(DoR)中從頁面延伸出來。 </td>
        <td></td>
    </tr>
</table>

## 限制 {#limitations}

* 不支援具有複雜動態版面的PDF forms、具有虛線輪廓的欄位或已填欄位。
* 未識別影像內的影像和文字。 手動將影像新增至轉換的表單。
* 不支援圖稿XDP文檔。
* 不支援超過15頁的PDF forms。
* 加密、密碼保護和安全的文檔不會轉換。 在執行轉換之前，請刪除加密或密碼。
* 不支援具有佔位符值的複雜表，如無邊框表、嵌套表和表。 轉換後，使用最適化表單編輯器來新增或修改複雜表格。 僅支援帶有空欄位、適當標題和清除邊界的簡單表。
* 此服務僅將英文、法文、德文、西班牙文、義大利文和葡萄牙文等語言表單轉換為最適化表單。 您可以使用[AEM翻譯工作流程](https://helpx.adobe.com/experience-manager/6-5/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.html)將轉換的最適化表單翻譯成其他語言。
* AEM 6.4 Forms不支援自動偵測輸入表單的多欄版面配置。
* 使用來源PDF表單中的顏色編碼的資訊不會傳遞至最適化表單。
* 來源PDF表單的顏色不會傳遞至最適化表單主題。
* 彩色PDF forms被視為灰度形式，並相應地檢測欄位。
