---
title: 常見問題
seo-title: 常見問題
description: 常見查詢或常見問題
seo-description: Automated Forms Conversion Service的常見問題
uuid: 0f6dc39c-99b7-49a4-8e9e-ecc4a35110c0
topic-tags: introduction
discoiquuid: e17c2d2c-8300-4467-aa01-57365697939f
translation-type: tm+mt
source-git-commit: 92cd241915ef5818fb004a8982674b4f6753c171
workflow-type: tm+mt
source-wordcount: '1825'
ht-degree: 4%

---


# 常見問題{#frequently-asked-questions}

1. **Automated Forms Conversion服務支援哪個AEM Forms版本？**

   <p>Automated Forms Conversion服務支援AEM 6.4 Forms和AEM 6.5 Forms。 它可與OSGi上的AEM Forms和JEE上的AEM Forms搭配使用。 您需要AEM作者例項上方的最新AEM Forms附加套件才能使用服務。 如需詳細指示，請參閱<a href="configure-service.md">設定自動表單轉換</a>服務。</p> 
    <br>

1. **此服務是否可在內部部署？**

   <p>Adobe會定期訓練自動表單轉換服務的AI和ML演算法，並提供新的資料集，以提升轉換精度。 更新的演算法會以定期間隔部署至在Adobe Cloud上執行的轉換服務。 服務的所有客戶都從更新的演算法中獲益。 因此，雲端托管的中央部署最適合Automated Forms Conversion服務，以持續學習並改善所有客戶。</p> 
    <p>該服務將空白表單轉換為自適應表單。 此服務不支援填寫表單，也不支援從填寫表單擷取資料。 在將表單傳送至服務進行轉換之前，先從填寫的表單中移除資料，並移除或允許表單中的專屬資訊</p> <br>

1. **此服務是否支援所有格式的PDF表格？支援哪些語言？**

   <p>此服務可將非互動式PDF表單、以XFA為基礎的XDP和PDF表單，以及AcroForms轉換為最適化表單。 服務不支援掃描或填寫的表單。 如需其他限制，請參閱<a href="known-issues.md">已知問題</a>文章。<br /> </p> 
    <p>我們定期新增對其他來源類型的支援。 請將<a href="introduction.md">supportedPDF forms</a>區段保留在您的監視清單上，以定期更新新增的功能和功能。</p>

   此服務僅能將英語表單轉換為最適化表單。 您可以使用[AEM轉換工作流程，將產生的最適化表單翻譯成其他語言。](https://helpx.adobe.com/experience-manager/6-5/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.html)</br> </br>

1. **該服務是否可以生成XDP而不是自適應表單？**

   <p>服務不會生成XDP輸出。 我們會定期在服務中新增功能。 請保留您監看清單上的<a href="introduction.md">支援的語言和PDF表格</a>區段，以定期更新新增的功能。</p> <br>

1. **產生的架構類型為何？**

   <p>您可以使用服務來產生： </p>

   * 系結至JSON結構描述的最適化表單，以及
   * 未綁定到任何模式<br><br>的自適應表單

1. **此服務是否可將Microsoft Word表格轉換為最適化表格？**

   <p>否，服務不會將Microsoft Word表格轉換為最適化表格。 您可以將Microsoft Word表格儲存為PDF表格，並將PDF表格轉換為最適化表格。 整個程式是 </p> <br>

   1. 使用Adobe Acrobat將Word檔案轉換為非互動式PDF[。](https://helpx.adobe.com/acrobat/how-to/create-pdf-files-word-excel-website.html)
   1. 使用Adobe Acrobat將製作的PDF表單轉換為可填寫的PDF表單[。](https://helpx.adobe.com/acrobat/how-to/convert-word-excel-paper-pdf-forms.html)
   1. 使用Adobe Acrobat手動更新和修正表單欄位。
   1. 儲存PDF表格。 現在，您可以搭配轉換服務使用表單來產生最適化表單。 您也可以將表單用作記錄檔案範本。


1. **該服務是否可將掃描的紙本表單和彩色表單轉換為最適化表單？**

   <p>此服務可將彩色PDF表單轉換為最適化表單。 服務不支援掃描或填寫的表單。 如需其他限制，請參閱<a href="known-issues.md">已知問題</a>文章。</p> <br>

1. **該服務是否可將掃描的表單或僅將表單的影像轉換為自適應表單？**

   <p>該服務不支援將掃描的表單或表單的影像轉換為自適應的出廠設定。 但是，您可以使用 Adobe Acrobat 將表單影像轉換為 PDF 表單。 然後，使用本服務將 PDF 表單轉換為最適化表單。 請總是使用高品質的表單影像在 Acrobat 中進行轉換。 這可以提升轉換的品質。</p> <br>

1. **有些以XDP為基礎的表單會使用表單片段，這些表單片段應該上傳到哪裡？**

   <p class="MsoNormal">將表單片段上傳至轉換檔案夾並保留原始檔案夾結構。 它有助於保留XDP型表單和表單片段中使用的相對路徑。</p> <br>

1. **服務是否支援模式綁定的XDP表單？如果我的XDP綁定到模式，我是否需要將模式嵌入到XDP?**

   <p>是的，該服務支援模式綁定的XDP表單，並要求將模式嵌入到源XDP表單中。 當您轉換結構限定的XDP表單時，服務會產生JSON結構描述。 JSON結構類似於來源XDP表單的XSD結構。</p> <br>

1. **服務無法轉換表單。原因何在，如何解決？**
轉換失敗的最常見原因是：
</p>
   * 提供安全的PDF表單以進行轉換。 切勿使用密碼保護或安全的PDF表單進行轉換。
   * 網際網路連線中斷。 確保您在轉換期間已連線至網際網路。
   * 來源PDF的影像為表格，而非實際表格。
   * 服務設定不正確、未提供服務URL，或提供的服務URL不正確。 檢查[服務配置](configure-service.md#configure-the-cloud-service)在&#x200B;**[!UICONTROL AEM]** > **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Automated Forms Conversion configuration]**。
   * IMS設定未正確設定。 對IMS配置執行運行狀況檢查以確保其正常運行。 要檢查IMS配置是否正確：
      1. 前往 `http://[servername]:[port]/libs/cq/adobeims-configuration/content/configurations.html`
      2. 選擇配置。 按一下標題中的&#x200B;**[!UICONTROL Check Health]** ，然後按一下&#x200B;**[!UICONTROL Check]**。 如果成功，您會收到&#x200B;**[!UICONTROL Token retrieved successfully!]**&#x200B;訊息。<br> <br>

1. **使用自訂字型會影響轉換嗎？**

   <p>當非互動式PDF表單轉換為最適化表單時，為了改善轉換品質，字型會內嵌在PDF表單中。 內嵌字型的支援僅限於非互動式PDF表單。 若要最佳化AcroForm和XFA型PDF表單的轉換，請使用備援字型。</p> 
    <p>只有<strong><strong> CQ-DAM-Handler-Gibson Font Manager Service</strong>組態的&lt;a0/&gt;Customer fonts directory</strong>欄位中列出的自訂字型目錄中可用的表單，才會內嵌在非互動式PDF表單中。</p> 
    <p> </p> <br>

1. **本服務是否識別並使用輸出最適化表單中的來源PDF字型？**

   <p>回應式HTML表單的樣式和版面通常與PDF或書面表單不同。 為支援組織內一致的版面配置和樣式，最適化表單使用<a href="https://helpx.adobe.com/experience-manager/6-5/forms/using/themes.html">主題來設定表單的樣式。 </a>轉換服務會使用轉換期間套用之主題中指定的字型和字型樣式。 您可以變更主題的字型和字型樣式，為最適化表單的元件提供獨特的外觀和感覺。</p> <br>

1. **該服務是否會自動從以XDP為基礎的表單擷取JavaScript，並將它套用至對應的最適化表單？**

   <p>該服務不會自動將基於XFA的表單或Acro Forms的指令碼轉換為相應的自適應表單規則。 您(form-authors)可以使用<a href="https://helpx.adobe.com/experience-manager/6-5/forms/using/rule-editor.html">規則編輯器</a>為最適化表單新增互動功能。</p> <br>

1. **有些表單物件無法正確轉換為最適化的表單元件。如何解決問題？**

   <p>自動化表單轉換服務是針對大量表單進行培訓的。 但基於AI/ML的應用程式受其訓練資料和模式的限制。 可能有多種欄位類型、版面、圖樣和內容，人類可以察覺，但難以自動辨識。 服務可能無法識別此類對象或可能識別錯誤。 您可以使用<a href="review-correct-ui-edited.md" target="_blank">Review and Correct</a>編輯器，對輸入表單的版面配置進行必要的修改。</p> <br/>

1. **有些修正會在不同表單間重複。服務能否識別並修正未來轉換中的所有此類例項？**

   此服務可持續地培訓您的表單和模式。 它每天都會學習新的模式。 目前尚未開始自動套用在表單間重複的修正。 請留意搶鮮表單，以取得此類功能。<br/><br/>

   您可以使用元模型將表單物件對應至您選擇的自適應表單元件，並預先設定元件的驗證、規則、資料模式、說明文字和協助工具屬性。 所有指定的屬性都會在轉換期間套用。 您可以使用元模型將常用屬性套用至欄位。 它可協助您減少表單間重複發生的問題。<br/><br/>

1. **有敏感資料(例如個人識別資訊(PII)資訊)的表單有哪些選擇？**
此服務僅支援空白或未填寫的表格。請勿上傳填妥的表單或表單，並附上個人識別資訊(PII)。 此外，移除來源表單中預先填入的資料、個人識別資訊(PII)、機密資訊和專屬資訊。 
<br/>

1. **頁首和頁尾應放在何處？**

   <p>將頁首和頁尾置於最適化表單範本中。 如果來源PDF表單有頁首和頁尾，則服務會在轉換期間，以最適化表單範本中可用的頁首和頁尾來偵測並取代偵測到的頁首和頁尾。 如果最適化表單中包含任何額外的頁首或頁尾，您可以使用<a href="review-correct-ui-edited.md">Review and Correct</a>編輯器來修正或移除此類頁首或頁尾。</p> <br />

1. **與手動規劃、建立資產（主題、範本）、建立和發佈最適化表單的程式相比，服務可節省多少時間？**

   <p>時間長度取決於輸入表單的大小和複雜性以及請求數。 與手動轉換表單的程式相比，本服務希望以更快的速度將PDF表單轉換為可調式表單，大幅縮短實現價值的時間。 </p> <br />

1. **如果遇到與RSA庫相關的錯誤，該怎麼辦？錯誤訊息類似於以下提及的訊息：** <br/>

如果未為RSA/BuncyCastle庫配置引導委託，則會發生上述錯誤。 執行以下步驟以解決問題：   `*ERROR* [0:0:0:0:0:0:0:1 [1565757652491] POST /content/dam/formsanddocuments/demo004.affBatchProcessor.html HTTP/1.1] org.apache.sling.engine.impl.SlingRequestProcessorImpl service: Uncaught Throwable java.lang.NoClassDefFoundError: Could not initialize class com.rsa.cryptoj.o.dl at com.rsa.jsafe.JSAFE_SecureRandom.getInstance(Unknown Source) at com.adobe.internal.pdfm.util.Util.appendRandomNumberToPrefix(Util.java: 169) [com.adobe.aemfd.adobe-aemfd-assembler:6.0.34] at com.adobe.internal.pdfm.logging.JobLog.&amp;lt;init&amp;gt;(JobLog.java:126) [com.adobe.aemfd.adobe-aemfd-assembler:6.0.34]` <br>
如果未為RSA/BuncyCastle庫配置引導委託，則會發生上述錯誤。執行以下步驟以解決問題：
   <p> </p>

   1. 停止AEM例項。 導覽至`[AEM installation directory]\crx-quickstart\conf\`資料夾。 開啟sling.properties檔案以進行編輯。 如果您使用`[AEM installation directory]\crx-quickstart\bin\start.bat`來啟動AEM例項，請編輯位於`[AEM_root]\crx-quickstart\`的sling.properties。
   1. 將下列屬性新增至sling.properties檔案：<br/> `sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*`<br />  `sling.bootdelegation.class.org.bouncycastle.jce.provider.BouncyCastleProvider=org.bouncycastle.*`<br /> `sling.bootdelegation.xerces=org.apache.xerces.*`
   1. 儲存並關閉檔案。<br/>
   1. 啟動AEM例項。<br/>

   <br/>

1. **如何自動變更自適應表單文字的外框？**

   <p>您可以使用主題或樣式編輯器中的自適應格式來更改自適應格式欄位的外框。 例如，您可以開啟主題編輯器，並將表單中所有文字的Case屬性值設為大寫、小寫或camelCase。 您也可以使用主題編輯器中的「CSS覆寫」選項來建立不同的樣式類型。</p>

1. **我是否可搭配Automated Forms Conversion服務使用Adobe Sign文字標籤？**

   <p> 當您使用Automated Forms Conversion Service將PDF表單轉換為最適化表單，而PDF表單具有Adobe Sign文字標籤時，這些標籤會轉換為對應的最適化表單欄位，並自動填入簽署者詳細資訊。  此功能僅適用於Acro Forms，而且最適化表單支援有限數目的Adobe Sign欄位。</p>  </br>

1. **如何建立啟用Adobe Sign的PDF表格？**

   </p>若要建立啟用Adobe Sign的PDF表格：</p>

   將[Adobe Sign文字標籤](https://helpx.adobe.com/sign/using/text-tag.html)新增至欄位名稱，或使用[轉換為Adobe Sign Form](https://helpx.adobe.com/sign/using/create-forms-with-acrobat.html)選項。
