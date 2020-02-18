---
title: 簡介
description: '加速將列印表單轉換為最適化表單 '
translation-type: tm+mt
source-git-commit: ef5789dabccc65dcf988b9424b435aa036017691

---


# 簡介 {#introduction-to-automated-forms-conversion-service}

「自動化表單轉換」服務可透過將PDF表單自動轉換為可調式表單，協助加速資料擷取體驗的數位化和現代化。 這項服務由Adobe Sensei提供支援，可自動將PDF表單轉換為適用於裝置、回應速度快且以HTML5為基礎的最適化表單。 在運用PDF表單和XFA的現有投資的同時，本服務也會在轉換期間將適當的驗證、樣式和版面套用至最適化表單欄位。 此服務有助於：

* 節省將列印表單轉換為最適化表單所需的手動工作
* 在轉換期間套用模式和適當的驗證
* 在轉換期間產生記錄檔案
* 將常出現的欄位群組為可重複使用的表單片段
* 在轉換期間啟用Adobe Analytics

![很簡單。 您只需提供來源表單，並將一切交給我們。 我們將提供您精美的調適性表單。 當然，您會將產出調整為滿意。 ](assets/pdf-to-adaptive-form-gitx50.gif)

## 入門 {#onboarding}

此服務可免費提供給AEM 6.5 Forms On-Premise定期客戶和Adobe Managed Service企業客戶。 您可以聯絡Adobe銷售團隊或您的Adobe代表以要求存取服務。

Adobe可讓您的組織存取權，並為組織中指定為管理員的人員提供必要的權限。 管理員可以授與您組織的AEM Forms開發人員（使用者）的存取權，以連線至服務。 如需詳 [細資訊，請參閱設定自動表單轉換](configure-service.md) 服務。

## 支援的PDF表格和語言 {#supported-languages-and-pdf-forms}

本服務支援非互動式PDF表單、使用Adobe Acrobat建立的表單（稱為AcroForms），以及使用AEM Forms或Adobe LiveCycle建立的XFA架構。

該服務只能將英語表單轉換為自適應表單。 您可以使用 [AEM轉換工作流程，將產生的最適化表單翻譯成其他語言](https://helpx.adobe.com/experience-manager/6-5/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.html)。

## 轉換工作流程 {#conversion-workflow}

自動化表單轉換服務可在Adobe cloud上執行。 您可將AEM例項連接至服務、將表單上傳至AEM例項，然後開始轉換。 完整的轉換程式如下：

![工作流程](assets/conversion-workflow.png)

### 1.設定環境 {#set-up-the-environment}

自動化表單轉換服務可在Adobe cloud上執行。 [設定您組織的Adobe I/O帳戶，並將您本機的AEM例項](configure-service.md) ，連線至Adobe cloud上執行的轉換服務。

### 2.將PDF表單轉換為可調整的表單 {#use-the-conversion-service}

在您的AEM Forms環境設定好後，若要將PDF表單轉換為最適化表單，請將 [PDF表單](convert-existing-forms-to-adaptive-forms.md) 上傳至AEM例項並 [開始轉換](convert-existing-forms-to-adaptive-forms.md#run-the-conversion)。 在上傳表單之前，請考慮下列事項：

* 請勿上傳安全表單。 該服務不會轉換受密碼保護和加密的表單。
* 請勿上傳掃描、彩色、非英文和填寫的表格。 不支援此類表格。
* 請勿上傳檔案名稱中含空格的PDF表格。
* 請勿上傳 [PDF資料夾](https://helpx.adobe.com/acrobat/using/overview-pdf-portfolios.html)。 本服務不會將PDF資料夾轉換為最適化表單。
* 在PDF表單中進行建議的變更，如「最佳實務與考 [慮事項」文章所述](styles-and-pattern-considerations-and-best-practices.md) 。
* 請閱讀「已 [知問題](known-issues.md) 」文章，以避免陷阱。

### 3.審核轉換的表單 {#review-converted-forms}

現實世界的表單在欄位配置、命名或隱含建議方面可能有複雜的資料擷取需求，而這些可能無法由AI/ML偵測邏輯精確擷取。 自動轉換完成後，您可以使用「 [Review and Correct」（檢閱與修正）編輯器來檢閱轉換的表格](review-correct-ui-edited.md) ，並進行必要的更新，並產生更精良的輸出，讓您體驗更加完美。 進行必要的變更後，請再次傳送表格以進行轉換。

自動轉換所花費的時間取決於多種因素，如輸入表單的大小、表單的複雜性、貸款在服務的處理隊列上。 通過資料夾／檔案上的狀態指示器定期通知用戶進度。 轉換完成後，也會傳送電子郵件通知給已設定的電子郵件地址。
