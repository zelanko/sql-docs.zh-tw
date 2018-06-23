---
title: 定義 Cube 屬性 (Property) |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- cubes [Analysis Services], defining
ms.assetid: 579ca818-f33d-4060-906d-c8bfee93bf99
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 09285c7b1492905fa6a7155e5abdc7ba5bfaf1ed
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36133556"
---
# <a name="define-cube-attribute-properties"></a>定義 Cube 屬性 (Attribute) 屬性 (Property)
  Cube 屬性 (Attribute) 的屬性 (Property) 可讓您根據同一個資料庫維度，為 Cube 維度中的維度屬性 (Attribute) 指定唯一的設定。 下表描述 Cube 屬性 (Attribute) 的屬性 (Property)。  
  
|屬性|描述|  
|--------------|-----------------|  
|`AggregationUsage`|指定 [彙總設計精靈] 將如何設計這個屬性的彙總。 此屬性可以有下列的值：<br /><br /> `Default`： 預設值。 [彙總設計精靈] 會根據屬性的類型來套用預設規則 (Full 代表索引鍵，Unrestricted 代表其他項目)。<br /><br /> `None`： 沒有 cube 的彙總應該包含這個屬性。<br /><br /> `Unrestricted`： 彙總設計精靈沒有沒有限制。<br /><br /> `Full`： 每個 cube 的彙總必須包含這個屬性。|  
|`AttributeHierarchyEnabled`|識別這個 Cube 維度上是否啟用此屬性階層， 如此可允許在特定 Cube 或維度角色上停用屬性階層。 如果已停用基礎屬性階層，這個設定不會有任何作用。 預設值是`True`。|  
|`OptimizedState`|指出這個 Cube 維度上是否要最佳化此屬性階層， 如此可允許在特定 Cube 或維度角色上最佳化屬性階層。 如果基礎屬性階層並未最佳化，這個設定不會有任何作用。 此屬性可以有下列的值：<br /><br /> `FullyOptimized`： 預設值。 執行個體會建立階層的索引，以增進查詢效能。 這是預設值。<br /><br /> `NotOptimized`： 執行個體不會建立其他索引。|  
|`AttributeHierarchyVisible`|指出這個 Cube 維度上是否可以看見此屬性階層， 如此可允許在特定 Cube 或維度角色上看見屬性階層。 如果看不到基礎屬性階層，這個設定不會有任何作用。 預設值是 `True`。|  
|`AttributeID`|包含此屬性的唯一識別碼 (ID)。|  
  
## <a name="see-also"></a>另請參閱  
 [定義 Cube 維度屬性](define-cube-dimension-properties.md)   
 [定義 Cube 階層屬性](define-cube-hierarchy-properties.md)  
  
  