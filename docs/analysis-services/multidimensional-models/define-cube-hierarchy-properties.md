---
title: "定義 Cube 階層屬性 |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- hierarchies [Analysis Services], multilevel
- hierarchies [Analysis Services], cubes
ms.assetid: 819d0a4e-7815-4332-a605-b07ca2ade6ac
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 69781dd1476cd0396e748be0ddf91fd4dd0bb0dc
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="define-cube-hierarchy-properties"></a>定義 Cube 階層屬性
  Cube 階層屬性可以讓您根據同一個資料庫維度，為 Cube 維度中的使用者自訂階層指定唯一設定。 下表描述 Cube 階層的屬性。  
  
|屬性|說明|  
|--------------|-----------------|  
|**已啟用**|決定是否為 Cube 維度啟用階層。|  
|**HierarchyID**|包含階層的唯一識別碼 (ID)。|  
|**OptimizedState**|決定套用至階層的最佳化層級。 此屬性可以有下列的值：<br /><br /> **FullyOptimized**：<br />                    執行個體會建立階層的索引，以增進查詢效能。 這是預設值。<br /><br /> **NotOptimized**：<br />                    執行個體不會建立其他索引。|  
|**Visible**|決定 Cube 階層的可見性。 預設值為 **True**。|  
  
## <a name="see-also"></a>請參閱＜  
 [使用者階層](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md)  
  
  
