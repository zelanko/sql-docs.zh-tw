---
title: 採礦結構資料行 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining [Analysis Services], structure
- mining structures [Analysis Services], columns
- data sources [Analysis Services], mining structure columns
- columns [data mining], mining structure columns
ms.assetid: 20cbf433-70d1-4b61-a462-41a8435b27b4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1c843a74b831315c98deda9a9d6fb0c3a463bc5c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66083407"
---
# <a name="mining-structure-columns"></a>採礦結構資料行
  當您建立採礦結構時會定義採礦結構中的資料行，其方法是選擇外部資料的資料行，然後指定資料如何用於模型化。 因此，採礦結構資料行不只是資料來源中的資料複本：這些資料行會定義採礦模型如何使用來源中的資料。 您可以指派可判斷如何將資料離散化的屬性以及可描述如何分佈資料值的屬性。  
  
 採礦結構資料行的設計就是要提供彈性和擴充性，因為您用於建立採礦模型的每一個演算法，都可能使用結構中的不同資料行來解譯資料。 您可以使用單一採礦結構並使用其中的資料行來自訂每一個模型的資料，而不必在每一個模型中都有一組資料。  
  
## <a name="defining-mining-structure-columns"></a>定義採礦結構資料行  
 定義結構資料行的基本資料類型和內容類型是衍生自您用於建立結構的資料來源。 您可以在採礦結構內變更這些設定，也可以設定模型旗標和設定連續資料行的分佈。  
  
 採礦結構資料行的定義必須包含下列資訊：  
  
-   **識別碼**：資料行，通常與名稱相同的唯一名稱。 在您建立採礦結構之後無法變更識別碼，但是可以變更名稱。  
  
-   **名稱**：名稱或別名資料行中。  
  
-   **內容**:描述資料為離散或連續的列舉。  
  
-   **類型**：列舉型別，表示一般資料類型。  
  
-   **發佈**:列舉型別描述預期的值分佈。 如果資料行是連續的，便包括分佈。  
  
-   **模型旗標**:列舉，指出如何處理遺失值等。 也可以在採礦模型上定義模型旗標，但是這些模型旗標與結構資料行上使用的旗標不一樣。  
  
-   **繫結**:指定來源資料的屬性。  
  
 協力廠商演算法也可以包括可在採礦結構資料行上定義的自訂屬性。  
  
 如需資料採礦結構和資料採礦模型的詳細資訊，請參閱 [採礦結構 &#40;Analysis Services - 資料採礦&#41;](mining-structures-analysis-services-data-mining.md)。  
  
## <a name="related-content"></a>相關內容  
 如需有關如何定義及使用採礦結構資料行的詳細資訊，請參閱下列主題。  
  
|主題|連結|  
|-----------|-----------|  
|描述您可以用於定義採礦結構資料行的資料類型。|[資料類型 &#40;資料採礦&#41;](data-types-data-mining.md)|  
|描述可供採礦結構資料行內包含之每一個資料類型使用的內容類型。 內容類型相依於資料類型。 內容類型會在模型層級指派，而且會決定模型使用資料行資料的方式。|[內容類型 &#40;資料採礦&#41;](content-types-data-mining.md)|  
|介紹巢狀資料表的概念，並說明如何將巢狀資料表當做採礦結構資料行加入至資料來源。|[分類資料行 &#40;資料採礦&#41;](classified-columns-data-mining.md)|  
|列出並說明您可以在採礦結構資料行上設定的分佈屬性，以便指定資料行中預期的值分佈。|[資料行分佈 &#40;資料採礦&#41;](column-distributions-data-mining.md)|  
|說明分隔 (有時稱為「資料收納」  ) 的概念，並描述 Analysis Services 為分隔連續數值資料所提供的方法。|[分隔方法 &#40;資料採礦&#41;](discretization-methods-data-mining.md)|  
|描述您可以在採礦結構資料行上設定的模型旗標。|[模型旗標 &#40;資料採礦&#41;](modeling-flags-data-mining.md)|  
|描述分類資料行，這是一種特殊類型的資料行，可用來讓採礦結構資料行之間產生關聯。|[分類資料行 &#40;資料採礦&#41;](classified-columns-data-mining.md)|  
|學習加入及修改採礦結構資料行。|[採礦結構工作和使用說明](mining-structure-tasks-and-how-tos.md)|  
  
## <a name="see-also"></a>另請參閱  
 [採礦結構 &#40;Analysis Services - 資料採礦&#41;](mining-structures-analysis-services-data-mining.md)   
 [採礦模型資料行](mining-model-columns.md)  
  
  
