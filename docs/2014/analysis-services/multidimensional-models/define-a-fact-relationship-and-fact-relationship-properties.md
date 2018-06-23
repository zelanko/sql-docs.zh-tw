---
title: 定義事實關聯性及事實關聯性屬性 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- fact dimensions [Analysis Services]
ms.assetid: d8e41724-da77-4ac1-bc42-956b5d91ea5d
caps.latest.revision: 10
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: f122cd92a08b4de54c01ca224fab7a02c4a7f87f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36035325"
---
# <a name="define-a-fact-relationship-and-fact-relationship-properties"></a>定義事實關聯性及事實關聯性屬性
  當您定義新的 Cube 維度或新的量值群組時，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會嘗試偵測是否有事實維度關聯性，然後將維度使用方式設定設為 `Fact`。 您可以在 Cube 設計師的 [維度使用方式] 索引標籤上，檢視或編輯事實維度關聯性。 維度和量值群組之間的事實關聯性具有下列條件約束：  
  
-   Cube 維度只能與特定量值群組有單一事實關聯性。  
  
-   Cube 維度可以與多個量值群組有不同的事實關聯性。  
  
-   關聯性的資料粒度屬性必須是維度的索引鍵屬性 (例如，交易號碼)。 這會在維度和事實資料表的事實之間建立一對一關聯性。  
  
  