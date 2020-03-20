---
title: 新功能? 發行說明——自動化表單轉換服務
description: '瞭解Automated Forms Conversion Service的最新功能和修正的錯誤 '
translation-type: tm+mt
source-git-commit: 01dfd20951314017d47713bfb1a2a5f2d563f434

---


# 自動化表單轉換服務：發行說明

Automated Forms Conversion Service不斷獲得改進。 若要隨時掌握最新動態，請定期造訪本頁。 本頁提供有關以下內容的資訊：

* 最新版本
* 新功能
* 錯誤修正
* 不建議使用的功能
* 特殊指示
* 未來變更計畫

本頁面會每月更新，請定期重新造訪。

## 2020年3月20日（亞足聯-2020.03.1）

### 新功能

**自動檢測表單中的邏輯部分**

依預設，服務會針對輸入PDF表單的每一頁建立個別的頂層面板。 現在，您可以選取 **[!UICONTROL Auto-detect logical sections]** 選項來移除為每個PDF頁面建立個別頂層面板並自動偵測邏輯區段的概念。 服務俱樂部將表單的欄位與邏輯部分相關。 例如，與開單地址相關的所有欄位都被拖到一個區域，而與發運地址相關的所有欄位被拖到另一個區域。 服務還為每個自動檢測到的邏輯部分建立一個單獨的頂層面板。

### 改進功能

**清單偵測的改進**

這項服務現在在偵測項目清單和編號清單時更有效率。 它現在可輕鬆偵測多層級清單。

### 特殊指示

**安裝Automated Forms Conversion Service Connector套件**

您需要使用1.1.38或更高版本的連接器封裝，才能使用AFC-2020.03.1版中提供的最新功能和改進。您可以從 [AEM Package Share下載連接器套件](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/servicepack/fd/AEM-Forms-6.5.4.0-WIN)。

如果您已安裝並執行Automated Forms Conversion服務環境，若要使用轉換服務的最新功能，請依上述順序安裝最新的服務套件、最新的AEM Forms附加套件和最新的連接器套件。 如需詳細指示，請參 [閱設定自動表單轉換服務](configure-service.md) 。
