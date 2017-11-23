---
title: "探索事件資料行 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: trace-events
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: Discover Events event category
ms.assetid: 10ec598e-5b51-4767-b4f7-42e261d96a40
caps.latest.revision: "29"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: fd7ca49c095ceb88e72392eadb15a879a9ece614
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="discover-events-data-columns"></a>探索事件資料行
  探索事件類別目錄具有下列事件類別：  
  
-   Discover Begin 類別  
  
-   Discover End 類別  
  
 下表列出每一個這類事件類別的資料行。  
  
## <a name="discover-begin-classdata-columns"></a>Discover Begin 類別—資料行  
  
|||||  
|-|-|-|-|  
|**資料行名稱**|**資料行識別碼**|**資料行類型**|**資料行描述**|  
|EventClass|0|1|事件類別用於將事件分類。|  
|EventSubclass|1|1|事件子類別提供有關每個事件類別的額外資訊。  以下是有效的 **子類別識別碼**/**子類別名稱** 值組︰<br /><br /> 0︰DBSCHEMA_CATALOGS<br /><br /> 1︰DBSCHEMA_TABLES<br /><br /> 2︰DBSCHEMA_COLUMNS<br /><br /> 3︰DBSCHEMA_PROVIDER_TYPES<br /><br /> 4︰MDSCHEMA_CUBES<br /><br /> 5︰MDSCHEMA_DIMENSIONS<br /><br /> 6︰MDSCHEMA_HIERARCHIES<br /><br /> 7︰MDSCHEMA_LEVELS<br /><br /> 8︰MDSCHEMA_MEASURES<br /><br /> 9︰MDSCHEMA_PROPERTIES<br /><br /> 10︰MDSCHEMA_MEMBERS<br /><br /> 11︰MDSCHEMA_FUNCTIONS<br /><br /> 12︰MDSCHEMA_ACTIONS<br /><br /> 13︰MDSCHEMA_SETS<br /><br /> 14︰DISCOVER_INSTANCES<br /><br /> 15︰MDSCHEMA_KPIS<br /><br /> 16︰MDSCHEMA_MEASUREGROUPS<br /><br /> 17︰MDSCHEMA_COMMANDS<br /><br /> 18︰DMSCHEMA_MINING_SERVICES<br /><br /> 19︰DMSCHEMA_MINING_SERVICE_PARAMETERS<br /><br /> 20︰DMSCHEMA_MINING_FUNCTIONS<br /><br /> 21︰DMSCHEMA_MINING_MODEL_CONTENT<br /><br /> 22︰DMSCHEMA_MINING_MODEL_XML<br /><br /> 23︰DMSCHEMA_MINING_MODELS<br /><br /> 24︰DMSCHEMA_MINING_COLUMNS<br /><br /> 25︰DISCOVER_DATASOURCES<br /><br /> 26︰DISCOVER_PROPERTIES<br /><br /> 27︰DISCOVER_SCHEMA_ROWSETS<br /><br /> 28︰DISCOVER_ENUMERATORS<br /><br /> 29︰DISCOVER_KEYWORDS<br /><br /> 30︰DISCOVER_LITERALS<br /><br /> 31︰DISCOVER_XML_METADATA<br /><br /> 32︰DISCOVER_TRACES<br /><br /> 33︰DISCOVER_TRACE_DEFINITION_PROVIDERINFO<br /><br /> 34︰DISCOVER_TRACE_COLUMNS<br /><br /> 35︰DISCOVER_TRACE_EVENT_CATEGORIES<br /><br /> 36︰DMSCHEMA_MINING_STRUCTURES<br /><br /> 37︰DMSCHEMA_MINING_STRUCTURE_COLUMNS<br /><br /> 38︰DISCOVER_MASTER_KEY<br /><br /> 39︰MDSCHEMA_INPUT_DATASOURCES<br /><br /> 40︰DISCOVER_LOCATIONS<br /><br /> 41︰DISCOVER_PARTITION_DIMENSION_STAT<br /><br /> 42︰DISCOVER_PARTITION_STAT<br /><br /> 43︰DISCOVER_DIMENSION_STAT<br /><br /> 44︰MDSCHEMA_MEASUREGROUP_DIMENSIONS<br /><br /> 49︰DISCOVER_XEVENT_TRACE_DEFINITION|  
|CurrentTime|2|5|事件的開始時間 (如果可以取得的話)。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|StartTime|3|5|事件的開始時間 (如果可以取得的話)。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|ConnectionID|25|1|包含與探索事件相關聯的唯一連接識別碼。|  
|DatabaseName|28|8|正在執行使用者之陳述式的資料庫名稱。|  
|NTUserName|32|8|包含與探索事件相關聯的 Windows 使用者名稱。 使用者名稱採用標準格式。 例如，engineering.microsoft.com/software/user。|  
|NTDomainName|33|8|包含與探索事件相關聯的 Windows 網域。|  
|ClientProcessID|36|1|包含用戶端應用程式的處理序識別碼。|  
|ApplicationName|37|8|建立伺服器連接的用戶端應用程式名稱。 這個資料行會填入應用程式所傳送的值，而非程式的顯示名稱。|  
|SessionID|39|8|包含與探索事件相關聯的工作階段識別碼。|  
|NTCanonicalUserName|40|8|包含與探索事件相關聯的 Windows 使用者名稱。 使用者名稱採用標準格式。 例如，engineering.microsoft.com/software/user。|  
|SPID|41|1|包含伺服器處理序識別碼 (SPID)，它會唯一識別與探索事件相關聯的使用者工作階段。 SPID 直接對應到 XMLA 使用的工作階段 GUID。|  
|TextData|42|9|包含與事件相關聯的文字資料。|  
|ServerName|43|8|包含發生探索事件之 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體的名稱。|  
|RequestProperties|45|9|包含與探索事件相關聯的 XML for Analysis (XMLA) 要求屬性。|  
  
## <a name="discover-end-classdata-columns"></a>Discover End 類別—資料行  
  
|||||  
|-|-|-|-|  
|**資料行名稱**|**資料行識別碼**|**資料行類型**|**資料行描述**|  
|EventClass|0|1|包含事件類別；事件類別用於將事件分類。|  
|EventSubclass|1|1|事件子類別提供有關每個事件類別的額外資訊。 以下是有效的 **子類別識別碼**/**子類別名稱** 值組︰<br /><br /> 0︰DBSCHEMA_CATALOGS<br /><br /> 1︰DBSCHEMA_TABLES<br /><br /> 2︰DBSCHEMA_COLUMNS<br /><br /> 3︰DBSCHEMA_PROVIDER_TYPES<br /><br /> 4︰MDSCHEMA_CUBES<br /><br /> 5︰MDSCHEMA_DIMENSIONS<br /><br /> 6︰MDSCHEMA_HIERARCHIES<br /><br /> 7︰MDSCHEMA_LEVELS<br /><br /> 8︰MDSCHEMA_MEASURES<br /><br /> 9︰MDSCHEMA_PROPERTIES<br /><br /> 10︰MDSCHEMA_MEMBERS<br /><br /> 11︰MDSCHEMA_FUNCTIONS<br /><br /> 12︰MDSCHEMA_ACTIONS<br /><br /> 13︰MDSCHEMA_SETS<br /><br /> 14︰DISCOVER_INSTANCES<br /><br /> 15︰MDSCHEMA_KPIS<br /><br /> 16︰MDSCHEMA_MEASUREGROUPS<br /><br /> 17︰MDSCHEMA_COMMANDS<br /><br /> 18︰DMSCHEMA_MINING_SERVICES<br /><br /> 19︰DMSCHEMA_MINING_SERVICE_PARAMETERS<br /><br /> 20︰DMSCHEMA_MINING_FUNCTIONS<br /><br /> 21︰DMSCHEMA_MINING_MODEL_CONTENT<br /><br /> 22︰DMSCHEMA_MINING_MODEL_XML<br /><br /> 23︰DMSCHEMA_MINING_MODELS<br /><br /> 24︰DMSCHEMA_MINING_COLUMNS<br /><br /> 25︰DISCOVER_DATASOURCES<br /><br /> 26︰DISCOVER_PROPERTIES<br /><br /> 27︰DISCOVER_SCHEMA_ROWSETS<br /><br /> 28︰DISCOVER_ENUMERATORS<br /><br /> 29︰DISCOVER_KEYWORDS<br /><br /> 30︰DISCOVER_LITERALS<br /><br /> 31︰DISCOVER_XML_METADATA<br /><br /> 32︰DISCOVER_TRACES<br /><br /> 33︰DISCOVER_TRACE_DEFINITION_PROVIDERINFO<br /><br /> 34︰DISCOVER_TRACE_COLUMNS<br /><br /> 35︰DISCOVER_TRACE_EVENT_CATEGORIES<br /><br /> 36︰DMSCHEMA_MINING_STRUCTURES<br /><br /> 37︰DMSCHEMA_MINING_STRUCTURE_COLUMNS<br /><br /> 38︰DISCOVER_MASTER_KEY<br /><br /> 39︰MDSCHEMA_INPUT_DATASOURCES<br /><br /> 40︰DISCOVER_LOCATIONS<br /><br /> 41︰DISCOVER_PARTITION_DIMENSION_STAT<br /><br /> 42︰DISCOVER_PARTITION_STAT<br /><br /> 43︰DISCOVER_DIMENSION_STAT<br /><br /> 44︰MDSCHEMA_MEASUREGROUP_DIMENSIONS<br /><br /> 49︰DISCOVER_XEVENT_TRACE_DEFINITION|  
|CurrentTime|2|5|包含探索事件的目前時間 (如果有的話)。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|StartTime|3|5|包含啟動探索結束事件的時間 (如果有的話)。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|EndTime|4|5|包含事件結束的時間。 此資料行不會因啟動的事件類別 (如 SQL:BatchStarting 或 SP:Starting) 而擴展。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|有效期間|5|2|包含探索事件所花費的大約時間量 (毫秒)。|  
|CPUTime|6|2|包含事件所使用的 CPU 時間量 (以毫秒為單位)。|  
|Severity|22|1|包含例外狀況的嚴重性層級。|  
|成功|23|1|包含探索事件的成功或失敗。 值為：<br /><br /> 0 = 失敗<br /><br /> 1 = 成功|  
|錯誤|24|1|包含與探索事件相關聯之任何錯誤的錯誤號碼。|  
|ConnectionID|25|1|包含與探索事件相關聯的唯一連接識別碼。|  
|DatabaseName|28|8|包含發生探索事件之資料庫的名稱。|  
|NTUserName|32|8|包含與物件權限事件相關聯的 Windows 使用者名稱。|  
|NTDomainName|33|8|包含與探索事件相關聯的 Windows 網域帳戶。|  
|ClientProcessID|36|1|包含起始事件之應用程式的用戶端處理序識別碼。|  
|ApplicationName|37|8|包含建立伺服器之連接的用戶端應用程式名稱。 這個資料行會填入應用程式所傳送的值，而非程式的顯示名稱。|  
|SessionID|39|8|包含與探索事件相關聯的工作階段識別碼。|  
|NTCanonicalUserName|40|8|包含與物件權限事件相關聯的 Windows 使用者名稱。 使用者名稱採用標準格式。 例如，engineering.microsoft.com/software/user。|  
|SPID|41|1|包含伺服器處理序識別碼 (SPID)，它會唯一識別與探索結束事件相關聯的使用者工作階段。 SPID 直接對應到 XMLA 使用的工作階段 GUID。|  
|TextData|42|9|包含與事件相關聯的文字資料。|  
|ServerName|43|8|包含發生探索事件之 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體的名稱。|  
|RequestProperties|45|9|包含 XMLA 要求中的屬性。|  
  
## <a name="see-also"></a>請參閱＜  
 [Discover Events Event Category](../../analysis-services/trace-events/discover-events-event-category.md)  
  
  
