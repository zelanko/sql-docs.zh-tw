---
title: "模糊查閱轉換編輯器 (進階索引標籤) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.fuzzylookuptransformation.advanced.f1"
helpviewer_keywords: 
  - "模糊查閱轉換編輯器"
ms.assetid: 0a2919be-2ea7-4c06-82b8-0ffad5f0dd83
caps.latest.revision: 27
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 27
---
# 模糊查閱轉換編輯器 (進階索引標籤)
  使用 **[模糊查閱轉換編輯器]** 對話方塊的 **[進階]** 索引標籤，即可設定模糊查閱的參數。  
  
 若要深入了解模糊查閱轉換，請參閱＜ [Fuzzy Lookup Transformation](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation.md)＞。  
  
## 選項。  
 **每次查閱輸出的相符項目上限**  
 指定轉換針對每一個輸入資料列，可以傳回的相符項目上限。 預設值是 **1**。  
  
 **相似度臨界值**  
 使用滑桿設定元件層級的相似度臨界值。 此值越接近 1，查閱值與來源值的相似度必須越接近才能認定為相符。 增加臨界值可改善比對速度，因為需要考慮的候選記錄越少。  
  
 **Token 分隔符號**  
 指定轉換用來 Token 化資料行值的分隔符號。  
  
## 請參閱＜  
 [Integration Services 錯誤和訊息參考](../../../integration-services/integration-services-error-and-message-reference.md)   
 [模糊查閱轉換編輯器 &#40;參考資料表索引標籤&#41;](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation-editor-reference-table-tab.md)   
 [模糊查閱轉換編輯器 &#40;資料行索引標籤&#41;](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation-editor-columns-tab.md)  
  
  