---
title: 最佳實務和考量
description: 不發佈
seo-description: DO NOT PUBLISH
page-status-flag: never-activated
uuid: c2821264-39e2-44f8-b234-835c46f33fd5
topic-tags: introduction
discoiquuid: b786e40a-202e-4e17-a2f5-1f77c46538c2
privatebeta: true
index: false
source-git-commit: b2d29c22a275f2dc6a82593cf5e441c8da0bba13
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 7%

---


# 最佳實務和考量 {#do-not-publish-best-practices-and-considerations}

<!--
[DO NOT PUBLISH]
-->

AEM Forms自動轉換服務將PDF表單轉換為自適應表單。 服務採用人工智慧和機器學習算法來理解源表單的佈局和欄位。 每個機器學習服務都不斷從源資料中學習，並在每次混亂中產生改進的輸出。 這些服務從人類的經驗中學習。

automated forms conversion服務受到大量表單的培訓。 它可輕鬆識別源表單中的欄位並生成自適應表單。 但是，PDF forms中也有一些領域和風格，它們很容易被人們看到，但很難為服務理解。 該服務可以為某些欄位或樣式指定不同於適用的欄位類型或面板。 下面列出了所有此類欄位和樣式模式。

當服務不斷從源資料中學習時，它將開始識別並為這些模式分配正確的欄位或面板。 目前，你可以 [審閱並更正](review-correct-ui-edited.md) 編輯器來解決這些問題。 在開始解決問題或進一步閱讀之前，請熟悉 [自適應表單元件](https://helpx.adobe.com/experience-manager/6-5/forms/using/introduction-forms-authoring.html)。

## 一般 {#general}

<table border="1" cellpadding="1" cellspacing="0" style="border-collapse: separate; border-spacing: 0px;" width="100%"> 
 <tbody>
  <tr>
   <td width="30%">已知模式和解析度</td> 
   <td width="70%">範例</td> 
  </tr>
   <td><p><strong>模式</strong></p> <p>服務不會將填充的PDF forms轉換為自適應表單。</p> <p> </p> <p><strong>解析度</strong></p> <p>使用空的自適應表單。</p> </td> 
   <td style="text-align: left;"><img src="assets/pre-filled-form.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>模式</strong></p> <p>服務無法識別密集表單中的文本和欄位。</p> <p> </p> <p><strong>解析度</strong></p> <p>在開始轉換之前，增加密集表單的文本和欄位之間的寬度。</p> </td> 
   <td style="text-align: left;"><img src="assets/dense%20form.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>模式</strong></p> <p>服務不支援掃描的表單。</p> <p> </p> <p><strong>解析度</strong></p> <p>不要使用掃描的表單。 </p> </td> 
   <td><img src="assets/scanned-form.jpg" /></td> 
  </tr>
  <tr>
   <td><p><strong>模式</strong></p> <p>服務不提取影像內的影像和文本。 </p> <p> </p> <p><strong>解析度</strong></p> <p>手動將影像或文本添加到已轉換的表單。</p> </td> 
   <td><img src="assets/image-in-adaptive-form.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>模式</strong></p> <p>不轉換帶點線或不清除邊界和邊框的表。</p> <p><strong>解析度</strong></p> <p>使用具有明確顯式邊界和邊框的表。 支援。</p> </td> 
   <td><img src="assets/border-less-tables.png" /></td> 
  </tr>
 </tbody>
</table>

## 選擇組  {#choice-group}

<table border="1" cellpadding="1" cellspacing="0" width="100%"> 
 <tbody>
  <tr>
   <td width="30%">模式</td> 
   <td width="70%">範例</td> 
  </tr>
  <tr>
   <td><p><strong>模式</strong></p> <p>不會將形狀為框或圓以外的選項組選項轉換為相應的自適應窗體元件。 </p> <p> </p> <p><strong>解析度</strong></p> <p>將選擇選項形狀更改為框或圓，或使用「審閱」和「正確」編輯器來標識形狀。</p> </td> 
   <td><img src="assets/shaded-box-patterns.png" /> </td> 
  </tr>
 </tbody>
</table>

## 表單域 {#form-fields}

<table border="1" cellpadding="1" cellspacing="0" width="100%"> 
 <tbody>
  <tr>
   <td width="30%">模式</td> 
   <td width="70%">範例</td> 
  </tr>
  <tr>
   <td width="25%"><p><strong>模式</strong></p> <p>服務不標識沒有清除邊框的欄位。</p> <p> </p> <p><strong>解析度</strong></p> <p>使用「審閱」(Review)和「正確」(Correct)編輯器來標識此類欄位。</p> <p> </p> <p> </p> </td> 
   <td width="50%"><br /> <img src="assets/fields-without-clear-borders.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>模式</strong></p> <p>「服務」會留下一些表格欄位，其底部或右側的標題未標識。</p> <p> </p> <p><strong>解析度</strong></p> <p>使用「審閱」和「正確」編輯器來標識此類欄位</p> </td> 
   <td><br /> <img src="assets/forms-with-clear-borders-scale.png" /><br /> </td> 
  </tr>
  <tr>
   <td><p><strong>模式</strong></p> <p>服務會將錯誤類型合併或分配給彼此非常靠近或沒有明確邊框的某些表單域。 </p> <p> </p> <p><strong>解析度</strong></p> <p>使用「審閱」(Review)和「正確」(Correct)編輯器來標識此類欄位。</p> </td> 
   <td><img src="assets/forms-with-fields-placed-nearby.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>模式</strong></p> <p>服務無法識別帶有遠離字幕或字幕和輸入欄位之間的虛線的欄位。</p> <p> </p> <p><strong>解析度</strong></p> <p>使用具有明確邊界的表單域或使用「審閱」和「更正」編輯器修復此類問題。</p> </td> 
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
   <td><p><strong>模式</strong></p> <p>包含表單域的清單被合併或未轉換為相應的自適應表單元件</p> <p><strong>解析度</strong></p> <p>使用具有明確邊界的表單域或使用「審閱」和「更正」編輯器修復此類問題。</p> </td> 
   <td><img src="assets/lists-with-fields.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>模式</strong></p> <p>服務可以保留幾個未標識的嵌套清單</p> <p> </p> <p><strong>解析度</strong></p> <p>使用「審閱」(Review)和「正確」(Correct)編輯器修復此類問題。</p> </td> 
   <td><img src="assets/nested-lists.png" /> </td> 
  </tr>
  <tr>
   <td><p><strong>模式</strong></p> <p>服務將包含選擇組的某些清單彼此合併</p> <p><strong>解析度</strong></p> <p>使用「審閱」(Review)和「正確」(Correct)編輯器修復此類問題。</p> </td> 
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

