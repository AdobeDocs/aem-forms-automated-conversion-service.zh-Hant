---
title: '將 PDF 表單轉換為最適化表單 '
seo-title: '將 PDF 表單轉換為最適化表單 '
description: 執行自動表單轉換服務，將PDF表單轉換為最適化表單
seo-description: 執行自動表單轉換服務，將PDF表單轉換為最適化表單
uuid: 49fcd5c0-0e72-496d-9831-00f79d582f57
contentOwner: khsingh
topic-tags: forms
discoiquuid: 9358219c-6079-4552-92b9-b427a23811af
translation-type: tm+mt
source-git-commit: c4f0d07b38cdb6aa162a0b61abe12fe9d1677a8c
workflow-type: tm+mt
source-wordcount: '1487'
ht-degree: 7%

---


# 將 PDF 表單轉換為最適化表單 {#convert-print-forms-to-adaptive-forms}

AEM Forms Automated Forms Conversion服務（採用Adobe Sensei）會自動將PDF表單轉換為裝置友好且回應速度快的調適性表單。 無論您是使用非互動式PDF表單、Acro Forms或XFA型PDF表單，Automated Forms Conversion服務都可輕鬆將這些表單轉換為最適化表單。 如需功能、轉換工作流程和入門資訊的詳細資訊，請參閱[自動化表單轉換](introduction.md)服務。

## 先決條件{#pre-requisites}

* [**設定轉換服務**](configure-service.md)

* **準備范 [](https://helpx.adobe.com/experience-manager/6-5/forms/using/template-editor.html) 本以套用至轉換的表單：使** 用範本可讓您在所有最適化表單上套用一致的品牌。此外，Automated Forms Conversion服務不會擷取並使用來源PDF檔案的頁首和頁尾。 您可以使用最適化表單範本來指定頁首和頁尾。 在轉換期間，範本中指定的頁首和頁尾會套用至最適化表單。 為模板建立資料夾時，請為每個人選擇&#x200B;**[!UICONTROL Browse configurations]**&#x200B;選項。

* **準備要套 [](https://helpx.adobe.com/experience-manager/6-5/forms/using/themes.html) 用至轉換表單的主題：使** 用主題可讓您對組織的所有最適化表單套用一致的樣式。

* **（選用）** [**將來源PDF表格轉換為Adobe Sign表格**](frequently-asked-questions.md)


## 啟動轉換過程{#start-the-conversion-process}

在您將AEM實例與AEM Forms Conversion Service連接後，您就可以將PDF表單轉換為最適化表單。 請依所列順序執行下列步驟以轉換表單：

* [將PDF表格上傳至AEM Forms伺服器](convert-existing-forms-to-adaptive-forms.md#upload-pdf-forms-to-your-aem-forms-server)
* [執行轉換](convert-existing-forms-to-adaptive-forms.md#run-the-conversion)
* [檢閱並修正轉換的表單](review-correct-ui-edited.md)

### 將PDF表格上傳至您的AEM Forms伺服器{#upload-pdf-forms-to-your-aem-forms-server}

轉換服務會將AEM Forms例項上可用的PDF表單轉換為最適化表單。 您可以視需要一次或分階段上傳所有PDF表格。 在上傳表單前，請參閱以下提醒：

* 將資料夾中的表單數保持在小於15，並將資料夾中的頁數總數保持在小於50。
* 將檔案夾大小保持在10 MB以下。 請勿將表單保留在子資料夾中。
* 將頁數保持在小於15的形式中。
* 請勿上傳受保護的表單。 該服務不會轉換受密碼保護和安全的表單。
* 請勿上傳檔案名稱中含空格的來源表單。 在上傳表單之前，先從檔案名稱中移除空格。
* 請勿上傳 [PDF Portfolio](https://helpx.adobe.com/acrobat/using/overview-pdf-portfolios.html)。 本服務不會將PDF資料夾轉換為最適化表單。
* 閱讀[已知問題](known-issues.md)和[最佳實踐和注意事項](styles-and-pattern-considerations-and-best-practices.md)章節，並對表單進行建議的更改。

請執行下列步驟，將要轉換為AEM Forms例項資料夾的表單上傳：

1. 登入AEM Forms例項。

1. 點選&#x200B;**[!UICONTROL Adobe Experience Manager]** ![](assets/adobeexperiencemanager.png) > **[!UICONTROL Navigation]** ![](assets/compass.png) > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**。
1. 點選&#x200B;**[!UICONTROL Create]**> **[!UICONTROL Folder]**。 指定資料夾的&#x200B;**標題**&#x200B;和&#x200B;**名稱**。 點選&#x200B;**[!UICONTROL Create]**。 建立資料夾。
1. 點選以開啟新建立的資料夾。
1. 點選&#x200B;**[!UICONTROL Create]**> **[!UICONTROL File Upload]**。 選擇要上傳的表單，按一下&#x200B;**[!UICONTROL Open]** ，然後按一下&#x200B;**[!UICONTROL Upload]**。 表單會上傳。

### 執行轉換{#run-the-conversion}

上傳表單並設定服務後，請執行下列步驟以開始轉換：

1. 在您的AEM Forms例項中，點選「**[!UICONTROL Adobe Experience Manager]** ![轉換設定對話方塊> ](assets/adobeexperiencemanager.png) > **[!UICONTROL Navigation]** ![](assets/compass.png) > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**」。
1. 選擇包含PDF表單（要轉換的表單）的表單或資料夾，然後點選&#x200B;**[!UICONTROL Start Automated Conversion]**。 出現&#x200B;**[!UICONTROL Conversion Settings]**&#x200B;對話框。

   ![指定配置](assets/conversion-settings-dialog.png)

1. 在「轉換設定」對話方塊的&#x200B;**[!UICONTROL Basic]**&#x200B;標籤中：

   * **[!UICONTROL Select a cloud configuration]**. 選擇配置時，已指定預設模板和主題。 您可以視需要指定不同的範本或主題。
   * 指定儲存產生的最適化表單和對應架構的位置。 您可以使用預設路徑或指定自訂路徑。
   * 使用&#x200B;**產生不含資料模型系結的最適化表單**選項，以選擇您是否要產生含或不含資料模型系結的最適化表單。
如果您未選取此選項，轉換服務會自動將最適化表單與JSON結構描述關聯，並在最適化表單和JSON結構描述中可用的欄位間建立資料系結。 **[!UICONTROL Save generated data model schema at]**欄位會顯示儲存產生之JSON結構描述的預設位置。 您也可以自訂位置以儲存產生的結構。
如果您選取此選項，轉換服務會產生不含資料模型系結的最適化表單。 成功轉換後，您可將最適化表單與表單資料模型、XML結構描述或JSON結構描述建立關聯。 如需詳細資訊，請參閱[建立最適化表單](https://helpx.adobe.com/experience-manager/6-5/forms/using/creating-adaptive-form.html)。

   <!--
   Comment Type: draft

   <note type="note">
   <p>The XDP or XFA-based PDF form is not used to generate the Document of Record. The conversion service auto-generates the Document of Record only if you enable the Tools &gt; Cloud Services &gt; Automated Forms Conversion Configuration &gt; <strong>&lt;Properties of selected configuration&gt; &gt;</strong> Advanced &gt; Generate Document of Record option.</p>
   <p> </p>
   </note>
   -->

1. 在「轉換設定」對話方塊的&#x200B;**[!UICONTROL Additional]**&#x200B;標籤中，
   * 選取&#x200B;**[!UICONTROL Extract fragment from adaptive forms]**&#x200B;選項，允許轉換服務識別、擷取和下載轉換表單片段。 選擇&#x200B;**[!UICONTROL Extract fragment from adaptive forms]**&#x200B;選項時，將啟用指定路徑以保存提取的表單片段和相應表單片段結構描述的選項。
   * 如果您現有的JSON結構描述和結構描述不太適應的表單片段，而且您打算在自動產生的最適化表單中使用這些片段，請指定&#x200B;**[!UICONTROL existing adaptive form fragments]**&#x200B;的位置。 轉換服務會將可用的JSON架構型和架構較不適應性的表單片段與輸入的PDF表單（僅限非互動式PDF表單）相符，如果有相符，則相符的最適化表單片段會用於對應的最適化表單。

   >[!NOTE]
   >
   >
   > * 一次只能使用&#x200B;**[!UICONTROL  Extract Fragment]**&#x200B;或&#x200B;**[!UICONTROL Use existing adaptive form fragments]**&#x200B;選項。 您不能同時使用這兩個選項。
   > * 您只能將&#x200B;**[!UICONTROL Use existing adaptive form fragments]**&#x200B;選項用於非互動式PDF表單。 目前尚未支援其他表格類型。
   > * 您只能使用自動轉換服務中系結至JSON結構描述的未系結片段或片段。 請勿使用XFA片段。 不支援XFA片段。


   * 選擇&#x200B;**[!UICONTROL Auto-detect multi-column layout of input forms]**&#x200B;選項，以保留大型螢幕（如台式機和筆記型電腦）的源表單佈局。 此選項有助於保留來源表單的多欄版面配置。 例如，當來源PDF有雙欄版面時，服務會針對大螢幕顯示產生雙欄版面的輸出最適化表單，而針對行動電話等小螢幕裝置則產生單欄版面。 此功能與資料來源架構結構有一些已知問題。 如需詳細資訊，請參閱[known-issues](known-issues.md)文章。
   * 在預設狀態中，此服務會為 PDF 表單的每一頁分別建立頂層面板。 現在，您可使用&#x200B;**[!UICONTROL Auto-detect logical sections]**&#x200B;選項，來建立頁面層級面板（以頁碼為基礎的面板），並僅建立邏輯面板。 這個選項還可將不屬於任何具有前置邏輯區段之區段的欄位，與橫跨至兩個相鄰頁面的邏輯區段的欄位合併成一個邏輯區段。 例如，如果邏輯區段中有些欄位位於第一頁底部，有些位於第二頁頂部，則所有該欄位都會合併成一個邏輯區段。

      >[!NOTE]
      > 您需要連接器軟體包1.1.38或更高版本才能使用&#x200B;**[!UICONTROL Auto-detect logical sections]**&#x200B;功能。



1. 點選&#x200B;**[!UICONTROL Start Conversion]**。 轉換即會開始。 轉換進度會顯示在資料夾或表單上，直到轉換進行為止。 轉換完成後，消息將替換另一個狀態消息（轉換、部分轉換或轉換失敗）。 完成轉換時，也會在設定的電子郵件地址上傳送狀態電子郵件：

   * 在成功轉換時，將轉換的自適應表單和相關模式下載到轉換對話框的&#x200B;**[!UICONTROL Basic]**&#x200B;頁籤中指定的路徑。 只有在開始轉換之前選取「擷取片段」選項時，才會下載表單片段和對應的架構。
   * 在轉換失敗時，如果所有輸入表單都無法轉換，則顯示&#x200B;**[!UICONTROL Conversion Failed]**&#x200B;消息；如果只有少數輸入表單無法轉換，則顯示&#x200B;**[!UICONTROL Partially Failed]**&#x200B;消息。 在[配置的電子郵件地址](configure-service.md#configureemailnotification)上發送狀態電子郵件，並將錯誤記錄到error.log檔案。

   如果您要將以XFA為基礎的PDF表單轉換為最適化表單，轉換服務會自動將PDF表單與已轉換的最適化表單建立關聯，做為記錄檔案範本。 轉換後，您可以開啟最適化表單屬性，在&#x200B;**[!UICONTROL Form Model]**&#x200B;標籤的&#x200B;**[!UICONTROL Document of Record Template Configuration]**&#x200B;區段中查看「記錄文檔」模板。</br>

   只有啟用&#x200B;**[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Automated Forms Conversion Configuration]** > **[!UICONTROL Properties of selected configuration]** > **[!UICONTROL Advanced]** > **[!UICONTROL Generate Document of Record]**&#x200B;選項，轉換服務才會自動將PDF表單上傳為已轉換的最適化表單，作為「記錄文檔」模板。

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
   >如果轉換程式需要60分鐘以上，而PDF表格仍未轉換為最適化表格，請在AEM Forms例項上建立檔案夾、將PDF表格上傳至新建立的檔案夾，然後重新開始轉換。

## 查看並更正已轉換的表單{#review-and-correct-the-converted-forms}

現實世界的表單有複雜的資料擷取需求。 自動轉換完成後，客戶可以檢閱表單的轉換品質，並對表單進行必要的更新。 AEM Forms提供[檢閱和更正](review-correct-ui-edited.md)編輯器，以進行必要的變更。 它可讓您改善表單欄位的自動識別，並將識別的欄位從一種類型轉換為另一種類型。 例如，您可以協助識別表單的雙欄版面配置，並將自動識別為選項按鈕的欄位變更為多個選項欄位。
