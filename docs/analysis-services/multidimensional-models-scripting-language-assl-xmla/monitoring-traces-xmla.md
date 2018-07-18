---
title: 監視追蹤 (XMLA) |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 24aab35b34ed9339ec2d7950efab21a94b2c0d96
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34021515"
---
# <a name="monitoring-traces-xmla"></a>監視追蹤 (XMLA)
  您可以使用[訂閱](../../analysis-services/xmla/xml-elements-commands/subscribe-element-xmla.md)XML for Analysis (XMLA) 來監視現有的執行個體上定義的追蹤命令[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。 **訂閱**命令會傳回成資料列集追蹤的結果。  
  
## <a name="specifying-a-trace"></a>指定追蹤  
 [物件](../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)屬性**訂閱**命令必須包含物件參考為[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]執行個體或上的追蹤[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]執行個體。 如果**物件**未指定屬性，或在未指定追蹤識別碼**物件**屬性，**訂閱**命令監視的預設工作階段追蹤指定命令的 SOAP 標頭中的明確工作階段。  
  
## <a name="returning-results"></a>傳回結果  
 **訂閱**命令會傳回包含指定追蹤所擷取的追蹤事件的資料列集。 **訂閱**命令會傳回追蹤結果，直到取消命令為止[取消](../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md)命令。  
  
 資料列集包含下表中列出的資料行。  
  
|資料行|資料類型|Description|  
|------------|---------------|-----------------|  
|EventClass|Integer|追蹤所收到的事件類別。|  
|EventSubclass|長整數|追蹤所收到的事件子類別。|  
|CurrentTime|Datetime|事件啟動的時間 (如果有的話)。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|StartTime|Datetime|事件啟動的時間 (如果有的話)。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|EndTime|Datetime|事件的結束時間 (如果有的話)。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。<br /><br /> 這個資料行不會為描述處理序或動作之開始的事件類別而擴展。|  
|有效期間|長整數|事件所經歷的總時間 (以毫秒為單位)。|  
|CPUTime|長整數|事件所經歷的處理器時間 (以毫秒為單位)。|  
|JobID|長整數|處理序的作業識別碼。|  
|SessionID|字串|發生事件的工作階段識別碼。|  
|SessionType|字串|發生事件的工作階段類型。|  
|ProgressTotal|長整數|事件報告的進度數量。|  
|IntegerData|長整數|與事件相關聯的整數資料。 這個資料行的內容會隨著事件類別與事件子類別而不同。|  
|ObjectID|字串|發生事件的物件識別碼。|  
|ObjectType|字串|在 ObjectName 中指定的物件類型。|  
|ObjectName|字串|發生事件的物件名稱。|  
|ObjectPath|字串|發生事件的物件階層路徑。 路徑是以逗號分隔字串來表示 ObjectName 中指定物件之父系的物件識別碼。|  
|ObjectReference|字串|以 XML 表示法呈現 ObjectName 中指定之物件的物件參考。|  
|NestLevel|Integer|發生事件的交易等級。|  
|NumSegments|長整數|發生事件的命令所影響或是存取的資料區段數目。|  
|Severity|Integer|事件例外狀況的嚴重性層級。 此資料行可包含下列其中一個值：<br /><br /> <br /><br /> 0： 成功<br /><br /> <br /><br /> 1： 資訊<br /><br /> <br /><br /> 2： 警告<br /><br /> <br /><br /> 3： 錯誤|  
|成功|布林|指出命令是成功或失敗。|  
|錯誤|長整數|事件的錯誤號碼 (如果適用的話)。|  
|ConnectionID|字串|發生事件的連接識別碼。|  
|DatabaseName|字串|發生事件的資料庫名稱。|  
|NTUserName|字串|與事件相關聯的使用者之 Windows 使用者名稱。|  
|NTDomainName|字串|與事件相關聯的使用者之 Windows 網域。|  
|ClientHostName|字串|用戶端應用程式執行時所在的電腦名稱。 這個資料行會以用戶端應用程式所傳遞的值來擴展。|  
|ClientProcessID|長整數|用戶端應用程式的處理序識別碼。|  
|ApplicationName|字串|建立 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體之連接的用戶端應用程式名稱。 這個資料行會以用戶端應用程式所傳遞的值，而非程式的顯示名稱來擴展。|  
|NTCanonicalUserName|字串|與事件相關聯之使用者的 Windows 標準使用者名稱。|  
|SPID|字串|發生事件之工作階段的伺服器處理序識別碼 (SPID)。 此資料行的值會直接對應到發生事件的 XMLA 訊息之 SOAP 標頭中，所指定的工作階段識別碼。|  
|TextData|字串|與事件相關聯的文字資料。 這個資料行的內容會隨著事件類別與事件子類別而不同。|  
|ssSqlProfiler|字串|發生事件之 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體的名稱。|  
|RequestParameters|字串|發生事件的參數化查詢或是 XMLA 命令的參數。|  
|RequestProperties|字串|發生事件之 XMLA 方法的屬性。|  
  
## <a name="see-also"></a>另請參閱  
 [使用 Analysis Services 中的 XMLA 進行開發](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
