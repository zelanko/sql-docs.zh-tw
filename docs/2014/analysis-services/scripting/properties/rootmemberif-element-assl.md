---
title: RootMemberIf 元素 (ASSL) |Microsoft 文件
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
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 5a923b08efc636d2635d60b00f85c42dc00a312e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36032396"
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
 值`RootMemberIf`項目僅供父屬性 (換言之的值[使用量](usage-element-dimensionattribute-assl.md)元素`DimensionAttribute`父項目設定為*父*) 來判斷根 （父子式階層最上層） 成員。  
  
 這個元素的值限制為下表所列的其中一個字串。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|*ParentIsBlankSelfOrMissing*|只有符合一或多個如所述條件的成員*ParentIsBlank*， *ParentIsSelf*，或*ParentIsMissing*會被視為根成員。|  
|*ParentIsBlank*|只有具有 null、 零或空字串索引鍵所代表的資料行成員[KeyColumns](../collections/columns-element-assl.md)集合`DimensionAttribute`會被視為根成員。|  
|*ParentIsSelf*|只有本身是父系的成員會被視為根成員。|  
|*ParentIsMissing*|只有找不到父系的成員會被視為根成員。|  
  
 在「分析管理物件」(AMO) 物件模型中對應至 `RootMemberIf` 允許值的列舉是 <xref:Microsoft.AnalysisServices.RootIfValue>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  