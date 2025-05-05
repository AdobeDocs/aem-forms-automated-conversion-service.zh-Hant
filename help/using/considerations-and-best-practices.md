---
title: 最佳實務和考量事項
description: 不要PUBLISH
seo-description: DO NOT PUBLISH
page-status-flag: never-activated
uuid: c2821264-39e2-44f8-b234-835c46f33fd5
topic-tags: introduction
discoiquuid: b786e40a-202e-4e17-a2f5-1f77c46538c2
privatebeta: true
index: false
source-git-commit: c2392932d1e29876f7a11bd856e770b8f7ce3181
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 6%

---


# 最佳實務和考量事項 {#do-not-publish-best-practices-and-considerations}

<!--
[DO NOT PUBLISH]
-->

AEM Forms自動轉換服務會將PDF表單轉換為最適化表單。 此服務使用人工智慧和機器學習演演算法來瞭解來源表單的版面和欄位。 每個機器學習服務都會持續學習來源資料，並在每次流失時產生改良的輸出。 這些服務就像人類一樣，從經驗中學習。

automated forms conversion服務(AFCS)已接受大量表單的訓練。 它可輕鬆識別來源表單中的欄位並產生調適型表單。 不過，PDF forms中有些欄位和樣式雖然肉眼很容易看見，但服務上卻難以理解。 此服務可將與適用欄位型別或面板不同的指派給某些欄位或樣式。 以下列出所有此類欄位和樣式模式。

服務會持續從來源資料學習，開始識別並指派正確的欄位或面板給這些模式。 目前，您可以使用[檢閱並修正](review-correct-ui-edited.md)編輯器來修正此類問題。 在開始修正問題或進一步閱讀之前，請先熟悉[最適化表單元件](https://helpx.adobe.com/tw/experience-manager/6-5/forms/using/introduction-forms-authoring.html)。

## 一般 {#general}

<table border="1" cellpadding="1" cellspacing="0" style="border-collapse: separate; border-spacing: 0px;" width="100%"> 
 <tbody>
  <tr>
   <td width="30%">已知的模式和解析度</td> 
   <td width="70%">範例</td> 
  </tr>
   <td><p><strong>模式</strong></p> <p>服務無法將填寫的PDF forms轉換為最適化表單。</p> <p> </p> <p><strong>解決方法</strong></p> <p>使用空白的最適化表單。</p> </td> 
   <td style="text-align: left;"><img src="assets/pre-filled-form.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>模式</strong></p> <p>服務可能無法識別密集表單中的文字和欄位。</p> <p> </p> <p><strong>解決方法</strong></p> <p>在開始轉換之前，增加文字與密集表單欄位之間的寬度。</p> </td> 
   <td style="text-align: left;"><img src="assets/dense%20form.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>模式</strong></p> <p>服務不支援掃描的表單。</p> <p> </p> <p><strong>解決方法</strong></p> <p>請勿使用掃描的表單。 </p> </td> 
   <td><img src="assets/scanned-form.jpg" /></td> 
  </tr>
  <tr>
   <td><p><strong>模式</strong></p> <p>服務不會擷取影像中的影像和文字。 </p> <p> </p> <p><strong>解決方法</strong></p> <p>手動將影像或文字新增至轉換後的表單。</p> </td> 
   <td><img src="assets/image-in-adaptive-form.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>模式</strong></p> <p>具有虛線或不清除邊界與邊界的表格不會轉換。</p> <p><strong>解決方法</strong></p> <p>使用具有明確邊界和框線的表格。 支援。</p> </td> 
   <td><img src="assets/border-less-tables.png" /></td> 
  </tr>
 </tbody>
</table>

## 選擇群組  {#choice-group}

<table border="1" cellpadding="1" cellspacing="0" width="100%"> 
 <tbody>
  <tr>
   <td width="30%">模式</td> 
   <td width="70%">範例</td> 
  </tr>
  <tr>
   <td><p><strong>模式</strong></p> <p>具有方塊或圓圈以外形狀的選擇群組選項不會轉換為對應的最適化表單元件。 </p> <p> </p> <p><strong>解決方法</strong></p> <p>將選擇選項形狀變更為方塊或圓形，或使用「稽核並修正」編輯器來識別形狀。</p> </td> 
   <td><img src="assets/shaded-box-patterns.png" /> </td> 
  </tr>
 </tbody>
</table>

## 表單欄位 {#form-fields}

<table border="1" cellpadding="1" cellspacing="0" width="100%"> 
 <tbody>
  <tr>
   <td width="30%">模式</td> 
   <td width="70%">範例</td> 
  </tr>
  <tr>
   <td width="25%"><p><strong>模式</strong></p> <p>沒有清晰的框線，服務無法識別欄位。</p> <p> </p> <p><strong>解決方法</strong></p> <p>使用檢閱和修正編輯器來識別這些欄位。</p> <p> </p> <p> </p> </td> 
   <td width="50%"><br /> <img src="assets/fields-without-clear-borders.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>模式</strong></p> <p>服務在某些表單欄位底端或右側留下未識別的字幕。</p> <p> </p> <p><strong>解決方法</strong></p> <p>使用檢閱和修正編輯器來識別此類欄位</p> </td> 
   <td><br /> <img src="assets/forms-with-clear-borders-scale.png" /><br /> </td> 
  </tr>
  <tr>
   <td><p><strong>模式</strong></p> <p>服務會合併或指派錯誤型別給一些彼此非常接近或沒有明確框線的表單欄位。 </p> <p> </p> <p><strong>解決方法</strong></p> <p>使用檢閱和修正編輯器來識別這些欄位。</p> </td> 
   <td><img src="assets/forms-with-fields-placed-nearby.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>模式</strong></p> <p>服務可能無法識別含有遙遠字幕的欄位，或字幕與輸入欄位之間的虛線。</p> <p> </p> <p><strong>解決方法</strong></p> <p>使用具有明確界限的表單欄位，或使用檢閱和修正編輯器來修正此類問題。</p> </td> 
   <td><img src="assets/form-fields-with-far-away-captions.png" /></td> 
  </tr>
 </tbody>
</table>

## 清單 {#lists}

<table border="1" cellpadding="1" cellspacing="0" width="100%"> 
 <tbody>
  <tr>
   <td width="30%">模式</td> 
   <td width="70%">範例</td> 
  </tr>
  <tr>
   <td><p><strong>模式</strong></p> <p>包含表單欄位的清單會合併或未轉換為對應的最適化表單元件</p> <p><strong>解決方法</strong></p> <p>使用具有明確界限的表單欄位，或使用檢閱和修正編輯器來修正此類問題。</p> </td> 
   <td><img src="assets/lists-with-fields.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>模式</strong></p> <p>服務可能會保留一些無法識別的巢狀清單</p> <p> </p> <p><strong>解決方法</strong></p> <p>使用檢閱和修正編輯器來修正此類問題。</p> </td> 
   <td><img src="assets/nested-lists.png" /> </td> 
  </tr>
  <tr>
   <td><p><strong>模式</strong></p> <p>服務會將一些包含選擇群組的清單合併在一起</p> <p><strong>解決方法</strong></p> <p>使用檢閱和修正編輯器來修正此類問題。</p> </td> 
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

