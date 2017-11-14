---
title: "進度報表的資料行 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: trace-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- Progress Reports event category
ms.assetid: d34a6322-e26b-4454-b98f-32307d6956b5
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 18f95a363c72cde1e067bb930d44c65254631ce2
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="progress-reports-data-columns"></a>進度報表資料行
  [進度報表] 事件類別目錄具有下列事件類別：  
  
|**事件識別碼**|**事件名稱**|**事件描述**|  
|------------------|--------------------|---------------------------|  
|5|進度報表開始|進度報表開始。|  
|6|進度報表結束|進度報表結束。|  
|7|進度報表目前事件|目前的進度報表。|  
|8|進度報表錯誤|進度報表錯誤。|  
  
 下表列出每一個這類事件類別的資料行。  
  
## <a name="progress-report-begindata-columns"></a>進度報表開始–資料行  
  
|**資料行名稱**|**資料行識別碼**|**資料行類型**|**資料行描述**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件類別用於將事件分類。|  
|EventSubclass|1|1|事件子類別提供有關每個事件類別的額外資訊。 以下是有效的 **子類別識別碼**： **子類別名稱** 組︰<br /><br /> 1︰ **Process**<br /><br /> 2︰ **Merge**<br /><br /> 3︰ **Delete**<br /><br /> 4： **DeleteOldAggregations**<br /><br /> 5： **Rebuild**<br /><br /> 6： **Commit**<br /><br /> 7： **Rollback**<br /><br /> 8： **CreateIndexes**<br /><br /> 9： **CreateTable**<br /><br /> 10： **InsertInto**<br /><br /> 11： **Transaction**<br /><br /> 12： **Initialize**<br /><br /> 13： **Discretize**<br /><br /> 14： **Query**<br /><br /> 15： **CreateView**<br /><br /> 16： **WriteData**<br /><br /> 17： **ReadData**<br /><br /> 18： **GroupData**<br /><br /> 19： **GroupDataRecord**<br /><br /> 20： **BuildIndex**<br /><br /> 21： **Aggregate**<br /><br /> 22： **BuildDecode**<br /><br /> 23： **WriteDecode**<br /><br /> 24： **BuildDMDecode**<br /><br /> 25： **ExecuteSQL**<br /><br /> 26： **ExecuteModifiedSQL**<br /><br /> 27： **Connecting**<br /><br /> 28： **BuildAggsAndIndexes**<br /><br /> 29： **MergeAggsOnDisk**<br /><br /> 30： **BuildIndexForRigidAggs**<br /><br /> 31： **BuildIndexForFlexibleAggs**<br /><br /> 32： **WriteAggsAndIndexes**<br /><br /> 33： **WriteSegment**<br /><br /> 34： **DataMiningProgress**<br /><br /> 35： **ReadBufferFullReport**<br /><br /> 36： **ProactiveCacheConversion**<br /><br /> 37： **Backup**<br /><br /> 38： **Restore**<br /><br /> 39： **Synchronize**<br /><br /> 40： **Build Processing Schedule**<br /><br /> 41： **Detach**<br /><br /> 42： **Attach**<br /><br /> 43： **Analyze\Encode Data**<br /><br /> 44： **Compress Segment**<br /><br /> 45： **Write Table Column**<br /><br /> 46： **Relationship Build Prepare**<br /><br /> 47： **Build Relationship Segment**<br /><br /> 48： **Load**<br /><br /> 49： **Metadata Load**<br /><br /> 50： **Data Load**<br /><br /> 51： **Post Load**<br /><br /> 52： **Metadata traversal during Backup**<br /><br /> 53： **VertiPaq**<br /><br /> 54： **Hierarchy processing**<br /><br /> 55： **Switching dictionary**|  
|CurrentTime|2|5|包含報告事件的目前時間 (如果有的話)。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|StartTime|3|5|包含事件開始的時間 (如果有的話)。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|JobID|7|1|包含與報告事件相關聯的作業識別碼。|  
|SessionType|8|8|包含與報告事件相關聯的工作階段類型 (造成事件的實體)。 針對處理事件，值為：<br /><br /> 1= 使用者<br /><br /> 2= 主動式快取<br /><br /> 3= 延遲處理|  
|ObjectID|11|8|包含與報告事件相關聯的物件識別碼 (字串)。|  
|ObjectType|12|1|包含物件類型。|  
|ObjectName|13|8|包含與報告事件相關聯之物件的名稱。|  
|ObjectPath|14|8|包含與報告事件相關聯之物件的物件路徑，做為以物件的父系開頭之父系清單 (以逗號分隔)。|  
|ObjectReference|15|8|包含報告事件的物件參考，所有父系編碼為 XML，並使用標記來描述物件。|  
|ConnectionID|25|1|包含與報告事件相關聯的唯一連接識別碼。|  
|DatabaseName|28|8|包含發生報告事件之資料庫的名稱。|  
|NTUserName|32|8|包含與報告事件相關聯的 Windows 使用者帳戶。|  
|NTDomainName|33|8|包含與報告事件相關聯的 Windows 網域帳戶。|  
|SessionID|39|8|包含與報告事件相關聯的工作階段識別碼。|  
|NTCanonicalUserName|40|8|標準格式的使用者名稱。 例如，engineering.microsoft.com/software/someone。|  
|SPID|41|1|包含伺服器處理序識別碼 (SPID)，它會唯一識別與報告事件相關聯的使用者工作階段。 SPID 直接對應至 XML for Analysis (XMLA) 使用的工作階段 GUID。|  
|TextData|42|9|包含與報告事件相關聯的文字資料。|  
|ServerName|43|8|包含發生報表事件之 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體的名稱。|  
  
## <a name="progress-report-enddata-columns"></a>進度報表結束–資料行  
  
|**資料行名稱**|**資料行識別碼**|**資料行類型**|**資料行描述**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件類別用於將事件分類。|  
|EventSubclass|1|1|事件子類別提供有關每個事件類別的額外資訊。 以下是有效的 **子類別識別碼**： **子類別名稱** 組︰<br /><br /> 1︰ **Process**<br /><br /> 2︰ **Merge**<br /><br /> 3︰ **Delete**<br /><br /> 4： **DeleteOldAggregations**<br /><br /> 5： **Rebuild**<br /><br /> 6： **Commit**<br /><br /> 7： **Rollback**<br /><br /> 8： **CreateIndexes**<br /><br /> 9： **CreateTable**<br /><br /> 10： **InsertInto**<br /><br /> 11： **Transaction**<br /><br /> 12： **Initialize**<br /><br /> 13： **Discretize**<br /><br /> 14： **Query**<br /><br /> 15： **CreateView**<br /><br /> 16： **WriteData**<br /><br /> 17： **ReadData**<br /><br /> 18： **GroupData**<br /><br /> 19： **GroupDataRecord**<br /><br /> 20： **BuildIndex**<br /><br /> 21： **Aggregate**<br /><br /> 22： **BuildDecode**<br /><br /> 23： **WriteDecode**<br /><br /> 24： **BuildDMDecode**<br /><br /> 25： **ExecuteSQL**<br /><br /> 26： **ExecuteModifiedSQL**<br /><br /> 27： **Connecting**<br /><br /> 28： **BuildAggsAndIndexes**<br /><br /> 29： **MergeAggsOnDisk**<br /><br /> 30： **BuildIndexForRigidAggs**<br /><br /> 31： **BuildIndexForFlexibleAggs**<br /><br /> 32： **WriteAggsAndIndexes**<br /><br /> 33： **WriteSegment**<br /><br /> 34： **DataMiningProgress**<br /><br /> 35： **ReadBufferFullReport**<br /><br /> 36： **ProactiveCacheConversion**<br /><br /> 37： **Backup**<br /><br /> 38： **Restore**<br /><br /> 39： **Synchronize**<br /><br /> 40： **Build Processing Schedule**<br /><br /> 41： **Detach**<br /><br /> 42： **Attach**<br /><br /> 43： **Analyze\Encode Data**<br /><br /> 44： **Compress Segment**<br /><br /> 45： **Write Table Column**<br /><br /> 46： **Relationship Build Prepare**<br /><br /> 47： **Build Relationship Segment**<br /><br /> 48： **Load**<br /><br /> 49： **Metadata Load**<br /><br /> 50： **Data Load**<br /><br /> 51： **Post Load**<br /><br /> 52： **Metadata traversal during Backup**<br /><br /> 53： **VertiPaq**<br /><br /> 54： **Hierarchy processing**<br /><br /> 55： **Switching dictionary**|  
|CurrentTime|2|5|包含報告事件的目前時間 (如果有的話)。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|StartTime|3|5|包含事件開始的時間 (如果有的話)。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|EndTime|4|5|包含事件結束的時間。 此資料行不會因啟動的事件類別 (如 SQL:BatchStarting 或 SP:Starting) 而擴展。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|有效期間|5|2|包含事件所經歷的時間量 (以毫秒為單位)。|  
|CPUTime|6|2|包含事件所使用的 CPU 時間量 (以毫秒為單位)。|  
|JobID|7|1|包含與報告事件相關聯的作業識別碼。|  
|SessionType|8|8|包含與報告事件相關聯的工作階段類型 (造成事件的實體)。 針對處理事件，值為：<br /><br /> 1= 使用者<br /><br /> 2= 主動式快取<br /><br /> 3= 延遲處理|  
|ProgressTotal|9|1|包含報告事件的整體進度。|  
|IntegerData|10|1|包含與報告事件相關聯的整數資料，例如針對處理事件處理之資料列數的目前計數。|  
|ObjectID|11|8|包含與報告事件相關聯的物件識別碼 (字串)。|  
|ObjectType|12|1|包含物件類型。|  
|ObjectName|13|8|包含與報告事件相關聯之物件的名稱。|  
|ObjectPath|14|8|包含與報告事件相關聯之物件的物件路徑，做為以物件的父系開頭之父系清單 (以逗號分隔)。|  
|ObjectReference|15|8|包含報告事件的物件參考，所有父系編碼為 XML，並使用標記來描述物件。|  
|Severity|22|1|包含與報告事件相關聯之例外狀況的嚴重性層級。 值為：<br /><br /> 0 = 成功<br /><br /> 1 = 參考資訊<br /><br /> 2 = 警告<br /><br /> 3 = 錯誤|  
|成功|23|1|包含伺服器報告事件的成功或失敗。 值為：<br /><br /> 0 = 失敗<br /><br /> 1 = 成功|  
|錯誤|24|1|包含給定事件的錯誤號碼。|  
|ConnectionID|25|1|包含與報告事件相關聯的唯一連接識別碼。|  
|DatabaseName|28|8|包含發生報告事件之資料庫的名稱。|  
|NTUserName|32|8|包含與報告事件相關聯的 Windows 使用者帳戶。|  
|NTDomainName|33|8|包含與報告事件相關聯的 Windows 網域帳戶。|  
|SessionID|39|8|包含與報告事件相關聯的工作階段識別碼。|  
|NTCanonicalUserName|40|8|包含與報告事件相關聯的 Windows 使用者名稱。 使用者名稱採用標準格式。 例如，engineering.microsoft.com/software/user。|  
|SPID|41|1|包含伺服器處理序識別碼 (SPID)，它會唯一識別與報告事件相關聯的使用者工作階段。 SPID 直接對應至 XML for Analysis (XMLA) 使用的工作階段 GUID。|  
|TextData|42|9|包含與報告事件相關聯的文字資料。|  
|ServerName|43|8|包含發生報表事件之 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體的名稱。|  
  
## <a name="progress-report-currentdata-columns"></a>目前的進度報表–資料行  
  
|**資料行名稱**|**資料行識別碼**|**資料行類型**|**資料行描述**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件類別用於將事件分類。|  
|EventSubclass|1|1|事件子類別提供有關每個事件類別的額外資訊。 以下是有效的 **子類別識別碼**： **子類別名稱** 組︰<br /><br /> 1︰ **Process**<br /><br /> 2︰ **Merge**<br /><br /> 3︰ **Delete**<br /><br /> 4： **DeleteOldAggregations**<br /><br /> 5： **Rebuild**<br /><br /> 6： **Commit**<br /><br /> 7： **Rollback**<br /><br /> 8： **CreateIndexes**<br /><br /> 9： **CreateTable**<br /><br /> 10： **InsertInto**<br /><br /> 11： **Transaction**<br /><br /> 12： **Initialize**<br /><br /> 13： **Discretize**<br /><br /> 14： **Query**<br /><br /> 15： **CreateView**<br /><br /> 16： **WriteData**<br /><br /> 17： **ReadData**<br /><br /> 18： **GroupData**<br /><br /> 19： **GroupDataRecord**<br /><br /> 20： **BuildIndex**<br /><br /> 21： **Aggregate**<br /><br /> 22： **BuildDecode**<br /><br /> 23： **WriteDecode**<br /><br /> 24： **BuildDMDecode**<br /><br /> 25： **ExecuteSQL**<br /><br /> 26： **ExecuteModifiedSQL**<br /><br /> 27： **Connecting**<br /><br /> 28： **BuildAggsAndIndexes**<br /><br /> 29： **MergeAggsOnDisk**<br /><br /> 30： **BuildIndexForRigidAggs**<br /><br /> 31： **BuildIndexForFlexibleAggs**<br /><br /> 32： **WriteAggsAndIndexes**<br /><br /> 33： **WriteSegment**<br /><br /> 34： **DataMiningProgress**<br /><br /> 35： **ReadBufferFullReport**<br /><br /> 36： **ProactiveCacheConversion**<br /><br /> 37： **Backup**<br /><br /> 38： **Restore**<br /><br /> 39： **Synchronize**<br /><br /> 40： **Build Processing Schedule**<br /><br /> 41： **Detach**<br /><br /> 42： **Attach**<br /><br /> 43： **Analyze\Encode Data**<br /><br /> 44： **Compress Segment**<br /><br /> 45： **Write Table Column**<br /><br /> 46： **Relationship Build Prepare**<br /><br /> 47： **Build Relationship Segment**<br /><br /> 48： **Load**<br /><br /> 49： **Metadata Load**<br /><br /> 50： **Data Load**<br /><br /> 51： **Post Load**<br /><br /> 52： **Metadata traversal during Backup**<br /><br /> 53： **VertiPaq**<br /><br /> 54： **Hierarchy processing**<br /><br /> 55： **Switching dictionary**|  
|CurrentTime|2|5|包含報告事件的目前時間 (如果有的話)。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|StartTime|3|5|包含事件開始的時間 (如果有的話)。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|JobID|7|1|包含與報告事件相關聯的作業識別碼。|  
|SessionType|8|8|包含與報告事件相關聯的工作階段類型 (造成事件的實體)。 針對處理事件，值為：<br /><br /> 1= 使用者<br /><br /> 2= 主動式快取<br /><br /> 3= 延遲處理|  
|ProgressTotal|9|1|包含報告事件的整體進度。|  
|IntegerData|10|1|包含與報告事件相關聯的整數資料，例如針對處理事件處理之資料列數的目前計數。|  
|ObjectID|11|8|包含與報告事件相關聯的物件識別碼 (字串)。|  
|ObjectType|12|1|包含物件類型。|  
|ObjectName|13|8|包含與報告事件相關聯之物件的名稱。|  
|ObjectPath|14|8|包含與報告事件相關聯之物件的物件路徑，做為以物件的父系開頭之父系清單 (以逗號分隔)。|  
|ObjectReference|15|8|包含報告事件的物件參考，所有父系編碼為 XML，並使用標記來描述物件。|  
|ConnectionID|25|1|包含與報告事件相關聯的唯一連接識別碼。|  
|DatabaseName|28|8|包含發生報告事件之資料庫的名稱。|  
|SessionID|39|8|包含與報告事件相關聯的工作階段識別碼。|  
|SPID|41|1|包含伺服器處理序識別碼 (SPID)，它會唯一識別與報告事件相關聯的使用者工作階段。 SPID 直接對應至 XML for Analysis (XMLA) 使用的工作階段 GUID。|  
|TextData|42|9|包含與報告事件相關聯的文字資料。|  
|ServerName|43|8|包含發生報表事件之 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體的名稱。|  
  
## <a name="progress-report-errordata-columns"></a>進度報表錯誤–資料行  
  
|**資料行名稱**|**資料行識別碼**|**資料行類型**|**資料行描述**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件類別用於將事件分類。|  
|EventSubclass|1|1|事件子類別提供有關每個事件類別的額外資訊。 以下是有效的 **子類別識別碼**： **子類別名稱** 組︰<br /><br /> 1︰ **Process**<br /><br /> 2︰ **Merge**<br /><br /> 3︰ **Delete**<br /><br /> 4： **DeleteOldAggregations**<br /><br /> 5： **Rebuild**<br /><br /> 6： **Commit**<br /><br /> 7： **Rollback**<br /><br /> 8： **CreateIndexes**<br /><br /> 9： **CreateTable**<br /><br /> 10： **InsertInto**<br /><br /> 11： **Transaction**<br /><br /> 12： **Initialize**<br /><br /> 13： **Discretize**<br /><br /> 14： **Query**<br /><br /> 15： **CreateView**<br /><br /> 16： **WriteData**<br /><br /> 17： **ReadData**<br /><br /> 18： **GroupData**<br /><br /> 19： **GroupDataRecord**<br /><br /> 20： **BuildIndex**<br /><br /> 21： **Aggregate**<br /><br /> 22： **BuildDecode**<br /><br /> 23： **WriteDecode**<br /><br /> 24： **BuildDMDecode**<br /><br /> 25： **ExecuteSQL**<br /><br /> 26： **ExecuteModifiedSQL**<br /><br /> 27： **Connecting**<br /><br /> 28： **BuildAggsAndIndexes**<br /><br /> 29： **MergeAggsOnDisk**<br /><br /> 30： **BuildIndexForRigidAggs**<br /><br /> 31： **BuildIndexForFlexibleAggs**<br /><br /> 32： **WriteAggsAndIndexes**<br /><br /> 33： **WriteSegment**<br /><br /> 34： **DataMiningProgress**<br /><br /> 35： **ReadBufferFullReport**<br /><br /> 36： **ProactiveCacheConversion**<br /><br /> 37： **Backup**<br /><br /> 38： **Restore**<br /><br /> 39： **Synchronize**<br /><br /> 40： **Build Processing Schedule**<br /><br /> 41： **Detach**<br /><br /> 42： **Attach**<br /><br /> 43： **Analyze\Encode Data**<br /><br /> 44： **Compress Segment**<br /><br /> 45： **Write Table Column**<br /><br /> 46： **Relationship Build Prepare**<br /><br /> 47： **Build Relationship Segment**<br /><br /> 48： **Load**<br /><br /> 49： **Metadata Load**<br /><br /> 50： **Data Load**<br /><br /> 51： **Post Load**<br /><br /> 52： **Metadata traversal during Backup**<br /><br /> 53： **VertiPaq**<br /><br /> 54： **Hierarchy processing**<br /><br /> 55： **Switching dictionary**|  
|CurrentTime|2|5|包含報告事件的目前時間 (如果有的話)。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|StartTime|3|5|包含事件開始的時間 (如果有的話)。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|EndTime|4|5|包含事件結束的時間。 此資料行不會因啟動的事件類別 (如 SQL:BatchStarting 或 SP:Starting) 而擴展。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|有效期間|5|2|包含事件所經歷的時間量 (以毫秒為單位)。|  
|JobID|7|1|包含與報告事件相關聯的作業識別碼。|  
|SessionType|8|8|包含與報告事件相關聯的工作階段類型 (造成事件的實體)。 針對處理事件，值為：<br /><br /> 1= 使用者<br /><br /> 2= 主動式快取<br /><br /> 3= 延遲處理|  
|ProgressTotal|9|1|包含報告事件的整體進度。|  
|IntegerData|10|1|包含與報告事件相關聯的整數資料，例如針對處理事件處理之資料列數的目前計數。|  
|ObjectID|11|8|包含與報告事件相關聯的物件識別碼 (字串)。|  
|ObjectType|12|1|包含物件類型。|  
|ObjectName|13|8|包含與報告事件相關聯之物件的名稱。|  
|ObjectPath|14|8|包含與報告事件相關聯之物件的物件路徑，做為以物件的父系開頭之父系清單 (以逗號分隔)。|  
|ObjectReference|15|8|包含報告事件的物件參考，所有父系編碼為 XML，並使用標記來描述物件。|  
|Severity|22|1|包含與報告事件相關聯之例外狀況的嚴重性層級。 值為：<br /><br /> 0 = 成功<br /><br /> 1 = 參考資訊<br /><br /> 2 = 警告<br /><br /> 3 = 錯誤|  
|錯誤|24|1|包含給定事件的錯誤號碼。|  
|ConnectionID|25|1|包含與報告事件相關聯的唯一連接識別碼。|  
|DatabaseName|28|8|包含發生報告事件之資料庫的名稱。|  
|SessionID|39|8|包含與報告事件相關聯的工作階段識別碼。|  
|SPID|41|1|包含伺服器處理序識別碼 (SPID)，它會唯一識別與報告事件相關聯的使用者工作階段。 SPID 直接對應至 XML for Analysis (XMLA) 使用的工作階段 GUID。|  
|TextData|42|9|包含與報告事件相關聯的文字資料。|  
|ServerName|43|8|包含發生報表事件之 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體的名稱。|  
  
## <a name="see-also"></a>請參閱＜  
 [Progress Reports Event Category](../../analysis-services/trace-events/progress-reports-event-category.md)  
  
  

