---
title: "ALTER DATABASE File and Filegroup Options (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 08/07/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ADD FILE
- ADD_FILE_TSQL
dev_langs: TSQL
helpviewer_keywords:
- deleting files
- removing files
- deleting filegroups
- file modifications [SQL Server]
- databases [SQL Server], size
- relocating files
- databases [SQL Server], modifying
- file additions [SQL Server], ALTER DATABASE
- file moving [SQL Server]
- default filegroups
- ALTER DATABASE statement, files and filegroups
- initializing files [SQL Server]
- database files [SQL Server]
- moving files
- filegroups [SQL Server], deleting
- adding filegroups
- adding files
- database filegroups [SQL Server]
- adding log files
- modifying files
- filegroups [SQL Server], adding
- file initialization [SQL Server]
- files [SQL Server], deleting
- files [SQL Server], adding
- databases [SQL Server], moving
ms.assetid: 1f635762-f7aa-4241-9b7a-b51b22292b07
caps.latest.revision: "61"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 0672b00cbb7064bdb889908585b4333865ac75c9
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="alter-database-transact-sql-file-and-filegroup-options"></a>ALTER DATABASE (TRANSACT-SQL) 檔案及檔案群組選項 
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  修改與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫相關聯的檔案和檔案群組。 在資料庫中新增或移除檔案和檔案群組，以及變更資料庫或其檔案和檔案群組的屬性。 如需其他 ALTER DATABASE 選項，請參閱[ALTER DATABASE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
ALTER DATABASE database_name   
{  
    <add_or_modify_files>  
  | <add_or_modify_filegroups>  
}  
[;]  
  
<add_or_modify_files>::=  
{  
    ADD FILE <filespec> [ ,...n ]   
        [ TO FILEGROUP { filegroup_name } ]  
  | ADD LOG FILE <filespec> [ ,...n ]   
  | REMOVE FILE logical_file_name   
  | MODIFY FILE <filespec>  
}  
  
<filespec>::=   
(  
    NAME = logical_file_name    
    [ , NEWNAME = new_logical_name ]   
    [ , FILENAME = {'os_file_name' | 'filestream_path' | 'memory_optimized_data_path' } ]   
    [ , SIZE = size [ KB | MB | GB | TB ] ]   
    [ , MAXSIZE = { max_size [ KB | MB | GB | TB ] | UNLIMITED } ]   
    [ , FILEGROWTH = growth_increment [ KB | MB | GB | TB| % ] ]   
    [ , OFFLINE ]  
)   
  
<add_or_modify_filegroups>::=  
{  
    | ADD FILEGROUP filegroup_name   
        [ CONTAINS FILESTREAM | CONTAINS MEMORY_OPTIMIZED_DATA ]  
    | REMOVE FILEGROUP filegroup_name   
    | MODIFY FILEGROUP filegroup_name  
        { <filegroup_updatability_option>  
        | DEFAULT  
        | NAME = new_filegroup_name   
        | { AUTOGROW_SINGLE_FILE | AUTOGROW_ALL_FILES }  
        }  
}  
<filegroup_updatability_option>::=  
{  
    { READONLY | READWRITE }   
    | { READ_ONLY | READ_WRITE }  
}  
  
```  
  
## <a name="arguments"></a>引數  
**\<add_or_modify_files >:: =**
  
 指定要新增、移除或修改的檔案。  
  
 *database_name*  
 這是要修改之資料庫的名稱。  
  
 ADD FILE  
 將檔案加入資料庫中。  
  
 至檔案群組 { *filegroup_name* }  
 指定要加入指定之檔案的檔案群組。 若要顯示目前的檔案群組和哪個檔案群組是目前的預設值，請使用[sys.filegroups](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)目錄檢視。  
  
 ADD LOG FILE  
 將記錄檔加入指定的資料庫中。  
  
 REMOVE FILE*邏輯檔案名稱*  
 從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中移除邏輯檔案描述和刪除實體檔案。 除非檔案是空的，否則無法移除檔案。  
  
 *邏輯檔案名稱*  
 這是在參考檔案時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所用的邏輯名稱。  
  
> [!WARNING]  
>  移除資料庫檔案具有 FILE_SNAPSHOT 與其相關聯的備份將會成功，但不是會刪除任何相關聯的快照集以避免使無效參考資料庫檔案的備份。 檔案將會被截斷，但不是會實際刪除為了 FILE_SNAPSHOT 備份的保留不變。 如需詳細資訊，請參閱 [使用 Microsoft Azure Blob 儲存體服務進行 SQL Server 備份及還原](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)。 **適用於**:[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]透過[新版](http://go.microsoft.com/fwlink/p/?LinkId=299658)。  
  
 MODIFY FILE  
 指定應該修改的檔案。 只有一個\<filespec > 屬性可以變更一次。 名稱必須一律在中指定\<filespec > 來指定要修改的檔案。 如果指定了 SIZE，新的大小必須大於目前檔案大小。  
  
 若要修改資料檔或記錄檔的邏輯名稱，請在 `NAME` 子句中指定要重新命名的邏輯檔案名稱，並在 `NEWNAME` 子句中指定檔案的新邏輯名稱。 例如：  
  
```  
MODIFY FILE ( NAME = logical_file_name, NEWNAME = new_logical_name )   
```  
  
 若要將資料檔或記錄檔移至新的位置，請在 `NAME` 子句中指定目前的邏輯檔案名稱，並在 `FILENAME` 子句中指定新的路徑和作業系統檔案名稱。 例如：  
  
```  
MODIFY FILE ( NAME = logical_file_name, FILENAME = ' new_path/os_file_name ' )  
```  
  
 當您移動全文檢索目錄時，只能在 FILENAME 子句中指定新的路徑。 請勿指定作業系統檔案名稱。  
  
 如需詳細資訊，請參閱[移動資料庫檔案](../../relational-databases/databases/move-database-files.md)。  
  
 如果是 FILESTREAM 檔案群組，可以在線上修改 NAME。 可以在線上修改 FILENAME；但是，要等到實際重新放置容器且伺服器關閉並重新啟動之後，變更才會生效。  
  
 您可以將 FILESTREAM 檔案設定為 OFFLINE。 當 FILESTREAM 檔案離線時，它的父檔案群組會在內部標示為離線；因此，該檔案群組內 FILESTREAM 資料的所有存取都將失敗。  
  
> [!NOTE]  
>  \<add_or_modify_files > 不包含資料庫中可用選項。
  
 **\<filespec >:: =**  
  
 控制檔案屬性。  
  
 名稱*邏輯檔案名稱*  
 指定檔案的邏輯名稱。  
  
 *邏輯檔案名稱*  
 這是在參考檔案時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體所用的邏輯名稱。  
  
 NEWNAME *new_logical_file_name*  
 指定檔案的新邏輯名稱。  
  
 *new_logical_file_name*  
 這是要取代現有邏輯檔案名稱的名稱。 名稱必須在資料庫內是唯一的且必須符合的規則[識別碼](../../relational-databases/databases/database-identifiers.md)。 這個名稱可以是字元或 Unicode 常數、正規識別碼，或分隔的識別碼。  
  
 檔名 { **'***os_file_name***'** | **'***filestream_path* **'** | **'***memory_optimized_data_path***'**}  
 指定作業系統 (實體) 檔案名稱。  
  
 ' *os_file_name* '  
 如果是標準 (ROWS) 檔案群組，這就是當您建立檔案時，作業系統所用的路徑和檔案名稱。 這個檔案必須在安裝了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的伺服器中。 在執行 ALTER DATABASE 陳述式之前，指定的路徑必須已經存在。  
  
 當指定檔案的 UNC 路徑時，無法設定 SIZE、MAXSIZE 和 FILEGROWTH 參數。  
  
> [!NOTE]  
>  系統資料庫無法位於 UNC 共用目錄。  
  
 除非檔案是唯讀的次要檔案，或資料庫是唯讀的，否則，不應將資料檔放在壓縮的檔案系統中。 記錄檔永遠不應放在壓縮的檔案系統中。  
  
 如果檔案在原始的分割區， *os_file_name*必須指定只有現有的未經處理資料分割的磁碟機代號。 每個原始分割區只能放置一個檔案。  
  
 **'** *filestream_path* **'**  
 如果是 FILESTREAM 檔案群組，FILENAME 會參考儲存 FILESTREAM 資料所在的路徑。 到最後一個資料夾為止的路徑必須存在，而最後一個資料夾則不得存在。 例如，如果您指定 C:\MyFiles\MyFilestreamData 路徑，則在您執行 ALTER DATABASE 之前，C:\MyFiles 必須存在，但是 MyFilestreamData 資料夾不得存在。  
  
 SIZE 和 FILEGROWTH 屬性不會套用到 FILESTREAM 檔案群組。  
  
 **'** *memory_optimized_data_path* **'**  
 如果是記憶體最佳化的檔案群組，FILENAME 會參考將儲存記憶體最佳化資料的路徑。 到最後一個資料夾為止的路徑必須存在，而最後一個資料夾則不得存在。 例如，如果您指定 C:\MyFiles\MyData 路徑，則在您執行 ALTER DATABASE 之前，C:\MyFiles 必須存在，但是 MyData 資料夾不得存在。  
  
 檔案群組和檔案 (`<filespec>`) 必須在相同的陳述式中建立。  
  
 SIZE、MAXSIZE 和 FILEGROWTH 屬性不會套用到記憶體最佳化的檔案群組。  
  
 大小*大小*  
 指定檔案大小。 SIZE 不會套用到 FILESTREAM 檔案群組。  
  
 *大小*  
 這是檔案的大小。  
  
 當指定的 ADD FILE，*大小*是檔案初始大小。 修改檔案，以指定時*大小*是新檔案的大小，而且必須大於目前的檔案大小。  
  
 當*大小*未提供主要檔案，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用中主要檔案的大小**模型**資料庫。 當指定了次要資料檔或記錄檔，但*大小*檔案，未指定[!INCLUDE[ssDE](../../includes/ssde-md.md)]能檔案 1 MB。  
  
 您可以利用 KB、MB、GB 和 TB 後置詞來指定千位元組、百萬位元組、十億位元組或兆位元組。 預設值是 MB。 請指定不包括小數的整數。 若要指定 MB 的小數，請將數字乘以 1024，以便將值轉換成 KB。 例如，請指定 1536 KB，而不要指定 1.5 MB (1.5 x 1024 = 1536)。  
  
 MAXSIZE { *max_size*|無限制}  
 指定檔案所能成長的大小上限。  
  
 *max_size*  
 這是檔案大小上限。 您可以利用 KB、MB、GB 和 TB 後置詞來指定千位元組、百萬位元組、十億位元組或兆位元組。 預設值是 MB。 請指定不包括小數的整數。 如果*max_size*未指定，檔案大小會增加，直到磁碟已滿。  
  
 UNLIMITED  
 指定檔案可成長直到磁碟已滿。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，指定為無限成長的記錄檔，大小上限是 2 TB，資料檔案的大小上限是 16 TB。 為 FILESTREAM 容器指定這個選項時沒有最大大小。 它會繼續成長，直到磁碟已滿。  
  
 FILEGROWTH *growth_increment*  
 指定檔案的自動成長遞增。 檔案的 FILEGROWTH 設定不能超過 MAXSIZE 設定。 FILEGROWTH 不會套用到 FILESTREAM 檔案群組。  
  
 *growth_increment*  
 這是每次需要新空間時，檔案所增加的空間量。  
  
 您可以利用 MB、KB、GB、TB 或百分比 (%) 來指定這個值。 如果指定的數字不含 MB、KB 或 % 後置詞，預設值是 MB。 當指定 % 時，成長遞增大小便是遞增發生時，檔案大小的指定百分比。 指定的大小會捨入到最接近 64 KB。  
  
 0 值表示將自動成長設為關閉，且不允許任何其他空間。  
  
 如果未指定 FILEGROWTH，預設值為：  
  
|Version|預設值|  
|-------------|--------------------|  
|開頭[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|資料 64 MB。 記錄檔 64 MB。|  
|開頭[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|資料 1 MB。 記錄檔以 10%。|  
|之前[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|資料 10%。 記錄檔以 10%。|  
  
 OFFLINE  
 將檔案設成離線，使檔案群組中的所有物件都無法存取。  
  
> [!CAUTION]  
>  請只在檔案損毀且可以還原時，才使用這個選項。 設為 OFFLINE 的檔案，只能藉由從備份中還原檔案來設成線上狀態。 如需有關還原單一檔案的詳細資訊，請參閱 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)。  
  
> [!NOTE]  
>  \<filespec > 不包含資料庫中可用選項。  
  
 **\<add_or_modify_filegroups >:: =**  
  
 在資料庫中新增、修改或移除檔案群組。  
  
 加入檔案群組*filegroup_name*  
 將檔案群組加入資料庫中。  
  
 CONTAINS FILESTREAM  
 指定檔案群組會將 FILESTREAM 二進位大型物件 (BLOB) 儲存在檔案系統中。  
  
 CONTAINS MEMORY_OPTIMIZED_DATA  

**適用於**:[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 指定檔案群組將記憶體最佳化的資料儲存在檔案系統中。 如需詳細資訊，請參閱[記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)。 每個資料庫只允許一個 MEMORY_OPTIMIZED_DATA 檔案群組。 若要建立記憶體最佳化的資料表，檔案群組不能空白。 至少必須有一個檔案。 *filegroup_name*參考的路徑。 到最後一個資料夾為止的路徑必須存在，而最後一個資料夾則不得存在。  
  
 下列範例會建立檔案群組並將其加入至名為 xtp_db 的資料庫中，然後將檔案加入檔案群組中。 檔案群組儲存記憶體最佳化的資料。  
  
```  
ALTER DATABASE xtp_db ADD FILEGROUP xtp_fg CONTAINS MEMORY_OPTIMIZED_DATA;  
GO  
ALTER DATABASE xtp_db ADD FILE (NAME='xtp_mod', FILENAME='d:\data\xtp_mod') TO FILEGROUP xtp_fg;  
```  
  
 移除檔案群組*filegroup_name*  
 從資料庫中移除檔案群組。 除非檔案群組是空的，否則無法移除檔案群組。 請先移除檔案群組中的所有檔案。 如需詳細資訊，請參閱 「 移除檔案*邏輯檔案名稱*，「 本主題較前面。  
  
> [!NOTE]  
>  除非 FILESTREAM 記憶體回收行程已移除 FILESTREAM 容器中的所有檔案，否則移除 FILESTREAM 容器的 ALTER DATABASE REMOVE FILE 作業會失敗並傳回錯誤訊息。 請參閱本主題後面的＜備註＞中的＜移除 FILESTREAM 容器＞一節。  
  
修改檔案群組*filegroup_name* { \<filegroup_updatability_option > |預設 |名稱 **=**  *new_filegroup_name* } 修改檔案群組的狀態設為 READ_ONLY 或 READ_WRITE，使檔案群組的預設檔案群組的資料庫，或變更檔案群組名稱。  
  
 \<filegroup_updatability_option >  
 將檔案群組的屬性設成唯讀或讀取/寫入。  
  
 DEFAULT  
 變更預設的資料庫檔案群組到*filegroup_name*。 資料庫中只能有一個檔案群組是預設檔案群組。 如需相關資訊，請參閱 [Database Files and Filegroups](../../relational-databases/databases/database-files-and-filegroups.md)。  
  
 名稱 = *new_filegroup_name*  
 變更檔案群組名稱*new_filegroup_name*。  
  
 AUTOGROW_SINGLE_FILE  
**適用於**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]透過[新版](http://go.microsoft.com/fwlink/p/?LinkId=299658))
  
 當群組中的檔案符合自動成長臨界值時，只有該檔案會成長。 這是預設值。  
  
 AUTOGROW_ALL_FILES  

**適用於**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]透過[新版](http://go.microsoft.com/fwlink/p/?LinkId=299658))
  
 檔案群組中的檔案已到達的自動成長臨界值時的檔案群組中的所有檔案會都成長。  
  
 **\<filegroup_updatability_option >:: =**  
  
 將檔案群組的屬性設成唯讀或讀取/寫入。  
  
 READ_ONLY | READONLY  
 將檔案群組指定成唯讀狀態。 不允許更新其中的物件。 主要檔案群組不能設為唯讀。 若要變更這個狀態，您必須具有資料庫的獨佔存取權。 如需詳細資訊，請參閱 SINGLE_USER 子句。  
  
 由於唯讀資料庫不允許修改資料，因此，會出現下列情況：  
  
-   在系統開機時跳過自動復原。  
  
-   不可能壓縮資料庫。  
  
-   唯讀資料庫不會出現鎖定。 因此，查詢效能會比較快。  
  
> [!NOTE]  
>  未來版本將移除 READONLY 關鍵字[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 請避免在新的開發工作中使用 READONLY，並規劃修改目前在使用 READONLY 的應用程式。 請改用 READ_ONLY。  
  
 READ_WRITE | READWRITE  
 將群組指定成 READ_WRITE 狀態。 檔案群組中的物件可以更新。 若要變更這個狀態，您必須具有資料庫的獨佔存取權。 如需詳細資訊，請參閱 SINGLE_USER 子句。  
  
> [!NOTE]  
>  未來版本將移除 READWRITE 關鍵字[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 請避免在新的開發工作中使用 READWRITE，並規劃修改目前在使用 READWRITE 的應用程式。 請改用 READ_WRITE。  
  
 可以判斷這些選項的狀態，藉由檢查**is_read_only**中的資料行**sys.databases**目錄檢視或**可更新性**屬性DATABASEPROPERTYEX 函式。  
  
## <a name="remarks"></a>備註  
 若要減少資料庫大小，請使用[DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md)。  
  
 當 BACKUP 陳述式在執行中，您不能新增或移除檔案。  
  
 每個資料庫最多可以指定 32,767 個檔案和 32,767 個檔案群組。  
  
 在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更新版本中，資料庫檔案狀態 (如線上或離線) 的維護與資料庫狀態無關。 如需詳細資訊，請參閱[檔案狀態](../../relational-databases/databases/file-states.md)。 檔案群組內的檔案狀態決定了整個檔案群組的可用性。 若要使某個檔案群組為可用的，則在檔案群組中的所有檔案必須都在線上。 如果檔案群組離線，SQL 陳述式存取檔案群組的任何嘗試都會失敗，且會出現錯誤。 當您建置 SELECT 陳述式的查詢計劃時，查詢最佳化工具會避開在離線檔案群組中的非叢集索引和索引檢視表。 這樣會讓這些陳述式能夠執行成功。 不過，如果離線檔案群組包含目標資料表的堆積或叢集索引，SELECT 陳述式將會失敗。 除此之外，在離線檔案群組中，以 INSERT、UPDATE 或 DELETE 陳述式修改含有索引的資料表將會失敗。  
  
## <a name="moving-files"></a>移動檔案  
 您可以在 FILENAME 中指定新位置來移動系統或使用者定義資料檔和記錄檔。 在下列狀況中，這非常有用：  
  
-   失敗復原。 例如，資料庫處於可疑模式或硬體故障所造成的關閉。  
  
-   計畫的重新放置  
  
-   排程的磁碟維護重新放置  
  
 如需詳細資訊，請參閱[移動資料庫檔案](../../relational-databases/databases/move-database-files.md)。  
  
## <a name="initializing-files"></a>初始化檔案  
 依預設，資料檔和記錄檔初始化的方式是在您執行下列作業之一時，在檔案中填入 0：  
  
-   建立資料庫  
  
-   將檔案加入現有的資料庫  
  
-   增加現有檔案的大小  
  
-   還原資料庫或檔案群組  
  
 資料檔可以立即初始化。 這可以加快這些檔案作業的執行速度。  
  
## <a name="removing-a-filestream-container"></a>移除 FILESTREAM 容器  
 即使 FILESTREAM 容器已使用 "DBCC SHRINKFILE" 作業來清空，基於各種系統維護原因，資料庫可能仍然需要維護已刪除之檔案的參考。 [s &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-filestream-force-garbage-collection.md)會執行 FILESTREAM 記憶體回收行程來移除這些檔案時，則若要這樣做。 除非 FILESTREAM 記憶體回收行程已移除 FILESTREAM 容器中的所有檔案，否則移除 FILESTREAM 容器的 ALTER DATABASE REMOVE FILE 作業會失敗並傳回錯誤訊息。 以下是移除 FILESTREAM 容器的建議處理序。  
  
1.  執行[DBCC SHRINKFILE &#40;TRANSACT-SQL &#41;](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md)具有 EMPTYFILE 選項，將此容器中的作用中內容移至其他容器。  
  
2.  確定已透過 FULL 或 BULK_LOGGED 復原模式建立記錄備份。  
  
3.  確定已執行複寫記錄讀取器作業 (如果相關)。  
  
4.  執行[s &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-filestream-force-garbage-collection.md)若要強制記憶體回收行程，刪除不再需要此容器中的任何檔案。  
  
5.  執行 ALTER DATABASE 搭配 REMOVE FILE 選項，移除這個容器。  
  
6.  再次重複步驟 2 到 4，以完成記憶體回收。  
  
7.  使用 ALTER Database...REMOVE FILE 移除此容器。  
  
## <a name="examples"></a>範例  
  
### <a name="a-adding-a-file-to-a-database"></a>A. 將檔案加入資料庫中  
 下列範例會將 5 MB 的資料檔加入 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫中。  
  
```  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012   
ADD FILE   
(  
    NAME = Test1dat2,  
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\t1dat2.ndf',  
    SIZE = 5MB,  
    MAXSIZE = 100MB,  
    FILEGROWTH = 5MB  
);  
GO  
  
```  
  
### <a name="b-adding-a-filegroup-with-two-files-to-a-database"></a>B. 將含有兩個檔案的檔案群組加入資料庫中  
 下列範例會在 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫中建立 `Test1FG1` 檔案群組，且會將兩個 5 MB 的檔案加入檔案群組中。  
  
```  
USE master  
GO  
ALTER DATABASE AdventureWorks2012  
ADD FILEGROUP Test1FG1;  
GO  
ALTER DATABASE AdventureWorks2012   
ADD FILE   
(  
    NAME = test1dat3,  
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\t1dat3.ndf',  
    SIZE = 5MB,  
    MAXSIZE = 100MB,  
    FILEGROWTH = 5MB  
),  
(  
    NAME = test1dat4,  
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\t1dat4.ndf',  
    SIZE = 5MB,  
    MAXSIZE = 100MB,  
    FILEGROWTH = 5MB  
)  
TO FILEGROUP Test1FG1;  
GO  
  
```  
  
### <a name="c-adding-two-log-files-to-a-database"></a>C. 將兩個記錄檔加入資料庫中  
 下列範例會將兩個 5 MB 的記錄檔加入 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫中。  
  
```  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012   
ADD LOG FILE   
(  
    NAME = test1log2,  
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\test2log.ldf',  
    SIZE = 5MB,  
    MAXSIZE = 100MB,  
    FILEGROWTH = 5MB  
),  
(  
    NAME = test1log3,  
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL10_50.MSSQLSERVER\MSSQL\DATA\test3log.ldf',  
    SIZE = 5MB,  
    MAXSIZE = 100MB,  
    FILEGROWTH = 5MB  
);  
GO  
  
```  
  
### <a name="d-removing-a-file-from-a-database"></a>D. 從資料庫中移除檔案  
 下列範例會移除 B 範例中所加入的其中一個檔案。  
  
```  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
REMOVE FILE test1dat4;  
GO  
  
```  
  
### <a name="e-modifying-a-file"></a>E. 修改檔案  
下列範例會增加 B 範例中所加入的其中一個檔案的大小。  
 ALTER DATABASE MODIFY FILE 命令可以只提供檔案大小變大，因此如果您要讓檔案大小變小，您必須使用 DBCC SHRINKFILE。  
  
```  
USE master;  
GO
  
ALTER DATABASE AdventureWorks2012   
MODIFY FILE  
(NAME = test1dat3,  
SIZE = 200MB);  
GO  
```

這個範例會壓縮資料檔大小為 100 MB，，然後再指定在該數量的大小。 

```
USE AdventureWorks2012;
GO

DBCC SHRINKFILE (AdventureWorks2012_data, 100);
GO

USE master;  
GO
  
ALTER DATABASE AdventureWorks2012   
MODIFY FILE  
(NAME = test1dat3,  
SIZE = 200MB);  
GO
```
 
  
### <a name="f-moving-a-file-to-a-new-location"></a>F. 將檔案移到新位置  
 下列範例會將 A 範例中所建立的 `Test1dat2` 檔移至新目錄中。  
  
> [!NOTE]  
>  您必須實際上將檔案移到新目錄之後，才能執行這個範例。 之後，請停止再啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體，或使 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫離線 (OFFLINE) 再連接 (ONLINE) 來實作變更。  
  
```  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
MODIFY FILE  
(  
    NAME = Test1dat2,  
    FILENAME = N'c:\t1dat2.ndf'  
);  
GO  
```  
  
### <a name="g-moving-tempdb-to-a-new-location"></a>G. 將 tempdb 移到新位置  
 下列範例會將 `tempdb` 從磁碟中目前的位置移到另一個磁碟位置。 由於在每次啟動 MSSQLSERVER 服務時都會重新建立 `tempdb`，因此您不需要實際移動資料和記錄檔。 在步驟 3 重新啟動此服務時，將會建立檔案。 在重新啟動此服務之前，`tempdb` 會繼續在現有的位置運作。  
  
1.  決定 `tempdb` 資料庫的邏輯檔案名稱，及它們目前在磁碟中的位置。  
  
    ```  
    SELECT name, physical_name  
    FROM sys.master_files  
    WHERE database_id = DB_ID('tempdb');  
    GO  
    ```  
  
2.  請利用 `ALTER DATABASE`來變更每個檔案的位置。  
  
    ```  
    USE master;  
    GO  
    ALTER DATABASE tempdb   
    MODIFY FILE (NAME = tempdev, FILENAME = 'E:\SQLData\tempdb.mdf');  
    GO  
    ALTER DATABASE  tempdb   
    MODIFY FILE (NAME = templog, FILENAME = 'E:\SQLData\templog.ldf');  
    GO  
    ```  
  
3.  停止和重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體。  
  
4.  確認檔案變更。  
  
    ```  
    SELECT name, physical_name  
    FROM sys.master_files  
    WHERE database_id = DB_ID('tempdb');  
    ```  
  
5.  將 tempdb.mdf 和 templog.ldf 檔案從它們的原始位置刪除。  
  
### <a name="h-making-a-filegroup-the-default"></a>H. 使檔案群組成為預設值  
 下列範例使`Test1FG1`B 範例中建立檔案群組的預設檔案群組。 之後，預設檔案群組會重設為 `PRIMARY` 檔案群組。 請注意，您必須用方括號或引號來分隔 `PRIMARY`。  
  
```  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012   
MODIFY FILEGROUP Test1FG1 DEFAULT;  
GO  
ALTER DATABASE AdventureWorks2012   
MODIFY FILEGROUP [PRIMARY] DEFAULT;  
GO  
  
```  
  
### <a name="i-adding-a-filegroup-using-alter-database"></a>I. 使用 ALTER DATABASE 加入檔案群組  
 下列範例會將包含 `FILEGROUP` 子句的 `FILESTREAM` 加入 `FileStreamPhotoDB` 資料庫。  
  
```  
--Create and add a FILEGROUP that CONTAINS the FILESTREAM clause to  
--the FileStreamPhotoDB database.  
ALTER DATABASE FileStreamPhotoDB  
ADD FILEGROUP TodaysPhotoShoot  
CONTAINS FILESTREAM;  
GO  
  
--Add a file for storing database photos to FILEGROUP   
ALTER DATABASE FileStreamPhotoDB  
ADD FILE  
(  
    NAME= 'PhotoShoot1',  
    FILENAME = 'C:\Users\Administrator\Pictures\TodaysPhotoShoot.ndf'  
)  
TO FILEGROUP TodaysPhotoShoot;  
GO  
```      
        
### <a name="j-change-filegroup-so-that-when-a-file-in-the-filegroup-meets-the-autogrow-threshold-all-files-in-the-filegroup-grow"></a>J. 使檔案群組中的所有檔案都成長的檔案群組中的檔案已到達的自動成長臨界值時，請變更檔案群組
 下列範例會產生所需`ALTER DATABASE`陳述式以修改具有讀寫檔案群組`AUTOGROW_ALL_FILES`設定。  
  
```  
--Generate ALTER DATABASE ... MODIFY FILEGROUP statements  
--so that all read-write filegroups grow at the same time.  
SET NOCOUNT ON;

DROP TABLE IF EXISTS #tmpdbs
CREATE TABLE #tmpdbs (id int IDENTITY(1,1), [dbid] int, [dbname] sysname, isdone bit);

DROP TABLE IF EXISTS #tmpfgs
CREATE TABLE #tmpfgs (id int IDENTITY(1,1), [dbid] int, [dbname] sysname, fgname sysname, isdone bit);

INSERT INTO #tmpdbs ([dbid], [dbname], [isdone])
SELECT database_id, name, 0 FROM master.sys.databases (NOLOCK) WHERE is_read_only = 0 AND state = 0;

DECLARE @dbid int, @query VARCHAR(1000), @dbname sysname, @fgname sysname

WHILE (SELECT COUNT(id) FROM #tmpdbs WHERE isdone = 0) > 0
BEGIN
    SELECT TOP 1 @dbname = [dbname], @dbid = [dbid] FROM #tmpdbs WHERE isdone = 0

    SET @query = 'SELECT ' + CAST(@dbid AS NVARCHAR) + ', ''' + @dbname + ''', [name], 0 FROM [' + @dbname + '].sys.filegroups WHERE [type] = ''FG'' AND is_read_only = 0;'
    INSERT INTO #tmpfgs
    EXEC (@query)

    UPDATE #tmpdbs
    SET isdone = 1
    WHERE [dbid] = @dbid
END;

IF (SELECT COUNT(ID) FROM #tmpfgs) > 0
BEGIN
    WHILE (SELECT COUNT(id) FROM #tmpfgs WHERE isdone = 0) > 0
    BEGIN
        SELECT TOP 1 @dbname = [dbname], @dbid = [dbid], @fgname = fgname FROM #tmpfgs WHERE isdone = 0

        SET @query = 'ALTER DATABASE [' + @dbname + '] MODIFY FILEGROUP [' + @fgname + '] AUTOGROW_ALL_FILES;'

        PRINT @query

        UPDATE #tmpfgs
        SET isdone = 1
        WHERE [dbid] = @dbid AND fgname = @fgname
    END
END; 
GO  
```      
  
## <a name="see-also"></a>請參閱＜  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md)   
 [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)   
 [sp_spaceused &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.data_spaces &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)   
 [sys.filegroups &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [sys.master_files &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
 [二進位大型物件 &#40;Blob&#41; 資料 &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)   
 [DBCC SHRINKFILE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md)   
 [sp_filestream_force_garbage_collection &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-filestream-force-garbage-collection.md)  
  
  
