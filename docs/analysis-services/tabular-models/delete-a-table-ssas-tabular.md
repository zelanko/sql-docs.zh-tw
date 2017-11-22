---
title: "刪除資料表 (SSAS 表格式) |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: be4ed45f-fde3-466c-9869-49bd3ddb505e
caps.latest.revision: "9"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: be456ceeef0d8d965c9e922bffbcec0507cb3777
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="delete-a-table-ssas-tabular"></a>刪除資料表 (SSAS 表格式)
  在模型設計師中，您可以刪除模型工作空間資料庫中不再需要的資料表。 刪除資料表並不會影響原始來源資料，只會影響您匯入並在其中處理的資料。 您無法恢復資料表的刪除作業。  
  
### <a name="to-delete-a-table"></a>若要刪除資料表  
  
-   針對您要刪除的資料表，以滑鼠右鍵按一下模型設計師底部的索引標籤，然後按一下 [刪除]。  
  
## <a name="considerations-when-deleting-tables"></a>刪除資料表時的考量  
  
-   當您刪除資料表時，資料表所在的整個索引標籤都會遭到刪除。  
  
-   如果有任何量值與該資料表相關聯，則也會刪除該量值的定義。  
  
-   如果您使用該資料表建立任何導出資料行，該資料表中的資料行也會遭到刪除；其他資料表中使用已刪除資料表之資料行的所有導出資料行則會顯示錯誤。  
  
## <a name="see-also"></a>請參閱＜  
 [資料表與資料行 &#40;SSAS 表格式&#41;](../../analysis-services/tabular-models/tables-and-columns-ssas-tabular.md)  
  
  
