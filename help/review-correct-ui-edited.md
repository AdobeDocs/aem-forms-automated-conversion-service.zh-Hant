---
title: 檢閱並修正轉換後的表格
seo-title: 檢閱並修正轉換後的表格
description: 檢閱並修正Automated forms conversion服務轉換的最適化表單。
seo-description: 檢閱並修正由Automated forms conversion服務轉換的最適化表單
uuid: 5a0a6d24-dff6-4732-b607-24848b07b26d
topic-tags: forms
discoiquuid: f45ab2d7-5234-42d6-aeb6-b2cb1a7ce3c2
exl-id: 64330fa2-aa9d-4ba4-96df-b75deed3e693
source-git-commit: 1a3f79925f25dcc7dbe007f6e634f6e3a742bf72
workflow-type: tm+mt
source-wordcount: '2536'
ht-degree: 0%

---

# 檢閱並修正轉換後的表格{#review-and-correct-converted-forms}

AEM FormsAutomated forms conversion服務可識別輸入PDF檔案的欄位、內容和版面，並將PDF檔案轉換為最適化表單。 輸出最適化表單可能缺少一些欄位或未正確轉換的欄位。 您可以使用檢閱和修正編輯器來改善已識別的欄位，並重新產生最適化表單，讓輸出更接近所需的體驗。 第一次轉換後，您可以在編輯器中開啟輸入的PDF檔案，以：

* 檢視轉換期間識別的所有欄位和內容
* 識別轉換期間遺漏的欄位和內容
* 驗證欄位的類型，並視需要變更其類型
* 驗證已識別的表格、調整欄的大小以及修改儲存格內容
* 移除識別錯誤的欄位

進行必要的變更後，將PDF forms重新傳送至轉換服務。 成功轉換後，更新的資產（包括最適化表單和結構）會下載至您的AEM Forms例項。 您可以重複此程式，直到達到所需的體驗。![](assets/stages-of-form-2.gif)

您需要Google Chrome、Mozilla FireFox或Microsoft Edge瀏覽器，才能使用審核和正確的編輯器。 編輯器不支援Internet Explorer。

## 歡迎使用檢閱和修正編輯器{#welcome-to-review-and-correct-editor}

「檢閱與修正」編輯器提供簡單易用的介面。 其元件如下：

* 內容瀏覽器：您可以使用內容瀏覽器來變更元素的位置。 內容瀏覽器可讓您拖放表單物件以變更其位置。 例如，在文本框之前移動表。 它會據此變更輸出最適化表單的索引標籤順序。
* 屬性瀏覽器：它顯示所選欄位的屬性。 您也可以修改屬性。
* 工具列：工具列位於編輯器頂端。 它顯示用於添加、修改、分組、取消分組和刪除欄位的工具。
* 開啟屬性：點選![](assets/properties.png)圖示時會顯示「開啟屬性」選項。 您可以按一下開啟屬性以開啟表單屬性並檢視其他選項。
* 篩選按鈕：篩選器按鈕![](assets/toggle_eye.png)位於編輯器頂端。 它可讓您篩選欄位，以僅顯示文字、欄位、選擇群組、面板或所有元件。
* 「保存」按鈕：**[!UICONTROL Save]**&#x200B;按鈕位於編輯器的右上角。 您也可以使用「儲存」按鈕旁的箭頭，檢視傳送表單以進行轉換的選項。

* PDF表單：編輯器會顯示來源PDF檔案，並以已識別的欄位覆蓋它。 您可以使用工具列中的工具來修改欄位。
* 頁面：來源表單可以有多個頁面。 編輯器提供右上角的按鈕，可在頁面之間導覽。

![檢閱並修正UI](assets/reviewcorrectui.png)

**A.** 內容瀏 **覽器B.** 屬性瀏覽器 **C.** 工具列 **D.** 屬性按鈕 **E.** 篩選按鈕 **F.** 儲存按鈕 **G.** PDF表單以已識別欄位覆蓋

第一次成功轉換後，轉換服務會覆蓋原始PDF檔案及已識別的欄位和元件。 以下欄位或元件屬於類型：文本、欄位、面板、選擇組和表：

* 文字：源PDF文檔中的純文字檔案。 例如，上方顯示的影像中的「貸款申請」文字。
* 欄位：與值或輸入框關聯的文本或表徵表徵圖簽的組合。 例如，上圖中的「第一個」欄位名稱。 它有文字標籤和輸入框。 欄位支援文字、數值、下拉式清單、日期、電子郵件、電話號碼、簽名、貨幣和密碼資料類型。
* 面板：內容和元件的邏輯集合。 例如，上圖中「人員1」和「人員2」面板的個人詳細資料。
* 選擇組：與多個選擇選項相關聯的文字組合：複選框和單選按鈕。 例如，上圖中的「婚姻狀態」和「現有客戶」。\
   轉換服務會根據選擇組標題及其多選選項，自動將選擇組轉換為單選單選按鈕或多選複選框。 例如，如果&#x200B;**選擇任何一個**&#x200B;作為選擇組標題或多選選項允許您僅選擇一個選項，**是**&#x200B;或&#x200B;**否**，則轉換服務會自動將選擇組轉換為單選單選按鈕。 同樣地，如果存在&#x200B;**選擇所有應用**&#x200B;或&#x200B;**選擇多個**&#x200B;作為選擇組標題或多選擇選項允許您選擇多個選項，則轉換服務會自動將選擇組轉換為多選擇複選框。

* 表：2-d表，其資訊以列和行表示。 您可以新增或移除列至表格。

## 開始檢閱轉換{#start-reviewing-a-conversion}

第一次成功轉換後，轉換服務會覆蓋原始PDF檔案及已識別的欄位和元件。 您可以對已識別的欄位進行改良，並重新產生最適化表單，使輸出更接近所需體驗。 您必須先成功轉換，才能開始檢閱轉換。

### 開始之前{#before-you-start}

* 檢閱和修正編輯器不支援片段。 請勿使用編輯器來檢閱在轉換期間啟用了&#x200B;**擷取片段**&#x200B;選項的轉換。 您可以對這類轉換使用[適用性表單編輯器](https://helpx.adobe.com/experience-manager/6-5/forms/using/introduction-forms-authoring.html)。

* 檢閱和修正編輯器沒有還原動作。 僅使用「保存」按鈕來永久保存更改。

### 開始查看{#start-the-review}

若要開始查看轉換，請選擇用於轉換的源PDF文檔，然後選擇並點選&#x200B;**查看轉換**。 「檢閱和修正」編輯器會在新索引標籤中開啟。 您可以開始檢閱轉換。 請先執行下列基本檢查，再開始修正任何其他問題：

![](assets/usingreviewandcorrecteditor.png)

1. **檢查所有欄位的類型**:轉換服務可能會將錯誤的類型指派給欄位。例如，將文字指派給行動電話欄位，而非類型電話。 您可以暫留在欄位上，以尋找欄位類型。

   要更改欄位類型，請選擇欄位，開啟屬性瀏覽器，從&#x200B;**[!UICONTROL Type]**&#x200B;下拉清單中選擇值，然後點選&#x200B;**[!UICONTROL Save]**。 類型已變更。

   ![](assets/check-typex75.gif)

1. **移除額外面板**:轉換服務可產生額外的面板。例如，父面板中包含額外的子面板，空白空間轉換為面板，核取方塊轉換為面板。 檢閱所有面板的邊界，並移除額外的面板。 您可以使用篩選器![](assets/toggle_eye.png)按鈕或內容瀏覽器來檢視所有面板。

   您可以刪除或取消面板的群組以將其移除。 使用刪除選項時，也會刪除面板的子欄位或元件：

   * 若要刪除面板，請選取面板，然後點選工具列中的「刪除![](assets/delete-icon.png) 」圖示。 在確認對話方塊上，點選&#x200B;**[!UICONTROL Confirm]**。 點選&#x200B;**[!UICONTROL Save]**&#x200B;以儲存變更。

   * 若要取消面板的群組，請選取面板，然後點選工具列中的取消群組圖示。 此面板會取消分組，而未分組面板的子欄位會調整為父欄位。 點選**[!UICONTROL Save]**以儲存變更。

1. **建立文本的邏輯組**:驗證所標識的文本的完整性和正確性。此外，文本在邏輯上被放置在正確的面板或組中。 例如，在多列佈局中，一個邏輯組的文本放置在另一個組中。

   * 要檢查文本的完整性和正確性，請使用篩選器![](assets/toggle_eye.png)按鈕來僅查看文本，按一下每個文本，然後驗證。 修正拼字、錯字或文法問題（如果有）。

   * 若要新增文字至表單，請點選+按鈕，點選&#x200B;**[!UICONTROL Text]**。 繪製框、開啟屬性瀏覽器，並鍵入要添加到「內容」框的文本。

1. **查看表：** 確保標識表的所有邊框。同時，請確定儲存格的內容已正確識別。

   * 要識別遺漏的邊界，請使用&#x200B;**[!UICONTROL Add Column]**&#x200B;或&#x200B;**[!UICONTROL Add Row]**&#x200B;選項。

   * 要刪除額外邊框，請使用&#x200B;**[!UICONTROL Delete Column]**&#x200B;或&#x200B;**[!UICONTROL Delete Row]**&#x200B;選項。

進行必要的變更後，點選&#x200B;**[!UICONTROL Save & Convert]**&#x200B;按鈕以重新傳送PDF forms至轉換服務。 將每個欄位轉換為相應的自適應欄位元件。 轉換後，更新的資產（包括最適化表單和結構）會下載至您的AEM Forms例項。 視表單的複雜度而定，服務可能需要一些時間才能完成轉換。

![儲存並轉換](assets/save-and-convert.png)

執行基本檢查後，您可以檢閱表單以修正貴組織的特定問題。 這些問題可能與新增遺失的欄位等有關。 您可以檢視[使用檢閱和修正編輯器工具](review-correct-ui-edited.md#use-the-review-and-correct-editor-tools)區段，了解編輯器為修正此類問題提供的所有工具。

您也可以確認幾乎所有表單中都發生的相同問題，並將這類模式報告給Adobe。 使用檢閱和修正編輯器，直到達到所需體驗為止。

## 使用「查看並更正」編輯器工具{#use-the-review-and-correct-editor-tools}

使用檢閱和修正編輯器，您可以：

* [將元件新增至表單](review-correct-ui-edited.md#add-a-component-to-the-form)
* [添加或編輯表](review-correct-ui-edited.md)
* [變更元件類型](review-correct-ui-edited.md#change-type-a-component)

* [建立或移除面板](review-correct-ui-edited.md#create-or-remove-a-panel)
* [刪除面板或元件](review-correct-ui-edited.md#delete-a-panel-or-component)
* [設定元件的屬性](review-correct-ui-edited.md#set-properties-of-a-component)
* [傳送表單以進行轉換](review-correct-ui-edited.md#send-a-form-for-conversion)

### 將元件添加到{#add-a-component-to-the-form}窗體中

轉換服務可能無法識別列印表單的某些元件。 例如，在轉換期間，表單的&#x200B;**出生日期**&#x200B;元件未識別。 您可以使用&#x200B;**+**&#x200B;工具來協助識別此類元件。 此工具可讓您新增文字、欄位、選擇群組、表格和面板元件。

![](assets/add-component.gif)

若要將元件新增至表單，請點選&#x200B;**[!UICONTROL +]**&#x200B;並點選&#x200B;**[!UICONTROL Field]**。 繪製覆蓋欄位標籤和輸入框的框。 例如，上述範例影像使用欄位元件，將&#x200B;**出生日期**&#x200B;標籤和值方塊新增至表單中。 當您繪製框時，轉換服務將標識欄位的類型。 如有需要，您可以從屬性瀏覽器變更欄位類型。 建立元件後，開啟屬性瀏覽器，並設定元件的屬性。

點選&#x200B;**[!UICONTROL Save]**&#x200B;按鈕以儲存修改，或使用&#x200B;**[!UICONTROL Save & Convert]**&#x200B;按鈕將PDF forms重新傳送至轉換服務。

### 添加或編輯表 {#addedittable}

轉換可能會讓數個儲存格、邊界或表格儲存格的內容未識別。 例如，表格的一行未被標識。 您可以使用「檢閱和修正」編輯器來識別此類項目。 您可以對表格執行下列動作：

* 若要選取表格，請按一下表格的任何儲存格。
* 若要修改儲存格的屬性，例如名稱、標題或類型，請連按兩下儲存格。 您也可以連按兩下儲存格來修改內容、標示必填欄位，然後選取其他屬性。
* 若要在表單中添加/標識完全未標識或新表，請使用&#x200B;**[!UICONTROL +]**&#x200B;工具。
* 要調整表格的單元格或行的大小，請按一下表格的空區域，將滑鼠移到行或列邊界上，當游標指針更改時，選擇並移動邊界。 調整大小後，按一下&#x200B;**[!UICONTROL Done]**&#x200B;以提交更改。 您可以按&#x200B;**[!UICONTROL ESC]**&#x200B;鍵捨棄重新調整大小。

* 要添加或刪除行或列，請選擇表行中的單元格，然後從![](assets/table_18x18.png)菜單中選擇&#x200B;**[!UICONTROL Add Row]**、**[!UICONTROL Add Column]**、**[!UICONTROL Delete Row]**&#x200B;或&#x200B;**[!UICONTROL Delete Column]**&#x200B;選項。

* 要將單元格拆分為表，請從![](assets/table_18x18.png)菜單中選擇&#x200B;**[!UICONTROL Spilt Vertical]**&#x200B;或&#x200B;**[!UICONTROL Split Horizontal]**&#x200B;選項。

* 要合併表的單元格，請選擇要合併的單元格，然後從![](assets/table_18x18.png)表菜單中選擇&#x200B;**[!UICONTROL Merge Cells]**&#x200B;選項。

### 更改元件類型{#change-type-a-component}

轉換服務可能會建立某些類型不正確的欄位。 例如，在下圖中，將&#x200B;**Gender**&#x200B;欄位錯誤地標識為&#x200B;**Text**&#x200B;欄位。 此外，標籤的內容不正確。 欄位應為選擇欄位類型，標籤應為「性別」。 要更改元件類型並更正其標籤：

選取要轉換的欄位，點選![](assets/smock_shuffle_18_n.svg)並點選欄位類型。 欄位會轉換為選取的欄位類型。 欄位只能轉換為下表中列出的類型。 面板元件只能取消分組，不能轉換。

| **元件** | **轉換為** |
|---|---|
| 文字 | 欄位或選擇組 |
| 欄位 | 文本或選擇組 |
| 選擇組 | 文字或面板 |

轉換後，開啟屬性瀏覽器、指定標籤，以及指定其他必要屬性。 點選&#x200B;**[!UICONTROL Save]**&#x200B;按鈕以儲存修改內容，或使用「儲存並轉換」按鈕以將PDF forms重新傳送至轉換服務。

### 建立或移除面板{#create-or-remove-a-panel}

轉換服務將列印表單的相關元件和內容匯總至面板。 例如，表單可以有一個地址面板，其中包含欄位，如名稱、出圖號、區域、城市、州、郵遞區號和國家。 這些欄位會分組在面板中。 表單可以有多個面板。

轉換服務可建立元件與其他元件無關的面板，或將相對元件移出面板。 您可以使用群組或取消群組工具來修正這類面板：

* 若要移除面板，請選取面板，然後點選「取消群組![取消群組](assets/ungroupX18.png)」。 此時會移除面板，並將面板的子元件移至父元件。 您也可以使用[delete component](review-correct-ui-edited.md#delete-a-panel-or-component)選項來刪除面板及其子項。

* 要建立面板，請使用Ctrl鍵（在Windows或Linux上）或Control鍵（在Mac上）選擇相關元件，然後點選![group](assets/group.jpg)以建立面板。 開啟屬性瀏覽器以指定面板的屬性。

點選&#x200B;**[!UICONTROL Save]**&#x200B;按鈕以儲存修改，或使用&#x200B;**[!UICONTROL Save & Convert]**&#x200B;按鈕將PDF forms重新傳送至轉換服務。

### 刪除面板或元件{#delete-a-panel-or-component}

轉換服務可識別某些錯誤的面板或元件。 這些面板的大部分元件都與非相關。 您可以刪除這類面板或元件。

若要刪除面板或元件，請選取面板或元件，然後點選「刪除![](assets/delete-icon.png)」圖示。 在確認對話方塊上，點選&#x200B;**[!UICONTROL Confirm]**。 選定的面板或元件將被刪除。 刪除面板時，也會刪除面板的所有子項。 您可以使用Ctrl鍵（在Windows或Linux上）或Control鍵（在Mac上）來選取多個元件或面板。

### 設定元件{#set-properties-of-a-component}的屬性

表單的每個元件都有一組屬性，例如名稱、標題、類型。 若要設定元件的屬性，請選取元件，然後點選屬性瀏覽器。 將顯示所選元件的屬性。 變更或設定屬性。

點選&#x200B;**[!UICONTROL Save]**&#x200B;按鈕以儲存修改，或使用&#x200B;**[!UICONTROL Save & Convert]**&#x200B;按鈕將PDF forms重新傳送至轉換服務。

### 傳送表單以進行轉換{#send-a-form-for-conversion}

在檢閱和修正編輯器中完成所有必要變更後，您就可以重新傳送表單以進行轉換。 若要傳送表單以進行轉換，請點選&#x200B;**[!UICONTROL Save & Convert]**。 **[!UICONTROL Sent for conversion label]**&#x200B;會套用至包含來源檔案的資料夾，而更新的來源表單會上傳至Adobe I/O上執行的轉換服務。

視表單的複雜度而定，轉換服務可能需要一些時間才能轉換表單。 轉換完成後，轉換的最適化表單和相關資產會下載至您的電腦。 轉換完成後，您可以在編輯器中檢閱表單，並視需要在[適用性表單編輯器](https://helpx.adobe.com/experience-manager/6-5/forms/using/introduction-forms-authoring.html)中開啟最適化表單，以取得最終的修正集。

如果您在適用性表單編輯器中更新表單後重新傳送表單以進行轉換，在適用性表單中所做的所有變更都會遺失。 您只能在成功轉換後，才能開啟審核中的表單並修正編輯器。

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
