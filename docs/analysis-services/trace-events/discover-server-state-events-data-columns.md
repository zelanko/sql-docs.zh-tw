---
title: 探索伺服器狀態事件資料行 |Microsoft 文件
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: trace-events
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 992dc91233947af8368255a5a2e6103cf33f842d
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="discover-server-state-events-data-columns"></a>探索伺服器狀態事件資料行
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  探索伺服器狀態事件類別目錄具有下列事件類別：  
  
|**事件識別碼**|**事件名稱**|**事件描述**|  
|------------------|--------------------|---------------------------|  
|33|伺服器狀態探索的開始|伺服器狀態探索的開始。|  
|34|伺服器狀態探索資料|伺服器狀態探索回應的內容。|  
|35|伺服器狀態探索的結束|伺服器狀態探索的結束。|  
  
 下表列出每一個這類事件類別的資料行。  
  
## <a name="server-state-discover-begin-classdata-columns"></a>伺服器狀態探索開始類別—資料行  
  
|||||  
|-|-|-|-|  
|**資料行名稱**|**資料行識別碼**|**資料行類型**|**資料行描述**|  
|EventClass|0|1|事件類別用於將事件分類。|  
|EventSubclass|1|1|事件子類別提供有關每個事件類別的額外資訊：<br /><br /> 1： **DISCOVER_CONNECTIONS**<br /><br /> 2： **DISCOVER_SESSIONS**<br /><br /> 3： **DISCOVER_TRANSACTIONS**<br /><br /> 6： **DISCOVER_DB_CONNECTIONS**<br /><br /> 7： **DISCOVER_JOBS**<br /><br /> 8： **DISCOVER_LOCKS**<br /><br /> 12： **DISCOVER_PERFORMANCE_COUNTERS**<br /><br /> 13： **DISCOVER_MEMORYUSAGE**<br /><br /> 14： **DISCOVER_JOB_PROGRESS**<br /><br /> 15： **DISCOVER_MEMORYGRANT**|  
|CurrentTime|2|5|包含伺服器狀態探索事件的目前時間 (如果有的話)。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|StartTime|3|5|包含事件開始的時間 (如果有的話)。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|ConnectionID|25|1|包含與伺服器狀態探索事件相關聯的唯一連接識別碼。|  
|NTUserName|32|8|包含與伺服器狀態探索事件相關聯的 Windows 使用者帳戶。|  
|NTDomainName|33|8|包含與伺服器狀態探索事件相關聯的 Windows 網域帳戶。|  
|ClientProcessID|36|1|包含建立伺服器之連接的用戶端應用程式處理序識別碼。|  
|ApplicationName|37|8|包含建立伺服器之連接的用戶端應用程式名稱。 這個資料行會填入應用程式所傳送的值，而非程式的顯示名稱。|  
|SessionID|39|8|包含與伺服器狀態探索事件相關聯的工作階段識別碼。|  
|NTCanonicalUserName|40|8|包含與伺服器狀態探索事件相關聯的 Windows 使用者名稱。 使用者名稱採用標準格式。 例如，engineering.microsoft.com/software/user。|  
|SPID|41|1|包含伺服器處理序識別碼 (SPID)，它會唯一識別與伺服器狀態探索事件相關聯的使用者工作階段。 SPID 直接對應到 XMLA 使用的工作階段 GUID。|  
|TextData|42|9|包含與事件相關聯的文字資料。|  
|ServerName|43|8|包含發生伺服器狀態探索事件的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體名稱。|  
|RequestProperties|45|9|包含目前 XMLA 要求的屬性。|  
  
## <a name="server-state-discover-data-classdata-columns"></a>伺服器狀態探索資料類別—資料行  
  
|||||  
|-|-|-|-|  
|**資料行名稱**|**資料行識別碼**|**資料行類型**|**資料行描述**|  
|EventClass|0|1|事件類別用於將事件分類。|  
|EventSubclass|1|1|事件子類別提供有關每個事件類別的額外資訊：<br /><br /> 1： **DISCOVER_CONNECTIONS**<br /><br /> 2： **DISCOVER_SESSIONS**<br /><br /> 3： **DISCOVER_TRANSACTIONS**<br /><br /> 6： **DISCOVER_DB_CONNECTIONS**<br /><br /> 7： **DISCOVER_JOBS**<br /><br /> 8： **DISCOVER_LOCKS**<br /><br /> 12： **DISCOVER_PERFORMANCE_COUNTERS**<br /><br /> 13： **DISCOVER_MEMORYUSAGE**<br /><br /> 14： **DISCOVER_JOB_PROGRESS**<br /><br /> 15： **DISCOVER_MEMORYGRANT**|  
|CurrentTime|2|5|包含伺服器狀態探索事件的目前時間 (如果有的話)。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|StartTime|3|5|包含事件開始的時間 (如果有的話)。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|ConnectionID|25|1|包含與伺服器狀態探索事件相關聯的唯一連接識別碼。|  
|SessionID|39|8|包含與伺服器狀態探索事件相關聯的工作階段識別碼。|  
|SPID|41|1|包含伺服器處理序識別碼 (SPID)，它會唯一識別與伺服器狀態探索事件相關聯的使用者工作階段。 SPID 直接對應到 XMLA 使用的工作階段 GUID。|  
|TextData|42|9|包含與伺服器對探索要求之回應相關聯的文字資料。|  
|ServerName|43|8|包含發生伺服器狀態探索事件的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體名稱。|  
  
## <a name="server-state-discover-end-classdata-columns"></a>伺服器狀態探索結束類別—資料行  
  
|||||  
|-|-|-|-|  
|**資料行名稱**|**資料行識別碼**|**資料行類型**|**資料行描述**|  
|EventClass|0|1|事件類別用於將事件分類。|  
|EventSubclass|1|1|事件子類別提供有關每個事件類別的額外資訊：<br /><br /> 1： **DISCOVER_CONNECTIONS**<br /><br /> 2： **DISCOVER_SESSIONS**<br /><br /> 3： **DISCOVER_TRANSACTIONS**<br /><br /> 6： **DISCOVER_DB_CONNECTIONS**<br /><br /> 7： **DISCOVER_JOBS**<br /><br /> 8： **DISCOVER_LOCKS**<br /><br /> 12： **DISCOVER_PERFORMANCE_COUNTERS**<br /><br /> 13： **DISCOVER_MEMORYUSAGE**<br /><br /> 14： **DISCOVER_JOB_PROGRESS**<br /><br /> 15： **DISCOVER_MEMORYGRANT**|  
|CurrentTime|2|5|包含伺服器狀態探索事件的目前時間 (如果有的話)。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|StartTime|3|5|包含事件開始的時間 (如果有的話)。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|EndTime|4|5|包含事件結束的時間。 此資料行不會因啟動的事件類別 (如 SQL:BatchStarting 或 SP:Starting) 而擴展。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|有效期間|5|2|包含事件所花費的時間量 (以毫秒為單位)。|  
|CPUTime|6|2|包含伺服器狀態探索事件所使用的 CPU 時間量 (以毫秒為單位)。|  
|ConnectionID|25|1|包含與伺服器狀態探索事件相關聯的唯一連接識別碼。|  
|NTUserName|32|8|包含與伺服器狀態探索事件相關聯的 Windows 使用者帳戶。|  
|NTDomainName|33|8|包含與伺服器狀態探索事件相關聯的 Windows 網域帳戶。|  
|ClientProcessID|36|1|包含起始 XMLA 要求之用戶端應用程式的處理序識別碼。|  
|ApplicationName|37|8|包含建立伺服器之連接的用戶端應用程式名稱。 這個資料行會填入應用程式所傳送的值，而非程式的顯示名稱。|  
|SessionID|39|8|包含與伺服器狀態探索事件相關聯的 Windows 網域帳戶。|  
|NTCanonicalUserName|40|8|包含與伺服器狀態探索事件相關聯的 Windows 使用者名稱。 使用者名稱採用標準格式。 例如，engineering.microsoft.com/software/user。|  
|SPID|41|1|包含伺服器處理序識別碼 (SPID)，它會唯一識別與伺服器狀態探索事件相關聯的使用者工作階段。 SPID 直接對應到 XMLA 使用的工作階段 GUID。|  
|TextData|42|9|包含與伺服器對探索要求之回應相關聯的文字資料。|  
|ServerName|43|8|包含發生伺服器狀態探索事件的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體名稱。|  
  
## <a name="see-also"></a>另請參閱  
 [探索伺服器狀態事件類別目錄](../../analysis-services/trace-events/discover-server-state-event-category.md)  
  
  
