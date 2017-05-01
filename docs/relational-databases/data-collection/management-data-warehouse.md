---
title: "管理資料倉儲 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data collector [SQL Server], management data warehouse
- data warehouse
- management data warehouse
ms.assetid: 9874a8b2-7ccd-494a-944c-ad33b30b5499
caps.latest.revision: 43
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0430b88308cb3ebc07b1addfb2e34575150fa41e
ms.lasthandoff: 04/11/2017

---
# <a name="management-data-warehouse"></a>管理資料倉儲
  管理資料倉儲是一種關聯式資料庫，其中包含從伺服器 (它是資料收集目標) 收集而來的資料。 這項資料是用來產生系統資料收集組的報表，而且也可用來建立自訂報表。  
  
 資料收集器基礎結構會定義實作資料庫管理員所定義之保留原則所需的作業和維護計畫。  
  
> [!IMPORTANT]  
>  在這一版的資料收集器中，會使用簡單復原模式建立管理資料倉儲，使記錄量降到最小。 您應該實作適合於組織的復原模式。  
  
## <a name="deploying-and-using-the-data-warehouse"></a>部署及使用資料倉儲  
 您可以將這個管理資料倉儲安裝在執行資料收集器的相同 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上。 但是，如果所監視的伺服器上有伺服器資源或效能的問題，您可以將管理資料倉儲安裝在另一部電腦上。  
  
 當您建立管理資料倉儲時，將會針對預先定義的系統收集組建立必要的結構描述及其物件。 所建立的結構描述包括核心和快照集。第三個結構描述 custom_snapshots 是在建立使用者定義的收集組 (其中包含使用一般 T-SQL 收集器型別的收集項) 時建立。  
  
###### <a name="core-schema"></a>核心結構描述  
 核心結構描述會描述用來組織及識別所收集之資料的資料表、預存程序和檢視表。 這些資料表會在針對個別收集器型別建立的所有資料表之間共用。 這個結構描述已經鎖定，只有管理資料倉儲資料庫的擁有者才可以修改。 此結構描述中的資料表名稱會有 "core" 的前置詞。  
  
 下表描述核心結構描述中的資料庫資料表。 這些資料庫資料表可讓資料收集器追蹤資料的來源、繼承者，以及何時將資料上傳到資料倉儲。  
  
|資料表名稱|描述|  
|----------------|-----------------|  
|core.performance_counter_report_group_items|儲存有關管理資料倉儲報表應該如何群組和彙總效能計數器的資訊。|  
|core.snapshots_internal|識別每個新的快照集。 每當上傳封裝開始上傳新的資料批次時，就會在這個資料表中插入新的資料列。|  
|core.snapshot_timetable_internal|儲存有關快照集時間的資訊。 快照集時間會儲存在個別的資料表中，因為許多快照集可以幾乎發生在相同的時間。|  
|core.source.info_internal|此資料表會儲存有關資料來源的資訊。 每當新的收集組開始上傳資料到資料倉儲時，就會更新這個資料表。|  
|core.supported_collector_types_internal|包含可以上傳資料到管理資料倉儲之已註冊收集器型別的識別碼。 只有當更新倉儲的結構描述來支援新的收集器型別時，才會更新這個資料表。 當建立管理資料倉儲時，這個資料表中會填入資料收集器所提供之收集器型別的識別碼。|  
|core.wait_categories|包含用來根據 wait_type 特性分組等候類型的類別。|  
|core.wait_types|包含資料收集器所辨識的等候類型。|  
|core.purge_info_internal|表示已經發出要求來停止從管理資料倉儲中移除資料的作業。|  
  
 以上資料表會搭配收集器型別資料表一起使用，以便儲存資訊。 例如，一般 SQL 追蹤收集器型別會使用以下資料表來儲存追蹤資料：  
  
-   core.source_info_internal  
  
-   core.snapshots_internal  
  
-   snapshots.trace_info  
  
-   snapshots.trace_data  
  
###### <a name="snapshots-schema"></a>快照集結構描述  
 快照集結構描述會描述用來儲存及維護資料所需的物件 (這些資料是由提供的收集器型別所收集而來)。 此結構描述中的資料表是固定的，在收集器型別的存留期間不需要變更。 如果需要變更，只有 mdw_admin 角色的成員才可以變更此結構描述。 建立這些資料表是為了儲存系統資料收集組所收集的資料。  
  
 下表說明伺服器活動和查詢統計資料收集組所需的管理資料倉儲結構描述部分。  
  
-   系統層級的資源資料表  
  
    -   **snapshots.os_wait_stats**  
  
    -   **snapshots.os_latch_stats**  
  
    -   **snapshots.os_schedulers**  
  
    -   **snapshots.os_memory_clerks**  
  
    -   **snapshots.os_memory_nodes**  
  
    -   snapshots.sql_process_and_system_memory  
  
-   系統活動  
  
    -   snapshots.active_sessions_and_requests  
  
-   查詢統計資料  
  
    -   snapshots.query_stats  
  
-   I/O 統計資料  
  
    -   **snapshots.io_virtual_file_stats**  
  
-   查詢文字和計畫  
  
    -   snapshots.notable_query_text  
  
    -   snapshots.notable_query_plan  
  
-   正規化的查詢統計資料  
  
    -   snapshots.distinct_queries  
  
    -   snapshots.distinct_query_to_handle  
  
 **Custom_snapshots 結構描述**  
  
 custom_snapshots 結構描述會描述當使用標準或協力廠商收集器型別來建立使用者定義的收集組時，所建立的新資料表和檢視表。 任何需要收集項之新資料表的收集器型別都可以在這個結構描述中建立該資料表。 mdw_writer 角色的成員可以在這個結構描述中加入新的資料表。 只有 mdw_admin 角色的成員才可以對此結構描述進行其他任何變更。  
  
 如果要取得資料庫資料表資料行的詳細資料類型和內容資訊，請讀取每一個資料表適合之資料收集器預存程序的文件集。  
  
### <a name="best-practices"></a>最佳作法  
 當使用管理資料倉儲時，我們建議您遵循以下最佳作法：  
  
-   請勿修改管理資料倉儲資料表的中繼資料，除非您要加入新的收集器型別。  
  
-   請勿在管理資料倉儲中直接修改資料。 變更您收集的資料會讓收集的資料變成無效。  
  
-   請勿直接使用資料表，而是要使用資料收集器所提供之記載的預存程序和函數，以存取執行個體和應用程式資料。 資料表名稱和定義可以變更，在您更新應用程式時也確實會變更，也可能在未來版本中變更。  
  
## <a name="change-history"></a>變更記錄  
  
|更新的內容|  
|---------------------|  
|在「核心結構描述」一節中，新增 core.performance_counter_report_group_items 資料表。|  
|在「快照集結構描述」一節中，更新資料表的清單。 新增 snapshots.os_memory_clerks、snapshots.sql_process_and_system_memory 和 snapshots.io_virtual_file_stats。 移除 snapshots.os_process_memory 和 snapshots.distinct_query_stats。|  
  
## <a name="see-also"></a>另請參閱  
 [管理資料倉儲預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/management-data-warehouse-stored-procedures-transact-sql.md)   
 [資料收集器預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [資料收集](../../relational-databases/data-collection/data-collection.md)   
 [檢視收集組報表 &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/view-a-collection-set-report-sql-server-management-studio.md)  
  
  
