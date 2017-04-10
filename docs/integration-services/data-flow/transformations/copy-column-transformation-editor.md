---
title: "複製資料行轉換編輯器 | Microsoft Docs"
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
  - "sql13.dts.designer.copymaptransformation.f1"
helpviewer_keywords: 
  - "複製資料行轉換編輯器"
ms.assetid: d8e70541-d563-4ce4-bf66-bc888a0d3026
caps.latest.revision: 26
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 26
---
# 複製資料行轉換編輯器
  使用 **[複製資料行轉換編輯器]** 對話方塊，即可選取要複製的資料行，並為新的輸出資料行指派名稱。  
  
 若要深入了解複製資料行轉換，請參閱＜ [Copy Column Transformation](../../../integration-services/data-flow/transformations/copy-column-transformation.md)＞。  
  
> [!NOTE]  
>  如果只是將所有的來源資料複製到目的地時，就可能不需要使用複製資料行轉換。 在某些不需要進行資料轉換的狀況下，可以將來源直接連接到目的地。 在這些狀況下，最好使用「SQL Server 匯入和匯出精靈」為您建立封裝。 稍後可依需要來增強和重新設定封裝。 如需詳細資訊，請參閱＜ [SQL Server Import and Export Wizard](../Topic/SQL%20Server%20Import%20and%20Export%20Wizard.md)＞。  
  
## 選項。  
 **可用的輸入資料行**  
 使用核取方塊來選取要複製的資料行。 您的選取範圍會將輸入資料行加入下列資料表中。  
  
 **輸入資料行**  
 從可用輸入資料行的清單中選取要複製的資料行。 您的選擇會反映在 **[可用的輸入資料行]** 資料表的核取方塊選擇中。  
  
 **輸出別名**  
 輸入每個新輸出資料行的別名。 預設為 **[的副本]**，後面緊接著輸入資料行的名稱，但是您也可以選擇任何唯一的描述性名稱。  
  
## 請參閱＜  
 [Integration Services 錯誤和訊息參考](../../../integration-services/integration-services-error-and-message-reference.md)  
  
  