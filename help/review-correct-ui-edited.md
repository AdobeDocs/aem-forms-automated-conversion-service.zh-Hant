---
title: 檢閱並修正轉換後的表單
seo-title: Review and correct converted forms
description: 查看並更正由Automated forms conversion服務轉換的自適應表單。
seo-description: Review and correct the adaptive forms converted by the Automated Forms Conversion service
uuid: 5a0a6d24-dff6-4732-b607-24848b07b26d
topic-tags: forms
discoiquuid: f45ab2d7-5234-42d6-aeb6-b2cb1a7ce3c2
exl-id: 64330fa2-aa9d-4ba4-96df-b75deed3e693
source-git-commit: 1a3f79925f25dcc7dbe007f6e634f6e3a742bf72
workflow-type: tm+mt
source-wordcount: '2518'
ht-degree: 0%

---

# 檢閱並修正轉換後的表單{#review-and-correct-converted-forms}

AEM FormsAutomated forms conversion服務識別輸入PDF文檔的欄位、內容和佈局，並將PDF文檔轉換為自適應格式。 輸出自適應表單中可能缺少一些欄位或轉換不正確。 可以使用「審閱」(Review)和「正確」(Correct)編輯器對已標識的欄位進行改進，並重新生成自適應表單，使輸出更接近所需的體驗。 第一次轉換後，可以在編輯器中開啟輸入PDF文檔，以：

* 查看轉換過程中標識的所有欄位和內容
* 標識轉換過程中遺漏的欄位和內容
* 驗證欄位的類型並更改其類型（如果需要）
* 驗證已標識的表，調整列大小，並修改單元格內容
* 刪除錯誤標識的欄位

進行所需更改後，將PDF forms重新發送到轉換服務。 成功轉換後，更新的資產（包括自適應表單和模式）將下載到您的AEM Forms實例。 可以重複該過程，直到獲得所需的體驗。 ![](assets/stages-of-form-2.gif)

您需要GoogleChrome、Mozilla FireFox或MicrosoftEdge瀏覽器使用審閱和正確的編輯器。 編輯器不支援Internet Explorer。

## 歡迎使用「審閱」和「正確」編輯器 {#welcome-to-review-and-correct-editor}

「審閱」和「正確」編輯器提供了易於使用的介面。 它具有以下元件：

* 內容瀏覽器：可以使用內容瀏覽器更改元素的位置。 內容瀏覽器允許您拖放表單對象以更改其位置。 例如，在文本框前移動表。 它相應地改變輸出自適應表單的制表順序。
* 屬性瀏覽器：它顯示選定欄位的屬性。 也可以修改屬性。
* 工具欄：工具欄位於編輯器頂部。 它顯示添加、修改、分組、取消分組和刪除欄位的工具。
* 開啟屬性：點擊「Open properties（開啟屬性）」選項時，將顯示 ![](assets/properties.png) 表徵圖 可以按一下開啟屬性以開啟窗體屬性並查看其他選項。
* 「篩選」按鈕：篩選器按鈕 ![](assets/toggle_eye.png) 在編輯器的頂部。 它允許您篩選欄位以僅顯示文本、欄位、選擇組、面板或所有元件。
* 「保存」按鈕：的 **[!UICONTROL Save]** 按鈕。 您還可以使用「保存」按鈕旁的箭頭查看用於發送表單以進行轉換的選項。

* PDF窗體：編輯器將顯示源PDF文檔，並將其與標識的欄位重疊。 可以使用工具欄中的工具修改欄位。
* 頁面：源窗體可以具有多個頁面。 編輯器在右上角提供一個按鈕，用於在頁面之間導航。

![審閱並更正UI](assets/reviewcorrectui.png)

**答：** 內容瀏覽器 **B** 屬性瀏覽器 **C.** 工具欄 **D** 「屬性」按鈕 **E.** 「篩選」按鈕 **F.** 「保存」按鈕 **G.** PDF表單與已標識欄位重疊

在第一次成功轉換之後，轉換服務將源PDF文檔與已標識的欄位和元件重疊。 這些欄位或元件的類型為：文本、欄位、面板、選擇組和表：

* 文本：源PDF文檔中的純文字檔案。 例如，上面顯示的影像中的「貸款應用程式」文本。
* 欄位：與值或輸入框關聯的文本或表徵圖標籤的組合。 例如，上圖中的第一個欄位名。 它有文本標籤和一個輸入框。 欄位支援文本、數字、下拉清單、日期、電子郵件、電話號碼、簽名、貨幣和密碼資料類型。
* 面板：內容和元件的邏輯集合。 例如，上圖中的「人員1」和「人員2」面板的「個人詳細資訊」。
* 選擇組：與多個選項關聯的文本組合：按鈕。 例如，上圖中的「婚姻狀態」和「現有客戶」。\
   轉換服務基於選擇組標題及其多選選項，自動將選擇組轉換為單選單選按鈕或多選複選框。 例如，如果 **選擇任意一個** 由於選擇組標題或多選項選項允許您只選擇一個選項， **是** 或 **否**，轉換服務將選擇組自動轉換為單選單選按鈕。 同樣，如果 **選擇所有適用項** 或 **選擇多個** 由於選擇組標題或多選項選項允許您選擇多個選項，因此轉換服務會自動將選擇組轉換為多選複選框。

* 表：包含以列和行表示的資訊的二維表。 可以向表添加或刪除行或列。

## 開始查看轉換 {#start-reviewing-a-conversion}

在第一次成功轉換之後，轉換服務將源PDF文檔與已標識的欄位和元件重疊。 您可以對已標識的欄位進行改進，並重新生成自適應表單以使輸出更接近所需體驗。 只有在第一次成功轉換後，才可開始查看轉換。

### 開始之前 {#before-you-start}

* 「審閱」和「正確」編輯器不支援片段。 不要使用編輯器查看具有 **提取片段** 選項在轉換過程中啟用。 您可以使用 [自適應表單編輯器](https://helpx.adobe.com/experience-manager/6-5/forms/using/introduction-forms-authoring.html) 轉換。

* 「審閱」和「正確」編輯器沒有撤消操作。 僅使用「保存」按鈕永久保存更改。

### 開始審閱 {#start-the-review}

要開始複查轉換，請選擇用於轉換的源PDF文檔，然後選擇並點擊 **審閱轉換**。 「審閱並更正」(Review and Correct)編輯器將在新頁籤中開啟。 您可以開始審閱轉換。 在開始解決任何其他問題之前，請執行以下基本檢查：

![](assets/usingreviewandcorrecteditor.png)

1. **所有欄位的檢查類型**:轉換服務可以為欄位指定錯誤類型。 例如，將鍵入文本而不是鍵入電話分配給行動電話欄位。 可以懸停在欄位上以查找欄位的類型。

   要更改欄位的類型，請選擇該欄位，開啟屬性瀏覽器，從 **[!UICONTROL Type]** 下拉，點擊 **[!UICONTROL Save]**。 類型已更改。

   ![](assets/check-typex75.gif)

1. **刪除額外的面板**:轉換服務可以生成額外的面板。 例如，父面板中包含額外的子面板，將空格轉換為面板，將複選框轉換為面板。 檢查所有面板的邊界並移除額外的面板。 可以使用篩選器 ![](assets/toggle_eye.png) 按鈕或內容瀏覽器來查看所有面板。

   可以刪除或取消組合面板以將其刪除。 使用「刪除」選項時，還會刪除面板的子欄位或元件：

   * 要刪除面板，請選擇面板，然後點擊刪除 ![](assets/delete-icon.png) 的子菜單。 在確認對話框上，按一下 **[!UICONTROL Confirm]**。 點擊 **[!UICONTROL Save]** 的子菜單。

   * 要取消組合面板，請選擇面板，然後點擊工具欄中的「取消組合」表徵圖。 該面板被取消分組，未分組面板的子欄位將調整為父欄位。 點擊**[!UICONTROL Save]**保存更改。

1. **建立文本的邏輯組**:驗證所標識的文本是否完整和正確。 同時檢查，文本在邏輯上放置在正確的面板或組中。 例如，在多列佈局中，一個邏輯組的文本被放置在另一個組中。

   * 要查看文本的完整性和正確性，請使用篩選器 ![](assets/toggle_eye.png) 按鈕以僅查看文本，按一下每個文本，然後驗證。 修復拼寫、拼寫或語法問題（如果有）。

   * 要向表單中添加文本，請點擊+按鈕，點擊 **[!UICONTROL Text]**。 繪製框，開啟屬性瀏覽器，然後鍵入要添加到「內容」框的文本。

1. **查看表：** 確保標識表的所有邊框。 同時，確保正確識別單元格的內容。

   * 要標識遺漏的邊框，請使用 **[!UICONTROL Add Column]** 或 **[!UICONTROL Add Row]** 的雙曲餘切值。

   * 要移除額外的邊框，請使用 **[!UICONTROL Delete Column]** 或 **[!UICONTROL Delete Row]** 的雙曲餘切值。

進行所需更改後，點擊 **[!UICONTROL Save & Convert]** 按鈕，將PDF forms重新發送到轉換服務。 將每個欄位轉換為相應的自適應欄位分量。 轉換後，更新的資產（包括自適應表單和模式）將下載到您的AEM Forms實例。 根據表單的複雜性，服務可能需要一些時間才能完成轉換。

![保存並轉換](assets/save-and-convert.png)

執行基本檢查後，您可以查看表單以修復特定於您組織的問題。 這些問題可能與添加缺少的欄位有關，等等。 您可以查看 [使用「審閱」和「正確」編輯器工具](review-correct-ui-edited.md#use-the-review-and-correct-editor-tools) 的子菜單。

您還可以致力於識別幾乎所有表單中出現的相同問題，並將此類模式報告給Adobe。 使用「審閱」(Review)和「正確」(Correct)編輯器，直到獲得所需的體驗。

## 使用「審閱」和「正確」編輯器工具 {#use-the-review-and-correct-editor-tools}

使用「審閱」和「正確」編輯器，您可以：

* [將元件添加到窗體](review-correct-ui-edited.md#add-a-component-to-the-form)
* [添加或編輯表](review-correct-ui-edited.md)
* [更改元件類型](review-correct-ui-edited.md#change-type-a-component)

* [建立或刪除面板](review-correct-ui-edited.md#create-or-remove-a-panel)
* [刪除面板或元件](review-correct-ui-edited.md#delete-a-panel-or-component)
* [設定元件的屬性](review-correct-ui-edited.md#set-properties-of-a-component)
* [發送表單以進行轉換](review-correct-ui-edited.md#send-a-form-for-conversion)

### 將元件添加到窗體 {#add-a-component-to-the-form}

轉換服務可能無法識別打印表單的某些元件。 例如，在 **出生日期** 在轉換過程中，不標識窗體的元件。 您可以使用 **+** 工具來幫助識別這些元件。 該工具允許您添加文本、欄位、選擇組、表和面板元件。

![](assets/add-component.gif)

要向表單中添加元件，請點擊 **[!UICONTROL +]** 點擊 **[!UICONTROL Field]**。 繪製覆蓋欄位標籤和輸入框的框。 例如，上面的示例影像使用欄位元件來添加 **出生日期** 標籤和值框。 繪製框時，轉換服務會標識欄位的類型。 如果需要，可以從屬性瀏覽器更改欄位類型。 建立元件後，開啟屬性瀏覽器並設定元件的屬性。

點擊 **[!UICONTROL Save]** 按鈕保存修改或使用 **[!UICONTROL Save & Convert]** 按鈕，將PDF forms重新發送到轉換服務。

### 添加或編輯表 {#addedittable}

轉換可使表單元格的幾個單元格、邊界或內容未標識。 例如，表的行未標識。 可以使用「審閱和更正」編輯器來標識此類項目。 可對表執行以下操作：

* 要選擇表，請按一下表的任何單元格。
* 要修改單元格的屬性，例如，名稱、標題或類型，請按兩下一個單元格。 您還可以按兩下該單元格來修改內容、標籤必填欄位並選擇其他屬性。
* 要向表單添加/標識完全未標識或新表，請使用 **[!UICONTROL +]** 工具欄。
* 要調整表格的單元格或行的大小，請按一下表格的空區域，將滑鼠懸停在行或列邊界上，當游標指針變化時，選擇並移動邊界。 調整大小後，按一下 **[!UICONTROL Done]** 提交更改。 按 **[!UICONTROL ESC]** 鍵以放棄調整大小。

* 要添加或刪除行或列，請在表的行中選擇一個單元格，然後選擇 **[!UICONTROL Add Row]**。 **[!UICONTROL Add Column]**。 **[!UICONTROL Delete Row]**&#x200B;或 **[!UICONTROL Delete Column]** 的 ![](assets/table_18x18.png) 的子菜單。

* 要拆分表格的單元格，請選擇 **[!UICONTROL Spilt Vertical]** 或 **[!UICONTROL Split Horizontal]** 的 ![](assets/table_18x18.png) 的子菜單。

* 要合併表的單元格，請選擇要合併的單元格，然後選擇 **[!UICONTROL Merge Cells]** 選項 ![](assets/table_18x18.png) 的子菜單。

### 更改元件類型 {#change-type-a-component}

轉換服務可以建立某些類型不正確的欄位。 例如，在下圖中， **性別** 欄位被錯誤標識為 **文本** 的子菜單。 此外，標籤的內容不正確。 欄位應為選擇欄位類型，標籤應為「性別」。 要更改元件類型並更正其標籤，請執行以下操作：

選擇要轉換的欄位，點擊 ![](assets/smock_shuffle_18_n.svg) 點擊欄位類型。 該欄位將轉換為選定的欄位類型。 欄位只能轉換為下表中列出的類型。 只能對面板元件取消分組，不能進行轉換。

| **Component** | **轉換為** |
|---|---|
| 文字 | 欄位或選擇組 |
| 欄位 | 文本或選擇組 |
| 選擇組 | 文本或面板 |

轉換後，開啟屬性瀏覽器，指定標籤，並指定其它必需屬性。 點擊 **[!UICONTROL Save]** 按鈕保存修改或使用「保存並轉換」按鈕將PDF forms重新發送到轉換服務。

### 建立或刪除面板 {#create-or-remove-a-panel}

轉換服務將打印表單的相關元件和內容聚合到面板。 例如，表單可以有一個地址面板，其中包含欄位，如名稱、出圖號、區域、城市、州、郵遞區號和國家/地區。 這些欄位將分組在一個面板中。 一個表單可以具有多個面板。

轉換服務可以建立具有與其它元件沒有關係的元件或將相對元件從面板之外的面板。 可以使用組或取消組合工具來修復這些面板：

* 要刪除面板，請選擇面板，然後點按「取消分組」 ![取消分組](assets/ungroupX18.png)。 該面板被移除，面板的子元件被移動到父元件。 您還可以使用 [刪除元件](review-correct-ui-edited.md#delete-a-panel-or-component) 的子菜單。

* 要建立面板，請使用Ctrl鍵（在Windows或Linux上）或Control鍵(在Mac)選擇相關元件，然後點擊 ![組](assets/group.jpg) 的子菜單。 開啟屬性瀏覽器以指定面板的屬性。

點擊 **[!UICONTROL Save]** 按鈕保存修改或使用 **[!UICONTROL Save & Convert]** 按鈕，將PDF forms重新發送到轉換服務。

### 刪除面板或元件 {#delete-a-panel-or-component}

轉換服務可以識別某些不正確的面板或元件。 這些面板的大部分部件是無關的。 可以刪除此類面板或元件。

要刪除面板或元件，請選擇面板或元件，然後點擊刪除 ![](assets/delete-icon.png) 表徵圖 在確認對話框上點擊 **[!UICONTROL Confirm]**。 將刪除選定的面板或元件。 刪除面板時，面板的所有子項也會被刪除。 可以使用Ctrl鍵（在Windows或Linux上）或Control鍵(在Mac)選擇多個元件或面板。

### 設定元件的屬性 {#set-properties-of-a-component}

表單的每個元件都有一組屬性，如名稱、標題、類型。 要設定元件的屬性，請選擇元件，然後點擊屬性瀏覽器。 將顯示選定元件的屬性。 更改或設定屬性。

點擊 **[!UICONTROL Save]** 按鈕保存修改或使用 **[!UICONTROL Save & Convert]** 按鈕，將PDF forms重新發送到轉換服務。

### 發送表單以進行轉換 {#send-a-form-for-conversion}

在「審閱」和「正確」編輯器中完成所有必需的更改後，可以重新發送表單以進行轉換。 要發送表單以進行轉換，請點擊 **[!UICONTROL Save & Convert]**。 的 **[!UICONTROL Sent for conversion label]** 將其應用於包含源文檔的資料夾，並將更新的源表單上載到運行在Adobe I/O上的轉換服務。

根據表單的複雜性，轉換服務可能需要一些時間才能轉換表單。 轉換完成後，轉換後的自適應表單和相關資產將下載到您的電腦。 轉換完成後，可以在編輯器中查看表單，並在 [自適應表單編輯器](https://helpx.adobe.com/experience-manager/6-5/forms/using/introduction-forms-authoring.html) ，如果需要。

如果在自適應表單編輯器中更新表單後重新發送表單進行轉換，則在自適應表單中所做的所有更改都將丟失。 只有成功轉換後，才能開啟正在審閱的表單並正確編輯器。

<!--
Comment Type: draft

<h3>Open adaptive forms editor</h3>
-->

<!--
Comment Type: draft

<p>There can be instances where you require adaptive forms editor to make the changes like, applying a different theme to the form or fixing tables. Once you have made all the required changes in Review and Correct editor and converted the form, you can open your form in adaptive forms editor to make the final set of changes.</p>
<p>To open the form with adaptive forms editor, tap the <img src="assets/properties.png" /> icon, and tap <strong>Open Adaptive Form Editor</strong>. The form opens in adaptive form editor. </p>


## Previous {#previous}

[Use Automated Forms Conversion service](convert-existing-forms-to-adaptive-forms.md)
-->
