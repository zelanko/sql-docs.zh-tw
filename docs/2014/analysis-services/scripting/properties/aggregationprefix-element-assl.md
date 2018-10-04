---
title: AggregationPrefix 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- AggregationPrefix Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AggregationPrefix
helpviewer_keywords:
- AggregationPrefix element
ms.assetid: 1581e0df-ae8e-41ce-9c92-f0f7cac487f2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c6cb7355644a437b7427dcd366c5f102f469135a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48121538"
---
# <a name="aggregationprefix-element-assl"></a>AggregationPrefix 元素 (ASSL)
  定義要在整個相關聯父元素中用於彙總名稱的一般前置詞。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Cube> <!-- or Database, MeasureGroup, Partition -->  
   ...  
   <AggregationPrefix>...</AggregationPrefix>  
   ...  
</Database>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|None|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Cube](../objects/cube-element-assl.md)，[資料庫](../objects/database-element-assl.md)， [MeasureGroup](../objects/group-element-assl.md)，[資料分割](../objects/partition-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 彙總前置詞產生彙總鼎[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]，而且也會儲存在關聯式 OLAP (ROLAP) 資料分割的彙總在關聯式資料庫中產生資料表名稱。  
  
 完全展開的彙總名稱具有下列部分：  
  
 *\<DatabasePrefix >\<CubePrefix >\<MeasureGroupPrefix >\<PartitionPrefix >\<AggregationID >*  
  
 彙總名稱的前四個部分組成彙總前置詞。 使用者會提供前四個部分：  
  
-   *DatabasePrefix*代表的值`AggregationPrefix`相關聯的項目`Database`項目。  
  
-   *CubePrefix*代表的值`AggregationPrefix`相關聯的項目`Cube`項目。  
  
-   *MeasureGroupPrefix*代表的值`AggregationPrefix`相關聯的項目`MeasureGroup`項目。  
  
-   *PartitionPrefix*代表的值`AggregationPrefix`相關聯的項目`Partition`項目。  
  
 名稱 的第五個部分*AggregationID*是系統定義的識別碼，且使用者無權控制這一部分的名稱。  
  
 在「分析管理物件」(AMO) 物件模型中對應至 `AggregationPrefix` 父系的元素是 <xref:Microsoft.AnalysisServices.Cube>、<xref:Microsoft.AnalysisServices.Database>、<xref:Microsoft.AnalysisServices.MeasureGroup> 和 <xref:Microsoft.AnalysisServices.Partition>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
