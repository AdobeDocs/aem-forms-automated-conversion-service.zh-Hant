---
title: automated forms conversion服務(AFCS)簡介
description: 將列印表單加速轉換為最適化表單
solution: Experience Manager Forms
feature: Adaptive Forms, Foundation Components
topic: Administration
topic-tags: forms
role: Admin, Developer
level: Beginner, Intermediate
exl-id: edabeac8-cd66-48ca-a99f-9643a1c184cf
source-git-commit: c2392932d1e29876f7a11bd856e770b8f7ce3181
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 58%

---

# automated forms conversion服務(AFCS) {#introduction-to-automated-forms-conversion-service}

automated forms conversion服務(AFCS)可將PDF forms自動轉換為最適化表單，協助加速資料擷取體驗的數位化和現代化。 這項由 Adobe Sensei 支援的服務會將您的 PDF 表單自動轉換為適合裝置、回應式且基於 HTML5 的最適化表單。 妥善利用現有的 PDF Forms 和 XFA 功能，該服務還可以在轉換過程中將適當的驗證、樣式和佈局應用於最適化表單欄位。 此服務的好處：

* 無須手動將列印表單轉換為最適化表單
* 在轉換過程中應用模式和適當的驗證
* 在轉換過程中生成記錄文件
* 將常見欄位分組為可重複使用的表單片段
* 在轉換過程中啟用 Adobe Analytics

![這相當容易。 您提供源表單，接下來交給我們所有內容。 我們為您提供美觀的最適化表單。 您可以隨時修改成果以致完美。](assets/pdf-to-adaptive-form-gitx50.gif)

## 上線 {#onboarding}

AEM 6.4 Forms和AEM 6.5 Forms內部部署定期客戶和Adobe管理服務企業客戶可免費使用該服務。 您可以聯絡Adobe銷售團隊或您的Adobe代表，要求存取該服務。 AEM Formsas a Cloud Service客戶也可以免費使用此服務並預先啟用該服務。

Adobe 為您的組織啟用存取權限，並向您指定的組織管理員提供所需的特權。 管理員可以授予組織的 AEM Forms 開發人員（使用者）存取權限以連接到該服務。 欲知詳情，請參閱[設定自動表單轉換服務](configure-service.md)。

## 支援的PDF forms和語言 {#supported-languages-and-pdf-forms}

此服務支援非互動式 PDF 表單、使用 Adobe Acrobat 建立的名為 AcroForms 的表單，以及使用 AEM Forms 或 Adobe LiveCycle 建立的基於 XFA 的表單。

此服務也支援啟用Adobe Sign的PDF forms。 如果源 PDF 表單有 Adobe Sign 文字標記，則此服務會保留轉換期間所有 Adobe Sign 的相關資訊，並將源 PDF 中顯示的簽署者資訊與對應的最適化表單欄位建立關聯。 此功能僅適用於 AcroForms。

此服務可將英文、法文、德文、西班牙文、義大利文和葡萄牙文的表單轉換為最適化表單。 您也可以使用[AEM翻譯工作流程](https://helpx.adobe.com/experience-manager/6-5/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.html)將產生的自適應表單翻譯成其他語言。

## 轉換工作流程  {#conversion-workflow}

automated forms conversion服務(AFCS)會在Adobe雲端上執行。 您將 AEM 執行個體連接到服務，並將表單上傳到 AEM 執行個體後，即可開始轉換。 完整的轉換過程如下所列：

![工作流程](assets/conversion-workflow.png)

### 1.設定環境 {#set-up-the-environment}

automated forms conversion服務(AFCS)會在Adobe雲端上執行。 [設定您組織的 Adobe I/O 帳戶，並將您本端的 AEM 執行個體連接](configure-service.md)至 Adobe Cloud 上運行的轉換服務。

### 2.將PDF forms轉換為最適化表單 {#use-the-conversion-service}

設定 AEM Forms 環境後，如欲將 PDF 表單轉換為最適化表單，請 [上傳 PDF 表單](convert-existing-forms-to-adaptive-forms.md)至 AEM 執行個體，然後[開始轉換](convert-existing-forms-to-adaptive-forms.md#run-the-conversion)。 在上傳表單前，請參閱以下提醒：

* 請勿上傳受保護的表單。 此服務無法轉換受密碼保護和加密的表單。
* 請勿上傳英文、法文、德文、西班牙文、義大利文和葡萄牙文以外任何語言的掃描、彩色、已填寫表單和表單。 此服務不支援這些表單。
* 請勿上傳檔案名中帶有空格的 PDF 表單。
* 請勿上傳 [PDF Portfolio](https://helpx.adobe.com/acrobat/using/overview-pdf-portfolios.html)。 此服務無法將PDFPortfolio轉換為最適化表單。
* 完成[最佳實務和考量](styles-and-pattern-considerations-and-best-practices.md)文章中描述的 PDF 表單的建議更改。
* 閱讀[已知問題](known-issues.md)文章以避免犯錯。

### 3.檢閱轉換後的表單 {#review-converted-forms}

現實世界的表單在欄位佈局、命名或內隱建議方面可能具有複雜的資料擷取要求，而基於AI/ML的檢測邏輯可能無法準確擷取這些表單。 自動轉換完成後，您可以使用[檢閱和修正編輯器](review-correct-ui-edited.md)來檢查轉換後的表格並進行必要的更新，使成果更佳並更能提供符合期望的體驗。 完成必要的修改後，再一次轉換表單。

自動轉換所需的時間取決於多種因素，例如輸入表單的大小、表單的複雜性，以及服務處理佇列上所缺的時間。 使用者可透過資料夾 / 檔案上的狀態顯示器時時瞭解進度。 轉換完成後，使用者設定的電子郵件地址也會收到電子郵件通知。
