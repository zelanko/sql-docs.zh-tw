---
title: 定義 Cube 階層屬性 |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9632719018cf91eebc97b7a56e651bdc3037e5a3
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="define-cube-hierarchy-properties"></a>定義 Cube 階層屬性
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Cube 階層屬性可以讓您根據同一個資料庫維度，為 Cube 維度中的使用者自訂階層指定唯一設定。 下表描述 Cube 階層的屬性。  
  
|屬性|Description|  
|--------------|-----------------|  
|**已啟用**|決定是否為 Cube 維度啟用階層。|  
|**HierarchyID**|包含階層的唯一識別碼 (ID)。|  
|**OptimizedState**|決定套用至階層的最佳化層級。 此屬性可以有下列的值：<br /><br /> **FullyOptimized**：<br />                    執行個體會建立階層的索引，以增進查詢效能。 這是預設值。<br /><br /> **NotOptimized**：<br />                    執行個體不會建立其他索引。|  
|**Visible**|決定 Cube 階層的可見性。 預設值為 **True**。|  
  
## <a name="see-also"></a>另請參閱  
 [使用者階層](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md)  
  
  
