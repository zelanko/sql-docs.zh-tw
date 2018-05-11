---
title: RootMemberIf 元素 (ASSL) |Microsoft 文件
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: cca19adce1c964272c87495af9ef0ed74a315ca7
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="rootmemberif-element-assl"></a>RootMemberIf 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*ParentIsBlankSelfOrMissing*|  
|基數|0-1：只能出現一次的選擇性元素|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 值**RootMemberIf**項目僅供父屬性 (換言之，值[使用量](../../../analysis-services/scripting/properties/usage-element-dimensionattribute-assl.md)元素**DimensionAttribute**父項目是設定為*父*) 決定父子式階層的根 （最上層） 成員。  
  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|Description|  
|-----------|-----------------|  
|*ParentIsBlankSelfOrMissing*|只有符合一或多個如所述條件的成員*ParentIsBlank*， *ParentIsSelf*，或*ParentIsMissing*會被視為根成員。|  
|*ParentIsBlank*|只有具有 null、 零或空字串索引鍵所代表的資料行成員[KeyColumns](../../../analysis-services/scripting/collections/keycolumns-element-assl.md)集合**DimensionAttribute**會被視為根成員。|  
|*ParentIsSelf*|只有本身是父系的成員會被視為根成員。|  
|*ParentIsMissing*|只有找不到父系的成員會被視為根成員。|  
  
 列舉型別對應至允許的值**RootMemberIf**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.RootIfValue>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
