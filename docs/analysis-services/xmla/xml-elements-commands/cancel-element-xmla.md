---
title: Cancel 元素 (XMLA) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7bc3cd9330261d0ec4e13a715612d73e6ecb44eb
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2018
ms.locfileid: "34574870"
---
# <a name="cancel-element-xmla"></a>Cancel 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  取消目前執行中命令的 Analysis Services 執行個體。  
  
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
|父元素|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|子元素|[CancelAssociated](../../../analysis-services/xmla/xml-elements-properties/cancelassociated-element-xmla.md)， [ConnectionID](../../../analysis-services/xmla/xml-elements-properties/connectionid-element-xmla.md)， [SessionID](../../../analysis-services/xmla/xml-elements-properties/sessionid-element-xmla.md)， [SPID](../../../analysis-services/xmla/xml-elements-properties/spid-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 **取消**命令取消目前正在執行的工作階段內容中的命令。 如果用戶端應用程式尚未要求工作階段，您就無法取消命令。  
  
 如果**取消**命令執行期間執行**批次**命令時，整個**批次**取消命令為止。 如果**批次**命令是交易式，命令所包含的所有**批次**命令都會回復。 如果**批次**命令並非交易式，只有在所包含的命令**批次**當時所執行的命令**取消**命令是回復。 在非交易式命令**批次**已經執行的命令不會被回復。  
  
 一般而言，**取消**命令用來取消目前作用中工作階段上執行的命令。 在此情況下，沒有任何子項目**取消**必須指定命令。 **取消**命令也可由系統管理員取消連接或目前使用中工作階段以外的工作階段上執行的命令。 針對給定資料庫擁有管理權限之角色的成員可以取消適用於該資料庫之連接和工作階段的命令，而伺服器管理員可以取消給定 Analysis Services 執行個體之連接和工作階段的命令。  
  
 若要擷取目前的連接和工作階段的相關資訊[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]執行個體，**探索**方法來分別要求 DISCOVER_CONNECTIONS 和 DISCOVER_SESSIONS 結構描述資料列上執行。 針對給定資料庫擁有管理權限之角色的成員可以在 DISCOVER_SESSIONS 結構描述資料列集的 SESSION_CURRENT_DATABASE 限制資料行中指定該資料庫，以便僅針對給定資料庫傳回工作階段。 如需有關**探索**方法，請參閱[探索方法&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-methods-discover.md)。  
  
## <a name="see-also"></a>另請參閱
 [批次項目&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)   
 [命令&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
