---
title: "DBCC SHRINKFILE (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 87
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 14746a5bfac3674299e03b6eba0da1a823f1bba9
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-shrinkfile-transact-sql"></a>DBCC SHRINKFILE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

壓縮目前資料庫之指定資料或記錄檔的大小，或藉由將資料從指定檔案移到同一檔案群組中的其他檔案的方式來清除檔案 (讓檔案可以從資料庫中移除)。 檔案可以壓縮成小於當初建立時所指定的大小。 這會將檔案大小下限重設為新值。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
  
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
這是要壓縮之檔案的邏輯名稱。
  
*file_id*  
這是要壓縮之檔案的識別碼 (ID)。 若要取得檔案識別碼，請使用[FILE_IDEX](../../t-sql/functions/file-idex-transact-sql.md)系統函式或查詢[sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)目錄檢視中目前的資料庫。
  
*target_size*  
這是檔案的大小 (MB)，以整數表示。 若未指定，DBCC SHRINKFILE 會將大小縮減成預設檔案大小。 預設的大小是在建立檔案時所指定的大小。
  
> [!NOTE]  
>  您也可以使用 DBCC SHRINKFILE 來減少 「 空白檔案的預設大小*target_size*。 例如，如果建立 5 MB 的檔案，然後再將檔案縮減為 3 MB 且檔案仍維持空白，則預設的檔案大小會設定為 3 MB。 這僅適用於從未包含過資料的空白檔案。  
  
FILESTREAM 檔案群組容器不支援此選項。  
如果*target_size*指定，則 DBCC SHRINKFILE 會嘗試將檔案壓縮成指定的大小。 檔案將釋出之部分所用的頁面，重新放置到檔案保留部分的可用空間中。 例如，如果有 10 MB 的資料檔案，DBCC SHRINKFILE 作業*target_size* 8 原因的所有頁面中使用的檔案最後 2 MB 都重新配置到任何未配置的頁面中的檔案前 8 MB。 DBCC SHRINKFILE 不會將檔案壓縮到小於將資料儲存在檔案中所需要的大小。 例如，如果使用 10 MB 的資料檔案中的 7 MB 時，DBCC SHRINKFILE 陳述式*target_size* 6 之會將檔案縮小僅 7 MB，而不是 6 MB。
  
EMPTYFILE  
將所有資料從指定的檔案都移轉到其他檔案中**相同的檔案群組**。 換句話說，EmptyFile 將資料移轉從指定的檔案至相同的檔案群組中的其他檔案。 Emptyfile 可確保任何新的資料將會加入檔案。會移除檔案，請使用[ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md)陳述式。
對於 FILESTREAM 檔案群組容器來說，在 FILESTREAM 記憶體回收行程已執行並刪除所有由 EMPTYFILE 複製至其他容器且已不需要的檔案群組容器檔案之前，檔案將無法使用 ALTER DATABASE 移除。 如需詳細資訊，請參閱[s &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-filestream-force-garbage-collection.md)
  
> [!NOTE]  
>  如需有關移除 FILESTREAM 容器的資訊，請參閱中對應的章節[ALTER DATABASE 檔案及檔案群組選項 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)  
  
NOTRUNCATE  
將配置的頁面從資料檔案的結尾或不指定到檔案前面未配置的頁面來*target_percent*。 檔案結尾的可用空間並不會還給作業系統，檔案的實際大小也不會改變。 因此，當指定了 NOTRUNCATE 時，檔案不會呈現壓縮狀態。
NOTRUNCATE 只適用於資料檔案。 記錄檔不受影響。   FILESTREAM 檔案群組容器不支援此選項。
  
TRUNCATEONLY  
將檔案結尾的所有可用空間釋放給作業系統，但是不會在檔案內移動任何頁面。 資料檔案只會壓縮為最後配置的範圍。
*target_size*如果指定了 truncateonly，便會被忽略。  
TRUNCATEONLY 選項不會移動記錄檔中的資訊，但會移除記錄檔結尾之非使用中的 VLF。 FILESTREAM 檔案群組容器不支援此選項。
  
WITH NO_INFOMSGS  
隱藏所有參考訊息。
  
## <a name="result-sets"></a>結果集  
下表描述結果集中的資料行。
  
|資料行名稱|Description|  
|---|---|
|**DbId**|[!INCLUDE[ssDE](../../includes/ssde-md.md)] 試圖壓縮之檔案的資料庫識別碼。|  
|**FileId**|[!INCLUDE[ssDE](../../includes/ssde-md.md)] 試圖壓縮之檔案的檔案識別碼。|  
|**CurrentSize**|檔案目前所佔的 8 KB 頁數。|  
|**MinimumSize**|檔案所能佔用的 8 KB 頁數最小值。 這對應於檔案的大小下限或最初建立的大小。|  
|**UsedPages**|檔案目前所用的 8 KB 頁數。|  
|**EstimatedPages**|[!INCLUDE[ssDE](../../includes/ssde-md.md)] 估計檔案可以壓縮成 8 KB 頁面的數目。|  
  
## <a name="remarks"></a>備註  
DBCC SHRINKFILE 適用於目前資料庫中的檔案。 如需如何變更目前資料庫的詳細資訊，請參閱[使用 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/use-transact-sql.md).
  
在這個處理序中，隨時可以停止 DBCC SHRINKFILE 作業，任何已完成的工作都會保留下來。
  
當 DBCC SHRINKFILE 作業失敗時，會引發錯誤。
  
 壓縮的資料庫不必是單一使用者模式；在檔案壓縮之後，其他使用者也可以在這個資料庫中工作。 您不需要在單一使用者模式中執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，來壓縮系統資料庫。  
  
## <a name="shrinking-a-log-file"></a>壓縮記錄檔  
針對記錄檔，[!INCLUDE[ssDE](../../includes/ssde-md.md)]使用*target_size*計算目標大小，整份記錄中; 因此， *target_size*是壓縮作業後的記錄檔中的可用空間量。 之後，便會將整份記錄的目標大小轉換成每個記錄檔的目標大小。 DBCC SHRINKFILE 會試圖將每個實體記錄檔立即壓縮成目標大小。 不過，如果邏輯記錄有任何部分是在超出目標大小的虛擬記錄中，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 盡可能釋出的空間，然後發出一則參考用訊息。 這個訊息描述將邏輯記錄移出檔案結尾的虛擬記錄，需要哪些動作。 執行這些動作之後，就可以利用 DBCC SHRINKFILE 來釋出其餘空間。
  
由於記錄檔只能壓縮成虛擬記錄檔界限，因此，可能無法將記錄檔壓縮成小於虛擬記錄檔的大小，即使它不在使用中，也是如此。 建立或擴充記錄檔時，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 會動態選擇虛擬記錄檔的大小。
  
## <a name="best-practices"></a>最佳作法  
當您計畫壓縮檔案時，請考量下列資訊：
-   壓縮作業在截斷資料表或卸除資料表等產生大量未用空間的作業之後最有效。  
-   大部分資料庫都需要一些可用空間來執行每天的例行作業。 如果您反覆壓縮資料庫，發現資料庫再次增長，就表示例行作業需要被壓縮的空間。 在這些情況之下，反覆壓縮資料庫是一項會造成浪費的作業。  
-   壓縮作業不會保留資料庫中索引的片段狀態，它通常會使片段增加到某個程度。 這就是不要反覆壓縮資料庫的另一個原因。  
-   循序而不是同時壓縮相同資料庫中的多個檔案。 系統資料表上的競爭可能因封鎖而造成延遲。  
  
## <a name="troubleshooting"></a>疑難排解  
此章節描述如何診斷和更正在執行 DBCC SHRINKFILE 命令時可能發生的問題。
  
### <a name="the-file-does-not-shrink"></a>檔案無法壓縮  
如果壓縮作業並未發生錯誤，但檔案並未呈現出大小變更的狀態，請執行下列其中一項作業來確認檔案具有足夠的可用空間可以移除：
- 執行下列查詢。  
  
```sql
SELECT name ,size/128.0 - CAST(FILEPROPERTY(name, 'SpaceUsed') AS int)/128.0 AS AvailableSpaceInMB
FROM sys.database_files;
```

-   執行[DBCC SQLPERF](../../t-sql/database-console-commands/dbcc-sqlperf-transact-sql.md)命令傳回交易記錄檔中使用的空間。  
如果可用的空間不足，壓縮作業無法更進一步地縮減檔案大小。
  
一般而言，呈現未壓縮狀態的都是記錄檔。 這通常是因為記錄檔未遭截斷而造成。 您可以藉由下列方式截斷記錄檔：將資料庫復原模式設定為 SIMPLE，或者先備份記錄檔，然後再執行 DBCC SHRINKFILE 作業一次。
  
### <a name="the-shrink-operation-is-blocked"></a>壓縮作業遭到封鎖  
封鎖交易下執行壓縮作業可能會[資料列版本設定為基礎的隔離等級](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)。 例如，當 DBCC SHRINK DATABASE 作業執行時，如果以資料列版本設定為基礎的隔離等級之下正在進行大量刪除作業，則壓縮作業將會等到刪除作業完成之後，才會開始壓縮檔案。 當這種情況發生時，DBCC SHRINKFILE 和 DBCC SHRINKDATABASE 作業在第一個小時裡，會每五分鐘列印一次參考用訊息 (SHRINKDATABASE 是 5202，SHRINKFILE 是 5203) 到 SQL Server 錯誤記錄檔中，之後則每小時列印一次。 例如，如果錯誤記錄檔包含下列錯誤訊息，就會發生下列錯誤：
  
```sql
DBCC SHRINKFILE for file ID 1 is waiting for the snapshot   
transaction with timestamp 15 and other snapshot transactions linked to   
timestamp 15 or with timestamps older than 109 to finish.  
```  
  
這表示壓縮作業是由時間戳記在 109 (壓縮作業所完成的最後一項交易) 之前的快照集交易所封鎖。 它也會指出**transaction_sequence_num**，或**first_snapshot_sequence_num**中的資料行[sys.dm_tran_active_snapshot_database_transactions](../../relational-databases/system-dynamic-management-views/sys-dm-tran-active-snapshot-database-transactions-transact-sql.md)動態管理檢視會包含 15 的值。 如果有任一個**transaction_sequence_num**，或**first_snapshot_sequence_num**檢視中的資料行包含數字，其低於最後一個交易 (109)，壓縮作業所完成壓縮作業將會等到這些交易完成。
  
若要解決這個問題，可以執行下列其中一項工作：
-   結束正在封鎖壓縮作業的交易。
-   結束壓縮作業。 如果結束壓縮作業，則所有已完成的工作都會保留。  
-   不執行任何動作，並允許壓縮作業等到封鎖交易完成。  
  
## <a name="permissions"></a>Permissions  
需要 **系統管理員** 固定伺服器角色或 **db_owner** 固定資料庫角色中的成員資格。
  
## <a name="examples"></a>範例  
  
### <a name="a-shrinking-a-data-file-to-a-specified-target-size"></a>A. 將資料檔案壓縮為指定的目標大小  
下列範例會壓縮名為的資料檔案的大小`DataFile1`中`UserDB`成 7 MB 的使用者資料庫。
  
```sql  
USE UserDB;  
GO  
DBCC SHRINKFILE (DataFile1, 7);  
GO  
```  
  
### <a name="b-shrinking-a-log-file-to-a-specified-target-size"></a>B. 將記錄檔壓縮為指定的目標大小  
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
下列範例示範清除檔案，使其能從資料庫中移除的程序。 在此範例中會先建立一個資料檔案，然後假設該檔案包含資料。
  
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
[FILE_ID &#40;TRANSACT-SQL &#41;](../../t-sql/functions/file-id-transact-sql.md)  
[sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)  
[壓縮檔案](../../relational-databases/databases/shrink-a-file.md)
  
  

