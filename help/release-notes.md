---
title: 新增功能 發行說明——自動表單轉換服務
description: '瞭解自動表單轉換服務的最新功能及錯誤修正 '
translation-type: tm+mt
source-git-commit: caa019d1a7dd1968a52df5ec5be4755e1c6c4ee6
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 94%

---


# 發行說明

自動表單轉換服務不斷改善。 如欲瞭解最新發展，請定期造訪此頁面。 此頁面內含下列資訊：

* 搶先體驗
* 最新版本
* 新功能
* 改善
* 錯誤修正
* 已棄用功能
* 特殊說明
* 未來變更計劃


## 2020年7月16日(AFC-2020.07.0)

### 功能改善

文字、表單和選擇群組欄位自動轉換至對應最適化表單元件的改進。

## 2020 年 3 月 20 日 (AFC-2020.03.1)

### 搶先體驗

**自動偵測表單中的邏輯區段**

在預設狀態中，此服務會為 PDF 表單的每一頁分別建立頂層面板。 現在，您可以透過 **[!UICONTROL Auto-detect logical sections]** 選項僅建立邏輯面板，不再建立頁面層級面板（基於頁碼的面板）。 這個選項還可將不屬於任何具有前置邏輯區段之區段的欄位，與橫跨至兩個相鄰頁面的邏輯區段的欄位合併成一個邏輯區段。 例如，如果邏輯區段中有些欄位位於第一頁底部，有些位於第二頁頂部，則所有該欄位都會合併成一個邏輯區段。

### 功能改善

**改善清單偵測**

現在，此服務可以更有效地偵測有項目符號及編號的清單。

### 特殊說明

**安裝自動表單轉換服務連接工具封裝**

如欲使用 AFC-2020.03.1 版本中提供的最新功能與改善，您需要連接工具封裝 1.1.38 版本或更高。您可以於 [AEM 封裝共用](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/featurepack/AFCS-Connector-2020.03.1)下載連接工具封裝。

如果您已有正常運轉的自動表單轉換服務環境，並欲使用轉換服務的最新功能，請依序安裝最新的服務包、最新的 AEM Forms 附加封裝，與最新的連接工具封裝。 欲知詳細說明，請參閱[設定自動表單轉換服務](configure-service.md)文章。