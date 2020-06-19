---
title: '[不發佈]最佳做法和注意事項 '
seo-title: '[不發佈]最佳做法和注意事項 '
description: 'null'
seo-description: 'null'
page-status-flag: never-activated
uuid: c2821264-39e2-44f8-b234-835c46f33fd5
topic-tags: introduction
discoiquuid: b786e40a-202e-4e17-a2f5-1f77c46538c2
privatebeta: true
index: false
translation-type: tm+mt
source-git-commit: 356eb083b889a1bf151c32bc5f01a6d263b96274
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 3%

---


# [不要發佈最佳做法] 和注意事項 {#do-not-publish-best-practices-and-considerations}

AEM Forms Automated Conversion服務可將PDF表單轉換為最適化表單。 該服務使用人工智慧和機器學習算法來理解源表單的佈局和領域。 每項機器學習服務都會持續從來源資料中學習，並在每次流失時產生改善的輸出。 這些服務從人類的體驗中學習。

自動化表單轉換服務是針對大量表單進行培訓的。 它可輕鬆識別來源表單中的欄位，並產生最適化表單。 不過，PDF表格中有些欄位和樣式很容易讓人看得到，但是卻很難為服務瞭解。 服務可指派不同於適用欄位類型或面板給某些欄位或樣式。 以下列出所有此類欄位和樣式模式。

服務會開始識別並指派正確的欄位或面板給這些模式，因為它會不斷從來源資料中學習。 目前，您可以使用「檢閱」 [和「更正」編輯器](review-correct-ui-edited.md) ，來修正此類問題。 在開始修正問題或進一步閱讀之前，請先熟悉最適 [化表單元件](https://helpx.adobe.com/experience-manager/6-5/forms/using/introduction-forms-authoring.html)。

## 一般 {#general}

<!--
Comment Type: draft

<ul>
<li>Service does not convert filled PDF forms to adaptive form. Use empty adaptive forms.Service does not convert colored PDF forms to adaptive form. Use  and white or grayscale adaptive forms. <br /> </li>
<li>Service does not convert filled PDF forms to adaptive form. Use empty adaptive forms.</li>
<li>Service does not support scanned forms. Do not use scanned forms. </li>
<li>Service can fail to recognize text and fields in a dense form. Increase the width between text and fields of a dense form before starting the conversion.</li>
<li>Service does not extract images. Manually add images to converted forms.</li>
<li>Service does not extract text present within an image. Manually add text to the adaptive form.</li>
</ul>
-->

<table border="1" cellpadding="1" cellspacing="0" style="border-collapse: separate; border-spacing: 0px;" width="100%"> 
 <tbody>
  <tr>
   <td width="30%">已知圖樣與解析度</td> 
   <td width="70%">範例</td> 
  </tr>
  <tr>
   <td><p><strong>圖樣</strong></p> <p>服務不會將彩色的PDF表單轉換為最適化表單。</p> <p> </p> <p><strong>解析度</strong></p> <p>使用黑白或灰階PDF表單。 </p> </td> 
   <td style="text-align: left;"> <img src="assets/coloured-form.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>圖樣</strong></p> <p>服務不會將已填寫的PDF表格轉換為最適化表格。</p> <p> </p> <p><strong>解析度</strong></p> <p>使用空的最適化表單。</p> </td> 
   <td style="text-align: left;"><img src="assets/pre-filled-form.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>圖樣</strong></p> <p>服務無法識別密集表單中的文字和欄位。</p> <p> </p> <p><strong>解析度</strong></p> <p>在開始轉換之前，增加密集表單的文字和欄位之間的寬度。</p> </td> 
   <td style="text-align: left;"><img src="assets/dense%20form.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>圖樣</strong></p> <p>服務不支援掃描的表單。</p> <p> </p> <p><strong>解析度</strong></p> <p>請勿使用掃描的表格。 </p> </td> 
   <td><img src="assets/scanned-form.jpg" /></td> 
  </tr>
  <tr>
   <td><p><strong>圖樣</strong></p> <p>服務不會擷取影像和影像中的文字。 </p> <p> </p> <p><strong>解析度</strong></p> <p>手動將影像或文字新增至轉換的表單。</p> </td> 
   <td><img src="assets/image-in-adaptive-form.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>圖樣</strong></p> <p>不會轉換帶有虛線或非清晰邊界和邊框的表格。</p> <p><strong>解析度</strong></p> <p>使用具有明確邊界和邊界的表。 支援。</p> </td> 
   <td><img src="assets/border-less-tables.png" /></td> 
  </tr>
 </tbody>
</table>

## Choice Group  {#choice-group}

<table border="1" cellpadding="1" cellspacing="0" width="100%"> 
 <tbody>
  <tr>
   <td width="30%">圖樣</td> 
   <td width="70%">範例</td> 
  </tr>
  <tr>
   <td><p><strong>圖樣</strong></p> <p>具有框或圓形以外形狀的選擇組選項不會轉換為相應的自適應表單元件。 </p> <p> </p> <p><strong>解析度</strong></p> <p>將選擇選項形狀變更為方塊或圓形，或使用「檢閱與修正」編輯器來識別形狀。</p> </td> 
   <td><img src="assets/shaded-box-patterns.png" /> </td> 
  </tr>
 </tbody>
</table>

## 表單欄位 {#form-fields}

<table border="1" cellpadding="1" cellspacing="0" width="100%"> 
 <tbody>
  <tr>
   <td width="30%">圖樣</td> 
   <td width="70%">範例</td> 
  </tr>
  <tr>
   <td width="25%"><p><strong>圖樣</strong></p> <p>服務不會識別沒有明確邊界的欄位。</p> <p> </p> <p><strong>解析度</strong></p> <p>使用「檢閱」和「更正」編輯器來識別這些欄位。</p> <p> </p> <p> </p> </td> 
   <td width="50%"><br /> <img src="assets/fields-without-clear-borders.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>圖樣</strong></p> <p>服務會在某些表單欄位底部或右側留下未識別標題。</p> <p> </p> <p><strong>解析度</strong></p> <p>使用「檢閱與修正」編輯器來識別這些欄位</p> </td> 
   <td><br /> <img src="assets/forms-with-clear-borders-scale.png" /><br /> </td> 
  </tr>
  <tr>
   <td><p><strong>圖樣</strong></p> <p>服務會將錯誤類型合併或分配給彼此相距甚遠或邊界不明確的某些表單域。 </p> <p> </p> <p><strong>解析度</strong></p> <p>使用「檢閱」和「更正」編輯器來識別這些欄位。</p> </td> 
   <td><img src="assets/forms-with-fields-placed-nearby.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>圖樣</strong></p> <p>服務可能無法識別字幕遠離的欄位，或字幕與輸入欄位之間的虛線。</p> <p> </p> <p><strong>解析度</strong></p> <p>使用邊界明確的表單欄位，或使用「檢閱並更正」編輯器來修正此類問題。</p> </td> 
   <td><img src="assets/form-fields-with-far-away-captions.png" /></td> 
  </tr>
 </tbody>
</table>

## 清單 {#lists}

<table border="1" cellpadding="1" cellspacing="0" width="100%"> 
 <tbody>
  <tr>
   <td width="30%">圖樣</td> 
   <td width="70%">範例</td> 
  </tr>
  <tr>
   <td><p><strong>圖樣</strong></p> <p>包含表單欄位的清單被合併或未轉換為相應的自適應表單元件</p> <p><strong>解析度</strong></p> <p>使用邊界明確的表單欄位，或使用「檢閱並更正」編輯器來修正此類問題。</p> </td> 
   <td><img src="assets/lists-with-fields.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>圖樣</strong></p> <p>服務可讓數個巢狀清單無法識別</p> <p> </p> <p><strong>解析度</strong></p> <p>使用「檢閱」和「修正」編輯器來修正此類問題。</p> </td> 
   <td><img src="assets/nested-lists.png" /> </td> 
  </tr>
  <tr>
   <td><p><strong>圖樣</strong></p> <p>服務將包含選擇組的某些清單合併</p> <p><strong>解析度</strong></p> <p>使用「檢閱」和「修正」編輯器來修正此類問題。</p> </td> 
   <td><img src="assets/lists-containing-choice-groups.png" /> </td> 
  </tr>
 </tbody>
</table>

<!--
Comment Type: draft

<h3>Choice groups</h3>
-->

<!--
Comment Type: draft

<ul>
<li>Lists with form fields, nested lists, and nested choice groups are not supported.</li>
<li>Form fields with captions at bottom or right are not supported.</li>
<li>Form fiields without bordes are not supported.</li>
<li>Hidden form fields are not supported.</li>
<li>Button in PDF forms are not converted to adaptive form buttons.<br /> </li>
<li>Tables with clear explicit boundaries and borders are supported.</li>
<li>Fields with far away captions are not supported.<br /> </li>
<li>Choice groups with only box or circle shaped selectors are supported. </li>
</ul>
-->

