---
title: "建置導出的成員的 MDX (MDX) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- MDX [Analysis Services], calculated members
- calculated members [MDX]
- Multidimensional Expressions [Analysis Services], calculated members
- queries [MDX], calculated members
ms.assetid: 9322e8b8-43e1-4e02-a7d1-e41a586a5bb8
caps.latest.revision: "29"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 03ee94149faf02f0ef99bdde82f4f5847842fd57
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="mdx-calculated-members---building-calculated-members"></a>MDX 導出成員-建立導出的成員
  在多維度運算式 (MDX) 中，導出成員是藉由計算 MDX 運算式以傳回一個值而解析出來的成員。 此一定義涵蓋的範圍相當廣泛。 在 MDX 查詢中建構和使用導出成員的能力，提供了許多管理多維度資料的功能。  
  
 您可以在階層內的任意點建立導出成員。 您也可以建立一個導出成員，使它不僅要依據 Cube 中現有的成員，還要依據同一 MDX 運算式中定義的其他導出成員。  
  
 您可以定義導出成員，以擁有以下其中一個內容：  
  
-   **查詢範圍** ：若要建立一個導出資料格，把它定義為 MDX 查詢的一部份，而且範圍限制在查詢內，請使用 WITH 關鍵字。 然後您就可以在 MDX SELECT 陳述式內使用導出成員。 使用這種方式，可以變更利用 WITH 關鍵字建立的導出成員，而不會影響到 SELECT 陳述式。  
  
     如需如何使用 WITH 關鍵字建立導出成員的詳細資訊，請參閱[建立查詢範圍導出成員 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-calculated-members-query-scoped-calculated-members.md)。  
  
-   **工作階段範圍**：若要建立一個範圍超出查詢內容的導出成員，也就是說它的範圍是 MDX 工作階段的存留時間，您可以使用 CREATE MEMBER 陳述式。 使用 CREATE MEMBER 陳述式定義的導出成員，可以在那個工作階段中的所有 MDX 查詢使用。 對於需要在不同查詢中重覆使用相同命名集的用戶端應用程式而言，CREATE MEMBER 陳述式很有用處。  
  
     如需如何使用 CREATE MEMBER 陳述式來建立工作階段中導出成員的詳細資訊，請參閱[建立工作階段範圍導出成員 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-calculated-members-session-scoped-calculated-members.md)。  
  
## <a name="see-also"></a>請參閱＜  
 [CREATE MEMBER 陳述式 &#40;MDX&#41;](../../../mdx/mdx-data-definition-create-member.md)   
 [MDX 函數參考 &#40;MDX&#41;](../../../mdx/mdx-function-reference-mdx.md)   
 [SELECT 陳述式 &#40;MDX &#41;](../../../mdx/mdx-data-manipulation-select.md)  
  
  
