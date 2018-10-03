---
title: ServerProperty 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ServerProperty Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- SERVERPROPERTY
helpviewer_keywords:
- ServerProperty element
ms.assetid: f152a1b5-0972-40d8-907f-f131c2a108bb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d84d9fc4bb78969265399d2a67207ea15e753f39
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48185768"
---
# <a name="serverproperty-element-assl"></a>ServerProperty 元素 (ASSL)
  定義相關聯的伺服器屬性[Server](server-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ServerProperties>  
   <ServerProperty>  
      <Name>...</Name>  
      <Value>...</Value>  
            <RequiresRestart>...</RequiresRestart>  
            <PendingValue>...</PendingValue>  
      <DefaultValue>...</DefaultValue>  
      <DisplayFlag>...</DisplayFlag>  
   </ServerProperty>  
</ServerProperties>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|None|  
|預設值|None|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[ServerProperties](../collections/serverproperties-element-assl.md)|  
|子元素|[DefaultValue](../properties/value-element-assl.md)， [DisplayFlag](../properties/displayflag-element-assl.md)，[名稱](../properties/name-element-assl.md)， [PendingValue](../properties/pendingvalue-element-assl.md)， [RequiresRestart](../properties/requiresrestart-element-assl.md)，[值](../properties/value-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 `ServerProperty`項目描述的資料和相關聯的執行個體之伺服器屬性的中繼資料[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。 與「Analysis Services 指令碼語言」(ASSL) 中其他集合所包含的元素不同之處在於，`ServerProperty` 元素會使用名稱/值組 (而非明確命名元素) 來描述伺服器屬性。 名稱/值組可提供彈性和擴充性。  
  
 在 「 分析管理物件 (AMO) 物件模型的對應元素是<xref:Microsoft.AnalysisServices.ServerProperty>。  
  
## <a name="see-also"></a>另請參閱  
 [伺服器項目&#40;ASSL&#41;](server-element-assl.md)   
 [物件&#40;ASSL&#41;](objects-assl.md)  
  
  
