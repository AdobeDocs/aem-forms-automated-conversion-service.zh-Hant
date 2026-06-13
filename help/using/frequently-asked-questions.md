---
title: 常見問題
description: 常見查詢或常見問題
solution: Experience Manager Forms
feature: Adaptive Forms
topic: Administration
topic-tags: introduction
role: Admin, Developer
level: Beginner, Intermediate
exl-id: 3a29f8d4-8ea0-49eb-bfe0-0eab5f0c52c7
TQID: https://experienceleague.adobe.com/yp0Kt5IApys-pqUHzqYJlzY9zhMg7z26v-bB0Fp9fjI
product_v2:
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
feature_v2:
  - id: d49d6117-dd89-469c-a774-cc96b7eee433
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: cc72dcf1-72e1-48cc-b434-e7c27d62d67c
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 0be767cc3d09331ea7a61c114a11bb0354b5f4ad
workflow-type: tm+mt
source-wordcount: 1830
ht-degree: 4%

---

# 常見問題{#frequently-asked-questions}

1. **自動錶單轉換服務(AFCS)支援哪個AEM Forms版本？**
   <p>自動錶單轉換服務(AFCS)支援AEM 6.5 Forms、AEM 6.5 LTS Forms和AEM Forms as a Cloud Service。 它適用於OSGi上的AEM Forms和JEE上的AEM表單。 針對AEM 6.5和AEM 6.5 LTS，您需要在AEM製作執行個體之上最新AEM Forms附加套件，並且如果您想要使用核心元件型範本和主題，必須<a href="https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-core-components/enable-adaptive-forms-core-components.html?lang=zh-Hant">啟用調適型表單核心元件</a>。 如需詳細指示，請參閱<a href="configure-service.md">設定自動錶單轉換</a>服務。</p> 
    <br>

1. **是否可以在內部部署安裝服務？**
   <p>Adobe會定期使用新資料集訓練自動錶單轉換服務(AFCS)的AI和ML演演算法，以改善轉換準確性。 更新後的演演算法會定期部署至Adobe Cloud上執行的轉換服務。 此服務的所有客戶都受益於更新的演演算法。 因此，雲端主控的中央部署最適合自動化表單轉換服務(AFCS)，以便持續學習並提供改良給所有客戶。</p> 
    <p>此服務會將空白表單轉換為最適化表單。 此服務不支援填寫的表單，以及從填寫的表單中擷取資料。 將表單傳送至服務進行轉換之前，請先從已填寫的表單中移除資料，並從表單中移除或允許列出專屬資訊</p> <br>

1. **此服務是否支援所有PDF forms格式？ 支援哪些所有語言？**
   <p>此服務可將非互動式PDF forms、XFA型XDP和PDF forms以及AcroForms轉換為最適化表單。 此服務不支援掃描或填寫的表單。 如需其他限制，請參閱<a href="known-issues.md">已知問題</a>文章。<br /> </p> 
    <p>我們定期新增對其他來源型別的支援。 將<a href="introduction.md">supportedPDF forms</a>區段保留在您的監看清單中，以定期更新新增的功能。</p>

   此服務只能將英文、法文、德文、西班牙文、義大利文和葡萄牙文的表單轉換為最適化表單。 您可以使用[AEM翻譯工作流程將產生的自適應表單翻譯成其他語言。](https://helpx.adobe.com/tw/experience-manager/6-5/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.html)</br> </br>

1. **服務是否可產生XDP而非最適化表單？**
   <p>此服務未產生XDP輸出。 我們定期為服務新增功能與功能。 將<a href="introduction.md">支援的語言和PDF forms</a>區段保留在關注清單上，以定期更新新新增的功能。</p> <br>

1. **產生的結構描述型別為何？**
   <p>您可以使用服務來產生： </p>

   * 與JSON結構描述繫結的調適型表單，以及
   * 未繫結至任何結構描述<br><br>的最適化表單

1. **此服務是否可將Microsoft Word表單轉換為最適化表單？**
   <p>否，此服務無法將Microsoft Word表單轉換為最適化表單。 您可以將Microsoft Word表單儲存至PDF表單，並將PDF表單轉換為最適化表單。 完整的程式為 </p> <br>

   1. 使用Adobe Acrobat將Word檔案[轉換為非互動式PDF](https://helpx.adobe.com/tw/acrobat/how-to/create-pdf-files-word-excel-website.html)。
   1. 使用Adobe Acrobat將[產生的PDF forms轉換為可填寫的PDF表單](https://helpx.adobe.com/tw/acrobat/how-to/convert-word-excel-paper-pdf-forms.html)。
   1. 使用Adobe Acrobat手動更新和修正表單欄位。
   1. 儲存PDF表單。 現在，您可以將此表單與轉換服務搭配使用，以產生最適化表單。 您也可以使用表單作為記錄檔案範本。


1. **此服務是否可將掃描的紙張表單及彩色表單轉換為最適化表單？**
   <p>此服務可將色彩PDF forms轉換為最適化表單。 此服務不支援掃描或填寫的表單。 如需其他限制，請參閱<a href="known-issues.md">已知問題</a>文章。</p> <br>

1. **此服務是否可以將掃描的表單或僅表單影像轉換為最適化表單？**
   <p>此服務無法直接將掃描後的表單或表單影像轉換為最適化表單。 但是，您可以使用 Adobe Acrobat 將表單影像轉換為 PDF 表單。 然後，使用本服務將 PDF 表單轉換為最適化表單。 請總是使用高品質的表單影像在 Acrobat 中進行轉換。 這可以提升轉換的品質。</p> <br>

1. **某些以XDP為基礎的表單會使用表單片段，這些表單片段應該上傳到哪裡？**
   <p class="MsoNormal">將表單片段上傳到轉換資料夾並保留原始資料夾結構。 它有助於保留在XDP型表單和表單片段中使用的相對路徑。</p> <br>

1. **服務是否支援結構描述繫結的XDP表單？ 如果我有XDP繫結至結構描述，是否需要將結構描述內嵌至XDP？**
   <p>是，此服務支援結構描述繫結的XDP表單，並要求將結構描述內嵌到來源XDP表單中。 當您轉換結構描述繫結的XDP表單時，服務會產生JSON結構描述。 JSON結構描述在結構上與來源XDP表單的XSD結構描述類似。</p> <br>

1. **服務無法轉換表單。問題的原因及解決方式？**
轉換失敗的最常見原因是：</p>
   * 轉換時提供安全的PDF forms。 請勿使用受密碼保護或安全的PDF forms進行轉換。
   * 網際網路連線已中斷。 請確認您在轉換期間已連線至網際網路。
   * Source PDF有表單的影像，而非實際表單。
   * 服務設定不正確、未提供服務URL，或提供的服務URL不正確。 在&#x200B;**[!UICONTROL AEM]** > **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Automated Forms Conversion configuration]**&#x200B;檢查[服務組態](configure-service.md#configure-the-cloud-service)。
   * IMS設定未正確設定。 對IMS設定執行健康狀態檢查以確保其正常運作。 若要檢查IMS設定是否正確：
      1. 前往`http://[servername]:[port]/libs/cq/adobeims-configuration/content/configurations.html`
      2. 選取設定。 按一下標題中的&#x200B;**[!UICONTROL Check Health]**，然後按一下&#x200B;**[!UICONTROL Check]**。 如果成功，您會收到&#x200B;**[!UICONTROL Token retrieved successfully!]**&#x200B;訊息。<br> <br>

1. **使用自訂字型是否會影響轉換？**
   <p>當非互動式PDF表單轉換為最適化表單時，為了改善轉換品質，字型會嵌入到PDF表單中。 僅限非互動式PDF forms支援內嵌字型。 為了最佳化AcroForm和XFA型PDF forms的轉換，使用遞補字型。</p> 
    <p><strong> CQ-DAM-Handler-Gibson Font Manager Service</strong>設定的<strong>Customer fonts目錄</strong>欄位中所列的自訂字型目錄中只有可用的表單會內嵌在非互動式PDF表單中。</p> 
    <p> </p> <br>

1. **此服務是否會在輸出的最適化表單中識別並使用來源PDF的字型？**
   <p>回應式HTML表單的樣式和版面配置通常與PDF或書面表單不同。 為了支援跨組織的一致版面配置和樣式，最適化表單使用<a href="https://helpx.adobe.com/tw/experience-manager/6-5/forms/using/themes.html">主題來設定表單</a>的樣式。 轉換服務會使用轉換期間套用之主題中指定的字型和字型樣式。 您可以變更佈景主題的字型和字型樣式，為最適化表單的元件提供獨特的外觀和風格。</p> <br>

1. **此服務是否自動從XDP式表單中擷取JavaScript，並將其套用至對應的調適型表單？**
   <p>此服務不會自動將XFA型表單或Acro Forms的指令碼轉換為對應的調適型表單規則。 您（表單作者）可以使用<a href="https://helpx.adobe.com/tw/experience-manager/6-5/forms/using/rule-editor.html">規則編輯器</a>將互動性新增至最適化表單。</p> <br>

1. **部分表單物件未正確轉換為最適化表單元件。 如何解決問題？**
   <p>自動化表單轉換服務(AFCS)已接受大量表單的訓練。 但AI/ML型應用程式受到訓練資料和模式的限制。 可能有多種欄位型別、版面配置、模式及上下文可供人類感知識別，但難以進行自動辨識。 服務可能無法識別這類物件，或可能無法正確識別它們。 您可以使用<a href="review-correct-ui-edited.md" target="_blank">檢閱並修正</a>編輯器，在熟悉的書面表單式輸入表單版面配置中進行必要的修改。</p> <br/>

1. **表格間會重複某些更正。 此服務可以在未來的轉換中識別並修正所有這類執行個體嗎？**

   此服務會持續針對您的表單和模式提供訓練。 它會每天學習新模式。 尚未開始自動套用表單上重複的更正。 請留意發行前表單，瞭解這類功能的可用性。<br/><br/>

   您可以使用中繼模型將表單物件對應至您選擇的最適化表單元件，並預先設定元件的驗證、規則、資料模式、說明文字和協助工具屬性。 所有指定的屬性都會在轉換期間套用。 您可以使用中繼模型來套用一般屬性至欄位。 它可以協助您減少表單間的一些重複問題。<br/><br/>

1. **具有敏感資料(例如個人識別資訊(PII)資訊)的表單有哪些選項？**
此服務僅支援空白或未填寫的表單。請勿上傳含有個人識別資訊(PII)的已填表格或表單。此外，請移除來源表單中預先填入的資料、個人識別資訊(PII)、機密與專屬資訊。<br/>

1. **頁首和頁尾應該放在哪裡？**
   <p>在最適化表單範本中放置頁首和頁尾。 如果來源PDF表單有頁首和頁尾，服務會在轉換期間以適用性表單範本中可用的頁首和頁尾偵測並取代偵測到的頁首和頁尾。 如果最適化表單中包含任何額外的頁首或頁尾，您可以使用<a href="review-correct-ui-edited.md">檢閱和修正</a>編輯器來修正或移除此類頁首或頁尾。</p> <br />

1. **與手動規劃、建立資產（主題、範本）、建立及發佈最適化表單的流程相比，此服務可節省多少時間？**
   <p>時間長短取決於輸入表單的大小和複雜性，以及請求數量。 此服務旨在透過以快得多的速度將PDF forms轉換為最適化表單，大幅縮短實現價值的時間，而不是以手動方式轉換表單。 </p> <br />

1. **如果我遇到與RSA資料庫相關的錯誤，該怎麼辦？錯誤訊息類似於以下提及的訊息：** <br/>
   `*ERROR* [0:0:0:0:0:0:0:1 [1565757652491] POST /content/dam/formsanddocuments/demo004.affBatchProcessor.html HTTP/1.1] org.apache.sling.engine.impl.SlingRequestProcessorImpl service: Uncaught Throwable java.lang.NoClassDefFoundError: Could not initialize class com.rsa.cryptoj.o.dl at com.rsa.jsafe.JSAFE_SecureRandom.getInstance(Unknown Source) at com.adobe.internal.pdfm.util.Util.appendRandomNumberToPrefix(Util.java: 169) [com.adobe.aemfd.adobe-aemfd-assembler:6.0.34] at com.adobe.internal.pdfm.logging.JobLog.&amp;lt;init&amp;gt;(JobLog.java:126) [com.adobe.aemfd.adobe-aemfd-assembler:6.0.34]` <br>
未針對RSA/BouncyCastle程式庫設定開機委派時，會發生上述錯誤。執行以下步驟以解決問題：
   <p> </p>

   1. 停止AEM執行個體。 導覽至 `[AEM installation directory]\crx-quickstart\conf\` 檔案夾。 開啟sling.properties檔案進行編輯。 如果您使用`[AEM installation directory]\crx-quickstart\bin\start.bat`啟動AEM執行個體，請編輯位於`[AEM_root]\crx-quickstart\`的sling.properties。
   1. 將下列屬性新增至sling.properties檔案： <br/> `sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*`<br />  `sling.bootdelegation.class.org.bouncycastle.jce.provider.BouncyCastleProvider=org.bouncycastle.*`<br /> `sling.bootdelegation.xerces=org.apache.xerces.*`
   1. 儲存並關閉檔案。<br/>
   1. 啟動AEM執行個體。<br/>
   <br/>

1. **如何自動變更最適化表單文字的大小寫？**
   <p>您可以使用主題或樣式編輯器的最適化來變更最適化表單欄位的大小寫。 例如，您可以開啟主題編輯器，並將表單所有文字的Case屬性值設定為大寫、小寫或駝峰式大小寫。 您也可以使用主題編輯器中的「CSS覆寫」選項來建立不同型別的樣式。</p>

1. **我可以搭配Automated Forms Conversion Service (AFCS)使用Adobe Sign文字標籤嗎？**
   <p> 當您使用自動錶單轉換服務(AFCS)將PDF表單轉換為最適化表單，且PDF表單具有Adobe Sign文字標籤時，這些標籤會轉換為對應的最適化表單欄位，且簽署者詳細資料會自動填入。  此功能僅適用於Acro Forms，且調適型表單支援有限數量的Adobe Sign欄位。</p>  </br>

1. **如何建立啟用Adobe Sign的PDF表單？**
   </p>若要建立啟用Adobe Sign的PDF表單：</p>

   新增[Adobe Sign文字標籤](https://helpx.adobe.com/tw/sign/using/text-tag.html)至欄位名稱或使用[轉換成Adobe Sign表單](https://helpx.adobe.com/tw/sign/using/create-forms-with-acrobat.html)選項。

