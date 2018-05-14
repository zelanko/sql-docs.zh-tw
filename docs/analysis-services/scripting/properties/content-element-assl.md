---
title: 內容元素 (ASSL) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ee3c1babd828463e8654280c421d616535aca88e
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="content-element-assl"></a>Content 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  說明內容中的資料行的[MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ScalarMiningStructureColumn>  
   ...  
   <Content>...</Content>  
   ...  
</ScalarMiningStructureColumn>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|無|  
|基數|1-1：只能出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個列舉會描述採礦結構資料行所代表的內容類型，而且可由採礦演算法提供者視需要擴充。 如需內容類型的詳細資訊，請參閱[內容類型 &#40;資料採礦&#41;](../../../analysis-services/data-mining/content-types-data-mining.md)。  
  
 下表所列的值通常受到所有採礦演算法提供者支援。  
  
|Value|Description|  
|-----------|-----------------|  
|*離散*|此資料行包含離散值。|  
|*連續*|此資料行的值會定義一組連續的數值資料。|  
|*離散化*|此資料行的值代表衍生自連續資料行之值的群組 (或值區)。|  
|*排序*|此資料行的值會定義已排序集合。|  
|*循環*|此資料行的值會定義循環的已排序集合。|  
|*機率*|資料行的值指定資料行中包含機率[ClassifiedColumns](../../../analysis-services/scripting/collections/classifiedcolumns-element-assl.md)父元素之**ScalarMiningStructureColumn**。|  
|*Variance*|資料行的值指定在包含的資料行的變異數**ClassifiedColumns**父元素之**ScalarMiningStructureColumn**。|  
|*標準差*|資料行的值指定資料行中所包含的標準差**ClassifiedColumns**父元素之**ScalarMiningStructureColumn**。|  
|*ProbabilityVariance*|資料行的值指定機率變異數中所包含的資料行**ClassifiedColumns**父元素之**ScalarMiningStructureColumn**。|  
|*ProbabilityStdDev*|資料行的值指定機率標準差資料行中包含**ClassifiedColumns**父元素之**ScalarMiningStructureColumn**。|  
|*支援*|資料行的值會指定資料行中所包含的支援資訊**ClassifiedColumns**父元素之**ScalarMiningStructureColumn**。<br /><br /> 注意： 此資料行是依現狀標準的一部分的協力廠商採礦演算法提供者。 Microsoft 提供的演算法請勿使用此資料行。|  
|*索引鍵*|此資料行為索引鍵資料行。<br /><br /> 注意： 此內容類型是僅適用於索引鍵資料行，其中**IsKey**元素設定為**True**。|  
  
 除了這些標準值時，採礦演算法提供者隨附[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]支援下表中的值。  
  
|Value|Description|  
|-----------|-----------------|  
|*索引鍵的順序*|此資料行為索引鍵資料行，而且資料行的值代表事件序列。<br /><br /> 注意： 此內容類型是僅適用於索引鍵資料行，其中**IsKey**元素設定為**True**。|  
|*Key Time*|此資料行為索引鍵資料行，而且資料行的值代表時間測量單位。<br /><br /> 注意： 此內容類型是僅適用於索引鍵資料行，其中**IsKey**元素設定為**True**。|  
|*順序*|此資料行的值代表事件序列。|  
|*Time*|此資料行的值代表時間測量單位。|  
  
 列舉型別對應至允許的值**內容**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>。  
  
## <a name="see-also"></a>另請參閱  
 [ClassifiedColumns 元素&#40;ASSL&#41;](../../../analysis-services/scripting/collections/classifiedcolumns-element-assl.md)   
 [屬性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
