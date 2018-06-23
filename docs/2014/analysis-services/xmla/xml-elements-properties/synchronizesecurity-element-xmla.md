---
title: SynchronizeSecurity 元素 (XMLA) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- SynchronizeSecurity Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.synchronizesecurity
- http://schemas.microsoft.com/analysisservices/2003/engine#SynchronizeSecurity
- urn:schemas-microsoft-com:xml-analysis#SynchronizeSecurity
helpviewer_keywords:
- SynchronizeSecurity element
ms.assetid: d37dbb95-f4a4-44ac-8eb9-f661d5bb5018
caps.latest.revision: 12
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: cc50a9acd38fe394e5ac6b457f72e76669b5ec64
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36030131"
---
# <a name="synchronizesecurity-element-xmla"></a>SynchronizeSecurity 元素 (XMLA)
  指定期間如何同步處理安全性定義，例如角色和權限， [Synchronize](../xml-elements-commands/synchronize-element-xmla.md)命令。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Synchronize>  
   ...  
   <SynchronizeSecurity>...</SynchronizeSecurity>  
   ...  
</Synchronize>  
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
|父元素|[同步處理](../xml-elements-commands/synchronize-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 `Security`元素會決定是否在上定義的安全性定義，例如角色和權限， [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]資料庫會同步處理期間`Synchronize`命令。 此外，這個元素也會決定定義為安全性定義成員的 Windows 使用者帳戶和群組是否會包含成為 `Synchronize` 命令的一部分。  
  
 這個元素的值限制為下表所列的其中一個字串。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|*SkipMembership*|在進行 `Synchronize` 命令期間，包含安全性定義，但是排除成員資格資訊。|  
|*CopyAll*|在進行 `Synchronize` 命令期間，包含安全性定義和成員資格資訊。|  
|*IgnoreSecurity*|在進行 `Synchronize` 命令期間，排除安全性定義。|  
  
## <a name="see-also"></a>另請參閱  
 [安全性項目&#40;XMLA&#41;](security-element-xmla.md)   
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  