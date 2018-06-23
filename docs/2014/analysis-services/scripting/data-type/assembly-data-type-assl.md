---
title: Assembly 資料類型 (ASSL) |Microsoft 文件
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
- Assembly Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- Assembly data type
ms.assetid: 0a381322-9509-4579-a754-c6cdd0a70cc9
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 3fd706974b0cb4a897a7ef75e147dcd35ac91481
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36132007"
---
# <a name="assembly-data-type-assl"></a>Assembly 資料類型 (ASSL)
  定義表示的抽象基本資料類型[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]組件或 COM 動態連結程式庫 (DLL) 相關聯[伺服器](../objects/server-element-assl.md)或[資料庫](../objects/database-element-assl.md)項目。  
  
> [!IMPORTANT]  
>  COM 組件可能會造成安全性風險。 由於這項風險和其他考量，COM 組件在 [!INCLUDE[ssASversion10](../../../includes/ssasversion10-md.md)]中已經被取代。 在未來的版本中，可能不再支援 COM 組件。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Assembly>  
   <Name>...</Name>  
   <ID>...</ID>  
   <Description>...</Description>  
   <CreatedTimestamp>...</CreatedTimestamp>  
   <LastSchemaUpdate>...</LastSchemaUpdate>  
   <ImpersonationInfo>...</ImpersonationInfo>  
   <Annotations>...</Annotations>  
</Assembly>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|描述|  
|--------------------|-----------------|  
|基底資料類型|無|  
|衍生資料類型|[ClrAssembly](assembly-data-type-assl.md)， [ComAssembly](comassembly-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[註解](../collections/annotations-element-assl.md)， [CreatedTimestamp](../properties/createdtimestamp-element-assl.md)，[描述](../properties/description-element-assl.md)，[識別碼](../properties/id-element-assl.md)， [ImpersonationInfo](../properties/impersonationinfo-element-assl.md)， [LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md)，[名稱](../properties/name-element-assl.md)|  
|衍生的元素|無|  
  
## <a name="remarks"></a>備註  
 `Assembly` 資料類型會當做 `ComAssembly` 元素 (代表與執行個體或資料庫相關聯的 COM 程式庫) 和 `ClrAssembly` 元素 (代表與執行個體或資料庫相關聯的 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 組件) 的基底資料類型。 如需組件的詳細資訊，請參閱[多維度模型組件管理](../../multidimensional-models/multidimensional-model-assemblies-management.md)。  
  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.Assembly>。  
  
## <a name="see-also"></a>另請參閱  
 [Server 元素&#40;ASSL&#41;](../objects/server-element-assl.md)   
 [Database 元素&#40;ASSL&#41;](../objects/database-element-assl.md)   
 [Analysis Services 指令碼語言 XML 資料類型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  