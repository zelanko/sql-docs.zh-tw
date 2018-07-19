---
title: Security 元素 (XMLA) |Microsoft Docs
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
- Security Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.security
- urn:schemas-microsoft-com:xml-analysis#Security
- http://schemas.microsoft.com/analysisservices/2003/engine#Security
helpviewer_keywords:
- Security element
ms.assetid: 0b601f69-d16d-4d10-9361-b8afaa6ed357
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 138b93043cbfeba51472dfa61816cf9023a3f2c6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37155019"
---
# <a name="security-element-xmla"></a>Security 元素 (XMLA)
  指定如何備份或還原安全性定義，例如角色和權限，期間[備份](../xml-elements-commands/backup-element-xmla.md)或是[還原](../xml-elements-commands/restore-element-xmla.md)命令。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Backup> <!-- or Restore -->  
   ...  
   <Security>...</Security>  
   ...  
</Backup>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*SkipMembership*|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[備份](../xml-elements-commands/backup-element-xmla.md)，[還原](../xml-elements-commands/restore-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 `Security`元素會決定上定義的安全性定義，例如角色和權限，是否[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]資料庫備份或還原期間，分別`Backup`或`Restore`命令。 此外，這個元素也會決定定義為安全性定義成員的 Windows 使用者帳戶和群組是否會包含成為 `Backup` 或 `Restore` 命令的一部分。  
  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|描述|  
|-----------|-----------------|  
|*SkipMembership*|在進行 `Backup` 或 `Restore` 命令期間，包含安全性定義，但是排除成員資格資訊。|  
|*CopyAll*|在進行 `Backup` 或 `Restore` 命令期間，包含安全性定義和成員資格資訊。|  
|*IgnoreSecurity*|在進行 `Backup` 或 `Restore` 命令期間，排除安全性定義。|  
  
## <a name="see-also"></a>另請參閱  
 [SynchronizeSecurity 元素&#40;XMLA&#41;](security-element-xmla.md)   
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
