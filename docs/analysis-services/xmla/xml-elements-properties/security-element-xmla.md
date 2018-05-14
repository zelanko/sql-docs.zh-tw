---
title: Security 元素 (XMLA) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 14cbfaf2e50a2eb77b3918317113823a342857cc
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="security-element-xmla"></a>Security 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
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
|預設值|*skipMembership*|  
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
|*skipMembership*|納入安全性定義，但是排除成員資格資訊期間**備份**或**還原**命令。|  
|*CopyAll*|包含安全性定義和成員資格資訊期間**備份**或**還原**命令。|  
|*IgnoreSecurity*|期間，排除安全性定義**備份**或**還原**命令。|  
  
## <a name="see-also"></a>另請參閱  
 [SynchronizeSecurity 元素&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/synchronizesecurity-element-xmla.md)   
 [屬性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
