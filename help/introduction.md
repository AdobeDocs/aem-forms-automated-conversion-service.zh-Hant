---
title: 簡介
description: '將列印表單加速轉換為最適化表單 '
translation-type: tm+mt
source-git-commit: ceff5cb56aa9896a28004628c5e26c262b7918bd

---


# 簡介 {#introduction-to-automated-forms-conversion-service}

「自動表單轉換」服務可透過將 PDF 表單自動轉換為最適化表單，協助加速資料擷取體驗的數位化和現代化。 這項由 Adobe Sensei 支援的服務會將您的 PDF 表單自動轉換為適合裝置、回應式且基於 HTML5 的最適化表單。 妥善利用現有的 PDF Forms 和 XFA 功能，該服務還可以在轉換過程中將適當的驗證、樣式和佈局應用於最適化表單欄位。 此服務的好處：

* 無須手動將列印表單轉換為最適化表單
* 在轉換過程中應用模式和適當的驗證
* 在轉換過程中生成記錄文件
* 將常見的欄位分組為可再使用的表單片段
* 在轉換過程中啟用 Adobe Analytics

![這相當容易。 您只需提供源表單，接下來交給我們就可以了。 我們將向您呈現美觀的最適化表單。 當然，您也可以修改成果以致完美。 ](assets/pdf-to-adaptive-form-gitx50.gif)

## 入門 {#onboarding}

此服務可免費提供給AEM 6.4 Forms和AEM 6.5 Forms On-Premise客戶和Adobe Managed Service企業客戶。 您可以聯絡 Adobe Sales 團隊或您的 Adobe 代表，請求存取該服務。

Adobe 為您的組織啟用存取權限，並向您指定的組織管理員提供所需的特權。 管理員可以授予組織的 AEM Forms 開發人員（使用者）存取權限以連接到該服務。 欲知詳情，請參閱[設定自動表單轉換服務](configure-service.md)。

## 支援的 PDF 表單和語言{#supported-languages-and-pdf-forms}

此服務支援非互動式 PDF 表單、使用 Adobe Acrobat 建立的名為 AcroForms 的表單，以及使用 AEM Forms 或 Adobe LiveCycle 建立的基於 XFA 的表單。

此服務僅能將英語表單轉換為最適化表單。 您可以使用 [AEM 翻譯工作流程](https://helpx.adobe.com/experience-manager/6-5/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.html)將生成的最適化表單翻譯成另一種語言。

## 轉換工作流程  {#conversion-workflow}

自動表單轉換服務在 Adobe Cloud 上運行。 您將 AEM 執行個體連接到服務，並將表單上傳到 AEM 執行個體後，即可開始轉換。 完整的轉換過程如下所列：

![工作流程](assets/conversion-workflow.png)

### 1. 設定環境 {#set-up-the-environment}

自動表單轉換服務在 Adobe Cloud 上運行。 [設定您組織的 Adobe I/O 帳戶，並將您本端的 AEM 執行個體連接](configure-service.md)至 Adobe Cloud 上運行的轉換服務。

### 2. 將 PDF 表單轉換為最適化表單 {#use-the-conversion-service}

設定 AEM Forms 環境後，如欲將 PDF 表單轉換為最適化表單，請 [上傳 PDF 表單](convert-existing-forms-to-adaptive-forms.md)至 AEM 執行個體，然後[開始轉換](convert-existing-forms-to-adaptive-forms.md#run-the-conversion)。 在上傳表單前，請參閱以下提醒：

* 請勿上傳受保護的表單。 此服務無法轉換受密碼保護和加密的表單。
* 請勿上傳掃描、彩色、非英語和已填寫的表單。 此服務不支援這些表單。
* 請勿上傳檔案名中帶有空格的 PDF 表單。
* 請勿上傳 [PDF Portfolio](https://helpx.adobe.com/acrobat/using/overview-pdf-portfolios.html)。 此服務無法將 PDF Portfolio 轉換為最適化表單。
* 完成[最佳實務和考量](styles-and-pattern-considerations-and-best-practices.md)文章中描述的 PDF 表單的建議更改。
* 閱讀[已知問題](known-issues.md)文章以避免犯錯。

### 3. 檢閱轉換後的表單 {#review-converted-forms}

現實世界的表單在欄位佈局、命名或內隱建議方面可能具有複雜的資料擷取要求，而基於 AI/ML 的檢測邏輯可能無法精準擷取這些表單。 自動轉換完成後，您可以使用[檢閱和修正編輯器](review-correct-ui-edited.md)來檢查轉換後的表格並進行必要的更新，使成果更佳並更能提供符合期望的體驗。 完成必要的修改後，再一次轉換表單。

自動轉換所需的時間會受多樣因素影響：輸入的表單大小、表單複雜度，以及服務處理佇列上工作的多寡。 使用者可透過資料夾 / 檔案上的狀態顯示器時時瞭解進度。 轉換完成後，使用者設定的電子郵件地址也會收到電子郵件通知。
