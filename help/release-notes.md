---
title: 新功能? 發行說明——自動化表單轉換服務
description: '瞭解Automated Forms Conversion Service的最新功能和修正的錯誤 '
translation-type: tm+mt
source-git-commit: 6d658dbb181c09e42073e328e0232e40d4fb6b58

---


# 自動化表單轉換服務：發行說明

Automated Forms Conversion Service不斷獲得改進。 若要隨時掌握最新動態，請定期造訪本頁。 本頁提供有關以下內容的資訊：

* 最新版本
* 新功能
* 錯誤修正
* 不建議使用的功能
* 特殊指示
* 未來的變更計畫

## 2020年3月20日（亞足聯-2020.03.1）

### 新功能

**自動檢測表單中的邏輯部分**

依預設，服務會針對PDF表單的每一頁建立個別的頂層面板。 現在，您可以使用選 **[!UICONTROL Auto-detect logical sections]** 項來放置頁面層級面板（以頁碼為基礎的面板），並僅建立邏輯面板。  它還會將不屬於任何具有前置邏輯部分的欄位限定為俱樂部。 它還將跨兩個相鄰頁的邏輯部分的欄位限定為單個邏輯部分。 例如，如果某個邏輯部分的某些欄位位於第1頁的末尾，而某些欄位位於第2頁的開頭，則所有這些欄位都會被拖入單個邏輯部分。

### 改進功能

**清單偵測的改進**

這項服務現在在偵測項目清單和編號清單時更有效率。 它現在可輕鬆偵測多層級清單。

### 特殊指示

**安裝Automated Forms Conversion Service Connector套件**

您需要使用1.1.38或更高版本的連接器封裝，才能使用AFC-2020.03.1版中提供的最新功能和改進。您可以從 [AEM Package Share下載連接器套件](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/servicepack/fd/AEM-Forms-6.5.4.0-WIN)。

如果您已安裝並執行Automated Forms Conversion服務環境，若要使用轉換服務的最新功能，請依上述順序安裝最新的服務套件、最新的AEM Forms附加套件和最新的連接器套件。 如需詳細指示，請參 [閱設定自動表單轉換服務](configure-service.md) 。
