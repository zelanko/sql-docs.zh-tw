---
title: "SynchronizeSecurity 元素 (XMLA) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- SynchronizeSecurity Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.synchronizesecurity
- http://schemas.microsoft.com/analysisservices/2003/engine#SynchronizeSecurity
- urn:schemas-microsoft-com:xml-analysis#SynchronizeSecurity
helpviewer_keywords:
- SynchronizeSecurity element
ms.assetid: d37dbb95-f4a4-44ac-8eb9-f661d5bb5018
caps.latest.revision: 12
author: jeannt
ms.author: jeannt
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 94f58bf16e0127b1686e83a0e81ba754c3cf0066
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="synchronizesecurity-element-xmla"></a>SynchronizeSecurity 元素 (XMLA)
  指定期間如何同步處理安全性定義，例如角色和權限， [Synchronize](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)命令。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Synchronize>  
   ...  
   <SynchronizeSecurity>...</SynchronizeSecurity>  
   ...  
</Synchronize>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*SkipMembership*|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[同步處理](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 **安全性**元素會決定是否在上定義的安全性定義，例如角色和權限， [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]資料庫會同步處理期間**同步處理**命令。 這個項目也會決定的 Windows 使用者帳戶和群組定義為安全性定義成員會包含在**Synchronize**命令。  
  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|Description|  
|-----------|-----------------|  
|*SkipMembership*|納入安全性定義，但是排除成員資格資訊期間**Synchronize**命令。|  
|*CopyAll*|包含安全性定義和成員資格資訊期間**Synchronize**命令。|  
|*IgnoreSecurity*|期間，排除安全性定義**Synchronize**命令。|  
  
## <a name="see-also"></a>另請參閱  
 [安全性項目 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/security-element-xmla.md)   
 [屬性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

