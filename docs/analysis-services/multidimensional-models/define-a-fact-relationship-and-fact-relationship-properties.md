---
title: "定義事實關聯性及事實關聯性屬性 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: fact dimensions [Analysis Services]
ms.assetid: d8e41724-da77-4ac1-bc42-956b5d91ea5d
caps.latest.revision: "10"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: e1e58f9616fc40ad895858a6eb6b3cfa7e0bbed1
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2017
---
# <a name="define-a-fact-relationship-and-fact-relationship-properties"></a>定義事實關聯性及事實關聯性屬性
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]當您定義新的 cube 維度或新的量值群組，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]會嘗試偵測是否有事實維度關聯性存在，並將維度使用方式設定設**事實**。 您可以在 Cube 設計師的 [維度使用方式] 索引標籤上，檢視或編輯事實維度關聯性。 維度和量值群組之間的事實關聯性具有下列條件約束：  
  
-   Cube 維度只能與特定量值群組有單一事實關聯性。  
  
-   Cube 維度可以與多個量值群組有不同的事實關聯性。  
  
-   關聯性的資料粒度屬性必須是維度的索引鍵屬性 (例如，交易號碼)。 這會在維度和事實資料表的事實之間建立一對一關聯性。  
  
  
