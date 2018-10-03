---
title: 內容元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b27152b0c181061e25727270fd89bd423728a5a2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48097858"
---
# <a name="content-element-assl"></a>Content 元素 (ASSL)
  說明中的資料行的內容[MiningStructure](../objects/miningstructure-element-assl.md)項目。  
  
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
|預設值|None|  
|基數|1-1：只能出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[ScalarMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 這個列舉會描述採礦結構資料行所代表的內容類型，而且可由採礦演算法提供者視需要擴充。 如需內容類型的詳細資訊，請參閱[內容類型 &#40;資料採礦&#41;](../../data-mining/content-types-data-mining.md)。  
  
 下表所列的值通常受到所有採礦演算法提供者支援。  
  
|值|描述|  
|-----------|-----------------|  
|*不連續*|此資料行包含離散值。|  
|*連續*|此資料行的值會定義一組連續的數值資料。|  
|*離散化*|此資料行的值代表衍生自連續資料行之值的群組 (或值區)。|  
|*排序*|此資料行的值會定義已排序集合。|  
|*循環*|此資料行的值會定義循環的已排序集合。|  
|*機率*|資料行的值指定資料行中包含機率[ClassifiedColumns](../collections/columns-element-assl.md)項目之父代`ScalarMiningStructureColumn`。|  
|*Variance*|此資料行的值會針對包含在父 `ClassifiedColumns` 之 `ScalarMiningStructureColumn` 元素中的資料行指定變異數。|  
|*StdDev*|此資料行的值會針對包含在父 `ClassifiedColumns` 之 `ScalarMiningStructureColumn` 元素中的資料行指定標準差。|  
|*ProbabilityVariance*|此資料行的值會針對包含在父 `ClassifiedColumns` 之 `ScalarMiningStructureColumn` 元素中的資料行指定機率變異數。|  
|*ProbabilityStdDev*|此資料行的值會針對包含在父 `ClassifiedColumns` 之 `ScalarMiningStructureColumn` 元素中的資料行指定機率標準差。|  
|*支援*|此資料行的值會針對包含在父 `ClassifiedColumns` 之 `ScalarMiningStructureColumn` 元素中的資料行指定支援資訊。 **注意：** 本專欄的協力廠商採礦演算法提供者時，可作為標準的一部分。 **注意：** Microsoft 提供的演算法並沒有任何使用此資料行。 <br /><br /> .|  
|*索引鍵*|此資料行為索引鍵資料行。 **注意︰** 這個內容類型是僅適用於索引鍵資料行，其中`IsKey`元素設定為`True`。|  
  
 除了這些標準值，採礦演算法提供者隨附[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]支援下表中的值。  
  
|值|描述|  
|-----------|-----------------|  
|*索引鍵的順序*|此資料行為索引鍵資料行，而且資料行的值代表事件序列。 **注意︰** 這個內容類型是僅適用於索引鍵資料行，其中`IsKey`元素設定為`True`。|  
|*Key Time*|此資料行為索引鍵資料行，而且資料行的值代表時間測量單位。 **注意︰** 這個內容類型是僅適用於索引鍵資料行，其中`IsKey`元素設定為`True`。|  
|*序列*|此資料行的值代表事件序列。|  
|*Time*|此資料行的值代表時間測量單位。|  
  
 在「分析管理物件」(AMO) 物件模型中對應至 `Content` 允許值的列舉是 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>。  
  
## <a name="see-also"></a>另請參閱  
 [ClassifiedColumns 元素&#40;ASSL&#41;](../collections/columns-element-assl.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
