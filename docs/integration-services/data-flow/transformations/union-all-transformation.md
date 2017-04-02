---
title: "聯集全部轉換 | Microsoft Docs"
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
  - "sql13.dts.designer.unionalltrans.f1"
helpviewer_keywords: 
  - "合併資料集 [Integration Services]"
  - "組合資料集"
  - "聯集全部轉換"
  - "資料集 [Integration Services], 合併"
ms.assetid: 942e4b90-9c41-4e9c-a6f3-80b3afe57f2f
caps.latest.revision: 39
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 39
---
# 聯集全部轉換
  「聯集全部」轉換會將多項輸入結合至單一輸出。 例如，五個不同的「一般檔案」來源的輸出，可做為「聯集全部」轉換的輸入並組合成一個輸出。  
  
## 輸入和輸出  
 轉換輸入會逐一加入至轉換輸出；不會發生任何重新排列資料列的情形。 如果封裝需要經過排序的輸出，則您應使用「合併」轉換而非「聯集全部」轉換。  
  
 您連接到「聯集全部」轉換的第一個輸入，是轉換從中建立轉換輸出的輸入。 您接著連接到轉換的輸入中的資料行，會對應至轉換輸出中的資料行。  
  
 若要合併輸入，請將輸入中的資料行對應至輸出中的資料行。 您至少必須將一個輸入的資料行對應至各輸出資料行。 兩個資料行之間的對應，會要求資料行的中繼資料相符。 例如，對應的資料行必須擁有相同的資料類型。  
  
 如果對應的資料行包含字串資料，而輸出資料行的長度比輸入資料行短，則輸出資料行的長度會自動增加，以包含輸入資料行。 未對應至輸出資料行的輸入資料行會在輸出資料行中設為 Null 值。  
  
 此轉換有多個輸入和一個輸出。 它不支援錯誤輸出。  
  
## 聯集全部轉換的組態  
 您可以透過「 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師」或以程式設計方式設定屬性。  
  
 如需可在 [聯集全部轉換編輯器] 對話方塊中設定之屬性的詳細資訊，請參閱[聯集全部轉換編輯器](../../../integration-services/data-flow/transformations/union-all-transformation-editor.md)。  
  
 如需可透過程式設計方式設定之屬性的詳細資訊，請參閱[通用屬性](../Topic/Common%20Properties.md)。  
  
 如需有關如何設定屬性的詳細資訊，請按下列其中一個主題：  
  
-   [設定資料流程元件的屬性](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## 相關工作  
 [使用聯集全部轉換來合併資料](../../../integration-services/data-flow/transformations/merge-data-by-using-the-union-all-transformation.md)  
  
  