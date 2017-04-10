---
title: "資料列取樣轉換編輯器 (取樣頁面) | Microsoft Docs"
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
  - "sql13.DTS.DESIGNER.ROWSAMPLINGTRANSFORMATION.COLUMNS.F1"
  - "sql13.dts.designer.rowsamplingtransformation.f1"
helpviewer_keywords: 
  - "資料列取樣轉換編輯器"
ms.assetid: 544c7709-6de0-4c08-bda3-759985be9a05
caps.latest.revision: 23
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 23
---
# 資料列取樣轉換編輯器 (取樣頁面)
  使用 **[資料列取樣轉換編輯器]** 對話方塊，即可將輸入的一部分分割為指定資料列數目的取樣。 這個轉換會將輸入分成兩個不同的輸出。  
  
 若要深入了解資料列取樣轉換，請參閱＜ [Row Sampling Transformation](../../../integration-services/data-flow/transformations/row-sampling-transformation.md)＞。  
  
## 選項。  
 **資料列數目**  
 指定輸入中的資料列數目作為取樣。  
  
 此屬性的值可以使用屬性運算式指定。  
  
 **取樣輸出名稱**  
 提供包含取樣資料列之輸出的唯一名稱。 提供的名稱將顯示在 SSIS 設計師內。  
  
 **未選取的輸出名稱**  
 提供輸出的唯一名稱，其中包含從取樣排除的資料列。 提供的名稱將顯示在 SSIS 設計師內。  
  
 **使用下列隨機種子**  
 指定轉換用來建立取樣之隨機號碼產生器的取樣種子。 只建議用於開發和測試。 如果未指定隨機種子，則轉換會使用 Microsoft Windows 滴答計數作為種子。  
  
## 請參閱＜  
 [Integration Services 錯誤和訊息參考](../../../integration-services/integration-services-error-and-message-reference.md)   
 [百分比取樣轉換](../../../integration-services/data-flow/transformations/percentage-sampling-transformation.md)  
  
  