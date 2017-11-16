---
title: "取消命令 (XMLA) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- connections [XML for Analysis]
- associated connections [XML for Analysis]
- XML for Analysis, canceling
- associated sessions [XML for Analysis]
- canceling connections
- canceling commands
- canceling sessions
- SPID
- XMLA, canceling
- server process IDs [XML for Analysis]
- sessions [XML for Analysis]
ms.assetid: b59f8197-c33d-4e65-9022-848ccba540f5
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e74ce7bd5b03aa84b6c6580342504148a62a68bf
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="canceling-commands-xmla"></a>取消命令 (XMLA)
  視發出命令的使用者的系統管理權限[取消](../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md)命令在 XML for Analysis (XMLA) 可以取消工作階段，工作階段、 連接、 伺服器處理序或相關聯的工作階段上的命令或連接。  
  
## <a name="canceling-commands"></a>取消命令  
 使用者可以取消目前執行的命令在目前的明確工作階段的內容傳送**取消**命令沒有指定屬性。  
  
> [!NOTE]  
>  使用者無法取消在明確的工作階段中執行的命令。  
  
### <a name="canceling-batch-commands"></a>取消批次命令  
 如果使用者取消**批次**命令，則所有剩餘的命令中尚未執行**批次**命令已取消。 如果**批次**命令是交易式、 之前所執行的任何命令**取消**執行命令會回復。  
  
## <a name="canceling-sessions"></a>取消工作階段  
 將工作階段識別碼指定為明確工作階段中的[SessionID](../../analysis-services/xmla/xml-elements-properties/sessionid-element-xmla.md)屬性**取消**命令時，資料庫管理員或伺服器管理員可以取消工作階段，包括目前執行中命令。 資料庫管理員只能取消他或她擁有管理權限的資料庫之工作階段。  
  
 資料庫管理員可以擷取 DISCOVER_SESSIONS 結構描述資料列集，以擷取指定資料庫的使用中工作階段。 若要擷取 DISCOVER_SESSIONS 結構描述資料列集，資料庫管理員可以使用 XMLA**探索**方法，並指定適當的資料庫識別碼，為 SESSION_CURRENT_DATABASE 限制資料行中[限制](../../analysis-services/xmla/xml-elements-properties/restrictions-element-xmla.md)屬性**探索**方法。  
  
## <a name="canceling-connections"></a>取消連接  
 藉由指定中的連線識別碼[ConnectionID](../../analysis-services/xmla/xml-elements-properties/connectionid-element-xmla.md)屬性**取消**命令時，伺服器管理員可以取消所有指定的連接，包括所有相關聯的工作階段執行命令，並取消連接。  
  
> [!NOTE]  
>  如果執行個體[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]無法找出並取消與連接相關聯的工作階段，例如當資料幫浦開啟多個工作階段，同時提供 HTTP 連線時，執行個體無法取消連接。 如果在執行期間發生此情況下**取消**命令時，發生錯誤。  
  
 伺服器系統管理員可以擷取作用中連線的[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]使用 XMLA DISCOVER_CONNECTIONS 結構描述資料列集的執行個體**探索**方法。  
  
## <a name="canceling-server-processes"></a>取消伺服器處理序  
 藉由在指定的伺服器處理序識別碼 (SPID) [SPID](../../analysis-services/xmla/xml-elements-properties/spid-element-xmla.md)屬性**取消**命令時，伺服器管理員可以取消與指定 SPID 相關聯的命令。  
  
## <a name="canceling-associated-sessions-and-connections"></a>取消關聯的工作階段和連接。  
 您可以設定[CancelAssociated](../../analysis-services/xmla/xml-elements-properties/cancelassociated-element-xmla.md)屬性設定為 true，若要取消連接、 工作階段和連接、 工作階段或在指定的 SPID 相關聯的命令**取消**命令。  
  
## <a name="see-also"></a>另請參閱  
 [探索方法 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-methods-discover.md)   
 [使用 Analysis Services 中的 XMLA 進行開發](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  

