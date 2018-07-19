---
title: LName 元素 (XMLA) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3c831c286de105f10762bbd8b926df7b4bb33623
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2018
ms.locfileid: "34575320"
---
# <a name="lname-element-xmla"></a>LName 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含父層級的唯一名稱的相關資訊[HierarchyInfo](../../../analysis-services/xmla/xml-elements-properties/hierarchyinfo-element-xmla.md)或[成員](../../../analysis-services/xmla/xml-elements-properties/member-element-xmla.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<HierarchyInfo> <!-- or Member -->  
   ...  
   <LName>...</LName>  
   ...  
</HierarchyInfo>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[HierarchyInfo](../../../analysis-services/xmla/xml-elements-properties/hierarchyinfo-element-xmla.md)，[成員](../../../analysis-services/xmla/xml-elements-properties/member-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 如**HierarchyInfo**元素，這個項目會包含提供階層層級的唯一名稱之屬性的名稱。 此值相當於針對 OLE DB for OLAP 規格中軸資料列集定義的 LEVEL_UNIQUE_NAME 屬性。  
  
 如**成員**項目，這個項目包含唯一的名稱中包含父系所代表之成員的階層層級**成員**項目。  
  
## <a name="see-also"></a>另請參閱
 [屬性&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
