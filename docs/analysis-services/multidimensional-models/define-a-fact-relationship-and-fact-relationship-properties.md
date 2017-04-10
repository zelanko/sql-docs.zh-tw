---
title: "定義事實關聯性及事實關聯性屬性 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "事實維度 [Analysis Services]"
ms.assetid: d8e41724-da77-4ac1-bc42-956b5d91ea5d
caps.latest.revision: 10
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 10
---
# 定義事實關聯性及事實關聯性屬性
  當您定義新的 Cube 維度或新的量值群組時，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會嘗試偵測是否有事實維度關聯性，然後將維度使用方式設定設為 **Fact**。 您可以在 Cube 設計師的 [維度使用方式] 索引標籤上，檢視或編輯事實維度關聯性。 維度和量值群組之間的事實關聯性具有下列條件約束：  
  
-   Cube 維度只能與特定量值群組有單一事實關聯性。  
  
-   Cube 維度可以與多個量值群組有不同的事實關聯性。  
  
-   關聯性的資料粒度屬性必須是維度的索引鍵屬性 (例如，交易號碼)。 這會在維度和事實資料表的事實之間建立一對一關聯性。  
  
  