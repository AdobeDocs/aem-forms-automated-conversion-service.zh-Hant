---
title: '將 PDF 表單轉換為最適化表單 '
seo-title: Convert PDF forms to adaptive forms
description: 運行Automated forms conversion服務以將PDF forms轉換為自適應表單
seo-description: Run the Automated Forms Conversion service to convert PDF forms to adaptive forms
uuid: 49fcd5c0-0e72-496d-9831-00f79d582f57
contentOwner: khsingh
topic-tags: forms
discoiquuid: 9358219c-6079-4552-92b9-b427a23811af
exl-id: 415e05b5-5a90-490c-bf7c-d3365ce95e24
source-git-commit: 5f07f5df6369007a491cf0873839f84a61827cb5
workflow-type: tm+mt
source-wordcount: '1631'
ht-degree: 6%

---

# 將 PDF 表單轉換為最適化表單 {#convert-print-forms-to-adaptive-forms}

AEM FormsAutomated forms conversion服務由Adobe Sensei提供支援，可自動將PDF forms轉換為設備友好且響應迅速的自適應格式。 無論您是使用非互動式PDF forms、 AcroFormsPDF forms還是基於XFA的，Automated forms conversion服務都可以輕鬆地將這些表單轉換為自適應表單。 有關功能、轉換工作流和登錄資訊的資訊，請參閱 [automated forms conversion](introduction.md) 服務。

## 先決條件 {#pre-requisites}

* [**配置轉換服務**](configure-service.md)

* **準備 [模板](https://helpx.adobe.com/experience-manager/6-5/forms/using/template-editor.html) 要應用於轉換的表單：** 使用模板可以在所有自適應表單中應用一致的品牌。 此外，Automated forms conversion服務不提取和使用源PDF文檔的頁眉和頁腳。 可以使用自適應表單模板指定頁眉和頁腳。 在轉換期間，模板中指定的頁眉和頁腳將應用於自適應表單。 為模板建立資料夾時，選擇 **[!UICONTROL Browse configurations]** 選項。

* **準備 [主題](https://helpx.adobe.com/experience-manager/6-5/forms/using/themes.html) 要應用於轉換的表單：** 使用主題可以將一致的樣式應用於組織的所有自適應形式。

* **（可選）** [**將源PDF forms轉換為Adobe Sign窗體**](frequently-asked-questions.md)

## 啟動轉換進程 {#start-the-conversion-process}

將實例與AEMAEM Forms轉換服務連接後，可將PDF forms轉換為自適應表單。 按列出順序執行以下步驟以轉換表單：

* [將PDF forms上載到您的AEM Forms伺服器](convert-existing-forms-to-adaptive-forms.md#upload-pdf-forms-to-your-aem-forms-server)
* [運行轉換](convert-existing-forms-to-adaptive-forms.md#run-the-conversion)
* [查看並更正已轉換的表單](review-correct-ui-edited.md)

### 將PDF forms上載到您的AEM Forms伺服器 {#upload-pdf-forms-to-your-aem-forms-server}

轉換服務將AEM Forms實例上可用的PDF forms轉換為自適應表單。 您可以按需要一次或分階段上載所有PDF forms。 在上傳表單前，請參閱以下提醒：

* 將資料夾中的表單數保留為小於15，並將資料夾中的總頁數保留為小於50。
* 將資料夾大小保持在10 MB以下。 不要將表單保留在子資料夾中。
* 將頁數保持在小於15的形式下。
* 不要上載受保護的表單。 該服務不轉換受密碼保護和安全的表單。
* 不要上載檔案名中帶空格的源表單。 在上載表單之前，從檔案名中刪除空間。
* 請勿上傳 [PDF Portfolio](https://helpx.adobe.com/acrobat/using/overview-pdf-portfolios.html)。 該服務不會將PDFPortfolio轉換為自適應格式。
* 閱讀 [已知問題](known-issues.md) 和 [最佳做法和考慮事項](styles-and-pattern-considerations-and-best-practices.md) 並對窗體進行建議的更改。

執行以下步驟以上載要轉換為AEM Forms實例上的資料夾的表單：

1. 登錄到AEM Forms實例。

1. 點擊 **[!UICONTROL Adobe Experience Manager]** ![](assets/adobeexperiencemanager.png) > **[!UICONTROL Navigation]** ![](assets/compass.png) > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**。
1. 點擊 **[!UICONTROL Create]**> **[!UICONTROL Folder]**。 指定 **標題** 和 **名稱** 的子菜單。 點選 **[!UICONTROL Create]**。建立資料夾。
1. 按一下以開啟新建立的資料夾。
1. 點擊 **[!UICONTROL Create]**> **[!UICONTROL File Upload]**。 選擇要上載的表單，按一下 **[!UICONTROL Open]**，然後按一下 **[!UICONTROL Upload]**。 將上載表單。

### 運行轉換 {#run-the-conversion}

上載表單並配置服務後，請執行以下步驟以啟動轉換：

1. 在你的AEM Forms案例上，點擊 **[!UICONTROL Adobe Experience Manager]** ![「轉換設定」對話框](assets/adobeexperiencemanager.png) > **[!UICONTROL Navigation]** ![](assets/compass.png) > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**。
1. 選擇包含PDF forms（要轉換的表單）的表單或資料夾，然後點擊 **[!UICONTROL Start Automated Conversion]**。 的 **[!UICONTROL Conversion Settings]** 對話框。

   ![指定配置](assets/conversion-settings-dialog.png)

1. 在 **[!UICONTROL Basic]** 的子菜單：

   * **[!UICONTROL Select a cloud configuration]**. 選擇配置時，已指定預設模板和主題。 如果需要，可以指定其他模板或主題。
   * 指定保存生成的自適應表單和相應架構的位置。 可以使用預設路徑或指定自定義路徑。
   * 使用 **生成沒有資料模型綁定的自適應表單** 選項，以選擇是否要生成具有或不具有資料模型綁定的自適應窗體。
如果未選擇此選項，則轉換服務將自動將自適應表單與JSON架構相關聯，並在自適應表單和JSON架構中可用的欄位之間建立資料綁定。 的 **[!UICONTROL Save generated data model schema at]** 欄位顯示用於保存生成的JSON架構的預設位置。 還可以自定義位置以保存生成的架構。
如果選擇此選項，轉換服務將生成一個沒有資料模型綁定的自適應表單。 成功轉換後，可以將自適應表單與表單資料模型、XML架構或JSON架構關聯。 有關詳細資訊，請參見 [建立自適應窗體](https://helpx.adobe.com/experience-manager/6-5/forms/using/creating-adaptive-form.html)。

   <!--

   Comment Type: draft

   <note type="note">
   <p>The XDP or XFA-based PDF form is not used to generate the Document of Record. The conversion service auto-generates the Document of Record only if you enable the Tools &gt; Cloud Services &gt; Automated Forms Conversion Configuration &gt; <strong>&lt;Properties of selected configuration&gt; &gt;</strong> Advanced &gt; Generate Document of Record option.</p>
   <p> </p>
   </note>
   -->

1. 在 **[!UICONTROL Additional]** 的子菜單。
   * 選擇 **[!UICONTROL Extract fragment from adaptive forms]** 選項，以允許轉換服務識別、提取和下載轉換的表單片段。 選擇 **[!UICONTROL Extract fragment from adaptive forms]** 選項，啟用指定用於保存提取的表單片段和相應表單片段架構的路徑的選項。
   * 指定的位置 **[!UICONTROL existing adaptive form fragments]**，如果您有一些基於JSON架構的現有和模式的自適應性較差的表單片段，並且您計畫在自動生成的自適應表單中使用這些片段。 轉換服務將可用的基於JSON架構和模式的非自適應格式片段與輸入PDF forms(僅非互動式PDF forms)匹配，如果存在匹配，則匹配的自適應格式片段用於相應的自適應格式。

   >[!NOTE]
   >
   >
   > * 您只能使用 **[!UICONTROL  Extract Fragment]** 或 **[!UICONTROL Use existing adaptive form fragments]** 的上界。 不能同時使用這兩個選項。
   > * 您可以使用 **[!UICONTROL Use existing adaptive form fragments]** 的子菜單。 尚不支援其他窗體類型。
   > * 您只能使用自動轉換服務綁定到JSON架構的未綁定片段或片段。 不要使用XFA片段。 不支援XFA片段。


   * 選擇 **[!UICONTROL Auto-detect multi-column layout of input forms]** 選項，以保留台式機和筆記型電腦等大螢幕的源窗體佈局。 此選項有助於保留源表單的多列佈局。 例如，當源PDF具有雙列佈局時，服務將生成輸出自適應表單，該表單具有用於大螢幕顯示的雙列佈局和用於諸如行動電話的小螢幕設備的單列佈局。 該功能與資料源架構結構有一些已知問題。 有關詳細資訊，請參閱 [已知問題](known-issues.md) 文章。
   * 在預設狀態中，此服務會為 PDF 表單的每一頁分別建立頂層面板。 現在，你可以 **[!UICONTROL Auto-detect logical sections]** 選項，不建立頁級面板（基於頁數的面板）和僅建立邏輯面板。 這個選項還可將不屬於任何具有前置邏輯區段之區段的欄位，與橫跨至兩個相鄰頁面的邏輯區段的欄位合併成一個邏輯區段。 例如，如果邏輯區段中有些欄位位於第一頁底部，有些位於第二頁頂部，則所有該欄位都會合併成一個邏輯區段。

      >[!NOTE]
      > 您需要連接器包1.1.38或更高版本才能使用  **[!UICONTROL Auto-detect logical sections]** 的子菜單。


* (僅AEM Formsas a Cloud Service) [自動將節轉換為片段] 的子菜單。 它將檢測到的頂級部分轉換為片段。 它還允許對所有建立的片段進行延遲載入。 它有助於提高轉換表單的渲染速度，並使在自適應表單編輯器中載入大型表單更加容易。

   >[!NOTE]
   > 使用「自動將節轉換為片段」選項時，不要使用響應佈局模板。
   > 使用審閱和正確編輯器將小面板合併為大面板。 它有助於減少轉換後的自適應形式中的片段數。
   > 如果遇到&quot;呼叫過多&quot;的異常，
   >
   > * 重構表單以建立簡化層次
   > * [增加sling.max.calls參數的值]達到足夠高的數字，直到異常消失。
   > * [增加快取大小](https://experienceleague.adobe.com/docs/experience-manager-65/forms/install-aem-forms/configure-aem-forms/configure-adaptive-forms-cache.html)。 如果表單過於複雜、表數較多且具有多層層次結構，則會出現錯誤。


1. 點選 **[!UICONTROL Start Conversion]**。轉換即會啟動。 轉換進度顯示在資料夾或窗體上，直到轉換正在進行。 轉換完成後，該消息將被替換另一個狀態消息（轉換、部分轉換或轉換失敗）。 在完成轉換時，還會在配置的電子郵件地址上發送狀態電子郵件：

   * 在成功轉換時，轉換後的自適應表單和相關模式將下載到在 **[!UICONTROL Basic]** 的子菜單。 僅當在開始轉換之前選擇了「提取片段」選項時，才下載表單片段和相應的架構。
   * 在轉換失敗時， **[!UICONTROL Conversion Failed]** 如果所有輸入表單無法轉換或 **[!UICONTROL Partially Failed]** 當只有少數輸入表單無法轉換時，將顯示消息。 在 [已配置電子郵件地址](configure-service.md#configureemailnotification) 錯誤記錄到error.log檔案。

   如果要將基於XFA的PDF表單轉換為自適應表單，則轉換服務會自動將PDF表單與轉換後的自適應表單關聯為「記錄文檔」模板。 轉換後，可以開啟自適應表單屬性，以在 **[!UICONTROL Document of Record Template Configuration]** 部分 **[!UICONTROL Form Model]** 頁籤。 </br>

   只有在啟用了「記錄文檔」模板時，轉換服務才會將PDF表單自動上載到轉換後的自適應表單中 **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Automated Forms Conversion Configuration]** > **[!UICONTROL Properties of selected configuration]** > **[!UICONTROL Advanced]** > **[!UICONTROL Generate Document of Record]** 的雙曲餘切值。

   <!--

   Comment Type: draft

   <note type="note">
   <p>By default, the adaptive form produces a JSON schema instead of XML schema on submission. JSON schema of a converted adaptive form is complaint with XML schema of an XFA-based form. You can use the <a href="https://sling.apache.org/apidocs/sling5/org/apache/sling/commons/json/xml/XML.html#toString">org.apache.sling.commons.json.xml API</a> to convert a JSON schema to XML schema. You can also use the following sample code for conversion:</p>
   <p><code class="code">import org.apache.sling.commons.json.JSONException;
   <discoiqbr /> import org.apache.sling.commons.json.JSONObject;
   <discoiqbr /> import org.apache.sling.commons.json.xml.XML;
   <discoiqbr />
   <discoiqbr /> public class ConversionUtils {
   <discoiqbr />
   <discoiqbr /> public static String jsonToXML(String jsonString) throws JSONException {
   <discoiqbr /> //https://sling.apache.org/apidocs/sling5/org/apache/sling/commons/json/xml/XML.html#toString(java.lang.Object)
   <discoiqbr /> //jar - http://maven.ibiblio.org/maven2/org/apache/sling/org.apache.sling.commons.json/2.0.18/
   <discoiqbr /> //Note: Need to extract boundData part before converting to XML
   <discoiqbr /> return XML.toString(new JSONObject(jsonString));
   <discoiqbr /> }
   <discoiqbr /> }</code><br /> </p>
   </note>
   -->

   >[!NOTE]
   >
   >如果轉換過程需要60分鐘以上，並且PDF表單仍未轉換為自適應表單，請在AEM Forms實例上建立資料夾，將PDF表單上載到新建立的資料夾，然後重新啟動轉換。

## 查看並更正已轉換的表單 {#review-and-correct-the-converted-forms}

現實世界中的表單對資料捕獲有著複雜的要求。 完成自動轉換後，客戶可以查看表單的轉換質量並對表單進行必要的更新。 AEM Forms提供 [審閱和更正](review-correct-ui-edited.md) 編輯器以進行所需更改。 它允許您改進表單域的自動標識，並將標識的域從一種類型轉換為另一種類型。 例如，您可以幫助標識表單的兩列佈局，並將自動標識為單選按鈕的欄位更改為多個選項欄位。
