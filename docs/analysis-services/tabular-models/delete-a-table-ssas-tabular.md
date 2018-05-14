---
title: 刪除資料表 |Microsoft 文件
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: de1fa5d58beb36a5f3a7ce6eee0c09c5636acfd4
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="delete-a-table"></a>刪除資料表
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  在模型設計師中，您可以刪除模型工作空間資料庫中不再需要的資料表。 刪除資料表並不會影響原始來源資料，只會影響您匯入並在其中處理的資料。 您無法恢復資料表的刪除作業。  
  
### <a name="to-delete-a-table"></a>若要刪除資料表  
  
-   針對您要刪除的資料表，以滑鼠右鍵按一下模型設計師底部的索引標籤，然後按一下 [刪除]。  
  
## <a name="considerations-when-deleting-tables"></a>刪除資料表時的考量  
  
-   當您刪除資料表時，資料表所在的整個索引標籤都會遭到刪除。  
  
-   如果有任何量值與該資料表相關聯，則也會刪除該量值的定義。  
  
-   如果您使用該資料表建立任何導出資料行，該資料表中的資料行也會遭到刪除；其他資料表中使用已刪除資料表之資料行的所有導出資料行則會顯示錯誤。  
  
## <a name="see-also"></a>另請參閱  
 [資料表和資料行](../../analysis-services/tabular-models/tables-and-columns-ssas-tabular.md)  
  
  
