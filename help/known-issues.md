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

在開始使用AEM FormsAutomated forms conversion服務之前，請查看以下已知問題和限制：

## 已知問題 {#known-issues}

* 包含要轉換的表單的資料夾的表單總數不應超過15個，頁數不應超過50頁。 源資料夾的大小不應超過10 MB。 不要在源資料夾中建立子資料夾。
* 某些形狀的物體很容易被人眼看到，但 [難以識別服務](styles-and-pattern-considerations-and-best-practices.md)。 使用 [審閱並正確編輯器](review-correct-ui-edited.md) 來標識和轉換此類窗體對象。
* 審閱並正確編輯器：

   * 沒有撤消操作。 「保存」按鈕永久保存更改。
   * 不支援基於XFA的表單的可重複面板。
   * 如果使用「審閱」和「正確」編輯器修改表中的清單，行寬不會自動調整，文本可能會溢出到表的下一行。
   * 的 **[!UICONTROL Auto-detect multi-column layout from input forms]** 功能不能與「審閱」和「正確」編輯器和「表單片段」一起使用。
   * 使用「審閱」和「正確」編輯器建立的Scribble簽名無法載入已發佈的自適應表單。


* 對於基於XFA的表單：
   * 不支援從基於XFA的表單中提取片段。
   * 不支援XFA指令碼。 例如，用於自動為下拉元件生成值的指令碼。
   * 元模型不適用於選擇組
   * 未標識單個字元的選擇組選項
   * 當源文檔是動態XFA(.XDP)且它 [定義自適應形式中XFA屬性的行為](https://helpx.adobe.com/experience-manager/6-5/forms/using/xfa-api-supported-in-adaptive-form.html#supportedxfaelementsandtheirmappinginadaptiveformsbr)，則源文檔的存在屬性不被尊重。 例如，源文檔中的欄位被標籤為隱藏，指令碼使欄位可見，然後該欄位在輸出自適應窗體中保持可見。

* 使用 **將輸入AcroForm用作記錄文檔(DoR)用於生成的自適應表單** 選項，請考慮以下內容：

<table>
    <tr>
        <td>複合文本欄位的綁定和資料丟失。 複合文本欄位具有多個相互對齊的文本框。 例如，在AcroForm中，信用卡號被拆分為多個文本框，每個文本框都有單獨的綁定。 當AcroForm轉換為自適應表單時，轉換後的自適應表單對所有文本框具有單個綁定。 作為解決方法，在將AcroForm轉換為自適應表單之前，請修改AcroForm以使用單個文本框來接受信用卡號。</td>
        <td><img  src="assets/creditCard_Composite.png"/>                                                            </td>
    </tr>
    <tr>
        <td>組合日期欄位的綁定和資料丟失。 複合日期欄位由三個不同的欄位組成。 例如，AcroForm中的出生日期欄位被拆分為三個單獨的欄位。 自適應表單提供現成日期選取器元件。 要在保留AcroForm綁定的同時使用自適應表單的日期選取器元件，在將AcroForm轉換為自適應表單之前，請修改AcroForm以使用單個日期欄位。</td>
        <td><img  src="assets/CompositeDateField.png"/></td>
    </tr>
    <tr>
        <td>如果複選框的大小大於隨附的文本，則不會檢測到複選框，並且AcroForm中的綁定將丟失。 修改AcroForm，使複選框的大小小於隨附的文本。</td>
        <td><img  src="assets/large-text-box.png"/><br/><img  src="assets/small-text-box.png"/></td>
    </tr>
    <tr>
        <td>如果輸入欄位未與相應的文本欄位對齊，則不檢測輸入欄位。  </td>
        <td><img  src="assets/non-alingned-fields.png"/></td>
    </tr>
    <tr >
        <td>該服務將AcroForm的所有複選框轉換為單獨的選擇組。 建立單獨的選擇組以保留與AcroForm的綁定。 不要在自適應窗體中合併選擇組。 將導致綁定丟失。 如果合併choice-groups，請再次轉換表單以重新獲取丟失的綁定。 </td>
        <td></td>
    </tr>
    <tr >
        <td>某些表的邊界在自動生成的記錄文檔(DoR)中從頁面外延伸。 </td>
        <td></td>
    </tr>
</table>

## 限制 {#limitations}

* 不支援具有複雜動態佈局的PDF forms、帶虛線輪廓的欄位或填充欄位。
* 不標識影像內的影像和文本。 手動將影像添加到已轉換的表單。
* 不支援圖稿XDP文檔。
* 不支援大於15頁的PDF forms。
* 加密、受密碼保護和安全文檔不會轉換。 在運行轉換之前，請刪除加密或密碼。
* 不支援複雜表，如無邊距表、嵌套表和具有佔位符值的表。 轉換後，使用自適應表單編輯器添加或修改複雜表。 僅支援帶空欄位、正確標題和清除邊界的簡單表。
* 該服務僅將英語、法語、德語、西班牙語、義大利語和葡萄牙語形式轉換為適應形式。 可以使用 [AEM翻譯工作流](https://helpx.adobe.com/experience-manager/6-5/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.html)。
* 6AEM.4Forms不支援多列輸入表格佈局的自動檢測。
* 使用源PDF形式中的顏色編碼的資訊不會被傳送到自適應形式。
* 源PDF窗體的顏色不會傳遞到自適應窗體主題。
* 彩色PDF forms被視為灰度形式並相應地檢測場。
