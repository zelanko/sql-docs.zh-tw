---
title: 定義 Cube 屬性內容 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- cubes [Analysis Services], defining
ms.assetid: 579ca818-f33d-4060-906d-c8bfee93bf99
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2e84c49055a1fdb5b11487ab17af19762f86686c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62726412"
---
# <a name="define-cube-attribute-properties"></a>定義 Cube 屬性 (Attribute) 屬性 (Property)
  Cube 屬性 (Attribute) 的屬性 (Property) 可讓您根據同一個資料庫維度，為 Cube 維度中的維度屬性 (Attribute) 指定唯一的設定。 下表描述 Cube 屬性 (Attribute) 的屬性 (Property)。  
  
|屬性|描述|  
|--------------|-----------------|  
|`AggregationUsage`|指定 [彙總設計精靈] 將如何設計這個屬性的彙總。 此屬性可以有下列的值：<br /><br /> `Default`:預設值。 [彙總設計精靈] 會根據屬性的類型來套用預設規則 (Full 代表索引鍵，Unrestricted 代表其他項目)。<br /><br /> `None`:此 Cube 不應該有任何彙總包含這個屬性。<br /><br /> `Unrestricted`:彙總設計精靈 沒有任何限制。<br /><br /> `Full`:此 Cube 的每一個彙總都必須包含這個屬性。|  
|`AttributeHierarchyEnabled`|識別這個 Cube 維度上是否啟用此屬性階層， 如此可允許在特定 Cube 或維度角色上停用屬性階層。 如果已停用基礎屬性階層，這個設定不會有任何作用。 預設值為 `True`。|  
|`OptimizedState`|指出這個 Cube 維度上是否要最佳化此屬性階層， 如此可允許在特定 Cube 或維度角色上最佳化屬性階層。 如果基礎屬性階層並未最佳化，這個設定不會有任何作用。 此屬性可以有下列的值：<br /><br /> `FullyOptimized`:預設值。 執行個體會建立階層的索引，以增進查詢效能。 這是預設值。<br /><br /> `NotOptimized`:執行個體不會建立其他索引。|  
|`AttributeHierarchyVisible`|指出這個 Cube 維度上是否可以看見此屬性階層， 如此可允許在特定 Cube 或維度角色上看見屬性階層。 如果看不到基礎屬性階層，這個設定不會有任何作用。 預設值是 `True`。|  
|`AttributeID`|包含此屬性的唯一識別碼 (ID)。|  
  
## <a name="see-also"></a>另請參閱  
 [定義 Cube 維度屬性](define-cube-dimension-properties.md)   
 [定義 Cube 階層屬性](define-cube-hierarchy-properties.md)  
  
  
