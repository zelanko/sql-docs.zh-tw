---
title: 鎖定元素 (XMLA) |Microsoft Docs
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
- Lock Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Lock
- microsoft.xml.analysis.lock
- http://schemas.microsoft.com/analysisservices/2003/engine#Lock
helpviewer_keywords:
- Lock command
ms.assetid: a819e805-4793-43bb-8af3-16a19f8bdab3
caps.latest.revision: 14
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 44225f211ac013edd82de08c9ca82f22cb349f96
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37209868"
---
# <a name="lock-element-xmla"></a>Lock 元素 (XMLA)
  鎖定指定的物件上[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]執行個體。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Command>  
   <Lock>  
      <ID>...</ID>  
      <Object>...</Object>  
      <Mode>...</Mode>  
   </Lock>  
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
|子元素|[ID](../xml-elements-properties/id-element-xmla.md)，[模式](../xml-elements-properties/mode-element-xmla.md)，[物件](../xml-elements-properties/object-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 `Lock` 命令會在目前使用中交易的內容中鎖定某個物件，以便共用或獨佔使用。 只有資料庫管理員或伺服器管理員可以明確發出 `Lock` 命令。 鎖定物件會防止認可交易，直到移除鎖定為止。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 支援兩種鎖定類型：共用鎖定和獨佔鎖定。 如需所支援的鎖定類型[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]，請參閱 <<c2> [ 模式項目&#40;XMLA&#41;](../xml-elements-properties/mode-element-xmla.md)。</c2>  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 僅允許鎖定資料庫。 `Object` 元素必須包含 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 資料庫的物件參考。 如果您沒有指定 `Object` 元素或者 `Object` 元素參考資料庫以外的物件，就會發生錯誤。  
  
 其他命令會隱含地針對 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 資料庫發出 `Lock` 命令。 任何從資料庫讀取資料或中繼資料的作業 (例如，執行 `Discover` 命令的任何 `Execute` 方法或 `Statement` 方法) 都會隱含地針對資料庫發出共用鎖定。 任何將資料或中繼資料變更認可至 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 資料庫上之物件的交易 (例如，執行 `Execute` 命令的 `Alter` 方法) 都會隱含地針對資料庫發出獨佔共用鎖定。  
  
 所有鎖定都會保存在目前交易的內容中。 當目前的交易經過認可或回復時，就會自動釋放在交易內部定義的所有鎖定。  
  
## <a name="see-also"></a>另請參閱  
 [Unlock 元素&#40;XMLA&#41;](lock-element-xmla.md)   
 [命令&#40;XMLA&#41;](xml-elements-commands.md)  
  
  
