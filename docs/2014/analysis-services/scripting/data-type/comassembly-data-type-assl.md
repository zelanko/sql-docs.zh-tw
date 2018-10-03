---
title: ComAssembly 資料類型 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ComAssembly Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ComAssembly
helpviewer_keywords:
- ComAssembly data type
ms.assetid: 23c0f4b3-b6ac-4ec8-9254-74d2f84f5244
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9cf05a673de90310563cdc5264f61e2da0952450
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48133448"
---
# <a name="comassembly-data-type-assl"></a>ComAssembly 資料類型 (ASSL)
  定義代表與相關聯之 COM 程式庫的衍生的資料類型[伺服器](../objects/server-element-assl.md)或是[資料庫](../objects/database-element-assl.md)項目。  
  
> [!IMPORTANT]  
>  COM 組件可能會造成安全性風險。 由於這項風險和其他考量，COM 組件在 [!INCLUDE[ssASversion10](../../../includes/ssasversion10-md.md)]中已經被取代。 在未來的版本中，可能不再支援 COM 組件。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ComAssembly>  
      <!-- The following elements extend Assembly -->  
   <Source>...</Source>  
</ComAssembly>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|描述|  
|--------------------|-----------------|  
|基底資料類型|[組件](../objects/assembly-element-assl.md)|  
|衍生資料類型|None|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|None|  
|子元素|[Source](../properties/source-element-comassembly-assl.md)|  
|衍生的元素|請參閱[組件](../objects/assembly-element-assl.md)([組件](../collections/assemblies-element-assl.md)集合[資料庫](../objects/database-element-assl.md)或是[Server](../objects/server-element-assl.md))|  
  
## <a name="remarks"></a>備註  
 `ComAssembly`項目包含的參考 （完整的檔案名稱或程式設計識別碼） 的執行個體相關聯之 COM 程式庫[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]或與特定資料庫執行個體上的[!INCLUDE[ssAS](../../../includes/ssas-md.md)].  
  
 在 「 分析管理物件 (AMO) 物件模型的對應元素是<xref:Microsoft.AnalysisServices.ComAssembly>。  
  
## <a name="see-also"></a>另請參閱  
 [ClrAssembly 資料類型&#40;ASSL&#41;](assembly-data-type-assl.md)   
 [Analysis Services 指令碼語言 XML 資料類型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
