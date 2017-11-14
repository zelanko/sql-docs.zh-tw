---
title: "Cancel 元素 (XMLA) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Cancel Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.cancel
- http://schemas.microsoft.com/analysisservices/2003/engine#Cancel
- urn:schemas-microsoft-com:xml-analysis#Cancel
helpviewer_keywords:
- Cancel command
ms.assetid: de4062c1-7434-44dc-9f01-29fcf78963bd
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a12372d43b20395e878e305b036fe5a63f399d2b
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="cancel-element-xmla"></a>Cancel 元素 (XMLA)
  取消目前正在執行的命令[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]執行個體。  
  
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
  
|特性|說明|  
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
  
 若要擷取目前的連接和工作階段的相關資訊[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]執行個體，**探索**方法來分別要求 DISCOVER_CONNECTIONS 和 DISCOVER_SESSIONS 結構描述資料列上執行。 針對給定資料庫擁有管理權限之角色的成員可以在 DISCOVER_SESSIONS 結構描述資料列集的 SESSION_CURRENT_DATABASE 限制資料行中指定該資料庫，以便僅針對給定資料庫傳回工作階段。 如需有關**探索**方法，請參閱[探索方法 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-methods-discover.md).  
  
## <a name="see-also"></a>另請參閱  
 [批次元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)   
 [命令 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  

