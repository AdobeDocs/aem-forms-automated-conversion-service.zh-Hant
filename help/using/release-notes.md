---
title: 新增功能 發行說明——自動表單轉換服務
description: 瞭解自動表單轉換服務的最新功能及錯誤修正
solution: Experience Manager Forms
feature: Adaptive Forms
topic: Administration
topic-tags: forms
role: Admin, Developer
level: Beginner, Intermediate
exl-id: fccafbc9-28c1-4736-922c-24d675b25213
source-git-commit: e95b4ed35f27f920b26c05f3398529f825948f1f
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 64%

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

## 2022年2月24日(AFC-2022.02.0) {#feb-2022}

* 新增功能，[可自動將區段轉換為片段](convert-existing-forms-to-adaptive-forms.md)，協助改善轉換表單的轉譯速度，並讓在調適型表單編輯器中載入大型表單變得更容易。

## 2021年8月29日(AFC-2021.08.0) {#aug-2021}

* 新增將義大利文和葡萄牙文PDF forms轉換為最適化表單的功能。

## 2021 年 7 月 29 日 (AFC-2021.07.2) {#july-2021}

* 新增將法文、德文和西班牙文PDF表單轉換為最適化表單的功能。

## 2021年6月24日(AFC-2021.06.2) {#june-2021}

### 功能改善 {#june-2021-improvements}

改善自動偵測來源表單中邏輯區段並將這些區段轉換為對應的最適化表單面板的準確性。

## 2021年3月03日(AFC-2021.02.2) {#mar-2021}

### 功能改善 {#march-2021-improvements}

改善將來源表單轉換為最適化表單時，將表單內容組織成選擇群組和欄位。

## 2021年2月02日(AFC-2021.01.2) {#feb-2021}

### 功能改善 {#feb-2021-improvements}

改善將表單內容組織成面板，以及為面板產生標題，同時將來源表單轉換為最適化表單。

## 2020 年 7 月 16 日 (AFC-2020.07.2) {#jul-2020}

### 新增功能 {#whats-new-jul-2020-}

新增將彩色 PDF 表單轉換為最適化表單的功能。

### 功能改善 {#jul-2020-improvements}

改善文字、表單及選擇群組欄位自動轉換至相應的最適化表單元件的功能。

## 2020 年 3 月 20 日 (AFC-2020.03.1) {#mar-2020}

### 搶先體驗 {#early-access}

**自動偵測表單中的邏輯區段**

在預設狀態中，此服務會為 PDF 表單的每一頁分別建立頂層面板。 現在，您可以透過 **[!UICONTROL Auto-detect logical sections]** 選項僅建立邏輯面板，不再建立頁面層級面板（基於頁碼的面板）。 這個選項還可將不屬於任何具有前置邏輯區段之區段的欄位，與橫跨至兩個相鄰頁面的邏輯區段的欄位合併成一個邏輯區段。 例如，如果邏輯區段中有些欄位位於第一頁底部，有些位於第二頁頂部，則所有該欄位都會合併成一個邏輯區段。

### 功能改善 {#mar-2020-improvements}

**改善清單偵測**

現在，此服務可以更有效地偵測有項目符號及編號的清單。

### 特殊說明 {#special-instructions}

**安裝自動表單轉換服務連接工具封裝**

如欲使用AFC-2020.03.1發行版本中提供的最新功能與改善，您需要連線工具封裝1.1.38或更高版本。

如果您已有正常運轉的自動表單轉換服務環境，並欲使用轉換服務的最新功能，請依序安裝最新的服務包、最新的 AEM Forms 附加封裝，與最新的連接工具封裝。 欲知詳細說明，請參閱[設定自動表單轉換服務](configure-service.md)文章。
