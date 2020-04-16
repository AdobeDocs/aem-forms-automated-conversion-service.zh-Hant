---
title: '疑難排解自動化表單轉換服務 '
seo-title: '疑難排解Automated Forms Conversion Service(AFCS) '
description: '常見的AFCS問題及解決方案 '
seo-description: 常見的AFCS問題及解決方案
contentOwner: khsingh
topic-tags: forms
translation-type: tm+mt
source-git-commit: 4b9f3f4fe3b3901cb99c9374ff40e8f49855237f

---


# 疑難排解自動化表單轉換服務


文章提供有關Automated Forms Conversion Service生產環境中可能出現的安裝、配置和管理問題的資訊。 本檔案也提供常見錯誤訊息的基本疑難排解步驟和說明。

## 常見錯誤 {#commonerrors}

| 錯誤 | 範例 |
|--- |--- |
| **錯誤訊息**<br> ：存取Token標題無法使用。 <br><br>**原因&#x200B;**<br>管理員已建立多個IMS設定，或IMS設定無法在Adobe Cloud上存取AFCS服務。<br><br>**解析度**<br> ：如果有多個配置，請刪除所有配置並 [建立新配置](configure-service.md#obtainpubliccertificates)。 <br> 如果有單一配置，請使用 **[!UICONTROL Health Check]** 檢查 [連接性](configure-service.md#createintegrationoption)。 | ![存取Token標題無法使用](assets/invalid-ims-configuration.png) |
| **錯誤消息**<br> ：無法連接到服務。  <br><br>**原因&#x200B;**<br>「自動化表單轉換服務」雲端服務中提及錯誤的服務URL或沒有服務URL。<br><br>**解析度**<br>[](configure-service.md#configure-the-cloud-service) Automated Forms Conversion Service Cloud服務中的正確服務URL。 | ![無法連線至服務。](assets/wrong-endpoint-configured.png) |
| **錯誤消息**<br> ：服務無法轉換表單。  <br><br>**原因&#x200B;**<br>：您端的網路連線問題，或由於Adobe Cloud的排程維護或中斷，服務中斷。<br><br>**解決**<br> ：解決您端的網路連接問題，並在https://status.adobe.com/上檢查服務的狀態，以瞭解計畫內或計畫外停機。 | ![無法連線至服務。](assets/service-failure.png) |
| **錯誤訊息**<br> ：頁數超過15個。  <br><br>**原因&#x200B;**<br>：包含來源XDP和PDF表單的資料夾有15個以上的檔案。<br><br>**解析度**<br> ：將資料夾中的表單數量調整為小於或等於15。 將資料夾中的頁數總計放入小於50的資料夾。 將資料夾的大小調整到小於10 MB。 請勿將表單保留在子資料夾中。 將來源檔案整理成8-15份檔案。 | ![無法連線至服務。](assets/number-of-pages.png) |
| **錯誤消息**<br> ：不支援源檔案格式。  <br><br>**原因&#x200B;**<br>：包含源表單的資料夾包含一些不支援的檔案。<br><br>**解析度**<br> ：服務僅支援。xdp和。pdf檔案。 從資料夾移除具有任何其他副檔名的檔案，然後執行轉換。 | ![無法連線至服務。](assets/unsupported-file-formats.png) |
| **不支援錯誤消息**<br> 「掃描的表單」。  <br><br>**原因&#x200B;**<br>PDF表單只包含表單的掃描影像，不包含任何內容結構。<br><br>**解析度**<br> ：服務不支援將掃描的表單或表單的影像轉換為可調整的現成功能。 不過，您使用Adobe Acrobat將表單的影像轉換為PDF表單。 然後，使用服務將PDF表單轉換為最適化表單。 在Acrobat中，請務必使用高品質的表單影像進行轉換。 它改善了轉換的品質。 | ![無法連線至服務。](assets/scanned-forms-error.png) |