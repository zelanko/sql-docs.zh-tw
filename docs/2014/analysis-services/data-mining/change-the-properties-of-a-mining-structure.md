---
title: 變更採礦結構的屬性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining structures [Analysis Services], properties
ms.assetid: 03b16897-2e36-42b8-9f7d-db1b9b898401
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7c9ca227753b8ebbd80d4de0c672fc8cab5c1b56
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66085856"
---
# <a name="change-the-properties-of-a-mining-structure"></a>變更採礦結構的屬性
  採礦結構有兩種屬性，這兩種屬性都可以修改：  
  
-   影響整個採礦結構的採礦結構屬性  
  
-   採礦結構中個別資料行的屬性  
  
 請注意，某些屬性相依於其他屬性設定值。 例如，在您將資料行的資料類型設定為 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationMethod%2A> 之前，無法設定控制分類收納行為的屬性 (例如 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationBucketCount%2A> 或 `Discretized`)。  
  
 如需採礦結構屬性的詳細資訊，請參閱 [Mining Structure Columns](mining-structure-columns.md)(採礦結構資料行)。  
  
### <a name="to-change-the-properties-of-a-mining-structure"></a>若要變更採礦結構的屬性  
  
1.  在資料採礦設計師的 [採礦結構]**** 索引標籤上，以滑鼠右鍵按一下採礦結構或採礦結構中的資料行，然後選取 [屬性]****。  
  
     如果 **[屬性]** 視窗還沒有出現，則它會在螢幕的右邊開啟。  
  
2.  在 **[屬性]** 視窗中，選取對應到您要變更之屬性的值，然後輸入新值。  
  
     您在設計師中選取其他元素時，新值就會生效。  
  
## <a name="see-also"></a>另請參閱  
 [採礦結構工作和使用說明](mining-structure-tasks-and-how-tos.md)  
  
  
