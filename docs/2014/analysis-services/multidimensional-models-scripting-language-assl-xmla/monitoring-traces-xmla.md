---
title: 監視追蹤 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- XML for Analysis, traces
- XMLA, traces
- monitoring traces [XMLA]
- traces [Analysis Services]
ms.assetid: cdbfb984-18bd-4c4e-8fb7-d64ce298ed35
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bb8056842eb19bfa81cfdcf7494e058108f3e836
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48077878"
---
# <a name="monitoring-traces-xmla"></a>監視追蹤 (XMLA)
  您可以使用[Subscribe](../xmla/xml-elements-commands/subscribe-element-xmla.md)命令，在 XML for Analysis (XMLA) 來監視現有的執行個體上定義的追蹤[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。 `Subscribe` 命令會以資料列集傳回追蹤的結果。  
  
## <a name="specifying-a-trace"></a>指定追蹤  
 [物件](../xmla/xml-elements-properties/object-element-xmla.md)屬性`Subscribe`命令必須包含物件參考[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]執行個體或在追蹤[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]執行個體。 如果未指定 `Object` 屬性，或者如果在 `Object` 屬性中沒有指定追蹤識別碼，則 `Subscribe` 命令會監視命令的 SOAP 標頭中指定的明確工作階段之預設工作階段追蹤。  
  
## <a name="returning-results"></a>傳回結果  
 `Subscribe` 命令會傳回包含指定追蹤擷取的追蹤事件之資料列集。 `Subscribe`命令會傳回追蹤結果，直到取消命令為止[取消](../xmla/xml-elements-commands/cancel-element-xmla.md)命令。  
  
 資料列集包含下表中列出的資料行。  
  
|「資料行」|資料類型|描述|  
|------------|---------------|-----------------|  
|EventClass|Integer|追蹤所收到的事件類別。|  
|EventSubclass|長整數|追蹤所收到的事件子類別。|  
|CurrentTime|DATETIME|事件啟動的時間 (如果有的話)。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|StartTime|DATETIME|事件啟動的時間 (如果有的話)。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|EndTime|DATETIME|事件的結束時間 (如果有的話)。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。<br /><br /> 這個資料行不會為描述處理序或動作之開始的事件類別而擴展。|  
|Duration|長整數|事件所經歷的總時間 (以毫秒為單位)。|  
|CPUTime|長整數|事件所經歷的處理器時間 (以毫秒為單位)。|  
|JobID|長整數|處理序的作業識別碼。|  
|SessionID|String|發生事件的工作階段識別碼。|  
|SessionType|String|發生事件的工作階段類型。|  
|ProgressTotal|長整數|事件報告的進度數量。|  
|IntegerData|長整數|與事件相關聯的整數資料。 這個資料行的內容會隨著事件類別與事件子類別而不同。|  
|ObjectID|String|發生事件的物件識別碼。|  
|ObjectType|String|在 ObjectName 中指定的物件類型。|  
|ObjectName|String|發生事件的物件名稱。|  
|ObjectPath|String|發生事件的物件階層路徑。 路徑是以逗號分隔字串來表示 ObjectName 中指定物件之父系的物件識別碼。|  
|ObjectReference|String|以 XML 表示法呈現 ObjectName 中指定之物件的物件參考。|  
|NestLevel|Integer|發生事件的交易等級。|  
|NumSegments|長整數|發生事件的命令所影響或是存取的資料區段數目。|  
|Severity|Integer|事件例外狀況的嚴重性層級。 此資料行可包含下列其中一個值：<br /><br /> 值： 0 = 成功<br /><br /> 值： 1 = 資訊<br /><br /> 值： 2 = 警告<br /><br /> Value: 3 = 錯誤|  
|成功|布林|指出命令是成功或失敗。|  
|錯誤|長整數|事件的錯誤號碼 (如果適用的話)。|  
|ConnectionID|String|發生事件的連接識別碼。|  
|DatabaseName|String|發生事件的資料庫名稱。|  
|NTUserName|String|與事件相關聯的使用者之 Windows 使用者名稱。|  
|NTDomainName|String|與事件相關聯的使用者之 Windows 網域。|  
|ClientHostName|String|用戶端應用程式執行時所在的電腦名稱。 這個資料行會以用戶端應用程式所傳遞的值來擴展。|  
|ClientProcessID|長整數|用戶端應用程式的處理序識別碼。|  
|ApplicationName|String|建立 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體之連接的用戶端應用程式名稱。 這個資料行會以用戶端應用程式所傳遞的值，而非程式的顯示名稱來擴展。|  
|NTCanonicalUserName|String|與事件相關聯之使用者的 Windows 標準使用者名稱。|  
|SPID|String|發生事件之工作階段的伺服器處理序識別碼 (SPID)。 此資料行的值會直接對應到發生事件的 XMLA 訊息之 SOAP 標頭中，所指定的工作階段識別碼。|  
|TextData|String|與事件相關聯的文字資料。 這個資料行的內容會隨著事件類別與事件子類別而不同。|  
|ServerName|String|發生事件之 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體的名稱。|  
|RequestParameters|String|發生事件的參數化查詢或是 XMLA 命令的參數。|  
|RequestProperties|String|發生事件之 XMLA 方法的屬性。|  
  
## <a name="see-also"></a>另請參閱  
 [在 Analysis Services 中使用 XMLA 進行開發](developing-with-xmla-in-analysis-services.md)  
  
  
