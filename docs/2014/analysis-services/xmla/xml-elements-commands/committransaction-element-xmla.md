---
title: CommitTransaction 元素 (XMLA) |Microsoft 文件
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
- CommitTransaction Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#CommitTransaction
- urn:schemas-microsoft-com:xml-analysis#CommitTransaction
- microsoft.xml.analysis.committransaction
helpviewer_keywords:
- CommitTransaction command
ms.assetid: 1cd814dc-a0be-4305-b44d-faf15e843f7d
caps.latest.revision: 14
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 85db6f53386023acb32a9e853ad1d69f92f6860c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36031296"
---
# <a name="committransaction-element-xmla"></a>CommitTransaction 元素 (XMLA)
  目前工作階段上認可交易[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]執行個體。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Command>  
   <CommitTransaction />  
</Command>  
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
|父元素|[Command](../xml-elements-properties/command-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 `CommitTransaction` 命令會在目前的工作階段上認可使用 `BeginTransaction` 元素明確定義的使用中交易。 如果使用中交易尚未存在，就會發生錯誤。 如果使用中交易已經存在，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體就會遞減目前工作階段之交易的參考計數。 如果明確定義之使用中交易的參考計數到達零，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體就會認可交易。  
  
## <a name="see-also"></a>另請參閱  
 [BeginTransaction 元素&#40;XMLA&#41;](begintransaction-element-xmla.md)   
 [Cancel 元素&#40;XMLA&#41;](cancel-element-xmla.md)   
 [RollbackTransaction 元素&#40;XMLA&#41;](rollbacktransaction-element-xmla.md)   
 [命令&#40;XMLA&#41;](xml-elements-commands.md)  
  
  