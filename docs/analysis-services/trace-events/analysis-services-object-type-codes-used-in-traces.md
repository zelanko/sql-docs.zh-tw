---
title: "Analysis Services 物件用於追蹤內的類型代碼 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: trace-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: e4119db1-4a41-4335-9b33-f1ea95564300
caps.latest.revision: 5
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 7bd50f15603440953dc2f9c52ae669e5fcbd3108
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="analysis-services-object-type-codes-used-in-traces"></a>用於追蹤內的 Analysis Services 物件類型代碼
  此頁面會列出 Analysis Services 資料模型中，每個物件的物件類型 (六位數數字)。 追蹤記錄檔中會出現這些程式碼，可用於識別與特定鎖定相關聯的物件類型。 例如，資料庫上的鎖定逾時會指出物件類型 100002 (也就是資料庫物件類型)。  
  
> [!NOTE]  
>  以下列出的程式碼數，超過追蹤記錄檔中實際出現的數目。 以下清單是每個物件的類型程式碼之完整清單，但只有採用鎖定的物件才會出現在追蹤記錄中內的物件類型程式碼。  
  
## <a name="object-type-reference"></a>物件類型參考  
  
|物件類型|物件名稱|  
|-----------------|-----------------|  
|100000|Server|  
|100001|Command|  
|100002|資料庫|  
|100003|DataSource|  
|100004|DatabasePermission|  
|100005|角色|  
|100006|維度|  
|100007|DimensionAttribute|  
|100008|階層|  
|100009|Level|  
|100010|Cube|  
|100011|CubePermission|  
|100012|CubeDimension|  
|100013|CubeAttribute|  
|100014|CubeHierarchy|  
|100016|MeasureGroup|  
|100017|MeasureGroupDimension|  
|100018|MeasureGroupAttribute|  
|100020|[量值]|  
|100021|資料分割|  
|100025|AggregationDesign|  
|100026|AggregationDesignDimension|  
|100027|AggregationDesignAttribute|  
|100028|彙總|  
|100029|AggregationDimension|  
|100030|AggregationAttribute|  
|100032|MiningStructure|  
|100033|MiningStructureColumn|  
|100037|MiningModel|  
|100038|MiningModelColumn|  
|100039|AlgorithmParameter|  
|100041|MiningModelPermission|  
|100042|DimensionPermission|  
|100043|MiningStructurePermission|  
|100044|組件|  
|100045|DatabaseRole|  
|100046|AttributePermission|  
|100047|CubeAttributePermission|  
|100048|CellPermission|  
|100049|CubeDimensionPermission|  
|100050|Trace|  
|100051|ServerAssembly|  
|100052|CubeAssembly|  
|100053|Command|  
|100054|KPI|  
|100055|DataSourceView|  
|100056|檢視方塊|  
|100100|CommandCollection|  
|100101|DatabaseCollection|  
|100102|DataSourceCollection|  
|100103|DatabasePermission|  
|100104|RoleCollection|  
|100105|DimensionCollection|  
|100106|DimensionAttributeCollection|  
|100107|HierarchyCollection|  
|100108|LevelCollection|  
|100109|CubeCollection|  
|100110|CubePermissionCollection|  
|100111|CubeDimensionCollection|  
|100112|CubeAttributeCollection|  
|100113|CubeHierarchyCollection|  
|100115|MeasureGroupCollection|  
|100116|MeasureGroupDimensionCollection|  
|100117|MeasureGroupAttributeCollection|  
|100119|MeasureCollection|  
|100120|PartitionCollection|  
|100124|AggregationDesignCollection|  
|100125|AggregationDesignDimensionCollection|  
|100126|AggregationDesignAttributeCollection|  
|100127|AggregationCollection|  
|100128|AggregationDimensionCollection|  
|100129|AggregationAttributeCollection|  
|100131|MiningStructureCollection|  
|100132|MiningStructureColumnCollection|  
|100136|MiningModelCollection|  
|100137|MiningModelColumnCollection|  
|100138|AlgorithmParameterCollection|  
|100140|MiningModelPermissionCollection|  
|100141|DimensionPermissionCollection|  
|100142|MiningStructurePermissionCollection|  
|100143|AssemblyCollection|  
|100144|DatabaseRoleCollecction|  
|100145|AttributePermissionCollection|  
|100146|CubeAttributePermissionCollection|  
|100147|CellPermissionCollection|  
|100148|CubeDimensionPermissionCollection|  
|100149|TraceCollection|  
|100150|ServerAssemblyCollection|  
|100151|CubeAssemblyCollection|  
|100152|CommandCollection|  
|100153|KpiCollection|  
|100154|DataSourceViewCollection|  
|100155|PerspectiveCollection|  
  
  

