---
title: BeginTransaction 元素 (XMLA) |Microsoft Docs
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
- BeginTransaction Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#BeginTransaction
- microsoft.xml.analysis.begintransaction
- http://schemas.microsoft.com/analysisservices/2003/engine#BeginTransaction
helpviewer_keywords:
- BeginTransaction command
ms.assetid: fca122fc-b57c-4ba6-849b-ca8c93cf64e9
caps.latest.revision: 14
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1685c1c61c248cf37672cab17ccf3144e7d5e7ec
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37253040"
---
# <a name="begintransaction-element-xmla"></a>BeginTransaction 元素 (XMLA)
  執行個體的目前工作階段上開始交易[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Command>  
   <BeginTransaction />  
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
 `BeginTransaction` 命令會在目前的工作階段上開始使用中交易。 如果使用中交易已經存在，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體就會遞增目前工作階段之交易的參考計數。 如果沒有，此執行個體就會開始新的交易並將目前工作階段的參考計數設定為 1。 如果您使用 `BeginTransaction` 命令明確指定了使用中交易，所有後續命令都會在明確指定的交易內部執行。  
  
 當目前的工作階段結束而且交易的參考計數大於零時，系統就會回復所有使用中交易。  
  
 如果目前的工作階段上沒有任何明確指定的使用中交易，在目前工作階段上發出的每個命令都會在隱含定義的交易內部執行。 如果命令成功，就會認可隱含交易，但是如果命令失敗，則會回復隱含交易。  
  
## <a name="see-also"></a>另請參閱  
 [Cancel 元素&#40;XMLA&#41;](cancel-element-xmla.md)   
 [CommitTransaction 元素&#40;XMLA&#41;](committransaction-element-xmla.md)   
 [RollbackTransaction 元素&#40;XMLA&#41;](rollbacktransaction-element-xmla.md)   
 [命令&#40;XMLA&#41;](xml-elements-commands.md)  
  
  
