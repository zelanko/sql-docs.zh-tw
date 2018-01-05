---
title: "DBCC SHRINKDATABASE (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DBCC_SHRINKDATABASE_TSQL
- DBCC SHRINKDATABASE
- SHRINKDATABASE_TSQL
- SHRINKDATABASE
dev_langs: TSQL
helpviewer_keywords:
- data shrinking [SQL Server]
- shrinking files
- shrinking databases
- DBCC SHRINKDATABASE statement
- decreasing database size
- file shrinking [SQL Server]
- database shrinking [SQL Server]
- logs [SQL Server], shrinking
- reducing database size
ms.assetid: fc976afd-1edb-4341-bf41-c4a42a69772b
caps.latest.revision: "62"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 3a4ce958ed481b33f4785af2f0d7b32fb5baf519
ms.sourcegitcommit: 9b8c7883a6c5ba38b6393a9e05367fd66355d9a9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/04/2018
---
# <a name="dbcc-shrinkdatabase-transact-sql"></a>DBCC SHRINKDATABASE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

壓縮指定之資料庫中的資料和記錄檔大小。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
DBCC SHRINKDATABASE   
( database_name | database_id | 0   
     [ , target_percent ]   
     [ , { NOTRUNCATE | TRUNCATEONLY } ]   
)  
[ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>引數  
 *database_name* | *database_id* | 0  
 這是要壓縮之資料庫的名稱或識別碼。 如果指定 0，就會使用目前的資料庫。  
  
 *target_percent*  
 這是壓縮資料庫之後，資料庫檔案所要保留的可用空間百分比。  
  
 NOTRUNCATE  
 將配置的頁面從檔案結尾移到檔案前端的未配置頁面，壓縮資料檔案中的資料。 *target_percent*是選擇性的。 Azure SQL 資料倉儲不支援此選項。 
  
 檔案結尾的可用空間並不會還給作業系統，檔案的實際大小也不會改變。 因此，當指定了 NOTRUNCATE 時，資料庫不會呈現壓縮狀態。  
  
 NOTRUNCATE 只適用於資料檔案。 記錄檔不受影響。  
  
 TRUNCATEONLY  
 將檔案結尾的所有可用空間釋放給作業系統，但是不會在檔案內移動任何頁面。 資料檔案只會壓縮為最後配置的範圍。 *target_percent*如果指定了 truncateonly，便會被忽略。 Azure SQL 資料倉儲不支援此選項。
  
 TRUNCATEONLY 會影響記錄檔。 若要只能截斷資料檔案，請使用 DBCC SHRINKFILE。  
  
 WITH NO_INFOMSGS  
 抑制所有嚴重性層級在 0 到 10 的參考用訊息。  
  
## <a name="result-sets"></a>結果集  
下表描述結果集中的資料行。
  
|資料行名稱|描述|  
|-----------------|-----------------|  
|**DbId**|[!INCLUDE[ssDE](../../includes/ssde-md.md)] 試圖壓縮之檔案的資料庫識別碼。|  
|**FileId**|[!INCLUDE[ssDE](../../includes/ssde-md.md)] 試圖壓縮之檔案的識別碼。|  
|**CurrentSize**|檔案目前所佔的 8 KB 頁數。|  
|**MinimumSize**|檔案所能佔用的 8 KB 頁數最小值。 這對應於檔案的大小下限或最初建立的大小。|  
|**UsedPages**|檔案目前所用的 8 KB 頁數。|  
|**EstimatedPages**|[!INCLUDE[ssDE](../../includes/ssde-md.md)] 估計檔案可以壓縮成 8 KB 頁面的數目。|  
  
>[!NOTE]
> [!INCLUDE[ssDE](../../includes/ssde-md.md)] 不會顯示未壓縮之檔案的資料列。  
  
## <a name="remarks"></a>備註  
若要壓縮特定資料庫的所有資料和記錄檔，請執行 DBCC SHRINKDATABASE 命令。 若要壓縮資料或記錄檔的特定資料庫一次，執行[DBCC SHRINKFILE](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md)命令。
  
若要檢視資料庫目前的可用 （未配置） 空間量，執行[sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)。
  
在這個處理序中，隨時可以停止 DBCC SHRINKDATABASE 作業，任何已完成的工作都會保留下來。
  
資料庫的大小不得小於資料庫的大小下限。 大小下限是最初建立資料庫時所指定的大小，或是利用檔案大小變更作業 (例如 DBCC SHRINKFILE 或 ALTER DATABASE) 明確設定的最後大小。 例如，如果資料庫最初建立時為 10 MB 的大小，而後成長到 100 MB，則該資料庫最多只能縮小到 10 MB，即使該資料庫中的所有資料都已刪除，也是如此。
  
執行 DBCC SHRINKDATABASE 時若不指定 NOTRUNCATE 選項或 TRUNCATEONLY 選項，則與執行具有 NOTRUNCATE 選項的 DBCC SHRINKDATABASE 作業之後再執行具有 TRUNCATEONLY 選項的 DBCC SHRINKDATABASE 作業相等。
  
壓縮的資料庫不必是單一使用者模式；在資料庫壓縮之後，其他使用者也可以在這個資料庫中工作。 其中包括系統資料庫。
  
資料庫在備份時不能進行壓縮。 相反地，當資料庫上正在進行壓縮作業時，也不能對其進行備份。

>[!NOTE]
> 目前，Azure SQL 資料倉儲不支援 DBCC SHRINKDATABASE 與啟用 TDE。
  
## <a name="how-dbcc-shrinkdatabase-works"></a>DBCC SHRINKDATABASE 的運作方式  
DBCC SHRINKDATABASE 會以個別檔案為基礎來壓縮資料檔案，但會依照所有記錄檔都是在單一連續記錄集區的方式來壓縮記錄檔。 檔案必定從結尾處進行壓縮。
  
假設資料庫名為**mydb**使用資料的檔案和兩個記錄檔。 資料和記錄檔均為 10 MB，而資料檔包含 6 MB 的資料。
  
[!INCLUDE[ssDE](../../includes/ssde-md.md)] 會計算每個檔案的目標大小。 這是檔案所要壓縮的大小。 當 DBCC SHRINKDATABASE 指定*target_percent*、[!INCLUDE[ssDE](../../includes/ssde-md.md)]要將目標大小計算*target_percent*壓縮後檔案中的可用空間數量。 例如，如果您指定*target_percent*壓縮的 25 個**mydb**、[!INCLUDE[ssDE](../../includes/ssde-md.md)]計算為 8 MB （6 MB 資料加上 2 MB 的可用空間） 的資料檔案的目標大小。 因此，[!INCLUDE[ssDE](../../includes/ssde-md.md)]將從資料檔案最後 2 MB 的任何資料移至資料檔案前 8 MB 中任何可用的空間，然後再壓縮檔案。
  
假設資料檔案的**mydb**包含 7 MB 的資料。 指定*target_percent* 30，可以針對此資料檔案壓縮到可用百分比 30。 但是，指定*target_percent*為 40 並不壓縮資料檔，因為[!INCLUDE[ssDE](../../includes/ssde-md.md)]會將檔案壓縮到小於資料目前所佔的大小。 您也可以將此問題的另一個方法： 40%需要的可用空間 + 70%完整資料檔案 (超出 10 MB 的 7 MB) 已超過 100%。 因為可用百分比想要加上目前的資料檔案所佔的百分比超過 100%（以 10%)，任何*target_size*大於 30 都不會壓縮資料檔。
  
針對記錄檔，[!INCLUDE[ssDE](../../includes/ssde-md.md)]使用*target_percent*計算目標大小，整份記錄中; 因此， *target_percent*是壓縮作業後的記錄檔中的可用空間量。 之後，便會將整份記錄的目標大小轉換成每個記錄檔的目標大小。
  
DBCC SHRINKDATABASE 會試圖將每個實體記錄檔立即壓縮成目標大小。 如果邏輯記錄沒有任何部分是在超出記錄檔目標大小的虛擬記錄中，就會順利截斷檔案，DBCC SHRINKDATABASE 會完成作業，但沒有任何訊息。 不過，如果邏輯記錄有任何部分是在超出目標大小的虛擬記錄中，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 盡可能釋出的空間，然後發出一則參考用訊息。 這個訊息描述將邏輯記錄移出檔案結尾的虛擬記錄，需要哪些動作。 執行這些動作之後，就可以利用 DBCC SHRINKDATABASE 來釋出其餘空間。
  
由於記錄檔只能壓縮成虛擬記錄檔界限，因此，可能無法將記錄檔壓縮成小於虛擬記錄檔的大小，即使它不在使用中，也是如此。 建立或擴充記錄檔時，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 會動態選擇虛擬記錄檔的大小。
  
## <a name="best-practices"></a>最佳作法  
當您計畫壓縮資料庫時，請考量下列資訊：
-   壓縮作業在截斷資料表或卸除資料表等產生大量未用空間的作業之後最有效。  
-   大部分資料庫都需要一些可用空間來執行每天的例行作業。 如果您反覆壓縮資料庫，發現資料庫再次增長，就表示例行作業需要被壓縮的空間。 在這些情況之下，反覆壓縮資料庫是一項會造成浪費的作業。  
-   壓縮作業不會保留資料庫中索引的片段狀態，它通常會使片段增加到某個程度。 這就是不要反覆壓縮資料庫的另一個原因。  
-   除非您有特定的需求，否則請不要將 AUTO_SHRINK 資料庫選項設定為 ON。  
  
## <a name="troubleshooting"></a>疑難排解  
 封鎖交易下執行壓縮作業可能會[資料列版本設定為基礎的隔離等級](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)。 例如，當 DBCC SHRINK DATABASE 作業執行時，如果以資料列版本設定為基礎的隔離等級之下正在進行大量刪除作業，則壓縮作業將會等到刪除作業完成之後，才會開始壓縮檔案。 當這種情況發生時，DBCC SHRINKFILE 和 DBCC SHRINKDATABASE 作業在第一個小時裡，會每五分種列印一次參考用訊息 (SHRINKDATABASE 是 5202，SHRINKFILE 是 5203) 到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔中，之後則每小時列印一次。 例如，如果錯誤記錄檔包含下列的錯誤訊息：  
  
```sql
DBCC SHRINKDATABASE for database ID 9 is waiting for the snapshot   
transaction with timestamp 15 and other snapshot transactions linked to   
timestamp 15 or with timestamps older than 109 to finish.  
```  
  
這表示壓縮作業是由時間戳記在 109 (壓縮作業所完成的最後一項交易) 之前的快照集交易所封鎖。 它也會指出**transaction_sequence_num**，或**first_snapshot_sequence_num**中的資料行[sys.dm_tran_active_snapshot_database_transactions &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-active-snapshot-database-transactions-transact-sql.md)動態管理檢視會包含 15 的值。 如果有任一個**transaction_sequence_num**，或**first_snapshot_sequence_num**檢視中的資料行包含數字，其低於最後一個交易 (109)，壓縮作業所完成壓縮作業將會等到這些交易完成。
  
若要解決這個問題，可以執行下列其中一項工作：
-   結束正在封鎖壓縮作業的交易。  
-   結束壓縮作業。 所有已完成的工作都會保留。  
-   不執行任何動作，並允許壓縮作業等到封鎖交易完成。  
  
## <a name="permissions"></a>Permissions  
 需要 **系統管理員** 固定伺服器角色或 **db_owner** 固定資料庫角色中的成員資格。  
  
## <a name="examples"></a>範例  
  
### <a name="a-shrinking-a-database-and-specifying-a-percentage-of-free-space"></a>A. 壓縮資料庫並指定可用空間百分比  
 下列範例會縮小 `UserDB` 使用者資料庫中的資料和記錄檔大小，使資料庫中能有 10% 的可用空間。  
  
```sql  
DBCC SHRINKDATABASE (UserDB, 10);  
GO  
```  
  
### <a name="b-truncating-a-database"></a>B. 截斷資料庫  
 下列範例會將 `AdventureWorks` 範例資料庫中的資料檔案和記錄檔壓縮為最後配置的範圍。  
  
```sql  
DBCC SHRINKDATABASE (AdventureWorks2012, TRUNCATEONLY);  
```  
  
## <a name="see-also"></a>另請參閱  
[ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DBCC SHRINKFILE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md)  
[壓縮資料庫](../../relational-databases/databases/shrink-a-database.md)
  
  
