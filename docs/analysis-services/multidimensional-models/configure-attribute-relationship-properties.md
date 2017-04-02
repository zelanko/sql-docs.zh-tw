---
title: "設定屬性 (Attribute) 關聯性屬性 (Property) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
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
  - "彈性關聯性 (Analysis Services)"
  - "屬性 [Analysis Services], 關聯性"
  - "關聯性 [Analysis Services], 屬性"
  - "屬性 [Analysis Services], 屬性關聯性"
  - "固定關聯性 (Analysis Services)"
ms.assetid: fce511af-66d7-42fc-bb3a-6c516f16b10e
caps.latest.revision: 17
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# 設定屬性 (Attribute) 關聯性屬性 (Property)
  下表列出及描述屬性 (Attribute) 關聯性的屬性 (Property)。  
  
|屬性|說明|  
|--------------|-----------------|  
|Attribute|包含屬性的名稱。|  
|基數|指出關聯性的基數。 值可為許多 (針對多對一的關聯性)，或是一 (針對一對一的關聯性)。 預設值是「許多」。 在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中，Cardinality 屬性沒有作用，它是保留以備將來實作使用。|  
|名稱|包含屬性的易記名稱。|  
|RelationshipType|指出成員關聯性是否會隨時間變更。 值可為 Rigid，表示成員之間的關聯性並不會隨著時間變更；或為 Flexible，表示成員之間的關聯性會隨時間變更。 預設值是 Flexible。 如果將關聯性定義為彈性，彙總會進行卸除，並重新計算做為累加式更新的一部分 (如果只是加入新成員，就不會卸除)。 如果將關聯性定義為固定，當維度進行累加式更新時，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會保留彙總。 如果定義為固定的關聯性變更了，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 就會在累加式處理期間產生錯誤。 指定適當的關聯性和關聯性屬性可增加查詢和處理效能。|  
|Visible|決定屬性關聯性是否可見。 值為 True 或 False。 預設值是 True。|  
  
  