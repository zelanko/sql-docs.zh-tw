---
title: Assembly 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Assembly Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ASSEMBLY
helpviewer_keywords:
- Assembly element [ASSL]
ms.assetid: 1910ccb0-7da0-4ee1-9548-ad6e0068d23d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e242f0fe6af48330207c78d8af848cb8b46a6707
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48198628"
---
# <a name="assembly-element-assl"></a>Assembly 元素 (ASSL)
  代表[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]組件或 COM 動態連結程式庫 (DLL) 與相關聯[伺服器](server-element-assl.md)項目或有[資料庫](database-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Assemblies>  
   <Assembly xsi:type="ClrAssembly">...</Assembly>  
   <!-- or -->  
   <Assembly xsi:type="ComAssembly">...</Assembly>  
</Assemblies>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|[ClrAssembly](../data-type/assembly-data-type-assl.md)， [ComAssembly](../data-type/comassembly-data-type-assl.md)|  
|預設值|None|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[組件](../collections/assemblies-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 在 「 分析管理物件 (AMO) 物件模型的對應元素是<xref:Microsoft.AnalysisServices.Assembly>。  
  
## <a name="see-also"></a>另請參閱  
 [伺服器項目&#40;ASSL&#41;](server-element-assl.md)   
 [資料庫項目&#40;ASSL&#41;](database-element-assl.md)   
 [物件&#40;ASSL&#41;](objects-assl.md)  
  
  
