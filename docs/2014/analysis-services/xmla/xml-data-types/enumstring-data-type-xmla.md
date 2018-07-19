---
title: EnumString 資料類型 (XMLA) |Microsoft Docs
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
- EnumString Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- EnumString
- urn:schemas-microsoft-com:xml-analysis#EnumString
- http://schemas.microsoft.com/analysisservices/2003/engine#EnumString
helpviewer_keywords:
- EnumString data type
ms.assetid: 9214195e-4539-419b-95ec-b7aa75e033ab
caps.latest.revision: 29
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ea4f9057c05d7be5a5f8d8591d27460540a377fe
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37224022"
---
# <a name="enumstring-data-type-xmla"></a>EnumString 資料類型 (XMLA)
  定義代表給定列舉值之具名常數集合的衍生資料類型。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<EnumString>...</EnumString>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|描述|  
|--------------------|-----------------|  
|基底資料類型|`string`|  
|衍生資料類型|無|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|無|  
|衍生的元素|無|  
  
## <a name="remarks"></a>備註  
 XML for Analysis (XMLA) 會使用列舉，將字串值限制為可驗證設定集合。 `EnumString` 會使用標準的 XML `string` 資料類型。 每個具名常數的特定值都以列舉值定義指定。 列舉值定義加入至[DISCOVER_ENUMERATORS](../../schema-rowsets/xml/discover-enumerators-rowset.md)結構描述資料列，而且可以使用擷取[Discover](../xml-elements-methods-discover.md)方法搭配 DISCOVER_ENUMERATORS 要求類型。  
  
 下表描述的執行個體所支援的列舉值[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
|列舉值|描述|  
|----------------|-----------------|  
|ProviderType|支援的 ProviderType 資料行[DISCOVER_DATASOURCES](../../schema-rowsets/xml/discover-datasources-rowset.md)結構描述資料列集，可傳回的資料類型會決定[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]執行個體。<br /><br /> 這個列舉也支援 XMLA 屬性 `ProviderType`，而此屬性會決定 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體所支援的提供者類型。 此外，這個列舉還會用於 DISCOVER_DATASOURCES 結構描述資料列集中。<br /><br /> 如需詳細資訊`ProviderType`，請參閱 <<c2> [ 支援的 XMLA 屬性&#40;XMLA&#41;](../xml-elements-properties/propertylist-element-supported-xmla-properties.md)。</c2>|  
|AuthenticationMode|支援 DISCOVER_DATASOURCES 結構描述資料列集中的 AuthenticationMode 資料行，而此資料行會決定必須傳遞才能存取 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體的安全性認證。|  
|PropertyAccessType|支援的 PropertyAccessType 資料行[DISCOVER_PROPERTIES](../../schema-rowsets/xml/discover-properties-rowset.md)結構描述資料列集，可決定 XMLA 屬性可用的存取類型。|  
|StateSupport|支援 XMLA 屬性 `StateSupport`，而此屬性會決定 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體所支援的 Statefulness 層級。<br /><br /> 如需詳細資訊`StateSupport`，請參閱 <<c2> [ 支援的 XMLA 屬性&#40;XMLA&#41;](../xml-elements-properties/propertylist-element-supported-xmla-properties.md)。</c2>|  
|StateActionVerb|包含 SOAP 標頭中 XMLA 所支援的動詞清單，可用來開始、識別和結束工作階段。<br /><br /> 如需有關工作階段的詳細資訊，請參閱[管理連接和工作階段&#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)。|  
|ResultsetFormat|支援 XMLA 屬性`Format`，以決定傳回的資料型別[根](../xml-elements-properties/root-element-xmla.md)項目。<br /><br /> 如需詳細資訊`Format`，請參閱 <<c2> [ 支援的 XMLA 屬性&#40;XMLA&#41;](../xml-elements-properties/propertylist-element-supported-xmla-properties.md)。</c2>|  
|ResultsetAxisFormat|支援 XMLA 屬性 `AxisFormat`，而此屬性會決定在包含多維度資料之 `root` 元素中傳回的軸資訊格式。<br /><br /> 如需詳細資訊`AxisFormat`，請參閱 <<c2> [ 支援的 XMLA 屬性&#40;XMLA&#41;](../xml-elements-properties/propertylist-element-supported-xmla-properties.md)。</c2>|  
|ResultsetContents|支援 XMLA 屬性 `Content`，而此屬性會決定在 `root` 元素中傳回中繼資料或資料。<br /><br /> 如需詳細資訊`Content`，請參閱 <<c2> [ 支援的 XMLA 屬性&#40;XMLA&#41;](../xml-elements-properties/propertylist-element-supported-xmla-properties.md)。</c2>|  
|MDXSupportLevel|支援 XMLA 屬性 `MDXSupport`，而此屬性會指出 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體上可用的多維度運算式 (MDX) 支援層級。<br /><br /> 如需詳細資訊`MDXSupport`，請參閱 <<c2> [ 支援的 XMLA 屬性&#40;XMLA&#41;](../xml-elements-properties/propertylist-element-supported-xmla-properties.md)。</c2>|  
  
## <a name="see-also"></a>另請參閱  
 [XML 資料型別&#40;XMLA&#41;](xml-data-types-xmla.md)  
  
  
