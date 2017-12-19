---
title: "定義 Cube 屬性 (Property) |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: cubes [Analysis Services], defining
ms.assetid: 579ca818-f33d-4060-906d-c8bfee93bf99
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f051a3372b965e2652dfd6ea4c57826212509c1d
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2017
---
# <a name="define-cube-attribute-properties"></a>定義 Cube 屬性 (Attribute) 屬性 (Property)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Cube 屬性 (property) 可讓您在同一資料庫維度為基礎的 cube 維度中指定唯一設定維度屬性。 下表描述 Cube 屬性 (Attribute) 的屬性 (Property)。  
  
|屬性|說明|  
|--------------|-----------------|  
|**AggregationUsage**|指定 [彙總設計精靈] 將如何設計這個屬性的彙總。 預設值為 **Default**。 此屬性可以有下列的值：<br /><br /> **預設值**：<br />                    [彙總設計精靈] 會根據屬性的類型來套用預設規則 (Full 代表索引鍵，Unrestricted 代表其他項目)。<br /><br /> **無**：<br />                    此 Cube 不應該有任何彙總包含這個屬性。<br /><br /> **不受限制**：<br />                    [彙總設計精靈] 沒有任何限制<br /><br /> **完整**：<br />                    此 Cube 的每一個彙總都必須包含這個屬性。|  
|**AttributeHierarchyEnabled**|識別這個 Cube 維度上是否啟用此屬性階層， 如此可允許在特定 Cube 或維度角色上停用屬性階層。 如果已停用基礎屬性階層，這個設定不會有任何作用。 預設值為 [True]。|  
|**OptimizedState**|指出這個 Cube 維度上是否要最佳化此屬性階層， 如此可允許在特定 Cube 或維度角色上最佳化屬性階層。 如果基礎屬性階層並未最佳化，這個設定不會有任何作用。 預設值是 **FullyOptimized**。 此屬性可以有下列的值：<br /><br /> **FullyOptimized**：執行個體會建立階層的索引，以增進查詢效能。 這是預設值。<br /><br /> **NotOptimized**：<br />                    執行個體不會建立其他索引。|  
|**AttributeHierarchyVisible**|指出這個 Cube 維度上是否可以看見此屬性階層， 如此可允許在特定 Cube 或維度角色上看見屬性階層。 如果看不到基礎屬性階層，這個設定不會有任何作用。 預設值為 **True**。|  
|**AttributeID**|包含此屬性的唯一識別碼 (ID)。|  
  
## <a name="see-also"></a>請參閱  
 [定義 Cube 維度屬性](../../analysis-services/multidimensional-models/define-cube-dimension-properties.md)   
 [定義 Cube 階層屬性](../../analysis-services/multidimensional-models/define-cube-hierarchy-properties.md)  
  
  
