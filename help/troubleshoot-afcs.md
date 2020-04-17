---
title: '疑難排解自動化表單轉換服務 '
seo-title: '疑難排解Automated Forms Conversion Service(AFCS) '
description: '常見的AFCS問題及解決方案 '
seo-description: 常見的AFCS問題及解決方案
contentOwner: khsingh
topic-tags: forms
translation-type: tm+mt
source-git-commit: 0af626e21a0c3d6a7d3c339c0b87179b048092d3

---


# 疑難排解自動化表單轉換服務


<!--The article provides information on installation, configuration and administration issues that may arise in an Automated Forms Conversion Service production environment. --> The document  provides basic troubleshooting steps for common errors.

## 常見錯誤 {#commonerrors}

<table>
<thead>
<tr>
<th>錯誤</th>
<th>範例</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>錯誤訊息</strong><br> ：存取Token標題無法使用。 <br><br><strong>原因</strong><br> 管理員已建立多個IMS設定，或IMS設定無法在Adobe Cloud上存取AFCS服務。 <br><br><strong>解析度</strong><br> ：如果有多個配置，請刪除所有配置並 <a href="configure-service.md#obtainpubliccertificates">建立新配置</a>。 <br> 如果有單一配置，請使用 <strong> Health Check </strong> to <a href="configure-service.md#createintegrationoption">check connectivity</a>.</td>
<td><img alt="存取Token標題無法使用" src="assets/invalid-ims-configuration.png" /></td>
</tr>
<tr>
<td><strong>錯誤消息</strong><br> ：無法連接到服務。  <br><br><strong>原因</strong><br> 「自動化表單轉換服務」雲端服務中提及錯誤的服務URL或沒有服務URL。 <br><br><strong>解析度</strong><br><a href="configure-service.md#configure-the-cloud-service"></a> Automated Forms Conversion Service Cloud服務中的正確服務URL。</td>
<td><img alt="無法連線至服務。" src="assets/wrong-endpoint-configured.png" /></td>
</tr>
<tr>
<td><strong>錯誤消息</strong><br> ：服務無法轉換表單。  <br><br><strong>原因</strong><br> ：您端的網路連線問題、服務因Adobe Cloud的排程維護或中斷而中斷。 <br><br><strong>解決</strong> ：解決您端的網路連接問題，並在https://status.adobe.com/上檢查服務的狀態，以查 <br> 看計畫內 <a href="https://status.adobe.com/"></a> 或計畫外停機。</td>
<td><img alt="服務無法轉換表單。" src="assets/service-failure.png" /></td>
</tr>
<tr>
<td><strong>錯誤訊息</strong><br> ：頁數超過15頁。  <br><br><strong>原因</strong><br> ：來源表單長度超過15頁。  <br><br><strong>解析度</strong><br> ：使用Adobe Acrobat分割超過15頁的表單。 將表單中的頁數調整為少於15個。</td>
<td><img alt="頁數超過15頁。" src="assets/number-of-pages.png" /></td>
</tr>
<tr>
<td><strong>錯誤訊息</strong><br> ：檔案數目超過15個。  <br><br><strong>原因</strong><br> 資料夾包含15種以上表格。 <br><br><strong>解析度</strong><br> ：將資料夾中的表單數量調整為小於或等於15。 將資料夾中的頁數總計放入小於50的資料夾。 將資料夾的大小調整到小於10 MB。 請勿將表單保留在子資料夾中。 將來源表單組織成一組8-15個表單。</td>
<td><img alt="檔案數超過15個。" src="assets/number-of-pages.png" /></td>
</tr>
<tr>
<td><strong>錯誤消息</strong><br> ：不支援源檔案格式。  <br><br><strong>原因</strong><br> ：包含源表單的資料夾包含一些不支援的檔案。 <br><br><strong>解析度</strong><br> ：服務僅支援。xdp和。pdf檔案。 從資料夾移除具有任何其他副檔名的檔案，然後執行轉換。</td>
<td><img alt="不支援源檔案格式。" src="assets/unsupported-file-formats.png" /></td>
</tr>
<tr>
<td><strong>不支援錯誤消息</strong><br> 「掃描的表單」。  <br><br><strong>原因</strong><br> PDF表單只包含表單的掃描影像，不包含任何內容結構。 <br><br><strong>解析度</strong><br> ：服務不支援將掃描的表單或表單的影像轉換為可調整的現成功能。 不過，您使用Adobe Acrobat將表單的影像轉換為PDF表單。 然後，使用服務將PDF表單轉換為最適化表單。 在Acrobat中，請務必使用高品質的表單影像進行轉換。 它改善了轉換的品質。</td>
<td><img alt="不支援掃描的表單。" src="assets/scanned-forms-error.png" /></td>
</tr>
<tr>
<td><strong>不支援錯誤訊息</strong><br> 「加密的PDF」表單。  <br><br><strong>原因</strong><br> 資料夾包含加密的PDF表單。 <br><br><strong>解析度</strong><br> ：服務不支援將加密的PDF表單轉換為最適化表單。 移除加密、上傳未加密的表單，然後執行轉換。</td>
<td><img alt="不支援加密的PDF表單。" src="assets/secured-pdf-form.png" /></td>
</tr>
<tr>
<td><strong>錯誤訊息</strong><br> ：無法剖析中繼模型JSON結構描述。  <br><br><strong>原因</strong><br> ：提供給服務的JSON結構描述格式不正確、包含無效字元，或使用無效語法來映射元件。  <br><br><strong>解析度</strong><br> ：檢查JSON檔案的格式。 您可以使用任何線上JSON驗證器來檢查架構的格式和結構。 如需元 <a href="extending-the-default-meta-model.md"></a> 模型語法的相關資訊，請參閱擴充預設元模型文章。</td>
<td><img alt="無法剖析中繼模型JSON結構描述" src="assets/invalid-meta-model-schema.png" /></td>
</tr>
</tbody>
</table>
