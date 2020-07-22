---
title: DBCC (Transact-SQL)
ms.custom: ''
ms.date: 11/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DBCC
- DBCC_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- transactional consistency
- Database Console Command statements
- status information [SQL Server], DBCC statements
- snapshots [SQL Server database snapshots], DBCC statements
- emergency database state [SQL Server]
- TABLOCK
- internal database snapshots [SQL Server]
- reporting DBCC statement progress
- logical consistency of data [SQL Server]
- DBCC statements
- validation statements [SQL Server]
- miscellaneous statements [SQL Server]
- statements [SQL Server], DBCC statements
- DBCC commands [SQL Server]
- result sets [SQL Server], DBCC statements
- maintenance statements [SQL Server]
- physical consistency of data [SQL Server]
- current DBCC statement status
- progress reporting [DBCC statements]
- informational statements [SQL Server]
ms.assetid: c6da8c04-5b6b-459a-9f76-110c92ca8b29
author: pmasl
ms.author: umajay
ms.openlocfilehash: c64938e93401532fd4df7e44af84c86388444277
ms.sourcegitcommit: edba1c570d4d8832502135bef093aac07e156c95
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/20/2020
ms.locfileid: "86484211"
---
# <a name="dbcc-transact-sql"></a>DBCC (Transact-SQL)

[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

[!INCLUDE[tsql](../../includes/tsql-md.md)] 程式設計語言提供可用來作為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫主控台命令的 DBCC 陳述式。
  
資料庫主控台命令陳述式的分組類別目錄如下。
  
|命令類別目錄|執行|  
|---|---|
|維護|維護資料庫、索引或檔案群組的作業。|  
|其他|啟用追蹤旗標或從記憶體中移除 DLL 之類的其他作業。|  
|資訊|收集和顯示各類型資訊的作業。|  
|驗證|資料庫、資料表、索引、目錄、檔案群組或資料庫頁面配置的驗證作業。|  
  
DBCC 命令有輸入參數和傳回值。 所有 DBCC 命令參數都可以接受 Unicode 和 DBCS 常值。
  
## <a name="dbcc-internal-database-snapshot-usage"></a>DBCC 內部資料庫快照集使用方式  
下列 DBCC 命令會在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 所建立的內部唯讀資料庫快照集上運作。 這可以防止在執行這些命令時，發生封鎖和並行問題。 如需詳細資訊，請參閱[資料庫快照集 &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)。
- DBCC CHECKALLOC
- DBCC CHECKCATALOG
- DBCC CHECKDB
- DBCC CHECKFILEGROUP
- DBCC CHECKTABLE

當您執行這些 DBCC 命令時，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 會建立一個資料庫快照集，且會使它進入交易一致狀態。 之後，DBCC 命令會針對這個快照集來進行檢查。 DBCC 命令完成之後，會卸除這個快照集。
  
有時候，並不需要或無法建立內部資料庫快照集。 當這個情況發生時，會針對實際的資料庫來執行 DBCC 命令。 如果資料庫在線上，DBCC 命令會利用資料表鎖定來確保所檢查之物件的一致性。 這個行為與指定了 WITH TABLOCK 選項的情況相同。
  
當在下列情況下執行 DBCC 命令時，不會建立內部資料庫快照集：
-   針對 **master**，且 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體在單一使用者模式執行。  
-   針對 **master** 以外的資料庫，但已利用 ALTER DATABASE 陳述式，使資料庫進入單一使用者模式。  
-   針對唯讀資料庫。  
-   針對已利用 ALTER DATABASE 陳述式，設定為緊急模式的資料庫。  
-   針對 **tempdb**。 在這個情況下，會因為內部限制而無法建立資料庫快照集。  
-   使用 WITH TABLOCK 選項。 在這個情況下，DBCC 會接受要求，不會建立資料庫快照集。  
  
當針對下列項目來執行命令時，DBCC 命令會使用資料表鎖定，而不是內部資料庫快照集：
-   唯讀檔案群組  
-   FAT 檔案系統  
-   不支援「具名資料流」的磁碟區。  
-   不支援「替代資料流」的磁碟區。  
  
> [!NOTE]  
>  試圖利用 WITH TABLOCK 選項來執行 DBCC CHECKALLOC 或 DBCC CHECKDB 的對等部分，需要資料庫 X 鎖定。 這個資料庫鎖定無法在 **tempdb** 或 **master** 上設定，在所有其他資料庫上可能會失敗。  
  
> [!NOTE]  
>  如果無法建立內部資料庫快照集，在針對 **master** 執行 DBCC CHECKDB 時會失敗。  
  
## <a name="progress-reporting-for-dbcc-commands"></a>DBCC 命令的進度報告  
**sys.dm_exec_requests** 目錄檢視包含 DBCC CHECKDB、CHECKFILEGROUP 和 CHECKTABLE 命令的進度和目前執行階段的相關資訊。 **percent_complete** 資料行指出命令的完成比例，**command** 資料行則報告命令目前的執行階段。
  
進度單位的定義會隨著 DBCC 命令目前的執行階段而不同。 有時候，進度會以資料庫頁面的資料粒度來報告；在其他階段，則以單一資料庫或配置修復的資料粒度來報告。 下表描述每個執行階段，以及命令報告進度的資料粒度。
  
|執行階段|描述|進度報告資料粒度|  
|---------------------|-----------------|------------------------------------|  
|DBCC TABLE CHECK|在這個階段中，會檢查資料庫中各物件的邏輯和實體一致性。|資料庫頁面層級所報告的進度。<br /><br /> 每檢查 1000 個資料庫頁面，就會更新進度報告值。|  
|DBCC TABLE REPAIR|如果指定了 REPAIR_FAST、REPAIR_REBUILD 或 REPAIR_ALLOW_DATA_LOSS，而且有必須加以修復的物件錯誤，就會在這個階段期間執行資料庫修復。|個別修復層級所報告的進度。<br /><br /> 每次修復完成，就會更新計數器。|  
|DBCC ALLOC CHECK|在這個階段期間，會檢查資料庫中的配置結構。<br /><br /> 注意:DBCC CHECKALLOC 會執行相同的檢查。|不報告進度|  
|DBCC ALLOC REPAIR|如果指定了 REPAIR_FAST、REPAIR_REBUILD 或 REPAIR_ALLOW_DATA_LOSS，而且有必須加以修復的配置錯誤，就會在這個階段期間執行資料庫修復。|不報告進度。|  
|DBCC SYS CHECK|在這個階段期間，會檢查資料庫系統資料表。|資料庫頁面層級所報告的進度。<br /><br /> 每檢查 1000 個資料庫頁面，就會更新進度報告值。|  
|DBCC SYS REPAIR|如果指定了 REPAIR_FAST、REPAIR_REBUILD 或 REPAIR_ALLOW_DATA_LOSS，而且有必須加以修復的系統資料表錯誤，就會在這個階段期間執行資料庫修復。|個別修復層級所報告的進度。<br /><br /> 每次修復完成，就會更新計數器。|  
|DBCC SSB CHECK|在這個階段期間，會檢查 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Service Broker 物件。<br /><br /> 注意:當執行 DBCC CHECKTABLE 時，不會執行這個階段。|不報告進度。|  
|DBCC CHECKCATALOG|在這個階段期間，會檢查資料庫目錄的一致性。<br /><br /> 注意:當執行 DBCC CHECKTABLE 時，不會執行這個階段。|不報告進度。|  
|DBCC IVIEW CHECK|在這個階段中，會檢查資料庫中任何索引檢視的邏輯一致性。|在所檢查的個別資料庫檢視層級報告的進度。|  
  
## <a name="informational-statements"></a>資訊陳述式  

- [DBCC INPUTBUFFER](../../t-sql/database-console-commands/dbcc-inputbuffer-transact-sql.md)
- [DBCC SHOWCONTIG](../../t-sql/database-console-commands/dbcc-showcontig-transact-sql.md)
- [DBCC OPENTRAN](../../t-sql/database-console-commands/dbcc-opentran-transact-sql.md)
- [DBCC OUTPUTBUFFER](../../t-sql/database-console-commands/dbcc-outputbuffer-transact-sql.md)
- [DBCC PROCCACHE](../../t-sql/database-console-commands/dbcc-proccache-transact-sql.md)
- [DBCC SHOW_STATISTICS](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)
- [DBCC SQLPERF](../../t-sql/database-console-commands/dbcc-sqlperf-transact-sql.md)
- [DBCC TRACESTATUS](../../t-sql/database-console-commands/dbcc-tracestatus-transact-sql.md)
- [DBCC USEROPTIONS](../../t-sql/database-console-commands/dbcc-useroptions-transact-sql.md)
  
## <a name="validation-statements"></a>驗證陳述式  

- [DBCC CHECKALLOC](../../t-sql/database-console-commands/dbcc-checkalloc-transact-sql.md)
- [DBCC CHECKCATALOG](../../t-sql/database-console-commands/dbcc-checkcatalog-transact-sql.md)
- [DBCC CHECKCONSTRAINTS](../../t-sql/database-console-commands/dbcc-checkconstraints-transact-sql.md)
- [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)
- [DBCC CHECKFILEGROUP](../../t-sql/database-console-commands/dbcc-checkfilegroup-transact-sql.md)
- [DBCC CHECKIDENT](../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md)
- [DBCC CHECKTABLE](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md)
  
## <a name="maintenance-statements"></a>維護陳述式  

- [DBCC CLEANTABLE](../../t-sql/database-console-commands/dbcc-cleantable-transact-sql.md)
- [DBCC DBREINDEX](../../t-sql/database-console-commands/dbcc-dbreindex-transact-sql.md)
- [DBCC DROPCLEANBUFFERS](../../t-sql/database-console-commands/dbcc-dropcleanbuffers-transact-sql.md)
- [DBCC FREEPROCCACHE](../../t-sql/database-console-commands/dbcc-freeproccache-transact-sql.md)
- [DBCC INDEXDEFRAG](../../t-sql/database-console-commands/dbcc-indexdefrag-transact-sql.md)
- [DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md)
- [DBCC SHRINKFILE](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md)
- [DBCC UPDATEUSAGE](../../t-sql/database-console-commands/dbcc-updateusage-transact-sql.md)  

## <a name="miscellaneous-statements"></a>其他陳述式  

- [DBCC dllname (FREE)](../../t-sql/database-console-commands/dbcc-dllname-free-transact-sql.md)
- [DBCC HELP](../../t-sql/database-console-commands/dbcc-help-transact-sql.md)
- [DBCC FLUSHAUTHCACHE](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md)
- [DBCC TRACEOFF](../../t-sql/database-console-commands/dbcc-traceoff-transact-sql.md)
- [DBCC FREESESSIONCACHE](../../t-sql/database-console-commands/dbcc-freesessioncache-transact-sql.md)
- [DBCC TRACEON](../../t-sql/database-console-commands/dbcc-traceon-transact-sql.md)
- [DBCC FREESYSTEMCACHE](../../t-sql/database-console-commands/dbcc-freesystemcache-transact-sql.md)
- [DBCC CLONEDATABASE](../../t-sql/database-console-commands/dbcc-clonedatabase-transact-sql.md) <br /><br /> **適用於**：[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 及更新版本。
