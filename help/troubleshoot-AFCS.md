---
title: '疑難排解自動化表單轉換服務 '
seo-title: '疑難排解Automated Forms Conversion Service(AFCS) '
description: '常見的AFCS問題及解決方案 '
seo-description: 常見的AFCS問題及解決方案
contentOwner: khsingh
topic-tags: forms
translation-type: tm+mt
source-git-commit: aebfde420d02bd4184022ecb42496a379d66a3b5

---


# 疑難排解自動化表單轉換服務


文章提供有關Automated Forms Conversion Service生產環境中可能出現的安裝、配置和管理問題的資訊。 本檔案也提供常見錯誤訊息的基本疑難排解步驟和說明。

### 常見錯誤 {#commonerrors}

| 錯誤 | 範例 |
|--- |--- |
| **錯誤訊息**<br> ：存取Token標題無法使用。 <br><br>**原因&#x200B;**<br>管理員已建立多個IMS設定，或IMS設定無法在Adobe Cloud上存取AFCS服務。<br><br>**解析度**<br> ：如果有多個配置，請刪除所有配置並 [建立新配置](configure-service.md#obtainpubliccertificates)。 <br> 如果有單一配置，請使用 **[!UICONTROL Health Check]** 檢查 [連接性](configure-service.md#createintegrationoption)。 | ![彩色表格](assets/invalid-ims-configuration.png) |
| **錯誤消息**<br> ：無法連接到服務。  <br><br>**原因&#x200B;**<br>「自動化表單轉換服務」雲端服務中提及錯誤的服務URL或沒有服務URL。<br><br>**解析度**<br>[](configure-service.md#configure-the-cloud-service) Automated Forms Conversion Service Cloud服務中的正確服務URL。 | ![彩色表格](assets/wrong-endpoint-configured.png) |
