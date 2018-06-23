---
title: 內容元素 (ASSL) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Content Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Content
helpviewer_keywords:
- Content element
ms.assetid: 221addef-2f88-49c5-b8f5-9eee330497a9
caps.latest.revision: 42
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 98d2de4a0ce93e857a63ebd9fe79dd18d0f9a86e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36031304"
---
# <a name="content-element-assl"></a>Content 元素 (ASSL)
  說明內容中的資料行的[MiningStructure](../objects/miningstructure-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ScalarMiningStructureColumn>  
   ...  
   <Content>...</Content>  
   ...  
</ScalarMiningStructureColumn>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|無|  
|基數|1-1：只能出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[ScalarMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個列舉會描述採礦結構資料行所代表的內容類型，而且可由採礦演算法提供者視需要擴充。 如需內容類型的詳細資訊，請參閱[內容類型 &#40;資料採礦&#41;](../../data-mining/content-types-data-mining.md)。  
  
 下表所列的值通常受到所有採礦演算法提供者支援。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|*離散*|此資料行包含離散值。|  
|*連續*|此資料行的值會定義一組連續的數值資料。|  
|*離散化*|此資料行的值代表衍生自連續資料行之值的群組 (或值區)。|  
|*排序*|此資料行的值會定義已排序集合。|  
|*循環*|此資料行的值會定義循環的已排序集合。|  
|*機率*|資料行的值指定資料行中包含機率[ClassifiedColumns](../collections/columns-element-assl.md)父元素之`ScalarMiningStructureColumn`。|  
|*Variance*|此資料行的值會針對包含在父 `ClassifiedColumns` 之 `ScalarMiningStructureColumn` 元素中的資料行指定變異數。|  
|*標準差*|此資料行的值會針對包含在父 `ClassifiedColumns` 之 `ScalarMiningStructureColumn` 元素中的資料行指定標準差。|  
|*ProbabilityVariance*|此資料行的值會針對包含在父 `ClassifiedColumns` 之 `ScalarMiningStructureColumn` 元素中的資料行指定機率變異數。|  
|*ProbabilityStdDev*|此資料行的值會針對包含在父 `ClassifiedColumns` 之 `ScalarMiningStructureColumn` 元素中的資料行指定機率標準差。|  
|*支援*|此資料行的值會針對包含在父 `ClassifiedColumns` 之 `ScalarMiningStructureColumn` 元素中的資料行指定支援資訊。 **注意：** 這個資料行提供標準的一部分為協力廠商採礦演算法提供者。 **注意：** Microsoft 提供的演算法沒有任何使用此資料行。 <br /><br /> 執行個體時提供 SQL Server 登入。|  
|*索引鍵*|此資料行為索引鍵資料行。 **注意：** 此內容類型是僅適用於索引鍵資料行，其中`IsKey`元素設定為`True`。|  
  
 除了這些標準值時，採礦演算法提供者隨附[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]支援下表中的值。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|*索引鍵的順序*|此資料行為索引鍵資料行，而且資料行的值代表事件序列。 **注意：** 此內容類型是僅適用於索引鍵資料行，其中`IsKey`元素設定為`True`。|  
|*Key Time*|此資料行為索引鍵資料行，而且資料行的值代表時間測量單位。 **注意：** 此內容類型是僅適用於索引鍵資料行，其中`IsKey`元素設定為`True`。|  
|*序列*|此資料行的值代表事件序列。|  
|*Time*|此資料行的值代表時間測量單位。|  
  
 在「分析管理物件」(AMO) 物件模型中對應至 `Content` 允許值的列舉是 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>。  
  
## <a name="see-also"></a>另請參閱  
 [ClassifiedColumns 元素&#40;ASSL&#41;](../collections/columns-element-assl.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  