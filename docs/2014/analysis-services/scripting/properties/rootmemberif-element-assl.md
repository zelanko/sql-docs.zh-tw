---
title: RootMemberIf 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- RootMemberIf Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- RootMemberIf
helpviewer_keywords:
- RootMemberIf element
ms.assetid: b695e271-c748-4abc-a09f-acb1014f768f
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a7ac45d2111b8d3631160ce78f131f98d53230e7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37280294"
---
# <a name="rootmemberif-element-assl"></a>RootMemberIf 元素 (ASSL)
  決定如何識別父屬性的根成員。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<DimensionAttribute>  
   ...  
   <RootMemberIf>...</RootMemberIf>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*ParentIsBlankSelfOrMissing*|  
|基數|0-1：只能出現一次的選擇性元素|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 值`RootMemberIf`項目僅供父屬性 (亦即的值[使用量](usage-element-dimensionattribute-assl.md)項目`DimensionAttribute`父項目設定為*父*) 來判斷根 （父子式階層最上層） 成員。  
  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|描述|  
|-----------|-----------------|  
|*ParentIsBlankSelfOrMissing*|只有符合下列其中一或多個如所述條件的成員才*ParentIsBlank*， *ParentIsSelf*，或*ParentIsMissing*會被視為根成員。|  
|*ParentIsBlank*|只有具有 null、 零或空字串索引鍵所代表的資料行的成員，才[KeyColumns](../collections/columns-element-assl.md)的集合`DimensionAttribute`會被視為根成員。|  
|*ParentIsSelf*|只有本身是父系的成員會被視為根成員。|  
|*ParentIsMissing*|只有找不到父系的成員會被視為根成員。|  
  
 在「分析管理物件」(AMO) 物件模型中對應至 `RootMemberIf` 允許值的列舉是 <xref:Microsoft.AnalysisServices.RootIfValue>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
