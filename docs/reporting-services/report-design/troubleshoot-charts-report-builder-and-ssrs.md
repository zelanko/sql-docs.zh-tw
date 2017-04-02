---
title: "疑難排解圖表 (報表產生器及 SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3a327ffa-3b69-40d6-8015-cc01cfae9161
caps.latest.revision: 7
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 7
---
# 疑難排解圖表 (報表產生器及 SSRS)
  使用圖表時，這些問題很有協助。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## 為什麼我的圖表計數不會針對值軸上的值加總？  
 大多數的圖表類型都需要沿著值軸 (通常為 Y 軸) 放置數值，才能正確繪製。 如果值欄位的資料類型為 **String**，即使欄位中有數字，圖表也無法顯示數值。 但是，圖表會顯示在該欄位中包含值之資料列總數的計數。 若要避免發生這個問題，請確定您用於值數列的欄位具有數值資料類型，而不是包含格式化數字的字串。  
  
## 請參閱＜  
 [圖表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)  
  
  