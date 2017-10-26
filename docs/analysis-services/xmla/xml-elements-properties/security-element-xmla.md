---
title: "Security 元素 (XMLA) |Microsoft 文件"
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
- Security Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.security
- urn:schemas-microsoft-com:xml-analysis#Security
- http://schemas.microsoft.com/analysisservices/2003/engine#Security
helpviewer_keywords:
- Security element
ms.assetid: 0b601f69-d16d-4d10-9361-b8afaa6ed357
caps.latest.revision: 12
author: jeannt
ms.author: jeannt
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: cd1a4c292c1ac722fd91836b364724a0f59f8168
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="security-element-xmla"></a>Security 元素 (XMLA)
  指定如何備份或還原安全性定義，例如角色和權限，期間[備份](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)或[還原](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)命令。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Backup> <!-- or Restore -->  
   ...  
   <Security>...</Security>  
   ...  
</Backup>  
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
|父元素|[備份](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)，[還原](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 **安全性**元素會決定是否在上定義的安全性定義，例如角色和權限， [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]資料庫備份或還原期間，分別**備份**或**還原**命令。 這個項目也會決定的 Windows 使用者帳戶和群組定義為安全性定義成員會包含在**備份**或**還原**命令。  
  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|Description|  
|-----------|-----------------|  
|*SkipMembership*|納入安全性定義，但是排除成員資格資訊期間**備份**或**還原**命令。|  
|*CopyAll*|包含安全性定義和成員資格資訊期間**備份**或**還原**命令。|  
|*IgnoreSecurity*|期間，排除安全性定義**備份**或**還原**命令。|  
  
## <a name="see-also"></a>另請參閱  
 [SynchronizeSecurity 元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/synchronizesecurity-element-xmla.md)   
 [屬性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

