---
title: 加入或刪除使用者定義的階層 |Microsoft 文件
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- hierarchies [Analysis Services], adding
- removing hierarchies
- adding hierarchies
- deleting hierarchies
- hierarchies [Analysis Services], removing
ms.assetid: 953818b4-9543-4c01-bb20-1d45ec6dfb91
caps.latest.revision: 50
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 57e1f74d612add88c6a2c47497f0d6a55c64c665
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36134829"
---
# <a name="add-or-delete-a-user-defined-hierarchy"></a>加入或刪除使用者定義階層
  您會在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中，維度設計師的 [維度結構] 索引標籤上，從維度中加入或移除使用者自訂階層。  
  
 當您加入使用者自訂階層時，要等到在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體中具現化使用者自訂階層，而且處理維度之後，才可以提供此階層給使用者使用。 如需詳細資訊，請參閱[多維度模型資料庫&#40;SSAS&#41; ](multidimensional-model-databases-ssas.md)和[多維度模型物件處理](processing-a-multidimensional-model-analysis-services.md)。  
  
### <a name="to-add-a-user-defined-hierarchy-to-a-dimension"></a>將使用者自訂階層加入維度  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中，開啟適當的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案，然後開啟您想要使用的維度。  
  
     此維度會在 [維度設計師] 的 [維度結構] 索引標籤上開啟。  
  
2.  從 [屬性] 窗格中，將您要在使用者自訂階層中使用的屬性拖曳到 [階層] 窗格。  
  
3.  拖曳其他屬性，以便在使用者自訂階層中形成層級。  
  
     屬性列在階層中的順序很重要。 例如，在時間階層中，年應該出現在高於天的階層清單中。  
  
4.  也可以選擇，將使用者自訂階層中的層級拖曳到正確位置上，以重新排列這些階層。  
  
5.  也可以選擇，修改使用者自訂階層或其層級的屬性。  
  
     例如，您可能會想要指定使用者自訂階層的名稱，也可能重新命名一個或多個層級，然後定義「全部」層級的自訂名稱。 如需詳細資訊，請參閱[使用者階層屬性](../multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md)，和[層級屬性&#91;Paved Over&#93;](../multidimensional-models-olap-logical-dimension-objects/user-hierarchies-level-properties.md)。  
  
    > [!NOTE]  
    >  依預設，使用者自訂階層就是可以讓使用者向下鑽研資訊的路徑。 但是，如果層級之間有關聯性存在，則可以設定層級之間的屬性關聯性來提升查詢效能。 如需詳細資訊，請參閱 [屬性關聯性](../multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md) 和 [定義屬性關聯性](attribute-relationships-define.md)。  
  
### <a name="to-remove-a-user-defined-hierarchy-from-a-dimension"></a>從維度中移除使用者自訂階層  
  
-   在 [維度結構] 索引標籤上，按一下要在 [階層] 窗格中移除的使用者自訂階層。 在工具列上，按一下 [刪除]。  
  
     — 或者—  
  
-   在 [階層] 窗格中以滑鼠右鍵按一下要移除的使用者定義階層，然後按一下 [刪除]。  
  
     — 或者—  
  
-   將使用者自訂階層拖曳出設計介面。  
  
## <a name="see-also"></a>另請參閱  
 [使用者階層](../multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md)   
 [建立使用者定義階層](user-defined-hierarchies-create.md)  
  
  