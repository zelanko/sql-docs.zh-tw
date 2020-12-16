---
description: Performance Statistics 事件類別
title: Performance Statistics 事件類別 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Performance Statistics event class
ms.assetid: da9cd2c4-6fdd-4ada-b74f-105e3541393c
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 41f86301a0520201fb0316de6d4d3379d27c37d1
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97467869"
---
# <a name="performance-statistics-event-class"></a>Performance Statistics 事件類別
[!INCLUDE [SQL Server - ASDB](../../includes/applies-to-version/sql-asdb.md)]
  Performance Statistics 事件類別可用來監視正在執行之查詢、預存程序和觸發程序的效能。 其六個事件子類別分別表示了系統中查詢、預存程序和觸發程序存留期間內的一項事件。 您可以使用這些事件子類別以及關聯 sys.dm_exec_query_stats、sys.dm_exec_procedure_stats 和 sys.dm_exec_trigger_stats 動態管理檢視的組合，重新組成任何給定查詢、預存程序或觸發程序的效能記錄。  
  
## <a name="performance-statistics-event-class-data-columns"></a>Performance Statistics 事件類別資料行  
 下表描述與下列每個事件子類別相關聯的事件類別資料行：EventSubClass 0、EventSubClass 1、EventSubClass 2、EventSubClass 3、EventSubClass 4 和 EventSubClass 5。  
  
### <a name="eventsubclass-0"></a>EventSubClass 0  
  
|資料行名稱|資料類型|描述|資料行識別碼|可篩選|  
|----------------------|---------------|-----------------|---------------|----------------|  
|BigintData1|**bigint**|NULL|52|是|  
|BinaryData|**image**|NULL|2|是|  
|DatabaseID|**int**|由 USE *database* 陳述式所指定的資料庫識別碼，或者如果沒有針對指定執行個體發出 USE *database* 陳述式，則是預設的資料庫。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 如果在追蹤中擷取 ServerName 資料行，則會顯示資料庫的名稱。 請使用 DB_ID 函數判斷資料庫的值。|3|是|  
|EventSequence|**int**|要求中的給定事件順序。|51|否|  
|EventSubClass|**int**|事件子類別的類型。<br /><br /> 0 = 目前未顯示在快取中的新批次 SQL 文字。<br /><br /> 特定批次的追蹤會產生下列 EventSubClass 類型。<br /><br /> 針對查詢數目為 *n* 的隨選批次：<br /><br /> 類型 0 之 1|21|是|  
|IntegerData2|**int**|NULL|55|是|  
|ObjectID|**int**|NULL|22|是|  
|Offset|**int**|NULL|61|是|  
|PlanHandle|**映像**|NULL|65|是|  
|SessionLoginName|**nvarchar**|引發工作階段之使用者的登入名稱。 例如，如果您使用 Login1 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，並以 Login2 身分執行陳述式，則 SessionLoginName 將顯示 Login1 而 LoginName 則顯示 Login2。 此資料行將同時顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 登入。|64|是|  
|SPID|**int**|事件發生所在之工作階段的識別碼。|12|是|  
|SqlHandle|**image**|SQL 控制代碼，可用它來透過 sys.dm_exec_sql_text 動態管理檢視取得批次 SQL 文字。|63|是|  
|StartTime|**datetime**|事件啟動的時間 (如果有的話)。|14|是|  
|TextData|**ntext**|批次的 SQL 文字。|1|是|  
  
### <a name="eventsubclass-1"></a>EventSubClass 1  
  
|資料行名稱|資料類型|描述|資料行識別碼|可篩選|  
|----------------------|---------------|-----------------|---------------|----------------|  
|BigintData1|**bigint**|重新編譯這個計畫的累加次數。|52|是|  
|BinaryData|**image**|已編譯計畫的二進位 XML。|2|是|  
|DatabaseID|**int**|由 USE *database* 陳述式所指定的資料庫識別碼，或者如果沒有針對指定執行個體發出 USE *database* 陳述式，則是預設的資料庫。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 如果在追蹤中擷取 ServerName 資料行，則會顯示資料庫的名稱。 請使用 DB_ID 函數判斷資料庫的值。|3|是|  
|EventSequence|**int**|要求中的給定事件順序。|51|否|  
|SessionLoginName|**nvarchar**|引發工作階段之使用者的登入名稱。 例如，如果您使用 Login1 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，並以 Login2 身分執行陳述式，則 SessionLoginName 將顯示 Login1 而 LoginName 則顯示 Login2。 此資料行將同時顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 登入。|64|是|  
|EventSubClass|**int**|事件子類別的類型。<br /><br /> 1 = 預存程序內的已編譯查詢。<br /><br /> 預存程序的追蹤會產生下列 EventSubClass 類型。<br /><br /> 針對查詢數目為 *n* 的預存程序：<br /><br /> 數目為 *n* 的類型 1|21|是|  
|IntegerData2|**int**|預存程序內的陳述式結尾。<br /><br /> -1 代表預存程序的結尾。|55|是|  
|ObjectID|**int**|系統指派給物件的識別碼。|22|是|  
|Offset|**int**|預存程序或批次內之陳述式的起始位移。|61|是|  
|SPID|**int**|事件發生所在之工作階段的識別碼。|12|是|  
|SqlHandle|**image**|SQL 控制代碼，可用它來透過 dm_exec_sql_text 動態管理檢視取得預存程序的 SQL 文字。|63|是|  
|StartTime|**datetime**|事件啟動的時間 (如果有的話)。|14|是|  
|TextData|**ntext**|NULL|1|是|  
|PlanHandle|**image**|預存程序之已編譯計畫的計畫控制代碼。 這可用來取得 XML 計畫，其方式是利用 sys.dm_exec_query_plan 動態管理檢視。|65|是|  
|ObjectType|**int**|代表參與事件之物件類型的值。<br /><br /> 8272 = 預存程序|28|是|  
|BigintData2|**bigint**|編譯期間使用的總記憶體，以 KB 為單位。|53|是|  
|CPU|**int**|編譯期間所花的總 CPU 時間，以毫秒為單位。|18|是|  
|Duration|**int**|編譯期間所用的總時間，以百萬分之一秒為單位。|13|是|  
|IntegerData|**int**|已編譯計畫的大小，以 KB 為單位。|25|是|  
  
### <a name="eventsubclass-2"></a>EventSubClass 2  
  
|資料行名稱|資料類型|描述|資料行識別碼|可篩選|  
|----------------------|---------------|-----------------|---------------|----------------|  
|BigintData1|**bigint**|重新編譯這個計畫的累加次數。|52|是|  
|BinaryData|**image**|已編譯計畫的二進位 XML。|2|是|  
|DatabaseID|**int**|由 USE *database* 陳述式所指定的資料庫識別碼，或者如果沒有針對指定執行個體發出 USE *database* 陳述式，則是預設的資料庫。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 如果在追蹤中擷取 ServerName 資料行，則會顯示資料庫的名稱。 請使用 DB_ID 函數判斷資料庫的值。|3|是|  
|EventSequence|**int**|要求中的給定事件順序。|51|否|  
|SessionLoginName|**nvarchar**|引發工作階段之使用者的登入名稱。 例如，如果您使用 Login1 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，並以 Login2 身分執行陳述式，則 SessionLoginName 將顯示 Login1 而 LoginName 則顯示 Login2。 此資料行將同時顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 登入。|64|是|  
|EventSubClass|**int**|事件子類別的類型。<br /><br /> 2 = 特定 SQL 陳述式內的已編譯查詢。<br /><br /> 特定批次的追蹤會產生下列 EventSubClass 類型。<br /><br /> 針對查詢數目為 *n* 的隨選批次：<br /><br /> 數目為 *n* 的類型 2|21|是|  
|IntegerData2|**int**|批次內的陳述式結尾。<br /><br /> -1 代表批次的結尾。|55|是|  
|ObjectID|**int**|N/A|22|是|  
|Offset|**int**|批次內的陳述式起始位移。<br /><br /> 0 代表批次的開頭。|61|是|  
|SPID|**int**|事件發生所在之工作階段的識別碼。|12|是|  
|SqlHandle|**image**|SQL 控制代碼。 這可用來透過 dm_exec_sql_text 動態管理檢視取得批次 SQL 文字。|63|是|  
|StartTime|**datetime**|事件啟動的時間 (如果有的話)。|14|是|  
|TextData|**ntext**|NULL|1|是|  
|PlanHandle|**image**|批次之已編譯計畫的計畫控制代碼。 這可用來取得批次 XML 計畫，其方式是利用 dm_exec_query_plan 動態管理檢視。|65|是|  
|BigintData2|**bigint**|編譯期間使用的總記憶體，以 KB 為單位。|53|是|  
|CPU|**int**|編譯期間所花的總 CPU 時間，以百萬分之一秒為單位。|18|是|  
|Duration|**int**|編譯期間所用的總時間，以毫秒為單位。|13|是|  
|IntegerData|**int**|已編譯計畫的大小，以 KB 為單位。|25|是|  
  
### <a name="eventsubclass-3"></a>EventSubClass 3  
  
|資料行名稱|資料類型|描述|資料行識別碼|可篩選|  
|----------------------|---------------|-----------------|---------------|----------------|  
|BigintData1|**bigint**|重新編譯這個計畫的累加次數。|52|是|  
|BinaryData|**image**|NULL|2|是|  
|DatabaseID|**int**|由 USE *database* 陳述式所指定的資料庫識別碼，或者如果沒有針對指定執行個體發出 USE *database* 陳述式，則是預設的資料庫。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 如果在追蹤中擷取 ServerName 資料行，則會顯示資料庫的名稱。 請使用 DB_ID 函數判斷資料庫的值。|3|是|  
|EventSequence|**int**|要求中的給定事件順序。|51|否|  
|SessionLoginName|**nvarchar**|引發工作階段之使用者的登入名稱。 例如，如果您使用 Login1 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，並以 Login2 身分執行陳述式，則 SessionLoginName 將顯示 Login1 而 LoginName 則顯示 Login2。 此資料行將同時顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 登入。|64|是|  
|EventSubClass|**int**|事件子類別的類型。<br /><br /> 3 = 快取查詢已銷毀，該計畫相關聯的記錄效能資料也將被銷毀。<br /><br /> 追蹤會產生下列 EventSubClass 類型。<br /><br /> 針對查詢數目為 *n* 的隨選批次：<br /><br /> 從快取中排清查詢時，類型 3 之 1<br /><br /> 針對查詢數目為 *n* 的預存程序：<br /><br /> 從快取中排清查詢時，類型 3 之 1。|21|是|  
|IntegerData2|**int**|預存程序或批次內的陳述式結尾。<br /><br /> -1 代表預存程序或批次的結尾。|55|是|  
|ObjectID|**int**|NULL|22|是|  
|Offset|**int**|預存程序或批次內之陳述式的起始位移。<br /><br /> 0 代表預存程序或批次的開頭。|61|是|  
|SPID|**int**|事件發生所在之工作階段的識別碼。|12|是|  
|SqlHandle|**image**|SQL 控制代碼，可用它來透過 dm_exec_sql_text 動態管理檢視取得預存程序或批次 SQL 文字。|63|是|  
|StartTime|**datetime**|事件啟動的時間 (如果有的話)。|14|是|  
|TextData|**ntext**|QueryExecutionStats|1|是|  
|PlanHandle|**image**|預存程序或批次的編譯計畫之計畫控制代碼。 這可用來取得 XML 計畫，其方式是利用 dm_exec_query_plan 動態管理檢視。|65|是|  
|GroupID|**int**|SQL 追蹤事件引發所在之工作負載群組的識別碼。|66|是|  
  
### <a name="eventsubclass-4"></a>EventSubClass 4  
  
|資料行名稱|資料類型|描述|資料行識別碼|可篩選|  
|----------------------|---------------|-----------------|---------------|----------------|  
|BigintData1|**bigint**|NULL|52|是|  
|BinaryData|**image**|NULL|2|是|  
|DatabaseID|**int**|給定預存程序所在之資料庫的識別碼。|3|是|  
|EventSequence|**int**|要求中的給定事件順序。|51|否|  
|SessionLoginName|**nvarchar**|引發工作階段之使用者的登入名稱。 例如，如果您使用 Login1 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，並以 Login2 身分執行陳述式，則 SessionLoginName 將顯示 Login1 而 LoginName 則顯示 Login2。 此資料行將同時顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 登入。|64|是|  
|EventSubClass|**int**|事件子類別的類型。<br /><br /> 4 = 快取預存程序已經從快取中移除了，而且與它相關聯的記錄效能資料也將被銷毀。|21|是|  
|IntegerData2|**int**|NULL|55|是|  
|ObjectID|**int**|預存程序的識別碼。 這個識別碼與 sys.procedures 中的 object_id 資料行相同。|22|是|  
|Offset|**int**|NULL|61|是|  
|SPID|**int**|事件發生所在之工作階段的識別碼。|12|是|  
|SqlHandle|**image**|SQL 控制代碼，可用它來取得之前使用 dm_exec_sql_text 動態管理檢視執行的預存程序 SQL 文字。|63|是|  
|StartTime|**datetime**|事件啟動的時間 (如果有的話)。|14|是|  
|TextData|**ntext**|ProcedureExecutionStats|1|是|  
|PlanHandle|**image**|預存程序之已編譯計畫的計畫控制代碼。 這可用來取得 XML 計畫，其方式是利用 dm_exec_query_plan 動態管理檢視。|65|是|  
|GroupID|**int**|SQL 追蹤事件引發所在之工作負載群組的識別碼。|66|是|  
  
### <a name="eventsubclass-5"></a>EventSubClass 5  
  
|資料行名稱|資料類型|描述|資料行識別碼|可篩選|  
|----------------------|---------------|-----------------|---------------|----------------|  
|BigintData1|**bigint**|NULL|52|是|  
|BinaryData|**image**|NULL|2|是|  
|DatabaseID|**int**|給定觸發程序所在之資料庫的識別碼。|3|是|  
|EventSequence|**int**|要求中的給定事件順序。|51|否|  
|SessionLoginName|**nvarchar**|引發工作階段之使用者的登入名稱。 例如，如果您使用 Login1 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，並以 Login2 身分執行陳述式，則 SessionLoginName 將顯示 Login1 而 LoginName 則顯示 Login2。 此資料行將同時顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 登入。|64|是|  
|EventSubClass|**int**|事件子類別的類型。<br /><br /> 5 = 快取觸發程序已經從快取中移除了，而且與它相關聯的記錄效能資料也將被銷毀。|21|是|  
|IntegerData2|**int**|NULL|55|是|  
|ObjectID|**int**|觸發程序的識別碼。 這個識別碼與 sys.triggers/sys.server_triggers 目錄檢視中的 object_id 資料行相同。|22|是|  
|Offset|**int**|NULL|61|是|  
|SPID|**int**|事件發生所在之工作階段的識別碼。|12|是|  
|SqlHandle|**image**|SQL 控制代碼，可用它來透過 dm_exec_sql_text 動態管理檢視取得觸發程序的 SQL 文字。|63|是|  
|StartTime|**datetime**|事件啟動的時間 (如果有的話)。|14|是|  
|TextData|**ntext**|TriggerExecutionStats|1|是|  
|PlanHandle|**image**|觸發程序之已編譯計畫的計畫控制代碼。 這可用來取得 XML 計畫，其方式是利用 dm_exec_query_plan 動態管理檢視。|65|是|  
|GroupID|**int**|SQL 追蹤事件引發所在之工作負載群組的識別碼。|66|是|  
  
## <a name="see-also"></a>另請參閱  
 [擴充事件](../../relational-databases/extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [Showplan XML For Query Compile 事件類別](../../relational-databases/event-classes/showplan-xml-for-query-compile-event-class.md)   
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  
