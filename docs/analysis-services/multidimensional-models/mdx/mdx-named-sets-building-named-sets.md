---
title: 建立名為 MDX (MDX) 中的集合 |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b893dcd86ffcfa68c55057796c431e694903c46a
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34021275"
---
# <a name="mdx-named-sets---building-named-sets"></a>MDX 命名集-建立命名集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  集合運算式可能是一項冗長而複雜的宣告，因而不太容易遵照和了解。 或者，可能會相當頻繁地使用集合運算式，一再定義該集合就變得相當惱人。 若要讓冗長、複雜或經常使用的運算式更為容易處理，多維度運算式 (MDX) 可讓您將這類運算式作為「命名集」。  
  
 基本上，命名集是一個已指派別名的集合運算式。 命名集可以包含通常被包含於集合中的任何成員或函數。 因為 MDX 會將命名集別名視為集合運算式，您可以在可接受集合運算式的任何地方使用那個別名。  
  
 您可以定義命名集，以擁有以下其中一個內容：  
  
-   **查詢範圍** ：若要建立一個命名集，把它定義為 MDX 查詢的一部分，而且範圍限制在查詢內，請使用 WITH 關鍵字。 然後您就可以在 MDX SELECT 陳述式內使用命名集。 使用這種方式，可以變更利用 WITH 關鍵字建立的命名集，而不會影響到 SELECT 陳述式。  
  
     如需如何使用 WITH 關鍵字來建立命名集的詳細資訊，請參閱[建立查詢範圍命名集 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-named-sets-creating-query-scoped-named-sets.md)。  
  
-   **工作階段範圍**：若要建立一個範圍超出查詢內容的命名集，也就是說它的範圍是 MDX 工作階段的存留時間，您可以使用 CREATE SET 陳述式。 使用 CREATE SET 陳述式定義的命名集，可以在那個工作階段中的所有 MDX 查詢使用。 對於需要在不同查詢中重覆使用某一命名集的用戶端應用程式而言，CREATE SET 陳述式是很有用處的。  
  
     如需如何使用 CREATE SET 陳述式來建立工作階段中的命名集的詳細資訊，請參閱[建立工作階段範圍命名集 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-named-sets-creating-session-scoped-named-sets.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SELECT 陳述式 & #40;MDX & #41;](../../../mdx/mdx-data-manipulation-select.md)   
 [建立 SET 陳述式 & #40;MDX & #41;](../../../mdx/mdx-data-definition-create-set.md)   
 [MDX 查詢基礎觀念 & #40;Analysis Services & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  
