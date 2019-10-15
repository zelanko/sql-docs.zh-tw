---
title: sp_lock （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_lock_TSQL
- sp_lock
dev_langs:
- TSQL
helpviewer_keywords:
- sp_lock
ms.assetid: 9eaa0ec2-2ad9-457c-ae48-8da92a03dcb0
author: stevestein
ms.author: sstein
ms.openlocfilehash: c31148d09621caf9fd2ebc83a9b629f320418995
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/14/2019
ms.locfileid: "72305121"
---
# <a name="sp_lock-transact-sql"></a>sp_lock (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  報告鎖定的相關資訊。  
  
> [!IMPORTANT]  
> [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 若要取得 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 中鎖定的相關資訊，請使用[_tran_locks](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)動態管理檢視。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
sp_lock [ [ @spid1 = ] 'session ID1' ] [ , [@spid2 = ] 'session ID2' ]  
[ ; ]  
```  
  
## <a name="arguments"></a>引數  
`[ @spid1 = ] 'session ID1'` 是使用者想要鎖定資訊之 **_exec_sessions**的 @no__t 1 會話識別碼。 *SESSION ID1*是**int** ，預設值是 Null。 執行**sp_who**以取得會話的相關處理資訊。 如果未指定*SESSION ID1* ，則會顯示所有鎖定的相關資訊。  
  
`[ @spid2 = ] 'session ID2'` 是 **_exec_sessions**的另一個 @no__t 1 會話識別碼，可能會有與*會話 ID1*相同的時間，以及使用者也想要提供資訊的鎖定。 *SESSION ID2*是**int** ，預設值是 Null。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功)  
  
## <a name="result-sets"></a>結果集  
 **Sp_lock**結果集會針對 **\@spid1**和 **@no__t 4spid2**參數中指定的會話所持有的每個鎖定，各包含一個資料列。 如果未指定 **\@spid1**或 **\@spid2** ，則結果集會報告 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 實例中目前作用中的所有會話的鎖定。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**spid**|**smallint**|要求鎖定之處理序的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 工作階段識別碼。|  
|**dbid**|**smallint**|保留鎖定之資料庫的識別碼。 您可以利用 DB_NAME() 函數來識別資料庫。|  
|**ObjId**|**int**|保留鎖定之物件的識別碼。 您可以在相關資料庫中，利用 OBJECT_NAME() 函數來識別物件。 99 這個值是一個特殊情況，表示用來記錄資料庫頁面配置之某系統頁面的鎖定。|  
|**IndId**|**smallint**|保留鎖定之索引的識別碼。|  
|**型別**|**nchar(4)**|鎖定類型：<br /><br /> RID = 鎖定資料表中資料列識別碼 (RID) 所識別的單一資料列。<br /><br /> KEY = 在索引內鎖定，用來保護可序列化交易中的某個索引鍵範圍。<br /><br /> PAG = 鎖定資料或索引頁面。<br /><br /> EXT = 鎖定範圍。<br /><br /> TAB = 鎖定整份資料表，其中包括所有資料和索引。<br /><br /> DB = 鎖定資料庫。<br /><br /> FIL = 鎖定資料庫檔案。<br /><br /> APP = 鎖定應用程式指定資源。<br /><br /> MD = 鎖定中繼資料或目錄資訊。<br /><br /> HBT = 鎖定堆積或 B 型樹狀目錄（HoBT）。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的這項資訊並不完整。<br /><br /> AU = 鎖定配置單位。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的這項資訊並不完整。|  
|**Resource**|**nchar(32)**|用來識別鎖定資源的值。 值的格式取決於 [**類型**] 資料行中所識別的資源類型：<br /><br /> **類型**Value**資源**Value<br /><br /> 掉格式為 fileid： pagenumber： rid 的識別碼，其中 fileid 會識別包含該頁面的檔案，pagenumber 可識別包含該資料列的頁面，而 rid 則識別頁面上的特定資料列。 fileid 符合**database_files**目錄檢視中的**file_id**資料行。<br /><br /> 擊鍵@No__t-0 內部使用的十六進位數位。<br /><br /> PAG格式為 fileid： pagenumber 的數位，其中 fileid 會識別包含該頁面的檔案，而 pagenumber 則會識別該頁面。<br /><br /> 分機識別範圍中第一頁的數位。 這個號碼的格式為 fileid:pagenumber。<br /><br /> 標識未提供任何資訊，因為**ObjId**資料行中已經識別該資料表。<br /><br /> DB未提供任何資訊，因為**dbid**資料行中已識別資料庫。<br /><br /> FIL檔案的識別碼，該檔案符合**database_files**目錄檢視中的**file_id**資料行。<br /><br /> 相關要鎖定之應用程式資源的唯一識別碼。 格式為 DbPrincipleId： \<first 資源字串的2到16個字元 > \<hashed 值 >。<br /><br /> MD：隨資源類型而不同。 如需詳細資訊，請參閱[sys.databases _tran_locks &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)中**resource_description**資料行的描述。<br /><br /> HBT未提供任何資訊。 請改用 **_tran_locks**動態管理檢視。<br /><br /> 澳大利亞未提供任何資訊。 請改用 **_tran_locks**動態管理檢視。|  
|**模式**|**nvarchar(8)**|要求的鎖定模式。 可為以下項目：<br /><br /> NULL = 未授與資源的任何存取權。 這用來作為預留位置。<br /><br /> Sch-S = 結構描述穩定性。 確定在任何工作階段持有結構描述元素的結構描述穩定性鎖定時，不卸除結構描述元素，如資料表或索引。<br /><br /> Sch-M = 結構描述修改。 想要變更指定資源結構描述的任何工作階段都必須持有這個項目。 請確定沒有其他工作階段在參考指示的物件。<br /><br /> S = 共用。 持有它的工作階段，會取得資源的共用存取權。<br /><br /> U = 更新。 表示取得最終可能會更新之資源的更新鎖定。 它用來防止當多個工作階段為了後來可能更新資源而鎖定資源時，所常見的死結形式。<br /><br /> X = 獨佔。 持有它的工作階段，會取得資源的獨佔存取權。<br /><br /> IS = 意圖共用。 表示在鎖定階層中的某些從屬資源上設定 S 鎖定的意圖。<br /><br /> IU = 意圖更新。 表示在鎖定階層中的某些從屬資源上設定 U 鎖定的意圖。<br /><br /> IX = 意圖獨佔。 表示在鎖定階層中的某些從屬資源上設定 X 鎖定的意圖。<br /><br /> SIU = 共用意圖更新。 表示意圖取得鎖定階層中從屬資源的更新鎖定之共用資源存取權。<br /><br /> SIX = 共用意圖獨佔。 表示意圖取得鎖定階層中從屬資源的獨佔鎖定之共用資源存取權。<br /><br /> UIX = 更新意圖獨佔。 表示意圖取得鎖定階層中從屬資源的獨佔鎖定之資源更新鎖定。<br /><br /> BU = 大量更新。 供大量作業使用。<br /><br /> RangeS_S = 共用索引鍵範圍和共用資源鎖定。 指出可序列化的範圍掃描。<br /><br /> RangeS_U = 共用索引鍵範圍和更新資源鎖定。 指出可序列化的更新掃描。<br /><br /> RangeI_N = 插入索引鍵範圍和 Null 資源鎖定。 在將新索引鍵插入索引之前，用來測試範圍。<br /><br /> RangeI_S = 索引鍵範圍轉換鎖定。 這是重疊 RangeI_N 和 S 鎖定所建立。<br /><br /> RangeI_U = 重疊 RangeI_N 和 U 鎖定而建立的索引鍵範圍轉換鎖定。<br /><br /> RangeI_X = 重疊 RangeI_N 和 X 鎖定而建立的索引鍵範圍轉換鎖定。<br /><br /> RangeX_S = 重疊 RangeI_N 和 RangeS_S 鎖定建立的索引鍵範圍轉換鎖定。 。<br /><br /> RangeX_U = 重疊 RangeI_N 和 RangeS_U 鎖定而建立的索引鍵範圍轉換鎖定。<br /><br /> RangeX_X = 獨佔索引鍵範圍和獨佔資源鎖定。 這是更新範圍中的索引鍵時所用的轉換鎖定。|  
|**狀態**|**nvarchar(5)**|鎖定要求狀態：<br /><br /> CNVRT:正在從另一個模式轉換鎖定，但轉換被另一個持有衝突模式鎖定的進程封鎖。<br /><br /> 把已取得鎖定。<br /><br /> 等候鎖定已被另一個持有衝突模式鎖定的進程封鎖。|  
  
## <a name="remarks"></a>備註  
 使用者可以利用下列方式來控制讀取作業的鎖定：  
  
-   利用 SET TRANSACTION ISOLATION LEVEL 來指定工作階段的鎖定層級。 如需語法和限制，請參閱[SET TRANSACTION &#40;隔離等級 transact-sql&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)。  
  
-   利用鎖定資料表提示，在 FROM 子句中指定資料表之個別參考的鎖定層級。 如需語法和限制，請參閱[資料表提示&#40;transact-sql&#41;](../../t-sql/queries/hints-transact-sql-table.md)。  
  
 所有未關聯於工作階段的分散式交易都是被遺棄的交易。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會指派 -2 的 SPID 值給所有被遺棄的分散式交易，讓使用者更容易識別封鎖的分散式交易。 如需詳細資訊，請參閱 [使用標示的異動以一致的方式復原相關資料庫 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md)。  
  
## <a name="permissions"></a>Permissions  
 需要 VIEW SERVER STATE 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-listing-all-locks"></a>A. 列出所有鎖定  
 下列範例會顯示 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體目前保留之所有鎖定的相關資訊。  
  
```sql  
USE master;  
GO  
EXEC sp_lock;  
GO  
```  
  
### <a name="b-listing-a-lock-from-a-single-server-process"></a>B. 列出單一伺服器處理序的鎖定  
 下列範例會顯示處理序識別碼 `53` 的相關資訊，其中包括鎖定。  
  
```sql  
USE master;  
GO  
EXEC sp_lock 53;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sys.dm_tran_locks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)   
 [DB_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/db-name-transact-sql.md)   
 [KILL &#40;Transact-SQL&#41;](../../t-sql/language-elements/kill-transact-sql.md)   
 [OBJECT_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/object-name-transact-sql.md)   
 [sp_who &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.dm_os_tasks &#40;-SQL&AMP;&#41;&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md)   
 [sys.dm_os_threads &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-threads-transact-sql.md)  
  
  
