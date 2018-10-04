---
title: Version 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Version Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Version
helpviewer_keywords:
- Version element
ms.assetid: fb26fe5d-de40-443b-a8bc-031c950552e6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2e8c8cde757b0de5fb4076c395ac915650a12d4a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48091308"
---
# <a name="version-element-assl"></a>Version 元素 (ASSL)
  包含的執行個體的唯讀版本號碼[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]由[Server](../objects/server-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Server>  
      ...  
      <Version>...</Version>  
   ...  
</Server>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|None|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Server](../objects/server-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 `Version` 元素會描述已安裝哪一個 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 版本。  
  
 對應至父系的元素`Version`在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.Server>。  
  
## <a name="see-also"></a>另請參閱  
 [Edition 元素&#40;ASSL&#41;](edition-element-assl.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
