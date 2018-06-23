---
title: ServerProperty 元素 (ASSL) |Microsoft 文件
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
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 6cb62681b0c25c83d54076a67a37addc764102da
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36029895"
---
# <a name="serverproperty-element-assl"></a>ServerProperty 元素 (ASSL)
  定義相關聯的伺服器屬性[伺服器](server-element-assl.md)項目。  
  
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
|資料類型和長度|無|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[ServerProperties](../collections/serverproperties-element-assl.md)|  
|子元素|[DefaultValue](../properties/value-element-assl.md)， [DisplayFlag](../properties/displayflag-element-assl.md)，[名稱](../properties/name-element-assl.md)， [PendingValue](../properties/pendingvalue-element-assl.md)， [RequiresRestart](../properties/requiresrestart-element-assl.md)，[值](../properties/value-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 `ServerProperty`元素描述的資料和中繼資料的執行個體相關聯之伺服器屬性[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。 與「Analysis Services 指令碼語言」(ASSL) 中其他集合所包含的元素不同之處在於，`ServerProperty` 元素會使用名稱/值組 (而非明確命名元素) 來描述伺服器屬性。 名稱/值組可提供彈性和擴充性。  
  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.ServerProperty>。  
  
## <a name="see-also"></a>另請參閱  
 [Server 元素&#40;ASSL&#41;](server-element-assl.md)   
 [物件&#40;ASSL&#41;](objects-assl.md)  
  
  