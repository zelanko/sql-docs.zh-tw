---
title: "篩選追蹤 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-trace
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- filters [SQL Server], events
- events [SQL Server], filters
- filters [SQL Server]
- filters [SQL Server], traces
- traces [SQL Server], filters
ms.assetid: 019c10ab-68f6-4e40-a5e8-735b2e1270db
caps.latest.revision: "28"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 49755f29a54164f008e19bc542a9ca650e54b37b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="filter-a-trace"></a>篩選追蹤
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 篩選可限制追蹤中收集的事件。 如果沒有設定篩選條件，選定事件類別的所有事件都會傳回到追蹤輸出。 例如，限制追蹤裡的 Windows 使用者名稱為特定使用者，可將輸出資料縮小為只有這些使用者。  
  
 替追蹤設定篩選並非強制的。 不過，篩選可以讓追蹤期間造成的負擔降到最低。 篩選會傳回特別關注的資料，而讓效能分析和稽核都變得比較容易。  
  
 若要篩選追蹤內擷取的事件資料，請選取追蹤事件條件，以便只傳回追蹤裡的相關資料。 例如，您可以從追蹤包含或排除監視特定應用程式的活動。  
  
> [!NOTE]  
>  當 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 建立追蹤時，預設會篩選出它自己的活動。  
  
 舉個額外的例子說明，如果您要監視查詢以判斷花費最長時間執行的批次，可將追蹤事件條件設定為只監視花費超過 30 秒鐘執行的批次 (亦即 CPU 最小值 30,000 毫秒)。  
  
## <a name="filter-creation-guidelines"></a>篩選建立指導方針  
 一般而言，可依照下列步驟篩選追蹤。  
  
1.  識別您要在追蹤內包含的事件。  
  
2.  識別包含所需資訊的資料與資料行。  
  
3.  識別所需資料的子集，並且根據資料子集定義篩選。  
  
 例如，您可能只對花費超過某個長度時間的事件有興趣。 可以建立一個包含事件的追蹤，其中 **Duration** 資料行是大於 300 毫秒。 您的追蹤將不會包含 300 毫秒內完成的事件。  
  
 您可以使用 SQL Server Profiler 或 Transact-SQL 預存程序來建立篩選。  
  
 **若要篩選追蹤範本中的事件**  
  
 [篩選追蹤中的事件 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-in-a-trace-sql-server-profiler.md)  
  
 [設定追蹤篩選 &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/set-a-trace-filter-transact-sql.md)  
  
 **若要修改篩選**  
  
 [修改篩選 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/modify-a-filter-sql-server-profiler.md)  
  
 篩選的可用性視資料行而定。 部份資料行無法篩選。 可篩選的資料行只能由特定關聯式運算子進行篩選，如下表所示。  
  
|關聯式運算子|運算子符號|描述|  
|-------------------------|---------------------|-----------------|  
|相似|相似|指定追蹤事件資料必須和輸入的文字相似。 允許多值。|  
|不相似|不相似|指定追蹤事件資料絕對必須和輸入的文字不相似。 允許多值。|  
|等於|=|指定追蹤事件資料必須和輸入的值相等。 允許多值。|  
|不等於|<>|指定追蹤事件資料絕對必須和輸入的值不相等。 允許多值。|  
|大於|>|指定追蹤事件資料必須大於輸入的值。|  
|大於或等於|>=|指定追蹤事件資料必須大於或等於輸入的值。|  
|小於|<|指定追蹤事件資料必須小於輸入的值。|  
|小於或等於|<=|指定追蹤事件資料必須小於或等於輸入的值。|  
  
 下表列出可篩選的資料行與可用的關聯式運算子。  
  
|資料行|關聯式運算子|  
|------------------|--------------------------|  
|**ApplicationName**|LIKE、NOT LIKE|  
|**BigintData1**|=, <>, >=, <=|  
|**BigintData2**|=, <>, >=, <=|  
|**BinaryData**|使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 篩選這個資料行中的事件。 如需詳細資訊，請參閱 [使用 SQL Server Profiler 篩選追蹤](../../tools/sql-server-profiler/filter-traces-with-sql-server-profiler.md)。|  
|**ClientProcessID**|=, <>, >=, <=|  
|**ColumnPermissions**|=, <>, >=, <=|  
|**CPU**|=, <>, >=, <=|  
|**DatabaseID**|=, <>, >=, <=|  
|**DatabaseName**|LIKE、NOT LIKE|  
|**DBUserName**|LIKE、NOT LIKE|  
|**有效期間**|=, <>, >=, \<=|  
|**EndTime**|>=, <=|  
|**錯誤**|=, <>, >=, <=|  
|**EventSubClass**|=, <>, >=, <=|  
|**FileName**|LIKE、NOT LIKE|  
|**GUID**|使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 篩選這個資料行中的事件。 如需詳細資訊，請參閱 [使用 SQL Server Profiler 篩選追蹤](../../tools/sql-server-profiler/filter-traces-with-sql-server-profiler.md)。|  
|**Handle**|=, <>, >=, <=|  
|**HostName**|LIKE、NOT LIKE|  
|**IndexID**|=, <>, >=, <=|  
|**IntegerData**|=, <>, >=, <=|  
|**IntegerData2**|=, <>, >=, <=|  
|**IsSystem**|=, <>, >=, <=|  
|**LineNumber**|=, <>, >=, <=|  
|**LinkedServerName**|LIKE、NOT LIKE|  
|**LoginName**|LIKE、NOT LIKE|  
|**LoginSid**|使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 篩選這個資料行中的事件。 如需詳細資訊，請參閱 [使用 SQL Server Profiler 篩選追蹤](../../tools/sql-server-profiler/filter-traces-with-sql-server-profiler.md)。|  
|**MethodName**|LIKE、NOT LIKE|  
|**模式**|=, <>, >=, <=|  
|**NestLevel**|=, <>, >=, <=|  
|**NTDomainName**|LIKE、NOT LIKE|  
|**NTUserName**|LIKE、NOT LIKE|  
|**ObjectID**|=, <>, >=, <=|  
|**ObjectID2**|=, <>, >=, <=|  
|**ObjectName**|LIKE、NOT LIKE|  
|**ObjectType**|=, <>, >=, <=|  
|**Offset**|=, <>, >=, <=|  
|**OwnerID**|=, <>, >=, <=|  
|**OwnerName**|LIKE、NOT LIKE|  
|**ParentName**|LIKE、NOT LIKE|  
|**Permissions**|=, <>, >=, <=|  
|**ProviderName**|LIKE、NOT LIKE|  
|**Reads**|=, <>, >=, <=|  
|**RequestID**|=, <>, >=, <=|  
|**RoleName**|LIKE、NOT LIKE|  
|**RowCounts**|=, <>, >=, <=|  
|**SessionLoginName**|LIKE、NOT LIKE|  
|**Severity**|=, <>, >=, <=|  
|**SourceDatabaseID**|=, <>, >=, <=|  
|**SPID**|=, <>, >=, \<=|  
|**SqlHandle**|使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 篩選這個資料行中的事件。 如需詳細資訊，請參閱 [使用 SQL Server Profiler 篩選追蹤](../../tools/sql-server-profiler/filter-traces-with-sql-server-profiler.md)。|  
|**StartTime**|>=, <=|  
|**State**|=, <>, >=, <=|  
|**成功**|=, <>, >=, <=|  
|**TargetLoginName**|LIKE、NOT LIKE|  
|**TargetLoginSid**|使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 篩選這個資料行中的事件。 如需詳細資訊，請參閱 [使用 SQL Server Profiler 篩選追蹤](../../tools/sql-server-profiler/filter-traces-with-sql-server-profiler.md)。|  
|**TargetUserName**|LIKE、NOT LIKE|  
|**TextData** *|LIKE、NOT LIKE|  
|**TransactionID**|=, <>, >=, <=|  
|**型別**|=, <>, >=, <=|  
|**Writes**|=, <>, >=, <=|  
|**XactSequence**|=, <>, >=, <=|  
  
 \* 如果從 **osql** 公用程式或 **sqlcmd** 公用程式追蹤事件，篩選 **%** TextData **資料行時一律附加** 。  
  
 基於安全機制，「SQL 追蹤」會自動把任何與安全性相關、會影響密碼的預存程序的資訊從追蹤省略。 此安全機制無法設定，也永遠有效。 如此可預防有權限追蹤 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]上所有活動的使用者擷取到密碼。  
  
 下列與安全性相關的預存程序會受到監視，但是不會將輸出寫入 **TextData** 資料行：  
  
 [sp_addapprole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addapprole-transact-sql.md)  
  
 [sp_adddistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)  
  
 [sp_adddistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md)  
  
 [sp_adddistributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistributor-transact-sql.md)  
  
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)  
  
 [sp_addlinkedsrvlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)  
  
 [sp_addlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)  
  
 [sp_addmergepullsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)  
  
 [sp_addpullsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)  
  
 [sp_addremotelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addremotelogin-transact-sql.md)  
  
 [sp_addsubscriber &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscriber-transact-sql.md)  
  
 [sp_approlepassword &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-approlepassword-transact-sql.md)  
  
 [sp_changedistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md)  
  
 [sp_changesubscriber &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changesubscriber-transact-sql.md)  
  
 [sp_dsninfo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dsninfo-transact-sql.md)  
  
 [sp_helpsubscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)  
  
 [sp_link_publication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md)  
  
 [sp_password &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-password-transact-sql.md)  
  
 [sp_setapprole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-setapprole-transact-sql.md)  
  
  
