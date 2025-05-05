---
title: 已知問題
description: 自動錶單轉換服務(AFCS)的已知問題和限制
solution: Experience Manager Forms
feature: Adaptive Forms
topic: Administration
topic-tags: introduction
role: Admin, Developer
level: Beginner, Intermediate
exl-id: 35f59e02-e38e-473a-94c8-123e0a85ac8e
source-git-commit: a2472d5a1a66ffada7be485415f50f32643e03fc
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 1%

---

# 已知問題和限制 {#known-issues-limitations}

開始使用AEM Forms自動化表單轉換服務(AFCS)之前，請檢閱下列已知問題和限制：

## 已知問題 {#known-issues}

* 包含轉換表單的資料夾總共不應超過15個表單和50頁。 來源資料夾的大小不應超過10 MB。 請勿在來源資料夾中建立子資料夾。
* 某些表單物件很容易被人看見，但[對於服務](styles-and-pattern-considerations-and-best-practices.md)很難識別。 使用[檢閱並修正編輯器](review-correct-ui-edited.md)來識別並轉換這類表單物件。
* 檢閱並修正編輯器：

   * 沒有復原動作。 「儲存」按鈕會永久儲存變更。
   * 不支援XFA型表單的可重複面板。
   * 如果您使用「稽核並修正」編輯器修改表格中的清單，列寬不會自動調整，且文字可能會溢位至表格的下一列。
   * **[!UICONTROL Auto-detect multi-column layout from input forms]**&#x200B;功能不適用於檢閱和修正編輯器和表單片段。
   * 使用「稽核並修正」編輯器建立的手寫簽名無法載入已發佈的調適型表單。


* 對於XFA型表單：
   * 不支援從XFA型表單擷取片段。
   * 不支援XFA指令碼。 例如，自動為下拉式元件產生值的指令碼。
   * 中繼模型不適用於選擇群組
   * 無法識別含有單一字元的選擇群組選項
   * 當來原始檔是動態XFA (.XDP)，而且它[以最適化表單](https://helpx.adobe.com/tw/experience-manager/6-5/forms/using/xfa-api-supported-in-adaptive-form.html#supportedxfaelementsandtheirmappinginadaptiveformsbr)定義XFA屬性的行為時，將不會遵循來原始檔的存在性屬性。 例如，來原始檔中的欄位標籤為隱藏，且指令碼使欄位可見，則在輸出最適化表單中該欄位保持可見。

* 當您使用&#x200B;**使用輸入AcroForm作為產生的最適化表單的記錄檔案(DoR)**&#x200B;選項時，請考慮下列事項：

<table>
    <tr>
        <td>複合文字欄位的繫結和資料會遺失。 複合文字欄位有多個文字方塊彼此對齊。 例如，在AcroForm中，信用卡號碼會分割成多個文字方塊，而每個文字方塊都有個別的繫結。 當AcroForm轉換為最適化表單時，轉換後的最適化表單具有適用於所有文字方塊的單一繫結。 做為因應措施，在將AcroForm轉換為最適化表單之前，請修改AcroForm以使用單一文字方塊來接受信用卡號碼。</td>
        <td><img  src="assets/creditCard_Composite.png"/>                                                            </td>
    </tr>
    <tr>
        <td>複合日期欄位的繫結和資料遺失。 複合日期欄位由三個不同的欄位組成。 例如，AcroForm中的出生日期欄位會分割成三個個別的欄位。 最適化表單提供立即可用的日期選擇器元件。 若要使用最適化表單的日期選擇器元件同時保留AcroForm的繫結，在將AcroForm轉換為最適化表單之前，請修改AcroForm以使用單一日期欄位。</td>
        <td><img  src="assets/CompositeDateField.png"/></td>
    </tr>
    <tr>
        <td>如果核取方塊的大小大於隨附文字，則不會偵測核取方塊，且AcroForm中的繫結會遺失。 修改AcroForm，使核取方塊的大小小於隨附的文字。</td>
        <td><img  src="assets/large-text-box.png"/><br/><img  src="assets/small-text-box.png"/></td>
    </tr>
    <tr>
        <td>如果輸入欄位未對齊對應的文字欄位，則不會偵測輸入欄位。  </td>
        <td><img  src="assets/non-alingned-fields.png"/></td>
    </tr>
    <tr >
        <td>此服務會將AcroForm的所有核取方塊轉換為個別的選擇群組。 會建立個別的選擇群組以保留與AcroForm的繫結。 請勿在最適化表單中合併選擇群組。 這會導致連結遺失。 如果您合併選擇群組，請再次轉換表單以重新取得遺失的繫結。 </td>
        <td></td>
    </tr>
    <tr >
        <td>某些表格的邊界在自動產生的記錄檔案(DoR)中延伸出頁面。 </td>
        <td></td>
    </tr>
</table>

## 限制 {#limitations}

* 不支援具有複雜動態版面的PDF forms、具有虛線外框的欄位或實心欄位。
* 無法識別影像內的影像和文字。 手動將影像新增至轉換後的表單。
* 不支援圖稿XDP檔案。
* 不支援大於15頁的PDF forms。
* 加密的、受密碼保護及安全檔案不會轉換。 執行轉換前，請先移除加密或密碼。
* 不支援複雜表格，例如無框表格、巢狀表格和具有預留位置值的表格。 使用自適應表單編輯器在轉換後新增或修改複雜表格。 僅支援具有空白欄位、適當標題和清除邊界的簡單表格。
* 此服務僅將英文、法文、德文、西班牙文、義大利文和葡萄牙文的表單轉換為最適化表單。 您可以使用[AEM翻譯工作流程](https://helpx.adobe.com/tw/experience-manager/6-5/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.html)將轉換後的適用性表單翻譯成其他語言。
* AEM 6.4 Forms不支援自動偵測輸入表單的多欄配置。
* 使用來源PDF表單中的顏色編碼的資訊未轉存至最適化表單。
* 來源PDF表單的顏色未延續至最適化表單主題。
* 彩色PDF forms會被視為灰階表單，而系統也會據此偵測欄位。
* 資料繫結或資料模型結構描述等屬性無法用於核心元件型最適化表單。
* 檢閱並修正核心元件式表單無法使用轉換後的表單。
