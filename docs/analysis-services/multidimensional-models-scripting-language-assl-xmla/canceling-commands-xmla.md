---
title: 取消命令 (XMLA) |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 313708ad1575c7b9922ac796791d0d623c51b54b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63182950"
---
# <a name="canceling-commands-xmla"></a>取消命令 (XMLA)
  視發出命令之使用者的系統管理權限而定[取消](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/cancel-element-xmla)命令在 XML for Analysis (XMLA) 可以取消工作階段、 工作階段、 連接、 伺服器處理序或相關聯的工作階段上的命令或連接。  
  
## <a name="canceling-commands"></a>取消命令  
 使用者可以取消目前明確的工作階段的內容中目前執行的命令傳送**取消**命令沒有指定屬性。  
  
> [!NOTE]  
>  使用者無法取消在明確的工作階段中執行的命令。  
  
### <a name="canceling-batch-commands"></a>取消批次命令  
 如果使用者取消**批次**命令，則所有剩餘的命令中尚未執行**批次**命令已取消。 如果**批次**命令是交易式、 之前所執行的任何命令**取消**執行命令會回復。  
  
## <a name="canceling-sessions"></a>取消工作階段  
 藉由指定明確的工作階段中的工作階段識別項[SessionID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/id-element-xmla)屬性**取消**命令時，資料庫管理員或伺服器系統管理員可以取消工作階段，包括目前正在執行命令。 資料庫管理員只能取消他或她擁有管理權限的資料庫之工作階段。  
  
 資料庫管理員可以擷取 DISCOVER_SESSIONS 結構描述資料列集，以擷取指定資料庫的使用中工作階段。 若要擷取 DISCOVER_SESSIONS 結構描述資料列集，資料庫管理員可以使用 XMLA**探索**方法並指定適當的資料庫識別碼，為 SESSION_CURRENT_DATABASE 限制資料行中的[限制](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/restrictions-element-xmla)屬性**Discover**方法。  
  
## <a name="canceling-connections"></a>取消連接  
 藉由指定的連接識別項[ConnectionID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/connectionid-element-xmla)屬性**取消**命令時，伺服器系統管理員可以取消所有與指定的連接，包括所有相關聯的工作階段執行命令，並取消連接。  
  
> [!NOTE]
>  如果執行個體[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]無法找出並取消與連接相關聯的工作階段，例如當資料幫浦開啟多個工作階段，同時提供 HTTP 連線時，執行個體無法取消連接。 如果在執行期間發生此情況下**取消**命令時，發生錯誤。  
  
 伺服器系統管理員可以擷取的使用中連線[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]執行個體擷取 DISCOVER_CONNECTIONS 結構描述資料列集使用 XMLA **Discover**方法。  
  
## <a name="canceling-server-processes"></a>取消伺服器處理序  
 藉由指定伺服器處理序識別碼 (SPID)，在[SPID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/id-element-xmla)屬性**取消**命令時，伺服器系統管理員可以取消與指定 SPID 相關聯的命令。  
  
## <a name="canceling-associated-sessions-and-connections"></a>取消關聯的工作階段和連接。  
 您可以設定[CancelAssociated](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cancelassociated-element-xmla)屬性設為 true，若要取消連接、 工作階段及連線、 工作階段中或在指定的 SPID 相關聯的命令**取消**命令。  
  
## <a name="see-also"></a>另請參閱  
 [探索方法&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover)   
 [在 Analysis Services 中使用 XMLA 進行開發](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
