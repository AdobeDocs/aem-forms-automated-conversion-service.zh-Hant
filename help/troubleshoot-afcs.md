---
title: '疑難排解自動化表單轉換服務 '
seo-title: '疑難排解Automated Forms Conversion Service(AFCS) '
description: '常見的AFCS問題及解決方案 '
seo-description: 常見的AFCS問題及解決方案
contentOwner: khsingh
topic-tags: forms
translation-type: tm+mt
source-git-commit: 3a82102feffa7fc618dc37c9a745c254a46a0700

---


# 疑難排解自動化表單轉換服務


<!--The article provides information on installation, configuration and administration issues that may arise in an Automated Forms Conversion Service production environment. --> The document  provides basic troubleshooting steps for common errors.

## 常見錯誤 {#commonerrors}

| 錯誤 | 範例 |
|--- |--- |
| **錯誤訊息**<br> ：存取Token標題無法使用。 <br><br> **原因**<br> 管理員已建立多個IMS設定，或IMS設定無法在Adobe Cloud上存取AFCS服務。 <br><br>**解析度&#x200B;**<br>：如果有多個配置，請刪除所有配置並[建立新配置](configure-service.md#obtainpubliccertificates)。<br>如果有單一配置，請使用** Health Check **[to check connectivity](configure-service.md#createintegrationoption). | ![存取Token標題無法使用](assets/invalid-ims-configurations.png) |
| **錯誤消息**<br> ：無法連接到服務。  <br><br>**原因&#x200B;**<br>「自動化表單轉換服務」雲端服務中提及錯誤的服務URL或沒有服務URL。<br><br>**解析度**<br>[](configure-service.md#configure-the-cloud-service) Automated Forms Conversion Service Cloud服務中的正確服務URL。 | ![無法連線至服務。](assets/wrong-service-url-configured.png) |
| **錯誤消息**<br> ：服務無法轉換表單。  <br><br>**原因&#x200B;**<br>：您端的網路連線問題、服務因Adobe Cloud的排程維護或中斷而中斷。<br><br>**解決**<br> ：解決您端的網路連接問題，並在https://status.adobe.com/上檢查服務的狀態，以發現計畫內或計畫外停機。 | ![無法連線至服務。](assets/conversion-failure.png) |
| **錯誤訊息**<br> ：頁數超過15頁。  <br><br>**原因&#x200B;**<br>：來源表單長度超過15頁。<br><br>**解析度**<br> ：使用Adobe Acrobat分割超過15頁的表單。 將表單中的頁數調整為少於15個。 | ![無法連線至服務。](assets/number-of-pages.png) |
| **錯誤訊息**<br> ：檔案數目超過15個。  <br><br>**原因&#x200B;**<br>資料夾包含15種以上表格。<br><br>**解析度**<br> ：將資料夾中的表單數量調整為小於或等於15。 將資料夾中的頁數總計放入小於50的資料夾。 將資料夾的大小調整到小於10 MB。 請勿將表單保留在子資料夾中。 將來源表單組織成一組8-15個表單。 | ![無法連線至服務。](assets/number-of-pages.png) |
| **錯誤消息**<br> ：不支援源檔案格式。  <br><br>**原因&#x200B;**<br>：包含源表單的資料夾包含一些不支援的檔案。<br><br>**解析度**<br> ：服務僅支援。xdp和。pdf檔案。 從資料夾移除具有任何其他副檔名的檔案，然後執行轉換。 | ![無法連線至服務。](assets/unsupported-file-formats.png) |
| **不支援錯誤消息**<br> 「掃描的表單」。  <br><br>**原因&#x200B;**<br>PDF表單只包含表單的掃描影像，不包含任何內容結構。<br><br>**解析度**<br> ：服務不支援將掃描的表單或表單的影像轉換為可調整的現成功能。 不過，您使用Adobe Acrobat將表單的影像轉換為PDF表單。 然後，使用服務將PDF表單轉換為最適化表單。 在Acrobat中，請務必使用高品質的表單影像進行轉換。 它改善了轉換的品質。 | ![無法連線至服務。](assets/scanned-forms-error.png) |
| **不支援錯誤訊息**<br> 「加密的PDF」表單。  <br><br>**原因&#x200B;**<br>資料夾包含加密的PDF表單。<br><br>**解析度**<br> ：服務不支援將加密的PDF表單轉換為最適化表單。 移除加密、上傳未加密的表單，然後執行轉換。 | ![無法連線至服務。](assets/secured-pdf-form.png) |
| **錯誤訊息**<br> ：無法剖析中繼模型JSON結構描述。  <br><br>**原因&#x200B;**<br>：提供給服務的JSON結構描述格式不正確、包含無效字元，或使用無效語法來映射元件。<br><br>**解析度**<br> ：檢查JSON檔案的格式。 您可以使用任何線上JSON驗證器來檢查架構的格式和結構。 如需元 [](extending-the-default-meta-model.md) 模型語法的相關資訊，請參閱擴充預設元模型文章。 | ![無法連線至服務。](assets/invalid-meta-model-schema.png) |

<!--

<table>
<thead>
<tr>
<th>Error</th>
<th>Example</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>Error Message</strong> <p> The access token header is not available. </p><br><strong>Reason</strong> <br> An administrator has created multiple IMS configurations or IMS configuration is not able to reach AFCS service on Adobe Cloud. <br><br><strong>Resolution</strong> <br> If there are multiple configurations, delete all the configurations and <a href="configure-service.md#obtainpubliccertificates">create a new configuration</a>. <br> If there is a single configuration, use <strong> Health Check </strong> to <a href="configure-service.md#createintegrationoption">check connectivity</a>.</td>
<td><img alt="The access token header is not available" src="assets/invalid-ims-configuration.png" /></td>
</tr>
<tr>
<td><strong>Error Message</strong> <br> Unable to connect to the service.  <br><br><strong>Reason</strong> <br> Incorrect service URL or no service URL is mentioned in Automated Forms Conversion Service cloud services. <br><br><strong>Resolution</strong> <br> Correct <a href="configure-service.md#configure-the-cloud-service">Service URL</a> in Automated Forms Conversion Service Cloud services.</td>
<td><img alt="Unable to connect to the service." src="assets/wrong-endpoint-configured.png" /></td>
</tr>
<tr>
<td><strong>Error Message</strong> <br> The service failed to convert the form.  <br><br><strong>Reason</strong> <br> Network connectivity issues at your end, the service is down due to scheduled maintenance, or outage on Adobe Cloud. <br><br><strong>Resolution</strong> <br> Resolve network connectivity issues at your end and check the status of the service on <a href="https://status.adobe.com/">https://status.adobe.com/</a> for a planned or unplanned outage.</td>
<td><img alt="The service failed to convert the form." src="assets/service-failure.png" /></td>
</tr>
<tr>
<td><strong>Error Message</strong> <br> The number of pages is more than 15.  <br><br><strong>Reason</strong> <br> The source form is more than 15 pages long.  <br><br><strong>Resolution</strong> <br> Use Adobe Acrobat to split forms with more than 15 pages. Bring the number of pages in a form to less than 15.</td>
<td><img alt="The number of pages is more than 15." src="assets/number-of-pages.png" /></td>
</tr>
<tr>
<td><strong>Error Message</strong> <br> The number of files is more than 15.  <br><br><strong>Reason</strong> <br>  The folder contains more than 15 forms. <br><br><strong>Resolution</strong> <br> Bring the number of forms in a folder to less than or equal to 15. Bring the total number of pages in a folder less than 50. Bring the size of the folder to less than 10 MB. Do not keep forms in a sub-folder. Organize source forms into a batch of 8-15 forms.</td>
<td><img alt="The number of files is more than 15." src="assets/number-of-pages.png" /></td>
</tr>
<tr>
<td><strong>Error Message</strong> <br> The source file format is not supported.  <br><br><strong>Reason</strong> <br> The folder containing source forms have some unsupported files. <br><br><strong>Resolution</strong> <br> The service supports only .xdp and .pdf files. Remove files with any other extension from the folder and run the conversion.</td>
<td><img alt="The source file format is not supported." src="assets/unsupported-file-formats.png" /></td>
</tr>
<tr>
<td><strong>Error Message</strong> <br> Scanned forms are not supported.  <br><br><strong>Reason</strong> <br> The PDF form contains only scanned images of the form and contains no content structure. <br><br><strong>Resolution</strong> <br> The service does not support converting scanned forms or an image of a form to an adaptive out-of-the-box. However, you use Adobe Acrobat to convert the image of a form to a PDF Form. Then, use the service to convert the PDF Form to an adaptive form. Always use a high-quality image of the form for conversion in Acrobat. It improves the quality of the conversion.</td>
<td><img alt="Scanned forms are not supported." src="assets/scanned-forms-error.png" /></td>
</tr>
<tr>
<td><strong>Error Message</strong> <br> Encrypted PDF form is not supported.  <br><br><strong>Reason</strong> <br> The folder contains encrypted PDF forms. <br><br><strong>Resolution</strong> <br> The service does not support converting an encrypted PDF form to an adaptive form. Remove the encryption, upload the non-encrypted form, and run the conversion.</td>
<td><img alt="Encrypted PDF form is not supported." src="assets/secured-pdf-form.png" /></td>
</tr>
<tr>
<td><strong>Error Message</strong> <br> Unable to parse meta-model JSON schema.  <br><br><strong>Reason</strong> <br> The JSON schema supplied to the service is not properly formatted, contains invalid characters, or uses invalid syntax to map components.  <br><br><strong>Resolution</strong> <br> Check the formatting of the JSON file. You can use any online JSON validator to check the formatting and structure of the schema. See, <a href="extending-the-default-meta-model.md">Extend the default meta-model</a> article for information on meta-model syntax.</td>
<td><img alt="Unable to parse meta-model JSON schema" src="assets/invalid-meta-model-schema.png" /></td>
</tr>
</tbody>
</table>
-->