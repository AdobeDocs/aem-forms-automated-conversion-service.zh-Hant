---
title: 常見問題
seo-title: 常見問題
description: 常見查詢或常見問題
seo-description: automated forms conversion服務常見問題
uuid: 0f6dc39c-99b7-49a4-8e9e-ecc4a35110c0
topic-tags: introduction
discoiquuid: e17c2d2c-8300-4467-aa01-57365697939f
exl-id: 3a29f8d4-8ea0-49eb-bfe0-0eab5f0c52c7
source-git-commit: af05922f9eb76b7b0a30601824c6006fe555ea80
workflow-type: tm+mt
source-wordcount: '1830'
ht-degree: 3%

---

# 常見問題{#frequently-asked-questions}

1. **automated forms conversion服務支援哪個AEM Forms版本？**

   <p>automated forms conversion服務支援AEM 6.4 Forms和AEM 6.5 Forms。 適用於OSGi上的AEM Forms和JEE上的AEM表單。 您需要AEM製作例項上最新的AEM Forms附加套件才能使用服務。 有關詳細說明，請參閱<a href="configure-service.md">配置Automated forms conversion</a>服務。</p> 
    <br>

1. **是否可在內部部署安裝該服務？**

   <p>Adobe會定期訓練Automated forms conversion服務的AI和ML演算法，並提供新的資料集以改善轉換準確度。 更新的演算法會部署至定期在Experience Cloud上執行的Adobe服務。 更新的演算法可讓服務的所有客戶受益。 因此，雲端托管的中央部署最適合Automated forms conversion服務，以持續了解並改善所有客戶。</p> 
    <p>此服務會將空白表單轉換為最適化表單。 此服務不支援已填入的表單，以及從已填入的表單中擷取資料。 從已填寫的表單中移除資料，並在將表單傳送至服務進行轉換之前，從表單中移除或允許清單專有資訊</p> <br>

1. **此服務是否支援所有格式的PDF forms?支援哪些語言？**

   <p>此服務可將非互動式PDF forms、XFA型XDP和PDF forms，以及AcroForms轉換為最適化表單。 此服務不支援掃描或填寫的表單。 如需其他限制，請參閱<a href="known-issues.md">已知問題</a>文章。<br /> </p> 
    <p>我們定期增加對其他源類型的支援。 將<a href="introduction.md">受支援的PDF forms</a>區段保留在監視清單上，以定期更新新增的功能。</p>

   此服務只能將英文、法文、德文和西班牙文語言表單轉換為最適化表單。 您可以使用[AEM翻譯工作流程將產生的最適化表單翻譯成其他語言。](https://helpx.adobe.com/experience-manager/6-5/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.html)</br> </br>

1. **此服務是否可產生XDP而非最適化表單？**

   <p>服務不會產生XDP輸出。 我們定期為服務添加功能。 將<a href="introduction.md">支援的語言和PDF forms</a>區段保留在監視清單上，以定期更新新增的功能。</p> <br>

1. **產生的架構類型為何？**

   <p>您可以使用服務來產生： </p>

   * 系結至JSON結構描述的適用性表單，以及
   * 未綁定到任何架構<br><br>的自適應表單

1. **此服務能將Microsoft Word表單轉換為最適化表單嗎？**

   <p>否，服務不會將Microsoft Word表單轉換為最適化表單。 您可以將Microsoft Word表單儲存為PDF表單，並將PDF表單轉換為最適化表單。 整個過程是 </p> <br>

   1. 使用Adobe Acrobat將「Word文檔」轉換為非互動式PDF](https://helpx.adobe.com/acrobat/how-to/create-pdf-files-word-excel-website.html)。[
   1. 使用Adobe Acrobat將產生的PDF forms轉換為可填寫的PDF表單](https://helpx.adobe.com/acrobat/how-to/convert-word-excel-paper-pdf-forms.html)。[
   1. 使用Adobe Acrobat手動更新和修正表單欄位。
   1. 儲存PDF表單。 現在，您可以透過轉換服務使用表單來產生最適化表單。 您也可以將該表單用作「記錄文檔」模板。


1. **此服務能將掃描的紙面表單和彩色表單轉換為最適化表單嗎？**

   <p>此服務可將色彩PDF forms轉換為最適化表單。 此服務不支援掃描或填寫的表單。 如需其他限制，請參閱<a href="known-issues.md">已知問題</a>文章。</p> <br>

1. **服務是否可將掃描的表單或表單的僅影像轉換為最適化表單？**

   <p>此服務不支援將掃描的表單或表單影像轉換為可調整的現成可用表單。 但是，您可以使用 Adobe Acrobat 將表單影像轉換為 PDF 表單。 然後，使用本服務將 PDF 表單轉換為最適化表單。 請總是使用高品質的表單影像在 Acrobat 中進行轉換。 這可以提升轉換的品質。</p> <br>

1. **有些XDP型表單使用表單片段，應在何處上傳這些表單片段？**

   <p class="MsoNormal">將表單片段上傳至轉換資料夾，並保留原始資料夾結構。 有助於保留以XDP為基礎的表單和表單片段中使用的相對路徑。</p> <br>

1. **服務是否支援結構綁定的XDP表單？如果我的XDP綁定到架構，是否需要將架構嵌入到XDP?**

   <p>是的，此服務支援架構綁定的XDP表單，並要求將架構嵌入源XDP表單。 轉換結構界限的XDP表單時，服務會產生JSON結構描述。 JSON結構與來源XDP表單的XSD結構類似。</p> <br>

1. **服務無法轉換表單。原因為何以及如何解決此問題？**
轉換失敗的最常見原因為：
</p>
   * 為轉換提供安全PDF forms。 請勿使用密碼保護或安全PDF forms進行轉換。
   * 網際網路連接中斷。 確保在轉換期間您已連線至網際網路。
   * 源PDF具有表單的影像，而非實際表單。
   * 服務配置不正確、未提供服務URL或提供的服務URL不正確。 在&#x200B;**[!UICONTROL AEM]** > **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Automated Forms Conversion configuration]**&#x200B;檢查[服務配置](configure-service.md#configure-the-cloud-service)。
   * IMS設定未正確設定。 對IMS設定執行健康狀況檢查，以確保正常運作。 檢查IMS設定是否正確：
      1. 前往 `http://[servername]:[port]/libs/cq/adobeims-configuration/content/configurations.html`
      2. 選取設定。 按一下標題中的&#x200B;**[!UICONTROL Check Health]**，然後按一下&#x200B;**[!UICONTROL Check]**。 如果成功，您會收到&#x200B;**[!UICONTROL Token retrieved successfully!]**&#x200B;訊息。<br> <br>

1. **使用自訂字型是否會影響轉換？**

   <p>當非互動式PDF表單轉換為最適化表單時，為了改善轉換品質，字型會嵌入PDF表單中。 嵌入字型的支援僅限於非互動式PDF forms。 為了最佳化AcroForm和XFA型PDF forms的轉換，會使用備援字型。</p> 
    <p>只有<strong> CQ-DAM-Handler-Gibson Font Manager Service</strong>配置的<strong>客戶字型目錄</strong>欄位中列出的自定義字型目錄中可用的表單嵌入非互動式PDF表單。</p> 
    <p> </p> <br>

1. **此服務是否能在輸出最適化表單中識別和使用來源PDF的字型？**

   <p>回應式HTML表單的樣式和版面通常與PDF或紙面表單不同。 為了支援組織內一致的版面和樣式，最適化表單會使用<a href="https://helpx.adobe.com/experience-manager/6-5/forms/using/themes.html">主題來設定表單的樣式</a>。 轉換服務使用轉換期間所應用主題中指定的字型和字型樣式。 您可以變更主題的字型和字型樣式，為最適化表單的元件提供獨特的外觀和風格。</p> <br>

1. **此服務會自動從XDP型表單中擷取JavaScript，並套用至對應的最適化表單嗎？**

   <p>此服務不會自動將XFA型表單或Acro Forms的指令碼轉換為對應的最適化表單規則。 您（表單作者）可以使用<a href="https://helpx.adobe.com/experience-manager/6-5/forms/using/rule-editor.html">規則編輯器</a>為最適化表單新增互動功能。</p> <br>

1. **有些表單物件無法正確轉換為最適化表單元件。如何解決此問題？**

   <p>automated forms conversion服務是針對大量表單進行訓練。 但基於AI/ML的應用程式受其培訓資料和模式的限制。 可能有多種欄位類型、佈局、模式和上下文可以辨別人類感知，但難以自動識別。 服務可能無法識別此類對象或可能識別錯誤。 您可以使用<a href="review-correct-ui-edited.md" target="_blank">檢閱和修正</a>編輯器，在熟悉的紙質表單輸入表單的版面配置中進行必要的修改。</p> <br/>

1. **某些修正會在不同表單中重複。該服務是否可以識別並修正未來轉換中的所有此類例項？**

   此服務可持續地培訓您的表單和模式。 它每天學習新模式。 尚未開始自動套用在表單中重複的更正。 請留意發行前表單，以了解此功能是否可用。<br/><br/>

   您可以使用元模型將表單物件對應至您所選擇的最適化表單元件，並預先配置元件的驗證、規則、資料模式、說明文字和協助工具屬性。 轉換期間會套用所有指定的屬性。 可以使用元模型將公共屬性應用到欄位。 它可協助您減少表單間重複發生的問題。<br/><br/>

1. **含有個人識別資訊(PII)等敏感資料的表單有哪些選項？**
此服務僅支援空白或未填寫的表單。請勿上傳含有個人識別資訊(PII)的已填入表單或表單。 此外，還可移除原始碼表單中預先填入的資料、個人識別資訊(PII)、機密和專屬資訊。 
<br/>

1. **頁首和頁尾應放在何處？**

   <p>將頁首與頁尾置於最適化表單範本中。 如果來源PDF表單有頁首和頁尾，則服務會在轉換期間偵測並以適用性表單範本中可用的頁首和頁尾，來取代偵測到的頁首和頁尾。 如果適用性表單中包含任何額外的頁首或頁尾，您可以使用<a href="review-correct-ui-edited.md">檢閱和修正</a>編輯器來修正或移除此類頁首或頁尾。</p> <br />

1. **與手動規劃、建立資產（主題、範本）、建立和發佈最適化表單的程式相比，此服務可節省多少時間？**

   <p>時間長度取決於輸入表單的大小和複雜度以及請求數。 與手動轉換表單的程式相比，此服務打算以更快的速度將PDF forms轉換為最適化表單，大幅縮短實現價值的時間。 </p> <br />

1. **如果遇到與RSA庫相關的錯誤，該怎麼辦？錯誤訊息與下列提及的訊息類似：** <br/>

未為RSA/BuncyCastle庫配置引導委派時，將出現上述錯誤。 執行下列步驟以解決問題：   `*ERROR* [0:0:0:0:0:0:0:1 [1565757652491] POST /content/dam/formsanddocuments/demo004.affBatchProcessor.html HTTP/1.1] org.apache.sling.engine.impl.SlingRequestProcessorImpl service: Uncaught Throwable java.lang.NoClassDefFoundError: Could not initialize class com.rsa.cryptoj.o.dl at com.rsa.jsafe.JSAFE_SecureRandom.getInstance(Unknown Source) at com.adobe.internal.pdfm.util.Util.appendRandomNumberToPrefix(Util.java: 169) [com.adobe.aemfd.adobe-aemfd-assembler:6.0.34] at com.adobe.internal.pdfm.logging.JobLog.&amp;lt;init&amp;gt;(JobLog.java:126) [com.adobe.aemfd.adobe-aemfd-assembler:6.0.34]` <br>
未為RSA/BuncyCastle庫配置引導委派時，將出現上述錯誤。執行下列步驟以解決問題：
   <p> </p>

   1. 停止AEM例項。 導覽至`[AEM installation directory]\crx-quickstart\conf\`資料夾。 開啟sling.properties檔案以進行編輯。 如果您使用`[AEM installation directory]\crx-quickstart\bin\start.bat`啟動AEM例項，請編輯位於`[AEM_root]\crx-quickstart\`的sling.properties。
   1. 將下列屬性新增至sling.properties檔案：<br/> `sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*`<br />  `sling.bootdelegation.class.org.bouncycastle.jce.provider.BouncyCastleProvider=org.bouncycastle.*`<br /> `sling.bootdelegation.xerces=org.apache.xerces.*`
   1. 儲存並關閉檔案。<br/>
   1. 啟動AEM實例。<br/>

   <br/>

1. **如何自動變更最適化表單文字的大小寫？**

   <p>您可以使用主題或樣式編輯器中的最適化來變更最適化表單欄位的大小寫。 例如，您可以開啟主題編輯器，並將表單中所有文字的Case屬性的值設定為大寫、小寫或camelCase。 您也可以使用主題編輯器中的「CSS覆寫」選項來建立不同類型的樣式。</p>

1. **我可以搭配Automated forms conversion服務使用Adobe Sign文字標籤嗎？**

   <p> 當您使用Automated forms conversion服務將PDF表單轉換為最適化表單，且PDF表單具有Adobe Sign文字標籤時，這些標籤會轉換為對應的最適化表單欄位，並自動填入簽署者詳細資訊。  此功能僅適用於Acro Forms，且適用性表單支援有限數量的Adobe Sign欄位。</p>  </br>

1. **如何建立啟用Adobe Sign的PDF表單？**

   </p>若要建立啟用Adobe Sign的PDF表單：</p>

   將[Adobe Sign文字標籤](https://helpx.adobe.com/sign/using/text-tag.html)新增至欄位名稱，或使用[轉換為Adobe Sign表單](https://helpx.adobe.com/sign/using/create-forms-with-acrobat.html)選項。
