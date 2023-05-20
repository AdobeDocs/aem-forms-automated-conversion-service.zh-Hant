---
title: 常見問題
seo-title: Frequently asked questions
description: 常見查詢或常見問題
seo-description: frequently asked questions for Automated Forms Conversion Service
uuid: 0f6dc39c-99b7-49a4-8e9e-ecc4a35110c0
topic-tags: introduction
discoiquuid: e17c2d2c-8300-4467-aa01-57365697939f
exl-id: 3a29f8d4-8ea0-49eb-bfe0-0eab5f0c52c7
source-git-commit: 47261710e6616c27c210ac53bffcc2387a06ea7a
workflow-type: tm+mt
source-wordcount: '1821'
ht-degree: 3%

---

# 常見問題{#frequently-asked-questions}

1. **automated forms conversion服務支援哪個版本的AEM Forms?**

   <p>automated forms conversion服AEM務支援6.4FormsAEM和6.5Forms。 它與AEM Forms在OSGi和JEEAEM上的表格一起工作。 您需要作者實例上的最新AEM Forms附加AEM包才能使用該服務。 有關詳細說明，請參見 <a href="configure-service.md">配置Automated forms conversion</a> 服務。</p> 
    <br>

1. **能否在本地安裝該服務？**

   <p>Adobe定期訓練Automated forms conversion服務的AI和ML算法，用新的資料集來提高轉換精度。 更新的算法被部署到在Adobe雲上運行的轉換服務，並且間隔是週期性的。 所有用戶都從更新後的算法中獲益。 因此，雲托管的中央部署最適合於Automated forms conversion服務，以便不斷學習並向所有客戶提供改進。</p> 
    <p>該服務將空白表單轉換為自適應表單。 該服務不支援填充表單和從填充表單中提取資料。 從填寫的表單中刪除資料，在將表單發送到服務以進行轉換之前從表單中刪除或允許列出專有資訊</p> <br>

1. **該服務是否支援所有格式的PDF forms? 支援哪些語言？**

   <p>該服務可以將非交互PDF forms、基於XFA的XDP和PDF forms以及AcroForms轉換為自適應表單。 該服務不支援掃描或填寫的表單。 有關其他限制，請參見 <a href="known-issues.md">已知問題</a> 文章。<br /> </p> 
    <p>我們定期添加對其他源類型的支援。 保留 <a href="introduction.md">支援的PDF表單</a> 的子菜單。</p>

   該服務只能將英語、法語、德語、西班牙語、義大利語和葡萄牙語形式轉換為適應形式。 可以使用 [翻譯AEM工作流。](https://helpx.adobe.com/experience-manager/6-5/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.html)</br> </br>

1. **服務能否生成XDP而不是自適應形式？**

   <p>該服務不生成XDP輸出。 我們定期添加功能和服務。 保留 <a href="introduction.md">支援的語言和PDF forms</a> 的子菜單。</p> <br>

1. **生成的架構的類型是什麼？**

   <p>您可以使用服務生成： </p>

   * 綁定到JSON架構的自適應表單
   * 未綁定到任何架構的自適應窗體 <br><br>

1. **服務能否將MicrosoftWord表單轉換為自適應表單？**

   <p>否，服務不會將MicrosoftWord表單轉換為自適應表單。 可以將MicrosoftWord表單保存為PDF表單，並將PDF表單轉換為自適應表單。 整個過程是 </p> <br>

   1. 使用Adobe Acrobat [將Word文檔轉換為非互動式PDF](https://helpx.adobe.com/acrobat/how-to/create-pdf-files-word-excel-website.html)。
   1. 使用Adobe Acrobat [將生成的PDF forms轉換為可填充的PDF窗體](https://helpx.adobe.com/acrobat/how-to/convert-word-excel-paper-pdf-forms.html)。
   1. 使用Adobe Acrobat手動更新和修復表單域。
   1. 保存PDF窗體。 現在，您可以將表單與轉換服務一起使用以生成自適應表單。 您還可以將表單用作「記錄文檔」模板。


1. **該服務能否將掃描的紙面表單和彩色表單轉換為自適應表單？**

   <p>該服務可將顏色PDF forms轉換為自適應表單。 該服務不支援掃描或填寫的表單。 有關其他限制，請參見 <a href="known-issues.md">已知問題</a> 文章。</p> <br>

1. **該服務能否將掃描的表單或只將表單的影像轉換為自適應表單？**

   <p>該服務不支援將掃描的表單或表單的影像轉換為自適應的開箱即用。 但是，您可以使用 Adobe Acrobat 將表單影像轉換為 PDF 表單。 然後，使用本服務將 PDF 表單轉換為最適化表單。 請總是使用高品質的表單影像在 Acrobat 中進行轉換。 這可以提升轉換的品質。</p> <br>

1. **某些基於XDP的表單使用表單片段，這些表單片段應上載到哪裡？**

   <p class="MsoNormal">將表單片段上載到轉換資料夾並保留原始資料夾結構。 它有助於保留基於XDP的表單和表單片段中使用的相對路徑。</p> <br>

1. **服務是否支援架構綁定的XDP表單？ 如果XDP綁定到架構，是否需要將架構嵌入到XDP?**

   <p>是，該服務支援模式綁定的XDP表單，並要求將模式嵌入到源XDP表單。 轉換綁定到架構的XDP表單時，服務將生成JSON架構。 JSON架構的結構與源XDP表單的XSD架構相似。</p> <br>

1. **服務無法轉換表單。 原因何在，如何解決？**
轉換失敗的最常見原因是：
</p>
   * 轉換時提供有擔保PDF forms。 請勿使用受密碼保護或安全PDF forms進行轉換。
   * Internet連接中斷。 確保在轉換過程中已連接到Internet。
   * 源PDF具有窗體而不是實際窗體的影像。
   * 服務配置不正確、未提供服務URL或提供的服務URL不正確。 檢查 [服務配置](configure-service.md#configure-the-cloud-service) 在 **[!UICONTROL AEM]** > **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Automated Forms Conversion configuration]**。
   * IMS配置配置未正確配置。 對IMS配置執行運行狀況檢查以確保其正常工作。 檢查IMS配置是否正確：
      1. 前往 `http://[servername]:[port]/libs/cq/adobeims-configuration/content/configurations.html`
      2. 選擇配置。 按一下 **[!UICONTROL Check Health]** 按一下 **[!UICONTROL Check]**。 如果成功，您將 **[!UICONTROL Token retrieved successfully!]** 。 <br> <br>

1. **使用自定義字型會影響轉換嗎？**

   <p>當將非互動式PDF表單轉換為自適應表單時，為了提高轉換質量，字型被嵌入PDF表單中。 嵌入字型的支援僅限於非交互PDF forms。 為優化AcroForm和基於XFA的PDF forms的轉換，使用回退字型。</p> 
    <p>只有在中列出的自定義字型目錄中可用的表單 <strong>客戶字型目錄</strong> 的 <strong> CQ-DAM-Handler-Gibson字型管理器服務</strong> 配置嵌入到非互動式PDF表單中。</p> 
    <p> </p> <br>

1. **服務是否在輸出自適應表單中標識和使用源PDF的字型？**

   <p>響應HTML形式的樣式和佈局通常與PDF或基於紙的形式不同。 為支援組織間一致的佈局和樣式，自適應表單使用 <a href="https://helpx.adobe.com/experience-manager/6-5/forms/using/themes.html">主題到窗體樣式</a>。 轉換服務使用在轉換期間應用的主題中指定的字型和字型樣式。 您可以更改主題的字型和字型樣式，以為自適應表單的元件提供獨特的外觀和感覺。</p> <br>

1. **服務是否自動從基於XDP的表單中提取JavaScript並將其應用於相應的自適應表單？**

   <p>該服務不會自動將基於XFA的表單或AcroForms的指令碼轉換為相應的自適應表單規則。 您（窗體作者）可以使用 <a href="https://helpx.adobe.com/experience-manager/6-5/forms/using/rule-editor.html">規則編輯器</a> 的子菜單。</p> <br>

1. **某些表單對象未正確轉換為自適應表單元件。 如何解決問題？**

   <p>automated forms conversion服務受到大量表單的培訓。 但基於AI/ML的應用程式受其訓練資料和模式的限制。 可能有多種欄位類型、佈局、模式和上下文（人類感知可識別），但難以自動識別。 服務可能無法識別這些對象或可能識別錯誤。 您可以使用 <a href="review-correct-ui-edited.md" target="_blank">審閱並更正</a> 編輯器在熟悉的基於紙張表單的輸入表單佈局中進行必要的修改。</p> <br/>

1. **有些修正在表格之間重複。 該服務能否識別並修復所有此類實例，以便將來進行轉換？**

   該服務對您的表單和模式進行持續培訓。 它每天學習新模式。 目前尚未開始自動應用在表單上重複的更正。 請注意預發行表單，以瞭解此類功能的可用性。 <br/><br/>

   可以使用元模型將表單對象映射到所選的自適應表單元件，並預配置元件的驗證、規則、資料模式、幫助文本和輔助功能屬性。 所有指定的屬性都在轉換過程中應用。 可以使用元模型將公共屬性應用到欄位。 它可以幫助您減少表單中重複的問題。<br/><br/>

1. **對於包含敏感資料(如個人識別資訊(PII)資訊)的表單，有哪些選項？**
該服務僅支援空白或未填充的表單。 不要上載包含個人身份資訊(PII)的填充表單或表單。 此外，刪除源表單中預填充的資料、個人身份資訊(PII)、機密和專有資訊。 
<br/>

1. **頁眉和頁腳應放在哪裡？**

   <p>將頁眉和頁腳置於自適應表單模板中。 如果源PDF表單具有頁眉和頁腳，則在轉換期間，服務將檢測到的頁眉和頁腳，並用自適應表單模板中可用的頁眉和頁腳進行替換。 如果自適應表單中包含任何額外的頁眉或頁腳，則可以使用 <a href="review-correct-ui-edited.md">審閱並更正</a> 編輯器以修復或刪除此類頁眉或頁腳。</p> <br />

1. **與手動規劃、建立資產（主題、模板）、建立和發佈自適應表單的過程相比，服務可節省多少時間？**

   <p>時間量取決於輸入表單的大小和複雜性以及請求數。 與手動轉換表單的過程相比，該服務打算通過以更快的速度將PDF forms轉換為自適應表單來顯著縮短實現價值的時間。 </p> <br />

1. **如果遇到與RSA庫相關的錯誤，該怎麼辦？ 錯誤消息與下面提到的消息類似：** <br/>

未為RSA/BouncyCastle庫配置引導委派時，會出現上述錯誤。 執行以下步驟以解決問題：   `*ERROR* [0:0:0:0:0:0:0:1 [1565757652491] POST /content/dam/formsanddocuments/demo004.affBatchProcessor.html HTTP/1.1] org.apache.sling.engine.impl.SlingRequestProcessorImpl service: Uncaught Throwable java.lang.NoClassDefFoundError: Could not initialize class com.rsa.cryptoj.o.dl at com.rsa.jsafe.JSAFE_SecureRandom.getInstance(Unknown Source) at com.adobe.internal.pdfm.util.Util.appendRandomNumberToPrefix(Util.java: 169) [com.adobe.aemfd.adobe-aemfd-assembler:6.0.34] at com.adobe.internal.pdfm.logging.JobLog.&amp;lt;init&amp;gt;(JobLog.java:126) [com.adobe.aemfd.adobe-aemfd-assembler:6.0.34]` <br>
未為RSA/BouncyCastle庫配置引導委派時，會出現上述錯誤。 執行以下步驟以解決問題：
   <p> </p>

   1. 停止實AEM例。 導航到 `[AEM installation directory]\crx-quickstart\conf\` 的子菜單。 開啟sling.properties檔案進行編輯。 如果您使用 `[AEM installation directory]\crx-quickstart\bin\start.bat` 要啟動實AEM例，請編輯位於 `[AEM_root]\crx-quickstart\`。
   1. 將以下屬性添加到sling.properties檔案：<br/> `sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*`<br />  `sling.bootdelegation.class.org.bouncycastle.jce.provider.BouncyCastleProvider=org.bouncycastle.*`<br /> `sling.bootdelegation.xerces=org.apache.xerces.*`
   1. 保存並關閉檔案。 <br/>
   1. 啟動 AEM 執行個體。<br/>

   <br/>

1. **如何自動更改自適應表單文本的框？**

   <p>可以使用來自主題或樣式編輯器的自適應來更改自適應表單域的大小寫。 例如，可以開啟主題編輯器，並將所有表單文本的Case屬性的值設定為大寫、小寫或camelCase。 也可以使用主題編輯器中的「CSS覆蓋」選項來建立不同類型的樣式。</p>

1. **我可以將Adobe Sign文本標籤與Automated forms conversion服務一起使用嗎？**

   <p> 當使用Automated forms conversion服務將PDF表單轉換為自適應表單且PDF表單具有Adobe Sign文本標籤時，這些標籤將轉換為相應的自適應表單域，並自動填充簽名者詳細資訊。  該功能僅適用於AcroForms，自適應表單支援有限數量的Adobe Sign欄位。</p>  </br>

1. **如何建立啟用Adobe Sign的PDF表單？**

   </p>要建立啟用Adobe Sign的PDF表單：</p>

   添加 [Adobe Sign文本標籤](https://helpx.adobe.com/sign/using/text-tag.html) 到欄位名稱或使用 [轉換為Adobe Sign窗體](https://helpx.adobe.com/sign/using/create-forms-with-acrobat.html) 的雙曲餘切值。
