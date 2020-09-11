---
title: 已知問題
seo-title: 已知問題
description: 自動化表單轉換服務的已知問題和限制
seo-description: 在您開始使用AEM Forms Automated Forms Conversion服務之前，請先瞭解服務的已知問題和限制
uuid: b1dc661b-ccd3-457f-acbb-4bd25db86e1e
topic-tags: introduction
discoiquuid: 9cd2363c-47a0-46e9-98cd-1fe088b9cd6e
translation-type: tm+mt
source-git-commit: e2298422e0af9b1c678e7604be3efb6da377d7dd
workflow-type: tm+mt
source-wordcount: '768'
ht-degree: 1%

---

# 已知問題和限制 {#known-issues-limitations}

在您開始使用AEM Forms Automated Forms Conversion服務之前，請先檢閱下列已知問題和限制：

## 已知問題 {#known-issues}

* 包含要轉換的表單的資料夾，總共不應超過15個表單和50個頁面。 來源資料夾的大小不應超過10 MB。 請勿在來源檔案夾中建立子檔案夾。
* 有些表單物件在人眼中很容易看見，但 [在服務上卻很難識別](styles-and-pattern-considerations-and-best-practices.md)。 使用 [「檢閱」和正確的編輯器](review-correct-ui-edited.md) ，以識別和轉換此類表格物件。
* 檢閱和修正編輯器：

   * 沒有還原動作。 「儲存」按鈕會永久儲存變更。
   * 不支援XFA表單的可重複面板。
   * 如果您使用「檢閱與更正」編輯器修改表格中的清單，列寬不會自動調整，而文字可能會溢出至表格的下一行。
   * 此功 **[!UICONTROL Auto-detect multi-column layout from input forms]** 能無法與「檢閱」和「更正」編輯器和「表單片段」搭配使用。
   * 使用「檢閱」和「更正」編輯器建立的塗鴉簽名無法載入已發佈的最適化表單。


* 針對XFA型表單：
   * 不支援從以XFA為基礎的表單擷取片段。
   * 不支援XFA指令碼。 例如，用於自動生成下拉清單元件值的指令碼。
   * 元模型不適用於選擇群組
   * 單一字元的「選擇群組」選項無法識別
   * 如果源文檔是動態XFA(.XDP)，並且它以自適應形式定義 [XFA屬性的行為](https://helpx.adobe.com/experience-manager/6-5/forms/using/xfa-api-supported-in-adaptive-form.html#supportedxfaelementsandtheirmappinginadaptiveformsbr)，則源文檔的存在屬性將不被接受。 例如，源文檔中的欄位被標籤為隱藏，指令碼使該欄位可見，然後該欄位在輸出自適應表單中保持可見。

* 當您使用「將輸 **入的AcroForm用作記錄文檔(DoR)」選項來生成自適應表單** ，請考慮以下事項：

<table>
    <tr>
        <td>複合文字欄位的系結和資料會遺失。 複合文本欄位具有多個相互對齊的文本框。 例如，在AcroForm中，信用卡號碼會分割成多個文字方塊，而每個文字方塊都有個別的系結。 當AcroForm轉換為最適化表單時，轉換的最適化表單對所有文字方塊都有單一系結。 因應措施是，在將AcroForm轉換為最適化表單之前，請修改AcroForm，使用單一文字方塊來接受信用卡號碼。</td>
        <td><img  src="assets/creditCard_Composite.png"/>                                                            </td>
    </tr>
    <tr>
        <td>複合日期欄位的系結和資料會遺失。 複合日期欄位由三個不同欄位組成。 例如，AcroForm中的出生日期欄位被分為三個獨立欄位。 最適化表單提供現成可用的日期選擇器元件。 若要在保留AcroForm綁定的同時使用最適化表單的日期選擇器元件，請在將AcroForm轉換為最適化表單之前，將AcroForm修改為使用單一日期欄位。</td>
        <td><img  src="assets/CompositeDateField.png"/></td>
    </tr>
    <tr>
        <td>如果核取方塊的大小大於隨附的文字，則不會偵測到核取方塊，而且AcroForm中的系結會遺失。 修改AcroForm，使核取方塊的大小小於隨附的文字。</td>
        <td><img  src="assets/large-text-box.png"/><br/><img  src="assets/small-text-box.png"/></td>
    </tr>
    <tr>
        <td>如果輸入欄位與相應的文本欄位不對齊，則不檢測輸入欄位。  </td>
        <td><img  src="assets/non-alingned-fields.png"/></td>
    </tr>
    <tr >
        <td>該服務將AcroForm的所有複選框轉換為單獨的選擇組。 會建立個別的選擇群組，以保留與AcroForm的系結。 不要在最適化表單中合併選擇群組。 這會導致系結遺失。 如果您合併選擇群組，請再次轉換表單以重新獲得遺失的系結。 </td>
        <td></td>
    </tr>
    <tr >
        <td>在自動生成的記錄文檔(DoR)中，某些表的邊界從頁面延伸出。 </td>
        <td></td>
    </tr>
</table>

## 限制 {#limitations}

* 不支援具有複雜動態版面的PDF表格、具有虛線輪廓的欄位或填入欄位。
* 影像中的影像和文字無法識別。 手動將影像新增至轉換的表單。
* 不支援圖稿XDP檔案。
* 不支援超過15頁的PDF表格。
* 加密、受密碼保護和安全的檔案不會轉換。 在執行轉換之前，請先移除加密或密碼。
* 不支援複雜的表格，例如無邊框表格、巢狀表格和具有預留位置值的表格。 在轉換後，使用最適化表單編輯器來新增或修改複雜的表格。 僅支援包含空白欄位、正確標題和清除邊界的簡單表格。
* 該服務僅將英語表單轉換為自適應表單。 You can translate converted adaptive forms to another language using [AEM translation workflow](https://helpx.adobe.com/experience-manager/6-5/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.html).
* AEM 6.4 Forms不支援自動偵測多欄版面輸入表單。

