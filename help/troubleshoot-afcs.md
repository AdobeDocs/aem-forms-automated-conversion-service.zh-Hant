---
title: '疑難排解自動化表單轉換服務 '
seo-title: '疑難排解Automated Forms Conversion Service(AFCS) '
description: '常見的AFCS問題及解決方案 '
seo-description: 常見的AFCS問題及解決方案
contentOwner: khsingh
topic-tags: forms
translation-type: tm+mt
source-git-commit: 535267e20fb8e583e1c01f4160be378ffd31a4a4

---


# 疑難排解自動化表單轉換服務


<!--The article provides information on installation, configuration and administration issues that may arise in an Automated Forms Conversion Service production environment. --> The document  provides basic troubleshooting steps for common errors.

## 常見錯誤 {#commonerrors}

| 錯誤 | 範例 |
|--- |--- |
| **錯誤訊息**<br> ：存取Token標題無法使用。 <br><br>**原因&#x200B;**<br>管理員已建立多個IMS設定，或IMS設定無法在Adobe Cloud上存取AFCS服務。<br><br>**解析度**<br> ：如果有多個配置，請刪除所有配置並 [建立新配置](configure-service.md#obtainpubliccertificates)。 <br> 如果有單一配置，請使 **[!UICONTROL Health Check]** 用 [檢查連接](configure-service.md#createintegrationoption)。 | ![存取Token標題無法使用](assets/invalid-ims-configuration.png) |
| **錯誤消息**<br> ：無法連接到服務。  <br><br>**原因&#x200B;**<br>「自動化表單轉換服務」雲端服務中提及錯誤的服務URL或沒有服務URL。<br><br>**解析度**<br>[](configure-service.md#configure-the-cloud-service) Automated Forms Conversion Service Cloud服務中的正確服務URL。 | ![無法連線至服務。](assets/wrong-endpoint-configured.png) |
| **錯誤消息**<br> ：服務無法轉換表單。  <br><br>**原因&#x200B;**<br>：您端的網路連線問題、服務因Adobe Cloud的排程維護或中斷而中斷。<br><br>**解決**<br> ：解決您端的網路連接問題，並在https://status.adobe.com/上檢查服務的狀態，以發現計畫內或計畫外停機。 | ![無法連線至服務。](assets/service-failure.png) |
| **錯誤訊息**<br> ：頁數超過15頁。  <br><br>**原因&#x200B;**<br>：來源表單長度超過15頁。<br><br>**解析度**<br> ：使用Adobe Acrobat分割超過15頁的表單。 將表單中的頁數調整為少於15個。 | ![無法連線至服務。](assets/number-of-pages.png) |
| **錯誤訊息**<br> ：檔案數目超過15個。  <br><br>**原因&#x200B;**<br>資料夾包含15種以上表格。<br><br>**解析度**<br> ：將資料夾中的表單數量調整為小於或等於15。 將資料夾中的頁數總計放入小於50的資料夾。 將資料夾的大小調整到小於10 MB。 請勿將表單保留在子資料夾中。 將來源表單組織成一組8-15個表單。 | ![無法連線至服務。](assets/number-of-pages.png) |
| **錯誤消息**<br> ：不支援源檔案格式。  <br><br>**原因&#x200B;**<br>：包含源表單的資料夾包含一些不支援的檔案。<br><br>**解析度**<br> ：服務僅支援。xdp和。pdf檔案。 從資料夾移除具有任何其他副檔名的檔案，然後執行轉換。 | ![無法連線至服務。](assets/unsupported-file-formats.png) |
| **不支援錯誤消息**<br> 「掃描的表單」。  <br><br>**原因&#x200B;**<br>PDF表單只包含表單的掃描影像，不包含任何內容結構。<br><br>**解析度**<br> ：服務不支援將掃描的表單或表單的影像轉換為可調整的現成功能。 不過，您使用Adobe Acrobat將表單的影像轉換為PDF表單。 然後，使用服務將PDF表單轉換為最適化表單。 在Acrobat中，請務必使用高品質的表單影像進行轉換。 它改善了轉換的品質。 | ![無法連線至服務。](assets/scanned-forms-error.png) |
| **不支援錯誤訊息**<br> 「加密的PDF」表單。  <br><br>**原因&#x200B;**<br>資料夾包含加密的PDF表單。<br><br>**解析度**<br> ：服務不支援將加密的PDF表單轉換為最適化表單。 移除加密、上傳未加密的表單，然後執行轉換。 | ![無法連線至服務。](assets/secured-pdf-form.png) |
| **錯誤訊息**<br> ：無法剖析中繼模型JSON結構描述。  <br><br>**原因&#x200B;**<br>：提供給服務的JSON結構描述格式不正確、包含無效字元，或使用無效語法來映射元件。<br><br>**解析度**<br> ：檢查JSON檔案的格式。 您可以使用任何線上JSON驗證器來檢查架構的格式和結構。 如需元 [](extending-the-default-meta-model.md) 模型語法的相關資訊，請參閱擴充預設元模型文章。 | ![無法連線至服務。](assets/invalid-meta-model-schema.png) |
