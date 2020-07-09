---
title: DBCC SHRINKFILE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SHRINKFILE
- DBCC_SHRINKFILE_TSQL
- DBCC SHRINKFILE
- SHRINKFILE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- data shrinking [SQL Server]
- TRUNCATEONLY option
- shrinking files
- NOTRUNCATE option
- shrinking databases
- decreasing database size
- file shrinking [SQL Server]
- database shrinking [SQL Server]
- logs [SQL Server], shrinking
- reducing database size
- DBCC SHRINKFILE statement
ms.assetid: e02b2318-bee9-4d84-a61f-2fddcf268c9f
author: pmasl
ms.author: umajay
ms.openlocfilehash: a9498c5d2705abece345533573a768e71e0b7030
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85748900"
---
# <a name="dbcc-shrinkfile-transact-sql"></a>DBCC SHRINKFILE (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

壓縮目前資料庫的指定資料或記錄檔大小。 您可以使用它將資料從某個檔案移至同一檔案群組中的其他檔案，其可清空檔案並允許移除其資料庫。 您可以將檔案壓縮成小於其在建立時的大小，將檔案大小下限重設為新值。
  
![文章連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```syntaxsql
  
DBCC SHRINKFILE   
(  
    { file_name | file_id }   
    { [ , EMPTYFILE ]   
    | [ [ , target_size ] [ , { NOTRUNCATE | TRUNCATEONLY } ] ]  
    }  
)  
[ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>引數  
*file_name*  
所要壓縮檔案的邏輯名稱。
  
*file_id*  
所要壓縮檔案的識別碼 (ID)。 若要取得檔案識別碼，請使用 [FILE_IDEX](../../t-sql/functions/file-idex-transact-sql.md) 系統函數或在目前的資料庫中查詢 [sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md) 目錄檢視。
  
*target_size*  
整數 - 檔案的新 MB 大小。 若未指定，DBCC SHRINKFILE 會縮減成檔案建立大小。
  
> [!NOTE]  
>  您可以使用 DBCC SHRINKFILE *target_size* 縮減空白檔案的預設大小。 例如，如果建立 5 MB 的檔案，然後再將檔案縮減為 3 MB 且檔案仍維持空白，則預設的檔案大小會設定為 3 MB。 這僅適用於從未包含過資料的空白檔案。  
  
FILESTREAM 檔案群組容器不支援此選項。  
如果已指定，DBCC SHRINKFILE 會嘗試將檔案壓縮成 *target_size*。 檔案所要釋出區域中所使用頁面會移至檔案保留區域中的可用空間。 例如，有 10 MB 的資料檔案時，*target_size* 為 8 的 DBCC SHRINKFILE 作業會將檔案最後 2 MB 中所有已使用頁面移入檔案前 8 MB 中任何未配置的頁面。 DBCC SHRINKFILE 不會將檔案壓縮成超過所需的預存資料大小。 例如，如果使用了 10 MB 資料檔案中的 7 MB，將 *target_size* 設為 6 的 DBCC SHRINKFILE 陳述式，只會將檔案壓縮成 7 MB，而不是 6 MB。
  
EMPTYFILE  
將指定檔案中的所有資料移轉到「相同檔案群組」  的其他檔案中。 換言之，EMPTYFILE 會將指定檔案中資料移轉至同一檔案群組中的其他檔案。 儘管這不是唯讀檔案，但 EMPTYFILE 可確保不會將任何新資料新增至檔案。 您可以使用 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) 陳述式來移除檔案。 如果您使用 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) 陳述式來變更檔案大小，則唯讀旗標會重設，且可以新增資料。

對於 FILESTREAM 檔案群組容器來說，在 FILESTREAM 記憶體回收行程已執行並刪除所有由 EMPTYFILE 複製至其他容器且已不需要的檔案群組容器檔案之前，您無法使用 ALTER DATABASE 來移除檔案。 如需詳細資訊，請參閱 [sp_filestream_force_garbage_collection &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-filestream-force-garbage-collection.md)
  
> [!NOTE]  
>  如需移除 FILESTREAM 容器的詳細資訊，請參閱 [ALTER DATABASE 檔案及檔案群組選項 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)中對應的章節。  
  
NOTRUNCATE  
在有指定或未指定 *target_percent* 的情況下，將所配置頁面從資料檔案結尾移到檔案前面未配置的頁面。 檔案結尾的可用空間並不會歸還給作業系統，檔案的實際大小也不會改變。 因此，如果指定了 NOTRUNCATE，檔案不會呈現壓縮狀態。
NOTRUNCATE 只適用於資料檔案。 記錄檔不受影響。   FILESTREAM 檔案群組容器不支援此選項。
  
TRUNCATEONLY  
將檔案結尾的所有可用空間釋出給作業系統，但是不會在檔案內移動任何頁面。 資料檔案只會壓縮為最後配置的範圍。
如果在使用 TRUNCATEONLY 時指定 *target_size*，則會予以忽略。  
TRUNCATEONLY 選項不會移動記錄檔中的資訊，但會移除記錄檔結尾之非使用中的 VLF。 FILESTREAM 檔案群組容器不支援此選項。
  
WITH NO_INFOMSGS  
隱藏所有參考訊息。
  
## <a name="result-sets"></a>結果集  
下表會描述結果集資料行。
  
|資料行名稱|描述|  
|---|---|
|**DbId**|[!INCLUDE[ssDE](../../includes/ssde-md.md)] 試圖壓縮之檔案的資料庫識別碼。|  
|**FileId**|[!INCLUDE[ssDE](../../includes/ssde-md.md)] 試圖壓縮之檔案的檔案識別碼。|  
|**CurrentSize**|檔案目前所佔的 8 KB 頁數。|  
|**MinimumSize**|檔案所能佔用的 8 KB 頁數最小值。 此數字對應於檔案大小下限或最初建立的大小。|  
|**UsedPages**|檔案目前所用的 8 KB 頁數。|  
|**EstimatedPages**|[!INCLUDE[ssDE](../../includes/ssde-md.md)] 估計檔案可以壓縮成 8 KB 頁面的數目。|  
  
## <a name="remarks"></a>備註  
DBCC SHRINKFILE 適用於目前資料庫的檔案。 如需有關如何變更目前資料庫的詳細資訊，請參閱 [USE &#40;Transact-SQL&#41;](../../t-sql/language-elements/use-transact-sql.md)。
  
您可以隨時停止 DBCC SHRINKFILE 作業，任何已完成的工作都會保留下來。 如果您使用 EMPTYFILE 參數並取消作業，則不會標示檔案來防止新增額外的資料。
  
當 DBCC SHRINKFILE 作業失敗時，會引發錯誤。
  
 在檔案壓縮期間，其他使用者可以在資料庫中工作，資料庫不一定要處於單一使用者模式。 您不需要在單一使用者模式中執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體來壓縮系統資料庫。  
  
## <a name="shrinking-a-log-file"></a>壓縮記錄檔  

對於記錄檔，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 會使用 *target_size* 來計算整份記錄的目標大小。 因此，*target_size* 是壓縮作業之後的記錄檔可用空間。 之後，便會將整份記錄之目標大小轉換成每個記錄檔的目標大小。 DBCC SHRINKFILE 會試圖將每個實體記錄檔立即壓縮成目標大小。 不過，如果邏輯記錄有任何部分是在超出目標大小的虛擬記錄中，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 盡可能釋出的空間，然後發出一則參考用訊息。 這個訊息描述將邏輯記錄移出檔案結尾的虛擬記錄，需要哪些動作。 執行這些動作之後，就可以利用 DBCC SHRINKFILE 來釋出其餘空間。
  
由於記錄檔只能壓縮成虛擬記錄檔界限，因此可能無法將記錄檔壓縮成小於虛擬記錄檔的大小，即使它不在使用中也是如此。 建立或擴充記錄檔時，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 會以動態方式選擇虛擬記錄檔大小。
  
## <a name="best-practices"></a>最佳作法 
 
當您計畫壓縮檔案時，請考量下列資訊：
-   壓縮作業在截斷資料表或卸除資料表作業等建立大量未用空間的作業之後最有效。  

-   大部分資料庫都需要一些可用空間來執行每天的例行作業。 如果您反覆壓縮資料庫，且其大小再次增加，就表示例行作業需要被壓縮的空間。 在這些情況之下，反覆壓縮資料庫是一項會造成浪費的作業。  

-   壓縮作業不會保留資料庫中索引的片段狀態，它通常會使片段增加到某個程度。 此片段就是不要反覆壓縮資料庫的另一個原因。  

-   循序而不是同時壓縮相同資料庫中的多個檔案。 系統資料表上的競爭可能會造成封鎖，因而導致延遲。  
  
## <a name="troubleshooting"></a>疑難排解  
此章節描述如何診斷和更正在執行 DBCC SHRINKFILE 命令時可能發生的問題。
  
### <a name="the-file-doesnt-shrink"></a>檔案未壓縮
  
如果在無錯誤壓縮作業之後檔案大小不會變更，請嘗試下列命令來確認檔案具有足夠的可用空間：

- 執行下列查詢。  
  
```sql
SELECT name ,size/128.0 - CAST(FILEPROPERTY(name, 'SpaceUsed') AS int)/128.0 AS AvailableSpaceInMB
FROM sys.database_files;
```

-   執行 [DBCC SQLPERF](../../t-sql/database-console-commands/dbcc-sqlperf-transact-sql.md) 命令會傳回交易記錄中所使用的空間。  

如果可用的空間不足，壓縮作業無法更進一步地縮減檔案大小。
  
一般而言，呈現未壓縮狀態的都是記錄檔。 這種未壓縮狀態通常是因為記錄檔未遭截斷而造成。 若要截斷記錄檔，您可以將資料庫復原模式設定為 SIMPLE，或先備份記錄檔，然後再次執行 DBCC SHRINKFILE 作業。
  
### <a name="the-shrink-operation-is-blocked"></a>壓縮作業遭到封鎖  

在[以資料列版本設定為基礎的隔離等級](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)下執行的交易可以封鎖壓縮作業。 例如，當 DBCC SHRINK DATABASE 作業執行時，如果正在以資料列版本設定為基礎的隔離等級下進行大量刪除作業，則壓縮作業將會等到刪除作業完成之後，才會開始壓縮檔案。 當這種封鎖情況發生時，DBCC SHRINKFILE 和 DBCC SHRINKDATABASE 作業會列印資訊訊息 (SHRINKDATABASE 是 5202，SHRINKFILE 是 5203) 到 SQL Server 錯誤記錄檔中。 此訊息在第一個小時內每隔五分鐘記錄一次，然後每隔一小時記錄一次。 例如，如果錯誤記錄檔包含下列錯誤訊息，就會發生下列錯誤：
  
```sql
DBCC SHRINKFILE for file ID 1 is waiting for the snapshot   
transaction with timestamp 15 and other snapshot transactions linked to   
timestamp 15 or with timestamps older than 109 to finish.  
```  
  
此訊息表示時間戳記在 109 (壓縮作業所完成的最後一項交易) 之前的快照集交易將封鎖壓縮作業。 這也表示 **sys.dm_tran_active_snapshot_database_transactions** 動態管理檢視中的 **transaction_sequence_num** 或 [first_snapshot_sequence_num](../../relational-databases/system-dynamic-management-views/sys-dm-tran-active-snapshot-database-transactions-transact-sql.md) 資料行包含值 15。 如果 **transaction_sequence_num** 或 **first_snapshot_sequence_num** 檢視資料行所包含數字小於壓縮作業最後完成的交易 (109)，壓縮作業將會等到這些交易完成。
  
若要解決這個問題，可以執行下列其中一項工作：
-   結束正在封鎖壓縮作業的交易。
-   結束壓縮作業。 如果壓縮作業結束，則所有已完成的工作都會保留下來。  
-   不執行任何動作，並允許壓縮作業等到封鎖交易完成。  
  
## <a name="permissions"></a>權限  
需要 **系統管理員** 固定伺服器角色或 **db_owner** 固定資料庫角色中的成員資格。
  
## <a name="examples"></a>範例  
  
### <a name="shrinking-a-data-file-to-a-specified-target-size"></a>將資料檔案壓縮為指定的目標大小  
下列範例會將 `DataFile1` 使用者資料庫中名為 `UserDB` 之資料檔案大小壓縮成 7 MB。
  
```sql  
USE UserDB;  
GO  
DBCC SHRINKFILE (DataFile1, 7);  
GO  
```  
  
### <a name="shrinking-a-log-file-to-a-specified-target-size"></a>將記錄檔壓縮為指定的目標大小  
下列範例會將 `AdventureWorks` 資料庫中的記錄檔壓縮成 1 MB。 若要讓 DBCC SHRINKFILE 命令可以壓縮檔案，必須先將資料庫復原模式設定為 SIMPLE 以截斷檔案。
  
```sql  
USE AdventureWorks2012;  
GO  
-- Truncate the log by changing the database recovery model to SIMPLE.  
ALTER DATABASE AdventureWorks2012  
SET RECOVERY SIMPLE;  
GO  
-- Shrink the truncated log file to 1 MB.  
DBCC SHRINKFILE (AdventureWorks2012_Log, 1);  
GO  
-- Reset the database recovery model.  
ALTER DATABASE AdventureWorks2012  
SET RECOVERY FULL;  
GO  
```  
  
### <a name="c-truncating-a-data-file"></a>C. 截斷資料檔案  
下列範例會截斷 `AdventureWorks` 資料庫中的主要資料檔案， 並查詢 `sys.database_files` 目錄檢視以取得資料檔案的 `file_id`。
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT file_id, name  
FROM sys.database_files;  
GO  
DBCC SHRINKFILE (1, TRUNCATEONLY);  
```  
  
### <a name="d-emptying-a-file"></a>D. 清除檔案  
下列範例示範如何清空檔案，使其能夠從資料庫中移除。 基於此範例的目的，會先建立資料檔案並包含資料。
  
```sql  
USE AdventureWorks2012;  
GO  
-- Create a data file and assume it contains data.  
ALTER DATABASE AdventureWorks2012   
ADD FILE (  
    NAME = Test1data,  
    FILENAME = 'C:\t1data.ndf',  
    SIZE = 5MB  
    );  
GO  
-- Empty the data file.  
DBCC SHRINKFILE (Test1data, EMPTYFILE);  
GO  
-- Remove the data file from the database.  
ALTER DATABASE AdventureWorks2012  
REMOVE FILE Test1data;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
[ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DBCC SHRINKDATABASE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md)  
[FILE_ID &#40;Transact-SQL&#41;](../../t-sql/functions/file-id-transact-sql.md)  
[sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)  
[壓縮檔案](../../relational-databases/databases/shrink-a-file.md)
  
  
