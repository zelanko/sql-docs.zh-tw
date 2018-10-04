---
title: ExecuteResponse 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ExecuteResponse Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#ExecuteResponse
- http://schemas.microsoft.com/analysisservices/2003/engine#ExecuteResponse
- microsoft.xml.analysis.executeresponse
helpviewer_keywords:
- ExecuteResponse element
ms.assetid: 6edb1b82-da4c-4cd9-9385-bea04032f0eb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 002da257a4d1137b0e52743eec99f1b0aced56c0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48047579"
---
# <a name="executeresponse-element-xmla"></a>ExecuteResponse 元素 (XMLA)
  包含的執行個體所傳回的資訊[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]回應[Execute](xml-elements-methods-execute.md)方法呼叫。  
  
 **命名空間**urn: schemas-microsoft-microsoft-schemas-microsoft-com:-分析  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ExecuteResponse>  
   <return>  
</ExecuteResponse>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|None|  
|預設值|None|  
|基數|1-1：只能出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|None|  
|子元素|[傳回](xml-elements-properties/return-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 `ExecuteResponse` 元素是`Execute` 方法之 SOAP 回應本文內部的最上層元素。  
  
## <a name="see-also"></a>另請參閱  
 [DiscoverResponse 元素&#40;XMLA&#41;](xml-elements-objects-discoverresponse.md)   
 [物件&#40;XMLA&#41;](xml-elements-objects.md)  
  
  
