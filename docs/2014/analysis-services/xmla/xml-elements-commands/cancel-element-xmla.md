---
title: Cancel 元素 (XMLA) |Microsoft Docs
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
- Cancel Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.cancel
- http://schemas.microsoft.com/analysisservices/2003/engine#Cancel
- urn:schemas-microsoft-com:xml-analysis#Cancel
helpviewer_keywords:
- Cancel command
ms.assetid: de4062c1-7434-44dc-9f01-29fcf78963bd
caps.latest.revision: 15
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fb71b55e514a2e058d50cd1c923a3e0b794ac8f9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37173269"
---
# <a name="cancel-element-xmla"></a>Cancel 元素 (XMLA)
  取消目前執行中命令[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]執行個體。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Command>  
   <Cancel>  
      <ConnectionID>...</ConnectionID>  
      <SessionID>...</SessionID>  
      <SPID>...</SPID>  
      <CancelAssociated>...</CancelAssociated>  
   </Cancel>  
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
|子元素|[CancelAssociated](../xml-elements-properties/cancelassociated-element-xmla.md)， [ConnectionID](../xml-elements-properties/id-element-xmla.md)， [SessionID](../xml-elements-properties/sessionid-element-xmla.md)， [SPID](../xml-elements-properties/spid-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 `Cancel` 命令會取消工作階段內容中的目前執行中命令。 如果用戶端應用程式尚未要求工作階段，您就無法取消命令。  
  
 如果您在 `Cancel` 命令執行期間執行了 `Batch` 命令，就會取消整個 `Batch` 命令。 如果 `Batch` 命令是交易式，則會回復 `Batch` 命令所包含的所有命令。 如果 `Batch` 命令並非交易式，只會回復 `Batch` 命令所包含而且在執行 `Cancel` 命令時處於執行中狀態的這些命令。 但是，系統不會回復非交易式 `Batch` 命令中已經執行的命令。  
  
 一般而言，`Cancel` 命令會用來取消目前使用中工作階段上的執行中命令。 在該情況中，您不需要針對 `Cancel` 命令指定任何子元素。 此外，管理員也可以使用 `Cancel` 命令來取消目前使用中工作階段以外之連接或工作階段上的執行中命令。 針對給定資料庫擁有管理權限之角色的成員可以取消適用於該資料庫之連接和工作階段的命令，而伺服器管理員可以取消給定 Analysis Services 執行個體之連接和工作階段的命令。  
  
 若要擷取 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體之目前連接和工作階段的相關資訊，您可以執行 `Discover` 方法來分別要求 DISCOVER_CONNECTIONS 和 DISCOVER_SESSIONS 結構描述資料列集。 針對給定資料庫擁有管理權限之角色的成員可以在 DISCOVER_SESSIONS 結構描述資料列集的 SESSION_CURRENT_DATABASE 限制資料行中指定該資料庫，以便僅針對給定資料庫傳回工作階段。 如需詳細資訊`Discover`方法，請參閱 < [Discover 方法&#40;XMLA&#41;](../xml-elements-methods-discover.md)。  
  
## <a name="see-also"></a>另請參閱  
 [批次項目&#40;XMLA&#41;](batch-element-xmla.md)   
 [命令&#40;XMLA&#41;](xml-elements-commands.md)  
  
  
