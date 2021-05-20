---
title: '最佳實務和考量 '
description: 不發佈
seo-description: 不發佈
page-status-flag: never-activated
uuid: c2821264-39e2-44f8-b234-835c46f33fd5
topic-tags: introduction
discoiquuid: b786e40a-202e-4e17-a2f5-1f77c46538c2
privatebeta: true
index: false
source-git-commit: b2d29c22a275f2dc6a82593cf5e441c8da0bba13
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 4%

---


# 最佳實務和考量 {#do-not-publish-best-practices-and-considerations}

<!--
[DO NOT PUBLISH]
-->

AEM Forms自動轉換服務將PDF表單轉換為最適化表單。 該服務使用人工智慧和機器學習算法來理解源表單的佈局和欄位。 每個機器學習服務會持續從來源資料中學習，並透過每次流失產生改良的輸出。 這些服務從人類的經歷中學到。

automated forms conversion服務是針對大量表單進行訓練。 它可輕鬆識別來源表單中的欄位，並產生最適化表單。 然而，PDF forms中有些領域和風格很容易被人眼看到，但是卻難以理解。 服務可指派不同於適用欄位類型或面板給某些欄位或樣式。 下面列出了所有此類欄位和樣式模式。

隨著服務不斷從來源資料中學習，服務會開始識別並指派正確的欄位或面板給這些模式。 目前，您可以使用[檢閱和修正](review-correct-ui-edited.md)編輯器來修正此類問題。 開始修正問題或進一步閱讀前，請熟悉[最適化表單元件](https://helpx.adobe.com/experience-manager/6-5/forms/using/introduction-forms-authoring.html)。

## 一般 {#general}

<table border="1" cellpadding="1" cellspacing="0" style="border-collapse: separate; border-spacing: 0px;" width="100%"> 
 <tbody>
  <tr>
   <td width="30%">已知模式和解析度</td> 
   <td width="70%">範例</td> 
  </tr>
   <td><p><strong>圖樣</strong></p> <p>服務不會將已填入的PDF forms轉換為最適化表單。</p> <p> </p> <p><strong>解析度</strong></p> <p>使用空的最適化表單。</p> </td> 
   <td style="text-align: left;"><img src="assets/pre-filled-form.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>圖樣</strong></p> <p>服務可能無法識別密集表單中的文字和欄位。</p> <p> </p> <p><strong>解析度</strong></p> <p>開始轉換前，請增加密集表單的文字和欄位之間的寬度。</p> </td> 
   <td style="text-align: left;"><img src="assets/dense%20form.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>圖樣</strong></p> <p>服務不支援掃描的表單。</p> <p> </p> <p><strong>解析度</strong></p> <p>請勿使用掃描的表單。 </p> </td> 
   <td><img src="assets/scanned-form.jpg" /></td> 
  </tr>
  <tr>
   <td><p><strong>圖樣</strong></p> <p>服務不會擷取影像中的影像和文字。 </p> <p> </p> <p><strong>解析度</strong></p> <p>手動將影像或文字新增至轉換的表單。</p> </td> 
   <td><img src="assets/image-in-adaptive-form.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>圖樣</strong></p> <p>帶有點線或非清除邊界和邊界的表格不會轉換。</p> <p><strong>解析度</strong></p> <p>使用具有明確邊界和邊界的表。 支援。</p> </td> 
   <td><img src="assets/border-less-tables.png" /></td> 
  </tr>
 </tbody>
</table>

## 選擇組{#choice-group}

<table border="1" cellpadding="1" cellspacing="0" width="100%"> 
 <tbody>
  <tr>
   <td width="30%">圖樣</td> 
   <td width="70%">範例</td> 
  </tr>
  <tr>
   <td><p><strong>圖樣</strong></p> <p>具有框或圓以外形狀的選擇組選項不會轉換為相應的最適化表單元件。 </p> <p> </p> <p><strong>解析度</strong></p> <p>將選擇選項形狀更改為框或圓，或使用「查看並更正」編輯器來標識形狀。</p> </td> 
   <td><img src="assets/shaded-box-patterns.png" /> </td> 
  </tr>
 </tbody>
</table>

## 表單欄位{#form-fields}

<table border="1" cellpadding="1" cellspacing="0" width="100%"> 
 <tbody>
  <tr>
   <td width="30%">圖樣</td> 
   <td width="70%">範例</td> 
  </tr>
  <tr>
   <td width="25%"><p><strong>圖樣</strong></p> <p>服務不會識別沒有明確邊界的欄位。</p> <p> </p> <p><strong>解析度</strong></p> <p>使用「審閱」和「更正」編輯器來標識此類欄位。</p> <p> </p> <p> </p> </td> 
   <td width="50%"><br /> <img src="assets/fields-without-clear-borders.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>圖樣</strong></p> <p>服務會在某些表單欄位的底部或右側隱藏字幕。</p> <p> </p> <p><strong>解析度</strong></p> <p>使用「審閱」和「更正」編輯器來標識此類欄位</p> </td> 
   <td><br /> <img src="assets/forms-with-clear-borders-scale.png" /><br /> </td> 
  </tr>
  <tr>
   <td><p><strong>圖樣</strong></p> <p>服務會合併或為某些表單欄位指定錯誤的類型，這些欄位彼此相距甚遠或沒有清晰的邊界。 </p> <p> </p> <p><strong>解析度</strong></p> <p>使用「審閱」和「更正」編輯器來標識此類欄位。</p> </td> 
   <td><img src="assets/forms-with-fields-placed-nearby.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>圖樣</strong></p> <p>服務可能無法識別字幕遠離的欄位，或字幕與輸入欄位之間的虛線。</p> <p> </p> <p><strong>解析度</strong></p> <p>使用邊界明確的表單欄位，或使用「檢閱及修正」編輯器來修正此類問題。</p> </td> 
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
   <td><p><strong>圖樣</strong></p> <p>包含表單欄位的清單會合併或不轉換為對應的最適化表單元件</p> <p><strong>解析度</strong></p> <p>使用邊界明確的表單欄位，或使用「檢閱及修正」編輯器來修正此類問題。</p> </td> 
   <td><img src="assets/lists-with-fields.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>圖樣</strong></p> <p>服務可能會讓數個巢狀清單未識別</p> <p> </p> <p><strong>解析度</strong></p> <p>使用「檢閱」和「修正」編輯器來修正此類問題。</p> </td> 
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

