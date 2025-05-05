---
title: 檢閱並修正轉換後的表單
description: 檢閱並修正由Automated forms conversion服務(AFCS)轉換的最適化表單。
solution: Experience Manager Forms
feature: Adaptive Forms, Foundation Components
topic: Administration
topic-tags: forms
role: Admin, Developer
level: Beginner, Intermediate
exl-id: 64330fa2-aa9d-4ba4-96df-b75deed3e693
source-git-commit: c2392932d1e29876f7a11bd856e770b8f7ce3181
workflow-type: tm+mt
source-wordcount: '2512'
ht-degree: 0%

---

# 檢閱並修正轉換後的表單{#review-and-correct-converted-forms}

AEM FormsAutomated forms conversion服務(AFCS)可識別輸入PDF檔案的欄位、內容和版面，並將PDF檔案轉換為最適化表單。 輸出調適型表單可能有一些欄位遺失或轉換不正確。 您可以使用檢閱和修正編輯器來改善已識別的欄位，並重新產生最適化表單，使輸出更接近所需的體驗。 第一次轉換後，您可以在編輯器中開啟輸入PDF檔案，以：

* 檢視轉換期間識別的所有欄位和內容
* 識別轉換期間遺漏的欄位和內容
* 驗證欄位的型別並變更其型別（如果需要）
* 驗證已識別的表格、調整欄大小並修改儲存格內容
* 移除錯誤識別的欄位

進行必要的變更後，將PDF forms重新傳送至轉換服務。 成功轉換後，更新的資產（包括最適化表單和結構描述）會下載到您的AEM Forms執行個體。 您可以重複此程式，直到達到所需的體驗為止。![](assets/stages-of-form-2.gif)

您需要Google Chrome、Mozilla FireFox或Microsoft Edge瀏覽器才能使用檢閱和修正編輯器。 編輯器不支援Internet Explorer。

## 歡迎使用檢閱和修正編輯器 {#welcome-to-review-and-correct-editor}

「稽核並修正」編輯器提供簡單易用的介面。 它有下列元件：

* 內容瀏覽器：您可以使用內容瀏覽器來變更元素的位置。 內容瀏覽器可讓您拖放表單物件以變更其位置。 例如，在文字方塊之前移動表格。 這會相應地變更輸出最適化表單的索引標籤順序。
* 屬性瀏覽器：顯示所選欄位的屬性。 您也可以修改屬性。
* 工具列：工具列在編輯器頂端。 它會顯示新增、修改、分組、取消分組和刪除欄位的工具。
* 開啟屬性：點選![](assets/properties.png)圖示時，開啟屬性選項就會顯示。 您可以按一下「開啟屬性」來開啟表單屬性並檢視其他選項。
* 篩選按鈕：篩選按鈕![](assets/toggle_eye.png)在編輯器上方。 它可讓您篩選欄位以僅顯示文字、欄位、選擇群組、面板或所有元件。
* 儲存按鈕： **[!UICONTROL Save]**&#x200B;按鈕在編輯器的右上角。 您也可以使用儲存按鈕旁的箭頭，檢視傳送表單進行轉換的選項。

* PDF表單：編輯器顯示來源PDF檔案，並將它覆蓋在已識別的欄位中。 您可以使用工具列中的工具來修改欄位。
* 頁面：來源表單可以有多個頁面。 編輯器在右上角提供一個按鈕，用於在頁面之間導覽。

![檢閱並修正UI](assets/reviewcorrectui.png)

**A.**&#x200B;內容瀏覽器&#x200B;**B.**&#x200B;屬性瀏覽器&#x200B;**C.**&#x200B;工具列&#x200B;**D.**&#x200B;屬性按鈕&#x200B;**E.**&#x200B;篩選器按鈕&#x200B;**F.**&#x200B;儲存按鈕&#x200B;**G.** PDF表單已用已識別的欄位覆蓋

首次成功轉換後，轉換服務會以識別的欄位和元件覆蓋來源PDF檔案。 這些欄位或元件的型別為：文字、欄位、面板、選擇群組和表格：

* 文字：來源PDF檔案中的純文字。 例如，上方顯示影像中的貸款申請文字。
* 欄位：與值或輸入方塊相關聯的文字或圖示標籤組合。 例如，上述影像中的第一個欄位名稱。 它有文字標籤和一個輸入方塊。 欄位支援文字、數值、下拉式清單、日期、電子郵件、電話號碼、簽名、貨幣和密碼資料型別。
* 面板：內容和元件的邏輯集合。 例如，上圖中人員1和人員2的個人詳細資訊面板。
* 選擇群組：與多個選擇選項相關的文字組合：核取方塊和選項按鈕。 例如上圖中的婚姻狀況和現有客戶。\
  轉換服務會根據選擇群組標題及其多選選項，自動將選擇群組轉換為單選選項按鈕或多選核取方塊。 例如，如果有&#x200B;**選取任何一個**&#x200B;作為選擇群組標題，或複選選項僅允許您選取一個選項&#x200B;**是**&#x200B;或&#x200B;**否**，轉換服務會自動將選擇群組轉換為單選單選按鈕。 同樣地，如果有&#x200B;**選取所有適用的**&#x200B;或&#x200B;**選取多個**&#x200B;作為選擇群組標題，或選擇多個選項可讓您選取多個選項，轉換服務會自動將選擇群組轉換為多選核取方塊。

* 表格：以欄和列表示資訊的二維表格。 您可以在表格中新增或移除列或欄。

## 開始檢閱轉換 {#start-reviewing-a-conversion}

首次成功轉換後，轉換服務會以識別的欄位和元件覆蓋來源PDF檔案。 您可以改善已識別的欄位，並重新產生最適化表單，使輸出更接近所需的體驗。 您只能在首次成功轉換後開始檢閱轉換。

### 開始之前 {#before-you-start}

* 檢閱和修正編輯器不支援片段。 請勿使用編輯器來檢閱在轉換期間啟用了&#x200B;**擷取片段**&#x200B;選項的轉換。 您可以針對這類轉換使用[最適化表單編輯器](https://helpx.adobe.com/experience-manager/6-5/forms/using/introduction-forms-authoring.html)。

* 「稽核並修正」編輯器沒有復原動作。 僅使用「儲存」按鈕來永久儲存變更。

### 開始檢閱 {#start-the-review}

若要開始檢閱轉換，請選取用於轉換的來源PDF檔案，然後選取並點選&#x200B;**檢閱轉換**。 「檢閱並修正」編輯器會在新標籤中開啟。 您可以開始檢閱轉換。 在開始修正任何其他問題之前，請先執行下列基本檢查：

![](assets/usingreviewandcorrecteditor.png)

1. **檢查所有欄位的型別**：轉換服務可能會指派錯誤的型別給欄位。 例如，在行動電話欄位中，會指派型別文字而非型別電話。 您可以將滑鼠指標暫留在欄位上以尋找欄位型別。

   若要變更欄位型別，請選取欄位、開啟屬性瀏覽器、從&#x200B;**[!UICONTROL Type]**&#x200B;下拉式清單中選取值，然後點選&#x200B;**[!UICONTROL Save]**。 型別已變更。

   ![](assets/check-typex75.gif)

1. **移除額外的面板**：轉換服務可以產生額外的面板。 例如，父面板中包含一個額外的子面板，空白空間會轉換為面板，核取方塊會轉換為面板。 檢閱所有面板的邊界，並移除多餘的面板。 您可以使用篩選器![](assets/toggle_eye.png)按鈕或內容瀏覽器來檢視所有面板。

   您可以刪除或取消面板的群組以將其移除。 使用刪除選項時，也會刪除面板的子欄位或元件：

   * 若要刪除面板，請選取面板，然後點選工具列中的刪除![](assets/delete-icon.png)圖示。 在確認對話方塊中，點選&#x200B;**[!UICONTROL Confirm]**。 點選&#x200B;**[!UICONTROL Save]**&#x200B;以儲存變更。

   * 若要取消面板群組，請選取面板，然後點選工具列中的「取消群組」圖示。 面板會取消分組，取消分組面板的子欄位會調整為父欄位。 點選&#x200B;**[!UICONTROL Save]**&#x200B;以儲存變更。

1. **建立文字的邏輯群組**：驗證所識別的文字的完整性和正確性。 也請核取，文字會邏輯地放置在正確的面板或群組中。 例如，在多欄版面配置中，一個邏輯群組的文字並放置在另一個群組中。

   * 若要檢視文字的完整性和正確性，請使用篩選![](assets/toggle_eye.png)按鈕來檢視文字、按一下每個文字，然後驗證。 修正拼字、拼字或文法問題（如有）。

   * 若要新增文字至表單，請點選+按鈕，點選&#x200B;**[!UICONTROL Text]**。 在Draw方塊中，開啟屬性瀏覽器，然後輸入要新增至「內容」方塊的文字。

1. **檢閱資料表：**&#x200B;請確定資料表的所有邊界都已識別。 同時也請確定已正確識別儲存格的內容。

   * 若要識別遺漏的邊框，請使用&#x200B;**[!UICONTROL Add Column]**&#x200B;或&#x200B;**[!UICONTROL Add Row]**&#x200B;選項。

   * 若要移除額外邊框，請使用&#x200B;**[!UICONTROL Delete Column]**&#x200B;或&#x200B;**[!UICONTROL Delete Row]**&#x200B;選項。

進行必要的變更後，點選&#x200B;**[!UICONTROL Save & Convert]**&#x200B;按鈕以將PDF forms重新傳送至轉換服務。 每個欄位都會轉換為對應的調適型欄位元件。 轉換後，更新的資產（包括最適化表單和結構描述）會下載至您的AEM Forms執行個體。 根據表單的複雜程度，服務可能需要一些時間才能完成轉換。

![儲存並轉換](assets/save-and-convert.png)

執行基本檢查後，您可以檢閱表單以修正組織的特定問題。 這些問題可能與新增缺少的欄位等相關。 您可以檢視[使用檢閱和修正編輯器工具](review-correct-ui-edited.md#use-the-review-and-correct-editor-tools)區段，瞭解編輯器提供用來修正這類問題的所有工具。

您也可以努力辨識幾乎所有表單中發生的相同問題，並向Adobe報告此類模式。 使用「稽核並修正」編輯器，直到獲得所需的體驗為止。

## 使用檢閱和修正編輯器工具 {#use-the-review-and-correct-editor-tools}

使用「稽核並修正」編輯器，您可以：

* [將元件新增至表單](review-correct-ui-edited.md#add-a-component-to-the-form)
* [新增或編輯表格](review-correct-ui-edited.md)
* [變更元件型別](review-correct-ui-edited.md#change-type-a-component)

* [建立或移除面板](review-correct-ui-edited.md#create-or-remove-a-panel)
* [刪除面板或元件](review-correct-ui-edited.md#delete-a-panel-or-component)
* [設定元件的屬性](review-correct-ui-edited.md#set-properties-of-a-component)
* [傳送表單進行轉換](review-correct-ui-edited.md#send-a-form-for-conversion)

### 將元件新增至表單 {#add-a-component-to-the-form}

轉換服務可能無法識別列印表單的某些元件。 例如，在轉換期間未識別表單的&#x200B;**出生日期**&#x200B;元件中。 您可以使用&#x200B;**+**&#x200B;工具來協助識別這類元件。 此工具可讓您新增文字、欄位、選擇群組、表格和面板元件。

![](assets/add-component.gif)

若要將元件新增至表單，請點選&#x200B;**[!UICONTROL +]**&#x200B;並點選&#x200B;**[!UICONTROL Field]**。 Draw包含標籤和欄位輸入方塊的方塊。 例如，上述範例影像使用欄位元件將&#x200B;**出生日期**&#x200B;標籤及其下方的值方塊新增至表單。 當您繪製方塊時，轉換服務會識別欄位的型別。 如有需要，您可以從屬性瀏覽器變更欄位型別。 建立元件後，開啟屬性瀏覽器，並設定元件的屬性。

點選「**[!UICONTROL Save]**」按鈕以儲存修改，或使用「**[!UICONTROL Save & Convert]**」按鈕將PDF forms重新傳送至轉換服務。

### 新增或編輯表格 {#addedittable}

轉換可能會保留一些無法識別的儲存格、邊界或表格儲存格內容。 例如，未識別資料表的資料列。 您可以使用「稽核並修正」編輯器來識別此類專案。 您可以對表格執行下列動作：

* 若要選取表格，請按一下表格的任何儲存格。
* 若要修改儲存格的屬性（例如，名稱、標題或型別），請按兩下儲存格。 您也可以連按兩下儲存格以修改內容、標示必填欄位，以及選取其他屬性。
* 若要在表單中新增/識別完全無法識別的表格或新表格，請使用&#x200B;**[!UICONTROL +]**&#x200B;工具。
* 若要調整表格儲存格或列的大小，請在表格的空白區域上按一下滑鼠，將游標停留在列或欄邊界上，游標指標變更時，選取並移動邊界。 重新調整大小後，按一下&#x200B;**[!UICONTROL Done]**&#x200B;以認可變更。 您可以按下&#x200B;**[!UICONTROL ESC]**&#x200B;鍵以放棄調整大小。

* 若要新增或刪除列或欄，請選取表格列中的儲存格，然後從![](assets/table_18x18.png)功能表選取&#x200B;**[!UICONTROL Add Row]**、**[!UICONTROL Add Column]**、**[!UICONTROL Delete Row]**&#x200B;或&#x200B;**[!UICONTROL Delete Column]**&#x200B;選項。

* 若要分割資料表的儲存格，請從![](assets/table_18x18.png)功能表選取&#x200B;**[!UICONTROL Spilt Vertical]**&#x200B;或&#x200B;**[!UICONTROL Split Horizontal]**&#x200B;選項。

* 若要合併表格的儲存格，請選取要合併的儲存格，然後從![](assets/table_18x18.png)表格選單中選取&#x200B;**[!UICONTROL Merge Cells]**&#x200B;選項。

### 變更元件型別 {#change-type-a-component}

轉換服務可能會建立一些型別不正確的欄位。 例如，在下列影像中，**性別**&#x200B;欄位被錯誤識別為&#x200B;**文字**&#x200B;欄位。 此外，標籤的內容不正確。 欄位應為選擇欄位型別，標籤應為「性別」。 若要變更元件的型別並更正其標籤：

選取要轉換的欄位，點選![](assets/smock_shuffle_18_n.svg)並點選欄位型別。 該欄位會轉換為所選的欄位型別。 欄位只能轉換為下表列出的型別。 面板元件只能取消分組，不能轉換。

| **Component** | **轉換為** |
|---|---|
| 文字 | 欄位或選擇群組 |
| 欄位 | 文字或選擇群組 |
| 選擇群組 | 文字或面板 |

轉換之後，請開啟屬性瀏覽器，指定標籤，然後指定其他必要屬性。 點選「**[!UICONTROL Save]**」按鈕以儲存修改，或使用「儲存並轉換」按鈕將PDF forms重新傳送至轉換服務。

### 建立或移除面板 {#create-or-remove-a-panel}

轉換服務會將列印表單的相關元件和內容彙總至面板。 例如，表單可以有一個地址面板，內含欄位，例如，名稱、繪圖編號、地區、城市、州、郵遞區號和國家/地區。 這些欄位會分組在面板中。 一個表單可以有多個面板。

轉換服務可建立面板，其中的元件與其他元件沒有關係，或將相對元件排除在面板之外。 您可以使用群組或取消群組工具來修正這些面板：

* 若要移除面板，請選取面板，然後點選取消群組![取消群組](assets/ungroupX18.png)。 面板會移除，而面板的子元件會移至父元件。 您也可以使用[刪除元件](review-correct-ui-edited.md#delete-a-panel-or-component)選項來刪除面板及其子系。

* 若要建立面板，請使用Ctrl鍵（在Windows或Linux上）或Control鍵(在Mac上)選取相關元件，然後點選![群組](assets/group.jpg)以建立面板。 開啟屬性瀏覽器以指定面板的屬性。

點選「**[!UICONTROL Save]**」按鈕以儲存修改，或使用「**[!UICONTROL Save & Convert]**」按鈕將PDF forms重新傳送至轉換服務。

### 刪除面板或元件 {#delete-a-panel-or-component}

轉換服務可能會識別出某些不正確的面板或元件。 這些面板中的大部分元件都是不相關的。 您可以刪除此類面板或元件。

若要刪除面板或元件，請選取面板或元件，然後點選「刪除![](assets/delete-icon.png)」圖示。 在確認對話方塊中，點選&#x200B;**[!UICONTROL Confirm]**。 所選的面板或元件即被刪除。 刪除面板時，也會刪除面板的所有子項。 您可以使用Ctrl鍵（在Windows或Linux上）或Control鍵(在Mac上)來選取多個元件或面板。

### 設定元件的屬性 {#set-properties-of-a-component}

表單的每個元件都有一組屬性，例如名稱、標題、型別。 若要設定元件的屬性，請選取元件，然後點選「屬性」瀏覽器。 會顯示所選元件的屬性。 變更或設定屬性。

點選「**[!UICONTROL Save]**」按鈕以儲存修改，或使用「**[!UICONTROL Save & Convert]**」按鈕將PDF forms重新傳送至轉換服務。

### 傳送表單進行轉換 {#send-a-form-for-conversion}

在「稽核並修正」編輯器中完成所有必要的變更後，您可以重新傳送表單以進行轉換。 若要傳送表單以進行轉換，請點選&#x200B;**[!UICONTROL Save & Convert]**。 **[!UICONTROL Sent for conversion label]**&#x200B;已套用至包含來原始檔的資料夾，且更新的來源表單已上傳至Adobe I/O上執行的轉換服務。

根據表單的複雜性，轉換服務可能需要一些時間才能轉換表單。 轉換完成後，轉換後的自適應表單和相關資產會下載到您的電腦。 轉換完成後，您可以在編輯器中檢閱表單，並視需要在[最適化表單編輯器](https://helpx.adobe.com/experience-manager/6-5/forms/using/introduction-forms-authoring.html)中開啟最適化表單，以取得最終修正集。

如果您在更新最適化表單編輯器中的表單後，重新傳送表單以供轉換，則最適化表單中所做的所有變更都會遺失。 只有在成功轉換之後，您才能在檢閱和修正編輯器中開啟表單。

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
